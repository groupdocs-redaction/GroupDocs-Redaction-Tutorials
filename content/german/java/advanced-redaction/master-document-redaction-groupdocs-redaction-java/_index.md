---
date: '2026-11-02'
description: Erfahren Sie, wie Sie in einem GroupDocs redaction Java‑Tutorial mithilfe
  von Maven, streaming load, annotation deletion und save options ein Suffix zu einem
  Dateinamen hinzufügen.
keywords:
- groupdocs redaction java tutorial
- add suffix filename java
- document redaction workflow
- groupdocs maven dependency
- java inputstream redaction
lastmod: '2026-11-02'
og_description: Erfahren Sie, wie Sie in einem GroupDocs redaction Java‑Tutorial ein
  Suffix zu einem Dateinamen hinzufügen. Folgen Sie der Schritt‑für‑Schritt‑Maven‑Einrichtung,
  streaming load und save options.
og_image_alt: Guide showing Java code to add suffix to redacted filenames using GroupDocs
  Redaction
og_title: Wie man einem Dateinamen ein Suffix in GroupDocs redaction Java hinzufügt
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  headline: How to add suffix to filename in GroupDocs redaction Java
  type: TechArticle
- description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  name: How to add suffix to filename in GroupDocs redaction Java
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
tags:
- groupdocs redaction
- java tutorial
- maven dependency
- document redaction
title: Wie man einem Dateinamen ein Suffix in GroupDocs redaction Java hinzufügt
type: docs
url: /de/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Wie man einen Suffix zum Dateinamen in GroupDocs Redaction Java hinzufügt

In diesem **groupdocs redaction java tutorial** lernen Sie, wie Sie automatisch einen Suffix an den Ausgabedateinamen anhängen, wenn Sie Dokumente mit GroupDocs.Redaction redigieren. Das Hinzufügen eines Suffix eliminiert manuelles Umbenennen, reduziert das Risiko, nicht redigierte Dateien zu leaken, und passt nahtlos in CI/CD‑Pipelines, die auf Namenskonventionen basieren. Der Leitfaden führt Sie durch Maven‑Setup, Streaming‑Dokumenten‑Laden, Annotations‑Entfernung und das Konfigurieren von Speicheroptionen – alles mit prägnantem, produktionsreifem Code.

## Schnelle Antworten
- **Was bewirkt „add suffix to filename“?**  
  Wenn Sie die Suffix‑Option aktivieren, fügt das SDK automatisch einen vordefinierten String (standardmäßig „_redacted“) zum Basisnamen der Ausgabedatei vor der Erweiterung hinzu. Das macht sofort ersichtlich, welche Dateien verarbeitet wurden, hilft, eine versehentliche Verteilung des Originalinhalts zu verhindern, und vereinfacht nachgelagerte Automatisierungen, die auf Namensmustern basieren.  
- **Kann ich ein Dokument aus einem Stream laden?**  
  Ja – GroupDocs.Redaction unterstützt das Laden aus jedem `InputStream`, ideal für Cloud‑Speicher oder In‑Memory‑Verarbeitung.  
- **Benötige ich eine Lizenz für diese Funktion?**  
  Eine kostenlose Testversion funktioniert für grundlegende Redaktionen; eine temporäre oder vollständige Lizenz schaltet alle erweiterten Optionen frei, einschließlich Suffix‑Verarbeitung.  
- **Welche Formate werden unterstützt?**  
  Die Bibliothek verarbeitet DOCX, PDF, PPTX, XLSX und viele weitere.  
- **Ist Rasterisierung für PDF‑Ausgabe erforderlich?**  
  Rasterisierung ist optional; aktivieren Sie sie, wenn Sie das Dokument zur zusätzlichen Sicherheit flachlegen müssen.

## Was bewirkt „add suffix to filename“?

Wenn Sie die Suffix‑Option aktivieren, fügt das SDK automatisch einen vordefinierten String (standardmäßig „_redacted“) zum Basisnamen der Ausgabedatei vor der Erweiterung hinzu. Das macht sofort ersichtlich, welche Dateien verarbeitet wurden, hilft, eine versehentliche Verteilung des Originalinhalts zu verhindern, und vereinfacht nachgelagerte Automatisierungen, die auf Namensmustern basieren.

## Warum GroupDocs.Redaction für diese Aufgabe verwenden?

GroupDocs.Redaction bietet eine leistungsstarke Java‑API, die Redaktionsaktionen mit flexiblen Datei‑Handling‑Optionen wie automatischer Suffix‑Hinzufügung, Streaming‑Unterstützung und Batch‑Verarbeitung kombiniert. Sie unterstützt über 50 Eingabe‑ und Ausgabeformate und kann mehrseitige Dokumente verarbeiten, ohne die gesamte Datei in den Speicher zu laden, was niedrigen Speicherverbrauch und schnelle Ausführung gewährleistet.

