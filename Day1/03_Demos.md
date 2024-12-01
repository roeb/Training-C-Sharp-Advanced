# Demos

## Generics in Klassen

```csharp
public class GenericBox<T>
{
    private T _content;

    public GenericBox(T content)
    {
        _content = content;
    }

    public T GetContent()
    {
        return _content;
    }

    public void SetContent(T content)
    {
        _content = content;
    }
}

public class Program
{
    public static void Main()
    {
        var intBox = new GenericBox<int>(123);
        Console.WriteLine("IntBox contains: " + intBox.GetContent());

        var stringBox = new GenericBox<string>("Hello World");
        Console.WriteLine("StringBox contains: " + stringBox.GetContent());
    }
}
```

## Generic in Methoden

```csharp
public class Utilities
{
    public T Max<T>(T a, T b) where T : IComparable<T>
    {
        return a.CompareTo(b) > 0 ? a : b;
    }
}

public class Program
{
    public static void Main()
    {
        Utilities utilities = new Utilities();

        int maxInt = utilities.Max(5, 10);
        Console.WriteLine("Max Int: " + maxInt);

        string maxString = utilities.Max("apple", "banana");
        Console.WriteLine("Max String: " + maxString);
    }
}
```

## Generics in Interfaces und abstrakten Klassen

```csharp
public interface IRepository<T>
{
    void Add(T item);
    T Get(int id);
}

public abstract class AbstractRepository<T> : IRepository<T>
{
    protected List<T> _items = new List<T>();

    public abstract void Add(T item);

    public T Get(int id)
    {
        return _items[id];
    }
}

public class Product { public string Name { get; set; } }
public class ProductRepository : AbstractRepository<Product>
{
    public override void Add(Product item)
    {
        _items.Add(item);
    }
}

public class Program
{
    public static void Main()
    {
        var productRepo = new ProductRepository();
        productRepo.Add(new Product { Name = "Laptop" });
        
        Product product = productRepo.Get(0);
        Console.WriteLine("Product Name: " + product.Name);
    }
}
```

## Contraints with Generics

```csharp
// Constraint für class
public class ReferenceTypeOnly<T> where T : class
{
    private T _value;

    public ReferenceTypeOnly(T value)
    {
        _value = value;
    }

    public T GetValue()
    {
        return _value;
    }
}

// Constraint für struct
public class ValueTypeOnly<T> where T : struct
{
    private T _value;

    public ValueTypeOnly(T value)
    {
        _value = value;
    }

    public T GetValue()
    {
        return _value;
    }
}

// Constraint für new()
public class Creatable<T> where T : new()
{
    public T CreateInstance()
    {
        return new T();
    }
}

public class SampleClass { }

public struct SampleStruct { }

public class Program
{
    public static void Main()
    {
        var refType = new ReferenceTypeOnly<string>("Hello");
        Console.WriteLine("Reference Type Value: " + refType.GetValue());

        var valType = new ValueTypeOnly<int>(42);
        Console.WriteLine("Value Type Value: " + valType.GetValue());

        var creatable = new Creatable<SampleClass>();
        SampleClass instance = creatable.CreateInstance();
        Console.WriteLine("Created Instance: " + instance.GetType().Name);
    }
}
```

## Kombinierte Contraints

```csharp
public abstract class Animal
{
    public abstract void Speak();
}

public class Dog : Animal, new()
{
    public override void Speak()
    {
        Console.WriteLine("Woof!");
    }
}

public class AnimalCreator<T> where T : Animal, new()
{
    public T CreateAnimal()
    {
        return new T();
    }
}

public class Program
{
    public static void Main()
    {
        var dogCreator = new AnimalCreator<Dog>();
        var dog = dogCreator.CreateAnimal();
        dog.Speak();
    }
}
```