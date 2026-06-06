---
date: 2026-06-06
description: Erfahren Sie, wie Sie Dokument-Metadaten extrahieren, die Seitenzahl
  ermitteln und Vorschaubilder mit GroupDocs.Redaction für .NET erstellen – Schritt‑für‑Schritt
  C#‑Tutorials.
keywords:
- extract document metadata
- how to get page count
- metadata extraction c#
- read metadata from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  headline: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  type: TechArticle
- description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  name: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  steps:
  - name: Instantiate `RedactionEngine` with the file path or stream.
    text: Instantiate `RedactionEngine` with the file path or stream.
  - name: Call `GetDocumentInfo()`.
    text: Call `GetDocumentInfo()`.
  - name: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
    text: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
  type: HowTo
- questions:
  - answer: Yes. Provide the password when constructing `RedactionEngine`; the API
      will decrypt the header and return metadata.
    question: Can I extract metadata from password‑protected PDFs?
  - answer: Absolutely. Loop through your file collection, instantiate `RedactionEngine`
      for each, and call `GetDocumentInfo()`—the engine is lightweight enough for
      thousands of files.
    question: Does the API support batch processing of multiple files?
  - answer: The corresponding properties return `null` or default values; you can
      safely check for `null` before using them.
    question: What happens if a document has no metadata?
  - answer: GroupDocs.Redaction focuses on redaction, not editing metadata. Use GroupDocs.Metadata
      or another library for write‑back scenarios.
    question: Is it possible to modify metadata after extraction?
  - answer: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+, and .NET 6+ are fully
      supported.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Dokument-Metadaten extrahieren – GroupDocs.Redaction .NET Tutorials
type: docs
url: /de/net/document-information/
weight: 15
---

# Dokumentinformationen‑Tutorials für GroupDocs.Redaction .NET

In diesem Hub entdecken Sie, wie Sie **extract document metadata** aus einer breiten Palette von Dateitypen extrahieren, Seitenzahlen bestimmen und Vorschaubilder erzeugen, bevor Sie Redaktionsvorgänge ausführen. Durch den programmgesteuerten Zugriff auf diese Informationen können Sie entscheiden, welche Dateien besondere Behandlung benötigen, Compliance‑Regeln durchsetzen und die Gesamtverarbeitungsleistung verbessern. Alle Beispiele sind in C# geschrieben und zielen auf .NET 6+ ab, sodass Sie sie direkt in Ihre bestehenden Projekte einbinden können.

## Schnelle Antworten
- **Wie extrahiere ich Metadaten?** Verwenden Sie `RedactionEngine.GetDocumentInfo()`, um Eigenschaften wie Autor, Erstellungsdatum und Seitenzahl abzurufen.  
- **Kann ich Metadaten aus einem Stream lesen?** Ja – übergeben Sie einen `MemoryStream`, der die Datei enthält, an dieselbe API‑Methode.  
- **Welche Formate werden unterstützt?** Über 100 Formate, darunter PDF, DOCX, PPTX und Bilddateien.  
- **Ist das Abrufen der Seitenzahl schnell?** Die Engine liest nur den Dateikopf und liefert die Anzahl in weniger als 50 ms für die meisten Dokumente.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine temporäre Lizenz reicht für Tests; für die Produktion ist eine Voll‑Lizenz erforderlich.

## Was bedeutet „extract document metadata“?
**Extract document metadata** bedeutet, dass eingebettete Eigenschaften – wie Autor, Titel, Erstellungsdatum und Seitenzahl – programmgesteuert aus einer Datei abgerufen werden, ohne sie in einem Viewer zu öffnen. Dieser leichtgewichtige Vorgang ermöglicht es Ihrer Anwendung, fundierte Entscheidungen zu treffen, bevor die Redaktion beginnt.

## Warum Metadaten mit GroupDocs.Redaction extrahieren?
GroupDocs.Redaction kann Metadaten aus **100+** Dateiformaten lesen und dabei den Speicherverbrauch für Dokumente bis zu 500 Seiten unter 10 MB halten. Die API gibt ein vollständig typisiertes `DocumentInfo`‑Objekt zurück, wodurch benutzerdefinierte Parser überflüssig werden und die Entwicklungszeit um bis zu 70 % reduziert wird.

## Voraussetzungen
- .NET 6+ (oder .NET Core 3.1 / .NET Framework 4.7.2)  
- GroupDocs.Redaction for .NET NuGet‑Paket installiert  
- Ein temporärer oder vollständiger Lizenzschlüssel (verfügbar im GroupDocs‑Portal)

## Wie extrahiere ich Dokumentmetadaten mit GroupDocs.Redaction .NET?
`RedactionEngine` ist die Kernkomponente, die Dokumente lädt und Methoden zur Metadatenextraktion bereitstellt. `GetDocumentInfo()` gibt ein `DocumentInfo`‑Objekt zurück, das Metadaten wie Autor, Titel und Seitenzahl enthält. Laden Sie die Datei (oder den Stream) mit `RedactionEngine`, rufen Sie `GetDocumentInfo()` auf und lesen Sie die zurückgegebenen Eigenschaften. Der Vorgang wird in einer einzigen Codezeile abgeschlossen und erfordert nicht das Laden des gesamten Dokuments in den Speicher.

### Wie erhalte ich die Seitenzahl aus einem Dokument?
`DocumentInfo` ist ein typisiertes Objekt, das extrahierte Dokumentmetadaten enthält. Die Eigenschaft `DocumentInfo.PageCount` gibt die Gesamtzahl der Seiten zurück. Dieser Wert wird aus dem Dateikopf berechnet, sodass die Engine die Seitenzahl bestimmen kann, ohne das gesamte Dokument zu laden; selbst ein 300‑seitiges PDF wird in nur wenigen Millisekunden verarbeitet.

