---
date: '2026-10-01'
description: Erfahren Sie, wie Sie author metadata entfernen und redacted document
  files in Java mit GroupDocs Redaction speichern.
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Erfahren Sie, wie Sie author metadata entfernen und redacted document
  files in Java mit GroupDocs Redaction speichern. Folgen Sie der Schritt‑für‑Schritt-Anleitung.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: Wie man author metadata in Java mit GroupDocs entfernt
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: Wie man author metadata in Java mit GroupDocs entfernt
type: docs
url: /de/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Wie man Autor-Metadaten in Java mit GroupDocs entfernt

In der heutigen digitalen Landschaft ist der Schutz sensibler Informationen, die in Dokumenten verborgen sind, ein unverzichtbares Vorgehen. **Das Entfernen von Autor-Metadaten** verhindert die versehentliche Offenlegung persönlicher oder geschäftlicher Kennungen. Dieses Tutorial zeigt Ihnen Schritt für Schritt, wie Sie `EraseMetadataRedaction` aus GroupDocs.Redaction für Java verwenden, um Felder wie *Author* und *Manager* aus Word‑Dateien zu entfernen und dann **redigierte Dokumentkopien** sicher zum Teilen oder Archivieren zu speichern.

## Schnelle Antworten
- **Was macht EraseMetadataRedaction?** Es entfernt ausgewählte Metadatenfelder aus einem Dokument.  
- **Welche Bibliothek stellt diese Funktion bereit?** GroupDocs.Redaction für Java.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert für Tests; für die Produktion ist eine permanente Lizenz erforderlich.  
- **Kann ich mehrere Felder gleichzeitig anvisieren?** Ja, kombinieren Sie Filter mit einem logischen ODER.  
- **Ist der Vorgang thread‑sicher?** Redactor‑Instanzen werden nicht über Threads hinweg geteilt; erstellen Sie für jede Operation eine neue Instanz.

## Was ist EraseMetadataRedaction?
`EraseMetadataRedaction` ist eine integrierte Redaktionsklasse, mit der Sie festlegen können, welche Metadaten‑Einträge gelöscht werden sollen. Sie funktioniert mit einer breiten Palette von Dokumentformaten, die von GroupDocs.Redaction unterstützt werden, und stellt sicher, dass versteckte Autorinformationen niemals durchsickern. Sie können Standard‑Eigenschaften wie Author, Manager sowie benutzerdefinierte Metadatenfelder anvisieren und so umfassenden Datenschutz gewährleisten.

## Warum EraseMetadataRedaction mit GroupDocs verwenden?
GroupDocs.Redaction unterstützt **über 100 Eingabe‑ und Ausgabeformate** und kann Dokumente bis zu 500 Seiten verarbeiten, ohne die gesamte Datei in den Speicher zu laden. Die Verwendung dieser Klasse bietet Ihnen eine einheitliche, leistungsstarke API, um GDPR-, HIPAA‑ oder interne Compliance‑Anforderungen zu erfüllen und gleichzeitig Ihren Code‑Base einfach zu halten.

## Voraussetzungen
- Java 8 oder höher installiert.  
- Maven (oder die Möglichkeit, JARs manuell hinzuzufügen).  
- GroupDocs.Redaction für Java (Version 24.9 oder neuer).  
- Eine gültige GroupDocs‑Testversion oder permanente Lizenz.

## Einrichtung von GroupDocs.Redaction für Java

### Maven-Installation
Fügen Sie das GroupDocs‑Repository und die Abhängigkeit zu Ihrer **pom.xml** hinzu:

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
Alternativ können Sie das neueste JAR von [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) herunterladen.

### Lizenzbeschaffung
Erhalten Sie eine kostenlose Testversion oder erwerben Sie eine temporäre Lizenz über das GroupDocs‑Portal. Die Lizenzdatei sollte dort abgelegt werden, wo Ihre Anwendung sie laden kann (z. B. im Klassenpfad‑Root).

### Grundlegende Initialisierung und Einrichtung
Unten finden Sie ein minimales Beispiel, das eine `Redactor`‑Instanz für eine DOCX‑Datei erstellt:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Verwendung von EraseMetadataRedaction in Java
Die folgenden Abschnitte zerlegen die Implementierung in klare, umsetzbare Schritte.

### Funktion: bestimmte Metadaten-Elemente bereinigen

#### Übersicht
Wir werden die Metadatenfelder **Author** und **Manager** mit `EraseMetadataRedaction` löschen. Dies ist eine häufige Anforderung, wenn interne Berichte mit externen Partnern geteilt werden.

#### Schritt‑für‑Schritt-Implementierung

