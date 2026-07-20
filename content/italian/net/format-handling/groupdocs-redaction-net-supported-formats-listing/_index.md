---
date: '2026-07-20'
description: Scopri come elencare i formati utilizzando GroupDocs.Redaction .NET,
  integra la funzionalità nel tuo flusso di lavoro dei documenti e migliora le prestazioni.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Scopri come elencare i formati con GroupDocs.Redaction .NET, consulta
  una guida passo‑passo e ottieni consigli per prestazioni ottimali nelle tue applicazioni
  .NET.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Come elencare i formati con GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: Come elencare i formati con GroupDocs.Redaction .NET
type: docs
url: /it/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Come elencare i formati con GroupDocs.Redaction .NET

Gestire una vasta gamma di tipi di documento è una realtà quotidiana per gli sviluppatori che creano applicazioni incentrate sui documenti. In questo tutorial imparerai **come elencare i formati** che GroupDocs.Redaction .NET può gestire, così potrai convalidare i file prima dell'elaborazione, presentare agli utenti opzioni accurate e mantenere efficiente il tuo flusso di lavoro.

## Introduzione

Una gestione efficiente dei documenti inizia conoscendo esattamente quali tipi di file supporta la tua libreria. GroupDocs.Redaction fornisce un metodo integrato per recuperare queste informazioni, consentendoti di creare elementi UI dinamici, applicare regole di convalida e evitare errori di runtime. Di seguito troverai tutto il necessario per avviare il tutto, dall'installazione a snippet di codice pratici e consigli sulle prestazioni.

### Risposte rapide
- **Cosa significa “come elencare i formati”?** Si riferisce al recupero della collezione di estensioni di file che GroupDocs.Redaction può elaborare.  
- **È necessaria una licenza?** Sì, è richiesta una licenza valida di GroupDocs.Redaction per l'uso in produzione.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Quanti formati sono disponibili?** Oltre 30 formati di input e output sono supportati subito.  
- **È necessaria qualche configurazione speciale?** Non è richiesta alcuna configurazione aggiuntiva oltre l'inizializzazione standard della libreria.

## Cos'è “come elencare i formati”

Consiste nel chiamare l'API FileType della libreria per ottenere una collezione in cui ogni voce contiene l'estensione del file e un nome leggibile dall'uomo. Gli sviluppatori possono quindi iterare questa collezione per creare regole di convalida, popolare menu a tendina UI o registrare i tipi supportati, garantendo che vengano elaborati solo documenti compatibili.

## Perché elencare i formati con GroupDocs.Redaction?

GroupDocs.Redaction supporta **oltre 30** tipi di file distinti — inclusi PDF, DOCX, PPTX e formati immagine — consentendoti di gestire la maggior parte dei documenti aziendali senza convertitori di terze parti. Elencando programmaticamente questi formati elimini le congetture, riduci i ticket di supporto e garantisci che solo i file compatibili entrino nella tua pipeline di elaborazione.

## Prerequisiti

