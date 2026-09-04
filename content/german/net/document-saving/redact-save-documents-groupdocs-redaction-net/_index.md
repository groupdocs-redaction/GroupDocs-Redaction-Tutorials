---
date: '2026-07-20'
description: Erfahren Sie, wie Sie Dokumente redigieren, sensible Informationen verbergen
  und redigierte Dateien mithilfe von GroupDocs.Redaction für .NET in einen memory
  stream speichern.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: Wie man Dokumente mit GroupDocs.Redaction für .NET redigiert. Folgen
  Sie diesem step‑by‑step Leitfaden, um sensible Informationen zu verbergen und die
  redigierte Datei in einen memory stream zu speichern.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: Wie man Dokumente mit GroupDocs.Redaction für .NET redigiert
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: Wie man Dokumente mit GroupDocs.Redaction für .NET redigiert – ein vollständiger
  Leitfaden
type: docs
url: /de/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# Dokumente mit GroupDocs.Redaction für .NET redigieren

In modernen Unternehmensumgebungen ist **wie man Dokumente redigiert** eine entscheidende Fähigkeit zum Schutz personenbezogener Daten, Geschäftsgeheimnisse und compliance‑relevanter Informationen. Dieser Leitfaden führt Sie durch das Redigieren sensibler Informationen aus Word-, PDF- oder Bilddateien und das anschließende Speichern der redigierten Ausgabe direkt in einen MemoryStream – alles mit GroupDocs.Redaction für .NET.

## Schnelle Antworten
- **Was bewirkt die Redigierung?** Sie ersetzt ausgewählte Inhalte dauerhaft durch einen Platzhalter oder entfernt sie, sodass die Daten nie wiederhergestellt werden können.  
- **Welche Formate werden unterstützt?** Über 30 Dateitypen, darunter PDF, DOCX, PPTX und gängige Bildformate.  
- **Kann ich redigieren, ohne auf die Festplatte zu schreiben?** Ja – speichern Sie das Ergebnis in einem `MemoryStream` für die In‑Memory‑Verarbeitung.  
- **Benötige ich eine Lizenz für die Produktion?** Eine Voll‑Lizenz ist für den Produktionseinsatz erforderlich; ein kostenloser Testzeitraum steht zur Evaluierung zur Verfügung.  
- **Ist es mit .NET Core kompatibel?** Absolut – GroupDocs.Redaction funktioniert mit .NET Framework 4.6+, .NET Core 3.1+ und .NET 5/6/7.

## Was ist Dokumenten‑Redigierung?
Die Dokumenten‑Redigierung entfernt oder verdeckt vertraulichen Text, Bilder und Metadaten dauerhaft aus einer Datei, sodass der versteckte Inhalt nicht wiederhergestellt, angezeigt oder später extrahiert werden kann. Sie ersetzt die sensiblen Elemente durch einen Platzhalter wie ein schwarzes Rechteck oder benutzerdefinierten Text und aktualisiert die Dokumentstruktur, sodass die redigierten Daten nicht wiederherstellbar sind.

## Warum GroupDocs.Redaction zum Redigieren von Dokumenten verwenden?
GroupDocs.Redaction unterstützt **über 30 Dateiformate** und kann Dateien bis zu **2 GB** verarbeiten, ohne das gesamte Dokument in den Speicher zu laden, und liefert eine **30 % schnellere Verarbeitungszeit** im Vergleich zu vielen Wettbewerbern. Die API ermöglicht das Anwenden von exakten Phrasen‑, regulären Ausdrucks‑ oder bildbasierten Redigierungen mit einem einzigen Methodenaufruf, wodurch sie die effizienteste Wahl für .NET‑Entwickler ist.

## Voraussetzungen
- **GroupDocs.Redaction** NuGet‑Paket (neueste Version).  
- .NET Framework 4.6+ **oder** .NET Core 3.1+ installiert.  
- Eine C#‑kompatible IDE wie Visual Studio 2022.  
- Grundlegende C#‑Kenntnisse und Vertrautheit mit Datei‑I/O.

### Erforderliche Bibliotheken und Versionen
- **GroupDocs.Redaction** – Verwenden Sie stets die neueste Version, um Zugriff auf die neuesten Redigierungs‑Algorithmen und Sicherheitspatches zu erhalten.  
- **System.IO** – für die Stream‑Verarbeitung (integriert in .NET).

### Schritte zum Erwerb einer Lizenz
- **Free Trial:** Registrieren Sie sich auf der GroupDocs‑Website für eine 30‑tägige Testversion.  
- **Temporary License:** Fordern Sie einen temporären Schlüssel für Entwicklungstests an.  
- **Full License:** Kaufen Sie eine Produktionslizenz für uneingeschränkte Nutzung.

