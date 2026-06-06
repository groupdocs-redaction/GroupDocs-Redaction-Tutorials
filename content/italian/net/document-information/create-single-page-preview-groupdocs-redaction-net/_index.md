---
date: '2026-06-06'
description: Scopri come convertire una pagina in PNG e visualizzare le pagine PDF
  con GroupDocs.Redaction per .NET. Guida passo‑passo, esempi di codice e consigli
  pratici.
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: Converti pagina in PNG usando GroupDocs.Redaction .NET
type: docs
url: /it/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# Converti pagina in PNG usando GroupDocs.Redaction .NET

Creare un'anteprima di una singola pagina da un documento voluminoso è una necessità comune quando si desidera condividere solo la parte rilevante delle informazioni. In questo tutorial imparerai **come convertire una pagina in PNG** con GroupDocs.Redaction per .NET, configurare l'output dell'anteprima e integrare il risultato nelle tue applicazioni. Ti guideremo attraverso i prerequisiti, l'installazione, la configurazione del codice e consigli pratici, così potrai iniziare a generare anteprime PNG a pagina singola in pochi minuti.

## Risposte rapide
- **Posso generare un'anteprima PNG di una sola pagina?** Sì, usa `PreviewOptions` per specificare il numero di pagina e il formato.  
- **Quale formato supporta GroupDocs.Redaction per le anteprime?** PNG è il formato predefinito, ma sono disponibili anche JPEG e BMP.  
- **È necessaria una licenza per lo sviluppo?** Una prova gratuita è sufficiente per i test; è richiesta una licenza di produzione per l'uso commerciale.  
- **Funziona su .NET Core e .NET Framework?** Assolutamente – la libreria è destinata a .NET Standard 2.0+.  
- **Il processo è efficiente in termini di memoria per file di grandi dimensioni?** Sì, l'API trasmette le pagine in streaming, evitando il caricamento completo del documento.

## Cos'è convertire pagina in PNG?
**convert page to PNG** indica l'estrazione di una singola pagina da un documento supportato (PDF, DOCX, PPTX, ecc.) e il rendering di quella pagina come immagine Portable Network Graphics (PNG). L'immagine risultante conserva il layout visivo, i caratteri e la grafica della pagina originale, consentendo di condividere un'istantanea chiara mantenendo nascosta la restante parte del documento.

## Perché utilizzare un'anteprima a pagina singola?
Generare un'anteprima PNG a pagina singola riduce la larghezza di banda, velocizza i tempi di caricamento e protegge i contenuti sensibili esponendo solo ciò che è necessario. GroupDocs.Redaction può rendere un PDF di 300 pagine in un PNG da 200 KB in meno di 0,5 secondi su hardware server tipico, rendendolo ideale per portali web e strumenti di reporting.

## Prerequisiti

- **GroupDocs.Redaction for .NET** – la libreria principale che esegue la redazione dei documenti e la generazione di anteprime.  
- **System.IO** – namespace .NET standard per la gestione dei file.  
- .NET Core 3.1+ o .NET Framework 4.6.1+ (qualsiasi piattaforma che supporti .NET Standard 2.0).  
- Conoscenza di base di C# e familiarità con la gestione dei pacchetti NuGet.

## Configurazione di GroupDocs.Redaction per .NET

### Informazioni sull'installazione

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Apri il tuo progetto in Visual Studio.  
- Scegli **Manage NuGet Packages**.  
- Cerca **GroupDocs.Redaction** e installa l'ultima versione stabile.

### Passaggi per l'acquisizione della licenza
Per eseguire la libreria è necessaria una licenza valida. Puoi iniziare con una prova gratuita o richiedere una chiave temporanea:

