---
date: '2026-08-20'
description: Entdecken Sie, wie Sie Text mit regex in Java und GroupDocs.Redaction
  redigieren. Dieses Schritt‑für‑Schritt‑Tutorial zeigt Ihnen, wie Sie regex anwenden,
  save options konfigurieren und sensible Daten schützen.
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: Erfahren Sie, wie Sie Text in Java mit GroupDocs.Redaction redigieren.
  Dieser Leitfaden erklärt regex‑Redaktion, die Konfiguration von save options und
  performance tips zum Schutz sensibler Daten.
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: Wie man Text in Java mit GroupDocs.Redaction redigiert
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 'Wie man Text in Java mit GroupDocs.Redaction redigiert: Ein vollständiger
  Leitfaden'
type: docs
url: /de/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# Wie man Text in Java mit GroupDocs.Redaction redigiert: Ein vollständiger Leitfaden

In der heutigen schnelllebigen digitalen Welt ist **wie man Text redigiert** in Dokumenten eine Frage, der sich viele Entwickler stellen. Ob Sie persönliche Daten schützen, Vorschriften einhalten oder einfach Entwürfe bereinigen, dieser Leitfaden führt Sie durch die Verwendung von GroupDocs.Redaction für Java, um **regex‑basierte Redaktion schnell und sicher anzuwenden**. Sie erfahren, warum Redaktion wichtig ist, wie Sie die Bibliothek konfigurieren und erhalten Best‑Practice‑Tipps für eine Hochleistungs‑Verarbeitung.

## Schnelle Antworten
- **Was ist der Hauptzweck von GroupDocs.Redaction?** Sie bietet eine zuverlässige API, um sensible Texte in mehr als 50 Dokumentformaten zu finden und zu maskieren.  
- **Wie wende ich Regex für die Redaktion an?** Erstellen Sie ein `RegexRedaction`‑Objekt mit Ihrem Muster und übergeben Sie es an die Methode `Redactor.apply()`.  
- **Brauche ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; eine kostenpflichtige Lizenz schaltet alle Funktionen für die Produktion frei.  
- **Kann ich PDFs ebenso wie DOCX‑Dateien redigieren?** Ja – GroupDocs.Redaction unterstützt PDF, DOCX, PPTX und viele weitere Formate.  
- **Was ist der beste Weg, die Leistung zu verbessern?** Schließen Sie `Redactor`‑Instanzen umgehend, halten Sie Regex‑Muster einfach und verarbeiten Sie Dateien stapelweise.

## Was ist Textredaktion und warum ist sie wichtig?
Textredaktion entfernt oder verdeckt dauerhaft sensible Informationen aus einem Dokument und stellt sicher, dass vertrauliche Daten – wie Sozialversicherungsnummern, Kreditkartendetails oder medizinische Aufzeichnungen – nicht von unbefugten Personen wiederhergestellt oder eingesehen werden können. Sie funktioniert, indem die ursprünglichen Zeichen überschrieben oder durch eine Maske ersetzt werden, sodass der versteckte Inhalt nicht per Kopieren‑Einfügen oder OCR‑Tools extrahiert werden kann. Dies gewährleistet die Einhaltung von Datenschutzvorschriften und schützt Personen vor Identitätsdiebstahl oder Datenpannen.

## Warum Regex für Textredaktion verwenden?
Reguläre Ausdrücke ermöglichen es Ihnen, flexible Muster zu definieren, die eine Vielzahl von Datenformaten (z. B. Telefonnummern, Kreditkartennummern) abdecken. Die Verwendung von Regex mit GroupDocs.Redaction gibt Ihnen präzise Kontrolle darüber, was verborgen wird, und hält die Implementierung gleichzeitig kompakt und wartbar.

## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- **Java Development Kit (JDK)** installiert (Java 8 oder neuer).  
- Grundlegende Kenntnisse der Java‑Syntax und regulärer Ausdrücke.  
- Eine IDE wie **IntelliJ IDEA** oder **Eclipse**, um den Code auszuführen und zu debuggen.  

## Einrichtung von GroupDocs.Redaction für Java
Fügen Sie zunächst die Bibliothek zu Ihrem Projekt hinzu.

### Maven‑Einrichtung
Wenn Sie Maven verwenden, fügen Sie das Folgende in Ihre `pom.xml` ein:

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
Alternativ laden Sie das neueste JAR von [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) herunter.

### Grundlegende Initialisierung
`Redactor` ist die Kernklasse, die ein Dokument öffnet, Redaktionsregeln anwendet und die Ausgabe schreibt.

Sobald die Bibliothek verfügbar ist, können Sie mit der Redaktion von Dokumenten beginnen:

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## Wie man Text mit Regex in Java redigiert?
Der Vorgang umfasst das Laden der Quelldatei in eine `Redactor`‑Instanz, das Erstellen einer `RegexRedaction`‑Regel, die das zu matchende Muster definiert, das Anwenden der Regel mit `redactor.apply()` und schließlich das Speichern des modifizierten Dokuments mit `SaveOptions`. Wenn Sie diese Schritte befolgen, können Sie zuverlässig alle sensiblen Zeichenketten in den unterstützten Formaten finden und maskieren.

Die Klasse `Redactor` ist die Kernkomponente, die ein Dokument öffnet, Redaktionsregeln anwendet und die Ausgabedatei schreibt. Sie verwaltet Ressourcen intern, daher müssen Sie sie nach der Verarbeitung schließen, um Speicher freizugeben.

