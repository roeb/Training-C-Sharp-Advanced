# Übung 1: Modell- und Datenbankerstellung mit EF Core

## Komplette Lösung

```csharp
using Microsoft.EntityFrameworkCore;
using System;

public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}

public class AppDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        // Ersetzen Sie "YourConnectionString" durch Ihre tatsächliche SQL Server-Verbindungszeichenkette
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
            Console.WriteLine("Database created and ready to use.");
        }
    }
}
```