---
date: '2026-07-20'
description: Erfahren Sie, wie Sie Formate mit GroupDocs.Redaction .NET auflisten,
  die Funktion in Ihren Dokumenten‑Workflow integrieren und die Leistung verbessern.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Entdecken Sie, wie Sie Formate mit GroupDocs.Redaction .NET auflisten,
  eine Schritt‑für‑Schritt‑Anleitung ansehen und Tipps für optimale Leistung in Ihren
  .NET‑Anwendungen erhalten.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Wie man Formate mit GroupDocs.Redaction .NET auflistet
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: Wie man Formate mit GroupDocs.Redaction .NET auflistet
type: docs
url: /de/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Wie man Formate mit GroupDocs.Redaction .NET auflistet

Die Verwaltung einer großen Vielfalt von Dokumenttypen ist für Entwickler, die dokumentzentrierte Anwendungen erstellen, eine tägliche Realität. In diesem Tutorial lernen Sie **wie man Formate auflistet**, die GroupDocs.Redaction .NET verarbeiten kann, sodass Sie Dateien vor der Verarbeitung validieren, Benutzern genaue Optionen präsentieren und Ihren Workflow effizient halten können.

## Einführung

Effizientes Dokumenten‑Handling beginnt damit, genau zu wissen, welche Dateitypen Ihre Bibliothek unterstützt. GroupDocs.Redaction stellt eine integrierte Methode bereit, um diese Informationen abzurufen, sodass Sie dynamische UI‑Elemente erstellen, Validierungsregeln durchsetzen und Laufzeitfehler vermeiden können. Im Folgenden finden Sie alles, was Sie benötigen, um loszulegen – von der Installation bis zu praktischen Code‑Snippets und Performance‑Tipps.

### Schnelle Antworten
- **Was bedeutet “how to list formats”?** Es bezieht sich auf das Abrufen der Sammlung von Dateierweiterungen, die GroupDocs.Redaction verarbeiten kann.  
- **Benötige ich eine Lizenz?** Ja, für den Produktionseinsatz ist eine gültige GroupDocs.Redaction‑Lizenz erforderlich.  
- **Welche .NET‑Versionen werden unterstützt?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Wie viele Formate stehen zur Verfügung?** Über 30 Eingabe‑ und Ausgabeformate werden out‑of‑the‑box unterstützt.  
- **Ist eine spezielle Konfiguration nötig?** Keine zusätzliche Konfiguration ist über die Standard‑Bibliotheksinitialisierung hinaus erforderlich.

## Was ist “how to list formats”?

Es beinhaltet das Aufrufen der FileType‑API der Bibliothek, um eine Sammlung zu erhalten, bei der jeder Eintrag die Dateierweiterung und einen menschenlesbaren Namen enthält. Entwickler können diese Sammlung dann iterieren, um Validierungsregeln zu erstellen, UI‑Dropdowns zu füllen oder unterstützte Typen zu protokollieren, sodass nur kompatible Dokumente verarbeitet werden.

## Warum Formate mit GroupDocs.Redaction auflisten?

GroupDocs.Redaction unterstützt **30+** unterschiedliche Dateitypen – darunter PDF, DOCX, PPTX und Bildformate – sodass Sie die meisten Unternehmensdokumente ohne Drittanbieter‑Konverter verarbeiten können. Durch das programmgesteuerte Auflisten dieser Formate eliminieren Sie Rätselraten, reduzieren Support‑Tickets und stellen sicher, dass nur kompatible Dateien in Ihre Verarbeitungspipeline gelangen.

## Voraussetzungen

