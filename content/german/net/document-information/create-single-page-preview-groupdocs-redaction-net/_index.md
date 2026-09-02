---
date: '2026-06-06'
description: Erfahren Sie, wie Sie eine Seite in PNG konvertieren und PDF‑Seiten mit
  GroupDocs.Redaction für .NET in der Vorschau anzeigen. Schritt‑für‑Schritt‑Anleitung,
  Code‑Beispiele und praxisnahe Tipps.
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: Seite in PNG konvertieren mit GroupDocs.Redaction .NET
type: docs
url: /de/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# Seite in PNG konvertieren mit GroupDocs.Redaction .NET

Das Erstellen einer Vorschau einer einzelnen Seite aus einem großen Dokument ist ein häufiges Bedürfnis, wenn Sie nur den relevanten Ausschnitt von Informationen teilen möchten. In diesem Tutorial lernen Sie **wie man eine Seite in PNG konvertiert** mit GroupDocs.Redaction für .NET, konfigurieren die Vorschauausgabe und integrieren das Ergebnis in Ihre Anwendungen. Wir gehen die Voraussetzungen, Installation, Code‑Einrichtung und praktische Tipps durch, sodass Sie in wenigen Minuten einseitige PNG‑Vorschauen erzeugen können.

## Schnelle Antworten
- **Kann ich eine PNG‑Vorschau nur einer Seite erzeugen?** Ja, verwenden Sie `PreviewOptions`, um die Seitennummer und das Format anzugeben.  
- **Welches Format unterstützt GroupDocs.Redaction für Vorschauen?** PNG ist das Standardformat, aber JPEG und BMP sind ebenfalls verfügbar.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Testversion funktioniert zum Testen; für den kommerziellen Einsatz ist eine Produktionslizenz erforderlich.  
- **Funktioniert das auf .NET Core und .NET Framework?** Absolut – die Bibliothek zielt auf .NET Standard 2.0+ ab.  
- **Ist der Vorgang speichereffizient für große Dateien?** Ja, die API streamt Seiten und vermeidet das Laden des gesamten Dokuments.

## Was bedeutet Seite in PNG konvertieren?
**convert page to PNG** bezieht sich auf das Extrahieren einer einzelnen Seite aus einem unterstützten Dokument (PDF, DOCX, PPTX usw.) und das Rendern dieser Seite als Portable Network Graphics (PNG)‑Bild. Das resultierende Bild bewahrt das visuelle Layout, die Schriftarten und Grafiken der Originalseite und ermöglicht es, einen klaren Schnappschuss zu teilen, während der Rest des Dokuments verborgen bleibt.

## Warum eine einseitige Vorschau verwenden?
Das Erzeugen einer einseitigen PNG‑Vorschau reduziert die Bandbreite, beschleunigt die Ladezeiten und schützt sensible Inhalte, indem nur das Notwendige angezeigt wird. GroupDocs.Redaction kann ein 300‑seitiges PDF in weniger als 0,5 Sekunden auf typischer Serverhardware in ein 200 KB PNG rendern, was es ideal für Webportale und Reporting‑Tools macht.

## Voraussetzungen
- **GroupDocs.Redaction for .NET** – die Kernbibliothek, die Dokumenten‑Redaktion und Vorschauerstellung durchführt.  
- **System.IO** – Standard‑.NET‑Namespace für Dateiverarbeitung.  
- .NET Core 3.1+ oder .NET Framework 4.6.1+ (jede Plattform, die .NET Standard 2.0 unterstützt).  
- Grundkenntnisse in C# und Vertrautheit mit NuGet‑Paketverwaltung.

## Einrichtung von GroupDocs.Redaction für .NET

### Installationsinformationen

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Öffnen Sie Ihr Projekt in Visual Studio.  
- Wählen Sie **Manage NuGet Packages**.  
- Suchen Sie nach **GroupDocs.Redaction** und installieren Sie die neueste stabile Version.

### Schritte zum Erwerb einer Lizenz
Um die Bibliothek auszuführen, benötigen Sie eine gültige Lizenz. Sie können mit einer kostenlosen Testversion beginnen oder einen temporären Schlüssel anfordern:

