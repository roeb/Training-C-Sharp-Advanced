# Übung: Implementierung eines Temperaturüberwachungssystems

## Komplette Lösung

```csharp
using System;

// Delegate definition
public delegate void TemperatureThresholdReachedHandler(float temperature);

public class TemperatureSensor
{
    private readonly Random _random = new Random();
    private const float Threshold = 30.0f;

    // Event declaration
    public event TemperatureThresholdReachedHandler TemperatureThresholdReached;

    public void ReadTemperature()
    {
        for (int i = 0; i < 10; i++)
        {
            float currentTemperature = (float)(_random.NextDouble() * 50);
            Console.WriteLine($"Current Temperature: {currentTemperature}");

            if (currentTemperature >= Threshold)
            {
                OnTemperatureThresholdReached(currentTemperature);
            }
        }
    }

    protected virtual void OnTemperatureThresholdReached(float temperature)
    {
        TemperatureThresholdReached?.Invoke(temperature);
    }
}

public class AlarmSystem
{
    // Event handler method
    public void ActivateAlarm(float temperature)
    {
        Console.WriteLine($"Alarm! Temperature reached {temperature} degrees.");
    }
}

public class Program
{
    public static void Main()
    {
        TemperatureSensor sensor = new TemperatureSensor();
        AlarmSystem alarm = new AlarmSystem();

        // Subscribe to the event
        sensor.TemperatureThresholdReached += alarm.ActivateAlarm;

        // Simulate temperature readings
        sensor.ReadTemperature();
    }
}
```