1. Visita il [sito Web di GroupDocs](https://purchase.groupdocs.com/temporary-license) per richiedere una licenza temporanea.  
2. Segui le istruzioni inviate via email per aggiungere il file di licenza al tuo progetto.

### Inizializzazione e configurazione di base
La classe `RedactionEngine` è il punto di ingresso per tutte le operazioni, inclusa la generazione di anteprime.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## Guida all'implementazione

### Panoramica
Questa sezione mostra come **convertire una pagina in PNG** configurando `PreviewOptions` e invocando l'API di anteprima. L'approccio funziona per PDF, DOCX, PPTX e molti altri formati supportati da GroupDocs.Redaction.

### Passo 1: Preparare l'ambiente
Imposta il percorso del file sorgente e la cartella di output. Usa `Path.Combine` per costruire percorsi indipendenti dalla piattaforma.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### Passo 2: Configurare le opzioni di anteprima
`PreviewOptions` consente di definire il numero di pagina, le dimensioni dell'immagine e il formato di output. La classe è il fulcro della configurazione per la generazione dell'anteprima.  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### Spiegazione delle configurazioni chiave
- **Width & Height** – Regola questi valori per corrispondere alla risoluzione di visualizzazione desiderata.  
- **PageNumbers** – Fornisci un array con l'indice esatto della pagina che vuoi renderizzare (indice base zero).  
- **PreviewFormat** – PNG è il valore predefinito; passa a `PreviewFormat.Jpeg` per file più piccoli.

### Suggerimenti per la risoluzione dei problemi
Se il PNG non viene generato:

- Verifica che il percorso del file sorgente sia corretto e che il file sia accessibile.  
- Assicurati che il file di licenza sia caricato prima di chiamare qualsiasi metodo API.  
- Controlla che `PreviewOptions.PageNumbers` contenga un indice di pagina valido (ad esempio `0` per la prima pagina).

## Applicazioni pratiche
Creare un'anteprima PNG a pagina singola è utile in molti scenari:

1. **Presentazioni per clienti** – Mostra solo la diapositiva o la clausola contrattuale rilevante.  
2. **Revisioni interne** – Consente controlli visivi rapidi senza aprire l'intero documento.  
3. **Riepiloghi di contenuto** – Inserisci snapshot di pagina in email o dashboard per fornire contesto immediato.  

Integrare questa funzionalità in un CMS o CRM può automatizzare la generazione di miniature per i documenti caricati, migliorando l'esperienza utente.

## Considerazioni sulle prestazioni
- **Gestione della memoria** – Disporre delle istanze di `RedactionEngine` dopo l'uso per liberare le risorse.  
- **Esecuzione asincrona** – Usa `await engine.GeneratePreviewAsync(...)` nelle applicazioni UI per mantenere l'interfaccia reattiva.  
- **Aggiornamenti della libreria** – GroupDocs.Redaction supporta **oltre 30 formati di input e output** e processa documenti fino a 500 pagine senza caricare l'intero file in memoria. Mantieni il pacchetto aggiornato per beneficiare di ottimizzazioni delle prestazioni.

## Conclusione
Ora disponi di un metodo completo, pronto per la produzione, per **convertire una pagina in PNG** e generare anteprime a pagina singola con GroupDocs.Redaction per .NET. Seguendo i passaggi sopra potrai incorporare snapshot PNG di alta qualità in qualsiasi applicazione .NET, migliorando la condivisione dei documenti mantenendo sicurezza e prestazioni.

## Domande frequenti

**Q: Posso generare anteprime per PDF protetti da password?**  
A: Sì, fornisci la password durante l'inizializzazione di `RedactionEngine` e l'anteprima verrà creata normalmente.

**Q: Come cambio il formato di output da PNG a JPEG?**  
A: Imposta `options.PreviewFormat = PreviewFormat.Jpeg` prima di chiamare il metodo di anteprima.

**Q: È possibile visualizzare più pagine contemporaneamente?**  
A: Assolutamente – assegna un array di numeri di pagina a `options.PageNumbers` (ad esempio `new[] {0, 2, 4}`).

**Q: Cosa devo fare se l'immagine dell'anteprima è sfocata?**  
A: Aumenta `options.Width` e `options.Height` a una risoluzione più alta; la libreria scala l'immagine di conseguenza.

**Q: Funziona su container Linux?**  
A: Sì, GroupDocs.Redaction .NET è cross‑platform e funziona all'interno di container Docker che supportano .NET Core.

## Risorse
- [Documentazione](https://docs.groupdocs.com/redaction/net/)
- [Riferimento API](https://reference.groupdocs.com/redaction/net)
- [Scarica l'ultima versione](https://releases.groupdocs.com/redaction/net/)
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/redaction/33)
- [Acquisizione licenza temporanea](https://purchase.groupdocs.com/temporary-license)

---

**Ultimo aggiornamento:** 2026-06-06  
**Testato con:** GroupDocs.Redaction 5.6 for .NET  
**Autore:** GroupDocs

## Tutorial correlati

- [Padroneggiare la sicurezza dei documenti: rasterizzare e redigere documenti Word con GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)
- [Come eliminare pagine da PDF usando GroupDocs.Redaction .NET: guida completa](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)
- [Implementare la redazione dei documenti usando GroupDocs.Redaction .NET: guida passo‑passo](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)