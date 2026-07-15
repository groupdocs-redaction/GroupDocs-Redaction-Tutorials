---
date: '2026-03-28'
description: Scopri come implementare un logger personalizzato in C# in GroupDocs.Redaction
  per .NET, abilitando una registrazione dettagliata personalizzata in .NET e una
  più semplice generazione di report di conformità.
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: Implementare un logger personalizzato C# in GroupDocs.Redaction per .NET
type: docs
url: /it/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# Implementa logger personalizzato c# in GroupDocs.Redaction per .NET

Gestire le redazioni dei documenti in modo efficiente è fondamentale, soprattutto quando si trattano informazioni sensibili. In questa guida imparerai **come implementare un custom logger c#** con GroupDocs.Redaction per .NET, ottenendo il pieno controllo su logging, gestione degli errori e tracciamento degli audit.

## Risposte rapide
- **Cosa fa un custom logger c#?** Cattura errori, avvisi e messaggi informativi durante la redazione.  
- **Quale libreria fornisce l'interfaccia ILogger?** GroupDocs.Redaction per .NET.  
- **Posso salvare il documento redatto senza rasterizzazione?** Sì – usa `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`.  
- **È necessaria una licenza per l'uso in produzione?** È richiesta una licenza completa per la produzione; è disponibile una versione di prova per la valutazione.  
- **Questo approccio è compatibile con .NET Core / .NET 6+?** Assolutamente – la stessa API funziona su .NET Framework e .NET Core/5/6.

## Cos'è un custom logger c#?
Un **custom logger c#** è una classe che implementa l'interfaccia `ILogger` fornita da GroupDocs.Redaction. Ti consente di indirizzare i messaggi di log dove necessario—console, file, database o sistemi di monitoraggio esterni—offrendoti una visione chiara del flusso di lavoro di redazione.

## Perché utilizzare il logging personalizzato .net con GroupDocs.Redaction?
- **Conformità e audit:** Log dettagliati soddisfano i requisiti normativi.  
- **Visibilità degli errori:** `LogError` e `LogWarning` forniscono feedback immediato sui problemi.  
- **Flessibilità di integrazione:** Inoltra i log ai framework di logging .NET esistenti (Serilog, NLog, ecc.).

## Prerequisiti
- **GroupDocs.Redaction per .NET** installato (vedi installazione sotto).  
- Un ambiente di sviluppo .NET (Visual Studio, VS Code o CLI).  
- Conoscenza di base di C# e familiarità con gli stream di file.

## Installazione

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
Cerca **"GroupDocs.Redaction"** e installa l'ultima versione.

## Acquisizione licenza
- **Versione di prova gratuita:** Testa l'API con una licenza temporanea.  
- **Licenza temporanea:** Ottieni l'accesso a tutte le funzionalità per un periodo limitato.  
- **Acquisto:** Ottieni una licenza perpetua per le distribuzioni in produzione.

## Guida passo‑passo

### Passo 1: Definisci una classe custom logger (log warnings c#)

Crea una classe che implementa `ILogger`. Questa classe catturerà errori, avvisi e messaggi informativi.

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

**Spiegazione:** Il flag `HasErrors` ti aiuta a decidere se continuare l'elaborazione. I tre metodi corrispondono ai tre livelli di log di cui avrai bisogno nella maggior parte degli scenari di redazione.

### Passo 2: Prepara i percorsi dei file e apri il documento sorgente

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**Perché è importante:** L'uso di metodi di utilità mantiene il codice pulito e garantisce che la cartella di output esista prima di tentare di **salvare il documento redatto**.

### Passo 3: Applica le redazioni utilizzando il custom logger

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

**Spiegazione:**  
1. Il `Redactor` viene istanziato con `RedactorSettings(logger)`, collegando il tuo `CustomLogger`.  
2. Dopo aver applicato una redazione, il codice verifica `logger.HasErrors`. Se non si sono verificati errori, il documento viene salvato—dimostrando la logica di **salvare il documento redatto** senza rasterizzazione.

### Problemi comuni e risoluzione

- **Output di log mancante:** Verifica che ogni metodo `Log*` sia correttamente sovrascritto.  
- **Eccezioni di accesso al file:** Assicurati che l'applicazione abbia i permessi di lettura/scrittura sia per i percorsi di origine che di output.  
- **Logger non collegato:** Il parametro `RedactorSettings(logger)` è essenziale; ometterlo disabilita il logging personalizzato.

## Applicazioni pratiche

1. **Report di conformità:** Esporta le voci di log in CSV o database per i tracciati di audit.  
2. **Tracciamento degli errori:** Individua rapidamente i file problematici scansionando l'output di `LogError`.  
3. **Automazione del flusso di lavoro:** Attiva processi a valle (ad es., notificare un responsabile della conformità) quando viene invocato `LogWarning`.

## Considerazioni sulle prestazioni

- **Chiudi gli stream prontamente** per liberare memoria, specialmente durante l'elaborazione di grandi lotti.  
- **Monitora CPU e memoria** durante le redazioni massive; considera l'elaborazione dei documenti in parallelo con una sincronizzazione attenta del logger.  
- **Rimani aggiornato:** Le versioni più recenti di GroupDocs.Redaction includono spesso ottimizzazioni delle prestazioni e hook di logging aggiuntivi.

## Conclusione

Implementando un **custom logger c#**, ottieni una visione granulare di ogni fase della pipeline di redazione, facilitando il rispetto degli standard di conformità e il debug dei problemi. L'approccio mostrato qui funziona senza problemi con GroupDocs.Redaction per .NET e può essere esteso per integrarsi con qualsiasi framework di logging .NET che utilizzi già.

---

## Domande frequenti

**D: Qual è lo scopo del logging personalizzato con GroupDocs.Redaction?**  
R: Il logging personalizzato aiuta a tracciare e gestire le redazioni per la conformità, il tracciamento degli errori e l'ottimizzazione del flusso di lavoro.

**D: Come gestisco gli errori usando un custom logger?**  
R: Implementa `LogError` nella tua classe `CustomLogger`; il flag `HasErrors` ti consente di interrompere l'elaborazione se necessario.

**D: Il logging personalizzato può essere integrato con altri sistemi?**  
R: Sì, puoi inoltrare i messaggi di log a CRM, ERP o strumenti di monitoraggio centralizzati estendendo i metodi del logger.

**D: Quali sono alcuni errori comuni nell'implementare il logging personalizzato?**  
R: Implementazioni errate dei metodi, mancanza di `RedactorSettings(logger)` e problemi di permessi sui file sono i più frequenti.

**D: In che modo il logging personalizzato migliora i flussi di lavoro di redazione dei documenti?**  
R: Log dettagliati forniscono visibilità in tempo reale, semplificano il troubleshooting e soddisfano i requisiti di audit.

## Risorse

- **Documentazione:** [Documentazione GroupDocs.Redaction .NET](https://docs.groupdocs.com/redaction/net/)  
- **Riferimento API:** [Riferimento API GroupDocs.Redaction](https://reference.groupdocs.com/redaction/net)  
- **Download:** [Download GroupDocs.Redaction per .NET](https://downloads.groupdocs.com/redaction/net)

---

**Ultimo aggiornamento:** 2026-03-28  
**Testato con:** GroupDocs.Redaction 23.11 per .NET  
**Autore:** GroupDocs