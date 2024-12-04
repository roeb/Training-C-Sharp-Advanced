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