# Übung 3: Beziehungen und Navigationseigenschaften

## Anweisungen

1. **Erweitern Sie das bestehende Projekt:**
   - Verwenden Sie das bestehende Console-Projekt mit dem `Product`-Modell.

2. **Erstellen Sie ein neues Modell `Category`:**
   - Eigenschaften: `int Id`, `string Name`
   - Definieren Sie eine Beziehung zwischen `Product` und `Category` (ein Produkt gehört zu einer Kategorie).

3. **Aktualisieren Sie das `Product`-Modell:**
   - Fügen Sie eine Navigationseigenschaft `Category` hinzu.
   - Fügen Sie eine Fremdschlüssel-Eigenschaft `CategoryId` hinzu.

4. **Ändern Sie `AppDbContext`:**
   - Fügen Sie `DbSet<Category>` hinzu, um sowohl Produkte als auch Kategorien zu verwalten.

5. **Fügen Sie Migrationen hinzu und aktualisieren Sie die Datenbank:**
   - Stellen Sie sicher, dass Ihre Änderungen den Tabellen in der Datenbank korrekt zugeordnet werden.

6. **Verwenden Sie Navigationseigenschaften in CRUD-Operationen:**
   - Implementieren Sie CRUD-Operationen, um Produkte einer Kategorie zuzuordnen und um Kategorien mit Produkten aufzulisten.

## Lösungshinweise

- Verwenden Sie das `DbContext`, um die `Include`-Methode zu nutzen und verwandte Daten über Navigationseigenschaften zu laden.
- Sicherstellen, dass die Migrationen aktualisiert werden, um die neuen Beziehungen in der Datenbank widerzuspiegeln.
- Beachten Sie, dass `Category`-Objekte beim Erstellen neuer Produkte in der Datenbank existieren sollten.