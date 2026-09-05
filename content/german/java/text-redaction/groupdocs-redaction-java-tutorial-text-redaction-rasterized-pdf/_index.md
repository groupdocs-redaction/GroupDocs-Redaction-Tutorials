---
date: '2026-08-20'
description: Erfahren Sie, wie Sie Text mit GroupDocs.Redaction Java redigieren, als
  gerastertes PDF speichern, genaue Phrasen ersetzen und benutzerdefinierte PDF-Einstellungen
  anwenden.
keywords:
- how to redact text
- save pdf as image
- convert pdf to image
lastmod: '2026-08-20'
og_description: Wie man Text mit GroupDocs.Redaction Java redigiert. Dieser Leitfaden
  zeigt Ihnen die Ersetzung genauer Phrasen, die Erstellung gerasterter PDFs und die
  PDF/A‑1a‑Konformität in wenigen Schritten.
og_image_alt: Guide showing GroupDocs.Redaction Java code to redact text and create
  rasterized PDF
og_title: Wie man Text mit der GroupDocs.Redaction Java-Bibliothek redigiert
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  headline: How to redact text with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  name: How to redact text with GroupDocs.Redaction Java
  steps:
  - name: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
    text: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
  - name: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
    text: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
  - name: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
    text: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
  type: HowTo
