---
title: "Enum class type converters"
date: 2021-07-XX +0200
categories: C# classenum typeconverter
---

Everybody loves [class enums](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/enumeration-classes-over-enum-types), right? Maybe not, but how do you use them when you want to map them to settings read from configuration? You have a .Net app which reads JSON settings from `appSettings.json` and one of the settings needs to be mapped to an enumaration. But instead of an `enum` you would like to use an enumeration class. How do you do it? [Type converters](https://docs.microsoft.com/dotnet/api/system.componentmodel.typeconverter) to the rescue.

Let's say we have this `appSettings.json`: 
```json
{
  "MyOptions": {
    "MyEnumValue":  "enumTypeValue1"
  }
}
```
, and this enumeration class we try to map our `MyEnumValue` to:
```csharp
public class MyEnumValue
{
    public static MyEnumValue EnumTypeValue1 = new("enumTypeValue1");
    public string Name { get; set; }
    public MyEnumValue(string name) => Name = name;
    public static implicit operator string(MyEnumValue enumValue) => enumValue.Name;
}
```
> Note: usually these type of classes should iplement `IComparable` or `IEquatable<T>` - removed for brevity.

The implicit operator is used just to be able to use `string` and `MyEnumValue` interchangeably and has no other relevance to the case being described here.

The options class used to read the whole settings object:

```csharp
public class MyClass
{
    private readonly MyOptions _options;
    public MyClass(IOptions<MyOptions> options)
    {
        _options = options?.Value ?? throw new ArgumentNullException(nameof(options));
    }
    public string GetValue() => _options.MyEnumValue;
}
```

To be complete, this is the simplest way to build your app host to automatically read your app settings json and to register it for dependency injection via an `IOptions<T>` type:

```csharp
static void Main(string[] args)
{
  using IHost host = CreateHostBuilder(args).Build();
  var myClass = host.Services.GetService<MyClass>();
  Console.WriteLine(myClass.GetValue());
}

private static IHostBuilder CreateHostBuilder(string[] args) =>
  Host.CreateDefaultBuilder(args)
    .ConfigureServices((context, services) => 
    {
      var configuration = context.Configuration;
      services.Configure<MyOptions>(configuration.GetSection(nameof(MyOptions)));
      services.AddSingleton<MyClass>();
    });
```

> Note that `Host.CreateDefaultBuilder` will automatically load app `IConfiguration` from `appSettings.json` 

If you would run your program now, it would fail because the string value of `enumTypeValue1` cannot be mapped to `MyEnumValue.EnumTypeValue1` and the `_options.MyEnumValue` will be null.

By now you would already guess that the missing piece of the puzzle is the type converter:

```csharp
	public class MyEnumValueTypeConverter : TypeConverter
	{
		public override bool CanConvertFrom(ITypeDescriptorContext context, Type sourceType)
		{
			if (sourceType == typeof(string))
				return true;
			return base.CanConvertFrom(context, sourceType);
		}
		public override object ConvertFrom(ITypeDescriptorContext context, CultureInfo culture, object value)
		{
			if (value is string strValue)
				return new MyEnumValue(strValue);
			return base.ConvertFrom(context, culture, value);
		}
```

And now, if we adnotate our enum value class with the `[TypeConverter(typeof(MyEnumValueTypeConverter))]` attribute our app will work just fine.

This is it, the easy-peasy way of using enumeration classes mapped to `appSettings.json` options values.