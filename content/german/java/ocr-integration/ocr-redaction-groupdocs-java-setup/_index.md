---
date: '2026-02-08'
description: Erfahren Sie, wie Sie sensible Daten maskieren und PDF‑Java‑Dateien mit
  GroupDocs OCR Redaction und Microsoft Azure OCR redigieren.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: Vertrauliche Daten in PDFs mit GroupDocs OCR‑Redaktion maskieren
type: docs
url: /de/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Sensible Daten in PDFs mit GroupDocs OCR Redaction maskieren

In der heutigen digitalen Landschaft ist der Schutz persönlicher und vertraulicher Informationen oberste Priorität. In diesem Tutorial **lernen Sie, wie Sie sensible Daten** in PDF-Dateien maskieren, indem Sie GroupDocs Redaction mit Microsoft Azure OCR kombinieren. Dieser Ansatz bietet Ihnen zuverlässige Texterkennung auf gescannten Seiten und ermöglicht es Ihnen, **PDF Java**-Dokumente präzise zu redigieren, um die Einhaltung von Datenschutzbestimmungen sicherzustellen.

## Schnelle Antworten
- **Was bedeutet „mask sensitive data“?** Es ersetzt identifizierten vertraulichen Text durch einen Platzhalter (z. B. `[REDACTED]`).  
- **Welche Bibliothek übernimmt OCR?** Microsoft Azure OCR‑Connector, verwendet über GroupDocs Redaction.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Evaluierung; für die Produktion ist eine permanente Lizenz erforderlich.  
- **Kann ich gescannte PDFs redigieren?** Ja – OCR extrahiert den versteckten Text, bevor reguläre Ausdrucks‑Redaktionen angewendet werden.  
- **Ist diese Lösung nur für Java?** Das Beispiel ist Java‑basiert, aber GroupDocs bietet ähnliche APIs für .NET und andere Plattformen.

## Was ist OCR‑basierte Redaktion?
OCR‑basierte Redaktion führt zunächst Optical Character Recognition auf jeder Seite eines Dokuments aus und wandelt Textbilder in durchsuchbare Zeichenketten um. Sobald der Text durchsuchbar ist, können Sie reguläre Ausdrucks‑ (Regex‑) Regeln anwenden, um sensible Informationen zu finden – wie Sozialversicherungsnummern, Kreditkartennummern oder persönliche Kennungen – und diese durch eine Maske wie **`[REDACTED]`** ersetzen.

## Warum GroupDocs Redaction mit Azure OCR verwenden?
- **Hohe Genauigkeit** bei gescannten PDFs und Bildern.  
- **Nahtlose Java‑Integration** über Maven oder direkten JAR‑Download.  
- **Flexibles Regex‑Engine** ermöglicht das Definieren benutzerdefinierter Muster für jeden Datentyp.  
- **Skalierbar** für große Dokumenten‑Batches, mit Optionen für asynchrone Verarbeitung.

## Voraussetzungen
- **Java Development Kit (JDK) 8+** installiert.  
- **Maven** (wenn Sie die Abhängigkeitsverwaltung bevorzugen) oder die Möglichkeit, JARs manuell herunterzuladen.  
- **Microsoft Azure OCR‑Anmeldeinformationen** (Endpunkt und Abonnementschlüssel).  
- Grundlegende Java‑Kenntnisse und Vertrautheit mit regulären Ausdrücken.

## Einrichtung von GroupDocs Redaction für Java

### Maven‑Einrichtung
Add the GroupDocs repository and dependency to your `pom.xml`:

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
- **Kostenlose Testversion** – alle Funktionen ohne Kosten testen.  
- **Temporäre Lizenz** – Evaluationszeit verlängern.  
- **Vollständige Lizenz** – produktionsreife Funktionen freischalten.

### Grundlegende Initialisierung und Einrichtung
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## So maskieren Sie sensible Daten mit OCR‑Redaktion

### Schritt 1: Laden des Dokuments mit OCR‑Einstellungen
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – ersetzen Sie dies durch den Pfad zu Ihrer PDF.  
- **`LoadOptions`** – Standard‑Ladevorgang; bei Bedarf anpassbar.  
- **`settings`** – enthält den Azure OCR‑Connector, den Sie zuvor erstellt haben.

