# Übung 1: Generische Klasse für eine Sammlung

## Komplette Lösung

```csharp
using System;
using System.Collections.Generic;

public class GenericCollection<T>
{
    private List<T> items = new List<T>();

    // Add an item to the collection
    public void Add(T item)
    {
        items.Add(item);
    }

    // Remove an item from the collection
    public bool Remove(T item)
    {
        return items.Remove(item);
    }

    // Get an item at a specific index
    public T Get(int index)
    {
        if (index < 0 || index >= items.Count)
        {
            throw new IndexOutOfRangeException("Index out of range");
        }
        return items[index];
    }
}

// Example usage
public class Program
{
    public static void Main()
    {
        var intCollection = new GenericCollection<int>();
        intCollection.Add(10);
        intCollection.Add(20);
        Console.WriteLine(intCollection.Get(0)); // Output: 10

        var stringCollection = new GenericCollection<string>();
        stringCollection.Add("Hello");
        stringCollection.Add("World");
        Console.WriteLine(stringCollection.Get(1)); // Output: World

        stringCollection.Remove("Hello");
        try
        {
            Console.WriteLine(stringCollection.Get(0)); // Output: World
        }
        catch (IndexOutOfRangeException e)
        {
            Console.WriteLine(e.Message);
        }
    }
}
```