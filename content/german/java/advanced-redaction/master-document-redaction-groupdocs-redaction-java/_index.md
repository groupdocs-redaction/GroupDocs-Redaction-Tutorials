---
date: '2026-02-16'
description: Erfahren Sie, wie Sie die GroupDocs Maven‑Abhängigkeit verwenden, um
  beim Redigieren von Dokumenten in Java einen Suffix zu Dateinamen hinzuzufügen.
  Enthält das Laden aus einem Stream, das Löschen von Anmerkungen und Speicheroptionen.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: groupdocs Maven-Abhängigkeit – Suffix zum Dateinamen in Java hinzufügen
type: docs
url: /de/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

.# Wie man beim Redigieren von Dokumenten in Java mit GroupDocs.Redaction einen Suffix zum Dateinamen hinzufügt

Das Redigieren vertraulicher Daten ist nur die halbe Miete – Sie müssen außerdem sicherstellen, dass die gespeicherte Datei eindeutig anzeigt, dass sie verarbeitet wurde. **Die Verwendung der groupdocs Maven‑Abhängigkeit macht das unkompliziert**, sodass Sie in nur wenigen Codezeilen einen Suffix zum Ausgabedateinamen hinzufügen können. In diesem Leitfaden lernen Sie, wie Sie beim Speichern eines redigierten Dokuments einen Suffix zum Dateinamen hinzufügen, sowie das Laden, Annotieren und Speichern mit GroupDocs.Redaction für Java. Egal, ob Sie juristische Verträge, medizinische Unterlagen oder Finanzberichte schützen, diese Schritte halten Ihren Workflow sowohl sicher als auch nachvollziehbar.

## Schnelle Antworten
- **Was bewirkt „add suffix to filename“?**  
  Es hängt einen benutzerdefinierten Suffix (z. B. „_redacted“) an den Ausgabedateinamen an, sodass Sie verarbeitete Dateien sofort erkennen können.  
- **Kann ich ein Dokument aus einem Stream laden?**  
  Ja – GroupDocs.Redaction unterstützt das Laden aus jedem `InputStream`, ideal für Cloud‑Speicher oder In‑Memory‑Verarbeitung.  
- **Benötige ich eine Lizenz für diese Funktion?**  
  Eine kostenlose Testversion reicht für grundlegende Redaktionen; eine temporäre oder vollständige Lizenz schaltet alle erweiterten Optionen frei, einschließlich der Suffix‑Verarbeitung.  
- **Welche Formate werden unterstützt?**  
  Die Bibliothek verarbeitet DOCX, PDF, PPTX, XLSX und viele weitere.  
- **Ist Rasterisierung für die PDF‑Ausgabe erforderlich?**  
  Rasterisierung ist optional; aktivieren Sie sie, wenn Sie das Dokument zur zusätzlichen Sicherheit flachlegen müssen.

## Was bedeutet das Hinzufügen eines Suffixes zu einem Dateinamen?
Ein Suffix anzuhängen ist eine einfache Namenskonvention, die signalisiert, dass eine Datei einer Redaktion unterzogen wurde. Sie verhindert das versehentliche Teilen von Original‑ bzw. unredigierten Versionen und hilft automatisierten Pipelines, den Verarbeitungsstatus zu verfolgen.

## Warum GroupDocs.Redaction für diese Aufgabe verwenden?
GroupDocs.Redaction bietet eine flüssige Java‑API, mit der Sie Redaktionsaktionen mit Datei‑Handling‑Optionen – wie **dem Hinzufügen eines Suffixes zum Dateinamen** – in nur wenigen Zeilen Code kombinieren können. Das spart Entwicklungszeit und reduziert das Risiko manueller Fehler.

## Voraussetzungen

- **Java Development Kit (JDK):** Version 8 oder höher.  
- **GroupDocs.Redaction Library:** Kernbibliothek für Redaktionsaufgaben.  
- **IDE:** IntelliJ IDEA, Eclipse oder ein beliebiger Java‑kompatibler Editor.  
- **Maven:** Für das Abhängigkeitsmanagement.  

### Wissensvoraussetzungen
Vertrautheit mit Java I/O und grundlegenden objektorientierten Konzepten erleichtert das Verständnis der Beispiele.

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

### Direktdownload
Alternativ können Sie die neueste Version direkt von [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) herunterladen.

### Lizenzbeschaffung
1. **Kostenlose Testversion:** Zugriff auf Grundfunktionen ohne Einschränkungen.  
2. **Temporäre Lizenz:** Temporäre Lizenz erhalten, um erweiterte Features zu erkunden.  
3. **Kauf:** Für den langfristigen Einsatz empfiehlt sich der Erwerb einer Voll‑Lizenz.

#### Grundlegende Initialisierung und Setup
Initialisieren Sie Ihr Projekt, indem Sie die notwendigen Importe hinzufügen:

```java
import com.groupdocs.redaction.Redactor;
```

Mit diesem Setup sind Sie bereit, Dokument‑Redaktions‑Funktionalitäten zu implementieren.

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

- **Warum:** Die Verwendung von `InputStream` ermöglicht die nahtlose Handhabung von Dokumenten, die in verschiedenen Formaten gespeichert sind – entscheidend, wenn Sie **document from stream** in Cloud‑ oder Micro‑Service‑Szenarien laden müssen.

### Feature 2: Annotation‑Lösch‑Redaktion anwenden
**Übersicht:** Entfernen Sie Anmerkungen aus Ihrem Dokument mithilfe von `DeleteAnnotationRedaction`.

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
**Übersicht:** Lernen Sie, wie Sie Ihr verarbeitetes Dokument mit spezifischen Optionen wie Rasterisierung und **dem Hinzufügen eines Suffixes zum Dateinamen** speichern.

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

