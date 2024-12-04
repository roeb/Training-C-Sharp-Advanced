# Demos

## async /wait

### 1. Async/Await

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        Console.WriteLine("Starting async method...");
        string result = await FetchDataAsync();
        Console.WriteLine(result);
    }

    public static async Task<string> FetchDataAsync()
    {
        await Task.Delay(2000); // Simuliert eine 2-Sekunden-Wartezeit
        return "Data fetched after delay";
    }
}
```

### Async/Wait mit Webservice

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
    private static readonly HttpClient client = new HttpClient();

    public static async Task Main()
    {
        Console.WriteLine("Starting async method...");
        string result = await FetchDataAsync();
        Console.WriteLine(result);
    }

    public static async Task<string> FetchDataAsync()
    {
         // Beispiel-URL zu JSONPlaceholder für einen typischen Datensatz
        string url = "https://jsonplaceholder.typicode.com/posts/1";

        // HTTP GET-Anfrage
        HttpResponseMessage response = await client.GetAsync(url);
        response.EnsureSuccessStatusCode(); // Löst eine Ausnahme aus, wenn der Statuscode ein Fehler ist

        // Response als Zeichenkette auslesen
        string responseBody = await response.Content.ReadAsStringAsync();
        return responseBody;
    }
}
```

### 2. Task.WhenAll

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        Task<string> task1 = FetchDataAsync("First");
        Task<string> task2 = FetchDataAsync("Second");

        string[] results = await Task.WhenAll(task1, task2);
        foreach (var result in results)
        {
            Console.WriteLine(result);
        }
    }

    public static async Task<string> FetchDataAsync(string name)
    {
        await Task.Delay(1000);
        return $"{name} data fetched";
    }
}
```

### 3. Task.WaitAll

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        Task task1 = Task.Run(() => DoWork("First"));
        Task task2 = Task.Run(() => DoWork("Second"));

        Task.WaitAll(task1, task2);
        Console.WriteLine("Both tasks completed.");
    }

    public static void DoWork(string name)
    {
        System.Threading.Thread.Sleep(1000); // Simuliert Arbeit
        Console.WriteLine($"{name} task completed");
    }
}
```

## Parallele Entwicklung

### 4. Parallel.For

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("Start Parallel.For");
        Parallel.For(0, 5, i =>
        {
            Console.WriteLine($"Iteration {i} by Thread {Task.CurrentId}");
        });
    }
}
```

### 5. Parallel.ForEach

```csharp
using System;
using System.Linq;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        var items = Enumerable.Range(1, 5).ToList();

        Console.WriteLine("Start Parallel.ForEach");
        Parallel.ForEach(items, item =>
        {
            Console.WriteLine($"Processing item {item} by Thread {Task.CurrentId}");
        });
    }
}
```

### Parallel Foreach mit Options


```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        var items = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

        // Legen Sie die maximale Anzahl der Threads fest
        var parallelOptions = new ParallelOptions
        {
            MaxDegreeOfParallelism = 4 // Beispiel für die Begrenzung auf 4 gleichzeitig laufende Threads
        };

        Parallel.ForEach(items, parallelOptions, item =>
        {
            Console.WriteLine($"Processing item {item} on thread {Task.CurrentId}");
            // Simulate some work
            Task.Delay(500).Wait(); // Nur zur Veranschaulichung; kein async/await hier
        });

        Console.WriteLine("Processing complete.");
    }
}
```


## LINQ

### 1. LINQ: Where, Select, OrderBy

```csharp
using System;
using System.Linq;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        List<int> numbers = new List<int> { 10, 20, 30, 40, 50 };

        // Where
        var filtered = numbers.Where(n => n > 20);

        // Select
        var projected = filtered.Select(n => n * 2);

        // OrderBy
        var ordered = projected.OrderBy(n => n);

        Console.WriteLine("Filtered, Projected and Ordered: ");
        foreach (var number in ordered)
        {
            Console.WriteLine(number);
        }
    }
}
```

### 2. LINQ: GroupBy, Sum, Average

```csharp
using System;
using System.Linq;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        List<int> numbers = new List<int> { 10, 20, 10, 30, 20, 30, 40, 50 };

        // GroupBy
        var groups = numbers.GroupBy(n => n);
        Console.WriteLine("Grouped numbers:");
        foreach (var group in groups)
        {
            Console.WriteLine($"Number {group.Key} appears {group.Count()} times.");
        }

        // Sum
        int sum = numbers.Sum();
        Console.WriteLine($"Sum: {sum}");

        // Average
        double average = numbers.Average();
        Console.WriteLine($"Average: {average}");
    }
}
```

### GroupBy mit Order und Select

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

public class Person
{
    public string Name { get; set; }
    public string City { get; set; }
}

public class Program
{
    public static void Main()
    {
        var people = new List<Person>
        {
            new Person { Name = "Alice", City = "New York" },
            new Person { Name = "Bob", City = "New York" },
            new Person { Name = "Charlie", City = "Los Angeles" },
            new Person { Name = "David", City = "Chicago" },
            new Person { Name = "Eve", City = "Chicago" },
            new Person { Name = "Frank", City = "New York" }
        };

        // LINQ-Anweisung zum Gruppieren, Sortieren und Auswählen
        var groupedByCity = people
            .GroupBy(p => p.City)
            .OrderBy(g => g.Key)
            .Select(g => new
            {
                City = g.Key,
                People = g.OrderBy(p => p.Name) // Sortieren der Namen innerhalb der Gruppe
            });

        // Ausgabe
        foreach (var group in groupedByCity)
        {
            Console.WriteLine($"City: {group.City}");
            foreach (var person in group.People)
            {
                Console.WriteLine($"  {person.Name}");
            }
        }
    }
}
```

### 3. LINQ: Distinct, Join

```csharp
using System;
using System.Linq;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        List<int> numbers = new List<int> { 10, 20, 10, 30, 20, 30 };

        // Distinct
        var distinctNumbers = numbers.Distinct();
        Console.WriteLine("Distinct numbers:");
        foreach (var number in distinctNumbers)
        {
            Console.WriteLine(number);
        }

        // Join
        List<string> words = new List<string> { "ten", "twenty", "thirty" };
        var join = numbers.Join(words,
                                num => num.ToString(),
                                word => word.Length.ToString(),
                                (num, word) => $"{num} is {word}");

        Console.WriteLine("Join:");
        foreach (var text in join)
        {
            Console.WriteLine(text);
        }
    }
}
```

### 4. LINQ: Concat

```csharp
using System;
using System.Linq;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        List<int> first = new List<int> { 1, 2, 3 };
        List<int> second = new List<int> { 4, 5, 6 };

        // Concat
        var concatenated = first.Concat(second);

        Console.WriteLine("Concatenated list:");
        foreach (var number in concatenated)
        {
            Console.WriteLine(number);
        }
    }
}
```

### 5. PLINQ Example

```csharp
using System;
using System.Linq;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        int[] numbers = Enumerable.Range(1, 100).ToArray();

        // PLINQ Parallel.ForEach
        var parallelQuery = numbers.AsParallel()
                                   .Where(n => n % 2 == 0)
                                   .Select(n => n * 2);

        Console.WriteLine("PLINQ results:");
        foreach (var number in parallelQuery)
        {
            Console.WriteLine(number);
        }
    }
}
```