# Übung 1: Implementierung von Events mit Parametern

## Komplette Lösung

```csharp
using System;

public class Publisher
{
    public delegate void DataProcessedEventHandler(string message);
    public event DataProcessedEventHandler DataProcessed;

    public void ProcessData()
    {
        Console.WriteLine("Processing data...");

        // Simulieren der Datenverarbeitung
        System.Threading.Thread.Sleep(1000); // Wartezeit von 1 Sekunde

        Console.WriteLine("Data processing completed.");

        // Event auslösen mit einer Nachricht
        OnDataProcessed("Data processing was successful.");
    }

    protected virtual void OnDataProcessed(string message)
    {
        // Überprüfen, ob es Abonnenten gibt, bevor das Event ausgelöst wird
        DataProcessed?.Invoke(message);
    }
}

public class Subscriber
{
    public void OnDataProcessed(string message)
    {
        Console.WriteLine($"Subscriber received notification: {message}");
    }
}

public class Program
{
    public static void Main()
    {
        Publisher publisher = new Publisher();
        Subscriber subscriber = new Subscriber();

        // Abonnieren des Events
        publisher.DataProcessed += subscriber.OnDataProcessed;

        // Aufrufen der Datenverarbeitung
        publisher.ProcessData();
    }
}
```