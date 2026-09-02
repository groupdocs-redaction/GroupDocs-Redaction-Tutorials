---
date: 2026-06-11
description: Scopri come esportare file redatti, configurare le cartelle di output,
  creare PDF rasterizzati e salvare su stream utilizzando GroupDocs.Redaction per
  .NET.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: Come esportare documenti redatti con GroupDocs.Redaction .NET
type: docs
url: /it/net/document-saving/
weight: 3
---

# Come esportare documenti redatti con GroupDocs.Redaction .NET

In questa guida completa scoprirai **come esportare contenuti redatti** in modo sicuro ed efficiente usando GroupDocs.Redaction per .NET. Che tu debba mantenere il tipo di file originale, bloccare il documento come PDF rasterizzato o trasmettere il risultato direttamente in memoria, ti guideremo attraverso ogni opzione con spiegazioni chiare, conversazionali e consigli pratici. Alla fine di questo tutorial sarai in grado di scegliere la strategia di esportazione giusta per qualsiasi scenario guidato dalla conformità.

## Risposte rapide
- **Quali formati posso esportare?** Qualsiasi dei più di 30 formati nativi supportati da GroupDocs.Redaction, più PDF rasterizzato per la massima sicurezza.  
- **Ho bisogno di una licenza per lo streaming?** Sì, è necessaria una licenza valida di GroupDocs.Redaction per lo streaming in produzione.  
- **Posso impostare una cartella di output personalizzata?** Assolutamente – usa la proprietà `OutputPath` o `SaveOptions` per configurarla.  
- **La rasterizzazione è sicura per file di grandi dimensioni?** Gestisce documenti fino a 500 pagine senza caricare l'intero file in memoria.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Cos'è GroupDocs.Redaction?
GroupDocs.Redaction è una libreria .NET che rimuove o maschera programmaticamente le informazioni sensibili da PDF, Word, Excel, PowerPoint, immagini e molti altri formati. Offre un'API di alto livello per definire le regioni di redazione, applicare le politiche e infine esportare il documento pulito. Questo rende semplice integrare le funzionalità di redazione in qualsiasi applicazione .NET.

## Perché esportare documenti redatti come PDF rasterizzati?
I PDF rasterizzati convertono ogni pagina in un'immagine piatta, eliminando i livelli di testo nascosti che potrebbero essere estratti in seguito. Questo formato garantisce che i contenuti redatti non possano essere recuperati, soddisfacendo rigorosi standard normativi come GDPR e HIPAA. GroupDocs.Redaction può generare PDF rasterizzati fino a 300 dpi, preservando la fedeltà visiva garantendo al contempo la sicurezza.

## Come esportare documenti redatti?
Carica il file sorgente, applica le regole di redazione, quindi chiama il metodo di salvataggio appropriato—`Save` per il formato originale, `SaveAsRasterizedPdf` per PDF solo immagine, o `SaveToStream` per la gestione in memoria. Di seguito il flusso di lavoro passo‑passo. Ogni metodo garantisce che il contenuto redatto sia rimosso in modo permanente mantenendo il formato di output desiderato.

### Passo 1: Installa il pacchetto NuGet
Aggiungi il pacchetto più recente di GroupDocs.Redaction al tuo progetto:

```bash
dotnet add package GroupDocs.Redaction
```

### Passo 2: Carica il documento e definisci le redazioni
Crea un'istanza di `Redactor`, carica il file e specifica le regioni che desideri nascondere. La classe `Redactor` fornisce la funzionalità principale per caricare i documenti e applicare le regole di redazione.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Passo 3: Scegli il metodo di esportazione
#### Esporta nel formato originale
```csharp
redactor.Save("RedactedReport.docx");
```

#### Esporta come PDF rasterizzato
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Esporta in uno stream di memoria (ideale per API web)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

Il metodo `Save` scrive il documento redatto in un file nel suo formato originale. `SaveAsRasterizedPdf` crea un PDF in cui ogni pagina è resa come immagine, rimuovendo qualsiasi testo nascosto. `SaveToStream` restituisce il file redatto come stream di memoria, adatto per le risposte web.

