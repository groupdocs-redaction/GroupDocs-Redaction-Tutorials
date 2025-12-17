---
date: '2025-12-17'
description: Erfahren Sie, wie Sie einem Dateinamen ein Suffix hinzufügen und sensible
  Informationen aus Dokumenten mit GroupDocs.Redaction für Java redigieren. Verbessern
  Sie die Dokumentensicherheit und den Datenschutz effektiv.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Wie man beim Schwärzen von Dokumenten in Java mit GroupDocs.Redaction einen
  Suffix zum Dateinamen hinzufügt
type: docs
url: /de/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Wie man beim Redigieren von Dokumenten in Java mit GroupDocs.Redaction einen Suffix zum Dateinamen hinzufügt

Das Redigieren vertraulicher Daten ist nur die halbe Aufgabe – Sie müssen außerdem sicherstellen, dass die gespeicherte Datei eindeutig anzeigt, dass sie verarbeitet wurde. In diesem Leitfaden lernen Sie **wie man einen Suffix zum Dateinamen hinzufügt** beim Speichern eines redigierten Dokuments, zusammen mit dem Laden, Annotieren und Speichern mit GroupDocs.Redaction für Java. Egal, ob Sie juristische Verträge, medizinische Aufzeichnungen oder Finanzberichte schützen, diese Schritte halten Ihren Arbeitsablauf sowohl sicher als auch nachvollziehbar.

## Schnelle Antworten
- **Was bewirkt “add suffix to filename”?**  
  Es fügt dem Ausgabedateinamen einen benutzerdefinierten Suffix (z. B. “_redacted”) hinzu, sodass Sie verarbeitete Dateien sofort erkennen können.  
- **Kann ich ein Dokument aus einem Stream laden?**  
  Ja – GroupDocs.Redaction unterstützt das Laden aus jedem `InputStream`, ideal für Cloud‑Speicher oder In‑Memory‑Verarbeitung.  
- **Benötige ich eine Lizenz für diese Funktion?**  
  Eine kostenlose Testversion funktioniert für grundlegende Redaktionen; eine temporäre oder vollständige Lizenz schaltet alle erweiterten Optionen frei, einschließlich der Suffix‑Verarbeitung.  
- **Welche Formate werden unterstützt?**  Die Bibliothek verarbeitet DOCX, PDF, PPTX, XLSX und viele weitere.  
- **Ist Rasterisierung für PDF‑Ausgabe erforderlich?**  
  Rasterisierung ist optional; aktivieren Sie sie, wenn Sie das Dokument zur zusätzlichen Sicherheit flachlegen müssen.

## Was bedeutet das Hinzufügen eines Suffix zum Dateinamen?
Das Anhängen eines Suffix ist eine einfache Namenskonvention, die signalisiert, dass eine Datei einer Redaktion unterzogen wurde. Es verhindert das versehentliche Teilen von Original‑, nicht redigierten Versionen und hilft automatisierten Pipelines, den Verarbeitungsstatus zu verfolgen.

## Warum GroupDocs.Redaction für diese Aufgabe verwenden?
GroupDocs.Redaction bietet eine flüssige Java‑API, die es Ihnen ermöglicht, Redaktionsaktionen mit Datei‑Handling‑Optionen zu kombinieren – wie **das Hinzufügen eines Suffix zum Dateinamen** – in nur wenigen Codezeilen. Das spart Entwicklungszeit und reduziert das Risiko manueller Fehler.

## Voraussetzungen
- **Java Development Kit (JDK):** Version 8 oder höher.  
- **GroupDocs.Redaction Library:** Kernbibliothek für Redaktionsaufgaben.  
- **IDE:** IntelliJ IDEA, Eclipse oder ein beliebiger Java‑kompatibler Editor.  
- **Maven:** Für die Abhängigkeitsverwaltung.  

### Wissensvoraussetzungen
Vertrautheit mit Java I/O und grundlegenden objektorientierten Konzepten erleichtert das Verständnis der Beispiele.

## Einrichtung von GroupDocs.Redaction für Java
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
1. **Free Trial:** Zugriff auf Grundfunktionen ohne Einschränkungen.  
2. **Temporary License:** Erhalten Sie eine temporäre Lizenz, um erweiterte Funktionen zu erkunden.  
3. **Purchase:** Für den langfristigen Einsatz sollten Sie den Kauf einer Voll‑Lizenz in Betracht ziehen.  

#### Grundlegende Initialisierung und Setup
Initialisieren Sie Ihr Projekt, indem Sie die notwendigen Importe hinzufügen:

```java
import com.groupdocs.redaction.Redactor;
```

Mit dieser Einrichtung sind Sie bereit, Redaktionsfunktionen für Dokumente zu implementieren.

## Implementierungs‑Leitfaden

### Feature 1: Dokument aus Stream laden
**Übersicht:** Erfahren Sie, wie Sie Dokumente in einen `InputStream` zum Verarbeiten laden.

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

- **Warum:** Die Verwendung von `InputStream` ermöglicht es Ihnen, Dokumente, die in verschiedenen Formaten gespeichert sind, nahtlos zu verarbeiten, was entscheidend ist, wenn Sie **load document from stream** in Cloud‑ oder Micro‑Service‑Szenarien benötigen.

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

