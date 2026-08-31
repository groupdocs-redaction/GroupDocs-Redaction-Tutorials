---
date: '2026-03-28'
description: Erfahren Sie, wie Sie einen benutzerdefinierten Logger in C# in GroupDocs.Redaction
  für .NET implementieren, um detailliertes benutzerdefiniertes Logging in .NET zu
  ermöglichen und die Compliance-Berichterstattung zu erleichtern.
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: Implementieren Sie einen benutzerdefinierten Logger in C# in GroupDocs.Redaction
  für .NET
type: docs
url: /de/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# Benutzerdefinierten Logger c# in GroupDocs.Redaction für .NET implementieren

Die effiziente Verwaltung von Dokumentenredaktionen ist entscheidend, insbesondere beim Umgang mit sensiblen Informationen. In diesem Leitfaden lernen Sie **wie man einen benutzerdefinierten Logger c#** mit GroupDocs.Redaction für .NET implementiert, wodurch Sie die volle Kontrolle über Protokollierung, Fehlerbehandlung und Prüfpfade erhalten.

## Schnelle Antworten
- **Was macht ein benutzerdefinierter Logger c#?** Er erfasst Fehler, Warnungen und Informationsmeldungen während der Redaktion.  
- **Welche Bibliothek stellt die ILogger‑Schnittstelle bereit?** GroupDocs.Redaction für .NET.  
- **Kann ich das redigierte Dokument ohne Rasterisierung speichern?** Ja – verwenden Sie `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`.  
- **Benötige ich eine Lizenz für den Produktionseinsatz?** Für die Produktion ist eine Voll‑Lizenz erforderlich; eine Testversion ist zur Evaluierung verfügbar.  
- **Ist dieser Ansatz mit .NET Core / .NET 6+ kompatibel?** Absolut – dieselbe API funktioniert sowohl unter .NET Framework als auch unter .NET Core/5/6.

## Was ist ein benutzerdefinierter Logger c#?
Ein **benutzerdefinierter Logger c#** ist eine Klasse, die die von GroupDocs.Redaction bereitgestellte `ILogger`‑Schnittstelle implementiert. Sie ermöglicht es Ihnen, Protokollnachrichten dorthin zu leiten, wo Sie sie benötigen – Konsole, Datei, Datenbank oder externe Überwachungssysteme – und gibt Ihnen gleichzeitig einen klaren Überblick über den Redaktionsablauf.

## Warum benutzerdefinierte Protokollierung .net mit GroupDocs.Redaction verwenden?
- **Compliance & Auditing:** Detaillierte Protokolle erfüllen regulatorische Anforderungen.  
- **Fehlertransparenz:** `LogError` und `LogWarning` geben Ihnen sofortiges Feedback zu Problemen.  
- **Integrationsflexibilität:** Leiten Sie Protokolle an bestehende .NET‑Protokollierungsframeworks weiter (Serilog, NLog usw.).

## Voraussetzungen
- **GroupDocs.Redaction für .NET** installiert (siehe Installation unten).  
- Eine .NET‑Entwicklungsumgebung (Visual Studio, VS Code oder CLI).  
- Grundkenntnisse in C# und Vertrautheit mit Dateistreams.

## Installation

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
Suchen Sie nach **"GroupDocs.Redaction"** und installieren Sie die neueste Version.

## Lizenzbeschaffung
- **Kostenlose Testversion:** Testen Sie die API mit einer temporären Lizenz.  
- **Temporäre Lizenz:** Erhalten Sie vollen Funktionszugriff für einen begrenzten Zeitraum.  
- **Kauf:** Erwerben Sie eine unbefristete Lizenz für Produktionseinsätze.

## Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Definieren einer benutzerdefinierten Logger‑Klasse (Log‑Warnungen c#)
Erstellen Sie eine Klasse, die `ILogger` implementiert. Diese Klasse erfasst Fehler, Warnungen und Informationsmeldungen.

```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```

**Erklärung:** Das `HasErrors`‑Flag hilft Ihnen zu entscheiden, ob die Verarbeitung fortgesetzt werden soll. Die drei Methoden entsprechen den drei Protokollstufen, die Sie in den meisten Redaktionsszenarien benötigen.

### Schritt 2: Dateipfade vorbereiten und das Quellendokument öffnen
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**Warum das wichtig ist:** Die Verwendung von Hilfsmethoden hält Ihren Code sauber und stellt sicher, dass der Ausgabordner existiert, bevor Sie versuchen, das **redigierte Dokument zu speichern**.

### Schritt 3: Redaktionen anwenden und dabei den benutzerdefinierten Logger verwenden
```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```