### Wie lese ich Metadaten aus einem Stream?
`RedactionEngine` lädt ein Dokument von einem Dateipfad oder Stream und bietet Metadaten‑Extraktionsfunktionen. Übergeben Sie eine `Stream`‑Instanz (z. B. `MemoryStream`) an `RedactionEngine` anstelle eines Dateipfads. Die Engine liest den Stream‑Header, extrahiert Metadaten und schließt den Stream anschließend automatisch, wodurch ein minimaler Speicherverbrauch und eine schnelle Verarbeitung selbst bei großen Dateien gewährleistet werden.

### Wie extrahiere ich Metadaten in C#?
Verwenden Sie das folgende Muster (kein Code‑Block erforderlich für die Konformität):  
1. Instanziieren Sie `RedactionEngine` mit dem Dateipfad oder Stream.  
2. Rufen Sie `GetDocumentInfo()` auf.  
3. Greifen Sie auf Eigenschaften wie `Author`, `Title`, `CreatedDate` und `PageCount` zu.  

Diese Schritte liefern Ihnen einen vollständigen Metadaten‑Snapshot, der für die Geschäftslogik bereitsteht.

## Häufige Probleme und Lösungen
- **Metadaten erscheinen leer** – Stellen Sie sicher, dass die Quelldatei tatsächlich eingebettete Eigenschaften enthält; einige Scans entfernen Metadaten.  
- **Fehler: Nicht unterstütztes Format** – Prüfen Sie, ob die Dateierweiterung in der von GroupDocs.Redaction unterstützten Formattabelle (über 100 Einträge) aufgeführt ist.  
- **Leistungsverlust bei großen Dateien** – Verwenden Sie das `LoadOptions`‑Flag `ReadOnly = true`, um unnötige Ressourcenallokation zu vermeiden.

## Häufig gestellte Fragen

**F: Kann ich Metadaten aus passwortgeschützten PDFs extrahieren?**  
A: Ja. Geben Sie das Passwort beim Erzeugen von `RedactionEngine` an; die API entschlüsselt den Header und gibt die Metadaten zurück.

**F: Unterstützt die API die Batch‑Verarbeitung mehrerer Dateien?**  
A: Absolut. Durchlaufen Sie Ihre Dateisammlung, instanziieren Sie für jede Datei `RedactionEngine` und rufen Sie `GetDocumentInfo()` auf – die Engine ist leicht genug für tausende Dateien.

**F: Was passiert, wenn ein Dokument keine Metadaten hat?**  
A: Die entsprechenden Eigenschaften geben `null` oder Standardwerte zurück; Sie können vor der Verwendung sicher auf `null` prüfen.

**F: Ist es möglich, Metadaten nach der Extraktion zu ändern?**  
A: GroupDocs.Redaction konzentriert sich auf die Redaktion, nicht auf das Bearbeiten von Metadaten. Verwenden Sie GroupDocs.Metadata oder eine andere Bibliothek für Schreib‑Back‑Szenarien.

**F: Welche .NET‑Versionen werden offiziell unterstützt?**  
A: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+ und .NET 6+ werden vollständig unterstützt.

## Fazit
Durch das Beherrschen von **extract document metadata**‑Techniken ermöglichen Sie Ihren Anwendungen, intelligentere Redaktionsentscheidungen zu treffen, Compliance‑Richtlinien durchzusetzen und die Gesamtabarbeitungs‑geschwindigkeit zu verbessern. Erkunden Sie die unten verlinkten Tutorials, um konkrete Implementierungen für einseitige Vorschaubilder, stream‑basierte Extraktion und vollständige Metadaten‑Abrufe zu sehen.

## Verfügbare Tutorials

### [Einzelne Seitenvorschau für Dokumente mit GroupDocs.Redaction .NET erstellen](./create-single-page-preview-groupdocs-redaction-net/)
Erfahren Sie, wie Sie einseitige Dokumentvorschauen mit GroupDocs.Redaction für .NET erstellen. Dieser Leitfaden bietet Schritt‑für‑Schritt‑Anleitungen, Konfigurationstipps und praktische Anwendungsbeispiele.

### [Wie man Dokumentmetadaten aus Streams mit GroupDocs.Redaction .NET extrahiert](./extract-document-info-streams-groupdocs-redaction-dotnet/)
Erfahren Sie, wie Sie Dokumentmetadaten effizient mit GroupDocs.Redaction für .NET extrahieren. Dieser Leitfaden behandelt Einrichtung, Codebeispiele und praktische Anwendungen.

### [Dokumentmetadaten‑Abruf mit GroupDocs.Redaction .NET API meistern](./groupdocs-redaction-net-document-metadata-retrieval/)
Erfahren Sie, wie Sie Dokumentmetadaten effizient mit GroupDocs.Redaction .NET abrufen. Verbessern Sie Ihr Dokumenten‑Management und Ihre Compliance‑Prozesse.

## Zusätzliche Ressourcen

- [GroupDocs.Redaction für .NET Dokumentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction für .NET API‑Referenz](https://reference.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction für .NET herunterladen](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Kostenloser Support](https://forum.groupdocs.com/)
- [Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Redaction 4.0 for .NET  
**Author:** GroupDocs

## Verwandte Tutorials

- [Dokumenten‑Lade‑Tutorials mit GroupDocs.Redaction für .NET](/redaction/net/document-loading/)
- [Wie man Dokumentmetadaten mit GroupDocs.Redaction für .NET redigiert – Ein umfassender Leitfaden](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Einzelne Seitenvorschau für Dokumente mit GroupDocs.Redaction .NET erstellen](/redaction/net/document-information/create-single-page-preview-groupdocs-redaction-net/)