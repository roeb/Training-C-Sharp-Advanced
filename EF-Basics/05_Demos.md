# Demos

## Code First

### Schritt 1: Projekt einrichten

1. Erstelle ein neues Konsolenprojekt:

   ```bash
   dotnet new console -n EfCoreDemo
   cd EfCoreDemo
   ```

2. Füge die erforderlichen NuGet-Pakete hinzu:

   ```bash
   dotnet add package Microsoft.EntityFrameworkCore
   dotnet add package Microsoft.EntityFrameworkCore.Sqlite
   dotnet add package Microsoft.EntityFrameworkCore.Tools
   ```

### Schritt 2: Definiere die Entitäten

Lege zuerst die Entitätsklassen an, die die Tabellen in der Datenbank repräsentieren.

```csharp
// Models/Student.cs
namespace EfCoreDemo.Models
{
    public class Student
    {
        public int StudentId { get; set; }
        public string Name { get; set; }
        public int Age { get; set; }

        // Navigation property for relationships
        public List<Enrollment> Enrollments { get; set; } = new List<Enrollment>();
    }
}

// Models/Course.cs
namespace EfCoreDemo.Models
{
    public class Course
    {
        public int CourseId { get; set; }
        public string Title { get; set; }
        public string Description { get; set; }

        // Navigation property for relationships
        public List<Enrollment> Enrollments { get; set; } = new List<Enrollment>();
    }
}

// Models/Enrollment.cs
namespace EfCoreDemo.Models
{
    public class Enrollment
    {
        public int EnrollmentId { get; set; }
        public int StudentId { get; set; }
        public Student Student { get; set; }  // Navigation property
        public int CourseId { get; set; }
        public Course Course { get; set; }    // Navigation property
    }
}
```

### Schritt 3: Definiere den DbContext

Erstelle den `SchoolContext`, der den Zusammenhang der Datenbank definiert.

```csharp
// Data/SchoolContext.cs
using Microsoft.EntityFrameworkCore;
using EfCoreDemo.Models;

namespace EfCoreDemo.Data
{
    public class SchoolContext : DbContext
    {
        public DbSet<Student> Students { get; set; }
        public DbSet<Course> Courses { get; set; }
        public DbSet<Enrollment> Enrollments { get; set; }

        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            // Verwende SQLite als Datenbank
            optionsBuilder.UseSqlite("Data Source=school.db");
        }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<Enrollment>()
                .HasKey(e => new { e.EnrollmentId });

            modelBuilder.Entity<Enrollment>()
                .HasOne(e => e.Student)
                .WithMany(s => s.Enrollments)
                .HasForeignKey(e => e.StudentId);

            modelBuilder.Entity<Enrollment>()
                .HasOne(e => e.Course)
                .WithMany(c => c.Enrollments)
                .HasForeignKey(e => e.CourseId);
        }
    }
}
```

### Schritt 4: Migration erstellen und Datenbank aufbauen

1. Führe die Migrationen aus, um die Datenbankstruktur zu erstellen:

   ```bash
   dotnet ef migrations add InitialCreate
   dotnet ef database update
   ```

### Schritt 5: Daten hinzufügen und abfragen

Schreibe die Logik zum Hinzufügen und Abrufen von Daten in der `Program.cs` Datei:

```csharp
// Program.cs
using System;
using System.Linq;
using EfCoreDemo.Data;
using EfCoreDemo.Models;

class Program
{
    static void Main()
    {
        using var context = new SchoolContext();

        // Daten hinzufügen
        var student = new Student { Name = "John Doe", Age = 20 };
        var course = new Course { Title = "Mathematics 101", Description = "Introduction to Mathematics" };

        context.Students.Add(student);
        context.Courses.Add(course);
        context.SaveChanges();

        var enrollment = new Enrollment { StudentId = student.StudentId, CourseId = course.CourseId };
        context.Enrollments.Add(enrollment);
        context.SaveChanges();

        // Daten abfragen
        var students = context.Students
            .Select(s => new 
            { 
                s.Name, 
                s.Age, 
                Courses = s.Enrollments.Select(e => e.Course.Title) 
            })
            .ToList();

        Console.WriteLine("Liste der Studenten und ihrer Kurse:");
        foreach (var s in students)
        {
            Console.WriteLine($"Student: {s.Name}, Alter: {s.Age}");
            Console.WriteLine("Kurse:");
            foreach (var courseTitle in s.Courses)
            {
                Console.WriteLine($"- {courseTitle}");
            }
        }
    }
}
```

