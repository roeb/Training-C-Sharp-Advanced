# Übung 2: Einfaches CRUD mit EF Core

## Komplette Lösung

```csharp
using Microsoft.EntityFrameworkCore;
using System;
using System.Linq;

public class Program
{
    public static void Main()
    {
        using (var context = new AppDbContext())
        {
            // CRUD-Operationen ausführen
            AddProduct(context, "Sample Product", 10.99m);
            GetAllProducts(context);
            UpdateProductPrice(context, 1, 12.99m);
            DeleteProduct(context, 1);
            GetAllProducts(context);
        }
    }

    private static void AddProduct(AppDbContext context, string name, decimal price)
    {
        var product = new Product { Name = name, Price = price };
        context.Products.Add(product);
        context.SaveChanges();
        Console.WriteLine($"Product {name} added.");
    }

    private static void GetAllProducts(AppDbContext context)
    {
        var products = context.Products.ToList();
        Console.WriteLine("Products in database:");
        foreach (var product in products)
        {
            Console.WriteLine($"ID: {product.Id}, Name: {product.Name}, Price: {product.Price}");
        }
    }

    private static void UpdateProductPrice(AppDbContext context, int productId, decimal newPrice)
    {
        var product = context.Products.Find(productId);
        if (product != null)
        {
            product.Price = newPrice;
            context.SaveChanges();
            Console.WriteLine($"Product ID {productId} updated to new price: {newPrice}");
        }
        else
        {
            Console.WriteLine($"Product with ID {productId} does not exist.");
        }
    }

    private static void DeleteProduct(AppDbContext context, int productId)
    {
        var product = context.Products.Find(productId);
        if (product != null)
        {
            context.Products.Remove(product);
            context.SaveChanges();
            Console.WriteLine($"Product ID {productId} deleted.");
        }
        else
        {
            Console.WriteLine($"Product with ID {productId} does not exist.");
        }
    }
}
```
