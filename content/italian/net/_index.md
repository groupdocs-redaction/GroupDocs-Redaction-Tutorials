---
additionalTitle: GroupDocs API References
date: 2026-10-06
description: Scopri come redact pagine PDF, rimuovere le annotazioni PDF e redact
  celle Excel usando GroupDocs.Redaction for .NET – un'API sicura, cross‑platform
  per la redaction dei documenti.
keywords:
- how to redact pdf
- remove pdf annotations
- redact excel cells
- redact pdf pages
- load pdf from stream
lastmod: 2026-10-06
linktitle: Tutorial di GroupDocs.Redaction for .NET
og_description: Come redact pagine PDF rapidamente con GroupDocs.Redaction for .NET.
  L'API rimuove le annotazioni PDF, redact celle Excel e protegge i dati sensibili
  su più di 30+ formats.
og_image_alt: Guide to redact PDF pages using GroupDocs.Redaction for .NET
og_title: Come redact pagine PDF – GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  headline: How to redact PDF pages with GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  name: How to redact PDF pages with GroupDocs.Redaction for .NET
  steps:
  - name: load the PDF
    text: You can open a file from disk, a memory stream, or a remote source. The
      API accepts both a file path string and a `Stream` object, which is ideal for
      web services that receive uploads.
  - name: define the pages to redact
    text: Pass a list of zero‑based page indexes or a range string such as `"1-3,5"`
      to the `RemovePages` method. The library validates the range and throws a clear
      exception if a page does not exist.
  - name: save the sanitized document
    text: Call `Save` with the desired output format. You can keep the original PDF,
      export to a rasterized PDF, or stream the result directly to the client response.
  type: HowTo
- questions:
  - answer: Yes, the library removes the specified pages while preserving page numbering,
      bookmarks, and cross‑references for the remaining content.
    question: Can I redact PDF pages without affecting the rest of the document’s
      layout?
  - answer: Absolutely. Use `Redactor.RemoveAnnotations()` to strip all annotation
      objects in a single call.
    question: Is it possible to redact PDF annotations only?
  - answer: Load the workbook with `Redactor.LoadExcel(path)`, then call `Redactor.RedactCell(sheetName,
      cellAddress, RedactionMode.Blackout)` and save.
    question: How do I redact Excel cells directly?
  - answer: Yes, you can pass any `System.IO.Stream` to the `Load` method, which is
      ideal for processing files uploaded via ASP.NET Core controllers.
    question: Does GroupDocs.Redaction support loading PDFs from a stream?
  - answer: Metered licensing lets you pay per‑redaction operation, scaling cost‑effectively
      with usage spikes.
    question: What licensing model is recommended for high‑volume production use?
  type: FAQPage
tags:
- pdf redaction
- groupdocs.redaction
- .net document security
- redact pdf pages
title: Come redact pagine PDF con GroupDocs.Redaction for .NET
type: docs
url: /it/net/
weight: 10
---

# Come censurare pagine PDF con GroupDocs.Redaction per .NET

Se hai bisogno di **censurare pagine PDF** rapidamente e in modo affidabile, GroupDocs.Redaction per .NET ti offre un'API completa, multipiattaforma, che rimuove contenuti sensibili da oltre 30 formati di file. Che tu stia costruendo un flusso di lavoro guidato dalla conformità, un portale di gestione documenti o un'applicazione incentrata sulla privacy, questa libreria ti consente di cancellare definitivamente i dati riservati preservando il resto della struttura del documento.

**GroupDocs.Redaction per .NET è una libreria .NET che consente la rimozione permanente di contenuti sensibili da più di 30 formati di documento.** Supporta l'elaborazione ad alto volume, può gestire file con centinaia di pagine senza caricare l'intero documento in memoria e offre opzioni di rasterizzazione che trasformano il testo in immagini per una sicurezza aggiuntiva.

