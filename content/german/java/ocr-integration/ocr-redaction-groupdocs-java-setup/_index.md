---
date: '2026-06-26'
description: Erfahren Sie, wie Sie Text aus gescannten PDFs extrahieren und sensible
  Daten mit GroupDocs OCR Redaction und Azure OCR maskieren. Redact social security
  number und ersetzen Sie confidential info PDF effizient.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Text aus gescanntem PDF extrahieren – Daten maskieren mit GroupDocs OCR
type: docs
url: /de/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Text aus gescannten PDFs extrahieren – Daten mit GroupDocs OCR maskieren

## Schnelle Antworten
- **Was bedeutet „sensible Daten maskieren“?** Es ersetzt identifizierten vertraulichen Text durch einen Platzhalter (z. B. `[REDACTED]`).  
- **Welche Bibliothek übernimmt OCR?** Microsoft Azure OCR Connector, verwendet über GroupDocs Redaction.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Evaluierung; für den Produktionseinsatz ist eine permanente Lizenz erforderlich.  
- **Kann ich gescannte PDFs redigieren?** Ja—OCR extrahiert den versteckten Text, bevor reguläre Ausdrucks‑Redaktionen angewendet werden.  
- **Ist diese Lösung nur für Java?** Das Beispiel basiert auf Java, aber GroupDocs bietet ähnliche APIs für .NET und andere Plattformen.

## Was ist OCR‑basierte Redaktion?
OCR‑basierte Redaktion führt zunächst OCR auf jeder Seite aus, wandelt Bilder in durchsuchbaren Text um und wendet dann Regex‑Muster an, um Treffer durch eine Maske wie `[REDACTED]` zu ersetzen. Dieser zweistufige Prozess ermöglicht es Ihnen, persönliche Daten selbst in gescannten PDFs zuverlässig zu verbergen und stellt sicher, dass alle sensiblen Zeichenketten entfernt werden, bevor das Dokument geteilt oder archiviert wird.

## Warum GroupDocs Redaction mit Azure OCR verwenden?
Sie sollten GroupDocs Redaction mit Azure OCR verwenden, weil es **>98 % OCR‑Genauigkeit bei gedrucktem Text** liefert, **mehr als 50 Eingabe‑ und Ausgabeformate** unterstützt und **mehrseitige PDFs verarbeiten kann, ohne die gesamte Datei in den Speicher zu laden**, was eine schnelle, skalierbare Redaktion für Compliance gewährleistet. Die Lösung **skaliert zudem, um ein 1.000‑seitiges PDF in weniger als 2 Minuten auf einem 8‑Kern‑Server zu verarbeiten**, was Batch‑Jobs praktisch macht.

## Voraussetzungen
- **Java Development Kit (JDK) 8+** installiert.  
- **Maven** (wenn Sie die Abhängigkeitsverwaltung bevorzugen) oder die Möglichkeit, JARs manuell herunterzuladen.  
- **Microsoft Azure OCR credentials** (Endpoint und Subscription‑Key).  
- Grundlegende Java‑Kenntnisse und Vertrautheit mit regulären Ausdrücken.

## Einrichtung von GroupDocs Redaction für Java