## Come configurare una cartella di output?
Imposta la proprietà `OutputPath` sul `Redactor` o passa un oggetto `SaveOptions` personalizzato che includa la directory desiderata. `OutputPath` è una proprietà del `Redactor` che specifica la cartella in cui vengono scritti i file di output. `SaveOptions` consente di personalizzare vari parametri di salvataggio, inclusa la cartella di output. Questo garantisce che tutti i file esportati vengano salvati in una posizione prevedibile, semplificando le pipeline di elaborazione batch. È inoltre possibile specificare sottocartelle per tipo di documento per mantenere organizzato lo spazio di lavoro.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Problemi comuni e soluzioni
- **Redazione non applicata:** Verifica che il modello di ricerca corrisponda esattamente al testo del documento; usa `RegexOptions.IgnoreCase` se necessario. `RegexOptions` è un'enumerazione che controlla il comportamento del matching delle espressioni regolari, come la sensibilità al maiuscolo/minuscolo.  
- **I file di grandi dimensioni causano pressione sulla memoria:** Abilita la modalità streaming usando `SaveToStream` ed evita di chiamare `Save` sull'intero documento.  
- **Il PDF rasterizzato appare sfocato:** Aumenta i DPI in `RasterizationOptions` (ad es., 300–600) per migliorare la qualità dell'immagine. `RasterizationOptions` consente di impostare parametri come DPI e formato immagine per l'output PDF rasterizzato.

## Domande frequenti

**Q: Posso esportare in un formato che non era originariamente supportato?**  
A: Sì, GroupDocs.Redaction può convertire la maggior parte dei tipi di input in PDF, DOCX, XLSX, PPTX o PDF rasterizzato, coprendo oltre 30 formati.

**Q: Come la rasterizzazione protegge i dati redatti?**  
A: Renderizzando ogni pagina come immagine piatta, tutti i livelli di testo nascosti vengono rimossi, rendendo impossibile estrarre il contenuto originale.

**Q: È possibile concatenare più regole di redazione?**  
A: Assolutamente – puoi chiamare `Apply` ripetutamente o passare una collezione di `RedactionOptions` per elaborare molti pattern in un unico passaggio. `RedactionOptions` definisce le impostazioni per una singola operazione di redazione, come la regione e il tipo di sostituzione.

**Q: Devo chiudere l'oggetto Redactor?**  
A: Il `Redactor` implementa `IDisposable`; avvolgilo in un blocco `using` o chiama `Dispose()` per rilasciare rapidamente le handle dei file. `IDisposable` è un'interfaccia che fornisce un meccanismo per rilasciare risorse non gestite.

**Q: Quali runtime .NET sono ufficialmente testati?**  
A: GroupDocs.Redaction è validato su .NET Framework 4.6+, .NET Core 3.1+, e .NET 5/6/7.

## Risorse aggiuntive

### Tutorial disponibili

- [Come salvare i documenti come PDF rasterizzati usando GroupDocs.Redaction per .NET: Guida completa](./groupdocs-redaction-net-rasterized-pdfs/)
- [Implementare la directory di output in .NET con GroupDocs.Redaction: Guida completa](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Redigere e salvare documenti con GroupDocs.Redaction per .NET: Guida completa](./redact-save-documents-groupdocs-redaction-net/)
- [Salvare documenti redatti nel formato originale usando GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Redazione sicura di documenti in .NET usando Stream: Guida per GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Link utili

- [Documentazione GroupDocs.Redaction per .NET](https://docs.groupdocs.com/redaction/net/)
- [Riferimento API GroupDocs.Redaction per .NET](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction per .NET](https://releases.groupdocs.com/redaction/net/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Supporto gratuito](https://forum.groupdocs.com/)
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Redaction 23.11 for .NET  
**Author:** GroupDocs  

---

## Tutorial correlati

- [Salvare documenti redatti nel formato originale usando GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Come salvare i documenti come PDF rasterizzati usando GroupDocs.Redaction per .NET: Guida completa](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Redazione sicura di documenti in .NET usando Stream: Guida per GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)