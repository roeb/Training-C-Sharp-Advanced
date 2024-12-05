# Übung 3: Factory-Entwurfsmuster

## Anweisungen

1. **Erstellen Sie eine Schnittstelle `IShape`:**
   - Definieren Sie eine Methode `Draw()`, die die Implementierung zum Zeichnen der Form enthält.

2. **Implementieren Sie konkrete Klassen `Circle`, `Rectangle`, und `Square`:**
   - Jede Klasse implementiert die `IShape`-Schnittstelle.
   - Implementieren Sie die `Draw`-Methode, sodass jede Klasse eine spezifische Nachricht in der Konsole ausgibt (z.B. "Drawing a Circle").

3. **Erstellen Sie eine `ShapeFactory`-Klasse:**
   - Implementieren Sie eine Methode `GetShape(string shapeType)`, die je nach `shapeType` eine Instanz von `Circle`, `Rectangle` oder `Square` zurückgibt.

4. **Verwenden Sie die `ShapeFactory` in der `Main`-Methode:**
   - Fordern Sie verschiedene Formen durch die Factory an und rufen Sie `Draw` auf, um die Funktionalität zu demonstrieren.

## Lösungshinweise

- Nutzen Sie switch-Anweisungen oder Dictionary-Mapping in der Factory, um die richtige Objektinstanz basierend auf dem Eingabetyp bereitzustellen.
- Der Factory-Ansatz erleichtert die Erweiterbarkeit; bei neuen Formen muss lediglich die Factory und die neue Klasse implementiert werden.
- Stellen Sie sicher, dass eine Standard- oder Fehlerbedingung für unbekannte Formtypen existiert.

## MSDN Links

### Schnittstellen und Implementierung

- **Interfaces in C#:**
  - [Interfaces (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/interfaces/)

### Klassen und Methoden

- **Klassendefinition und -Implementierung:**
  - [Classes and Objects in C#](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/classes)

- **Methoden in C#:**
  - [Methods (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods)

### Kontrollstrukturen

- **Switch Statement:**
  - [switch Statement (C# Reference)](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/select-statement)

### Dictionary für Mapping

- **Dictionary-Klasse in C#:**
  - [Dictionary<TKey,TValue> Class](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2)

### Erweiterbarkeit und Fehlerbehandlung

- **Exception Handling:**
  - [Exception Handling (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/exceptions/)