##### 1️⃣ Redactor-Objekt initialisieren
`Redactor` ist die Kernklasse, die ein Dokument lädt, Redaktionsobjekte anwendet und das Ergebnis schreibt. Erstellen Sie für jede zu verarbeitende Datei eine neue Instanz:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ EraseMetadataRedaction anwenden
`MetadataFilters` stellt vordefinierte Filter für gängige Metadaten‑Schlüssel wie Author und Manager bereit.  
`EraseMetadataRedaction` entfernt Metadaten‑Einträge, die den angegebenen `MetadataFilters` entsprechen. Das bitweise ODER (`|`) kombiniert die `Author`‑ und `Manager`‑Filter, sodass beide Felder in einem Aufruf entfernt werden:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ Speicheroptionen konfigurieren
`SaveOptions` lässt Sie den Ausgabedateinamen, das Format und weitere Speicherparameter festlegen.  
`SaveOptions` ermöglicht die Kontrolle des Ausgabedateinamens, des Formats und ob das Dokument in PDF gerastert werden soll. Das Hinzufügen eines Suffixs lässt die Originaldatei unverändert:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## Häufige Anwendungsfälle
1. **Rechtsdokumente** – Autorinformationen redigieren, bevor Verträge an die Gegenpartei gesendet werden.  
2. **Unternehmensberichte** – Managernamen entfernen, wenn Quartalsergebnisse an Aktionäre veröffentlicht werden.  
3. **Projektdateien** – Interne Projektdokumentation bereinigen, bevor sie archiviert oder in ein öffentliches Repository hochgeladen wird.

## Tipps zur Fehlerbehebung
- **Datei nicht gefunden** – Stellen Sie sicher, dass der Pfad in `inputFilePath` auf eine vorhandene Datei zeigt und die Anwendung Leseberechtigungen hat.  
- **Fehlende Metadatenfelder** – Nicht alle Dokumenttypen speichern dieselben Metadaten‑Schlüssel; prüfen Sie zuerst die Dokumenteigenschaften in Office.  
- **Lizenzfehler** – Stellen Sie sicher, dass die Lizenzdatei korrekt geladen ist, bevor die `Redactor`‑Instanz erstellt wird.

## Leistungsüberlegungen
- Schließen Sie das `Redactor`‑Objekt umgehend (wie im `finally`‑Block gezeigt), um native Ressourcen freizugeben.  
- Vermeiden Sie das Rasterisieren großer Dokumente, es sei denn, Sie benötigen eine PDF‑Vorschau; das Rasterisieren kann CPU‑ und Speicherverbrauch bei 300‑seitigen Dateien um bis zu das Dreifache erhöhen.

## Häufig gestellte Fragen

**F1: Was ist Metadaten-Redaktion?**  
A1: Metadaten‑Redaktion beinhaltet das Entfernen versteckter Dokumenteigenschaften (wie Autor, Manager oder benutzerdefinierte Tags), um eine versehentliche Offenlegung sensibler Informationen zu verhindern.

**F2: Kann ich GroupDocs.Redaction für andere Dateitypen verwenden?**  
A2: Ja, die Bibliothek unterstützt PDF, DOCX, PPTX, XLSX und viele weitere Formate – über 100 insgesamt.

**F3: Wie gehe ich mit Fehlern während der Redaktion um?**  
A3: Wickeln Sie den `apply`‑Aufruf in einen try‑catch‑Block und schließen Sie stets den `Redactor` in einer finally‑Klausel, um sicherzustellen, dass Ressourcen freigegeben werden.

**F4: Ist es möglich, benutzerdefinierte Metadatenfelder zu redigieren?**  
A5: Absolut. Verwenden Sie `MetadataFilters.Custom("YourFieldName")`, um jede benutzerdefinierte Eigenschaft im Dokument anzusprechen.

**F5: Was sind bewährte Methoden für die Verwendung von GroupDocs.Redaction?**  
A5:  
- Laden Sie die Lizenz frühzeitig in Ihrer Anwendung.  
- `Redactor`‑Objekte umgehend schließen.  
- `SaveOptions` verwenden, um ein Suffix hinzuzufügen und die Originaldateien unverändert zu lassen.  
- Redaktion an einer Kopie des Dokuments testen, bevor Stapelverarbeitungen durchgeführt werden.

**F6: Unterstützt EraseMetadataRedaction Batch‑Operationen?**  
A6: Sie können über eine Sammlung von Dateipfaden iterieren, für jede Datei eine neue `Redactor`‑Instanz erstellen und dieselbe Redaktionslogik anwenden.

**F7: Kann ich EraseMetadataRedaction mit anderen Redaktionstypen kombinieren?**  
A7: Ja, Sie können mehrere Redaktionsobjekte verketten (z. B. Text‑Redaktion gefolgt von Metadaten‑Redaktion), bevor Sie speichern.

## Ressourcen

- **Documentation**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free support**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary license**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Zuletzt aktualisiert:** 2026-10-01  
**Getestet mit:** GroupDocs.Redaction 24.9 für Java  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Groupdocs Redaction Java Document Metadata Extraction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [How to Remove Metadata Java Using GroupDocs.Redaction](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [Retrieve Document Info Using Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)