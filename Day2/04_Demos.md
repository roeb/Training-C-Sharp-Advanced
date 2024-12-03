# Demos

## Delegate

```csharp
using System;

// Delegate definition
public delegate void OperationHandler(int x, int y);

public class Calculator
{
    // Method that uses the delegate
    public void ExecuteOperation(int a, int b, OperationHandler operation)
    {
        operation(a, b);
    }
}

public class Program
{
    public static void Add(int x, int y)
    {
        Console.WriteLine($"Addition: {x + y}");
    }

    public static void Subtract(int x, int y)
    {
        Console.WriteLine($"Subtraction: {x - y}");
    }

    public static void Main()
    {
        Calculator calculator = new Calculator();

        // Using the delegate to point to Add method
        OperationHandler addHandler = Add;
        calculator.ExecuteOperation(10, 5, addHandler);

        // Using the delegate to point to Subtract method
        OperationHandler subtractHandler = Subtract;
        calculator.ExecuteOperation(10, 5, subtractHandler);
    }
}
```

## Mehrere Delegate Zuweisungen 

```csharp
using System;

// Delegate definition
public delegate void OperationHandler(int x, int y);

public class Calculator
{
    // Method to execute multiple operations
    public void ExecuteOperations(int a, int b, OperationHandler operation)
    {
        if (operation != null)
        {
            operation(a, b);
        }
    }
}

public class Program
{
    public static void Add(int x, int y)
    {
        Console.WriteLine($"Addition: {x + y}");
    }

    public static void Subtract(int x, int y)
    {
        Console.WriteLine($"Subtraction: {x - y}");
    }

    public static void Multiply(int x, int y)
    {
        Console.WriteLine($"Multiplication: {x * y}");
    }

    public static void Main()
    {
        Calculator calculator = new Calculator();

        // Using multicast delegate to combine multiple methods
        OperationHandler operations = Add;
        operations += Subtract;
        operations += Multiply;

        // Execute all operations
        calculator.ExecuteOperations(10, 5, operations);

        // Remove Subtract method from the delegate
        operations -= Subtract;

        Console.WriteLine("\nAfter removing Subtract:");
        calculator.ExecuteOperations(10, 5, operations);
    }
}
```

## Multicast Delegate für Notifications

```csharp
using System;

// Definition des Delegaten
public delegate void NotifyUser(string message);

public class NotificationService
{
    // Methode zum Senden von E-Mails
    public void SendEmail(string message)
    {
        Console.WriteLine($"Sending Email: {message}");
    }

    // Methode zum Senden von SMS
    public void SendSms(string message)
    {
        Console.WriteLine($"Sending SMS: {message}");
    }

    // Methode zum Senden von Push-Benachrichtigungen
    public void SendPushNotification(string message)
    {
        Console.WriteLine($"Sending Push Notification: {message}");
    }
}

public class Program
{
    public static void Main()
    {
        NotificationService notifier = new NotificationService();

        // Zuweisung von mehreren Methoden zum Multicast-Delegate
        NotifyUser notify = notifier.SendEmail;
        notify += notifier.SendSms;
        notify += notifier.SendPushNotification;

        // Ausführung aller zugewiesenen Methoden
        notify("Hello, this is a multicast delegate notification.");

        // Entfernen einer Methode aus dem Delegate
        notify -= notifier.SendSms;

        // Ausführung nach Entfernen einer Methode
        Console.WriteLine("\nAfter removing the SMS notification:");
        notify("Hello again, without SMS notification.");
    }
}
```

## Delegate als Rückgabewert

