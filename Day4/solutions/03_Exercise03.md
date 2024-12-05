# Übung 3: Factory-Entwurfsmuster

## Komplette Lösung

```csharp
using System;

public interface IShape
{
    void Draw();
}

public class Circle : IShape
{
    public void Draw()
    {
        Console.WriteLine("Drawing a Circle");
    }
}

public class Rectangle : IShape
{
    public void Draw()
    {
        Console.WriteLine("Drawing a Rectangle");
    }
}

public class Square : IShape
{
    public void Draw()
    {
        Console.WriteLine("Drawing a Square");
    }
}

public class ShapeFactory
{
    public IShape GetShape(string shapeType)
    {
        switch (shapeType.ToLower())
        {
            case "circle":
                return new Circle();
            case "rectangle":
                return new Rectangle();
            case "square":
                return new Square();
            default:
                throw new ArgumentException("Invalid shape type");
        }
    }
}

public class Program
{
    public static void Main()
    {
        ShapeFactory factory = new ShapeFactory();

        IShape circle = factory.GetShape("circle");
        circle.Draw();

        IShape rectangle = factory.GetShape("rectangle");
        rectangle.Draw();

        IShape square = factory.GetShape("square");
        square.Draw();
    }
}
```