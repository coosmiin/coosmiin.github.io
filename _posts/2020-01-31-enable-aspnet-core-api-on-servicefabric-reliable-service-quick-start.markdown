---
title: "Enable ASP.NET Core Api on a Service Fabric Reliable Service"
date: 2020-01-31 +0200
categories: aspnetcore servicefabric quickstart
---

Often times I need to create a quick Service Fabric reliable service demo and I find myself looking up and repeating the same steps to initialize the app. Usually I need my service to also have a http listener so I can easily access it. Since I don't need the full blown asp.net core mvc template I start with a simple reliable service and just add the `Kestrel` listener. Here is the quick start:

1. Create a new Service Fabric app

    Using Visual Studio create a new Service Fabric application. When asked to configure your first project, select a reliable service (stateless or statefull, it doesn't matter)

2. Add the following nuget packages to your service: `Microsoft.AspNetCore.Hosting`, `Microsoft.AspNetCore.Mvc.Core`, `Microsoft.AspNetCore.Server.Kestrel`, `Microsoft.ServiceFabric.AspNetCore.Kestrel`

3. Add the `Kestrel` listener

    Following the [official documentation](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore) add the `KestrelCommunicationListener` listener to your service. There are subtle differences between statefull and stateless services so make sure to follow the documentation. For a stateless service the `CreateServiceInstanceListeners` from your `StatefulService` class could look like this:

    ```csharp
    ...
		protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
		{
			return new ServiceInstanceListener[]
			{
				new ServiceInstanceListener(serviceContext =>
					new KestrelCommunicationListener(serviceContext, (url, listener) =>
						new WebHostBuilder()
							.UseKestrel()
							.ConfigureServices(
								 services => services
									 .AddSingleton<StatelessServiceContext>(serviceContext))
							.UseContentRoot(Directory.GetCurrentDirectory())
							.UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
							.UseStartup<Startup>()
							.UseUrls(url)
							.Build()))
			};
		}
    ...
    ```

3. Add the `Startup.cs` class to configure your asp.net core host

    While there are many configurations you may touch in your [Startup.cs](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/startup) class, for a very basic api you only need the `Mvc` middleware. Your `Startup.cs` could look like this:

    ```csharp
	internal class Startup
	{
		public IConfiguration Configuration { get; }

		public void ConfigureServices(IServiceCollection services)
		{
			services.AddMvcCore();
		}

		public void Configure(IApplicationBuilder app, IHostingEnvironment env)
		{
			app.UseMvc();
		}
	}
    ```

4. Add a test controller

    Now all you need to do is to add a dummy controller:

    ```csharp
	[ApiController]
	public class DummyController : ControllerBase
	{
		[HttpGet("dummy")]
		public async Task<ActionResult> Get()
		{
			return Ok("ok");
		}
	}
    ```

5. Test it

    Using Service Fabric [reverse proxy](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reverseproxy) a GET would suffice:

    ```curl
    curl localhost:19081/Application/StatelessApi/dummy
    ```
    , where `Application` = name of the application and `StatelessApi` = name of the service

6. (for statefull service only) Check the partitioning type

    By default the [partitioning scheme](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-concepts-partitioning) for a stefull service is `UniformInt64Partition`. If you don't want to deal with multiple partitions you could easily change the partition scheme to `Singleton`. In the application manifest it would look like this:

    ```xml
    <Service Name="StatefulApi" ServicePackageActivationMode="ExclusiveProcess">
      <StatefulService ServiceTypeName="StatefulApiType" TargetReplicaSetSize="[StatefulApi_TargetReplicaSetSize]" MinReplicaSetSize="[StatefulApi_MinReplicaSetSize]">
        <SingletonPartition />
      </StatefulService>
    </Service>
    ```

Github repo with a full working example: [Service Fabric - Enable ASP.NET Core Api Quick Start](https://github.com/coosmiin/Playground/tree/master/Service%20Fabric%20-%20Enable%20ASP.NET%20Core%20Api%20Quick%20Start)