### Schritt 1: erforderliche Klassen importieren
Die folgenden Importe geben Ihnen Zugriff auf die Redaktions‑API:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### Schritt 2: Redactor initialisieren und Regex‑Muster anwenden
`RegexRedaction` stellt eine Redaktionsregel dar, die auf einem regulären Ausdrucksmuster basiert. Das von Ihnen bereitgestellte Muster bestimmt, welche Textfragmente ersetzt werden.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **Regex-Erklärung**: Das Muster `\b\d{3}-\d{2}-\d{4}\b` entspricht US‑Sozialversicherungsnummern (drei Ziffern, ein Bindestrich, zwei Ziffern, ein Bindestrich, vier Ziffern). `ReplacementOptions` ermöglicht die Auswahl einer durchgehenden schwarzen Überlagerung oder einer benutzerdefinierten Textmaske.

### Schritt 3: Speicheroptionen konfigurieren
`SaveOptions` steuert, wie die redigierte Datei geschrieben wird. Das Hinzufügen eines Suffixes macht deutlich, welche Dateien verarbeitet wurden, während das Beibehalten des Originalformats unerwünschte Konvertierungen vermeidet.

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **Speicheroptionen**: `setAddSuffix(true)` fügt dem Ausgabedateinamen automatisch “_redacted” hinzu und verhindert versehentliche Überschreibungen.

### Schritt 4: zusätzliche Speicher‑Einstellungen anpassen
Sie können die Ausgabe weiter anpassen – z. B. Metadaten beibehalten oder Anmerkungen flachlegen – indem Sie das `SaveOptions`‑Objekt anpassen.

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **Wichtige Konfiguration**: Das Setzen von `setPreserveMetadata(true)` bewahrt die ursprünglichen Dokumenteneigenschaften, was häufig für Compliance‑Audits erforderlich ist.

## Praktische Anwendungen
Praxisbeispiele, in denen **wie man Text redigiert** unverzichtbar ist:

1. **Rechtsdokumente** – Kundenkennungen verbergen, bevor Entwürfe mit externen Rechtsberatern geteilt werden.  
2. **Medizinische Aufzeichnungen** – Patientennamen, IDs oder Gesundheitsnummern maskieren, um HIPAA‑konform zu bleiben.  
3. **Finanzberichte** – Vertrauliche Kontonummern entfernen, wenn vierteljährliche Zusammenfassungen verteilt werden.  

## Leistungsüberlegungen
- **Speichermanagement**: Rufen Sie stets `redactor.close()` auf, um Dateihandles und native Ressourcen freizugeben.  
- **Effizientes Regex**: Einfachere Muster laufen schneller; vermeiden Sie übermäßiges Back‑Tracking, indem Sie nach Möglichkeit atomare Gruppen verwenden.  
- **Stapelverarbeitung**: Bei großen Dokumentensammlungen verarbeiten Sie Dateien in Stapeln von 20–50, um die Heap‑Nutzung vorhersehbar zu halten.

## Häufige Probleme und Lösungen
| Problem | Lösung |
|-------|----------|
| **Regex trifft zu viel** | Testen Sie Ihr Muster mit einem Online‑Regex‑Tester und verengen Sie die Zeichenklassen. |
| **Konflikt beim Ausgabedateinamen** | Verwenden Sie `setAddSuffix(true)` oder geben Sie einen benutzerdefinierten Ausgabepfad über `saveOptions.setOutputPath()` an. |
| **Speicherleck bei großen PDFs** | Verarbeiten Sie PDFs seitenweise oder erhöhen Sie die JVM‑Heap‑Größe (`-Xmx2g`). |

## Häufig gestellte Fragen

**Q: Was ist der Zweck von `setAddSuffix(true)` in SaveOptions?**  
A: Es fügt dem Ausgabedateinamen automatisch ein Suffix (z. B. `_redacted`) hinzu, sodass ersichtlich ist, welche Dateien verarbeitet wurden.

**Q: Kann ich Regex‑Muster außer Zahlen für die Textredaktion verwenden?**  
A: Absolut. Jeder gültige Java‑Reguläre‑Ausdruck kann an `RegexRedaction` übergeben werden, um E‑Mails, Telefonnummern, benutzerdefinierte IDs usw. zu adressieren.

**Q: Wie sollte ich Fehler während der Redaktion behandeln?**  
A: Umwickeln Sie die Redaktionslogik mit einem try‑catch‑Block, protokollieren Sie die Ausnahme und schließen Sie stets den `Redactor` in einem finally‑Block, um Ressourcen freizugeben.

**Q: Wird PDF‑Redaktion unterstützt?**  
A: Ja. GroupDocs.Redaction funktioniert mit PDF, DOCX, PPTX und vielen anderen Formaten.

**Q: Was sind bewährte Verfahren für groß angelegte Redaktionsprojekte?**  
A: Verwenden Sie Stapelverarbeitung, halten Sie Regex‑Muster einfach und überwachen Sie die Speichernutzung mit Profiling‑Tools.

## Zusätzliche Ressourcen
- **Dokumentation**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API‑Referenz**: [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**Zuletzt aktualisiert:** 2026-08-20  
**Getestet mit:** GroupDocs.Redaction 24.9 für Java  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Sensitive Data Java maskieren – GroupDocs.Redaction Leitfaden](/redaction/java/getting-started/)
- [Sensitive Data Java maskieren – Persönliche Infos mit GroupDocs.Redaction redigieren](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Wie man PDF mit Aspose OCR und Java redigiert – Regex‑Muster mit GroupDocs.Redaction implementieren](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)