**Erklärung:**  
1. Der `Redactor` wird mit `RedactorSettings(logger)` instanziiert, wodurch Ihr `CustomLogger` verknüpft wird.  
2. Nach dem Anwenden einer Redaktion prüft der Code `logger.HasErrors`. Wenn keine Fehler aufgetreten sind, wird das Dokument gespeichert – dies demonstriert die Logik zum **Speichern des redigierten Dokuments** ohne Rasterisierung.

## Häufige Fallstricke & Fehlersuche
- **Fehlende Protokollausgabe:** Stellen Sie sicher, dass jede `Log*`‑Methode korrekt überschrieben wurde.  
- **Dateizugriffs‑Ausnahmen:** Stellen Sie sicher, dass die Anwendung Lese‑/Schreibrechte für sowohl Quell‑ als auch Ausgabepfade hat.  
- **Logger nicht verbunden:** Der Parameter `RedactorSettings(logger)` ist essenziell; das Weglassen deaktiviert die benutzerdefinierte Protokollierung.

## Praktische Anwendungen
1. **Compliance‑Berichterstattung:** Exportieren Sie Protokolleinträge in eine CSV‑Datei oder Datenbank für Prüfpfade.  
2. **Fehlerverfolgung:** Finden Sie problematische Dateien schnell, indem Sie die `LogError`‑Ausgabe durchsuchen.  
3. **Workflow‑Automatisierung:** Lösen Sie nachgelagerte Prozesse aus (z. B. Benachrichtigung eines Compliance‑Beauftragten), wenn `LogWarning` aufgerufen wird.

## Leistungsüberlegungen
- **Streams sofort freigeben**, um Speicher zu schonen, besonders bei der Verarbeitung großer Stapel.  
- **CPU‑ & Speicherverbrauch überwachen** während Massenredaktionen; erwägen Sie die parallele Verarbeitung von Dokumenten bei sorgfältiger Logger‑Synchronisation.  
- **Aktuell bleiben:** Neuere Versionen von GroupDocs.Redaction enthalten häufig Leistungsoptimierungen und zusätzliche Protokoll‑Hooks.

## Fazit
Durch die Implementierung eines **benutzerdefinierten Logger c#** erhalten Sie detaillierte Einblicke in jeden Schritt der Redaktionspipeline, was das Erreichen von Compliance‑Standards und das Debuggen von Problemen erleichtert. Der hier gezeigte Ansatz funktioniert nahtlos mit GroupDocs.Redaction für .NET und kann erweitert werden, um sich in jedes bereits genutzte .NET‑Protokollierungsframework zu integrieren.

---

## Häufig gestellte Fragen

**Q: Was ist der Zweck der benutzerdefinierten Protokollierung mit GroupDocs.Redaction?**  
A: Die benutzerdefinierte Protokollierung hilft, Redaktionen für Compliance, Fehlerverfolgung und Workflow‑Optimierung zu verfolgen und zu verwalten.

**Q: Wie gehe ich mit Fehlern unter Verwendung eines benutzerdefinierten Loggers um?**  
A: Implementieren Sie `LogError` in Ihrer `CustomLogger`‑Klasse; das `HasErrors`‑Flag ermöglicht es Ihnen, die Verarbeitung bei Bedarf zu stoppen.

**Q: Kann benutzerdefinierte Protokollierung in andere Systeme integriert werden?**  
A: Ja, Sie können Protokollnachrichten an CRM-, ERP‑ oder zentrale Überwachungstools weiterleiten, indem Sie die Logger‑Methoden erweitern.

**Q: Was sind häufige Fallstricke bei der Implementierung benutzerdefinierter Protokollierung?**  
A: Falsche Methodenumsetzungen, fehlendes `RedactorSettings(logger)` und Dateiberechtigungsprobleme sind die häufigsten.

**Q: Wie verbessert benutzerdefinierte Protokollierung die Dokumenten‑Redaktions‑Workflows?**  
A: Detaillierte Protokolle bieten Echtzeit‑Transparenz, vereinfachen die Fehlersuche und erfüllen Prüfungsanforderungen.

## Ressourcen

- **Dokumentation:** [GroupDocs.Redaction .NET Dokumentation](https://docs.groupdocs.com/redaction/net/)  
- **API‑Referenz:** [GroupDocs.Redaction API Referenz](https://reference.groupdocs.com/redaction/net)  
- **Download:** [GroupDocs.Redaction für .NET](https://downloads.groupdocs.com/redaction/net)

---

**Zuletzt aktualisiert:** 2026-03-28  
**Getestet mit:** GroupDocs.Redaction 23.11 für .NET  
**Autor:** GroupDocs  

---