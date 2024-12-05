# Übung 3: LINQ-Abfragen auf Webservice-Daten

## Anweisungen

1. **Rufen Sie Nutzerdaten von einem Webservice ab:**
   - Verwenden Sie den Webservice "https://jsonplaceholder.typicode.com/users", um Nutzerdaten abzurufen.

2. **Definieren Sie eine `User`-Klasse:**
   - Enthalten Sie Eigenschaften wie `Id`, `Name`, `Username`, `Email`, `Address` und `Company`.

3. **Deserialisieren Sie die JSON-Daten:**
   - Verwenden Sie `System.Text.Json` oder `Newtonsoft.Json`, um die JSON-Daten in eine Liste von `User`-Objekten zu deserialisieren.

4. **Führen Sie komplexe LINQ-Abfragen durch:**

   - **Abfrage 1:** Filtern Sie Nutzer mit einem bestimmten Domainnamen in ihrer E-Mail-Adresse (z.B. alle Nutzer mit "@biz").
   - **Abfrage 2:** Gruppieren Sie Nutzer nach Stadt aus der Adresse.
   - **Abfrage 3:** Ermitteln Sie die häufigsten Namenpräfixe in den Unternehmen (bspw. "Group", "LLC").
   - **Abfrage 4:** Sortieren Sie Nutzer alphabetisch nach Name und dann Username.

5. **Geben Sie die Abfrageergebnisse in der Konsole aus:**
   - Präsentieren Sie die Ergebnisse strukturiert für jede Abfrage.

## Lösungshinweise

- Verwenden Sie `HttpClient` für die Webanfrage.
- Nutzen Sie LINQ-Methoden wie `Where`, `GroupBy`, `Select`, `OrderBy`, und `ThenBy` für Abfragen.
- Achten Sie darauf, JSON korrekt in das angegebene Modell zu deserialisieren.

## MSDN Links

### 1. HTTP-Anfragen mit HttpClient

- **HttpClient-Klasse**:
  - MSDN-Dokumentation: [HttpClient Class](https://learn.microsoft.com/dotnet/api/system.net.http.httpclient)
  - Einführung in die Verwendung von `HttpClient`, um HTTP-Anfragen zu senden und Antworten zu empfangen.

### 2. JSON-Daten Deserialisierung

- **System.Text.Json**:
  - MSDN-Dokumentation: [System.Text.Json Namespace](https://learn.microsoft.com/dotnet/api/system.text.json)
  - Tutorial zur JSON-Datenverarbeitung mit `System.Text.Json`: [How to serialize and deserialize JSON in .NET](https://learn.microsoft.com/dotnet/standard/serialization/system-text-json-how-to?pivots=dotnet-7-0)

- **Newtonsoft.Json (Json.NET)**:
  - Offizielle Dokumentation: [Json.NET Documentation](https://www.newtonsoft.com/json/help/html/Introduction.htm)
  - MSDN-Beispiel zur Verwendung von Json.NET: [Working with JSON in .NET (Newtonsoft.Json)](https://learn.microsoft.com/dotnet/standard/serialization/system-text-json-migrate-from-newtonsoft?pivots=dotnet-6-0)

### 3. LINQ-Abfragen

- **Grundlegende LINQ-Abfragen**:
  - MSDN-Dokumentation: [LINQ (Language-Integrated Query)](https://learn.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/)
  - Einführung in LINQ-Abfragen in C#: [Writing LINQ Queries in C#](https://learn.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/writing-linq-queries-csharp)

- **LINQ `Where`-Methode**:
  - MSDN-Dokumentation: [Enumerable.Where Method](https://learn.microsoft.com/dotnet/api/system.linq.enumerable.where)

- **LINQ `GroupBy`-Methode**:
  - MSDN-Dokumentation: [Enumerable.GroupBy Method](https://learn.microsoft.com/dotnet/api/system.linq.enumerable.groupby)

- **LINQ `OrderBy` und `ThenBy`-Methoden**:
  - MSDN-Dokumentation: 
    - [Enumerable.OrderBy Method](https://learn.microsoft.com/dotnet/api/system.linq.enumerable.orderby)
    - [Enumerable.ThenBy Method](https://learn.microsoft.com/dotnet/api/system.linq.enumerable.thenby)