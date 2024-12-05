# Übung 5: Strategy-Entwurfsmuster

## Komplette Lösung

```csharp
using System;

// Strategy interface
public interface IStrategy
{
    void Execute();
}

// Concrete strategy A
public class ConcreteStrategyA : IStrategy
{
    public void Execute()
    {
        Console.WriteLine("Executing Strategy A");
    }
}

// Concrete strategy B
public class ConcreteStrategyB : IStrategy
{
    public void Execute()
    {
        Console.WriteLine("Executing Strategy B");
    }
}

// Context class
public class Context
{
    private IStrategy _strategy;

    public void SetStrategy(IStrategy strategy)
    {
        _strategy = strategy;
    }

    public void ExecuteStrategy()
    {
        if (_strategy == null)
        {
            Console.WriteLine("Strategy not set.");
        }
        else
        {
            _strategy.Execute();
        }
    }
}

// Testing the Strategy pattern
public class Program
{
    public static void Main()
    {
        Context context = new Context();

        context.SetStrategy(new ConcreteStrategyA());
        context.ExecuteStrategy(); // Output: Executing Strategy A

        context.SetStrategy(new ConcreteStrategyB());
        context.ExecuteStrategy(); // Output: Executing Strategy B
    }
}
```