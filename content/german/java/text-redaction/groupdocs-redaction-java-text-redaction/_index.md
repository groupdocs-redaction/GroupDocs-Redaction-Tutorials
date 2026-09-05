---
date: '2026-08-14'
description: So redigieren Sie Text in Java-Dokumenten mit GroupDocs.Redaction – persönliche
  Informationen maskieren und sensible Texte effizient ersetzen.
keywords:
- how to redact text
- GroupDocs Redaction Java
- text redaction Java
- mask personal information
lastmod: '2026-08-14'
og_description: Mit GroupDocs.Redaction für Java können Sie persönliche Daten dauerhaft
  maskieren und sensible Zeichenketten in PDFs, DOCX und weiteren Formaten ersetzen,
  um die Einhaltung von GDPR und HIPAA sicherzustellen.
og_image_alt: 'Guide: redact text in Java using GroupDocs.Redaction library'
og_title: So redigieren Sie Text mit GroupDocs.Redaction für Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  headline: How to redact text with GroupDocs.Redaction for Java
  type: TechArticle
- description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  name: How to redact text with GroupDocs.Redaction for Java
  steps:
  - name: initialize the redactor
    text: '`Redactor` is the core class that loads a document, applies redaction rules,
      and writes the output.'
  - name: apply exact‑phrase redaction
    text: '`ExactPhraseRedaction` searches for an exact string match, while `ReplacementOptions`
      defines how the matched text should be replaced. - **Parameters:** - `"John
      Doe"` – the exact text to be redacted. - `ReplacementOptions("[personal]")`
      – the string that will replace the original content, effective'
  - name: save the redacted document
    text: '`Redactor.save` writes the modified document to a new file or overwrites
      the original, preserving the original format.'
  - name: clean up resources
    text: Always call `Redactor.close()` to release native resources and avoid memory
      leaks.
  type: HowTo
- questions:
  - answer: Yes, the library supports PDF, DOCX, XLSX, PPTX, and many other formats.
    question: Can I redact text from PDFs using GroupDocs.Redaction?
  - answer: No. Redactions permanently remove the original content, so keep a backup
      of the source file.
    question: Is a redaction reversible?
  - answer: Process them in chunks, use batch mode, and monitor memory usage with
      profiling tools.
    question: How do I handle very large documents efficiently?
  - answer: Besides DOCX and PDF, you can redact TXT, RTF, XLSX, PPTX, and more.
    question: What other text formats are supported?
  - answer: Absolutely. The API can be called from web services, background jobs,
      or CI/CD pipelines.
    question: Can I integrate GroupDocs.Redaction into existing workflows?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- privacy compliance
- redaction API
title: So redigieren Sie Text mit GroupDocs.Redaction für Java
type: docs
url: /de/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# Wie man Text mit GroupDocs.Redaction für Java redigiert

In diesem Tutorial lernen Sie **wie man Text** in Java‑basierten Dokumenten mit GroupDocs.Redaction redigiert. Sie sehen, wie persönliche Informationen maskiert, sensible Zeichenketten durch sichere Platzhalter ersetzt und mehrere Dateien batch‑freundlich verarbeitet werden können. Am Ende haben Sie eine produktionsbereite Lösung, die die Privatsphäre schützt, GDPR/HIPAA‑Anforderungen erfüllt und sich nahtlos in bestehende Java‑Anwendungen integriert.

## Schnelle Antworten
- **Welche Bibliothek wird verwendet?** GroupDocs.Redaction für Java.  
- **Kann ich persönliche Informationen maskieren?** Ja – verwenden Sie die exakte Phrase‑Redaktion mit Ersetzungsoptionen.  
- **Wird Batch‑Verarbeitung unterstützt?** Absolut, Sie können mehrere Dateien mit derselben Redactor‑Instanz durchlaufen.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion reicht für die Evaluierung; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Welche Java‑Version wird benötigt?** JDK 8 oder höher.

## Was bedeutet „Text redigieren“?

Redaktion entfernt oder verdeckt vertrauliche Daten dauerhaft aus einem Dokument. Mit GroupDocs.Redaction können Sie bestimmte Zeichenketten finden, sie durch sichere Platzhalter ersetzen und die bereinigte Datei speichern – alles ohne manuelle Bearbeitung.

## Warum GroupDocs.Redaction für Java verwenden?

GroupDocs.Redaction für Java unterstützt **mehr als 50 Eingabe‑ und Ausgabeformate** (einschließlich PDF, DOCX, XLSX, PPTX, TXT, RTF) und kann mehrhundertseitige Dateien verarbeiten, ohne das gesamte Dokument in den Speicher zu laden, und liefert hochdurchsatz‑Batch‑Operationen auf Standard‑Serverhardware.

## Voraussetzungen
- **Java Development Kit (JDK):** Version 8 oder neuer.  
- **IDE:** IntelliJ IDEA, Eclipse oder ein beliebiger Java‑kompatibler Editor.  
- **Maven:** Für das Abhängigkeitsmanagement.  
- **Grundlegende Java‑Kenntnisse:** Vertrautheit mit Klassen, Methoden und Ausnahmebehandlung.

## Einrichtung von GroupDocs.Redaction für Java
Um zu beginnen, fügen Sie die Bibliothek zu Ihrem Maven‑Projekt hinzu.