```csharp
using System;

// Delegate definition
public delegate string StringFormatter(string input);

public class FormatterFactory
{
    // Method that returns a delegate
    public StringFormatter GetFormatter(string formatType)
    {
        switch (formatType.ToLower())
        {
            case "uppercase":
                return ToUpperCase;
            case "lowercase":
                return ToLowerCase;
            case "reverse":
                return ReverseString;
            default:
                throw new InvalidOperationException("Invalid format type");
        }
    }

    private string ToUpperCase(string input)
    {
        return input.ToUpper();
    }

    private string ToLowerCase(string input)
    {
        return input.ToLower();
    }

    private string ReverseString(string input)
    {
        char[] chars = input.ToCharArray();
        Array.Reverse(chars);
        return new string(chars);
    }
}

public class Program
{
    public static void Main()
    {
        FormatterFactory factory = new FormatterFactory();

        // Get a delegate for uppercasing
        StringFormatter formatter = factory.GetFormatter("uppercase");
        Console.WriteLine(formatter("Hello World"));

        // Get a delegate for reversing
        formatter = factory.GetFormatter("reverse");
        Console.WriteLine(formatter("Hello World"));
    }
}
```

## Delegates mit Events

```csharp
using System;

// Delegate definition
public delegate void ThresholdReachedEventHandler(int threshold);

public class Counter
{
    private int _count;
    private int _threshold;

    // Event using the defined delegate
    public event ThresholdReachedEventHandler ThresholdReached;

    public Counter(int threshold)
    {
        _threshold = threshold;
    }

    public void Add(int value)
    {
        _count += value;
        Console.WriteLine($"Counter: {_count}");

        if (_count >= _threshold)
        {
            OnThresholdReached(_threshold);
        }
    }

    // Method to trigger the event
    protected virtual void OnThresholdReached(int threshold)
    {
        ThresholdReached?.Invoke(threshold);
    }
}

public class Program
{
    public static void Main()
    {
        Counter counter = new Counter(10);

        // Subscribe to the event
        counter.ThresholdReached += ThresholdReachedHandler;

        for (int i = 0; i < 5; i++)
        {
            counter.Add(3);
        }
    }

    // Event handler method
    public static void ThresholdReachedHandler(int threshold)
    {
        Console.WriteLine($"Threshold of {threshold} reached!");
    }
}
```

## Another Event Demo 

```csharp
using System;
using System.Collections.Generic;

// Delegate for the event
public delegate void NewsPublishedEventHandler(string news);

public class NewsPublisher
{
    // Event declaration
    public event NewsPublishedEventHandler NewsPublished;

    public void PublishNews(string news)
    {
        Console.WriteLine($"Publishing news: {news}");
        OnNewsPublished(news);
    }

    // Method to raise the event
    protected virtual void OnNewsPublished(string news)
    {
        NewsPublished?.Invoke(news);
    }
}

public class NewsSubscriber
{
    private string _name;

    public NewsSubscriber(string name, NewsPublisher publisher)
    {
        _name = name;
        // Subscribe to the event
        publisher.NewsPublished += ReceiveNews;
    }

    // Event handler
    public void ReceiveNews(string news)
    {
        Console.WriteLine($"{_name} received news: {news}");
    }
}

public class Program
{
    public static void Main()
    {
        NewsPublisher publisher = new NewsPublisher();

        // Subscribers
        NewsSubscriber subscriber1 = new NewsSubscriber("Subscriber 1", publisher);
        NewsSubscriber subscriber2 = new NewsSubscriber("Subscriber 2", publisher);

        // Publish news
        publisher.PublishNews("Breaking News: New C# Version Released!");
        publisher.PublishNews("Weather Alert: Heavy Rain Tomorrow!");
    }
}
```

## Benutzerdefinierte Attribute

```csharp
using System;
using System.Reflection;

// Define a custom attribute
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method)]
public class DocumentationAttribute : Attribute
{
    public string Author { get; }
    public string Version { get; }

    public DocumentationAttribute(string author, string version)
    {
        Author = author;
        Version = version;
    }
}

// Apply the custom attribute to a class
[Documentation("Jane Doe", "1.0")]
public class SampleClass
{
    [Documentation("John Smith", "1.2")]
    public void SampleMethod()
    {
        Console.WriteLine("This is a sample method.");
    }
}

public class Program
{
    public static void Main()
    {
        // Retrieve the attribute information
        Type type = typeof(SampleClass);
        DocumentationAttribute classAttr = (DocumentationAttribute)Attribute.GetCustomAttribute(type, typeof(DocumentationAttribute));

        if (classAttr != null)
        {
            Console.WriteLine($"Class {type.Name} is authored by {classAttr.Author}, version {classAttr.Version}");
        }

        MethodInfo methodInfo = type.GetMethod("SampleMethod");
        DocumentationAttribute methodAttr = (DocumentationAttribute)Attribute.GetCustomAttribute(methodInfo, typeof(DocumentationAttribute));

        if (methodAttr != null)
        {
            Console.WriteLine($"Method {methodInfo.Name} is authored by {methodAttr.Author}, version {methodAttr.Version}");
        }
    }
}
```

