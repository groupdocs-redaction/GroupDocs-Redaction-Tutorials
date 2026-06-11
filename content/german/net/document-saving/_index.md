---
date: 2026-06-11
description: Erfahren Sie, wie Sie redigierte Dateien exportieren, Ausgabeverzeichnisse
  konfigurieren, gerasterte PDFs erstellen und mit GroupDocs.Redaction für .NET in
  Streams speichern.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: Wie man redigierte Dokumente mit GroupDocs.Redaction .NET exportiert
type: docs
url: /de/net/document-saving/
weight: 3
---

# Wie man redigierte Dokumente mit GroupDocs.Redaction .NET exportiert

In diesem umfassenden Leitfaden entdecken Sie **wie man redigierte** Inhalte sicher und effizient mit GroupDocs.Redaction für .NET exportiert. Egal, ob Sie den ursprünglichen Dateityp beibehalten, das Dokument als rasterisiertes PDF sichern oder das Ergebnis direkt im Speicher streamen müssen, wir führen Sie durch jede Option mit klaren, leicht verständlichen Erklärungen und praxisnahen Tipps. Am Ende dieses Tutorials können Sie die richtige Exportstrategie für jedes compliance‑getriebene Szenario auswählen.

## Schnelle Antworten
- **Welche Formate kann ich exportieren?** Beliebige der 30+ nativen Formate, die von GroupDocs.Redaction unterstützt werden, plus rasterisiertes PDF für maximale Sicherheit.  
- **Benötige ich eine Lizenz für das Streaming?** Ja, eine gültige GroupDocs.Redaction‑Lizenz ist für das Streaming in der Produktion erforderlich.  
- **Kann ich einen benutzerdefinierten Ausgabepfad festlegen?** Absolut – verwenden Sie die `OutputPath`‑Eigenschaft oder `SaveOptions`, um ihn zu konfigurieren.  
- **Ist die Rasterisierung bei großen Dateien sicher?** Sie verarbeitet Dokumente bis zu 500 Seiten, ohne die gesamte Datei in den Speicher zu laden.  
- **Welche .NET‑Versionen werden unterstützt?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Was ist GroupDocs.Redaction?
GroupDocs.Redaction ist eine .NET‑Bibliothek, die programmgesteuert sensible Informationen aus PDFs, Word, Excel, PowerPoint, Bildern und vielen anderen Formaten entfernt oder maskiert. Sie bietet eine High‑Level‑API zum Definieren von Redaktionsbereichen, Anwenden von Richtlinien und schließlich zum Exportieren des bereinigten Dokuments. Das erleichtert die Integration von Redaktionsfunktionen in jede .NET‑Anwendung.

## Warum redigierte Dokumente als rasterisierte PDFs exportieren?
Rasterisierte PDFs wandeln jede Seite in ein flaches Bild um und entfernen versteckte Textebenen, die später extrahiert werden könnten. Dieses Format garantiert, dass redigierte Inhalte nicht wiederhergestellt werden können, und erfüllt strenge regulatorische Standards wie GDPR und HIPAA. GroupDocs.Redaction kann rasterisierte PDFs bis zu 300 dpi erzeugen, wobei die visuelle Treue erhalten bleibt und gleichzeitig Sicherheit gewährleistet wird.

## Wie exportiert man redigierte Dokumente?
Laden Sie die Quelldatei, wenden Sie Ihre Redaktionsregeln an und rufen Sie dann die passende Speichermethode auf – entweder `Save` für das Originalformat, `SaveAsRasterizedPdf` für PDF‑nur‑Bild oder `SaveToStream` für die Verarbeitung im Speicher. Nachfolgend finden Sie den schrittweisen Ablauf. Jede Methode stellt sicher, dass der redigierte Inhalt dauerhaft entfernt wird, während das gewünschte Ausgabeformat beibehalten wird.

### Schritt 1: NuGet‑Paket installieren
Fügen Sie das neueste GroupDocs.Redaction‑Paket zu Ihrem Projekt hinzu:

```bash
dotnet add package GroupDocs.Redaction
```

### Schritt 2: Dokument laden und Redaktionen definieren
Erstellen Sie eine `Redactor`‑Instanz, laden Sie die Datei und geben Sie die Bereiche an, die Sie ausblenden möchten. Die `Redactor`‑Klasse stellt die Kernfunktionalität zum Laden von Dokumenten und Anwenden von Redaktionsregeln bereit.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Schritt 3: Exportmethode auswählen
#### Export im Originalformat
```csharp
redactor.Save("RedactedReport.docx");
```

#### Export als rasterisiertes PDF
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Export in einen Memory‑Stream (ideal für Web‑APIs)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

Die `Save`‑Methode schreibt das redigierte Dokument in einer Datei im Originalformat. `SaveAsRasterizedPdf` erzeugt ein PDF, bei dem jede Seite als Bild gerendert wird, wodurch versteckter Text entfernt wird. `SaveToStream` gibt die redigierte Datei als Memory‑Stream zurück, was für Web‑Antworten geeignet ist.

