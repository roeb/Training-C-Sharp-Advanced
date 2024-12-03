# Übung 2: Verwendung von Attributen und Reflection

## Komplette Lösung

```csharp
using System;
using System.Reflection;

// Define a custom attribute
[AttributeUsage(AttributeTargets.Class)]
public class InfoAttribute : Attribute
{
    public string Description { get; }

    public InfoAttribute(string description)
    {
        Description = description;
    }
}

// Apply the attribute to some classes
[Info("This class handles customer data.")]
public class CustomerManager
{
}

[Info("This class processes orders.")]
public class OrderProcessor
{
}

public class Program
{
    public static void Main()
    {
        // Use reflection to find classes with InfoAttribute
        foreach (Type type in Assembly.GetExecutingAssembly().GetTypes())
        {
            InfoAttribute infoAttribute = type.GetCustomAttribute<InfoAttribute>();
            if (infoAttribute != null)
            {
                Console.WriteLine($"{type.Name}: {infoAttribute.Description}");
            }
        }
    }
}
```