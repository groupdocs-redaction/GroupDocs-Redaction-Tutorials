---
date: '2026-10-06'
description: Erfahren Sie, wie Sie sensible Daten mit GroupDocs.Redaction .NET schwärzen.
  Diese Schritt-für-Schritt-Anleitung zeigt Ihnen, wie Sie eine Redaction Policy als
  XML erstellen, anwenden und speichern.
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: Erfahren Sie, wie Sie sensible Daten mit GroupDocs.Redaction .NET
  schwärzen. Diese Schritt-für-Schritt-Anleitung zeigt Ihnen, wie Sie eine Redaction
  Policy als XML erstellen, anwenden und speichern.
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: Wie man sensible Daten mit GroupDocs.Redaction .NET schwärzt
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: Wie man sensible Daten mit GroupDocs.Redaction .NET schwärzt
type: docs
url: /de/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# Wie man sensible Daten mit GroupDocs.Redaction .NET redigiert

Der Schutz vertraulicher Informationen in Verträgen, Finanzberichten oder Patientenakten ist eine nicht verhandelbare Anforderung für moderne Anwendungen. In diesem Leitfaden lernen Sie **wie man sensible Daten** mit GroupDocs.Redaction für .NET redigiert, von der Installation des SDK bis zur Definition wiederverwendbarer XML‑Richtlinien, die auf jeden Dokumenttyp angewendet werden können.

## Schnelle Antworten
- **Was bedeutet „create redaction policy“?** Es ist der Prozess, Regeln (Text, Regex, Bilder usw.) zu definieren, die GroupDocs.Redaction mitteilen, wie vertrauliche Inhalte ausgeblendet oder ersetzt werden.  
- **Welche Bibliothek benötige ich?** GroupDocs.Redaction für .NET, verfügbar über NuGet.  
- **Brauche ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; eine permanente Lizenz ist für die Produktion erforderlich.  
- **Kann ich die Richtlinie wiederverwenden?** Ja – einmal als XML gespeichert, können Sie sie später laden und auf jedes Dokument anwenden.  
- **Welche .NET‑Versionen werden unterstützt?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Was ist eine Redaktionsrichtlinie?

Eine Redaktionsrichtlinie ist eine Sammlung von Regeln, die festlegen, *was* entfernt oder ersetzt werden soll und *wie* die Ersetzung aussehen soll. Durch das einmalige Erstellen einer Richtlinie können Sie konsistente Sicherheitsstandards auf jedes von Ihrer Anwendung verarbeitete Dokument anwenden.

## Wie funktioniert eine Redaktionsrichtlinie?

Laden Sie ein Dokument mit der `Redactor`‑Engine, fügen Sie eine oder mehrere Redaktionsregeln hinzu und rufen Sie dann `Apply` auf. Die Engine scannt das Dokument, maskiert den passenden Inhalt und kann optional eine neue Datei ausgeben. Der gleiche Regel‑Satz kann nach XML exportiert werden, sodass Sie die Richtlinie wiederverwenden können, ohne den Code neu zu kompilieren.

## Warum GroupDocs.Redaction zur Erstellung einer Redaktionsrichtlinie verwenden?

GroupDocs.Redaction bietet ein umfassendes Funktionsset, das die Erstellung, Verwaltung und Ausführung von Redaktionsrichtlinien vereinfacht, konsistenten Datenschutz über verschiedene Dokumenttypen hinweg sicherstellt und gleichzeitig hohe Leistung sowie eine einfache Integration in bestehende .NET‑Anwendungen für Teams und Organisationen liefert.

- **Breite Formatunterstützung** – das SDK verarbeitet 30+ Dateitypen, darunter PDF, DOCX, XLSX, PPTX und Bildformate, und kann Dateien bis zu 2 GB verarbeiten, ohne die gesamte Datei in den Speicher zu laden.  
- **Programmgesteuerte Präzision** – definieren Sie exakte Phrasen, reguläre Ausdrücke oder benutzerdefinierte Logik, um nur die Daten zu verbergen, die Sie ausblenden müssen.  
- **Wiederverwendbare XML‑Richtlinien** – exportieren Sie Ihre Regeln einmal und teilen Sie sie über Teams, Services oder Micro‑Services hinweg.  
- **Leistungsoptimierte Engine** – die Bibliothek verarbeitet mehrseitige Dokumente in unter einer Sekunde auf typischer Serverhardware, was sie für Hochdurchsatz‑Pipelines geeignet macht.

