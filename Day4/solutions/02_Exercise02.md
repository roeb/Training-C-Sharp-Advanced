# Übung 2: Singleton-Entwurfsmuster

## Komplette Lösung

```csharp
using System;

public sealed class Singleton
{
    private static Singleton instance = null;
    private static readonly object padlock = new object();

    Singleton()
    {
    }

    public static Singleton GetInstance()
    {
        if (instance == null)
        {
            lock (padlock)
            {
                if (instance == null)
                {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }

    public void ShowMessage()
    {
        Console.WriteLine("Single instance - Singleton pattern!");
    }
}

public class Program
{
    public static void Main()
    {
        Singleton s1 = Singleton.GetInstance();
        Singleton s2 = Singleton.GetInstance();

        if (s1 == s2)
        {
            Console.WriteLine("Both instances are the same.");
        }

        s1.ShowMessage();
    }
}
```