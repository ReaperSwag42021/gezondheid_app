# 🩺 GezondheidApp

> A complete CRUD desktop application for tracking personal health data — built with C# WinForms, SQL Server, and a generous helping of charts.

![C#](https://img.shields.io/badge/C%23-239120?logo=c-sharp&logoColor=white)
![.NET 10](https://img.shields.io/badge/.NET-10-512BD4?logo=dotnet&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL_Server-CC2927?logo=microsoftsqlserver&logoColor=white)
![WinForms](https://img.shields.io/badge/WinForms-Desktop-blue)

A 5-week school portfolio project showcasing full-stack desktop development: data entry, persistence, visualization and document export — all in a single self-contained Windows Forms application.

---

## ✨ Features

### 📝 Invoer (Create)
Form for entering new health records with type-safe input validation:
- `NumericUpDown` controls prevent invalid numeric input
- `Naam` field validated to letters-only via the `KeyPress` event
- Centered layout that auto-resizes with the form

### 📋 Overzicht (Read / Update / Delete)
DataGridView with full CRUD operations:
- **Update** — double-click any cell to edit, then "Bijwerken"
- **Delete** — select a row and click "Verwijder rij"
- **Export to Excel** (.xlsx) — entire grid, via ClosedXML
- **Export to PDF** — A4 with header, striped table and summary stats, via iText7
- `Id` column is read-only to prevent breakage

### 📊 Grafieken (Charts)
Three auto-generated visualizations:
- 🥧 Pie chart — fruit consumption vs. recommended max
- 🥧 Pie chart — sport sessions vs. recommended max
- 📊 Stacked column chart — fruit + sport side-by-side
- Tab is disabled when the database is empty
- 🔄 Manual refresh button included

### 🎭 Custom Events
- **Afsluit** button — turns the form red, repositions the cursor over "Ja", confirms exit
- **Tab change** — auto-reloads data on Overzicht, auto-redraws on Grafieken
- **Form resize** — fullscreen scary overlay with system sound (resize is also blocked via disabled maximize/minimize buttons)

---

## 🛠️ Tech Stack

| Layer | Tech |
|---|---|
| Language | C# (.NET 10) |
| UI | Windows Forms |
| Database | SQL Server Express |
| Excel Export | ClosedXML 0.105.0 |
| PDF Export | iText7 9.5.0 + bouncy-castle-adapter |
| Charts | HIC.System.Windows.Forms.DataVisualization 1.0.1 |
| SQL Client | Microsoft.Data.SqlClient 6.1.4 |

---

## 🚀 Setup

### 1. Create the database
In SQL Server Express, create a database called `GezondheidDB` and run:

```sql
CREATE TABLE gezondheid (
    Id INT IDENTITY(1,1) PRIMARY KEY,
    Naam VARCHAR(50),
    Leeftijd INT,
    Gewicht FLOAT,
    Lengte FLOAT,
    aantal_fruit_per_dag INT NOT NULL DEFAULT 0,
    aantal_sport_per_week INT NOT NULL DEFAULT 0
);
```

If you already have the older `gezondheid` table, run `migrate_gezondheid.sql` instead to add the new columns.

### 2. Install NuGet packages
Via Package Manager Console:
```powershell
Install-Package ClosedXML
Install-Package HIC.System.Windows.Forms.DataVisualization
Install-Package itext7
Install-Package itext7.bouncy-castle-adapter
Install-Package Microsoft.Data.SqlClient
```

### 3. Connection string
The app uses:
```
Data Source=.\SQLEXPRESS;Initial Catalog=GezondheidDB;Trusted_Connection=True;TrustServerCertificate=True
```
Adjust this if your SQL Server instance lives elsewhere.

### 4. Run
Open the solution in Visual Studio 2022+, build, run. That's it.

---

## 📁 Project Structure

```
gezondheid_app/
├── Form1.cs                    # All event handlers and business logic
├── Form1.Designer.cs           # UI layout (fully code-based, no .resx)
├── WinFormsAppSchool.csproj    # Project file targeting net10.0-windows
├── migrate_gezondheid.sql      # Migration script for the older schema
└── README.md
```

### Architecture notes
- All SQL queries use **parameterized commands** — no SQL injection risk
- UI is laid out **entirely in code** (no Designer.resx files)
- Charts use the ported `HIC.System.Windows.Forms.DataVisualization` library, since the original isn't .NET 10 compatible

---

## 👤 Author

**Rik Postma** — Software Developer student at Firda Leeuwarden  
📧 rik8postma@gmail.com

---

⭐ Built as part of a 5-week school assignment.
