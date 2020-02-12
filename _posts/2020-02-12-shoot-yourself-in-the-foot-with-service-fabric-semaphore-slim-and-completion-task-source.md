---
title: "How to shoot yourself in the foot with Service Fabric, SemaphoreSlim and CompletionTaskSource"
date: 2020-02-12 +0200
categories: servicefabric semaphoreslim completiontasksource
---

**TL;DR;** Service Fabric partition swapping can have undesirable effects if you don't pay attention on how you use dependency injected objects in the two methods that fire up a reliable service (`RunAsync` and `CreateServiceReplicaListeners`). While using a `TaskCompletionSource` to ensure object availability between the two methods is a good idea, it should be used with care since it could leak objects reuse while partitions are swapping.

### The scenario

You want host a Service Fabric statefull service to build a queue that waits for items to come in and starts processing automatically when a new item was added.

### `RunAsync` and `CreateServiceReplicaListeners`

According to the [documentation](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-lifecycle#stateful-service-startup) when a stateful service starts:

> The following things happen in parallel:
> * StatefulServiceBase.CreateServiceReplicaListeners() is invoked.
> * If the service is currently a Primary, the service's StatefulServiceBase.RunAsync() method is called.

Because the order of execution between the two methods is unknown, one way of making sure that object instances registered in the dependency container via `CreateServiceReplicaListeners` are available in `RunAsync` would be to use a `TaskCompletionSouce`. 

The code for enabling the service listener from `CreateServiceReplicaListeners` could look like this (consider using my previous [quick start]({% post_url 2020-01-31-enable-aspnet-core-api-on-servicefabric-reliable-service-quick-start %}) as a starting point):

```csharp
...
new ServiceReplicaListener(serviceContext =>
	new KestrelCommunicationListener(serviceContext, (url, listener) =>
	{
		var host = 
			new WebHostBuilder()
				.UseKestrel()
				.ConfigureServices(
						services => services
							.AddSingleton<StatefulServiceContext>(serviceContext)
							.AddSingleton<IReliableStateManager>(this.StateManager)
							.AddSingleton<DemoQueue>())
				.UseContentRoot(Directory.GetCurrentDirectory())
				.UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
				.UseStartup<Startup>()
				.UseUrls(url)
				.Build();
		_demoQueueCompletionSource.TrySetResult(host.Services.GetService<DemoQueue>());
		return host;
	}))
...
```

Where the `_demoQueueCompletionSource` is just a private member of our service of type `TaskCompletionSource<DemoQueue>`. 
And then in `RunAsync` we can get hold of our `demoQueue` just awaiting the completion source task:

```csharp
protected override async Task RunAsync(CancellationToken token)
{
	var demoQueue = await _demoQueueCompletionSource.Task;
	while (!token.IsCancellationRequested)
	{
		await demoQueue.ProcessQueueAsync(token);
	}
}
```

This construction makes sure that the same queue that is registered in the dependency container will be used in our `RunAsync` method.

### Implementing the queue using the SemaphorSlim

The queue will make use of [semaphore slim](https://docs.microsoft.com/en-us/dotnet/api/system.threading.semaphoreslim) to ensure that the processing of items will happen on demand, any time a new item is added into the queue. Awaiting for the semaphore will ensure that computing resources are released when there are no elements to be processed. A dummy implementation could look like this:

```csharp
public class DemoQueue
{
	private SemaphoreSlim _semaphore = new SemaphoreSlim(0);
	private Queue<string> _queue = new Queue<string>();
	public void AddItem(string item)
	{
		_queue.Enqueue(item);
		_semaphore.Release();
	}
	public async Task ProcessQueueAsync(CancellationToken token) 
	{
		await _semaphore.WaitAsync(token);
		while (_queue.TryDequeue(out string item))
		{ // do something with the item
		}
	}
	public int GetQueueSize()
	{
		return _queue.Count;
	}
}
```

As long as the processing of the elements is fast enough when the queue is interrogated for its size it should return zero:

```curl
curl localhost:19081/Application/StatefulApi/queue-size
0
```

### ... after few days in Production

Everything runs fine for few days and then suddenly no items are processed anymore and the queue starts to fill up:

```curl
curl localhost:19081/Application/StatefulApi/queue-size
23
```

It's not that there are too many requests to be processed and the server cannot cope with that, what happens is that **no items** are being processed.

### So what does actually happen

In a Service Fabric cluster we take orchestration for granted and we don't really pay attention when partitions are being re-created, swapped or moved between nodes. In this case, taking a closer look at what happens when [partitions are swapped](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-lifecycle#stateful-service-primary-swaps) we might get a clue about where the problem is. Looking back at our [listener creation](#runasync-and-createservicereplicalisteners) we see that:
- When completed, the `_demoQueueCompletionSource` will provide a `DemoQueue` object
- If the replica is swapped and becomes secondary the service class is not deconstructed and therefore the `_demoQueueCompletionSource` will remain in memory
- If the same replica is swapped again and becomes primary, the `_demoQueueCompletionSource.TrySetResult(host.Services.GetService<DemoQueue>())` will not get the `DemoQueue` from the DI container since the `TaskCompletionSource` is already [RanToCompletion](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.taskstatus?view=netcore-3.1#System_Threading_Tasks_TaskStatus_RanToCompletion) and can provide a `DemoQueue` object. In the same time, the listener creation (which happens every time a replica becomes primary) will register a new/different `DemoQueue` object in the DI container. 

Therefore, there will be two `DemoQueue`s and as a consequence two `SemaphoreSlim`s objects that the application will operate with. One is used for awaiting while the other one is used for releasing the semaphore. The result is obvious, the processing of the queue is always awaiting on a semaphore that is never released.

### The fix

Changing a bit our `RunAsync` we can easily solve our problem:

```csharp
protected override async Task RunAsync(CancellationToken token)
{
	try
	{
		var demoQueue = await _demoQueueCompletionSource.Task;

		while (!token.IsCancellationRequested)
		{
			await demoQueue.ProcessQueueAsync(token);
		}
	}
	finally
	{
		_demoQueueCompletionSource = new TaskCompletionSource<DemoQueue>();
	}
}
```

By simply wrapping our code in a try finally block we ensure that whenever our processing is suspended we also dismiss the `DemoQueue` objected linked to the `_demoQueueCompletionSource` by just creating a new `TaskCompletionSource` object. The try finally block is needed because when the replica is downgraded an `OperationCanceledException` is thrown.

In order to simulate the replica swapping conditions we can use the `Move-ServiceFabricPrimaryReplica` PowerShell command

```powershell
Connect-ServiceFabricCluster
Move-ServiceFabricPrimaryReplica -ServiceName fabric:/Application/StatefulApi -PartitionId 5044e7bb-e85f-44d6-85fe-cba4bd0a7465 -NodeName _Node_3
```

### Conclusion

Whatever the technology or frameworks used there are always plenty of opportunities to shoot yourself in the foot. Now at least you know how not to do it by using `ServiceFabric`, `SemaphorSlim` and `TaskCompletionSource`.

A full working example can be found on [GitHub](https://github.com/coosmiin/Playground/tree/master/Service%20Fabric%20-%20TaskCompletionSource%20and%20SemaphoreSlim).