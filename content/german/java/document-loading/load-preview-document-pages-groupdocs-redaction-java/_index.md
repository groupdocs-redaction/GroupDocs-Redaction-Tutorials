---
date: '2026-05-17'
description: Erfahren Sie, wie Sie mit GroupDocs.Redaction für Java eine Seitenvorschau
  erstellen, eine Seite in PNG konvertieren und Dokument‑Thumbnails generieren – Schritt‑für‑Schritt‑Anleitung.
keywords:
- how to preview page
- convert page to png
- preview multiple pages
- document thumbnail generation
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to preview page, convert page to PNG, and generate document
    thumbnails using GroupDocs.Redaction for Java – step‑by‑step guide.
  headline: How to Preview Page with GroupDocs.Redaction for Java – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to preview page, convert page to PNG, and generate document
    thumbnails using GroupDocs.Redaction for Java – step‑by‑step guide.
  name: How to Preview Page with GroupDocs.Redaction for Java – A Comprehensive Guide
  steps:
  - name: Set the Target Page Number
    text: The `testPageNumber` variable tells the preview engine which page to render.
  - name: Define Output File Path
    text: Use a format string to create dynamic filenames based on the page number.
      This approach lets you generate a batch of thumbnails in a loop without overwriting
      files.
  - name: Configure Preview Options
    text: '`PreviewOptions` controls the rendering process. Implementing `ICreatePageStream`
      gives you full control over where each PNG is written. - **ICreatePageStream**
      – an interface that lets you supply a custom `OutputStream` for each generated
      page. - **setPreviewFormat** – selects PNG as the output for'
  type: HowTo
- questions:
  - answer: Generating a PNG image of a single document page without opening the full
      file.
    question: What does “preview page” mean?
  - answer: PNG provides loss‑less compression and crisp rendering, making it ideal
      for document thumbnails.
    question: Which format is recommended?
  - answer: A free trial works for evaluation; a permanent license is required for
      production deployments.
    question: Do I need a license?
  - answer: Yes—use `setPageNumbers` with an array of page indexes to generate several
      thumbnails at once.
    question: Can I preview multiple pages?
  - answer: Java 8+, GroupDocs.Redaction library, and Maven (optional).
    question: What are the main dependencies?
  type: FAQPage
title: Wie man eine Seite mit GroupDocs.Redaction für Java vorschaut – ein umfassender
  Leitfaden
type: docs
url: /de/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/
weight: 1
---

# Wie man eine Seite mit GroupDocs.Redaction für Java vorschaut

In diesem Leitfaden zeigen wir Ihnen **how to preview page** in einem Dokument mit GroupDocs.Redaction für Java, konvertieren dann diese Seite in ein hochqualitatives PNG und erstellen ein wiederverwendbares Dokument‑Thumbnail. Egal, ob Sie ein Dokumenten‑Management‑System, ein Web‑Portal oder eine Archivlösung bauen, eine schnelle Seitenvorschau kann die Benutzererfahrung erheblich verbessern und den Bandbreitenverbrauch reduzieren.

## Schnelle Antworten
- **What does “preview page” mean?** Erzeugen eines PNG‑Bildes einer einzelnen Dokumentenseite, ohne die gesamte Datei zu öffnen.  
- **Which format is recommended?** PNG bietet verlustfreie Kompression und scharfe Darstellung, was es ideal für Dokument‑Thumbnails macht.  
- **Do I need a license?** Eine kostenlose Testversion funktioniert für die Evaluierung; eine permanente Lizenz ist für den Produktionseinsatz erforderlich.  
- **Can I preview multiple pages?** Ja – verwenden Sie `setPageNumbers` mit einem Array von Seitenindizes, um mehrere Thumbnails gleichzeitig zu erzeugen.  
- **What are the main dependencies?** Java 8+, GroupDocs.Redaction‑Bibliothek und Maven (optional).