{{% alert color="primary" %}}
GroupDocs.Redaction per .NET offre una suite completa di tutorial ed esempi per implementare la censura sicura dei documenti nelle tue applicazioni .NET. Dalle sostituzioni di testo di base alla pulizia avanzata dei metadati, queste risorse coprono le tecniche essenziali per censurare informazioni sensibili nei documenti. Scopri come rimuovere definitivamente dati privati da vari formati di documento, inclusi PDF, Word, Excel, PowerPoint e immagini, con controllo preciso e rimozione completa del contenuto riservato. Le nostre guide passo‑passo ti aiutano a padroneggiare sia le capacità di censura standard che quelle avanzate per soddisfare i requisiti di conformità e proteggere efficacemente le informazioni sensibili.
{{% /alert %}}

## Risposte rapide
- **GroupDocs.Redaction può censurare intere pagine PDF?** Sì, è possibile eliminare pagine singole o intervalli di pagine con una singola chiamata API.  
- **Supporta la rimozione delle annotazioni PDF?** Assolutamente – annotazioni, commenti e markup possono essere rimossi in un unico passaggio.  
- **Posso censurare celle Excel senza convertire in PDF?** Sì, la libreria agisce direttamente sui fogli di lavoro Excel.  
- **È supportato il caricamento di un PDF da uno stream?** L'API accetta oggetti `Stream`, consentendo l'elaborazione in‑memory.  
- **Quali versioni .NET sono compatibili?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Cos'è la censura nel contesto dei PDF?
La censura è la rimozione permanente o l'oscuramento di contenuti sensibili da un documento in modo che non possano essere recuperati o visualizzati in seguito. Nei file PDF, la censura può riguardare testo, immagini, annotazioni o intere pagine, e il risultato è un file sanificato che conserva il layout originale.

## Perché usare GroupDocs.Redaction per .NET?
GroupDocs.Redaction per .NET offre una soluzione robusta e ad alte prestazioni in grado di gestire documenti di grandi dimensioni garantendo la rimozione completa dei dati sensibili, offrendo rasterizzazione integrata, ampio supporto di formati e registrazione dettagliata degli audit, rendendola ideale per applicazioni guidate dalla conformità e ambienti enterprise.

- **30+ formati supportati** – inclusi PDF, DOCX, XLSX, PPTX, HTML e i comuni tipi di immagine.  
- **Prestazioni scalabili** – elabora PDF di 500 pagine in meno di 5 secondi su un server tipico, senza caricare l'intero file in RAM.  
- **Rasterizzazione integrata** – converte le pagine censurate in immagini, garantendo che non rimanga testo nascosto.  
- **Pronta per la conformità** – soddisfa i requisiti GDPR, HIPAA e PCI‑DSS con registrazione dei log di audit.

## Prerequisiti
- .NET Framework 4.5+ **or** .NET Core 3.1+ installato sulla tua macchina di sviluppo.  
- Una licenza valida di GroupDocs.Redaction (disponibile una versione di prova per la valutazione).  
- Accesso ai file PDF, Excel o Word che intendi elaborare.

## Come censurare pagine PDF passo passo

Redactor è la classe principale in GroupDocs.Redaction che carica, modifica e salva i documenti. RemovePages rimuove le pagine specificate dal documento caricato.

Carica il PDF, definisci le pagine da rimuovere, applica la censura e salva il risultato. La risposta diretta seguente spiega il modello di base:

Carica il PDF di destinazione con `Redactor.Load(streamOrPath)`, chiama `Redactor.RemovePages(pageNumbers)` per eliminare le pagine indesiderate e infine invoca `Redactor.Save(outputPath)` – questo flusso a tre passaggi censura le pagine in meno di un secondo per la maggior parte dei documenti.

### Passo 1: caricare il PDF
Puoi aprire un file dal disco, da uno stream di memoria o da una fonte remota. L'API accetta sia una stringa di percorso file sia un oggetto `Stream`, ideale per i servizi web che ricevono upload.

