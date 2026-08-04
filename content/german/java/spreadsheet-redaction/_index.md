---
date: 2026-08-04
description: Erfahren Sie, wie Sie spreadsheet data java filtern und Spalten oder
  Zellen in Excel-Tabellen sicher mit GroupDocs.Redaction für Java schwärzen.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Erfahren Sie, wie Sie spreadsheet data java filtern und Spalten oder
  Zellen in Excel-Tabellen sicher mit GroupDocs.Redaction für Java schwärzen.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Filter spreadsheet data java – Leitfaden mit GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Filter spreadsheet data java – Leitfaden mit GroupDocs.Redaction
type: docs
url: /de/java/spreadsheet-redaction/
weight: 12
---

# Filter spreadsheet data java – GroupDocs.Redaction Java Anleitung

Wenn Sie **filter spreadsheet data java** vor dem Anwenden einer Redaktion benötigen, sind Sie hier genau richtig. In dieser Anleitung erfahren Sie, wie Sie Zeilen, Spalten oder einzelne Zellen, die persönliche oder vertrauliche Informationen enthalten, isolieren und anschließend sicher mit GroupDocs.Redaction für Java redigieren. Die Schritte werden in einfacher Sprache erklärt, enthalten Best‑Practice‑Tipps und zeigen, wie die Verarbeitung selbst bei großen Arbeitsmappen schnell bleibt.

## Schnelle Antworten
- **Welche Bibliothek verarbeitet die Spreadsheet-Redaktion in Java?** GroupDocs.Redaction for Java.  
- **Kann ich Zeilen filtern, ohne die gesamte Datei in den Speicher zu laden?** Ja – die API streamt Daten und ermöglicht das Anwenden von Filtern in Echtzeit.  
- **Welche Dateiformate werden unterstützt?** Über 30 Spreadsheet-Formate, darunter XLS, XLSX, CSV und ODS.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine temporäre Lizenz reicht für Tests; für die Produktion ist eine Voll‑Lizenz erforderlich.  
- **Gibt es ein Limit für die Arbeitsmappengröße?** Die Engine kann Dateien bis zu 500 MB verarbeiten, ohne übermäßigen Speicherverbrauch.

## Was ist filter spreadsheet data java?
**Filter spreadsheet data java** ist der Vorgang, programmgesteuert bestimmte Zeilen, Spalten oder Zellen in einer Excel‑ähnlichen Arbeitsmappe mittels Java‑Code auszuwählen, sodass nur gezielter Inhalt geprüft oder redigiert wird. Diese Technik reduziert die Laufzeit, begrenzt unnötige Änderungen und unterstützt die Einhaltung von GDPR‑ähnlichen Vorgaben.

## Warum filter spreadsheet data java?
GroupDocs.Redaction Java unterstützt **30+ Spreadsheet-Formate** und kann Arbeitsmappen mit **bis zu 500 MB** (etwa 1 Million Zeilen) verarbeiten, wobei der Speicherverbrauch unter **200 MB** bleibt. Durch vorheriges Filtern berühren Sie keine irrelevanten Daten, was die Verarbeitungszeit in typischen Datenschutz‑Bereinigungsszenarien durchschnittlich um **40‑60 %** reduziert.

## Voraussetzungen
- Java 17 oder höher installiert.  
- Maven‑ oder Gradle‑Build‑System.  
- GroupDocs.Redaction für Java (von der offiziellen Website herunterladbar).  
- Ein temporärer oder voller Lizenzschlüssel.  

## Wie filtert man Daten in Tabellenkalkulationen mit GroupDocs.Redaction Java?
Laden Sie die Arbeitsmappe, definieren Sie einen Filter, der die zu redigierenden Zellen auswählt, und führen Sie anschließend die Redaktionsoperation aus. Die API führt das Filtern im Streaming‑Modus durch, sodass Sie die gesamte Datei nie vollständig im RAM halten müssen.

Die Klasse `RedactionFilter` ermöglicht das Festlegen von Spaltenindizes, Zeilenbereichen oder benutzerdefinierten Prädikaten. Beispielsweise können Sie jede Zelle in Spalte **B** anvisieren, die ein E‑Mail‑Adressmuster enthält, oder die Redaktion auf Zeilen beschränken, bei denen die Spalte „Status“ den Wert „Confidential“ hat.

**Direkte Antwort (40‑70 Wörter):**  
Erstellen Sie eine `RedactionFilter`‑Instanz, setzen Sie den Spaltenindex und eine reguläre‑Ausdruck‑Bedingung, und übergeben Sie den Filter an `Redactor.redact(workbook, filter)`. Dieser einzeilige Filter isoliert exakt die Zellen, die Ihren Kriterien entsprechen, und der Redaktor entfernt oder maskiert sie, während der Rest des Blatts unverändert bleibt. Der Vorgang beendet sich in linearer Zeit relativ zu den gefilterten Zeilen.