- **GroupDocs.Redaction for .NET** – Laden Sie das neueste Paket von der offiziellen Website herunter.  
- **.NET Framework oder .NET Core** – kompatibel mit Ihrer Entwicklungsumgebung.  
- **Visual Studio** (oder jede C#‑kompatible IDE).  
- Grundlegende Vertrautheit mit C#‑Syntax.

## Einrichtung von GroupDocs.Redaction für .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Paket-Manager
`Install-Package GroupDocs.Redaction`

### NuGet Package Manager UI
- Suchen Sie nach **“GroupDocs.Redaction”** und installieren Sie die neueste Version.

### Lizenzbeschaffung
GroupDocs bietet eine kostenlose Testversion, eine temporäre Lizenz für Evaluierungszwecke oder Vollkauf‑Optionen an. Besuchen Sie die GroupDocs‑Website, um die passende Lizenzdatei zu erhalten.

### Grundlegende Initialisierung und Einrichtung
Nach dem Hinzufügen des Pakets referenzieren Sie den Namespace und erstellen eine `Redactor`‑Instanz:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Implementierungsleitfaden

### Wie liste ich Formate mit GroupDocs.Redaction .NET auf?
Laden Sie die Bibliothek, rufen Sie den statischen Helfer auf und sortieren Sie die Ergebnisse – das liefert Ihnen in nur zwei Code‑Zeilen eine gebrauchsfertige Sammlung. Verwenden Sie `FileType.GetSupportedFileFormats()`, um ein `IEnumerable<FileType>` zu erhalten, das jede Format‑Erweiterung und den Anzeigenamen enthält, und ordnen Sie nach Erweiterung für eine saubere UI‑Liste.

### Abrufen unterstützter Dateiformate

#### Übersicht
Ziel ist es, eine Liste von Dateitypen zu erhalten, die GroupDocs.Redaction verarbeiten kann, um sie in Validierungslogik, UI‑Dropdowns oder Protokollierungsmechanismen zu integrieren.

#### Schritt‑für‑Schritt‑Implementierung

**1. Retrieve Supported File Types**  
`FileType.GetSupportedFileFormats()` gibt jedes Format zurück, das die Bibliothek erkennt. Die Methode ist Teil der Klasse `GroupDocs.Redaction.FileType`, die Metadaten wie Dateierweiterung und freundlichen Namen kapselt.

**2. Display Supported File Types**  
Iterieren Sie über die Sammlung und geben Sie jede Format‑Erweiterung sowie die Beschreibung aus. Inline‑Code‑Beispiel:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

Das Snippet gibt eine ordentlich sortierte Liste wie “.pdf – Portable Document Format” aus, was sich perfekt zum Befüllen von UI‑Elementen eignet.

### Tipps zur Fehlerbehebung
- **Missing Package** – Überprüfen Sie die NuGet‑Paketreferenz und stellen Sie sicher, dass Pakete wiederhergestellt wurden.  
- **Incorrect License Path** – Stellen Sie sicher, dass die Lizenzdatei in das Ausgabeverzeichnis kopiert wird oder geben Sie einen absoluten Pfad an.  
- **Unsupported Extension** – Wenn ein Format nicht aufgeführt ist, prüfen Sie, ob Sie die neueste Bibliotheksversion verwenden; neuere Releases fügen zusätzliche Formate hinzu.

## Praktische Anwendungen
Das Verständnis unterstützter Dateiformate eröffnet mehrere reale Szenarien:

1. **Document Management Systems** – Validieren Sie Uploads anhand der unterstützten Liste, um Verarbeitungsfehler zu verhindern.  
2. **Content Security** – Wenden Sie Redaktionsregeln nur auf Dateitypen an, die die Engine sicher bearbeiten kann.  
3. **Batch Processing Pipelines** – Filtern Sie große Dateibatches, bevor Sie die Redaktion aufrufen, und sparen Sie CPU‑ und Speicherressourcen.

## Leistungsüberlegungen
- **Memory Footprint** – Das Auflisten von Formaten ist ein leichtgewichtiges Vorgehen; es wird kein Dokument in den Speicher geladen.  
- **Batch Operations** – Bei der Verarbeitung von Hunderten von Dateien rufen Sie die Formatliste einmal ab und verwenden sie erneut, um redundante Aufrufe zu vermeiden.  
- **Thread Safety** – `FileType.GetSupportedFileFormats()` ist thread‑sicher und kann aus parallelen Tasks ohne Synchronisation aufgerufen werden.

## Fazit
Sie haben nun einen vollständigen, produktionsreifen Ansatz, **wie man Formate** mit GroupDocs.Redaction .NET auflistet. Durch die Integration dieser Funktion können Sie die Validierung verbessern, die Benutzererfahrung steigern und Ihre Dokumenten‑Pipelines robust halten.

### Nächste Schritte
- Erkunden Sie die `Redactor`‑API, um Redaktionsregeln basierend auf dem Dateityp anzuwenden.  
- Kombinieren Sie die Formatliste mit einem Front‑End‑Dropdown für nahtlose Dateiauswahl.  
- Lesen Sie den Performance‑Leitfaden, um groß angelegte Batch‑Jobs zu optimieren.

## Häufig gestellte Fragen

**Q: Kann ich die Formatliste abrufen, ohne eine Redactor‑Instanz zu initialisieren?**  
A: Ja, `FileType.GetSupportedFileFormats()` ist statisch und erfordert kein `Redactor`‑Objekt.

**Q: Enthält die Liste sowohl Eingabe‑ als auch Ausgabeformate?**  
A: Die Methode gibt alle Formate zurück, die die Bibliothek sowohl lesen als auch schreiben kann; jedes `FileType` enthält ein `CanRead`‑ und ein `CanWrite`‑Flag.

**Q: Wie oft wird die unterstützte Formatliste aktualisiert?**  
A: GroupDocs veröffentlicht Format‑Updates mit jeder Bibliotheksversion; das Prüfen der Liste zur Laufzeit stellt sicher, dass Sie stets das neueste Set haben.

**Q: Gibt es eine Möglichkeit, nur PDF‑kompatible Formate zu filtern?**  
A: Ja, filtern Sie die Sammlung, wo `format.Extension == ".pdf"` oder wo `format.Name.Contains("PDF")`.

**Q: Funktioniert dieser Ansatz auf .NET Core 2.1?**  
A: Die Methode erfordert .NET Core 3.1 oder höher; frühere Laufzeiten werden nicht unterstützt.

## FAQ-Bereich
1. **Wie installiere ich GroupDocs.Redaction für .NET?**  
   Verwenden Sie den CLI‑Befehl `dotnet add package GroupDocs.Redaction` oder installieren Sie das Paket über die NuGet Package Manager UI.  
2. **Welche häufigen Probleme gibt es beim Abrufen unterstützter Formate?**  
   Stellen Sie sicher, dass alle Abhängigkeiten wiederhergestellt sind und dass Sie den korrekten Namespace (`GroupDocs.Redaction`) referenzieren.  
3. **Kann ich diese Funktion mit Nicht‑.NET‑Anwendungen nutzen?**  
   Dieses Tutorial konzentriert sich auf .NET, aber GroupDocs bietet ähnliche APIs für Java, Python und andere Plattformen.  
4. **Wie kann ich die Performance bei der Nutzung von GroupDocs.Redaction optimieren?**  
   Wiederverwenden Sie die Formatliste, vermeiden Sie das Laden vollständiger Dokumente, wenn nur die Kompatibilität geprüft wird, und überwachen Sie den Speicherverbrauch bei Batch‑Jobs.  
5. **Welche Dateitypen unterstützt GroupDocs.Redaction?**  
   Die Bibliothek unterstützt 30+ Formate, darunter PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG und viele weitere. Verwenden Sie `FileType.GetSupportedFileFormats()`, um die vollständige Liste anzuzeigen.

## Ressourcen
- [Dokumentation](https://docs.groupdocs.com/redaction/net/)
- [API‑Referenz](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction herunterladen](https://releases.groupdocs.com/redaction/net/)
- [Kostenloses Support‑Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-07-20  
**Tested With:** GroupDocs.Redaction 4.2.0 for .NET  
**Author:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## Verwandte Tutorials

- [Format‑Handling‑Tutorials für GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Dokumenten‑Lade‑Tutorials mit GroupDocs.Redaction für .NET](/redaction/net/document-loading/)
- [Dokumenten‑Speicher‑Tutorials für GroupDocs.Redaction .NET](/redaction/net/document-saving/)