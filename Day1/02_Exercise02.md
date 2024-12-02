# Übung 2: Erweitertes Arbeiten mit Generischen Methoden und Constraints

## Anweisungen

1. **Erstellen Sie eine generische Methode `CompareAndSwap<T>`:**
   - Diese Methode soll zwei `ref`-Parameter von Typ `T` akzeptieren.
   - Die Methode soll die Objekte nur dann vertauschen, wenn das erste Objekt größer ist als das zweite.

2. **Verwenden Sie Constraints:**
   - Nutzen Sie den `where`-Constraint, um sicherzustellen, dass `T` das `IComparable<T>`-Interface implementiert.

3. **Erstellen Sie eine Hilfsmethode `PrintValues`:**
   - Diese Methode soll zwei generische Werte entgegennehmen und sie in der Konsole ausgeben, um den Vorher-Nachher-Zustand zu überprüfen.

4. **Testen Sie die Methode:**
   - Verwenden Sie die `CompareAndSwap`-Methode mit verschiedenen Datentypen (z.B. `int`, `string`) und mit verschiedenen Ausgangszuständen.

## Lösungshinweise

- Verwenden Sie `ref` für die Parameter in der `CompareAndSwap`-Methode, um einen tatsächlichen Swap der Originalwerte zu ermöglichen.
- Die `CompareTo`-Methode wird verwendet, um zu entscheiden, ob ein Swap erforderlich ist.
- Nutzen Sie die Hilfsmethode `PrintValues`, um im Vorfeld und nach dem Aufruf von `CompareAndSwap` zu überprüfen, ob die Werte korrekt ausgetauscht wurden oder nicht.

## Hilfreiche MSDN-Ressourcen

- [Generics Overview](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/)
- [Generic Constraints](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/constraints-on-type-parameters)
- [IComparable Interface](https://docs.microsoft.com/en-us/dotnet/api/system.icomparable)
- [ref Keyword](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/ref)
- [Methods](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods)