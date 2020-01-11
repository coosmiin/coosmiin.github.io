---
title: "Catching the .NET System.Console close event"
date: 2016-10-23 +0200
categories: dotnet console
---

If you created a console app in C# and you want to execute some code if the user closes the console window (by using the window close button, CTRL+C, shutdown etc) here is what you need to do:

```c#
class Program
{
	static void Main(string[] args)
	{
		SetConsoleCtrlHandler(ConsoleEventCallback, true); // true/false = the handler is added/removed;

		Console.Read();
	}

	private static bool ConsoleEventCallback(int eventType)
	{
		// DO YOUR THING

		return true;
		// Return FALSE. If none of the registered handler functions returns TRUE, 
		// the default handler terminates the process.
		// Return TRUE. In this case, no other handler functions are called 
		// and the system terminates the process.
	}

	[DllImport("kernel32.dll", SetLastError = true)]
	internal static extern bool SetConsoleCtrlHandler(HandlerRoutine callback, bool add);

	internal delegate bool HandlerRoutine(int eventType);
}
```
Details about handling different `eventType` values can be found on MSDN.

Further reading:

* [SetConsoleCtrlHandler](https://msdn.microsoft.com/en-us/library/windows/desktop/ms686016(v=vs.85).aspx) function on MSDN.
* [HandlerRoutine](https://msdn.microsoft.com/en-us/library/windows/desktop/ms683242(v=vs.85).aspx) callback function on MSDN.