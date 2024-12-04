# Übung 2: Parallele Verarbeitung mit Parallel.ForEach

## Komplette Lösung

```csharp
using System;
using System.Collections.Concurrent;
using System.Collections.Generic;
using System.Linq;
using System.Threading;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        List<int> numbers = Enumerable.Range(1, 20).ToList();
        ConcurrentBag<int> processedNumbers = new ConcurrentBag<int>();
        Random random = new Random();

        Console.WriteLine("Starting parallel processing...");
        Parallel.ForEach(numbers, number =>
        {
            // Simulate some processing work with a random delay
            int delay = random.Next(10, 100);
            Thread.Sleep(delay);

            // Multiply the number by a random factor
            int factor = random.Next(1, 10);
            int result = number * factor;

            processedNumbers.Add(result);
        });
        Console.WriteLine("Processing completed.");

        Console.WriteLine("Processed Numbers:");
        foreach (int processedNumber in processedNumbers)
        {
            Console.WriteLine(processedNumber);
        }
    }
}
```