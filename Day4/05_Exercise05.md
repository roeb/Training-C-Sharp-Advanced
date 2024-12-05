# Übung 5: Strategy-Entwurfsmuster

## Anweisungen

1. **Definieren Sie eine Schnittstelle `IStrategy`:**
   - Implementieren Sie eine Methode `Execute()`.

2. **Erstellen Sie konkrete Strategien `ConcreteStrategyA` und `ConcreteStrategyB`:**
   - Jede Implementierung von `Execute` sollte eine spezifische Ausführungsmeldung in der Konsole ausgeben.

3. **Erstellen Sie eine `Context`-Klasse:**
   - Diese Klasse sollte ein Feld für die `IStrategy` enthalten.
   - Implementieren Sie eine Methode `SetStrategy(IStrategy strategy)` zur Festlegung der Strategie.
   - Implementieren Sie die Methode `ExecuteStrategy()`, welche die aktuelle Strategie anwendet.

4. **Testen Sie das Muster in der `Main`-Methode:**
   - Erstellen Sie eine `Context`-Instanz.
   - Setzen Sie verschiedene Strategien und führen Sie jeweils `ExecuteStrategy()` aus, um die Änderung der Strategie zu demonstrieren.

## Lösungshinweise

- Die `Context`-Klasse sollte bei der Ausführung der Strategie keine Kenntnis über die konkreten Strategien haben.
- Das Muster ermöglicht die Änderung des Algorithmus zur Laufzeit, indem es einfach die Strategie im `Context` ändert.
- Jede Strategie sollte klar definierte Aktionen in `Execute` ausführen, um das Konzept zu verdeutlichen.

## MSDN Links

### Schnittstellen

- **Interfaces in C#:**
  - [Interfaces (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/interfaces/)

### Klassen und Objekte

- **Klassendefinition und Mitglieder:**
  - [Classes and Objects in C#](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/classes)
  - [Classes (C# Reference)](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/class)

### Methoden

- **Methoden in C#:**
  - [Methods (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods)

### Weitere Programmierkonzepte

- **Using Statements:**
  - [using Directive (C# Reference)](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/using-directive)