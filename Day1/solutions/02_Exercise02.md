# Übung 2: Erweitertes Arbeiten mit Generischen Methoden und Constraints

## Komplette Lösung

```csharp
using System;

public class Comparer
{
    // Generic method with constraint ensuring T implements IComparable
    public static void CompareAndSwap<T>(ref T item1, ref T item2) where T : IComparable<T>
    {
        if (item1.CompareTo(item2) > 0)
        {
            // Swap the values
            T temp = item1;
            item1 = item2;
            item2 = temp;
        }
    }

    // Helper method to print the values
    public static void PrintValues<T>(T item1, T item2)
    {
        Console.WriteLine($"Item1: {item1}, Item2: {item2}");
    }
}

// Example usage
public class Program
{
    public static void Main()
    {
        int a = 10, b = 5;
        Comparer.PrintValues(a, b); // Output: Item1: 10, Item2: 5
        Comparer.CompareAndSwap(ref a, ref b);
        Comparer.PrintValues(a, b); // Output: Item1: 5, Item2: 10

        string str1 = "banana", str2 = "apple";
        Comparer.PrintValues(str1, str2); // Output: Item1: banana, Item2: apple
        Comparer.CompareAndSwap(ref str1, ref str2);
        Comparer.PrintValues(str1, str2); // Output: Item1: apple, Item2: banana
    }
}
```