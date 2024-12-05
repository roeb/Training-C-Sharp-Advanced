# Übung 1: Dependency Injection mit .NET-Built-In Container

## Komplette Lösung

```csharp
using System;
using System.Collections.Generic;
using Microsoft.Extensions.DependencyInjection;

public interface ILoggingService
{
    void Log(string message);
}

public class ConsoleLoggingService : ILoggingService
{
    public void Log(string message)
    {
        Console.WriteLine($"Log: {message}");
    }
}

public interface IDataService
{
    List<string> GetData();
}

public class SimpleDataService : IDataService
{
    public List<string> GetData()
    {
        return new List<string> { "Data1", "Data2", "Data3" };
    }
}

public class Application
{
    private readonly ILoggingService _loggingService;
    private readonly IDataService _dataService;

    public Application(ILoggingService loggingService, IDataService dataService)
    {
        _loggingService = loggingService;
        _dataService = dataService;
    }

    public void Run()
    {
        _loggingService.Log("Application Starting...");

        var data = _dataService.GetData();
        foreach (var item in data)
        {
            _loggingService.Log(item);
        }

        _loggingService.Log("Application Finished.");
    }
}

public class Program
{
    public static void Main()
    {
        // Configure services
        var services = new ServiceCollection();
        services.AddSingleton<ILoggingService, ConsoleLoggingService>();
        services.AddSingleton<IDataService, SimpleDataService>();
        services.AddTransient<Application>();

        // Build service provider
        var serviceProvider = services.BuildServiceProvider();

        // Resolve and run the application
        var app = serviceProvider.GetService<Application>();
        app.Run();
    }
}
```