# Übung 2: Einfaches CRUD mit EF Core

## Anweisungen

1. **Verwenden Sie das bestehende Projekt aus der vorherigen Übung:**
   - Nutzen Sie das vorhandene Console-Projekt mit `Product` und `AppDbContext`.

2. **Fügen Sie CRUD-Operationen hinzu:**
   - Implementieren Sie Methoden im `Program` zur Erstellung, Lesen, Aktualisierung und Löschung von Produkten.

3. **Erstellen einer Methode `AddProduct`:**
   - Fügt ein neues Produkt mit Name und Preis zu `Products` hinzu.

4. **Lesen von Produkten mit `GetAllProducts`:**
   - Gibt eine Liste aller Produkte aus der Datenbank in der Konsole aus.

5. **Aktualisieren des Produktpreises (`UpdateProductPrice`):**
   - Aktualisiert den Preis eines Produkts, das über die `Id` gesucht wird.

6. **Löschen eines Produkts (`DeleteProduct`):**
   - Entfernt ein Produkt mit einer bestimmten `Id`.

7. **Rufen Sie diese Methoden in `Main` auf und prüfen Sie die Funktionalität:**
   - Fügen Sie ein Produkt hinzu, lesen und zeigen Sie alle Produkte an, aktualisieren und löschen Sie ein Produkt, zeigen Sie die geänderte Tabelle nochmals an.

## Lösungshinweise

- Nutzen Sie `context.Products.Add()`, um ein Produkt hinzuzufügen und `context.SaveChanges()` zur Speicherung.
- Verwenden Sie `context.Products.Find(id)`, um ein Produkt zur Aktualisierung oder zum Löschen zu suchen.
- `context.Products.Remove()` sollte genutzt werden, um ein Produkt zu löschen.
- Vergessen Sie nicht, nach jeder Modifikation `context.SaveChanges()` aufzurufen.