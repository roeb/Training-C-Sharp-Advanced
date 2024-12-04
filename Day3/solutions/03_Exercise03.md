# Übung 3: LINQ-Abfragen auf Webservice-Daten

## Komplette Lösung

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net.Http;
using System.Text.Json;
using System.Threading.Tasks;

public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Username { get; set; }
    public string Email { get; set; }
    public Address Address { get; set; }
    public Company Company { get; set; }
}

public class Address
{
    public string City { get; set; }
}

public class Company
{
    public string Name { get; set; }
}

public class Program
{
    public static async Task Main()
    {
        List<User> users = await FetchUsersAsync();

        // Abfrage 1: Benutzer mit bestimmtem Domainnamen in der E-Mail
        var domainUsers = users.Where(u => u.Email.Contains("@biz"));
        Console.WriteLine("Users with @biz in email:");
        foreach (var user in domainUsers)
        {
            Console.WriteLine($"{user.Name} - {user.Email}");
        }

        // Abfrage 2: Gruppieren nach Stadt
        var usersByCity = users.GroupBy(u => u.Address.City);
        Console.WriteLine("\nUsers grouped by city:");
        foreach (var group in usersByCity)
        {
            Console.WriteLine(group.Key + ":");
            foreach (var user in group)
            {
                Console.WriteLine($"  {user.Name}");
            }
        }

        // Abfrage 3: Häufigsten Namenpräfixe in den Unternehmen
        var commonCompanyPrefixes = users
            .GroupBy(u => u.Company.Name.Split(' ').LastOrDefault())
            .OrderByDescending(g => g.Count())
            .Select(g => new
            {
                Suffix = g.Key,
                Count = g.Count()
            });

        Console.WriteLine("\nMost common company name suffixes:");
        foreach (var prefix in commonCompanyPrefixes)
        {
            Console.WriteLine($"{prefix.Suffix} - {prefix.Count}");
        }

        // Abfrage 4: Sortieren nach Name, dann Benutzername
        var sortedUsers = users.OrderBy(u => u.Name).ThenBy(u => u.Username);
        Console.WriteLine("\nUsers sorted by name and username:");
        foreach (var user in sortedUsers)
        {
            Console.WriteLine($"{user.Name} ({user.Username})");
        }
    }

    public static async Task<List<User>> FetchUsersAsync()
    {
        using (HttpClient client = new HttpClient())
        {
            HttpResponseMessage response = await client.GetAsync("https://jsonplaceholder.typicode.com/users");
            response.EnsureSuccessStatusCode();

            string responseBody = await response.Content.ReadAsStringAsync();
            List<User> users = JsonSerializer.Deserialize<List<User>>(responseBody);

            return users;
        }
    }
}
```