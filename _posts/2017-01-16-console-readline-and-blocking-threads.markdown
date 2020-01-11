---
title: "Console.ReadLine and blocking threads"
date: 2017-01-16 +0200
categories: dotnet threading
---

>**The problem:** Let's say you have a console application that calls into a third party library that spins up a thread to do a continuous job (like monitoring network traffic for example). This library exposes event handlers that you can attach on to perform an action (for example when a specific url is requested in the browser). And now, let's also say that before performing that action you have to wait for user confirmation (`Console.ReadLine()`). How do you do that?

Here is the (initial) code to simulate it (note that, just for brevity, there is no third library here and some of the code is just meant to simulate the real situation - `while(true)` or `Thread.Sleep()` - and it would never be used in real scenarios):
```
static void Main(string[] args)
{
	Task.Factory.StartNew(Go);
	Console.ReadLine();
}

private static void Go()
{
	while (true)
	{
		if (DateTime.Now.Second % 10 == 0)
		{
			Console.WriteLine("Type 'OK' before proceeding");
			var input = Console.ReadLine();
			if (input == "OK")
				// Do some stuff
			Thread.Sleep(1000);
		}
	}
}
```
All good, except that this will block the thread that is supposed to run a ***continuous*** job. Maybe there are other handlers we are hooked on or maybe we want (taking the network monitoring example) to not stop monitoring traffic until the user gives his input.
The solution might be obvious: always let the background threads continue their work and take user input only from the main thread. While there are several ways to do that by using thread synchronization using a [`BlockingCollection<T>`](https://msdn.microsoft.com/en-us/library/dd267312) seems the most elegant solution to me:
```
private static BlockingCollection<string> commands = new BlockingCollection<string>();

static void Main(string[] args)
{
	Task.Factory.StartNew(Go);
	foreach (var command in commands.GetConsumingEnumerable())
	{
		Console.WriteLine("Type 'OK' before proceeding with command {0}", command);
		var input = Console.ReadLine();
		if (input == "OK")
			// Do some stuff
	}
}

private static void Go()
{
	while (true)
	{
		if (DateTime.Now.Second % 10 == 0)
		{
			commands.Add(string.Format("command {0}", DateTime.Now.Second));
			Thread.Sleep(1000);
		}
	}
}
```
The `BlockingCollection<T>` (as from the official documentation) provides blocking and bounding capabilities for thread-safe collections that implement IProducerConsumerCollection<T>. It is shared between the main thread and the background thread and while its being populated inside the background thread its being consumed on the main thread. There are two important advantages of using this collection:

- Is thread safe.
- As long as the `CompleteAdding()` method is not called the enumerator is not completed. It will always wait for new items to be processed.

While there are other enhancements that could be added (like simulating a timeout for the Command.ReadLine()), there you go, this is how you can easily let the background thread do its job while also responding to events signaled by the same thread. 