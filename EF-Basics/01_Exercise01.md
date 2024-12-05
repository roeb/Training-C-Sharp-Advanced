# Übung 1: Modell- und Datenbankerstellung mit EF Core

## Anweisungen

1. **Erstellen Sie ein neues Console-Projekt:**
   - Erstellen Sie ein .NET Core Console-Projekt in Ihrer bevorzugten Entwicklungsumgebung.

2. **Installieren Sie Entity Framework Core:**
   - Nutzen Sie die NuGet Package Manager Console oder .NET CLI, um die Pakete `Microsoft.EntityFrameworkCore` und `Microsoft.EntityFrameworkCore.SqlServer` zu installieren.

3. **Definieren Sie ein einfaches Datenmodell:**
   - Erstellen Sie eine Klasse `Product` mit folgenden Eigenschaften:
     - `int Id`
     - `string Name`
     - `decimal Price`

4. **Erstellen Sie eine DbContext-Klasse:**
   - Erstellen Sie eine Klasse `AppDbContext`, die von `DbContext` erbt. Fügen Sie eine `DbSet<Product>` hinzu.

5. **Konfigurieren Sie die Verbindung zum SQL Server:**
   - Überschreiben Sie die Methode `OnConfiguring` in `AppDbContext`, um den SQL Server mit einer passenden Verbindungszeichenkette zu verbinden.

6. **Erstellen Sie Migrationen und aktualisieren Sie die Datenbank:**
   - Initialisieren Sie Migrationen und aktualisieren Sie die Datenbank, um das Modell abzubilden.

## Lösungshinweise

- Verwenden Sie die .NET CLI-Befehle `dotnet ef migrations add InitialCreate` und `dotnet ef database update`, um die Migrationen durchzuführen und die Datenbank zu aktualisieren.
- Stellen Sie sicher, dass Ihr SQL Server läuft und der Benutzer die erforderlichen Berechtigungen hat, um die Datenbank zu erstellen/bearbeiten.
- Überlegen Sie, eine Methode vermaschinen-spezifische Anpassungen in der Verbindungszeichenkette anzupassen.