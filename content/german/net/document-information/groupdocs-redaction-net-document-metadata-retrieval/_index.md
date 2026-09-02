---
date: '2026-06-06'
description: Erfahren Sie, wie Sie metadata abrufen und document metadata mit GroupDocs.Redaction
  .NET extrahieren, um ein robustes document management und compliance zu ermöglichen.
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: Wie man metadata mit GroupDocs.Redaction .NET API abruft
type: docs
url: /de/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# Wie man Metadaten mit GroupDocs.Redaction .NET abruft

Im digitalen Zeitalter ist **wie man Metadaten abruft** aus einer Datei ein grundlegender Schritt für jede dokumentzentrierte Anwendung. Egal, ob Sie Dateimetadaten für Compliance‑Audits lesen, Dokumenteneigenschaften für die Indizierung extrahieren oder einfach die Dokumentgröße in einer Benutzeroberfläche anzeigen müssen, GroupDocs.Redaction .NET bietet Ihnen eine kompakte API, mit der Sie dies in nur wenigen Zeilen C# erledigen können. Dieses Tutorial führt Sie durch den gesamten Prozess, von der Einrichtung der Umgebung bis zur Anzeige der abgerufenen Informationen, sodass Sie sofort mit dem Extrahieren von Dokumentmetadaten beginnen können.

## Schnelle Antworten
- **Was ist die primäre Methode, um Metadaten zu erhalten?** Rufen Sie `Redactor.GetDocumentInfo()` auf einer `Redactor`-Instanz auf.  
- **Welche Formate werden unterstützt?** Über 50 Eingabe‑ und Ausgabeformate, darunter PDF, DOCX, XLSX, PPTX und Bildformate.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Testlizenz funktioniert für Tests; für die Produktion ist eine Volllizenz erforderlich.  
- **Kann ich große Dateien verarbeiten?** Ja – GroupDocs.Redaction verarbeitet Dokumente mit mehreren hundert Seiten, ohne die gesamte Datei in den Speicher zu laden.  
- **Ist Async‑Unterstützung verfügbar?** Die API kann in Async‑Muster eingebettet werden, um UI‑Threads reaktionsfähig zu halten.

## Was ist das Abrufen von Metadaten in GroupDocs.Redaction?
Das Abrufen von Metadaten ist der Prozess, über die API der Bibliothek auf die eingebauten Eigenschaften eines Dokuments zuzugreifen – wie Dateityp, Seitenzahl und Größe. Durch das Extrahieren dieser Eigenschaften können Entwickler programmgesteuert Dokumentmerkmale bewerten, die Indizierung unterstützen, Compliance‑Regeln durchsetzen und fundierte Entscheidungen über weitere Verarbeitungsschritte treffen.

## Wie ruft man Dokumentmetadaten ab?
Die `Redactor`‑Klasse ist die primäre Schnittstelle zum Laden und Inspizieren von Dokumenten in GroupDocs.Redaction.  
`GetDocumentInfo()` ist eine Methode, die ein `DocumentInfo`‑Objekt zurückgibt, das die Metadaten des Dokuments enthält.

Laden Sie Ihre Datei mit `new Redactor("path/to/file")` und rufen Sie `GetDocumentInfo()` auf – der Aufruf liefert ein `DocumentInfo`‑Objekt, das Typ, Seitenzahl, Größe und weitere Eigenschaften enthält. Dieser Zwei‑Schritt‑Ansatz funktioniert für jedes unterstützte Format und erfordert keine zusätzliche Konfiguration. Sie können dann Felder wie `FileType`, `PageCount` und `FileSize` lesen, um die Informationen anzuzeigen oder zu protokollieren.

## Voraussetzungen

- **GroupDocs.Redaction .NET** Version 21.6 oder neuer.  
- .NET Framework 4.7.2 +, .NET Core 3.1 + oder .NET 5/6+.  
- Grundkenntnisse in C# und eine Entwicklungs‑IDE (Visual Studio, Rider usw.).

## Einrichtung von GroupDocs.Redaction für .NET

Der Einstieg in GroupDocs.Redaction ist unkompliziert. Installieren Sie das Paket mit einer der folgenden Methoden:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

Oder verwenden Sie die **NuGet Package Manager UI**: Suchen Sie einfach nach „GroupDocs.Redaction“ und klicken Sie auf **Install**.

### Lizenzbeschaffung

Um GroupDocs.Redaction auszuprobieren, können Sie eine kostenlose Testlizenz erhalten. Für fortlaufende Entwicklung oder den Produktionseinsatz erwerben Sie eine Volllizenz oder beantragen Sie eine temporäre Lizenz auf der offiziellen Website.

Nach der Installation initialisieren Sie die Bibliothek wie folgt:

```csharp
using GroupDocs.Redaction;
```

## Implementierungs‑Leitfaden

### Dokumentinformations‑Funktion

Diese Funktion konzentriert sich darauf, wichtige Metadaten aus Dokumenten mit GroupDocs.Redaction .NET zu extrahieren. Folgen Sie diesen Schritten:

#### Schritt 1: Dokumentpfad vorbereiten

Definieren Sie den absoluten oder relativen Pfad zur Zieldatei:

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

Ersetzen Sie `YOUR_DOCUMENT_DIRECTORY` durch den Ordner, der Ihr Dokument enthält.

#### Schritt 2: Redactor‑Instanz initialisieren

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### Schritt 3: Dokumentinformationen abrufen

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

