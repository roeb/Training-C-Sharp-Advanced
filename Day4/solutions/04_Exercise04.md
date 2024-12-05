# Übung 4: Observer-Entwurfsmuster

## Komplette Lösung

```csharp
using System;
using System.Collections.Generic;

// Observer interface
public interface IObserver
{
    void Update(string message);
}

// Subject interface
public interface ISubject
{
    void Register(IObserver observer);
    void Unregister(IObserver observer);
    void NotifyObservers(string message);
}

// Concrete subject class
public class NewsAgency : ISubject
{
    private List<IObserver> observers = new List<IObserver>();

    public void Register(IObserver observer)
    {
        observers.Add(observer);
    }

    public void Unregister(IObserver observer)
    {
        observers.Remove(observer);
    }

    public void NotifyObservers(string message)
    {
        foreach (var observer in observers)
        {
            observer.Update(message);
        }
    }
}

// Concrete observer class
public class NewsChannel : IObserver
{
    private string _name;
    
    public NewsChannel(string name)
    {
        _name = name;
    }

    public void Update(string message)
    {
        Console.WriteLine($"{_name} received update: {message}");
    }
}

public class Program
{
    public static void Main()
    {
        NewsAgency agency = new NewsAgency();

        NewsChannel channel1 = new NewsChannel("Channel 1");
        NewsChannel channel2 = new NewsChannel("Channel 2");

        agency.Register(channel1);
        agency.Register(channel2);

        agency.NotifyObservers("Breaking news: New Observer pattern implemented!");

        agency.Unregister(channel1);

        agency.NotifyObservers("Update: Observer pattern working flawlessly.");
    }
}
```