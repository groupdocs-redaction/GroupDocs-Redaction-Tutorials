---
date: '2026-03-30'
description: Erfahren Sie, wie Sie mit GroupDocs.Redaction in .NET eine Redaktionsrichtlinie
  erstellen. Dieses Tutorial zeigt Ihnen, wie Sie eine Redaktionsrichtlinie erstellen,
  anwenden und als XML‑Datei speichern.
keywords:
- GroupDocs.Redaction .NET
- create redaction policy
- save XML policy
title: Erstellen einer Redaktionsrichtlinie mit GroupDocs.Redaction .NET – Schritt‑für‑Schritt‑Anleitung
type: docs
url: /de/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# Wie man eine Redaktionsrichtlinie mit GroupDocs.Redaction .NET erstellt

In modernen Anwendungen ist der Schutz vertraulicher Daten in Dokumenten ein unverzichtbares Sicherheitsmerkmal. Egal, ob Sie Verträge, Finanzberichte oder Patientendaten bearbeiten, Sie müssen häufig **create redaction policy** erstellen, die automatisch sensible Informationen maskiert oder entfernt. In diesem Leitfaden führen wir Sie durch den gesamten Prozess – die Bibliothek installieren, Redaktionen definieren, anwenden und schließlich die Richtlinie als XML-Datei speichern, die Sie projektübergreifend wiederverwenden können.

## Schnelle Antworten
- **What does “create redaction policy” mean?** Es ist der Prozess, Regeln (Text, Regex, Bilder usw.) zu definieren, die GroupDocs.Redaction mitteilen, wie vertrauliche Inhalte ausgeblendet oder ersetzt werden.  
- **Which library do I need?** GroupDocs.Redaction for .NET (verfügbar über NuGet).  
- **Do I need a license?** Eine kostenlose Testversion funktioniert für die Entwicklung; für die Produktion ist eine permanente Lizenz erforderlich.  
- **Can I reuse the policy?** Ja – einmal als XML gespeichert, können Sie sie später laden und auf jedes Dokument anwenden.  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Was ist eine Redaktionsrichtlinie?

Eine Redaktionsrichtlinie ist eine Sammlung von Regeln, die festlegen, *was* entfernt oder ersetzt werden soll und *wie* die Ersetzung aussehen soll. Wenn Sie eine Richtlinie einmal erstellen, können Sie konsistente Sicherheitsstandards auf jedes von Ihrer Anwendung verarbeitete Dokument anwenden.

## Warum GroupDocs.Redaction zum Erstellen einer Redaktionsrichtlinie verwenden?

- **Full‑document format support** – Word, PDF, Excel, PowerPoint und vieles mehr.  
- **Programmatic control** – Exakte Phrasen, reguläre Ausdrücke oder sogar benutzerdefinierte Logik definieren.  
- **Reusable XML policies** – Exportieren Sie Ihre Regeln einmal und teilen Sie sie über Teams oder Dienste hinweg.  
- **Performance‑optimized engine** – Verarbeitet große Dateien effizient und skaliert mit Ihrer Arbeitslast.

## Voraussetzungen

- **GroupDocs.Redaction** library (kompatibel mit Ihrer .NET-Laufzeit).  
- Visual Studio, VS Code oder jede IDE, die C# unterstützt.  
- Grundlegende Kenntnisse in C# und der .NET-Projektstruktur.

## Einrichtung von GroupDocs.Redaction für .NET

Zuerst fügen Sie die Bibliothek zu Ihrem Projekt hinzu.

**Verwendung von .NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Verwendung des Package Managers**
```powershell
Install-Package GroupDocs.Redaction
```

Oder suchen Sie nach “GroupDocs.Redaction” im NuGet Package Manager UI und installieren Sie es von dort.

### Lizenzbeschaffung
- Beginnen Sie mit einer **free trial**, um die Funktionen zu erkunden.  
- Fordern Sie eine **temporary license** für erweiterte Tests an und erwerben Sie anschließend eine vollständige Lizenz für die Produktion.

### Grundlegende Initialisierung
Fügen Sie den Namespace zu Ihrer Quelldatei hinzu:

```csharp
using GroupDocs.Redaction;
```

## Wie man eine Redaktionsrichtlinie mit GroupDocs.Redaction .NET erstellt

Im Folgenden finden Sie eine Schritt‑für‑Schritt‑Anleitung, die genau zeigt, wie Sie eine Redaktionsrichtlinie erstellen und speichern.

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
Das `Redactor`‑Objekt öffnet die Datei und verwaltet ihren Lebenszyklus.

