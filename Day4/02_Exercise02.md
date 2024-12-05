# Übung 2: Singleton-Entwurfsmuster

## Anweisungen

1. **Erstellen Sie eine Klasse `Singleton`:**
   - Implementieren Sie einen privaten, statischen Feld `instance` vom Typ der Klasse.
   - Erstellen Sie einen privaten Konstruktor, sodass die Klasse nicht von außen instanziiert werden kann.

2. **Erstellen Sie eine statische Methode `GetInstance`:**
   - Diese Methode gibt die einzige Instanz der Klasse zurück und erstellt sie, falls sie noch nicht existiert.

3. **Fügen Sie der Klasse eine Beispielmethode hinzu:**
   - Implementieren Sie `ShowMessage`, die eine einfache Nachricht in der Konsole ausgibt, um zu demonstrieren, dass dieselbe Instanz verwendet wird.

4. **Testen Sie das Singleton in der `Main`-Methode:**
   - Rufen Sie `GetInstance` und dann `ShowMessage` auf und zeigen Sie, dass mehrere Aufrufe dieselbe Instanz verwenden.

## Lösungshinweise

- Verwenden Sie `lock`-Schlüsselwort, um den Zugriff auf die Instance-Erstellung in einer Multithreading-Umgebung zu sichern.
- Achten Sie darauf, dass der Konstruktor privat ist, um direkte Instanziierung zu verhindern.
- `Lazy<T>` könnte ebenfalls verwendet werden, um die Instanziierung bei Bedarf zu optimieren.

## MSDN Links

### C# Schlüsselkonzepte und Grundlagen

- **Konstruktoren:**
  - [Constructor (C# Reference)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/constructors)

- **Static Classes and Static Class Members:**
  - [Static Classes and Static Class Members](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members)

- **C# Lock Statement:**
  - [lock Statement](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/lock)

### Thread-Sicherheit

- **Threading in .NET:**
  - [Threading (Task Parallel Library)](https://learn.microsoft.com/en-us/dotnet/standard/threading/)
  
- **Locks und Synchronisation in .NET:**
  - [lock Statement](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/lock)