- questions:
  - answer: Add the GroupDocs repository and the `groupdocs-redaction` dependency
      to your `pom.xml` as shown in the Maven Setup section.
    question: How do I install GroupDocs.Redaction in a Maven project?
  - answer: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.
    question: Can I redact text from PDF files using this library?
  - answer: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s
      spelling and case sensitivity.
    question: What happens if the exact phrase isn’t found?
  - answer: Process them in smaller page ranges, enable rasterization only where needed,
      and always close the `Redactor` to free resources.
    question: How can I handle very large documents efficiently?
  - answer: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()`
      to target the exact pages you want to rasterize.
    question: Is it possible to save rasterized PDFs with specific page ranges?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java PDF processing
title: Wie man Text mit GroupDocs.Redaction Java redigiert
type: docs
url: /de/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# Wie man Text mit GroupDocs.Redaction Java redigiert

In modernen Anwendungen ist es eine häufige Herausforderung für Entwickler, Prüfer und Compliance‑Beauftragte, **wie man Text redigiert** in einem Dokument, während der Arbeitsablauf schnell und konform bleibt. Dieses Tutorial führt Sie durch die Verwendung von GroupDocs.Redaction für Java, um genaue Phrasen zu finden, sie durch sichere Overlays zu ersetzen und schließlich das Ergebnis als rasterisiertes PDF/A‑1a‑Dokument zu exportieren – ideal für Archivierung oder rechtliche Verteilung.

## Schnelle Antworten
- **Was ist die primäre Klasse für die Redaktion?** `Redactor`  
- **Kann ich eine Phrase durch ein farbiges Overlay ersetzen?** Ja, mit `ExactPhraseRedaction` und `ReplacementOptions`.  
- **Wie erstelle ich ein rasterisiertes PDF?** Aktivieren Sie die Rasterisierung über `SaveOptions.getRasterization().setEnabled(true)`.  
- **Welches PDF‑Konformitätsniveau wird im Beispiel verwendet?** `PdfComplianceLevel.PdfA1a`.  
- **Benötige ich eine Lizenz für den Produktionseinsatz?** Eine gültige GroupDocs.Redaction‑Lizenz ist für Produktionsbereitstellungen erforderlich.

## Was bedeutet „wie man Text redigiert“ in Java?
`Redaction` ist das permanente Entfernen oder Verbergen sensibler Inhalte aus einer Datei, sodass sie später nicht wiederhergestellt oder gelesen werden können. Mit GroupDocs.Redaction können Sie programmgesteuert nach einer genauen Phrase suchen – z. B. einer Sozialversicherungsnummer oder einem vertraulichen Projektcode – und sie durch ein rotes Overlay, ein schwarzes Kästchen oder ein beliebiges benutzerdefiniertes visuelles Element ersetzen, wodurch garantiert wird, dass die Originaldaten nicht wiederherstellbar sind.

## Warum GroupDocs.Redaction für Java verwenden?
GroupDocs.Redaction unterstützt **30+ Eingabe‑ und Ausgabeformate** (PDF, DOCX, PPTX, XLSX, HTML und Bildformate) und kann Dokumente mit mehreren hundert Seiten verarbeiten, ohne die gesamte Datei in den Speicher zu laden. Sein Algorithmus für die exakte Phrasenerkennung reduziert Fehlalarme um > 95 % im Vergleich zu generischen Schlüsselwortsuchen, und die integrierte Rasterisierungs‑Engine ermöglicht es Ihnen, PDF/A‑1a‑Dateien zu erzeugen, die vollständig bildbasiert für die Langzeitarchivierung sind.

## Voraussetzungen
Bevor Sie beginnen, stellen Sie sicher, dass Sie folgendes haben:

- **GroupDocs.Redaction für Java** (v24.9 oder neuer).  
- **Java Development Kit (JDK) 8+**.  
- Eine IDE wie IntelliJ IDEA, Eclipse oder NetBeans.  
- Maven für das Abhängigkeitsmanagement.  

### Erforderliche Bibliotheken und Abhängigkeiten
- GroupDocs.Redaction für Java – fügen Sie das Repository und die Abhängigkeit zu Ihrer `pom.xml` hinzu (siehe den Abschnitt Maven‑Setup).  
- Optional: jedes von Ihnen bevorzugte Logging‑Framework (SLF4J, Log4j usw.).

### Wissensvoraussetzungen
- Grundlegende Java‑Syntax und Datei‑I/O.  
- Vertrautheit mit der Struktur von Mavens `pom.xml`.

## Einrichtung von GroupDocs.Redaction für Java
### Maven‑Setup
Fügen Sie das GroupDocs‑Repository und die `groupdocs-redaction`‑Abhängigkeit zu Ihrer `pom.xml`‑Datei hinzu:

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
Alternativ können Sie die neueste Version direkt von [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) herunterladen.

### Lizenzbeschaffung
- **Kostenlose Testversion** – erkunden Sie die API ohne Lizenzschlüssel.  
- **Temporäre Lizenz** – für erweiterte Evaluierung verwenden.  
- **Vollständige Lizenz** – für Produktionsumgebungen erforderlich.

### Grundlegende Initialisierung und Einrichtung
Die Klasse `Redactor` ist der Einstiegspunkt für alle Redaktions‑Operationen. Sie lädt ein Dokument, wendet Redaktionsregeln an und speichert das Ergebnis.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## Wie man Text redigiert – Beispiel für exakte Phrase
Redactor ist die primäre Klasse, die ein Dokument lädt und Redaktionsregeln anwendet. ExactPhraseRedaction definiert eine Regel, die eine bestimmte Zeichenkette abgleicht. Dieses Beispiel zeigt das Laden einer Datei, das Erstellen einer ExactPhraseRedaction‑Regel und die Ausführung der Redaktion in einem einzigen Schritt, wodurch ein kompakter Arbeitsablauf für Entwickler bereitgestellt wird, während der Originalinhalt dauerhaft verborgen bleibt.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

## Wie man als rasterisiertes PDF speichert
SaveOptions ist das Konfigurationsobjekt, das steuert, wie ein Dokument gespeichert wird. Durch Aktivieren der Rasterisierungsfunktion und Auswahl der PDF/A‑1a‑Konformität können Sie ein ausschließlich bildbasiertes PDF erzeugen, bei dem jede Seite als Bitmap gerendert wird, wodurch Archivierungsstandards erfüllt und die Textextraktion verhindert wird.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

## Praktische Anwendungen
1. **Sensiblen Daten redigieren** – persönliche Kennungen automatisch verbergen, bevor Verträge geteilt werden.  
2. **Dokumentenarchivierung** – fertige Berichte in rasterisiertes PDF/A für langfristige Konformität konvertieren.  
3. **Massenhafte Inhaltsaktualisierung** – veraltete Terminologie in Hunderten von Dateien mit einem einzigen Skript ersetzen.

## Leistungsüberlegungen
- **Schließen Sie den `Redactor`** nach jeder Operation, um Dateihandles und Speicher freizugeben.  
- **Batch‑Verarbeitung** – laden Sie eine Dateiliste und iterieren Sie darüber, wobei Sie nach Möglichkeit eine einzelne `Redactor`‑Instanz wiederverwenden.  
- **Ressourcen überwachen** – verwenden Sie Java‑Profiling‑Tools, um CPU‑ und Heap‑Nutzung während groß angelegter Redaktionen zu beobachten.

## Häufig gestellte Fragen

**Q: Wie installiere ich GroupDocs.Redaction in einem Maven‑Projekt?**  
A: Fügen Sie das GroupDocs‑Repository und die `groupdocs-redaction`‑Abhängigkeit zu Ihrer `pom.xml` hinzu, wie im Abschnitt Maven‑Setup gezeigt.

**Q: Kann ich Text aus PDF‑Dateien mit dieser Bibliothek redigieren?**  
A: Ja, GroupDocs.Redaction unterstützt PDF, DOCX, PPTX und viele andere Formate.

**Q: Was passiert, wenn die exakte Phrase nicht gefunden wird?**  
A: Der `RedactorChangeLog` gibt einen Status von `Failed` zurück. Überprüfen Sie die Rechtschreibung und Groß‑/Kleinschreibung der Phrase.

**Q: Wie kann ich sehr große Dokumente effizient verarbeiten?**  
A: Verarbeiten Sie sie in kleineren Seitenbereichen, aktivieren Sie die Rasterisierung nur bei Bedarf und schließen Sie stets den `Redactor`, um Ressourcen freizugeben.

**Q: Ist es möglich, rasterisierte PDFs mit bestimmten Seitenbereichen zu speichern?**  
A: Absolut. Verwenden Sie `options.getRasterization().setPageIndex()` und `setPageCount()`, um die genauen Seiten, die Sie rasterisieren möchten, anzugeben.

## Fazit
Sie haben nun eine vollständige, durchgängige Anleitung, wie man Text mit GroupDocs.Redaction Java **redigiert** und **als rasterisiertes PDF speichert**. Durch das Befolgen dieser Schritte können Sie sensible Informationen schützen, strenge Compliance‑Standards einhalten und Ihre Java‑Dienste skalierbar performant halten.

**Nächste Schritte**  
- Tauchen Sie tiefer in die API ein, indem Sie die [offizielle Dokumentation](https://docs.groupdocs.com/redaction/java/) erkunden.  
- Experimentieren Sie mit anderen Redaktionstypen wie `RegexRedaction` und `ImageRedaction`.  
- Treten Sie der Community im [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) bei, um Tipps und bewährte Verfahren zu erhalten.

---

**Last Updated:** 2026-08-20  
**Tested With:** GroupDocs.Redaction Java 24.9  
**Author:** GroupDocs

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

## Verwandte Tutorials

- [Wie man Text mit GroupDocs.Redaction für Java redigiert](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Java Text Redaction Tutorial: Anleitung mit GroupDocs.Redaction](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)