## Voraussetzungen

- **Java Development Kit (JDK):** Version 8 oder höher.  
- **GroupDocs.Redaction Library:** Kernbibliothek für Redaktionsaufgaben.  
- **IDE:** IntelliJ IDEA, Eclipse oder ein beliebiger Java‑kompatibler Editor.  
- **Maven:** Für das Abhängigkeitsmanagement.  

### Wissensvoraussetzungen
Vertrautheit mit Java‑I/O und grundlegenden objektorientierten Konzepten erleichtert das Verständnis der Beispiele.

## GroupDocs.Redaction für Java einrichten

### Maven‑Setup
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
1. **Free trial:** Zugriff auf Grundfunktionen ohne Einschränkungen.  
2. **Temporary license:** Temporäre Lizenz erhalten, um erweiterte Features zu erkunden.  
3. **Purchase:** Für den langfristigen Einsatz empfiehlt sich der Kauf einer Voll‑Lizenz.

#### Grundlegende Initialisierung und Setup
Initialisieren Sie Ihr Projekt, indem Sie die notwendigen Importe hinzufügen:

```java
import com.groupdocs.redaction.Redactor;
```

Mit diesem Setup sind Sie bereit, Dokumenten‑Redaktions‑Funktionalitäten zu implementieren.

## Implementierungs‑Leitfaden

### Feature 1: Dokument aus Stream laden
**Übersicht:** Lernen Sie, wie Sie Dokumente in einen `InputStream` laden, um sie zu verarbeiten.

`InputStream` ist eine Java‑I/O‑Klasse, die einen Bytestrom darstellt und das Lesen von Daten aus Dateien, Netzwerkverbindungen oder anderen Quellen ermöglicht, ohne den gesamten Inhalt in den Speicher zu laden.

#### Schritt 1.1: InputStream erstellen

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

- **Warum:** Die Verwendung von `InputStream` erlaubt das Handling von Dokumenten, die an verschiedenen Orten gespeichert sind – Cloud‑Buckets, Datenbanken oder In‑Memory‑Puffern – ohne sie zuerst auf die Festplatte zu schreiben. Dieser Ansatz ist entscheidend, wenn Sie **load document from stream** in Micro‑Service‑Architekturen benötigen.

### Feature 2: Annotations‑Lösch‑Redaktion anwenden
**Übersicht:** Entfernen Sie Anmerkungen aus Ihrem Dokument mit `DeleteAnnotationRedaction`.

`DeleteAnnotationRedaction` ist ein Redaktionsvorgang, der alle Anmerkungen – wie Kommentare, Hervorhebungen und Notizen – aus dem Dokument entfernt.

#### Schritt 2.1: DeleteAnnotationRedaction anwenden

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Warum:** Dieser Schritt stellt sicher, dass sensible Anmerkungen (Kommentare, Hervorhebungen oder versteckte Notizen) aus dem Dokument entfernt werden, wodurch Datenschutz und Compliance verbessert werden.

### Feature 3: Dokument mit Optionen speichern
**Übersicht:** Lernen Sie, wie Sie Ihr verarbeitetes Dokument mit spezifischen Optionen wie Rasterisierung und **add suffix filename java** speichern.

`SaveOptions` fasst Einstellungen zusammen, die steuern, wie das redigierte Dokument geschrieben wird, einschließlich Format, Rasterisierung und Namenskonventionen.

#### Schritt 3.1: SaveOptions konfigurieren

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

- **Warum:** Das Anpassen von SaveOptions ermöglicht flexible Ausgabeformate und Namenskonventionen. Das Aktivieren von `setAddSuffix(true)` **adds suffix to filename**, wodurch klar wird, dass die Datei redigiert wurde.

## Wie fügt man beim Speichern eines Dokuments in Java einen Suffix zum Dateinamen hinzu?

Die Klasse `Redactor` ist die Kernkomponente, die ein Dokument lädt und Redaktionsvorgänge anwendet. `SaveOptions` definiert, wie das redigierte Dokument gespeichert wird, einschließlich Format, Rasterisierung und Namenskonventionen. Erstellen Sie eine `Redactor`‑Instanz, wenden Sie erforderliche Redaktionen an und konfigurieren Sie ein `SaveOptions`‑Objekt mit `setAddSuffix(true)`. Rufen Sie `redactor.save(outputPath, options)` auf. Das SDK fügt automatisch „_redacted“ (oder den konfigurierten Suffix) zum Dateinamen hinzu, sodass Sie die Datei nie manuell umbenennen müssen.

## Überblick über GroupDocs Maven‑Abhängigkeit

Die **groupdocs maven dependency** bringt das gesamte Redaction‑SDK mit einem einzigen `<dependency>`‑Eintrag in Ihr Projekt. Sie verwaltet transitive Abhängigkeiten, hält Bibliotheken aktuell und vereinfacht die Build‑Automatisierung. Durch die Deklaration der Abhängigkeit in `pom.xml` vermeiden Sie manuelles JAR‑Management und stellen die Kompatibilität mit den neuesten Sicherheitspatches sicher.