## Voraussetzungen
- GroupDocs.Redaction‑Bibliothek, die mit Ihrer .NET‑Laufzeit kompatibel ist.  
- Visual Studio, VS Code oder jede IDE, die C# unterstützt.  
- Grundlegende Kenntnisse in C# und der .NET‑Projektstruktur.

## Einrichtung von GroupDocs.Redaction für .NET

Zuerst fügen Sie die Bibliothek zu Ihrem Projekt hinzu.

**Verwendung der .NET‑CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Verwendung des Package Managers**  
```powershell
Install-Package GroupDocs.Redaction
```  

Oder suchen Sie nach „GroupDocs.Redaction“ im NuGet Package Manager UI und installieren Sie es dort.

### Lizenzbeschaffung
- Beginnen Sie mit einer **kostenlosen Testversion**, um die Funktionen zu erkunden.  
- Fordern Sie eine **temporäre Lizenz** für erweiterte Tests an und erwerben Sie anschließend eine Voll‑Lizenz für den Produktionseinsatz.

### Grundlegende Initialisierung
Fügen Sie den Namespace zu Ihrer Quelldatei hinzu:

Die `Redactor`‑Klasse ist die Kern‑Engine, die ein Dokument lädt und Redaktionsregeln anwendet.  
```csharp
using GroupDocs.Redaction;
```  

Die `Redactor`‑Klasse ist die Kern‑Engine von GroupDocs.Redaction, die ein Dokument lädt und Redaktionsregeln anwendet.

## So erstellen Sie eine Redaktionsrichtlinie Schritt für Schritt

Im Folgenden finden Sie eine vollständige Anleitung, die zeigt, wie Sie programmgesteuert eine Redaktionsrichtlinie erstellen, ihre Regeln konfigurieren, sie auf ein Dokument anwenden und schließlich die Richtlinie als XML‑Datei für die zukünftige Wiederverwendung speichern, um konsistente Redaktionen über mehrere Projekte und Dokumenttypen hinweg sicherzustellen.

### Schritt 1: Bereiten Sie Ihr Dokumentverzeichnis vor
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*Ersetzen Sie `"YOUR_DOCUMENT_DIRECTORY"` durch den Ordner, der die zu schützenden Dokumente enthält.*

### Schritt 2: Laden Sie das Dokument
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
Das `Redactor`‑Objekt öffnet die Datei und verwaltet deren Lebenszyklus.

### Schritt 3: Definieren Sie die Redaktionen
ExactPhraseRedaction definiert eine Regel, die eine bestimmte Phrase ersetzt, während `RegexRedaction` einen regulären Ausdruck verwendet, um Muster zu finden.  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
Hier erstellen wir zwei Regeln:  
1. **ExactPhraseRedaction** – ersetzt eine bekannte Phrase durch „[REDACTED]“.  
2. **RegexRedaction** – findet Datumsangaben im Format `YYYY‑MM‑DD` und ersetzt sie durch „[DATE REDACTED]“.

### Schritt 4: Wenden Sie die Redaktionen an
```csharp
redactor.Apply(redactions);
```  
Alle definierten Regeln werden in einem Durchlauf auf das geöffnete Dokument angewendet.

### Schritt 5: Speichern Sie die Richtlinie als XML‑Datei
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
Die XML‑Datei speichert die Redaktionsdefinitionen, sodass Sie dieselbe Richtlinie wiederverwenden können, ohne den Code neu zu schreiben.

## Praktische Anwendungen

- **Rechtsanwaltskanzleien** können Aktenzeichen und Kundennamen redigieren, bevor Entwürfe geteilt werden.  
- **Finanzabteilungen** maskieren Kontonummern oder Transaktionsdaten in Berichten.  
- **Gesundheitsdienstleister** stellen die HIPAA‑Konformität sicher, indem sie Patientenkennungen entfernen.

## Performance‑Tipps

