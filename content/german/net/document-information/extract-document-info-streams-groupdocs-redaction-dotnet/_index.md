---
date: '2026-06-11'
description: Erfahren Sie, wie Sie Metadaten aus Dokumenten-Streams mit GroupDocs.Redaction
  für .NET extrahieren, einschließlich Einrichtung, Codebeispielen und praktischen
  Anwendungen.
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: Wie man Metadaten aus Dokumenten-Streams mit GroupDocs.Redaction .NET extrahiert
type: docs
url: /de/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# Wie man Metadaten aus Dokumenten-Streams mit GroupDocs.Redaction .NET extrahiert

Sind Sie es leid, Dokumentinformationen manuell zu extrahieren oder mit großen Dateien zu arbeiten, die Ihren Arbeitsablauf verlangsamen? **Metadaten extrahieren** schnell ist eine häufige Herausforderung, und die GroupDocs.Redaction-Bibliothek für .NET bietet eine schnelle, speichereffiziente Möglichkeit, Dokumentdetails direkt aus Streams abzurufen. In diesem Tutorial lernen Sie, wie Sie die Bibliothek einrichten, Dateityp, Seitenzahl und Größe aus einem Stream auslesen und einen Ausgabordner für die weitere Verarbeitung vorbereiten.

## Schnelle Antworten
- **Was bedeutet „extract metadata“?** Es bedeutet, Eigenschaften wie Dateityp, Seitenzahl und Größe zu lesen, ohne das gesamte Dokument im Speicher zu öffnen.  
- **Welche Bibliothek übernimmt das?** GroupDocs.Redaction für .NET bietet eine native API für stream‑basierte Metadatenextraktion.  
- **Brauche ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich PDFs größer als 1 GB verarbeiten?** Ja – Streams ermöglichen die Verarbeitung von Dateien bis zu 2 GB, ohne die gesamte Datei zu laden.  
- **Welche .NET-Versionen werden unterstützt?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ und .NET 6+.

## Was ist Metadatenextraktion aus Streams?
Metadatenextraktion aus Streams ist der Vorgang, Dokumenteigenschaften direkt aus einem `Stream`‑Objekt zu lesen, wodurch das vollständige Laden der Datei vermieden und Speicher‑ sowie CPU‑Zeit gespart werden. Diese Technik ist ideal für Batch‑Verarbeitung oder cloud‑basierte Dienste, bei denen Ressourcen begrenzt sind.

## Warum GroupDocs.Redaction für die Metadatenextraktion verwenden?
GroupDocs.Redaction unterstützt **30+ Dateiformate** (einschließlich PDF, DOCX, XLSX, PPTX und Bildtypen) und kann Dokumente bis zu **2 GB** verarbeiten, während der Speicherverbrauch unter **50 MB** bleibt. Die `Redactor`‑API bietet einen einzigen Aufruf, um alle wichtigen Dokumentinformationen abzurufen, und eliminiert damit die Notwendigkeit mehrerer Parser.

## Voraussetzungen

- **GroupDocs.Redaction for .NET** (neueste Version)  
- **.NET Framework** 4.5+ **oder** **.NET Core/5+/6+**  
- Grundkenntnisse in C# und Vertrautheit mit Datei‑I/O  
- Visual Studio 2019 oder neuer

## Wie richte ich GroupDocs.Redaction für .NET ein?
Um GroupDocs.Redaction zu verwenden, müssen Sie zunächst die Bibliothek zu Ihrem Projekt hinzufügen. Dies kann über die .NET‑CLI, den Visual‑Studio‑Package‑Manager oder die NuGet‑UI erfolgen. Wählen Sie den Ansatz, der zu Ihrem Workflow passt; die CLI ist ideal für skriptbare Builds, während die UI eine grafische Möglichkeit bietet, Versionen und Abhängigkeiten zu durchsuchen.

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**
- Öffnen Sie den NuGet Package Manager in Visual Studio.  
- Suchen Sie nach **"GroupDocs.Redaction"** und installieren Sie die neueste Version.