### Passo 2: definire le pagine da censurare
Passa un elenco di indici di pagina basati su zero o una stringa di intervallo come `"1-3,5"` al metodo `RemovePages`. La libreria valida l'intervallo e genera un'eccezione chiara se una pagina non esiste.

### Passo 3: salvare il documento sanificato
Chiama `Save` con il formato di output desiderato. Puoi mantenere il PDF originale, esportare in PDF rasterizzato o inviare lo stream del risultato direttamente alla risposta del client.

## Problemi comuni e soluzioni
- **Problema:** La censura sembra funzionare ma il testo originale è ancora ricercabile.  
  **Soluzione:** Abilita la rasterizzazione (`Redactor.Rasterize = true`) prima del salvataggio; questo converte la pagina in un'immagine, rimuovendo i livelli di testo nascosti.  

- **Problema:** PDF di grandi dimensioni causano eccezioni OutOfMemory.  
  **Soluzione:** Usa `Redactor.Load(stream, loadOptions => loadOptions.EnableMemoryOptimization = true)` per elaborare il file a blocchi.  

- **Problema:** Le annotazioni non vengono rimosse.  
  **Soluzione:** Chiama `Redactor.RemoveAnnotations()` dopo aver caricato il documento; questo metodo elimina commenti, evidenziazioni e campi modulo.

## Domande frequenti

**D: Posso censurare pagine PDF senza influire sul layout del resto del documento?**  
R: Sì, la libreria rimuove le pagine specificate preservando la numerazione delle pagine, i segnalibri e i riferimenti incrociati per il contenuto rimanente.

**D: È possibile censurare solo le annotazioni PDF?**  
R: Assolutamente. Usa `Redactor.RemoveAnnotations()` per rimuovere tutti gli oggetti di annotazione in una singola chiamata.

**D: Come posso censurare direttamente le celle Excel?**  
R: Carica la cartella di lavoro con `Redactor.LoadExcel(path)`, quindi chiama `Redactor.RedactCell(sheetName, cellAddress, RedactionMode.Blackout)` e salva.

**D: GroupDocs.Redaction supporta il caricamento di PDF da uno stream?**  
R: Sì, puoi passare qualsiasi `System.IO.Stream` al metodo `Load`, ideale per elaborare file caricati tramite controller ASP.NET Core.

**D: Quale modello di licenza è consigliato per un uso di produzione ad alto volume?**  
R: La licenza a consumo (metered) ti consente di pagare per operazione di censura, scalando in modo conveniente con i picchi di utilizzo.

---
**Ultimo aggiornamento:** 2026-10-06  
**Testato con:** GroupDocs.Redaction 23.10 per .NET  
**Autore:** GroupDocs  

### Tutorial di GroupDocs.Redaction per .NET – come censurare pagine PDF

### [Tutorial di avvio](./getting-started/)

Inizia qui se sei nuovo a GroupDocs.Redaction. Questo tutorial ti guida attraverso l'installazione, la licenza e la creazione del tuo primo progetto di censura in .NET. Vedrai come aprire un documento, definire una semplice regola di censura e salvare il file sanificato.

### [Tecniche di censura avanzate](./advanced-redaction/)

Approfondisci con gestori di censura personalizzati, politiche, callback e censura assistita dall'IA. Questa guida mostra come costruire pipeline flessibili che possono **censurare pagine PDF**, gestire strutture di documento complesse e integrare modelli di machine‑learning per una rilezione più intelligente dei contenuti.

### [Tutorial di censura delle annotazioni](./annotation-redaction/)

Le annotazioni spesso contengono note riservate. Impara a individuare, modificare o rimuovere completamente annotazioni, commenti e markup di revisione da PDF, file Word e altri formati supportati.

### [Tutorial sulle informazioni del documento](./document-information/)

Comprendere i metadati di un documento è il primo passo per una censura sicura. Questo tutorial spiega come recuperare le proprietà del documento, elencare i formati supportati e generare immagini di anteprima prima di applicare qualsiasi censura.