- Öffnen Sie **ein Dokument nach dem anderen**, um den Speicherverbrauch gering zu halten.  
- Schreiben Sie **effiziente reguläre Ausdrücke**; vermeiden Sie zu breite Muster, die die Verarbeitungszeit erhöhen.  
- Halten Sie die Bibliothek **aktuell**, um von Leistungsverbesserungen und neuen Redaktionstypen zu profitieren.

## Häufige Probleme und Lösungen

| Problem | Warum es passiert | Wie zu beheben |
|-------|----------------|------------|
| **IO‑Ausnahme beim Vorbereiten des Verzeichnisses** | Falscher Pfad oder fehlende Schreibberechtigungen | Stellen Sie sicher, dass das Verzeichnis existiert und die Anwendung Lese‑/Schreibrechte hat. |
| **Regex trifft nicht den erwarteten Text** | Muster ist zu streng oder es fehlen Escape‑Zeichen | Testen Sie den Regex mit einem Online‑Tester; passen Sie Quantifier an oder escapen Sie Sonderzeichen. |
| **Richtliniendatei wurde nicht erstellt** | `SavePolicy` wurde vor dem Anwenden der Redaktionen oder mit einem ungültigen Pfad aufgerufen | Stellen Sie sicher, dass das Ausgabeverzeichnis beschreibbar ist und rufen Sie `SavePolicy` nach `Apply` auf. |

## Häufig gestellte Fragen

**Q: Kann ich eine vorhandene XML‑Richtlinie laden, anstatt sie programmgesteuert zu erstellen?**  
A: Ja – verwenden Sie `redactor.LoadPolicy("policy.xml")`, um eine zuvor gespeicherte Richtlinie zu importieren.

**Q: Unterstützt GroupDocs.Redaction passwortgeschützte PDFs?**  
A: Absolut. Übergeben Sie das Passwort dem `Redactor`‑Konstruktor: `new Redactor(sourceFile, "password")`.

**Q: Ist es möglich, Bilder oder Metadaten zu redigieren?**  
A: Das SDK stellt die Klassen `ImageRedaction` und `MetadataRedaction` für diese Szenarien bereit.

**Q: Wie gehe ich mit großen Dokumenten (Hunderte MB) um?**  
A: Verarbeiten Sie sie in Teilen oder nutzen Sie die Streaming‑API, um den Speicherverbrauch zu reduzieren; die Engine kann Dateien bis zu 2 GB verarbeiten, ohne die gesamte Datei in den RAM zu laden.

**Q: Welches Lizenzmodell ist für die kommerzielle Nutzung erforderlich?**  
A: Für Produktionsumgebungen ist eine kostenpflichtige Lizenz erforderlich; eine Testlizenz ist für Entwicklung und Tests ausreichend.

## Fazit

Sie haben nun eine vollständige, wiederverwendbare **Redaktionsrichtlinie**, die Sie mit GroupDocs.Redaction für .NET auf jedes Dokument anwenden können. Durch das Exportieren der Richtlinie nach XML vereinfachen Sie zukünftige Aktualisierungen und gewährleisten konsistenten Datenschutz in Ihrer gesamten Organisation.

### Nächste Schritte
- Experimentieren Sie mit zusätzlichen Redaktionstypen wie `ImageRedaction` oder `MetadataRedaction`.  
- Integrieren Sie die Logik zum Laden der Richtlinie in Ihren Dokumenten‑Management‑Workflow für automatisierte Redaktionen.  
- Erkunden Sie die **GroupDocs.Redaction**‑API‑Referenz für erweiterte Anpassungen.

---

**Zuletzt aktualisiert:** 2026-10-06  
**Getestet mit:** GroupDocs.Redaction 5.8 for .NET  
**Autor:** GroupDocs  

**Ressourcen**  
- [Dokumentation](https://docs.groupdocs.com/redaction/net/)  
- [API‑Referenz](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Kostenloses Support‑Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Antrag für temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)

## Verwandte Tutorials

- [Sensible Daten mit GroupDocs.Redaction .NET (C#) redigieren](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)
- [Implementieren der Dokumenten‑Redaktion mit GroupDocs.Redaction .NET&#58; Eine Schritt‑für‑Schritt‑Anleitung](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
- [Wie man Dokumente mit GroupDocs.Redaction .NET redigiert – Ein vollständiger Leitfaden](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)