# Übung 1: Implementierung von Events mit Parametern

## Anweisungen

1. **Erstellen Sie die Klasse `Publisher`:**
   - Fügen Sie in der Klasse ein Event `DataProcessed` hinzu.
   - Definieren Sie einen Delegaten `DataProcessedEventHandler`, der einen `string`-Parameter akzeptiert.

2. **Implementieren Sie die Methode `ProcessData`:**
   - Diese Methode soll einige Daten verarbeiten. Simulieren Sie die Datenverarbeitung durch eine Konsolenausgabe.
   - Nach der Verarbeitung soll die Methode das `DataProcessed`-Event auslösen und eine Nachricht über den Verarbeitungserfolg als `string` übergeben.

3. **Erstellen Sie die Klasse `Subscriber`:**
   - Fügen Sie eine Methode `OnDataProcessed` hinzu, welche die `DataProcessed`-Event-Nachricht entgegennimmt und die Nachricht ausgibt.

4. **Verbinden Sie die `Subscriber`-Methode mit dem `Publisher`-Event:**
   - Erzeugen Sie Instanzen von `Publisher` und `Subscriber`.
   - Abonnieren Sie das `DataProcessed`-Event mit der Methode `OnDataProcessed`.

5. **Testen Sie das Event:**
   - Rufen Sie die `ProcessData`-Methode in `Publisher` auf und beobachten Sie die Ausführung des Events mit der übergebenen Nachricht.

## Lösungshinweise

1. **Delegat und Event:**
   - Definieren Sie einen Delegaten `DataProcessedEventHandler` mit einem `string`-Parameter.
   - Deklarieren Sie das Event `DataProcessed` basierend auf diesem Delegaten.

2. **Datenverarbeitung:**
   - Simulieren Sie die Datenverarbeitung in `ProcessData`.
   - Lösen Sie das Event mit einer Nachricht, nachdem die Verarbeitung abgeschlossen ist.

3. **Event auslösen:**
   - Nutzen Sie `?.Invoke(message)`, um das Event auszulösen, wenn es Abonnenten gibt.

4. **Abonnent:**
   - Implementieren Sie `OnDataProcessed` im `Subscriber`, um die Nachricht auszugeben.

5. **Verbindung:**
   - Verbinden Sie das Event mit `+=` im `Main`-Programm.

## Hilfreiche MSDN-Ressourcen

- [Events](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/events/)
- [Delegates](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/)
- [Event Handling](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/events/how-to-raise-and-consume-events)
- [?. (Null-conditional operator)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/member-access-operators#null-conditional-operators--and-)
- [Console Class](https://docs.microsoft.com/en-us/dotnet/api/system.console)