### Schritt 4: Neue Entität `Teacher` definieren

Zuerst erstellen wir eine neue Entitätsklasse für Lehrer:

```csharp
// Models/Teacher.cs
namespace EfCoreDemo.Models
{
    public class Teacher
    {
        public int TeacherId { get; set; }
        public string Name { get; set; }
        public string Subject { get; set; }

        // Navigation property for relationships
        public List<Course> Courses { get; set; } = new List<Course>();
    }
}
```

### Schritt 5: Update des `DbContext`

Fügen Sie die `DbSet<Teacher>`-Eigenschaft zum `SchoolContext` hinzu und konfigurieren Sie die Beziehung zwischen `Teacher` und `Course`.

```csharp
// Data/SchoolContext.cs

using Microsoft.EntityFrameworkCore;
using EfCoreDemo.Models;

namespace EfCoreDemo.Data
{
    public class SchoolContext : DbContext
    {
        public DbSet<Student> Students { get; set; }
        public DbSet<Course> Courses { get; set; }
        public DbSet<Enrollment> Enrollments { get; set; }
        public DbSet<Teacher> Teachers { get; set; } // Neue DbSet für Teacher

        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            optionsBuilder.UseSqlite("Data Source=school.db");
        }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<Enrollment>()
                .HasKey(e => new { e.EnrollmentId });

            modelBuilder.Entity<Enrollment>()
                .HasOne(e => e.Student)
                .WithMany(s => s.Enrollments)
                .HasForeignKey(e => e.StudentId);

            modelBuilder.Entity<Enrollment>()
                .HasOne(e => e.Course)
                .WithMany(c => c.Enrollments)
                .HasForeignKey(e => e.CourseId);

            // Konfiguration der Lehrer-Kurs-Beziehung
            modelBuilder.Entity<Course>()
                .HasOne<Teacher>()
                .WithMany(t => t.Courses)
                .HasForeignKey(c => c.CourseId);
        }
    }
}
```

### Schritt 6: Migration erstellen und auf die Datenbank anwenden

Führe eine neue Migration aus, um die Änderungen in der Datenbankstruktur zu reflektieren:

1. Erstelle eine neue Migration:

   ```bash
   dotnet ef migrations add AddTeacher
   ```

2. Aktualisiere die Datenbank mit der neuen Migration:

   ```bash
   dotnet ef database update
   ```

### Schritt 7: Anpassen des Codes zur Demonstration der neuen Entität

Aktualisiere die `Program.cs`, um Lehrer zu erstellen und ihnen Kurse zuzuweisen.

```csharp
// Program.cs
using System;
using System.Linq;
using EfCoreDemo.Data;
using EfCoreDemo.Models;

class Program
{
    static void Main()
    {
        using var context = new SchoolContext();

        // Lehrer hinzufügen
        var teacher = new Teacher { Name = "Alice Johnson", Subject = "Mathematics" };
        context.Teachers.Add(teacher);
        context.SaveChanges();

        // Kurs dem Lehrer zuweisen
        var course = context.Courses.FirstOrDefault();
        if (course != null)
        {
            teacher.Courses.Add(course);
            context.SaveChanges();
        }

        // Lehrer und zugehörige Kurse abfragen
        var teachers = context.Teachers
            .Select(t => new 
            { 
                t.Name, 
                t.Subject,
                Courses = t.Courses.Select(c => c.Title)
            })
            .ToList();

        Console.WriteLine("Liste von Lehrern und ihren Kursen:");
        foreach (var t in teachers)
        {
            Console.WriteLine($"Lehrer: {t.Name}, Fach: {t.Subject}");
            Console.WriteLine("Kurse:");
            foreach (var courseTitle in t.Courses)
            {
                Console.WriteLine($"- {courseTitle}");
            }
        }
    }
}
```

