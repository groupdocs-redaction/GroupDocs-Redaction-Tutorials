---
date: '2026-02-26'
description: Erfahren Sie, wie Sie Text mit GroupDocs.Redaction Java schwärzen und
  als gerastertes PDF mit exakter Phrasenersetzung und benutzerdefinierten PDF‑Einstellungen
  speichern.
keywords:
- GroupDocs.Redaction Java
- text redaction Java
- rasterized PDF conversion
title: Wie man Text mit GroupDocs.Redaction Java schwärzt
type: docs
url: /de/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# Wie man Text mit GroupDocs.Redaction Java redigiert

In der heutigen datengetriebenen Welt ist **wie man Text redigiert** in einem Dokument sicher und effizient ein Hauptanliegen für Entwickler und Compliance‑Beauftragte gleichermaßen. Ob Sie persönliche Kennungen, vertrauliche Kundendaten oder interne Projektcodes verbergen müssen, GroupDocs.Redaction for Java bietet Ihnen eine zuverlässige Möglichkeit, exakte Phrasen zu finden und durch sichere Overlays zu ersetzen. Dieses Tutorial zeigt Ihnen außerdem **wie man als rasterisiertes PDF speichert**, wobei jede Seite in ein bildbasiertes PDF umgewandelt wird, das den Archivierungsstandards entspricht.

## Schnelle Antworten
- **Was ist die primäre Klasse für die Redaktion?** `Redactor`  
- **Kann ich eine Phrase durch ein farbiges Overlay ersetzen?** Ja, mit `ExactPhraseRedaction` und `ReplacementOptions`.  
- **Wie erstelle ich ein rasterisiertes PDF?** Aktivieren Sie die Rasterisierung über `SaveOptions.getRasterization().setEnabled(true)`.  
- **Welches PDF‑Compliance‑Level wird im Beispiel verwendet?** `PdfComplianceLevel.PdfA1a`.  
- **Benötige ich eine Lizenz für den Produktionseinsatz?** Eine gültige GroupDocs.Redaction‑Lizenz ist für Produktionsbereitstellungen erforderlich.

## Was bedeutet „wie man Text redigiert“ in Java?
Redaktion ist der Prozess, bei dem sensible Inhalte dauerhaft entfernt oder unkenntlich gemacht werden. Mit GroupDocs.Redaction können Sie programmgesteuert nach einer exakten Phrase suchen – etwa einem Namen oder einer ID – und diese durch ein rotes Overlay, ein schwarzes Kästchen oder ein beliebiges benutzerdefiniertes visuelles Element ersetzen, sodass die ursprünglichen Daten nicht wiederhergestellt werden können.

## Warum GroupDocs.Redaction für Java verwenden?
- **Exakte Phrasenerkennung** eliminiert Fehlalarme.  
- **Integrierte Rasterisierung** ermöglicht die Erstellung von PDF/A‑konformen, rein bildbasierten PDFs für die Langzeitspeicherung.  
- **Cross‑Format‑Unterstützung** funktioniert mit DOCX, PDF, PPTX und mehr, sodass Sie denselben Code für verschiedene Dokumenttypen verwenden können.  
- **Performance‑orientierte API** ermöglicht die Stapelverarbeitung großer Dokumentensätze bei geringem Speicherverbrauch.

## Voraussetzungen
Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- **GroupDocs.Redaction for Java** (v24.9 oder neuer).  
- **Java Development Kit (JDK) 8+**.  
- Eine IDE wie IntelliJ IDEA, Eclipse oder NetBeans.  
- Maven für das Abhängigkeitsmanagement.  

### Erforderliche Bibliotheken und Abhängigkeiten
- **GroupDocs.Redaction for Java** – fügen Sie das Repository und die Abhängigkeit zu Ihrer `pom.xml` hinzu (siehe Code‑Block unten).  
- **Optional**: Beliebige zusätzliche Logging‑Bibliotheken nach Wahl.

### Wissensvoraussetzungen
- Grundlegende Java‑Syntax und Datei‑I/O.  
- Vertrautheit mit der Struktur von Maven’s `pom.xml`.

## Einrichtung von GroupDocs.Redaction für Java
### Maven‑Einrichtung
Add the repository and dependency to your `pom.xml` file:

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
Below is the minimal code to create a `Redactor` instance pointing at a sample DOCX file:

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## Wie man Text redigiert – Beispiel für exakte Phrase
### Schritt 1: Erforderliche Klassen importieren
These imports give you access to the redaction engine and replacement options:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