### Schritt 2: Definieren und Anwenden von Regex‑Redaktionen
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
- Das Muster `\b\d{3}-\d{2}-\d{4}\b` entspricht US‑Sozialversicherungsnummern.  
- `ReplacementOptions("[REDACTED]")` ersetzt jedes gefundene Vorkommen durch die Maske und **maskiert damit sensible Daten**.

## Häufige Anwendungsfälle für das Maskieren sensibler Daten
1. **Verwaltung rechtlicher Dokumente** – Kundenkennungen vor dem Teilen von Entwürfen verbergen.  
2. **Finanzberichterstattung** – Kontonummern und Transaktions‑IDs schützen.  
3. **Gesundheitsakten** – HIPAA‑Konformität durch Redaktion von Patientenkennungen.  
4. **Regierungsveröffentlichungen** – persönliche Daten aus öffentlichen Aufzeichnungen entfernen.  
5. **Unternehmensverträge** – proprietäre Bedingungen während externer Prüfungen verbergen.

## Leistungstipps
- **Regex optimieren** – vermeiden Sie zu breite Muster, die die Verarbeitungszeit erhöhen.  
- **Speicherverwaltung** – schließen Sie die `Redactor`‑Instanz umgehend (try‑with‑resources erledigt dies automatisch).  
- **Asynchrone Ausführung** – für die Massenverarbeitung Redaktionsjobs in separaten Threads ausführen oder eine Aufgabenwarteschlange nutzen.

## Fehlerbehebung
- **Azure‑Anmeldeinformationen‑Fehler** – prüfen Sie die Endpunkt‑URL und den Abonnementschlüssel in `MicrosoftAzureOcrConnector`.  
- **Dokument wird nicht geladen** – prüfen Sie den Dateipfad und stellen Sie sicher, dass das PDF nicht passwortgeschützt ist (oder übergeben Sie das Passwort via `LoadOptions`).  
- **Keine Redaktionen angewendet** – testen Sie Ihr Regex zuerst mit einem einfachen String; verwenden Sie `Pattern.compile` in einem Unit‑Test, um Treffer zu bestätigen.

## Häufig gestellte Fragen

**Q: Was ist OCR‑Redaktion?**  
A: OCR‑Redaktion verwendet Optical Character Recognition, um versteckten Text aus Bildern oder gescannten PDFs zu extrahieren, und wendet anschließend Redaktionsregeln an, um diesen Text zu maskieren.

**Q: Kann ich GroupDocs Redaction ohne Azure OCR verwenden?**  
A: Ja, aber OCR verbessert die Genauigkeit bei gescannten Dokumenten, bei denen die native Textextraktion fehlschlägt, erheblich.

**Q: Wie gehe ich mit komplexen Regex‑Mustern um?**  
A: Erstellen und testen Sie sie schrittweise, indem Sie die Java‑Klasse `Pattern` in einer Sandbox verwenden, bevor Sie sie auf große Dokumente anwenden.

**Q: Was sind typische Leistungsengpässe?**  
A: Große PDFs, zu komplexe Regex‑Muster und synchrone OCR‑Aufrufe können die Verarbeitung verlangsamen; erwägen Sie Batch‑Verarbeitung und optimierte Muster.

**Q: Ist Support für Implementierungsprobleme verfügbar?**  
A: Auf jeden Fall – wenden Sie sich über das [GroupDocs‑Forum](https://forum.groupdocs.com/c/redaction/33) an die Community oder kontaktieren Sie den GroupDocs‑Support.

## Zusätzliche Ressourcen
- **Dokumentation**: https://docs.groupdocs.com/redaction/java/  
- **API‑Referenz**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Kostenloser Support**: https://forum.groupdocs.com/c/redaction/33  
- **Temporäre Lizenz**: https://purchase.groupdocs.com/temporary-license/

---

**Zuletzt aktualisiert:** 2026-02-08  
**Getestet mit:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs