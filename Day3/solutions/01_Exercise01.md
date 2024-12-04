# Übung 1: Asynchrone Webservice-Anfrage mit `async` und `await`

## Komplette Lösung

```csharp
using System;
using System.Collections.Generic;
using System.Net.Http;
using System.Text.Json;
using System.Threading.Tasks;

public class Post
{
    public int UserId { get; set; }
    public int Id { get; set; }
    public string Title { get; set; }
    public string Body { get; set; }
}

public class Program
{
    public static async Task Main()
    {
        List<Post> posts = await FetchDataAsync();
        DisplayPostTitles(posts);
    }

    public static async Task<List<Post>> FetchDataAsync()
    {
        using (HttpClient client = new HttpClient())
        {
            Console.WriteLine("Sending request to web service...");
            HttpResponseMessage response = await client.GetAsync("https://jsonplaceholder.typicode.com/posts");
            response.EnsureSuccessStatusCode();

            string responseBody = await response.Content.ReadAsStringAsync();
            List<Post> posts = JsonSerializer.Deserialize<List<Post>>(responseBody);

            Console.WriteLine("Data fetch completed.");
            return posts;
        }
    }

    public static void DisplayPostTitles(List<Post> posts)
    {
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"Title {i + 1}: {posts[i].Title}");
        }
    }
}
```