### Schritt 3: Definieren Sie die Redaktionen
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```
Hier erstellen wir zwei Regeln:
1. **ExactPhraseRedaction** – ersetzt eine bekannte Phrase durch „[REDACTED]“.  
2. **RegexRedaction** – findet Daten im Format `YYYY‑MM‑DD` und ersetzt sie durch „[DATE REDACTED]“.

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

- **Legal firms** können Aktenzahlen und Kundennamen redigieren, bevor Entwürfe geteilt werden.  
- **Finance departments** maskieren Kontonummern oder Transaktionsdaten in Berichten.  
- **Healthcare providers** stellen die HIPAA‑Konformität sicher, indem sie Patientenkennungen entfernen.

## Leistungstipps

- Öffnen Sie **ein Dokument nach dem anderen**, um den Speicherverbrauch gering zu halten.  
- Schreiben Sie **effiziente reguläre Ausdrücke**; vermeiden Sie zu breite Muster, die die Verarbeitungszeit erhöhen.  
- Halten Sie die Bibliothek **auf dem neuesten Stand**, um von Leistungsverbesserungen und neuen Redaktionstypen zu profitieren.

## Häufige Probleme und Lösungen

| Problem | Warum es passiert | Wie zu beheben |
|-------|----------------|------------|
| **IO exception beim Vorbereiten des Verzeichnisses** | Falscher Pfad oder fehlende Schreibberechtigungen | Stellen Sie sicher, dass der Ordner existiert und die Anwendung Lese-/Schreibrechte hat. |
| **Regex stimmt nicht mit dem erwarteten Text überein** | Muster ist zu streng oder es fehlen Escape‑Zeichen | Testen Sie das Regex mit einem Online‑Tester; passen Sie Quantifier an oder escapen Sie Sonderzeichen. |
| **Richtliniendatei nicht erstellt** | `SavePolicy` wurde aufgerufen, bevor Redaktionen angewendet wurden oder mit einem ungültigen Pfad | Stellen Sie sicher, dass das Ausgabeverzeichnis beschreibbar ist und rufen Sie `SavePolicy` nach `Apply` auf. |

## Häufig gestellte Fragen

**Q: Kann ich eine vorhandene XML‑Richtlinie laden, anstatt sie programmgesteuert zu erstellen?**  
A: Ja – verwenden Sie `redactor.LoadPolicy("policy.xml")`, um eine zuvor gespeicherte Richtlinie zu importieren.

**Q: Unterstützt GroupDocs.Redaction passwortgeschützte PDFs?**  
A: Absolut. Übergeben Sie das Passwort dem `Redactor`‑Konstruktor: `new Redactor(sourceFile, "password")`.

**Q: Ist es möglich, Bilder oder Metadaten zu redigieren?**  
A: Die Bibliothek stellt die Klassen `ImageRedaction` und `MetadataRedaction` für diese Szenarien bereit.

**Q: Wie gehe ich mit großen Dokumenten (Hunderte MB) um?**  
A: Verarbeiten Sie sie in Teilen oder verwenden Sie die Streaming‑API, um den Speicherverbrauch zu reduzieren; erwägen Sie außerdem, den Heap zu vergrößern, falls OutOfMemory‑Fehler auftreten.

**Q: Welches Lizenzmodell ist für die kommerzielle Nutzung erforderlich?**  
A: Für Produktionsumgebungen ist eine kostenpflichtige Lizenz erforderlich; eine Testlizenz reicht für Entwicklung und Tests.

## Fazit

Sie haben nun eine vollständige, wiederverwendbare **redaction policy**, die Sie mit GroupDocs.Redaction für .NET auf jedes Dokument anwenden können. Durch das Exportieren der Richtlinie nach XML vereinfachen Sie zukünftige Updates und gewährleisten einen konsistenten Datenschutz in Ihrer gesamten Organisation.

### Nächste Schritte
- Experimentieren Sie mit zusätzlichen Redaktionstypen wie `ImageRedaction` oder `MetadataRedaction`.  
- Integrieren Sie die Logik zum Laden der Richtlinie in Ihren Dokumenten‑Management‑Workflow für automatisierte Redaktionen.  
- Erkunden Sie die **GroupDocs.Redaction**‑API‑Referenz für erweiterte Anpassungen.

---

**Zuletzt aktualisiert:** 2026-03-30  
**Getestet mit:** GroupDocs.Redaction 5.8 for .NET  
**Autor:** GroupDocs  

**Ressourcen**  
- [Dokumentation](https://docs.groupdocs.com/redaction/net/)  
- [API‑Referenz](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Kostenloses Support‑Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Antrag für temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)