### [Tutorial sul caricamento dei documenti](./document-loading/)

I documenti possono risiedere su disco, in stream o dietro strati di autenticazione. Scopri le migliori pratiche per caricare file locali, stream di memoria e documenti protetti da password in modo sicuro.

### [Tutorial sul salvataggio dei documenti](./document-saving/)

Dopo la censura dovrai conservare il file pulito. Questa guida copre il salvataggio nel formato originale, l'esportazione in PDF rasterizzato e lo streaming dei risultati direttamente a un'applicazione client.

### [Tutorial sulla gestione dei formati](./format-handling/)

GroupDocs.Redaction supporta una vasta gamma di formati. Esplora come lavorare con diversi tipi di file, creare gestori di formati personalizzati ed estendere la libreria per coprire standard di documenti di nicchia.

### [Tutorial di censura delle immagini](./image-redaction/)

Le immagini possono nascondere dati visivi sensibili. Impara a censurare regioni specifiche dell'immagine, rimuovere le immagini incorporate e pulire i metadati dell'immagine per garantire che non rimanga alcuna informazione nascosta.

### [Tutorial su licenze e configurazione](./licensing-configuration/)

Una licenza corretta è fondamentale per l'uso in produzione. Questo tutorial mostra come applicare le licenze, configurare le impostazioni di runtime e implementare la licenza a consumo per distribuzioni scalabili.

### [Tutorial di censura dei metadati](./metadata-redaction/)

I metadati spesso trapelano dettagli riservati. Segui questa guida per rimuovere le proprietà del documento, i commenti nascosti e altri metadati da file PDF, Word, Excel e PowerPoint.

### [Tutorial di integrazione OCR](./ocr-integration/)

Quando si lavora con PDF o immagini scannerizzate, l'OCR è essenziale. Impara a integrare motori OCR, estrarre testo ricercabile e poi **censurare pagine PDF** che contengono informazioni sensibili.

### [Tutorial di censura delle pagine](./page-redaction/)

A volte è necessario eliminare intere pagine. Questo tutorial dimostra come cancellare pagine singole, intervalli di pagine e rimuovere pagine in modo condizionale in base al contenuto.

### [Tutorial di censura specifica per PDF](./pdf-specific-redaction/)

I PDF hanno funzionalità uniche come livelli, annotazioni e campi modulo. Padroneggia le tecniche di censura specifiche per PDF, inclusi il filtraggio dei contenuti e la conservazione dell'integrità del documento.

### [Tutorial sulle opzioni di rasterizzazione](./rasterization-options/)

I PDF rasterizzati trasformano il contenuto in immagini, rendendo impossibile l'estrazione dei dati. Impara a configurare rumore, inclinazione, scala di grigi e bordi, e scopri come **salvare file PDF rasterizzati** per la massima sicurezza.

### [Tutorial di censura dei fogli di calcolo](./spreadsheet-redaction/)

I fogli di calcolo Excel spesso contengono celle riservate. Questa guida mostra come mirare e **censurare celle Excel**, nascondere formule e proteggere fogli di lavoro sensibili.

### [Tutorial di censura del testo](./text-redaction/)

Il testo è il tipo di dato più comune da proteggere. Segui le istruzioni passo‑passo per il matching di frasi esatte, la censura con espressioni regolari e le ricerche case‑sensitive, incluso come **censurare testo Word** in modo efficiente.

## Tutorial correlati

- [Come rimuovere le annotazioni – Tutorial di censura delle annotazioni per GroupDocs.Redaction .NET](/redaction/net/annotation-redaction/)
- [Come rimuovere l'ultima pagina di un PDF usando GroupDocs.Redaction per .NET](/redaction/net/page-redaction/remove-last-page-pdf-groupdocs-redaction-net/)
- [Come censurare PDF e salvare come PDF rasterizzato con GroupDocs.Redaction per .NET](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)