- **GroupDocs.Redaction per .NET** – scarica l'ultimo pacchetto dal sito ufficiale.  
- **.NET Framework o .NET Core** – compatibile con il tuo ambiente di sviluppo.  
- **Visual Studio** (o qualsiasi IDE compatibile con C#).  
- Familiarità di base con la sintassi C#.

## Configurazione di GroupDocs.Redaction per .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Package Manager
`Install-Package GroupDocs.Redaction`

### Interfaccia UI di NuGet Package Manager
- Cerca **“GroupDocs.Redaction”** e installa l'ultima versione.

### Acquisizione della licenza
GroupDocs offre una prova gratuita, una licenza temporanea per la valutazione o opzioni di acquisto completo. Visita il sito web di GroupDocs per ottenere il file di licenza appropriato.

### Inizializzazione e configurazione di base
Dopo aver aggiunto il pacchetto, importa lo spazio dei nomi e crea un'istanza di `Redactor`:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Guida all'implementazione

### Come elencare i formati con GroupDocs.Redaction .NET?
Carica la libreria, chiama l'helper statico e ordina i risultati — questo ti fornisce una collezione pronta all'uso in sole due righe di codice. Usa `FileType.GetSupportedFileFormats()` per recuperare un `IEnumerable<FileType>` che include l'estensione e il nome visualizzato di ogni formato, quindi ordina per estensione per ottenere un elenco UI pulito.

### Recupero dei formati di file supportati

#### Panoramica
L'obiettivo è ottenere un elenco di tipi di file che GroupDocs.Redaction può gestire, facilitando l'integrazione nella logica di convalida, nei menu a tendina UI o nei meccanismi di logging.

#### Implementazione passo‑a‑passo

**1. Recupera i tipi di file supportati**  
`FileType.GetSupportedFileFormats()` restituisce tutti i formati riconosciuti dalla libreria. Il metodo fa parte della classe `GroupDocs.Redaction.FileType`, che incapsula metadati come l'estensione del file e il nome leggibile.

**2. Visualizza i tipi di file supportati**  
Itera sulla collezione e stampa l'estensione e la descrizione di ogni formato. Esempio di codice inline:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

Lo snippet stampa un elenco ordinato come “.pdf – Portable Document Format”, rendendolo perfetto per popolare gli elementi UI.

### Suggerimenti per la risoluzione dei problemi
- **Pacchetto mancante** – Verifica il riferimento al pacchetto NuGet e ripristina i pacchetti se necessario.  
- **Percorso licenza errato** – Assicurati che il file di licenza sia copiato nella directory di output o fornisci un percorso assoluto.  
- **Estensione non supportata** – Se un formato non è elencato, conferma di utilizzare l'ultima versione della libreria; le versioni più recenti aggiungono formati aggiuntivi.

## Applicazioni pratiche
Comprendere i formati di file supportati apre diverse situazioni reali:

1. **Sistemi di gestione documentale** – Convalida i caricamenti rispetto all'elenco supportato per prevenire errori di elaborazione.  
2. **Sicurezza dei contenuti** – Applica regole di redazione solo ai tipi di file che il motore può modificare in modo sicuro.  
3. **Pipeline di elaborazione batch** – Filtra grandi lotti di file prima di invocare la redazione, risparmiando CPU e memoria.

## Considerazioni sulle prestazioni
- **Impronta di memoria** – L'elenco dei formati è un'operazione leggera; non carica alcun documento in memoria.  
- **Operazioni batch** – Quando si elaborano centinaia di file, recupera l'elenco dei formati una sola volta e riutilizzalo per evitare chiamate ridondanti.  
- **Sicurezza dei thread** – `FileType.GetSupportedFileFormats()` è thread‑safe e può essere chiamato da task paralleli senza sincronizzazione.

## Conclusione
Ora disponi di un approccio completo e pronto per la produzione per **come elencare i formati** usando GroupDocs.Redaction .NET. Integrando questa funzionalità, puoi migliorare la convalida, migliorare l'esperienza utente e mantenere robuste le tue pipeline di documenti.

### Prossimi passi
- Esplora l'API `Redactor` per applicare regole di redazione basate sul tipo di file.  
- Combina l'elenco dei formati con un menu a tendina front‑end per una selezione di file senza interruzioni.  
- Rivedi la guida alle prestazioni per ottimizzare i job batch su larga scala.

## Domande frequenti

**D: Posso recuperare l'elenco dei formati senza inizializzare un'istanza Redactor?**  
R: Sì, `FileType.GetSupportedFileFormats()` è statico e non richiede un oggetto `Redactor`.

**D: L'elenco include sia i formati di input che di output?**  
R: Il metodo restituisce tutti i formati che la libreria può sia leggere che scrivere; ogni `FileType` include un flag `CanRead` e `CanWrite`.

**D: Con quale frequenza viene aggiornato l'elenco dei formati supportati?**  
R: GroupDocs rilascia aggiornamenti dei formati con ogni versione della libreria; controllare l'elenco a runtime garantisce di avere sempre l'ultimo set.

**D: Esiste un modo per filtrare solo i formati compatibili con PDF?**  
R: Sì, filtra la collezione dove `format.Extension == ".pdf"` o dove `format.Name.Contains("PDF")`.

**D: Questo approccio funziona su .NET Core 2.1?**  
R: Il metodo richiede .NET Core 3.1 o versioni successive; i runtime precedenti non sono supportati.

## Sezione FAQ
1. **Come installo GroupDocs.Redaction per .NET?**  
   Usa il comando CLI `dotnet add package GroupDocs.Redaction` o installa tramite l'interfaccia UI di NuGet Package Manager.  
2. **Quali sono alcuni problemi comuni nel recuperare i formati supportati?**  
   Assicurati che tutte le dipendenze siano ripristinate e che tu stia facendo riferimento allo spazio dei nomi corretto (`GroupDocs.Redaction`).  
3. **Posso usare questa funzionalità con applicazioni non .NET?**  
   Questo tutorial si concentra su .NET, ma GroupDocs fornisce API simili per Java, Python e altre piattaforme.  
4. **Come posso ottimizzare le prestazioni usando GroupDocs.Redaction?**  
   Riutilizza l'elenco dei formati, evita di caricare documenti completi quando controlli solo la compatibilità e monitora l'uso della memoria durante i job batch.  
5. **Quali tipi di file supporta GroupDocs.Redaction?**  
   La libreria supporta oltre 30 formati, inclusi PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG e molti altri. Usa `FileType.GetSupportedFileFormats()` per visualizzare l'elenco completo.

## Risorse
- [Documentazione](https://docs.groupdocs.com/redaction/net/)
- [Riferimento API](https://reference.groupdocs.com/redaction/net)
- [Scarica GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/redaction/33)
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-07-20  
**Tested With:** GroupDocs.Redaction 4.2.0 for .NET  
**Author:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## Tutorial correlati

- [Tutorial sulla gestione dei formati per GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Tutorial sul caricamento dei documenti con GroupDocs.Redaction per .NET](/redaction/net/document-loading/)
- [Tutorial sul salvataggio dei documenti per GroupDocs.Redaction .NET](/redaction/net/document-saving/)