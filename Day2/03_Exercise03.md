# Übung 2: Verwendung von Attributen und Reflection

## Anweisungen

1. **Definieren Sie ein benutzerdefiniertes Attribut `InfoAttribute`:**
   - Erstellen Sie eine Klasse `InfoAttribute`, die von `System.Attribute` abgeleitet wird.
   - Fügen Sie eine Eigenschaft `Description` hinzu, die über den Konstruktor gesetzt werden kann.

2. **Wenden Sie das Attribut auf Klassen an:**
   - Dekorieren Sie zwei oder mehr Klassen mit `InfoAttribute` und geben Sie eine passende Beschreibung an.

3. **Verwenden Sie Reflection zur Laufzeit:**
   - Implementieren Sie eine Methode, die alle Klassen des aktuellen Assemblys durchsucht.
   - Finden Sie alle Klassen, die mit `InfoAttribute` versehen sind, und geben Sie deren Beschreibung aus.

## Lösungshinweise

1. **Benutzerdefiniertes Attribut:**
   - Verwenden Sie `[AttributeUsage(AttributeTargets.Class)]` um das Attribut nur auf Klassen anzuwenden.
   - Nutzen Sie einen Konstruktor, um die `Description`-Eigenschaft zu initialisieren.

2. **Anwendung des Attributs:**
   - Dekorieren Sie die zu prüfenden Klassen mit `[Info("Beschreibung")]`.

3. **Reflection verwenden:**
   - Verwenden Sie `Assembly.GetExecutingAssembly()` und `GetTypes()`, um alle Typen zu erhalten.
   - Für jede Klasse prüfen Sie mit `GetCustomAttribute<InfoAttribute>()`, ob das Attribut vorhanden ist.

## Hilfreiche MSDN-Ressourcen

- [Custom Attributes](https://docs.microsoft.com/en-us/dotnet/standard/attributes/writing-custom-attributes)
- [AttributeTargets Enum](https://docs.microsoft.com/en-us/dotnet/api/system.attributetargets)
- [Reflection in .NET](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/reflection)
- [Assembly.GetExecutingAssembly Method](https://docs.microsoft.com/en-us/dotnet/api/system.reflection.assembly.getexecutingassembly)
- [GetCustomAttribute Method](https://docs.microsoft.com/en-us/dotnet/api/system.reflection.customattributeextensions.getcustomattribute)