## Warum das Hinzufügen eines Suffix wichtig ist

Das Anhängen eines Suffix liefert sofortige visuelle Bestätigung, dass eine Datei verarbeitet wurde – entscheidend für Audit‑Trails, automatisierte Workflows und regulatorische Konformität. Es ermöglicht Skripten, redigierte Dateien zu filtern, verhindert versehentliche Verteilung des Originalinhalts und erfüllt viele Branchenstandards, die eine klare Kennzeichnung sanitärer Dokumente verlangen.

## Praktische Anwendungsfälle

Erkunden Sie diese realen Szenarien:

1. **Legal document redaction:** Verträge sichern, bevor sie an Kunden weitergegeben werden.  
2. **Medical record handling:** Patientendaten schützen, während klinische Informationen erhalten bleiben.  
3. **Financial reporting:** Sensible Zahlen während externer Audits vertraulich halten.  
4. **CRM integration:** Kundendaten automatisch redigieren, bevor sie in Drittanbieter‑Tools exportiert werden.  
5. **Collaboration tools:** Sicherstellen, dass geteilte Entwürfe keine versteckten Kommentare oder Metadaten preisgeben.

## Leistungsüberlegungen

### Performance optimieren
- Verwenden Sie Streaming (`load document from stream`), um das Laden ganzer Dateien in den Speicher zu vermeiden.  
- Schließen Sie `Redactor`‑Instanzen zügig, um Ressourcen freizugeben.  

### Richtlinien zur Ressourcennutzung
- Überwachen Sie CPU und Speicher während Batch‑Durchläufen.  
- Bevorzugen Sie `ByteArrayOutputStream` für In‑Memory‑Speicherungen bei moderaten Dateigrößen.

### Best Practices für Java‑Speicherverwaltung
- Wiederverwenden Sie `Redactor`‑Objekte, wenn Sie mehrere Dateien desselben Typs verarbeiten.  
- Rufen Sie `close()` in einem `try‑with‑resources`‑Block auf, um Lecks zu verhindern.

## Häufige Probleme und Lösungen
| Problem | Ursache | Lösung |
|-------|-------|-----|
| **Suffix nicht sichtbar** | `setAddSuffix(false)` oder Aufruf fehlt | Stellen Sie sicher, dass `options.setAddSuffix(true)` vor `save()` gesetzt ist. |
| **OutOfMemoryError bei großen DOCX** | Gesamtes Laden der Datei in den Speicher | Wechseln Sie zum Laden über `InputStream` (siehe Feature 1). |
| **Annotations noch sichtbar** | Redaktion nicht vor dem Speichern angewendet | Rufen Sie `redactor.apply(new DeleteAnnotationRedaction())` vor `save()` auf. |
| **PDF‑Rasterisierung nicht angewendet** | `setRasterizeToPDF(false)` oder fehlt | Setzen Sie `options.setRasterizeToPDF(true)`, wenn ein flaches PDF benötigt wird. |

## Häufig gestellte Fragen

**Q: Kann ich PDF‑Dokumente mit GroupDocs.Redaction redigieren?**  
A: Ja, die Bibliothek unterstützt PDFs, DOCX, PPTX, XLSX und viele weitere Formate.

**Q: Was ist der beste Weg, große Dateien mit GroupDocs.Redaction zu handhaben?**  
A: Nutzen Sie Streaming (`load document from stream`) und schließen Sie Ressourcen zügig, um den Speicherverbrauch gering zu halten.

**Q: Ist es möglich, den Suffix‑Text anzupassen?**  
A: Die API fügt standardmäßig einen Suffix (z. B. „_redacted“) hinzu. Für benutzerdefinierte Suffixe benennen Sie die Ausgabedatei nach dem Speichern um.

**Q: Wie erhalte ich eine temporäre Lizenz für GroupDocs.Redaction?**  
A: Besuchen Sie die [Temporary License page](https://purchase.groupdocs.com/temporary-license/) und folgen Sie den Anweisungen.

**Q: Wo bekomme ich Hilfe, wenn ich Probleme habe?**  
A: Treten Sie dem [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) bei, um fachkundige Unterstützung zu erhalten.

## Ressourcen
- **Documentation:** Detaillierte Anleitungen finden Sie unter [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API reference:** Umfassende API‑Details gibt es auf [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Die neueste Version erhalten Sie von [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub repository:** Beitrag leisten oder Quellcode erkunden Sie unter [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Last Updated:** 2026-11-02  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

## Verwandte Tutorials

- [Convert Word to PDF and Save Redacted Documents with GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Preview Document Pages Java Loading with GroupDocs.Redaction](/redaction/java/document-loading/)
- [Advanced Redaction Techniques for GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)