Das zurückgegebene Objekt enthält Dateityp, Seitenzahl und Dateigröße.

#### Schritt 4: Dokumentdetails anzeigen

Geben Sie die Informationen in der Konsole oder UI aus. Der Beispielcode (auskommentiert für eigenständige Ausführungen) zeigt, wie jede Eigenschaft ausgegeben wird:

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### Warum GroupDocs.Redaction für die Metadatenextraktion verwenden?
GroupDocs.Redaction unterstützt **mehr als 50 Dateiformate** und kann Dokumente bis zu **2 GB** Größe verarbeiten, wobei der Speicherverbrauch bei typischen Workloads unter **100 MB** bleibt. Die Bibliothek extrahiert Metadaten, ohne das Dokument vollständig zu laden, und liefert schnelle Antworten – oft unter **200 ms** für ein 100‑seitiges PDF auf Standard‑Serverhardware.

### Häufige Probleme und Lösungen
- **Falscher Dateipfad** – Überprüfen Sie die Pfadangabe und stellen Sie sicher, dass die Datei für den laufenden Prozess zugänglich ist.  
- **Nicht unterstütztes Format** – Prüfen Sie die Formatliste; falls ein Format fehlt, sollten Sie es zuerst konvertieren.  
- **Leistungsengpässe** – Bei sehr großen Dateien aktivieren Sie Streaming‑Optionen oder verarbeiten Sie Seiten in Batches, um den Speicherverbrauch zu begrenzen.

## Praktische Anwendungen

Das Verständnis der Metadaten eines Dokuments ermöglicht mehrere praxisnahe Szenarien:

1. **Document Management Systems (DMS)** – Automatisieren Sie die Kategorisierung und Indizierung basierend auf Typ, Größe oder Seitenzahl.  
2. **Compliance Auditing** – Verifizieren Sie, dass vertrauliche Dateien vor der Archivierung die erforderlichen Metadaten enthalten.  
3. **Data Migration** – Gruppieren Sie Dateien nach Eigenschaften, um Bulk‑Migrationsaufgaben zu optimieren.

## Leistungsüberlegungen
- **Effiziente Ressourcennutzung** – Verwenden Sie die `Redactor`‑Instanz innerhalb eines `using`‑Blocks, um eine ordnungsgemäße Entsorgung sicherzustellen.  
- **Asynchrone Muster** – Verpacken Sie Metadatenaufrufe in `Task.Run` oder implementieren Sie Async‑Wrapper, um UI‑Threads in Desktop‑ oder Web‑Apps reaktionsfähig zu halten.

## Häufig gestellte Fragen

**F: Aus welchen Dokumentformaten kann ich Metadaten extrahieren?**  
A: GroupDocs.Redaction liest Metadaten aus mehr als 50 Formaten, darunter PDF, DOCX, XLSX, PPTX, HTML und gängige Bildformate.

**F: Wie gehe ich mit passwortgeschützten Dateien um?**  
A: Übergeben Sie das Passwort dem `Redactor`‑Konstruktor; die API entschlüsselt die Datei, bevor sie Metadaten extrahiert.

**F: Gibt es ein Limit für die Größe der Dateien, die ich verarbeiten kann?**  
A: Obwohl es kein festes Limit gibt, können Dateien größer als 2 GB zusätzliche Speicheroptimierung erfordern; die Leistung bleibt linear zur Dateigröße.

**F: Kann ich Metadaten in einer Batch‑Operation abrufen?**  
A: Ja – iterieren Sie über eine Sammlung von Dateipfaden und rufen Sie für jede `GetDocumentInfo()` auf; die Bibliothek ist thread‑sicher für parallele Ausführungen.

**F: Benötige ich eine Lizenz für Entwicklungs‑Builds?**  
A: Eine kostenlose Testlizenz reicht für Entwicklung und Tests aus; für Produktions‑Deployments ist eine kommerzielle Lizenz erforderlich.

## Ressourcen

- [Dokumentation](https://docs.groupdocs.com/redaction/net/)  
- [API‑Referenz](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Kostenloses Support‑Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Informationen zur temporären Lizenz](https://purchase.groupdocs.com/temporary-license/)

## Fazit

Sie haben nun eine vollständige Schritt‑für‑Schritt‑Anleitung, **wie man Metadaten abruft** mit GroupDocs.Redaction .NET. Durch die Nutzung der Methode `Redactor.GetDocumentInfo()` können Sie Dateimetadaten schnell auslesen, Compliance‑Workflows unterstützen und jede Dokumentverarbeitungspipeline verbessern. Erkunden Sie weitere Redaction‑Funktionen – wie Inhaltsredaktion, Wasserzeichen und Dokumentkonvertierung – um eine voll ausgestattete Dokumenten‑Management‑Lösung zu erstellen.

---

**Zuletzt aktualisiert:** 2026-06-06  
**Getestet mit:** GroupDocs.Redaction .NET 21.6 (latest at time of writing)  
**Autor:** GroupDocs  

## Verwandte Tutorials

- [Wie man Dokumentmetadaten aus Streams mit GroupDocs.Redaction .NET extrahiert](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [Wie man Dokumentmetadaten mit GroupDocs.Redaction für .NET redigiert – ein umfassender Leitfaden](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Tutorials zum Laden von Dokumenten mit GroupDocs.Redaction für .NET](/redaction/net/document-loading/)