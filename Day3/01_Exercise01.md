# Übung 1: Asynchrone Webservice-Anfrage mit `async` und `await`

## Anweisungen

1. **Erstellen Sie eine HTTP-GET-Anfrage an einen öffentlichen Webservice:**
   - Wählen Sie einen kostenlosen Webservice wie "https://jsonplaceholder.typicode.com/posts".
   - Verwenden Sie `HttpClient`, um eine GET-Anfrage asynchron zu senden.

2. **Verarbeiten Sie die HTTP-Antwort:**
   - Verarbeiten Sie die Antwort als JSON-String und parsen Sie die wichtigsten Informationen.
   - Verwenden Sie `System.Text.Json` oder `Newtonsoft.Json`, um das JSON zu parsen und die Daten als Liste von Objekten darzustellen.

3. **Erstellen Sie eine Methode `DisplayPostTitlesAsync`:**
   - Diese Methode soll die Titel der ersten fünf Beiträge aus der Antwort extrahieren und in der Konsole anzeigen.

4. **Führen Sie die Methoden in der `Main`-Methode aus:**
   - Rufen Sie `FetchDataAsync` auf und verwenden Sie die verarbeiteten Daten in `DisplayPostTitlesAsync`, um das Ergebnis anzuzeigen.

## Lösungshinweise

- Verwenden Sie `HttpClient` innerhalb einer `using`-Anweisung oder als Singleton, da es ressourcenintensiv ist.
- Der `await`-Operator sollte für die `GetStringAsync` Methode genutzt werden.
- Nutzen Sie `JsonSerializer` aus `System.Text.Json` oder `JsonConvert` aus `Newtonsoft.Json` für das JSON-Parsing.
- Achten Sie darauf, Exceptions, die während der Webanfrage auftreten könnten, korrekt zu behandeln.