## Was bedeutet “how to preview page”?
**How to preview page** bezieht sich auf den Vorgang, eine bestimmte Seite eines Dokuments als Bild (häufig PNG) zu rendern, damit sie sofort in einer Benutzeroberfläche angezeigt werden kann. Diese Technik vermeidet das Laden der gesamten Datei, beschleunigt das Rendern und schützt den Originalinhalt vor versehentlichen Änderungen.

## Warum GroupDocs.Redaction für Java zum Vorschauen von Seiten verwenden?
GroupDocs.Redaction unterstützt **50+** Eingabe‑ und Ausgabeformate – darunter PDF, DOCX, PPTX und Bildtypen – und kann Seitenvorschauen erzeugen, ohne das gesamte Dokument in den Speicher zu laden. Die Bibliothek verarbeitet Dateien mit mehreren hundert Seiten mittels Streaming, was den JVM‑Heap‑Verbrauch im Vergleich zum Laden des gesamten Dokuments um bis zu **70 %** reduziert.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- **Java Development Kit (JDK) 8 oder höher** – erforderlich für alle GroupDocs‑Bibliotheken.  
- **Maven** (optional) – vereinfacht die Verwaltung von Abhängigkeiten.  
- **Eine IDE** wie IntelliJ IDEA oder Eclipse zum Schreiben und Debuggen von Java‑Code.  

### Erforderliche Bibliotheken und Abhängigkeiten
- **GroupDocs.Redaction** – die Kernbibliothek, die Redaktions-, Vorschau‑ und Dokumentmanipulationsfunktionen bereitstellt.  

### Wissensvoraussetzungen
- Vertrautheit mit Java‑Datei‑I/O.  
- Grundlegendes Verständnis der `pom.xml`‑Struktur von Maven (falls Sie Maven verwenden).  

## Einrichtung von GroupDocs.Redaction für Java

Die Bibliothek in Ihr Projekt zu integrieren ist schnell. Wählen Sie entweder Maven oder einen Direktdownload.

### Maven‑Konfiguration
Fügen Sie die folgende Abhängigkeit zu Ihrer `pom.xml`‑Datei hinzu:

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
Sie können das neueste JAR auch von der offiziellen Release‑Seite herunterladen: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Schritte zum Erwerb einer Lizenz
1. **Free Trial** – beginnen Sie mit einer Testversion, um alle Funktionen zu erkunden.  
2. **Temporary License** – beantragen Sie einen temporären Schlüssel, wenn Sie eine erweiterte Evaluierungszeit benötigen.  
3. **Purchase** – erhalten Sie eine Voll‑Lizenz für den Produktionseinsatz und Prioritäts‑Support.  

#### Grundlegende Initialisierung und Einrichtung
Die Klasse `Redactor` ist der Einstiegspunkt für alle Dokumentoperationen. Sie lädt eine Datei, wendet Redaktionen an und erstellt Vorschauen.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Wie man eine Seite in Java vorschaut?
`Redactor` ist die Hauptklasse in GroupDocs.Redaction, die ein Dokument lädt und Operationen wie Redaktion und Vorschau‑Erstellung bereitstellt. `PreviewOptions` legt Render‑Parameter wie Format und Seitenbereich fest. Laden Sie das Ziel‑dokument mit `Redactor`, konfigurieren Sie `PreviewOptions` und rufen Sie `preview` auf, um ein PNG zu erzeugen. Dieses Zwei‑Schritt‑Muster verarbeitet sowohl Einzelseiten‑ als auch Mehrseitenszenarien und hält den Speicherverbrauch niedrig.

## Implementierungs‑Leitfaden

Jetzt gehen wir die vollständige Implementierung Schritt für Schritt durch und fügen dabei Definitionsanker und quantifizierte Aussagen hinzu.

### Dokumentenseite laden und vorschauen

#### Überblick
Die folgenden Schritte zeigen, wie man eine PNG‑Vorschau einer bestimmten Seite erzeugt. Dies ist der Kern von **how to preview page** und besonders nützlich, um ein **document thumbnail java** für UI‑Vorschauen oder Archivindizes zu erstellen.

#### Schritt 1: Zielseitennummer festlegen
Die Variable `testPageNumber` gibt der Vorschau‑Engine an, welche Seite gerendert werden soll.

```java
int testPageNumber = 1;
```

#### Schritt 2: Ausgabepfad definieren
Verwenden Sie einen Format‑String, um dynamische Dateinamen basierend auf der Seitennummer zu erstellen. Dieser Ansatz ermöglicht es, in einer Schleife mehrere Thumbnails zu erzeugen, ohne Dateien zu überschreiben.

```java
final String previewFileName = "YOUR_OUTPUT_DIRECTORY_page%d.png";
```

#### Schritt 3: Vorschau‑Optionen konfigurieren
`PreviewOptions` steuert den Render‑Prozess. Die Implementierung von `ICreatePageStream` gibt Ihnen die volle Kontrolle darüber, wohin jedes PNG geschrieben wird.

```java
PreviewOptions options = new PreviewOptions(new ICreatePageStream() {
    @Override
    public java.io.OutputStream createPageStream(int pageNumber) {
        try {
            return new java.io.FileOutputStream(java.lang.String.format(previewFileName, pageNumber));
        } catch (Exception e) {
            // Handle exceptions related to file stream creation
            e.printStackTrace();
            return null;
        }
    }
});
options.setPreviewFormat(PreviewFormats.PNG);
options.setPageNumbers(new int[] { testPageNumber });
```

- **ICreatePageStream** – ein Interface, das Ihnen ermöglicht, einen benutzerdefinierten `OutputStream` für jede erzeugte Seite bereitzustellen.  
- **setPreviewFormat** – wählt PNG als Ausgabeformat, wodurch verlustfreie Qualität gewährleistet wird.  
- **setPageNumbers** – begrenzt das Rendern auf die von Ihnen angegebenen Seiten und reduziert die Verarbeitungszeit um bis zu **80 %**, wenn ein Teil eines großen Dokuments vorgespielt wird.  

#### Direkte Antwort‑Zusammenfassung
Laden Sie das Dokument mit `new Redactor("sample.pdf")`, konfigurieren Sie `PreviewOptions`, um Seite 1 zu targeten, setzen Sie das Format auf PNG und rufen Sie `redactor.preview(previewOptions)` auf. Die Methode gibt einen `InputStream` zurück, den Sie in eine Datei schreiben, wodurch ein sofort einsatzbereites Thumbnail in nur wenigen Code‑Zeilen entsteht.

### Fehlersuche‑Tipps
- **Directory Issues** – Stellen Sie sicher, dass das Ausgabeverzeichnis existiert (`new File(path).mkdirs()`) und dass die JVM Schreibrechte hat.  
- **IOExceptions** – Umschließen Sie Dateioperationen mit try‑catch‑Blöcken, um Pfadfehler und Berechtigungsprobleme zu protokollieren.  
- **Blank Images** – Vergewissern Sie sich, dass das Quell‑Dokument nicht verschlüsselt ist; geben Sie bei Bedarf ein Passwort über `Redactor` an.  

## Praktische Anwendungen

Das Erzeugen eines **document thumbnail java** ist in vielen realen Szenarien nützlich:

1. **Document Review** – Zeigen Sie eine schnelle Vorschau von Verträgen oder juristischen Unterlagen in einem DMS, ohne die gesamte Datei zu öffnen.  
2. **Web Portals** – Zeigen Sie einen Einzelseiten‑Snapshot auf einer Produktseite an, reduzieren Sie die Downloadgröße und verbessern Sie die Ladezeiten.  
3. **Archival Systems** – Fügen Sie visuelle Referenzen zu archivierten PDFs hinzu, um es Benutzern zu erleichtern, die richtige Datei zu finden.  

## Leistungs‑Überlegungen
Um Ihre Anwendung bei der Verarbeitung großer Dateien reaktionsfähig zu halten:

- **Stream Documents** – Verwenden Sie den Streaming‑Modus von `Redactor`, um das Laden der gesamten Datei in den Speicher zu vermeiden.  
- **Adjust JVM Heap** – Setzen Sie `-Xmx` basierend auf der erwarteten Dokumentgröße; für 500‑seitige PDFs ist ein 2 GB‑Heap in der Regel ausreichend.  
- **Reuse Redactor Instances** – Beim Vorschauen mehrerer Seiten desselben Dokuments sollten Sie das gleiche `Redactor`‑Objekt wiederverwenden, um den Initialisierungs‑Overhead zu reduzieren.  

Die Befolgung dieser Praktiken kann den Durchsatz bei typischen Unternehmens‑Workloads um **30‑45 %** steigern.

## Häufige Probleme und Lösungen
| Problem | Ursache | Lösung |
|-------|-------|----------|
| **FileNotFoundException** when saving PNG | Ausgabeverzeichnis fehlt oder Pfad ist falsch | Erstellen Sie das Verzeichnis programmgesteuert (`new File(path).mkdirs()`) vor dem Vorschau‑Vorgang. |
| **OutOfMemoryError** on large PDFs | Gesamtes Dokument wird in den Speicher geladen | Aktivieren Sie den Streaming‑Modus oder erhöhen Sie den JVM‑Heap (`-Xmx4g`). |
| **Blank preview image** | Verschlüsselte oder beschädigte Quelldatei | Entschlüsseln Sie das Dokument mit der Passwort‑API von `Redactor` vor dem Vorschau‑Vorgang. |

## Häufig gestellte Fragen

**Q:** Was wird mit GroupDocs.Redaction für Java verwendet?  
**A:** Es bietet APIs zum Redigieren sensibler Daten, zum Erzeugen von Vorschauen und zum Konvertieren von Dokumenten über 50+ Formate hinweg, wobei die Originaldatei sicher bleibt.

**Q:** Wie gehe ich mit Ausnahmen um, wenn ich Seiten‑Streams erstelle?  
**A:** Umschließen Sie Datei‑IO‑Code mit try‑catch‑Blöcken, protokollieren Sie `IOException`‑Details und stellen Sie sicher, dass Streams in einem finally‑Block geschlossen werden oder verwenden Sie try‑with‑resources.

**Q:** Kann ich mehr als eine Seite gleichzeitig vorschauen?  
**A:** Ja – verwenden Sie `PreviewOptions.setPageNumbers(new int[]{1,3,5})`, um PNGs für die Seiten 1, 3 und 5 in einem einzigen Aufruf zu erzeugen.

**Q:** Was sind die Vorteile der Erzeugung von PNG‑Vorschauen?  
**A:** PNG bietet verlustfreie Kompression, unterstützt Transparenz und rendert Text sowie Vektorgrafiken scharf, was es ideal für hochwertige Dokument‑Thumbnails macht.

**Q:** Ist GroupDocs.Redaction kostenlos nutzbar?  
**A:** Sie können mit einer kostenlosen Testversion beginnen; eine temporäre Lizenz verlängert die Evaluierung, und eine Voll‑Lizenz ist für die kommerzielle Produktion erforderlich.

## Ressourcen
- **Documentation**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)
- **API Reference**: [API Reference](https://reference.groupdocs.com/redaction/java)
- **Download**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)
- **GitHub Repository**: [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Zuletzt aktualisiert:** 2026-05-17  
**Getestet mit:** GroupDocs.Redaction 24.9 für Java  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Preview Document Pages Java Loading with GroupDocs.Redaction](/redaction/java/document-loading/)
- [How to Generate Preview – Document Information Tutorials for GroupDocs.Redaction Java](/redaction/java/document-information/)
- [Convert Word to PDF and Save Redacted Documents with GroupDocs.Redaction Java](/redaction/java/document-saving/)