1. Besuchen Sie die [GroupDocs-Website](https://purchase.groupdocs.com/temporary-license), um eine temporäre Lizenz anzufordern.  
2. Befolgen Sie die per E‑Mail erhaltenen Anweisungen, um die Lizenzdatei zu Ihrem Projekt hinzuzufügen.

### Grundlegende Initialisierung und Einrichtung
Die Klasse `RedactionEngine` ist der Einstiegspunkt für alle Vorgänge, einschließlich der Vorschauerstellung.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## Implementierungsanleitung

### Überblick
Dieser Abschnitt zeigt, wie man **convert page to PNG** durch Konfiguration von `PreviewOptions` und Aufruf der Vorschau‑API durchführt. Der Ansatz funktioniert für PDFs, DOCX, PPTX und viele andere von GroupDocs.Redaction unterstützte Formate.

### Schritt 1: Umgebung vorbereiten
Legen Sie den Pfad zur Quelldatei und den Ausgabepfad fest. Verwenden Sie `Path.Combine`, um plattformunabhängige Pfade zu erstellen.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### Schritt 2: Vorschauoptionen einrichten
`PreviewOptions` ermöglicht das Festlegen der Seitennummer, Bildgröße und des Ausgabeformats. Die Klasse ist das Konfigurationszentrum für die Vorschauerstellung.  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### Erklärung der wichtigsten Konfigurationen
- **Width & Height** – Passen Sie diese Werte an die Zielanzeigeresolution an.  
- **PageNumbers** – Geben Sie ein Array mit dem genauen Seitenindex an, den Sie rendern möchten (nullbasiert).  
- **PreviewFormat** – PNG ist das Standardformat; wechseln Sie zu `PreviewFormat.Jpeg` für kleinere Dateien.

### Tipps zur Fehlersuche
Wenn das PNG nicht erzeugt wird:
- Überprüfen Sie, ob der Pfad zur Quelldatei korrekt ist und die Datei zugänglich ist.  
- Stellen Sie sicher, dass die Lizenzdatei geladen ist, bevor Sie eine API‑Methode aufrufen.  
- Vergewissern Sie sich, dass `PreviewOptions.PageNumbers` einen gültigen Seitenindex enthält (z. B. `0` für die erste Seite).

## Praktische Anwendungsfälle
Das Erstellen einer einseitigen PNG‑Vorschau ist in vielen Szenarien nützlich:
1. **Client Presentations** – Zeigen Sie nur die relevante Folie oder Vertragsklausel.  
2. **Internal Reviews** – Ermöglichen Sie schnelle visuelle Prüfungen, ohne das gesamte Dokument zu öffnen.  
3. **Content Summaries** – Betten Sie Seiten‑Schnappschüsse in E‑Mails oder Dashboards ein, um sofortigen Kontext zu bieten.  

Die Integration dieser Funktion in ein CMS oder CRM kann die Thumbnail‑Erstellung für hochgeladene Dokumente automatisieren und die Benutzererfahrung verbessern.

## Leistungsüberlegungen
- **Memory Management** – Entsorgen Sie `RedactionEngine`‑Instanzen nach Gebrauch, um Ressourcen freizugeben.  
- **Asynchronous Execution** – Verwenden Sie `await engine.GeneratePreviewAsync(...)` in UI‑Anwendungen, um die Benutzeroberfläche reaktionsfähig zu halten.  
- **Library Updates** – GroupDocs.Redaction unterstützt **30+ Eingabe‑ und Ausgabeformate** und verarbeitet Dokumente bis zu 500 Seiten, ohne die gesamte Datei in den Speicher zu laden. Halten Sie das Paket aktuell, um von Leistungsverbesserungen zu profitieren.

## Fazit
Sie haben nun eine vollständige, produktionsreife Methode, um **convert page to PNG** durchzuführen und einseitige Vorschauen mit GroupDocs.Redaction für .NET zu erzeugen. Durch Befolgen der obigen Schritte können Sie hochwertige PNG‑Schnappschüsse in jede .NET‑Anwendung einbetten und das Dokumenten‑Sharing verbessern, während Sicherheit und Leistung erhalten bleiben.

## Häufig gestellte Fragen

**Q: Kann ich Vorschauen für passwortgeschützte PDFs erzeugen?**  
A: Ja, geben Sie das Passwort beim Initialisieren von `RedactionEngine` an und die Vorschau wird normal erstellt.

**Q: Wie ändere ich das Ausgabeformat von PNG zu JPEG?**  
A: Setzen Sie `options.PreviewFormat = PreviewFormat.Jpeg`, bevor Sie die Vorschaumethode aufrufen.

**Q: Ist es möglich, mehrere Seiten gleichzeitig vorzuschauen?**  
A: Absolut – weisen Sie `options.PageNumbers` ein Array von Seitennummern zu (z. B. `new[] {0, 2, 4}`).

**Q: Was soll ich tun, wenn das Vorschaubild unscharf ist?**  
A: Erhöhen Sie `options.Width` und `options.Height` auf eine höhere Auflösung; die Bibliothek skaliert das Bild entsprechend.

**Q: Funktioniert das in Linux‑Containern?**  
A: Ja, GroupDocs.Redaction .NET ist plattformübergreifend und läuft in Docker‑Containern, die .NET Core unterstützen.

## Ressourcen
- [Dokumentation](https://docs.groupdocs.com/redaction/net/)
- [API-Referenz](https://reference.groupdocs.com/redaction/net)
- [Neueste Version herunterladen](https://releases.groupdocs.com/redaction/net/)
- [Kostenloses Support-Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporäre Lizenz erwerben](https://purchase.groupdocs.com/temporary-license)

---

**Zuletzt aktualisiert:** 2026-06-06  
**Getestet mit:** GroupDocs.Redaction 5.6 for .NET  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Meisterung der Dokumentensicherheit: Word-Dokumente rasterisieren und redigieren mit GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)
- [Wie man Seiten aus PDFs mit GroupDocs.Redaction .NET löscht: Ein umfassender Leitfaden](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)
- [Implementierung der Dokumentenredaktion mit GroupDocs.Redaction .NET: Eine Schritt‑für‑Schritt‑Anleitung](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)