## Grundlegende Initialisierung und Einrichtung
Die Klasse `Redactor` ist der Einstiegspunkt für alle Redigierungs‑Operationen in GroupDocs.Redaction. Nachdem Sie das NuGet‑Paket installiert haben, instanziieren Sie `Redactor` mit dem Pfad zur Quelldatei.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## Wie man spezifischen Text in einem Dokument redigiert?
Um spezifischen Text zu redigieren, laden Sie die Quelldatei mit einer `Redactor`‑Instanz und wenden anschließend eine `ExactPhraseRedaction` an, die die exakte Zeichenkette, die Sie verbergen möchten, anvisiert. Die API durchsucht das Dokument, ersetzt jedes Vorkommen durch die gewählte Überlagerung und protokolliert die Änderungen in einem Änderungsprotokoll, sodass Sie die Redigierung vor dem Speichern überprüfen können.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

Die Klasse `ExactPhraseRedaction` ersetzt jedes Vorkommen der exakten Phrase durch ein schwarzes Rechteck (oder einen beliebigen benutzerdefinierten Platzhalter, den Sie konfigurieren).

**Schritt‑für‑Schritt:**
1. **Laden** – Erstellen Sie eine `Redactor`‑Instanz, die auf Ihre Datei verweist.  
2. **Anwenden** – Rufen Sie `Apply` mit einer `ExactPhraseRedaction` (oder einem anderen Redigierungstyp) auf.  
3. **Überprüfen** – Prüfen Sie `RedactorChangeLog`, um zu bestätigen, wie viele Treffer gefunden und ersetzt wurden.  

## Wie man ein redigiertes Dokument in einen MemoryStream speichert?
`MemoryStream` ist ein .NET‑Stream, der Daten im Speicher ablegt und schnelles Lesen/Schreiben ohne Festplatten‑I/O ermöglicht. Mit der `Save`‑Methode können Sie die redigierte Ausgabe in einen `MemoryStream` leiten, der dann über ein Netzwerk gesendet, in einer Datenbank gespeichert oder direkt von einem API‑Endpunkt zurückgegeben werden kann, ohne temporäre Dateien zu erzeugen.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**Wichtige Punkte:**
- Die `Save`‑Methode schreibt die redigierte Ausgabe in jede `Stream`‑Implementierung, einschließlich `MemoryStream`.  
- Es werden keine temporären Dateien erstellt, was Sicherheit und Leistung verbessert.  
- Sie können dies mit ASP.NET Core’s `FileStreamResult` kombinieren, um die Datei direkt an einen Browser zurückzugeben.

## Häufige Fallstricke und Lösungen
| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| **Redigierung nicht angewendet** | Die Groß‑/Kleinschreibung der Phrase unterscheidet sich von der Quelle. | Verwenden Sie `ExactPhraseRedaction("John Doe", caseSensitive: false)` oder eine reguläre Ausdrucks‑Redigierung für flexibles Matching. |
| **Große Dateien verursachen OutOfMemory** | Versuch, die gesamte Datei in den Speicher zu laden. | GroupDocs.Redaction streamt Daten intern; stellen Sie sicher, dass Sie die neueste Version verwenden, die Dateien in Teilen verarbeitet. |
| **Gespeicherte Datei ist beschädigt** | Stream wurde vor dem Senden nicht zurückgesetzt. | Nach `redactor.Save(stream)` setzen Sie `stream.Position = 0`, bevor Sie ihn lesen oder zurückgeben. |

## Häufig gestellte Fragen

**Q: Kann ich PDF‑Dateien mit derselben API redigieren?**  
A: Ja – GroupDocs.Redaction behandelt PDF, DOCX, PPTX und viele Bildformate einheitlich; zeigen Sie einfach `Redactor` auf eine PDF‑Datei.

**Q: Bleibt die Redigierung nach der Konvertierung des Dokuments in ein anderes Format erhalten?**  
A: Absolut – sobald redigiert, wird der Inhalt dauerhaft entfernt, unabhängig von späteren Konvertierungen.

**Q: Wie kann ich das Aussehen der Redigierung anpassen?**  
A: Verwenden Sie `RedactionOptions`, um die Überlagerungsfarbe, Transparenz festzulegen oder Text durch einen benutzerdefinierten String zu ersetzen.

**Q: Ist es möglich, mit regulären Ausdrücken zu redigieren?**  
A: Ja – `RegexRedaction` ermöglicht das Definieren von Mustern wie Kreditkartennummern oder E‑Mail‑Adressen.

**Q: Welche .NET‑Versionen werden offiziell unterstützt?**  
A: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6 und .NET 7.

---

**Zuletzt aktualisiert:** 2026-07-20  
**Getestet mit:** GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## Verwandte Tutorials

- [Wie man Dokumente lädt und redigiert mit GroupDocs.Redaction .NET&#58; Ein vollständiger Leitfaden](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Redigierte Dokumente im Originalformat speichern mit GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Sichere Dokumenten‑Redigierung in .NET mit Streams&#58; Ein Leitfaden für GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)