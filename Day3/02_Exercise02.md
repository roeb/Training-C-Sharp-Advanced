# Übung 2: Parallele Verarbeitung mit Parallel.ForEach

## Anweisungen

1. **Erstellen Sie eine Liste von Ganzzahlen:**
   - Erstellen Sie eine Liste mit mindestens 20 Ganzzahlen.

2. **Implementieren Sie parallele Verarbeitung mit `Parallel.ForEach`:**
   - Verwenden Sie `Parallel.ForEach`, um die Zahlen in der Liste zu verarbeiten.
   - Für jede Zahl multiplizieren Sie diese mit einem zufälligen Wert und speichern Sie das Ergebnis in einer synchronisierten Struktur.

3. **Verwenden Sie eine threadsichere Struktur für die Ergebnisse:**
   - Nutzen Sie `ConcurrentBag<int>` oder `BlockingCollection<int>`, um die Ergebnisse sicher zu speichern.

4. **Geben Sie die verarbeiteten Ergebnisse aus:**
   - Iterieren Sie über die threadsichere Struktur und geben Sie die verarbeiteten Werte in der Konsole aus.

## Lösungshinweise

- `Parallel.ForEach` führt Aktionen auf den Elementen der Sammlung parallel aus, erhöht jedoch den Bedarf an Synchronisation.
- `ConcurrentBag<>` ist eine threadsichere Sammlung, die schnellen Zugriff auf Elemente bietet.
- Zur Vermeidung von Nebenläufigkeitsproblemen sollten Veränderungen und Zugriffe auf gemeinsame Daten synchronisiert oder durch threadsichere Sammlungen abgewickelt werden.