### Maven‑Einrichtung
Fügen Sie das Repository und die Abhängigkeit zu Ihrer `pom.xml`‑Datei hinzu:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### Direkter Download
Falls Sie es bevorzugen, holen Sie sich das neueste JAR von [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Lizenzbeschaffung
Sie können mit einer **Free Trial** beginnen, eine **Temporary License** für erweiterte Tests anfordern oder eine **Commercial License** für den Produktionseinsatz erwerben.

## Wie man Text in Dokumenten mit GroupDocs.Redaction redigiert

Die folgenden Abschnitte führen Sie durch die genauen Schritte, die nötig sind, um **persönliche Informationen zu maskieren** und **sensiblen Text zu ersetzen**.

### Schritt 1: Redactor initialisieren

`Redactor` ist die Kernklasse, die ein Dokument lädt, Redaktionsregeln anwendet und die Ausgabe schreibt.  

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### Schritt 2: Exakte-Phrase‑Redaktion anwenden

`ExactPhraseRedaction` sucht nach einer exakten Zeichenkettenübereinstimmung, während `ReplacementOptions` definiert, wie der gefundene Text ersetzt werden soll.  

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **Parameter:**  
  - `\"John Doe\"` – der genaue Text, der redigiert werden soll.  
  - `ReplacementOptions("[personal]")` – die Zeichenkette, die den Originalinhalt ersetzt und damit **persönliche Informationen maskiert**.

### Schritt 3: Redigiertes Dokument speichern

`Redactor.save` schreibt das modifizierte Dokument in eine neue Datei oder überschreibt die Originaldatei und bewahrt das ursprüngliche Format.  

```java
redactor.save();
```

### Schritt 4: Ressourcen bereinigen

Rufen Sie stets `Redactor.close()` auf, um native Ressourcen freizugeben und Speicherlecks zu vermeiden.  

```java
finally {
    redactor.close();
}
```

## Wie man persönliche Informationen mit einem benutzerdefinierten Callback maskiert

Ein benutzerdefinierter Callback ermöglicht es Ihnen, auf jedes Redaktionsereignis zu reagieren – nützlich für Protokollierung, bedingte Ersetzungen oder Prüfpfade.

### Callback‑Klasse erstellen

`IRedactionCallback` definiert Methoden, die vor und nach jeder Redaktionsoperation aufgerufen werden.  

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### Callback bei der Instanziierung von Redactor verwenden

Übergeben Sie Ihre Callback‑Implementierung über `RedactorSettings`, damit die Engine sie während der Verarbeitung aufruft.  

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## Praktische Anwendungen
- **Rechtsverträge:** Automatisch Kundennamen, SSNs oder vertrauliche Klauseln ausblenden, bevor Entwürfe geteilt werden.  
- **Medizinische Aufzeichnungen:** **Persönliche Informationen** wie Patientenkennungen maskieren, wenn Aufzeichnungen an Forschungspartner exportiert werden.  
- **Unternehmenskommunikation:** **Sensiblen Text** wie interne Projektcodes vor externer Verteilung ersetzen, um versehentliche Lecks zu verhindern.

## Leistungsüberlegungen
Beim Verarbeiten großer oder zahlreicher Dateien beachten Sie diese Tipps:

- **Batch‑Verarbeitung:** Durchlaufen Sie eine Sammlung von Dateien, um den Startaufwand zu reduzieren.  
- **Speicherverwaltung:** Geben Sie den `Redactor` nach jeder Datei frei; vermeiden Sie, viele Dokumente gleichzeitig im Speicher zu halten.  
- **Profiling:** Verwenden Sie Java‑Profiler (z. B. VisualVM), um Engpässe bei I/O oder Redaktionslogik zu erkennen.

## Häufig gestellte Fragen
**Q: Kann ich Text aus PDFs mit GroupDocs.Redaction redigieren?**  
A: Ja, die Bibliothek unterstützt PDF, DOCX, XLSX, PPTX und viele weitere Formate.

**Q: Ist eine Redaktion reversibel?**  
A: Nein. Redaktionen entfernen den Originalinhalt dauerhaft, daher sollten Sie ein Backup der Quelldatei behalten.

**Q: Wie gehe ich effizient mit sehr großen Dokumenten um?**  
A: Verarbeiten Sie sie in Abschnitten, nutzen Sie den Batch‑Modus und überwachen Sie die Speichernutzung mit Profiling‑Tools.

**Q: Welche anderen Textformate werden unterstützt?**  
A: Neben DOCX und PDF können Sie TXT, RTF, XLSX, PPTX und weitere Formate redigieren.

**Q: Kann ich GroupDocs.Redaction in bestehende Workflows integrieren?**  
A: Absolut. Die API kann aus Web‑Services, Hintergrundjobs oder CI/CD‑Pipelines aufgerufen werden.

## Ressourcen
- **Dokumentation:** [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API‑Referenz:** [GroupDocs API Reference for Java](https://reference.groupdocs.com/redaction/java)  
- **Download:** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub‑Repository:** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Kostenloses Support‑Forum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **Antrag für eine temporäre Lizenz:** [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Zuletzt aktualisiert:** 2026-08-14  
**Getestet mit:** GroupDocs.Redaction 24.9 für Java  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Sensiblen Daten in Java maskieren – GroupDocs.Redaction Leitfaden](/redaction/java/getting-started/)
- [Sensiblen Daten in Java maskieren – Persönliche Infos mit GroupDocs.Redaction redigieren](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Passwortgeschützte Docs in Java bearbeiten – Dokumente mit GroupDocs.Redaction redigieren](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)