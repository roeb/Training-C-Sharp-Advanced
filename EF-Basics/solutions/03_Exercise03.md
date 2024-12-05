# Übung 3: Beziehungen und Navigationseigenschaften

## Komplette Lösung

```csharp
using Microsoft.EntityFrameworkCore;
using System;
using System.Collections.Generic;
using System.Linq;

public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
    public int CategoryId { get; set; }
    public Category Category { get; set; }
}

public class Category
{
    public int Id { get; set; }
    public string Name { get; set; }
    public ICollection<Product> Products { get; set; } = new List<Product>();
}

public class AppDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }
    public DbSet<Category> Categories { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        // Ersetzen Sie "YourConnectionString" durch Ihre tatsächliche Verbindungszeichenkette.
        optionsBuilder.UseSqlServer("YourConnectionString");
    }
}

public class Program
{
    public static void Main()
    {
        using (var context = new AppDbContext())
        {
            context.Database.EnsureCreated();
            AddCategoryWithProducts(context);
            GetCategoriesWithProducts(context);
        }
    }

    private static void AddCategoryWithProducts(AppDbContext context)
    {
        var category = new Category { Name = "Electronics" };
        category.Products.Add(new Product { Name = "Laptop", Price = 999.99m });
        category.Products.Add(new Product { Name = "Smartphone", Price = 599.99m });

        context.Categories.Add(category);
        context.SaveChanges();
        Console.WriteLine("Category with products added.");
    }

    private static void GetCategoriesWithProducts(AppDbContext context)
    {
        var categoriesWithProducts = context.Categories.Include(c => c.Products).ToList();
        
        foreach (var category in categoriesWithProducts)
        {
            Console.WriteLine($"Category: {category.Name}");
            foreach (var product in category.Products)
            {
                Console.WriteLine($"- Product: {product.Name}, Price: {product.Price}");
            }
        }
    }
}
```