## Wie konfiguriert man einen Ausgabepfad?
Setzen Sie die `OutputPath`‑Eigenschaft am `Redactor` oder übergeben Sie ein benutzerdefiniertes `SaveOptions`‑Objekt, das das gewünschte Verzeichnis enthält. `OutputPath` ist eine Eigenschaft des `Redactor`, die das Verzeichnis angibt, in das Ausgabedateien geschrieben werden. `SaveOptions` ermöglicht die Anpassung verschiedener Speicherparameter, einschließlich des Ausgabeverzeichnisses. Dadurch landen alle exportierten Dateien an einem vorhersehbaren Ort, was Batch‑Verarbeitungspipelines vereinfacht. Sie können zudem Unterordner pro Dokumenttyp angeben, um Ihren Arbeitsbereich organisiert zu halten.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Häufige Probleme und Lösungen
- **Redaktion nicht angewendet:** Stellen Sie sicher, dass das Suchmuster exakt mit dem Dokumenttext übereinstimmt; verwenden Sie bei Bedarf `RegexOptions.IgnoreCase`. `RegexOptions` ist eine Aufzählung, die das Verhalten von regulären Ausdrücken steuert, z. B. die Groß‑/Kleinschreibung.  
- **Große Dateien verursachen Speicherbelastung:** Aktivieren Sie den Streaming‑Modus, indem Sie `SaveToStream` verwenden und vermeiden Sie das Aufrufen von `Save` für das gesamte Dokument.  
- **Rasterisiertes PDF wirkt unscharf:** Erhöhen Sie die DPI in `RasterizationOptions` (z. B. 300–600), um die Bildqualität zu verbessern. `RasterizationOptions` ermöglicht das Festlegen von Parametern wie DPI und Bildformat für den rasterisierten PDF‑Export.

## Häufig gestellte Fragen

**Q: Kann ich in ein Format exportieren, das ursprünglich nicht unterstützt wurde?**  
A: Ja, GroupDocs.Redaction kann die meisten Eingabetypen in PDF, DOCX, XLSX, PPTX oder rasterisiertes PDF konvertieren und unterstützt über 30 Formate.

**Q: Wie schützt die Rasterisierung redigierte Daten?**  
A: Durch das Rendern jeder Seite als flaches Bild werden versteckte Textebenen entfernt, sodass es unmöglich ist, den ursprünglichen Inhalt zu extrahieren.

**Q: Ist es möglich, mehrere Redaktionsregeln zu verketten?**  
A: Absolut – Sie können `Apply` wiederholt aufrufen oder eine Sammlung von `RedactionOptions` übergeben, um viele Muster in einem Durchlauf zu verarbeiten. `RedactionOptions` definiert die Einstellungen für einen einzelnen Redaktionsvorgang, wie Region und Ersetzungstyp.

**Q: Muss ich das Redactor‑Objekt schließen?**  
A: Der `Redactor` implementiert `IDisposable`; wickeln Sie ihn in einen `using`‑Block ein oder rufen Sie `Dispose()` auf, um Dateihandles sofort freizugeben. `IDisposable` ist ein Interface, das einen Mechanismus zum Freigeben unmanaged Ressourcen bereitstellt.

**Q: Welche .NET‑Runtimes sind offiziell getestet?**  
A: GroupDocs.Redaction ist validiert für .NET Framework 4.6+, .NET Core 3.1+ und .NET 5/6/7.

## Zusätzliche Ressourcen

### Verfügbare Tutorials

- [Wie man Dokumente als rasterisierte PDFs mit GroupDocs.Redaction für .NET speichert: Ein vollständiger Leitfaden](./groupdocs-redaction-net-rasterized-pdfs/)
- [Implementierung des Ausgabeverzeichnisses in .NET mit GroupDocs.Redaction: Ein umfassender Leitfaden](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Redigieren und Speichern von Dokumenten mit GroupDocs.Redaction für .NET: Ein vollständiger Leitfaden](./redact-save-documents-groupdocs-redaction-net/)
- [Redigierte Dokumente im Originalformat speichern mit GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Sichere Dokumentenredaktion in .NET mit Streams: Ein Leitfaden für GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Nützliche Links

- [GroupDocs.Redaction für .NET Dokumentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction für .NET API‑Referenz](https://reference.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction für .NET herunterladen](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Kostenloser Support](https://forum.groupdocs.com/)
- [Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)

---

**Zuletzt aktualisiert:** 2026-06-11  
**Getestet mit:** GroupDocs.Redaction 23.11 für .NET  
**Autor:** GroupDocs  

---

## Verwandte Tutorials

- [Redigierte Dokumente im Originalformat speichern mit GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Wie man Dokumente als rasterisierte PDFs mit GroupDocs.Redaction für .NET speichert: Ein vollständiger Leitfaden](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Sichere Dokumentenredaktion in .NET mit Streams: Ein Leitfaden für GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)