## Attribut zum Serialisieren

```csharp
using System;
using System.IO;
using System.Runtime.Serialization;
using System.Runtime.Serialization.Formatters.Binary;

// Mark the class with the Serializable attribute
[Serializable]
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

public class Program
{
    public static void Main()
    {
        // Create a new instance of the Person class
        Person person = new Person { Name = "Alice", Age = 30 };

        // Serialize the object to a file
        IFormatter formatter = new BinaryFormatter();
        using (Stream stream = new FileStream("person.bin", FileMode.Create, FileAccess.Write, FileShare.None))
        {
            formatter.Serialize(stream, person);
        }

        Console.WriteLine("Person object serialized.");

        // Deserialize the object from the file
        using (Stream stream = new FileStream("person.bin", FileMode.Open, FileAccess.Read, FileShare.Read))
        {
            Person deserializedPerson = (Person)formatter.Deserialize(stream);
            Console.WriteLine($"Deserialized Person: {deserializedPerson.Name}, Age: {deserializedPerson.Age}");
        }

         // Serialize the object to a JSON file
        string jsonString = JsonSerializer.Serialize(person);
        File.WriteAllText("person.json", jsonString);
        Console.WriteLine("Person object serialized to JSON.");

        // Deserialize the object from the JSON file
        jsonString = File.ReadAllText("person.json");
        Person deserializedPerson = JsonSerializer.Deserialize<Person>(jsonString);
        Console.WriteLine($"Deserialized Person: {deserializedPerson.Name}, Age: {deserializedPerson.Age}");
    }
}
```

## Reflection: Analyse

```csharp
using System;
using System.Reflection;

public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public void Introduce()
    {
        Console.WriteLine($"Hi, I'm {Name} and I'm {Age} years old.");
    }
}

public class Program
{
    public static void Main()
    {
        // Create an instance of the Person class
        Person person = new Person { Name = "Alice", Age = 30 };

        // Get the type of the Person class
        Type type = person.GetType();

        // Display all properties of the Person class
        Console.WriteLine("Properties:");
        foreach (PropertyInfo property in type.GetProperties())
        {
            Console.WriteLine($"{property.Name} = {property.GetValue(person)}");
        }

        // Display all methods of the Person class
        Console.WriteLine("\nMethods:");
        foreach (MethodInfo method in type.GetMethods(BindingFlags.Public | BindingFlags.Instance | BindingFlags.DeclaredOnly))
        {
            Console.WriteLine(method.Name);
        }

        // Invoke the Introduce method using reflection
        Console.WriteLine("\nInvoking Introduce method:");
        MethodInfo introduceMethod = type.GetMethod("Introduce");
        introduceMethod.Invoke(person, null);
    }
}
```

## Reflection: Intialisierung, Invoke & SetValue

```csharp
using System;
using System.Reflection;

public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public void Introduce()
    {
        Console.WriteLine($"Hi, I'm {Name} and I'm {Age} years old.");
    }
}

public class Program
{
    public static void Main()
    {
        // Get the Type object for the Person class
        Type personType = typeof(Person);

        // Create an instance of the Person class using reflection
        object personInstance = Activator.CreateInstance(personType);

        // Set properties using reflection
        PropertyInfo nameProperty = personType.GetProperty("Name");
        PropertyInfo ageProperty = personType.GetProperty("Age");

        nameProperty.SetValue(personInstance, "Alice");
        ageProperty.SetValue(personInstance, 30);

        // Invoke the Introduce method using reflection
        MethodInfo introduceMethod = personType.GetMethod("Introduce");
        introduceMethod.Invoke(personInstance, null);
    }
}
```