- **Warum:** Das Anpassen von SaveOptions ermöglicht flexible Ausgabeformate und Namenskonventionen. Das Aktivieren von `setAddSuffix(true)` **fügt einen Suffix zum Dateinamen hinzu**, sodass klar erkennbar ist, dass die Datei redigiert wurde.

## groupdocs maven dependency Überblick
Die **groupdocs maven dependency** bringt das gesamte Redaction‑SDK mit einem einzigen `<dependency>`‑Eintrag in Ihr Projekt. Sie kümmert sich um transitive Abhängigkeiten, hält Bibliotheken aktuell und vereinfacht die Build‑Automatisierung. Durch die Deklaration der Abhängigkeit in `pom.xml` vermeiden Sie manuelles JAR‑Management und stellen die Kompatibilität mit den neuesten Sicherheitspatches sicher.

## Warum das Hinzufügen eines Suffixes wichtig ist
- **Auditierbarkeit:** Teams können sofort erkennen, welche Dateien sicher verteilt werden können.  
- **Automatisierung:** Skripte können Dateien nach Suffix filtern und verhindern so das versehentliche Verarbeiten von Originaldokumenten.  
- **Compliance:** Viele Vorschriften verlangen eine klare Kennzeichnung von gesäuberten Dokumenten.  

## Praktische Anwendungsfälle
Entdecken Sie diese realen Einsatzszenarien:
1. **Rechtliche Dokumenten‑Redaktion:** Verträge sichern, bevor sie an Kunden weitergegeben werden.  
2. **Umgang mit medizinischen Unterlagen:** Patienten‑Identifikatoren schützen.  
3. **Finanzberichte:** Sensible Zahlen vertraulich halten.  
4. **CRM‑Integration:** Kundendaten automatisch vor dem Export redigieren.  
5. **Kollaborationstools:** Sicherstellen, dass geteilte Entwürfe keine versteckten Kommentare preisgeben.

## Leistungs‑Überlegungen
### Performance‑Optimierung
- Verwenden Sie Streaming (`load document from stream`), um das Laden ganzer Dateien in den Speicher zu vermeiden.  
- Schließen Sie `Redactor`‑Instanzen zügig, um Ressourcen freizugeben.

### Ressourcen‑Nutzungs‑Richtlinien
- Überwachen Sie CPU und Speicher während Batch‑Durchläufen.  
- Bevorzugen Sie `ByteArrayOutputStream` für In‑Memory‑Saves bei moderaten Dateigrößen.

### Best Practices für Java‑Speicherverwaltung
- Wiederverwenden Sie `Redactor`‑Objekte, wenn Sie mehrere Dateien desselben Typs verarbeiten.  
- Rufen Sie `close()` in einem `try‑with‑resources`‑Block auf, um Lecks zu verhindern.

## Häufige Probleme und Lösungen
| Problem | Ursache | Lösung |
|-------|-------|-----|
| **Suffix erscheint nicht** | `setAddSuffix(false)` oder fehlender Aufruf | Stellen Sie sicher, dass `options.setAddSuffix(true)` vor `save()` gesetzt ist. |
| **OutOfMemoryError bei großen DOCX** | Laden der gesamten Datei in den Speicher | Wechseln Sie zum Laden über `InputStream` (siehe Feature 1). |
| **Annotationen weiterhin sichtbar** | Redaktion nicht vor dem Speichern angewendet | Rufen Sie `redactor.apply(new DeleteAnnotationRedaction())` vor `save()` auf. |
| **PDF‑Rasterisierung nicht angewendet** | `setRasterizeToPDF(false)` oder weggelassen | Setzen Sie `options.setRasterizeToPDF(true)`, wenn ein flaches PDF benötigt wird. |

## Häufig gestellte Fragen

**F: Kann ich PDF‑Dokumente mit GroupDocs.Redaction redigieren?**  
A: Ja, die Bibliothek unterstützt PDFs, DOCX, PPTX, XLSX und viele weitere Formate.

**F: Was ist der beste Weg, große Dateien mit GroupDocs.Redaction zu handhaben?**  
A: Nutzen Sie Streaming (`load document from stream`) und schließen Sie Ressourcen zügig, um den Speicherverbrauch gering zu halten.

**F: Ist es möglich, den Suffix‑Text anzupassen?**  
A: Die API fügt standardmäßig einen Suffix (z. B. „_redacted“) hinzu. Für benutzerdefinierte Suffixe können Sie die Ausgabedatei nach dem Speichern umbenennen.

**F: Wie erhalte ich eine temporäre Lizenz für GroupDocs.Redaction?**  
A: Besuchen Sie die [Temporary License page](https://purchase.groupdocs.com/temporary-license/) und folgen Sie den Anweisungen.

**F: Wo bekomme ich Hilfe, wenn ich auf Probleme stoße?**  
A: Treten Sie dem [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) bei, um fachkundige Unterstützung zu erhalten.

## Ressourcen
- **Dokumentation:** Detaillierte Anleitungen finden Sie unter [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API‑Referenz:** Umfassende API‑Details erhalten Sie unter [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Laden Sie die neueste Version von [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/) herunter.  
- **GitHub‑Repository:** Beitrag leisten oder Quellcode erkunden Sie unter [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Zuletzt aktualisiert:** 2026-02-16  
**Getestet mit:** GroupDocs.Redaction 24.9 für Java  
**Autor:** GroupDocs