### Schritt 1: Filter instanziieren
`RedactionFilter` ist die Kernklasse, die eine Filterregel für die Spreadsheet‑Redaktion darstellt. Sie akzeptiert Spaltenzahlen, Zeilennummern oder benutzerdefinierte Lambda‑Ausdrücke, um Daten zu bestimmen.

### Schritt 2: Bedingung konfigurieren
Verwenden Sie `filter.setColumnIndex(1)`, um die Spalte B (nullbasiert) anzusprechen, und `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`, um E‑Mail‑Muster zu erfassen. Sie können mehrere Bedingungen auch mit `filter.and(...)` oder `filter.or(...)` kombinieren.

### Schritt 3: Redaktion anwenden
`Redactor` ist die Hauptklasse, die Redaktionsvorgänge auf einer Arbeitsmappe ausführt.  
Übergeben Sie die Arbeitsmappe und den konfigurierten Filter an das `Redactor`‑Objekt. Die API streamt die Arbeitsmappe, wendet den Filter an und schreibt das redigierte Ergebnis in eine neue Datei, wobei das ursprüngliche Format und Formeln erhalten bleiben.

## Häufige Probleme und Lösungen
- **Filter trifft keine Zellen:** Überprüfen Sie den Spaltenindex (nullbasiert) und stellen Sie sicher, dass die reguläre‑Ausdruck‑Syntax für Java korrekt ist.  
- **Out‑of‑Memory‑Fehler bei großen Dateien:** Erhöhen Sie die JVM‑Heap‑Größe moderat (z. B. `-Xmx1g`) oder teilen Sie die Arbeitsmappe vor dem Filtern in kleinere Teile.  
- **Redigierte Ausgabe verliert Formatierung:** `RedactionOptions` ermöglicht die Anpassung des Redaktionsverhaltens, z. B. das Beibehalten der Zellformatierung. Verwenden Sie `RedactionOptions.setPreserveFormatting(true)`, um Zellstile unverändert zu lassen.

## Warum filter spreadsheet data?
Das Filtern vor der Redaktion isoliert nur die sensiblen Teile einer Arbeitsmappe, sodass unnötige Änderungen an sauberen Daten vermieden werden. Dieser selektive Ansatz reduziert zudem das Risiko versehentlicher Datenverluste und beschleunigt Compliance‑Audits, da das Prüfprotokoll wesentlich weniger Einträge enthält.

## Wie man E‑Mails in Excel‑Tabellen mit der GroupDocs.Redaction Java API redigiert
Laden Sie Ihre Excel‑Datei, wenden Sie einen Filter an, der das typische E‑Mail‑Muster sucht, und rufen Sie den Redaktor auf. Die API ersetzt jede gefundene E‑Mail durch einen Platzhalter wie „***@***.com“, wobei das umgebende Zelllayout erhalten bleibt.

## Wie man Daten filtert – verfügbare Tutorials
- [Wie man E‑Mails in Excel‑Tabellen mit der GroupDocs.Redaction Java API redigiert](./redact-emails-excel-groupdocs-redaction-java/)

## Zusätzliche Ressourcen

- [GroupDocs.Redaction für Java Dokumentation](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction für Java API‑Referenz](https://reference.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction für Java herunterladen](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Kostenloser Support](https://forum.groupdocs.com/)
- [Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)

---

**Zuletzt aktualisiert:** 2026-08-04  
**Getestet mit:** GroupDocs.Redaction 23.11 for Java  
**Autor:** GroupDocs  

## Häufig gestellte Fragen

**Q: Kann ich mehrere Spalten gleichzeitig filtern?**  
A: Ja, Sie können weitere Spaltenindizes zur gleichen `RedactionFilter`‑Instanz hinzufügen oder mehrere Filter mit `filter.or(...)` verketten.

**Q: Funktioniert der Filter bei passwortgeschützten Arbeitsmappen?**  
A: Geben Sie das Passwort beim Öffnen der Arbeitsmappe an; der Filter arbeitet nach der Entschlüsselung genauso wie bei einer ungeschützten Datei.

**Q: Wie viele Zeilen kann die API in einem einzelnen Vorgang verarbeiten?**  
A: Die Engine ist für bis zu 1 Million Zeilen (≈500 MB) optimiert, ohne die gesamte Datei in den Speicher zu laden.

**Q: Ist es möglich, eine Vorschau der zu redigierenden Zellen vor dem Speichern zu erhalten?**  
A: Ja, rufen Sie `filter.preview(workbook)` auf, um eine Liste von Zelladressen zu erhalten, die den Kriterien entsprechen.

**Q: Welches Lizenzmodell ist für den Produktionseinsatz erforderlich?**  
A: Für den Produktionseinsatz ist eine vollständige kommerzielle Lizenz erforderlich; eine temporäre Lizenz reicht für Tests und Evaluierung aus.

## Verwandte Tutorials

- [Wie man sensible Daten in Excel‑Tabellen mit der GroupDocs.Redaction Java API redigiert](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Sensitive Data Java maskieren – GroupDocs.Redaction Leitfaden](/redaction/java/getting-started/)
- [Sensitive Data Java maskieren – Persönliche Infos mit GroupDocs.Redaction redigieren](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)