### Schritte zum Erwerb einer Lizenz
1. **Free Trial:** Laden Sie eine Testlizenz herunter, um alle Funktionen ohne Einschränkungen zu erkunden.  
2. **Temporary License:** Fordern Sie eine temporäre Lizenz von [GroupDocs](https://purchase.groupdocs.com/temporary-license/) für erweiterte Tests an.  
3. **Purchase:** Wenn Sie für die Produktion bereit sind, erwerben Sie eine kommerzielle Lizenz.  

Für weitere Informationen besuchen Sie die [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).

### Grundlegende Initialisierung und Einrichtung
Die `Redactor`‑Klasse ist der Einstiegspunkt für alle Vorgänge, einschließlich Metadatenextraktion.

`Redactor` ist die Kernklasse, die eine Dokumentinstanz repräsentiert und Methoden für Redaktion, Informationsabfrage und Dateimanipulation bereitstellt. Nach der Installation können Sie ein `Redactor`‑Objekt wie unten gezeigt erstellen:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

Jetzt, da die Bibliothek bereit ist, tauchen wir in die Implementierungsdetails ein.

## Wie extrahiere ich Metadaten aus einem Dokumenten-Stream?
Laden Sie das Dokument als **read‑only stream**, initialisieren Sie den `Redactor` und rufen Sie `GetDocumentInfo()` auf, um die Metadaten in einem einzigen Schritt abzurufen. Dieser Ansatz vermeidet das Laden der gesamten Datei in den Speicher, was bei großen PDFs oder mehrseitigen Office‑Dokumenten entscheidend ist.

**Direkte Antwort:** Öffnen Sie die Datei mit `File.OpenRead()`, übergeben Sie den Stream an `new Redactor(stream)` und rufen Sie anschließend `redactor.GetDocumentInfo()` auf – die Methode gibt ein Objekt zurück, das Dateityp, Seitenzahl und Größe in nur drei Code‑Zeilen enthält.

### Schritt 1: Quelldateipfad vorbereiten
Stellen Sie zunächst sicher, dass die Quelldatei existiert und der Ausgabordner bereit ist. Die Hilfsmethode unten prüft das Ausgabeverzeichnis und erstellt es bei Bedarf.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*Warum?* Dies garantiert einen gültigen Pfad für nachfolgende Dateioperationen und verhindert `DirectoryNotFoundException`.

### Schritt 2: Dokumenten-Stream öffnen
Mit `File.OpenRead()` wird die Datei als **read‑only stream** geöffnet, was den Speicherverbrauch selbst bei Gigabyte‑großen Dateien gering hält.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*Warum?* Streams ermöglichen die Verarbeitung „on‑the‑fly“, sodass Sie mit Teilen der Datei arbeiten können, anstatt das gesamte Dokument zu laden.

### Schritt 3: Redactor mit dem Dokumenten-Stream initialisieren
`Redactor` ist das primäre API‑Objekt, das Ihnen Zugriff auf dokumentenbezogene Vorgänge gibt, einschließlich Metadatenextraktion.

`Redactor` stellt ein einzelnes Dokument dar, das aus einem Stream geladen wurde, und stellt Methoden wie `GetDocumentInfo()` für die schnelle Eigenschaftsabfrage bereit.  

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*Warum?* Durch die Instanziierung von `Redactor` mit einem Stream wird das Objekt an die zugrunde liegende Datei gebunden, ohne sie vollständig zu laden.

### Schritt 4: Dokumenten-Metadaten abrufen
Der Aufruf von `GetDocumentInfo()` liefert ein `DocumentInfo`‑Objekt, das Dateiformat, Seitenzahl und Dateigröße enthält.

`GetDocumentInfo()` extrahiert Kern‑Eigenschaften (Format, Seitenzahl, Größe) in einem einzigen Aufruf und eliminiert damit die Notwendigkeit separater Parser.  

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*Warum?* Dieser Schritt konsolidiert alle wesentlichen Metadaten, sodass Sie sie leicht protokollieren, filtern oder Dokumente basierend auf ihren Merkmalen weiterleiten können.

## Wie bereite ich ein Ausgabeverzeichnis für verarbeitete Dateien vor?
Bevor Sie verarbeitete Dateien schreiben, stellen Sie sicher, dass das Zielverzeichnis existiert und beschreibbar ist. Durch das programmatische Prüfen des Pfads und das Erstellen bei Bedarf vermeiden Sie gängige Laufzeit‑Ausnahmen wie `DirectoryNotFoundException` oder Berechtigungsfehler. Dieser einfache Schritt macht Ihren Code zudem portabel über verschiedene Umgebungen hinweg, egal ob lokal, auf einem Server oder innerhalb eines Containers.

**Direkte Antwort:** Verwenden Sie `Directory.Exists()`, um das Verzeichnis zu prüfen, und `Directory.CreateDirectory()`, um es zu erstellen, falls es nicht existiert – diese einzeilige Prüfung garantiert einen gültigen Pfad vor jeder Schreiboperation.

### Hilfsmethode implementieren
Die Methode unten fasst die Prüfen‑und‑Erstellen‑Logik zusammen und gibt den verifizierten Pfad für die spätere Verwendung zurück.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*Warum?* Die Zentralisierung dieser Logik reduziert Duplizierung und erleichtert die Wartung des Code‑Bestands.

## Häufige Probleme und Lösungen
- **Permission errors:** Stellen Sie sicher, dass die Anwendung unter einem Konto läuft, das Schreibzugriff auf das Zielverzeichnis hat.  
- **Invalid paths:** Überprüfen Sie Pfadtrenner (`\\` unter Windows, `/` unter Linux/macOS), um `DirectoryNotFoundException` zu vermeiden.  
- **Large file handling:** Schließen Sie Streams umgehend (`using`‑Anweisungen), um OS‑Handles freizugeben und Lecks zu verhindern.

## Praktische Anwendungen
1. **Automated Document Ingestion:** Metadaten beim Hochladen extrahieren und anschließend in einer Datenbank für schnelle Suche und Compliance‑Berichte speichern.  
2. **Legal & Compliance Audits:** Seitenzahlen und Dateitypen abrufen, um zu prüfen, ob Dokumente vor der Archivierung regulatorischen Standards entsprechen.  
3. **Enterprise Content Management:** Metadaten nutzen, um Dateien automatisch in Ordner zu kategorisieren, wodurch Organisation und Abrufgeschwindigkeit verbessert werden.

## Leistungsüberlegungen
- **Memory Management:** Umschließen Sie Streams stets mit `using`‑Blöcken, damit sie automatisch freigegeben werden.  
- **Batch Processing:** Verarbeiten Sie Dokumente in Gruppen von 10‑20, um Durchsatz und Speicherverbrauch, besonders auf ressourcenbeschränkten Servern, auszubalancieren.  
- **Parallelism:** Nutzen Sie `Parallel.ForEach` für unabhängige Dateien, überwachen Sie jedoch CPU und I/O, um Kontention zu vermeiden.

## Fazit
Sie haben nun einen vollständigen, produktionsreifen Leitfaden, wie Sie **Metadaten extrahieren** können aus Dokumenten‑Streams mit GroupDocs.Redaction für .NET. Durch Befolgen der obigen Schritte können Sie Dateityp, Seitenzahl und Größe effizient abrufen, den Speicherverbrauch gering halten und große Dateien problemlos verarbeiten.

**Nächste Schritte**
- Überprüfen Sie die vollständige API‑Referenz in der [documentation](https://docs.groupdocs.com/redaction/net/).  
- Vertiefen Sie sich in die [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/), um Redaktion, Wasserzeichen und OCR‑Funktionen zu erkunden.  
- Experimentieren Sie mit verschiedenen Dateiformaten (PDF, DOCX, XLSX), um zu sehen, wie sich Metadaten zwischen den Typen unterscheiden.  
- Integrieren Sie die extrahierten Metadaten in Ihre bestehende Dokumenten‑Management‑ oder Suchlösung.

## Häufig gestellte Fragen

**Q: Was ist der primäre Anwendungsfall für die Metadatenextraktion von GroupDocs.Redaction?**  
A: Sie ermöglicht eine schnelle, speichereffiziente Abfrage von Dokumenteigenschaften für Indexierung, Compliance‑Prüfungen und automatisches Routing, ohne die gesamte Datei zu öffnen.

**Q: Kann ich Metadaten aus passwortgeschützten Dateien extrahieren?**  
A: Ja, geben Sie das Passwort beim Erstellen des `Redactor`‑Objekts an; die API entschlüsselt den Stream intern.

**Q: Unterstützt die Bibliothek nicht‑PDF‑Formate wie DOCX oder XLSX?**  
A: Absolut – GroupDocs.Redaction verarbeitet über 30 Formate, darunter PDF, DOCX, XLSX, PPTX und gängige Bildtypen.

**Q: Wie groß darf ein Dokument sein, das ich mit Streams verarbeiten kann?**  
A: Streams erlauben die Verarbeitung von Dateien bis zu **2 GB**, während der Speicherverbrauch unter **50 MB** bleibt, dank on‑the‑fly‑Lesen.

**Q: Wo bekomme ich Hilfe, wenn ich auf Probleme stoße?**  
A: Besuchen Sie das [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) für Community‑Support oder konsultieren Sie die offizielle Dokumentation für Fehlersuch‑Tipps.

---

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs  

**Resources**  
- **Documentation:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API Reference:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Download:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## Verwandte Tutorials

- [Master Document Metadata Retrieval with GroupDocs.Redaction .NET API](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)
- [How to Redact Document Metadata Using GroupDocs.Redaction for .NET - A Comprehensive Guide](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Secure Document Redaction in .NET Using Streams: A Guide for GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)