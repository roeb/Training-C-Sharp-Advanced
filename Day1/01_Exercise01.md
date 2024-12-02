# Übung 1: Generische Klasse für eine Sammlung

## Anweisungen

1. **Erstellen Sie die generische Klasse `GenericCollection<T>`:**
   - Definieren Sie ein Feld oder eine Liste, um die Elemente der generischen Sammlung intern zu speichern.

2. **Implementieren Sie die Methode `Add`:**
   - Diese Methode soll ein Element vom Typ `T` zur Sammlung hinzufügen.

3. **Implementieren Sie die Methode `Remove`:**
   - Diese Methode soll ein Element vom Typ `T` aus der Sammlung entfernen und ein `bool` zurückgeben, das angibt, ob der Vorgang erfolgreich war.

4. **Implementieren Sie die Methode `Get`:**
   - Diese Methode soll das `T`-Element an einer angegebenen Indexposition zurückgeben.

5. **Testen Sie Ihre Klasse:**
   - Erstellen Sie mehrere Instanzen von `GenericCollection<T>` mit unterschiedlichen Datentypen (z.B. `int`, `string`) und testen Sie die Methoden `Add`, `Remove` und `Get`.

## Lösungshinweise

- Nutzen Sie eine interne Liste oder ein Array, um die Elemente von `GenericCollection<T>` zu speichern.
- Denken Sie daran, dass die Methoden von List (wie `Add`, `Remove`, `Count`) nützlich sein können, wenn Sie `List<T>` verwenden.
- Verwenden Sie die `IndexOutOfRangeException`, um ungültige Indexzugriffe in der `Get`-Methode abzufangen.
- Sie können den `Remove`-Methode Erfolg überprüfen, indem Sie die Rückgabe der `List<T>.Remove`-Methode nutzen.

## Hilfreiche MSDN-Ressourcen

- [Generics Overview](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/)
- [List<T> Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1)
- [Exception Handling](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/exceptions/)
- [Indexers](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/indexers/)
- [Methods](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods)