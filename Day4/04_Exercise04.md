# Übung 4: Observer-Entwurfsmuster

## Anweisungen

1. **Definieren Sie eine Schnittstelle `IObserver`:**
   - Erstellen Sie eine Methode `Update(string message)`, die Benachrichtigungen empfängt.

2. **Definieren Sie eine Schnittstelle `ISubject`:**
   - Implementieren Sie Methoden `Register(IObserver observer)`, `Unregister(IObserver observer)`, und `NotifyObservers(string message)`.

3. **Erstellen Sie die Klasse `NewsAgency` als `ISubject`:**
   - Implementieren Sie die Methoden, um Beobachter hinzuzufügen, zu entfernen und zu benachrichtigen.
   - Bewahren Sie eine Liste der registrierten Beobachter auf.

4. **Implementieren Sie konkrete Beobachterklassen `NewsChannel`:**
   - Diese Klassen implementieren `IObserver` und definieren die `Update`-Methode, die die empfangene Nachricht in der Konsole ausgibt.

5. **Testen Sie das Muster in der `Main`-Methode:**
   - Erzeugen Sie eine `NewsAgency`-Instanz.
   - Erstellen und registrieren Sie mehrere `NewsChannel`-Beobachter.
   - Demonstrieren Sie die Benachrichtigung der Beobachter durch Veröffentlichungen von `NewsAgency`.

## Lösungshinweise

- Nutzen Sie eine `List<IObserver>` in der `NewsAgency`, um alle Beobachter zu verfolgen.
- Stellen Sie sicher, dass bei `NotifyObservers` alle registrierten Beobachter in der Liste benachrichtigt werden.
- Eine `Console.WriteLine` in `Update` zeigt, dass Nachrichten korrekt übertragen werden.

## MSDN Links

### Schnittstellen

- **Interfaces in C#:**
  - [Interfaces (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/interfaces/)

### Sammlungen

- **List Collection:**
  - [List<T> Class](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1)

### Ereignisse und Delegates

- **Events and Delegates:**
  - [Events (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/events/)
  - [Delegates (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/)

### Klassen und Methoden

- **Class Definition and Members:**
  - [Classes and Objects in C#](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/classes)
  - [Methods (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods)