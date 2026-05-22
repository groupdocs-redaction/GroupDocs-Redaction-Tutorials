---
date: '2026-05-22'
description: Erfahren Sie, wie Sie das suffix filename java mit der GroupDocs Maven-Abhängigkeit
  hinzufügen, während Sie Dokumente redigieren. Enthält streaming load, annotation
  deletion und save options.
keywords:
- add suffix filename java
- groupdocs redaction java
- document redaction workflow
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  headline: Add suffix filename java with GroupDocs Maven
  type: TechArticle
- description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  name: Add suffix filename java with GroupDocs Maven
  steps:
  - name: '1: Create InputStream'
    text: '- **Why:** Using `InputStream` allows you to handle documents stored in
      various locations—cloud buckets, databases, or in‑memory buffers—without first
      writing them to disk. This approach is essential when you need to **load document
      from stream** in micro‑service architectures.'
  - name: '1: Apply DeleteAnnotationRedaction'
    text: '- **Why:** This step ensures that any sensitive annotations (comments,
      highlights, or hidden notes) are stripped from the document, enhancing privacy
      and compliance.'
  - name: '1: Configure SaveOptions'
    text: '- **Why:** Customizing save options allows flexible output formats and
      naming conventions. Enabling `setAddSuffix(true)` **adds suffix to filename**,
      making it clear that the file has been redacted.'
  type: HowTo
- questions:
  - answer: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.
    question: Can I redact PDF documents using GroupDocs.Redaction?
  - answer: Use streaming (`load document from stream`) and close resources promptly
      to keep memory usage low.
    question: What is the best way to handle large files with GroupDocs.Redaction?
  - answer: The API automatically adds a default suffix (e.g., “_redacted”). For custom
      suffixes, rename the output file after saving.
    question: Is it possible to customize the suffix text?
  - answer: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/)
      and follow the instructions.
    question: How do I obtain a temporary license for GroupDocs.Redaction?
  - answer: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for expert assistance.
    question: Where can I get help if I encounter issues?
  type: FAQPage
title: Suffix filename java mit GroupDocs Maven hinzufügen
type: docs
url: /de/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Suffix zum Dateinamen hinzufügen java mit GroupDocs Maven

Das Redigieren vertraulicher Daten ist nur die halbe Schlacht – Sie müssen außerdem sicherstellen, dass die gespeicherte Datei eindeutig anzeigt, dass sie verarbeitet wurde. **Die Verwendung der GroupDocs Maven-Abhängigkeit macht dies unkompliziert**, sodass Sie mit nur wenigen Codezeilen ein Suffix zum Ausgabedateinamen hinzufügen können. Die Methode zum **add suffix filename java** ist eine einzeilige Konfiguration, die Ihre redigierten Dateien sofort kennzeichnet und Ihnen hilft, konform und audit‑bereit zu bleiben.

## Schnelle Antworten
- **Was bewirkt “add suffix to filename”?**  
  Es fügt dem Ausgabedateinamen ein benutzerdefiniertes Suffix (z. B. “_redacted”) hinzu, sodass Sie verarbeitete Dateien sofort erkennen können.  
- **Kann ich ein Dokument aus einem Stream laden?**  
  Ja – GroupDocs.Redaction unterstützt das Laden aus jedem `InputStream`, ideal für Cloud‑Speicher oder In‑Memory‑Verarbeitung.  
- **Benötige ich eine Lizenz für diese Funktion?**  
  Eine kostenlose Testversion reicht für grundlegende Redaktion; eine temporäre oder vollständige Lizenz schaltet alle erweiterten Optionen frei, einschließlich der Suffix‑Verarbeitung.  
- **Welche Formate werden unterstützt?**  
  Die Bibliothek verarbeitet DOCX, PDF, PPTX, XLSX und viele weitere.  
- **Ist Rasterisierung für PDF-Ausgabe erforderlich?**  
  Rasterisierung ist optional; aktivieren Sie sie, wenn Sie das Dokument zur zusätzlichen Sicherheit flachlegen müssen.

## Was ist add suffix filename java?
Die **add suffix filename java**‑Technik fügt dem Dateinamen während des Speichervorgangs einen vordefinierten String hinzu und kennzeichnet das Dokument eindeutig als redigiert. Diese einfache Konvention verhindert die versehentliche Verteilung von Original‑ bzw. nicht redigierten Dateien und lässt sich nahtlos in automatisierte Pipelines integrieren.

## Warum GroupDocs.Redaction für diese Aufgabe verwenden?
GroupDocs.Redaction bietet eine flüssige Java‑API, mit der Sie Redaktionsaktionen mit Datei‑Verarbeitungsoptionen – wie **add suffix filename java** – in nur wenigen Codezeilen kombinieren können. Das SDK unterstützt **mehr als 50 Eingabe‑ und Ausgabeformate** und kann mehrseitige Dokumente verarbeiten, ohne die gesamte Datei in den Speicher zu laden, was sowohl Geschwindigkeit als auch geringen Speicherverbrauch liefert.

## Voraussetzungen

- **Java Development Kit (JDK):** Version 8 oder höher.  
- **GroupDocs.Redaction Library:** Kernbibliothek für Redaktionsaufgaben.  
- **IDE:** IntelliJ IDEA, Eclipse oder ein beliebiger Java‑kompatibler Editor.  
- **Maven:** Für das Abhängigkeitsmanagement.  

### Kenntnisvoraussetzungen
Vertrautheit mit Java I/O und grundlegenden objektorientierten Konzepten erleichtert das Verständnis der Beispiele.

## Einrichtung von GroupDocs.Redaction für Java
### Maven‑Einrichtung
Fügen Sie die folgende Konfiguration in Ihre `pom.xml`‑Datei ein, um über Maven auf die GroupDocs‑Bibliotheken zuzugreifen:

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
1. **Free Trial:** Zugriff auf grundlegende Funktionen ohne Einschränkungen.  
2. **Temporary License:** Eine temporäre Lizenz erhalten, um erweiterte Funktionen zu erkunden.  
3. **Purchase:** Für den langfristigen Einsatz sollten Sie den Kauf einer Voll‑Lizenz in Betracht ziehen.

#### Grundlegende Initialisierung und Einrichtung
Initialisieren Sie Ihr Projekt, indem Sie die erforderlichen Importe hinzufügen:

```java
import com.groupdocs.redaction.Redactor;
```

Mit dieser Einrichtung sind Sie bereit, Dokumenten‑Redaktionsfunktionen zu implementieren.

## Implementierungs‑Leitfaden

### Feature 1: Dokument aus Stream laden
**Übersicht:** Erfahren Sie, wie Sie Dokumente in einen `InputStream` laden, um sie zu verarbeiten.

#### Schritt‑für‑Schritt‑Implementierung
##### Schritt 1.1: InputStream erstellen

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Warum:** Die Verwendung von `InputStream` ermöglicht das Verarbeiten von Dokumenten, die an verschiedenen Orten gespeichert sind – Cloud‑Buckets, Datenbanken oder In‑Memory‑Puffer – ohne sie zunächst auf die Festplatte zu schreiben. Dieser Ansatz ist entscheidend, wenn Sie **load document from stream** in Mikro‑Service‑Architekturen benötigen.

### Feature 2: Annotationslöschung‑Redaktion anwenden
**Übersicht:** Entfernen Sie Anmerkungen aus Ihrem Dokument mit `DeleteAnnotationRedaction`.

#### Schritt‑für‑Schritt‑Implementierung
##### Schritt 2.1: DeleteAnnotationRedaction anwenden

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Warum:** Dieser Schritt stellt sicher, dass alle sensiblen Anmerkungen (Kommentare, Hervorhebungen oder versteckte Notizen) aus dem Dokument entfernt werden, wodurch Datenschutz und Konformität verbessert werden.

### Feature 3: Dokument mit Optionen speichern
**Übersicht:** Erfahren Sie, wie Sie Ihr verarbeitetes Dokument mit spezifischen Optionen wie Rasterisierung und **add suffix filename java** speichern.

#### Schritt‑für‑Schritt‑Implementierung
##### Schritt 3.1: SaveOptions konfigurieren

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Warum:** Das Anpassen der Speicheroptionen ermöglicht flexible Ausgabeformate und Namenskonventionen. Das Aktivieren von `setAddSuffix(true)` **fügt ein Suffix zum Dateinamen hinzu**, sodass klar ist, dass die Datei redigiert wurde.

## Wie kann man beim Speichern eines Dokuments das Suffix filename java hinzufügen?
`Redactor` ist die Hauptklasse in GroupDocs.Redaction, die ein Dokument lädt und Redaktionsvorgänge anwendet.  
`setAddSuffix` ist eine Methode von `SaveOptions`, die das automatische Hinzufügen eines Suffixes zum Ausgabedateinamen aktiviert.  

Laden Sie Ihre `Redactor`‑Instanz, wenden Sie die gewünschten Redaktionen an und rufen Sie anschließend `save()` mit `SaveOptions` auf, bei dem `setAddSuffix(true)` aktiviert ist. Diese einzelne Konfiguration hängt automatisch “_redacted” (oder das Standardsuffix) an den Dateinamen an, eliminiert manuelles Umbenennen und reduziert menschliche Fehler. Der Vorgang wird in O(n)-Zeit relativ zur Dokumentgröße abgeschlossen und funktioniert für alle unterstützten Formate.

## Übersicht über die groupdocs Maven‑Abhängigkeit
Die **groupdocs maven dependency** bringt das gesamte Redaction‑SDK mit einem einzigen `<dependency>`‑Eintrag in Ihr Projekt. Sie verwaltet transitive Abhängigkeiten, hält Bibliotheken aktuell und vereinfacht die Build‑Automatisierung. Durch die Deklaration der Abhängigkeit in `pom.xml` vermeiden Sie die manuelle JAR‑Verwaltung und stellen die Kompatibilität mit den neuesten Sicherheitspatches sicher.

## Warum das Hinzufügen eines Suffixes wichtig ist
Das Hinzufügen eines Suffixes liefert eine sofortige visuelle Bestätigung, dass ein Dokument verarbeitet wurde, was für Prüfpfade, automatisierte Workflows und regulatorische Konformität in allen Branchen entscheidend ist.

- **Auditierbarkeit:** Teams können sofort erkennen, welche Dateien sicher verteilt werden können.  
- **Automatisierung:** Skripte können Dateien nach Suffix filtern und verhindern so die versehentliche Verarbeitung von Originaldokumenten.  
- **Compliance:** Viele Vorschriften verlangen eine klare Kennzeichnung von gesäuberten Dokumenten.  

## Praktische Anwendungsfälle
Entdecken Sie diese Anwendungsbeispiele aus der Praxis:

1. **Rechtliche Dokumenten‑Redaktion:** Verträge sichern, bevor sie mit Kunden geteilt werden.  
2. **Umgang mit medizinischen Aufzeichnungen:** Patientendaten schützen und gleichzeitig klinische Daten erhalten.  
3. **Finanzberichterstattung:** Sensitive Zahlen während externer Prüfungen vertraulich halten.  
4. **CRM‑Integration:** Kundendaten automatisch redigieren, bevor sie in Drittanbieter‑Tools exportiert werden.  
5. **Zusammenarbeitstools:** Sicherstellen, dass geteilte Entwürfe keine versteckten Kommentare oder Metadaten preisgeben.  

## Leistungs‑Überlegungen
### Leistungsoptimierung
- Verwenden Sie Streaming (`load document from stream`), um das Laden ganzer Dateien in den Speicher zu vermeiden.  
- `Redactor`‑Instanzen sofort schließen, um Ressourcen freizugeben.  

### Richtlinien zur Ressourcennutzung
- CPU und Speicher während Batch‑Durchläufen überwachen.  
- `ByteArrayOutputStream` für In‑Memory‑Speicherungen bevorzugen, wenn mit überschaubaren Dateigrößen gearbeitet wird.  

### Best Practices für das Java‑Speichermanagement
- `Redactor`‑Objekte wiederverwenden, wenn mehrere Dateien desselben Typs verarbeitet werden.  
- `close()` in einem `try‑with‑resources`‑Block aufrufen, um Lecks zu verhindern.  

## Häufige Probleme und Lösungen
| Problem | Ursache | Lösung |
|-------|-------|-----|
| **Suffix erscheint nicht** | `setAddSuffix(false)` oder fehlender Aufruf | Stellen Sie sicher, dass `options.setAddSuffix(true)` vor `save()` gesetzt ist. |
| **OutOfMemoryError bei großem DOCX** | Laden der gesamten Datei in den Speicher | Wechseln Sie zum Laden über `InputStream` (siehe Feature 1). |
| **Anmerkungen weiterhin sichtbar** | Redaktion nicht vor dem Speichern angewendet | Rufen Sie `redactor.apply(new DeleteAnnotationRedaction())` vor `save()` auf. |
| **PDF‑Rasterisierung nicht angewendet** | `setRasterizeToPDF(false)` oder weggelassen | Setzen Sie `options.setRasterizeToPDF(true)`, wenn Sie ein flaches PDF benötigen. |

## Häufig gestellte Fragen

**F: Kann ich PDF‑Dokumente mit GroupDocs.Redaction redigieren?**  
A: Ja, die Bibliothek unterstützt PDFs, DOCX, PPTX, XLSX und viele weitere Formate.

**F: Was ist der beste Weg, große Dateien mit GroupDocs.Redaction zu verarbeiten?**  
A: Verwenden Sie Streaming (`load document from stream`) und schließen Sie Ressourcen sofort, um den Speicherverbrauch gering zu halten.

**F: Ist es möglich, den Suffix‑Text anzupassen?**  
A: Die API fügt automatisch ein Standardsuffix (z. B. “_redacted”) hinzu. Für benutzerdefinierte Suffixe benennen Sie die Ausgabedatei nach dem Speichern um.

**F: Wie erhalte ich eine temporäre Lizenz für GroupDocs.Redaction?**  
A: Besuchen Sie die [Temporary License page](https://purchase.groupdocs.com/temporary-license/) und folgen Sie den Anweisungen.

**F: Wo kann ich Hilfe erhalten, wenn ich Probleme habe?**  
A: Treten Sie dem [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) bei, um fachkundige Unterstützung zu erhalten.

## Ressourcen
- **Dokumentation:** Detaillierte Anleitungen finden Sie unter [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API‑Referenz:** Umfassende API‑Details finden Sie unter [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Die neueste Version erhalten Sie von [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub‑Repository:** Mitwirken oder den Quellcode erkunden Sie unter [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).  

---

**Zuletzt aktualisiert:** 2026-05-22  
**Getestet mit:** GroupDocs.Redaction 24.9 für Java  
**Autor:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Verwandte Tutorials

- [Word in PDF konvertieren und redigierte Dokumente mit GroupDocs.Redaction Java speichern](/redaction/java/document-saving/)
- [Vorschau von Dokumentseiten Java Laden mit GroupDocs.Redaction](/redaction/java/document-loading/)
- [Erweiterte Redaktionstechniken für GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)