### Schritt 2: Redaktion erstellen und anwenden
The following snippet searches for the phrase **“John Doe”** and replaces it with a red overlay:

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

**Warum das wichtig ist:** `ReplacementOptions` ermöglicht es Ihnen, den visuellen Stil der Redaktion zu steuern, sodass der versteckte Inhalt nicht durch Kopieren‑Einfügen oder OCR wiederhergestellt werden kann.

## Wie man als rasterisiertes PDF speichert
### Schritt 1: SaveOptions‑Klassen importieren
These classes let you configure PDF output, including rasterization and compliance levels:

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

### Schritt 2: Speicheroptionen konfigurieren und anwenden
After redacting, you can export the document as a rasterized PDF. The example below rasterizes page 5 only and forces PDF/A‑1a compliance:

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

**Wichtiger Punkt:** Das Rasterisieren eines PDFs **wandelt jede Seite in ein Bild um**, wodurch verborgene Textebenen entfernt werden und das Dokument manipulationssicher wird – ideal für die rechtliche Archivierung.

## Praktische Anwendungen
1. **Redaktion sensibler Daten** – Persönliche Kennungen automatisch verbergen, bevor Verträge geteilt werden.  
2. **Dokumentenarchivierung** – Abschließende Berichte in rasterisiertes PDF/A umwandeln für langfristige Konformität.  
3. **Massenhafte Inhaltsaktualisierung** – Veraltete Terminologie in Hunderten von Dateien mit einem einzigen Skript ersetzen.

## Leistungsüberlegungen
- **Schließen Sie den `Redactor`** nach jeder Operation, um Dateihandles und Speicher freizugeben.  
- **Stapelverarbeitung** – Laden Sie eine Dateiliste und iterieren Sie darüber, wobei Sie nach Möglichkeit eine einzelne `Redactor`‑Instanz wiederverwenden.  
- **Ressourcen überwachen** – Verwenden Sie Java‑Profiling‑Tools, um CPU‑ und Heap‑Nutzung während großflächiger Redaktionen zu beobachten.

## Häufig gestellte Fragen

**F: Wie installiere ich GroupDocs.Redaction in einem Maven‑Projekt?**  
A: Fügen Sie das GroupDocs‑Repository und die `groupdocs-redaction`‑Abhängigkeit zu Ihrer `pom.xml` hinzu, wie im Abschnitt Maven‑Einrichtung gezeigt.

**F: Kann ich Text aus PDF‑Dateien mit dieser Bibliothek redigieren?**  
A: Ja, GroupDocs.Redaction unterstützt PDF, DOCX, PPTX und viele weitere Formate.

**F: Was passiert, wenn die exakte Phrase nicht gefunden wird?**  
A: Der `RedactorChangeLog` gibt den Status `Failed` zurück. Überprüfen Sie die Schreibweise und Groß‑/Kleinschreibung der Phrase.

**F: Wie kann ich sehr große Dokumente effizient verarbeiten?**  
A: Verarbeiten Sie sie in kleineren Seitenbereichen, aktivieren Sie die Rasterisierung nur bei Bedarf und schließen Sie stets den `Redactor`, um Ressourcen freizugeben.

**F: Ist es möglich, rasterisierte PDFs mit bestimmten Seitenbereichen zu speichern?**  
A: Absolut. Verwenden Sie `options.getRasterization().setPageIndex()` und `setPageCount()`, um die genauen Seiten zu bestimmen, die Sie rasterisieren möchten.

## Fazit
Sie haben nun eine vollständige, durchgängige Anleitung zum **wie man Text redigiert** mit GroupDocs.Redaction Java und **wie man als rasterisiertes PDF speichert**. Durch Befolgen dieser Schritte können Sie sensible Informationen schützen, Compliance‑Anforderungen erfüllen und hohe Leistung in Produktionsumgebungen aufrechterhalten.

**Nächste Schritte**  
- Tauchen Sie tiefer in die API ein, indem Sie die [offizielle Dokumentation](https://docs.groupdocs.com/redaction/java/) erkunden.  
- Experimentieren Sie mit anderen Redaktionstypen (z. B. `RegexRedaction`, `ImageRedaction`).  
- Treten Sie der Community im [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) bei für Tipps und bewährte Verfahren.

---

**Zuletzt aktualisiert:** 2026-02-26  
**Getestet mit:** GroupDocs.Redaction Java 24.9  
**Autor:** GroupDocs