### Schritt 8: Transaktionen

```csharp
using System;
using EfCoreDemo.Data;
using EfCoreDemo.Models;
using Microsoft.EntityFrameworkCore;

class Program
{
    static void Main()
    {
        using var context = new SchoolContext();

        // Beginne eine Transaktion
        using var transaction = context.Database.BeginTransaction();
        
        try
        {
            // Neuen Studenten hinzufügen
            var student = new Student { Name = "Jane Doe", Age = 22 };
            context.Students.Add(student);
            context.SaveChanges();

            // Neuen Kurs hinzufügen
            var course = new Course { Title = "Physics 101", Description = "Introduction to Physics" };
            context.Courses.Add(course);
            context.SaveChanges();

            // Einschreibung hinzufügen
            var enrollment = new Enrollment { StudentId = student.StudentId, CourseId = course.CourseId };
            context.Enrollments.Add(enrollment);
            context.SaveChanges();
            
            // Transaktion übernehmen, wenn alles erfolgreich war
            transaction.Commit();
            Console.WriteLine("Transaktion erfolgreich abgeschlossen und übernommen.");
        }
        catch (Exception ex)
        {
            // Transaktion zurückrollen bei einem Fehler
            transaction.Rollback();
            Console.WriteLine($"Transaktion fehlgeschlagen. Änderungen wurden zurückgesetzt: {ex.Message}");
        }
    }
}
```

## Db First

### Voraussetzungen

- Eine bestehende Datenbank. Für dieses Beispiel gehen wir davon aus, dass wir eine Datenbank mit den Tabellen `Student`, `Course` und `Enrollment` haben.
- Installiertes Entity Framework Core und die EF Tools in deinem Projekt.

### Schritt-für-Schritt-Leitfaden

#### Schritt 1: Erstelle und konfiguriere das Projekt

1. **Neues Konsolenprojekt erstellen:**

   ```bash
   dotnet new console -n EfCoreDbFirstDemo
   cd EfCoreDbFirstDemo
   ```

2. **NuGet-Pakete hinzufügen:**

   - Installiere EF Core und die nötigen Tools:

   ```bash
   dotnet add package Microsoft.EntityFrameworkCore
   dotnet add package Microsoft.EntityFrameworkCore.Sqlite
   dotnet add package Microsoft.EntityFrameworkCore.Design
   ```

#### Schritt 2: Scaffold den `DbContext` und Entitäten

Verwende das `dotnet ef` Tool, um den `DbContext` und die Entitäten aus der Datenbank zu generieren.

1. **EF Core Tools installieren (falls noch nicht geschehen):**

   ```bash
   dotnet tool install --global dotnet-ef
   ```

2. **Scaffold den Datenbankkontext und die Modelle:**

   Verwende das folgende Kommando:

   ```bash
   dotnet ef dbcontext scaffold "Data Source=your-database-file.db" Microsoft.EntityFrameworkCore.Sqlite --output-dir Models
   ```

   Dabei ist `your-database-file.db` der Pfad zu deiner SQLite-Datenbank. Dies generiert die Entitätsklassen und den Kontext innerhalb des `Models`-Verzeichnisses.

#### Schritt 3: Implementiere die Logik im Hauptprogramm

Jetzt, da du den Kontext und die Modelle generiert hast, kannst du mit der Datenbank interagieren. Hier ein einfaches Beispiel zur Interaktion mit den generierten Entitäten.

```csharp
// Program.cs
using System;
using System.Linq;
using EfCoreDbFirstDemo.Models;

class Program
{
    static void Main()
    {
        using var context = new YourDbContext();

        // Beispiel: Abfrage aller Studenten
        var students = context.Students.ToList();

        Console.WriteLine("Liste aller Studenten:");
        foreach (var student in students)
        {
            Console.WriteLine($"Student ID: {student.StudentId}, Name: {student.Name}, Alter: {student.Age}");
        }
    }
}
```