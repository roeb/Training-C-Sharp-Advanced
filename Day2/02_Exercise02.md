# Übung: Implementierung eines Temperaturüberwachungssystems

In dieser Übung wirst du ein Temperaturüberwachungssystem implementieren. Deine Aufgabe ist es, eine Klasse `TemperatureSensor` zu erstellen, die ein Event `TemperatureThresholdReached` auslöst, wenn eine simulierte Temperatur einen definierten Schwellenwert überschreitet. Zusätzlich entwickelst du eine `AlarmSystem`-Klasse, die auf dieses Event reagiert und eine Warnung ausgibt. Diese Übung hilft dir, den Einsatz von Delegates und Events in der Entwicklung von ereignisgesteuertem Code zu verstehen und anzuwenden.

## Anweisungen

1. **Erstellen Sie eine Klasse `TemperatureSensor`:**
   - Diese Klasse sollte ein Event `TemperatureThresholdReached` haben.
   - Definieren Sie einen Delegaten `TemperatureThresholdReachedHandler`, der einen `float`-Parameter für die Temperatur akzeptiert.

2. **Implementieren Sie eine Methode `ReadTemperature`:**
   - Diese Methode soll zufällig Temperaturen simulieren und das `TemperatureThresholdReached`-Event auslösen, wenn eine Temperatur einen definierten Schwellenwert erreicht oder überschreitet.

3. **Erstellen Sie eine Klasse `AlarmSystem`:**
   - Fügen Sie eine Methode `ActivateAlarm` hinzu, die die `TemperatureThresholdReached`-Event-Nachricht entgegennimmt und eine Warnung ausgibt.

4. **Verknüpfen Sie den `AlarmSystem` mit dem `TemperatureSensor`:**
   - Erzeugen Sie Instanzen von `TemperatureSensor` und `AlarmSystem`.
   - Abonnieren Sie das `TemperatureThresholdReached`-Event mit der Methode `ActivateAlarm`.

5. **Testen Sie das System:**
   - Simulieren Sie Temperaturmessungen und beobachten Sie die Ausführung des Events mit der übergebenen Temperatur.

## Lösungshinweise

1. **Delegat und Event:**
   - Definieren Sie einen Delegaten `TemperatureThresholdReachedHandler` mit einem `float`-Parameter.
   - Deklarieren Sie das Event `TemperatureThresholdReached` basierend auf diesem Delegaten.

2. **Datenverarbeitung:**
   - Verwenden Sie Zufallsgenerierung zur Simulation von Temperaturdaten in `ReadTemperature`.
   - Lösen Sie das Event aus, wenn der Temperaturwert den Schwellenwert überschreitet.

3. **Event auslösen:**
   - Nutzen Sie `?.Invoke(temperature)`, um das Event auszulösen, wenn es Abonnenten gibt.

4. **Abonnent:**
   - Implementieren Sie `ActivateAlarm` im `AlarmSystem`, um die Warnung auszugeben.

5. **Verbindung:**
   - Nutzen Sie `+=` im Hauptprogramm, um das Event mit der Abonnentenmethode zu verbinden.

## Hilfreiche MSDN-Ressourcen

- [Delegates](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/)
- [Events](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/events/)
- [How to: Subscribe to and Unsubscribe from Events](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events)
- [Random Class](https://docs.microsoft.com/en-us/dotnet/api/system.random)
- [Nullable Reference Types](https://docs.microsoft.com/en-us/dotnet/csharp/nullable-references)