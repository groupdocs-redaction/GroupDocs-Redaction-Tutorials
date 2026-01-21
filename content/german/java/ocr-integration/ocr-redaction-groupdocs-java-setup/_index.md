---
date: '2026-01-21'
description: Erfahren Sie, wie Sie PDFs mit OCR schwärzen und gescannte Dokumente
  mit GroupDocs.Redaction für Java und Azure-OCR-Integration schwärzen.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: PDF mit OCR redigieren mit GroupDocs & Azure OCR – Java‑Leitfaden
type: docs
url: /de/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

 erfahren Sie, wie Sie **PDF mit OCR redigieren** in Java, indem Sie GroupDocs.Redaction zusammen mit Microsoft Azure OCR nutzen. Egal, ob Sie native PDFs oder gescannte Bilder bearbeiten, zeigt Ihnen genau lokalisieren und maskieren, sodass Sie **gescannte Dokumente redigieren** können, um Datenschutzbestimmungen zu erfüllen.

## Schnelle Antworten
- **Was macht OCR-Redaktion?** Sie extrahiert Text aus Bildern/PDFs und wendet automatisch Redaktionsregeln an.  
- **Welche Bibliothek stellt die Redaktions-.  
- **Brauche ich eine Lizenz?** Eine kostenlose Testversionmuster, um diese Informationen zu verbergen, bevor die Datei geteilt oder gespeichert wird.

## Warum GroupDocs.Redaction mit Azure OCR verwenden?
- **Hohe Genauigkeit** auf gescannten Seiten dank der cloud‑basierten OCR‑Engine von Azure.  
- **Einfache Java‑API**, die sich direkt in Ihren bestehenden Workflow integriert.  
- **Flexible Redaktionsregeln** – Regex, Schlüsselwörter oder benutzerdefinierte Logik.  
- **Compliance‑fertige** Ausgabe, die sensible Daten dauerhaft entfernt.

## Voraussetzungen
- Java Development Kit (JDK) 8 oder neuer.  
- Maven (oder die Möglichkeit, das JAR manuell herunterzuladen).  
- Microsoft Azure‑Konto mit OCR‑Anmeldedaten.  
- Grundkenntnisse in Java und Vertrautheit mit regulären Ausdrücken.

## Einrichtung von GroupDocs.Redaction für Java

### Maven‑Einrichtung
Fügen Sie das GroupDocs‑Repository und die Abhängigkeit zu Ihrer `pom.xml` hinzu:

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
Wenn Sie Maven nicht verwenden möchten, laden Sie das neueste JAR von der offiziellen Release‑Seite herunter: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Lizenzbeschaffung
- **Kostenlose Testversion** – Kernfunktionen ohne Verpflichtung erkunden.  
- **Temporäre Lizenz** – Testzeitraum für größere Projekte verlängern.  
- **Vollständige Lizenz** – unbegrenzte Nutzung und Premium‑Support freischalten.

### Grundlegende Initialisierung und Einrichtung
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Wie man PDF mit OCR in Java redigiert

### Schritt 1: Dokument mit OCR‑Einstellungen laden
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Subsequent redaction steps will be placed here
}
```
- **Parameter**  
  - `"YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf"` – Pfad zur Ziel‑PDF.  
  - `new LoadOptions()` – Standard‑Ladekonfiguration.  
  - `settings` – enthält den Azure OCR‑Connector.

### Schritt 2: Regex‑Redaktionen anwenden (z. B. Sozialversicherungsnummern)
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
- **Regex‑Erklärung** – `\b\d{3}-\d{2}-\d{4}\b` entspricht Mustern wie `123-45-6789`.  
- **ReplacementOptions** – ersetztAzure‑Anmeldedaten für1. **Rechtsanwaltskanzleien** – Kundenkennungen verbergen, bevor Falldateien geteilt werden.  
2. **Finanzinstitute** – Kontonummern in gescannten Kontoauszügen maskieren.  
3. **Gesundheitsdienstleister** – Patientendaten (PHI) in gescannten medizinischen Unterlagen schützen.  
4. **Behörden** – persönliche Daten aus öffentlichen PDF‑Aufzeichnungen entfernen.  
5. **Unternehmen** – Verträge vor Audits durch Dritte bereinigen.

## Leistungstipps
- Regex‑Muster so spezifisch wie möglich halten, um die Verarbeitungszeit zu reduzieren.  
- Die `Redactor`‑Instanz sofort freigeben (wie gezeigt `try‑ Für Stapelverarbeitung das Queuen von Jobs und das Ausführen in parallelen Threads in Betracht ziehen.

## Häufig gestellte Fragen

**Q: Was ist OCR‑Redaktion?**Q: Kann ich GroupDocs.Redaction ohne Azure OCR verwenden?**  
A: Ja, aber OCR verbessert die Genauigkeit bei gescannten Dokumenten erheblich, sodass Sie **gescannte Dokumente** effektiv **redig mit komplexen Regex‑Mustern um?**  
A: Muster mit Beispieldaten testen, Wortgrenzen (`\b`) verwenden, um Teilübereinstimmungen zu vermeiden, und große Ausdrücke in mehrere einfachere Redaktionen aufteilen.

**Q: Was sind typische Leistungsengpässe?**  
A: Aufwändige OCR‑Aufrufe bei großen Dateien, zu breit gefasste Regex und unzureichende Speicherzuweisung. Optimieren Sie durch Feinabstimmung der Regex und Skalierung der Ressourcen.

**Q: Wo kann ich Hilfe erhalten, wenn ich auf Probleme stoße?**  
A: Stellen Sie Fragen im GroupDocs‑Community‑Forum: [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33).

## Zusätzliche Ressourcen
- **Dokumentation**: https://docs.groupdocs.com/redaction/java/  
- **API Reference**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Free Support**: https://forum.groupdocs.com/c/redaction/33  
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

---

**Zuletzt aktualisiert:** 2026-01-21  
**Getestet mit:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs