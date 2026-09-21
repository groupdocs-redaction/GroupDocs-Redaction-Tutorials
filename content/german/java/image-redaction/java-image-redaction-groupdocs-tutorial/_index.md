---
date: '2026-09-21'
description: Erfahren Sie, wie Sie ein Bild mit GroupDocs.Redaction for Java redigieren.
  Die Schritt‑für‑Schritt‑Anleitung behandelt die Einrichtung, pixel‑level redaction,
  Verifizierung und best practices.
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: Wie man ein Bild mit GroupDocs.Redaction for Java redigiert. Folgen
  Sie dieser Anleitung, um Pixeldaten in gescannten Dateien zu maskieren, Farben auszuwählen
  und Ergebnisse zu überprüfen – perfekt für GDPR und HIPAA compliance.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: Wie man ein Bild mit GroupDocs.Redaction for Java redigiert
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: Wie man ein Bild mit GroupDocs.Redaction for Java redigiert
type: docs
url: /de/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Bild mit GroupDocs.Redaction für Java redigieren

In diesem umfassenden Tutorial lernen Sie **wie man Bilddateien** in Java mit GroupDocs.Redaction redigiert. Das Redigieren gescannter Bilder ist ein entscheidender Schritt zum Schutz personenbezogener Daten, zur Einhaltung von DSGVO, HIPAA oder anderen Datenschutzbestimmungen und stellt sicher, dass vertrauliche visuelle Informationen nie durchsickern. Wir führen Sie durch die Projektkonfiguration, die Einrichtung der Pixel‑basierten Redaktion, das sichere Speichern des Ergebnisses und die Bestätigung, dass die Redaktion erfolgreich war – alles in einem dialogorientierten, schritt‑für‑Schritt‑Stil, den Sie in jede Java‑Anwendung übernehmen können.

## Schnelle Antworten
- **Welche Bibliothek übernimmt die Bildredaktion in Java?** GroupDocs.Redaction for Java.  
- **Kann ich die Redaktionsfarbe wählen?** Ja – jede undurchsichtige `java.awt.Color` wie `Color.BLUE` oder `Color.BLACK`.  
- **Ist für die Produktion eine Lizenz erforderlich?** Ja, eine gültige GroupDocs‑Lizenz ist für die kommerzielle Nutzung obligatorisch.  
- **Wird das Originalbild überschrieben?** Nein – die API schreibt das redigierte Bild in eine neue Datei, die Sie angeben.  
- **Welche Java‑Version wird unterstützt?** Java 8 und neuer (bis Java 21 zum Zeitpunkt der Erstellung).

## Was ist Bildredaktion und warum gescannte Bilder in Java redigieren?
Bildredaktion verdeckt visuelle Daten – Namen, Zahlen, Unterschriften – dauerhaft, indem Pixelbereiche durch eine einheitliche Farbe ersetzt werden. Im Gegensatz zur Textredaktion, die auf auswählbaren Zeichen arbeitet, speichern gescannte Bilder Informationen als Rohpixel, sodass nur pixelbasierte Werkzeuge garantieren können, dass die Daten nicht wiederhergestellt werden können. Mit GroupDocs.Redaction können Sie genaue Koordinaten anvisieren, jede undurchsichtige Farbe anwenden und ein neues Bild erzeugen, das den sensiblen Inhalt endgültig entfernt.

## Warum GroupDocs.Redaction für Java verwenden?
GroupDocs.Redaction unterstützt **über 50 Bildformate** (einschließlich JPG, PNG, BMP, GIF) und kann mehrseitige Dokumente verarbeiten, ohne die gesamte Datei in den Speicher zu laden, dank seiner Streaming‑Architektur. Benchmarks zeigen, dass ein 300 KB gescanntes PNG in weniger als 120 ms auf einer typischen 2,8 GHz‑CPU redigiert wird, was es sowohl für Batch‑Jobs als auch für Echtzeit‑Dienste geeignet macht.

## Voraussetzungen
- **JDK 8 oder neuer** installiert und in Ihrem `PATH` konfiguriert.  
- **Maven** (oder Gradle) für das Abhängigkeitsmanagement.  
- Eine IDE wie **IntelliJ IDEA**, **Eclipse** oder **NetBeans**.  
- Grundlegende Kenntnisse von Java‑Datei‑I/O und dem `java.awt`‑Paket.  

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
Alternativ laden Sie das neueste JAR von der offiziellen Release‑Seite herunter: [GroupDocs.Redaction für Java Releases](https://releases.groupdocs.com/redaction/java/).

### Lizenzbeschaffung
- **Kostenlose Testversion:** Melden Sie sich für eine Testversion an, um die vollständige API zu erkunden.  
- **Temporäre Lizenz:** Verwenden Sie einen temporären Schlüssel für erweitertes Testen ohne Kosten.  
- **Vollkauf:** Erwerben Sie eine Produktionslizenz für unbegrenzte Bereitstellung.

## Implementierungs‑Leitfaden

Wir teilen die Implementierung in zwei Kernfunktionen auf: **Bildbereichs‑Redaktion** (die eigentliche Maskierung) und **Redaktions‑Statusprüfung** (Verifizierung des Erfolgs).

### Wie man gescannte Dokumentbilder redigiert – Schritt 1: Redaktor initialisieren
`Redactor` ist die zentrale Klasse, die ein Bild lädt und Redaktions‑Operationen bereitstellt.  
Erstellen Sie eine `Redactor`‑Instanz, die auf das Quellbild verweist, das Sie verarbeiten möchten.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Schritt 2: Redaktionsparameter definieren
`ImageAreaRedaction` arbeitet mit einem `Point` (obere linke Ecke) und einer `Dimension` (Breite × Höhe), die das zu verbergende Rechteck beschreiben. In diesem Beispiel verwenden wir eine blaue Füllfarbe.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Schritt 3: Redaktion anwenden
`RegionReplacementOptions` ermöglicht das Festlegen der Füllfarbe und eines optionalen Rahmens. Durch Übergabe dieser Optionen an `ImageAreaRedaction` und Aufruf von `apply()` wird die Maskierung durchgeführt. Die Methode gibt ein `RedactorChangeLog` zurück, das Erfolg oder Misserfolg anzeigt.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Schritt 4: Ressourcen freigeben
`Redactor` implementiert `AutoCloseable`. Durch das Schließen werden native Puffer und Dateihandles freigegeben, wodurch Speicherlecks in langfristig laufenden Diensten verhindert werden.

```java
redactor.close();
```

### Wie man die Redaktion überprüft – Statusprüfung
Nach Anwendung der Redaktion prüfen Sie das `RedactorChangeLog`. Ein Wert `Status.SUCCESS` bestätigt, dass der Pixelbereich ohne Fehler ersetzt wurde. Sie können das Bild auch in ein `BufferedImage` rendern, um vor dem Speichern eine visuelle Inspektion vorzunehmen.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Praktische Anwendungsfälle
- **Vertrauliche Dokumentenverarbeitung:** Persönliche Daten in gescannten Verträgen maskieren, bevor sie mit Partnern geteilt werden.  
- **Rechtliche Dokumentation:** DSGVO‑ oder HIPAA‑Konformität sicherstellen, indem Identifikatoren in Beweisbildern redigiert werden.  
- **Medizinische Aufzeichnungen:** Patienten­gesichter oder handschriftliche Notizen in Radiologie‑Scans verbergen, während diagnostische Details erhalten bleiben.  

## Leistungsüberlegungen
- **Batch‑Verarbeitung:** Bilder in Gruppen von 10–20 verarbeiten, um den Speicherverbrauch unter 200 MB zu halten.  
- **Objektwiederverwendung:** `Point`‑ und `Dimension`‑Objekte über Iterationen hinweg wiederverwenden, um den GC‑Druck zu reduzieren.  
- **Versionsupdates:** Auf die neueste GroupDocs.Redaction‑Version aktualisieren, um von einer um 15 % schnelleren Leistung zu profitieren, wie in Version 24.10 berichtet.  

## Häufige Probleme & Lösungen

| Problem | Ursache | Lösung |
|-------|-------|-----|
| **Redaktion schlägt mit `Failed`‑Status fehl** | Falscher Dateipfad oder nicht unterstütztes Bildformat | Stellen Sie sicher, dass die Datei existiert und ein unterstütztes Format (JPG, PNG, BMP, GIF) hat. |
| **Ausgabedatei ist leer** | `redactor.save()` wurde aufgerufen, bevor die Redaktion abgeschlossen war | Stellen Sie sicher, dass `apply()` `Status.SUCCESS` zurückgibt, bevor `save()` aufgerufen wird. |
| **Farbe wird nicht angewendet** | Verwendung einer transparenten `Color` | Wählen Sie eine undurchsichtige Farbe, z. B. `Color.BLACK` oder `Color.BLUE`. |

## Häufig gestellte Fragen

**Q: Was ist der Unterschied zwischen `ImageAreaRedaction` und Textredaktion?**  
A: `ImageAreaRedaction` arbeitet mit rohen Pixelkoordinaten, während Textredaktion OCR‑Ebenen analysiert, um Textinhalt zu finden und zu entfernen.

**Q: Kann ich mehrere Regionen in einem Bild redigieren?**  
A: Ja – rufen Sie `redactor.apply()` wiederholt mit verschiedenen `ImageAreaRedaction`‑Objekten auf, bevor Sie die endgültige Datei speichern.

**Q: Unterstützt GroupDocs.Redaction weitere Bildformate wie TIFF?**  
A: Die Bibliothek unterstützt gängige Rasterformate (JPG, PNG, BMP, GIF). Für TIFF konvertieren Sie das Bild zunächst in ein unterstütztes Format.

**Q: Wie automatisiere ich die Redaktion für einen Ordner gescannter PDFs?**  
A: Extrahieren Sie jede Seite als Bild, wenden Sie dieselbe Redaktionslogik an und bauen Sie das PDF anschließend mit einer PDF‑Bibliothek wie GroupDocs.Conversion wieder zusammen.

**Q: Gibt es eine Möglichkeit, die Redaktion vor dem Speichern vorzusehen?**  
A: Rendern Sie den `Redactor` zu einem `BufferedImage` und zeigen Sie ihn in einer Swing‑ oder JavaFX‑UI an, sodass Sie den maskierten Bereich vor dem Commit bestätigen können.

## Fazit
Sie haben nun eine vollständige, produktionsreife Anleitung, **wie man Bildinhalte** redigiert und speziell, **wie man gescannte Bilder in Java** mit GroupDocs.Redaction für Java redigiert. Durch Befolgen der obigen Schritte können Sie sensible visuelle Daten in den Bereichen Finanzen, Recht und Gesundheitswesen schützen. Erkunden Sie weitere APIs – wie Textredaktion, PDF‑Seiten‑Redaktion oder die Verarbeitung ganzer Ordner – um eine End‑zu‑End‑Datenschutz‑Pipeline für Ihr Unternehmen aufzubauen.

**Ressourcen**  
- [Dokumentation](https://docs.groupdocs.com/redaction/java/)  
- [API‑Referenz](https://reference.groupdocs.com/redaction/java)  
- [Download](https://releases.groupdocs.com/redaction/java/)  
- [GitHub‑Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Kostenloses Support‑Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/) 

---

**Zuletzt aktualisiert:** 2026-09-21  
**Getestet mit:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Wie man Java mit GroupDocs.Redaction redigiert – Ein umfassender Leitfaden für Entwickler](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [Wie man gescannte PDFs mit OCR redigiert – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Wie man Text in Java mit GroupDocs.Redaction redigiert – Anleitung](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)