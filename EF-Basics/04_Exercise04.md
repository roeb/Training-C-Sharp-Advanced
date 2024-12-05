# Übung 4: LINQ-Abfragen mit EF Core

## Anweisungen

1. **Verwenden Sie das bestehende Projekt mit `Product` und `Category`:**
   - Verwenden Sie das bestehende Console-Projekt aus der vorherigen Übung.

2. **Erstellen Sie komplexe LINQ-Abfragen:**
   - Die Abfragen sollten Folgendes umfassen:
     - Produkte nach Preis sortieren.
     - Produkte filtern, die zu einer bestimmten Kategorie gehören.
     - Die Anzahl der Produkte pro Kategorie abrufen.

3. **Abfrage 1: Sortieren Sie Produkte nach Preis:**
   - Geben Sie eine Liste von Produkten aus, die nach Preis aufsteigend sortiert sind.

4. **Abfrage 2: Filtern Sie Produkte nach Kategorie:**
   - Implementieren Sie eine Methode, die Produkte einer bestimmten Kategorie abfragt und ausgibt.

5. **Abfrage 3: Zählen Sie die Anzahl der Produkte in jeder Kategorie:**
   - Nutzen Sie LINQ, um die Anzahl der Produkte in jeder Kategorie zu ermitteln und auszugeben.

6. **Führen Sie die Abfragen in der `Main`-Methode aus und zeigen Sie die Ergebnisse an:**
   - Rufen Sie jede Methode auf und geben Sie die Ergebnisse in der Konsole aus.

## Lösungshinweise

- Verwenden Sie Methoden wie `OrderBy`, `Where`, und `GroupBy`, um die gewünschten Abfragen zu erstellen.
- Nutzen Sie `Include`, um Navigationseigenschaften in Abfragen zu laden, wenn Sie mit den Beziehungen arbeiten.
- `ToList()` kann verwendet werden, um die Ergebnisse zu erhalten und durchzugehen.