- **Warum:** Dieser Schritt stellt sicher, dass alle sensiblen Anmerkungen entfernt werden, wodurch die Dokumenten‑Privatsphäre erhöht wird.

### Feature 3: Dokument mit Optionen speichern
**Übersicht:** Erfahren Sie, wie Sie Ihr verarbeitetes Dokument mit speziellen Optionen wie Rasterisierung und **Hinzufügen eines Suffix zum Dateinamen** speichern.

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

- **Warum:** Das Anpassen der Speicheroptionen ermöglicht flexible Ausgabeformate und Namenskonventionen. Das Aktivieren von `setAddSuffix(true)` **fügt einen Suffix zum Dateinamen hinzu**, sodass klar ist, dass die Datei redigiert wurde.

## Warum das Hinzufügen eines Suffix wichtig ist
- **Auditierbarkeit:** Teams können sofort erkennen, welche Dateien sicher verteilt werden können.  
- **Automatisierung:** Skripte können Dateien nach Suffix filtern und verhindern so die versehentliche von Originaldokumenten.  
- **Compliance:** Viele Vorschriften verlangen eine klare Kennzeichnung von gesäuberten Dokumenten.

## Praktische Anwendungen
Entdecken Sie diese realen Anwendungsfälle:
1. **Legal Document Redaction:** Verträge sichern, bevor sie an Kunden weitergegeben werden.  
2. **Medical Record Handling:** Patientendaten schützen.  
3. **Financial Reporting:** Sensible Zahlen vertraulich halten.  
4. **CRM Integration:** Kundendaten automatisch vor dem Export redigieren.  
5. **Collaboration Tools:** Sicherstellen, dass geteilte Entwürfe keine versteckten Kommentare preisgeben.

## Leistungsüberlegungen
### Performance optimieren
- Verwenden Sie Streaming (`load document from stream`), um zu vermeiden, dass ganze Dateien in den Speicher geladen werden.  
- Schließen Sie `Redactor`‑Instanzen umgehend, um Ressourcen freizugeben.  

### Richtlinien zur Ressourcennutzung
- Überwachen Sie CPU und Speicher während Batch‑Durchläufen.  
- Bevorzugen Sie `ByteArrayOutputStream` für In‑Memory‑Speicherungen bei moderaten Dateigrößen.  

### Best Practices für Java‑Speicherverwaltung
- `Redactor`‑Objekte wiederverwenden, wenn mehrere Dateien desselben Typs verarbeitet werden.  
- `close()` in einem `finally`‑Block oder try‑with‑resources aufrufen, um Lecks zu verhindern.  

## Häufige Probleme und Lösungen
| Problem | Ursache | Lösung |
|-------|-------|-----|
| **Suffix not appearing** | `setAddSuffix(false)` oder fehlender Aufruf | Stellen Sie sicher, dass `options.setAddSuffix(true)` vor `save()` gesetzt ist. |
| **OutOfMemoryError on large DOCX** | Laden der gesamten Datei in den Speicher | Wechseln Sie zum Laden über `InputStream` (siehe Feature 1). |
| **Annotations still visible** | Redaktion nicht vor dem Speichern angewendet | Rufen Sie `redactor.apply(new DeleteAnnotationRedaction())` vor `save()` auf. |
| **PDF rasterization not applied** | `setRasterizeToPDF(false)` oder weggelassen | Setzen Sie `options.setRasterizeToPDF(true)`, wenn Sie ein flaches PDF benötigen. |

## Häufig gestellte Fragen

**Q: Kann ich PDF‑Dokumente mit GroupDocs.Redaction redigieren?**  
A: Ja, die Bibliothek unterstützt PDFs, DOCX, PPTX, XLSX und viele weitere Formate.

**Q: Was ist der beste Weg, große Dateien mit GroupDocs.Redaction zu verarbeiten?**  
A: Verwenden Sie Streaming (`load document from stream`) und schließen Sie Ressourcen umgehend, um den Speicherverbrauch gering zu halten.

**Q: Ist es möglich, den Suffix‑Text anzupassen?**  
A: Die API fügt automatisch einen Standardsuffix (z. B. “_redacted”) hinzu. Für benutzerdefinierte Suffixe können Sie die Ausgabedatei nach dem Speichern umbenennen.

**Q: Wie erhalte ich eine temporäre Lizenz für GroupDocs.Redaction?**  
A: Besuchen Sie die [Temporary License page](https://purchase.groupdocs.com/temporary-license/) und folgen Sie den Anweisungen.

**Q: Wo kann ich Hilfe erhalten, wenn ich auf Probleme stoße?**  
A: Treten Sie dem [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) bei, um fachkundige Unterstützung zu erhalten.

## Ressourcen
- **Documentation:** Detaillierte Anleitungen finden Sie unter [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Umfassende API‑Details erhalten Sie unter [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Die neueste Version erhalten Sie von [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Tragen Sie bei oder erkunden Sie den Quellcode unter [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).  

---

**Zuletzt aktualisiert:** 2025-12-17  
**Getestet mit:** GroupDocs.Redaction 24.9 für Java  
**Autor:** GroupDocs