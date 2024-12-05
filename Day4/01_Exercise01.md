# Übung 1: Dependency Injection mit .NET-Built-In Container

## Anweisungen

1. **Erstellen Sie eine Dienstschnittstelle `ILoggingService`:**
   - Definieren Sie eine Methode `Log(string message)`.

2. **Implementieren Sie die Schnittstelle in einer Klasse `ConsoleLoggingService`:**
   - Implementieren Sie `Log`, um Nachrichten in die Konsole auszugeben.

3. **Erstellen Sie eine weitere Dienstschnittstelle `IDataService`:**
   - Definieren Sie eine Methode `GetData()` die eine Liste von `string` zurückgibt.

4. **Implementieren Sie diese Schnittstelle in einer Klasse `SimpleDataService`:**
   - Implementieren Sie `GetData` mit einigen Beispielstrings.

5. **Konfigurieren Sie den DI-Container:**
   - Verwenden Sie den `ServiceCollection` für die Registrierung der Dienstschnittstellen und Implementierungen.

6. **Integrieren Sie die injizierten Dienste in eine Anwendung:**
   - Erstellen Sie eine Klasse `Application` mit Konstruktorinjektion für die Dienste.
   - Verwenden Sie die Dienste in der `Run`-Methode.

7. **Initialisieren Sie die Anwendung in `Main`:**
   - Rufen Sie die `Run`-Methode auf, um die Logik der Anwendung zu demonstrieren.

## Lösungshinweise

- Verwenden Sie die `ServiceCollection`-Klasse, um einen DI-Container zu erstellen und die Dienste zu registrieren.
- `AddSingleton` oder `AddScoped` können für die Dienstregistrierung verwendet werden, abhängig davon, ob Sie eine einzige Instanz oder eine pro Anforderung erstellen möchten.
- Vergessen Sie nicht, `BuildServiceProvider` aufzurufen, um den DI-Container zu erstellen, bevor Sie die Dienste aufrufen.

## MSDN Links

### Dependency Injection in .NET

- **Übersicht zu Dependency Injection in .NET**:
  - [Dependency injection in .NET](https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection)

### Erstellen und Verwenden von Schnittstellen

- **Schnittstellen in C#:**
  - [Interfaces (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/interfaces/)

### Dienstregistrierung und Konfiguration

- **ServiceCollection und ServiceProvider:**
  - [ServiceCollection Class](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.servicecollection)
  - [ServiceProvider Class](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovider)

- **Dienstregistrierungsmethoden (`AddSingleton`, `AddScoped`, `AddTransient`):**
  - [Dependency injection in .NET](https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection#service-lifetimes-and-registration-options)

### Konstruktorinjektion

- **DI und Konstruktoren:**
  - [Register and use interface in ASP.NET Core DI (constructor injection)](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection#register-an-interface-with-static-data)