### Maven-Konfiguration
Fügen Sie das GroupDocs-Repository und die Abhängigkeit zu Ihrer `pom.xml` hinzu:

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
Wenn Sie die manuelle JAR‑Verwaltung bevorzugen, holen Sie sich das neueste Release von [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Lizenzbeschaffung
- **Free Trial** – alle Funktionen kostenlos testen.  
- **Temporary License** – Evaluationszeit verlängern.  
- **Full License** – Produktionsbereite Funktionen freischalten.

### Grundlegende Initialisierung und Einrichtung
Die Klasse `Redactor` ist die Kern-Engine, die OCR‑Extraktion durchführt und Redaktionsregeln auf PDF‑Dokumente anwendet.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Wie man sensible Daten mit OCR‑Redaktion maskiert
Das Maskieren sensibler Daten mit OCR‑Redaktion beinhaltet das Laden des PDFs mit Azure‑OCR‑Einstellungen, das Definieren von Regex‑Mustern für die zu verbergenden Daten und das Aufrufen des Redactors, um jeden Treffer durch einen Platzhalter wie `[REDACTED]` zu ersetzen. Die Bibliothek übernimmt OCR, Mustererkennung und das Neuschreiben von PDFs in einem einzigen Workflow.

### Schritt 1: Dokument mit OCR‑Einstellungen laden
`LoadOptions` konfiguriert, wie GroupDocs eine Datei lädt, und ermöglicht das Übergeben von OCR‑Connectors wie Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – ersetzen Sie dies durch den Pfad zu Ihrem PDF.  
- **`settings`** – enthält den Azure‑OCR‑Connector, den Sie zuvor erstellt haben.

### Schritt 2: Regex‑Redaktionen definieren und anwenden
`ReplacementOptions` gibt den Ersatztext an, der jedes Regex‑Match während der Redaktion ersetzt.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- Das Muster `\b\d{3}-\d{2}-\d{4}\b` entspricht US‑Social‑Security‑Nummern.  
- `ReplacementOptions("[REDACTED]")` ersetzt jeden Treffer durch die Maske und **maskiert damit sensible Daten**.

## Häufige Anwendungsfälle für das Maskieren sensibler Daten
1. **Rechtsdokumenten‑Management** – verstecken Sie Kundenkennungen, bevor Entwürfe geteilt werden.  
2. **Finanzberichterstattung** – schützen Sie Kontonummern und Transaktions‑IDs.  
3. **Gesundheitsakten** – erfüllen Sie HIPAA, indem Sie Patientenkennungen redigieren.  
4. **Regierungsveröffentlichungen** – entfernen Sie persönliche Daten aus öffentlichen Aufzeichnungen.  
5. **Unternehmensverträge** – verbergen Sie proprietäre Bedingungen während externer Prüfungen.

## Leistungstipps
- **Regex optimieren** – vermeiden Sie zu breit gefasste Muster, die die Verarbeitungszeit erhöhen; gut gestaltete Ausdrücke können die Laufzeit um bis zu 40 % reduzieren.  
- **Speichermanagement** – schließen Sie die `Redactor`‑Instanz umgehend (try‑with‑resources erledigt dies automatisch).  
- **Asynchrone Ausführung** – für die Massenverarbeitung führen Sie Redaktionsjobs in separaten Threads aus oder verwenden Sie eine Aufgabenwarteschlange, um die UI reaktionsfähig zu halten.

## Fehlerbehebung
- **Azure‑Anmeldeinformationen‑Fehler** – überprüfen Sie die Endpoint‑URL und den Subscription‑Key in `MicrosoftAzureOcrConnector` erneut.  
- **Dokument wird nicht geladen** – überprüfen Sie den Dateipfad und stellen Sie sicher, dass das PDF nicht passwortgeschützt ist (oder geben Sie das Passwort über `LoadOptions` an).  
- **Keine Redaktionen angewendet** – testen Sie Ihr Regex zunächst mit einem einfachen String; verwenden Sie `Pattern.compile` in einem Unit‑Test, um Treffer zu bestätigen.

## Häufig gestellte Fragen

**Q: Was ist OCR‑Redaktion?**  
A: OCR‑Redaktion verwendet Optical Character Recognition, um versteckten Text aus Bildern oder gescannten PDFs zu extrahieren, und wendet dann Redaktionsregeln an, um diesen Text zu maskieren.

**Q: Kann ich GroupDocs Redaction ohne Azure OCR verwenden?**  
A: Ja, aber OCR verbessert die Genauigkeit bei gescannten Dokumenten, bei denen die native Textextraktion fehlschlägt, erheblich.

**Q: Wie gehe ich mit komplexen Regex‑Mustern um?**  
A: Erstellen und testen Sie sie schrittweise, indem Sie Java’s `Pattern`‑Klasse in einer Sandbox verwenden, bevor Sie sie auf große Dokumente anwenden.

**Q: Was sind typische Leistungsengpässe?**  
A: Große PDFs, zu komplexe Regex‑Muster und synchrone OCR‑Aufrufe können die Verarbeitung verlangsamen; erwägen Sie Batch‑Verarbeitung und optimierte Muster.

**Q: Steht Support für Implementierungsprobleme zur Verfügung?**  
A: Auf jeden Fall—wenden Sie sich über das [GroupDocs‑Forum](https://forum.groupdocs.com/c/redaction/33) für Community‑Hilfe an uns oder kontaktieren Sie den GroupDocs‑Support.

## Zusätzliche Ressourcen
- **Dokumentation**: https://docs.groupdocs.com/redaction/java/  
- **API‑Referenz**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Kostenloser Support**: https://forum.groupdocs.com/c/redaction/33  
- **Temporäre Lizenz**: https://purchase.groupdocs.com/temporary-license/

---

**Zuletzt aktualisiert:** 2026-06-26  
**Getestet mit:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs  

## Verwandte Tutorials

- [Sichere PDF‑Redaktion mit OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Wie man Text mit GroupDocs.Redaction für Java redigiert](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Sensible Daten in Java maskieren – Persönliche Infos mit GroupDocs.Redaction redigieren](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)