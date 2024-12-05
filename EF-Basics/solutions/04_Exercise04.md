# Übung 4: LINQ-Abfragen mit EF Core

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
            SortProductsByPrice(context);
            GetProductsByCategory(context, "Electronics");
            CountProductsInCategories(context);
        }
    }

    private static void SortProductsByPrice(AppDbContext context)
    {
        var sortedProducts = context.Products.OrderBy(p => p.Price).ToList();
        Console.WriteLine("Products sorted by price:");
        foreach (var product in sortedProducts)
        {
            Console.WriteLine($"Product: {product.Name}, Price: {product.Price}");
        }
    }

    private static void GetProductsByCategory(AppDbContext context, string categoryName)
    {
        var products = context.Products
            .Include(p => p.Category)
            .Where(p => p.Category.Name == categoryName)
            .ToList();
        
        Console.WriteLine($"Products in category '{categoryName}':");
        foreach (var product in products)
        {
            Console.WriteLine($"Product: {product.Name}, Price: {product.Price}");
        }
    }

    private static void CountProductsInCategories(AppDbContext context)
    {
        var productCounts = context.Categories
            .Include(c => c.Products)
            .Select(c => new 
            {
                Category = c.Name, 
                ProductCount = c.Products.Count()
            }).ToList();

        Console.WriteLine("Product counts per category:");
        foreach (var category in productCounts)
        {
            Console.WriteLine($"Category: {category.Category}, Product Count: {category.ProductCount}");
        }
    }
}
```