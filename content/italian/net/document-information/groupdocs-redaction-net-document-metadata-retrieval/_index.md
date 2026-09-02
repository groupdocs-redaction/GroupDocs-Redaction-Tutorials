---
date: '2026-06-06'
description: Scopri come recuperare i metadati ed estrarre i metadati dei documenti
  utilizzando GroupDocs.Redaction .NET, consentendo una gestione documentale robusta
  e la conformità.
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: Come recuperare i metadati con l'API GroupDocs.Redaction .NET
type: docs
url: /it/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# Come Recuperare i Metadati con GroupDocs.Redaction .NET

Nell'era digitale odierna, **come recuperare i metadati** da un file è un passaggio fondamentale per qualsiasi applicazione incentrata sui documenti. Che tu abbia bisogno di leggere i metadati del file per audit di conformità, estrarre le proprietà del documento per l'indicizzazione, o semplicemente visualizzare la dimensione del documento in un'interfaccia utente, GroupDocs.Redaction .NET ti offre un'API concisa per farlo in poche righe di C#. Questo tutorial ti guida attraverso l'intero processo, dalla configurazione dell'ambiente alla visualizzazione delle informazioni recuperate, così potrai iniziare subito a estrarre i metadati del documento.

## Risposte Rapide
- **Qual è il metodo principale per ottenere i metadati?** Chiama `Redactor.GetDocumentInfo()` su un'istanza `Redactor`.  
- **Quali formati sono supportati?** Oltre 50 formati di input e output, inclusi PDF, DOCX, XLSX, PPTX e tipi di immagine.  
- **È necessaria una licenza per lo sviluppo?** Una licenza di prova gratuita funziona per i test; è richiesta una licenza completa per la produzione.  
- **Posso elaborare file di grandi dimensioni?** Sì—GroupDocs.Redaction gestisce documenti con centinaia di pagine senza caricare l'intero file in memoria.  
- **È disponibile il supporto async?** L'API può essere avvolta in pattern async per mantenere reattivi i thread UI.

## Cos'è il recupero dei metadati in GroupDocs.Redaction?
Il recupero dei metadati è il processo di accesso alle proprietà integrate di un documento — come tipo di file, numero di pagine e dimensione — tramite l'API della libreria. Estrarre queste proprietà consente agli sviluppatori di valutare programmaticamente le caratteristiche del documento, supportare l'indicizzazione, applicare regole di conformità e prendere decisioni informate sui passaggi di elaborazione successivi.

## Come Recuperare i Metadati del Documento?
La classe `Redactor` è l'interfaccia principale per caricare e ispezionare i documenti in GroupDocs.Redaction.  
`GetDocumentInfo()` è un metodo che restituisce un oggetto `DocumentInfo` contenente i metadati del documento.  

Carica il tuo file con `new Redactor("path/to/file")` e invoca `GetDocumentInfo()` — la chiamata restituisce un oggetto `DocumentInfo` contenente tipo, numero di pagine, dimensione e altre proprietà. Questo approccio a due passaggi funziona per qualsiasi formato supportato e non richiede configurazioni aggiuntive. Puoi quindi leggere campi come `FileType`, `PageCount` e `FileSize` per visualizzare o registrare le informazioni.

## Prerequisiti
- **GroupDocs.Redaction .NET** versione 21.6 o successiva.  
- .NET Framework 4.7.2 +, .NET Core 3.1 +, o .NET 5/6+.  
- Conoscenza di base di C# e un IDE di sviluppo (Visual Studio, Rider, ecc.).

## Configurazione di GroupDocs.Redaction per .NET

Iniziare con GroupDocs.Redaction è semplice. Installa il pacchetto usando uno dei seguenti metodi:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

Oppure, utilizza l'**UI di NuGet Package Manager**: cerca semplicemente “GroupDocs.Redaction” e fai clic su **Install**.

### Acquisizione della Licenza

Per provare GroupDocs.Redaction, puoi ottenere una licenza di prova gratuita. Per lo sviluppo continuo o l'uso in produzione, acquista una licenza completa o richiedi una licenza temporanea dal sito ufficiale.

Una volta installata, inizializza la libreria come segue:

```csharp
using GroupDocs.Redaction;
```

## Guida all'Implementazione

### Funzionalità di Ottenimento Informazioni Documento

Questa funzionalità si concentra sull'estrazione dei metadati essenziali dai documenti usando GroupDocs.Redaction .NET. Segui questi passaggi:

#### Passo 1: Preparare il Percorso del Documento

Definisci il percorso assoluto o relativo al file di destinazione:

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

Sostituisci `YOUR_DOCUMENT_DIRECTORY` con la cartella che contiene il tuo documento.

#### Passo 2: Inizializzare l'Istanza Redactor

Crea un oggetto `Redactor` che fornisce l'accesso ai metodi dei metadati:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### Passo 3: Recuperare le Informazioni del Documento

Chiama `GetDocumentInfo()` sull'istanza `Redactor` per ottenere tutte le proprietà disponibili:

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

L'oggetto restituito include il tipo di file, il numero di pagine e la dimensione del file.

#### Passo 4: Visualizzare i Dettagli del Documento

Stampa le informazioni sulla console o sull'interfaccia utente. Il codice di esempio (commentato per esecuzioni autonome) dimostra come stampare ogni proprietà:

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### Perché Usare GroupDocs.Redaction per l'Estrazione dei Metadati?
GroupDocs.Redaction supporta **oltre 50 formati di file** e può elaborare documenti fino a **2 GB** di dimensione mantenendo il consumo di memoria sotto **100 MB** per carichi di lavoro tipici. La libreria estrae i metadati senza caricare completamente il documento, fornendo risposte rapide — spesso inferiori a **200 ms** per un PDF di 100 pagine su hardware server standard.

### Problemi Comuni e Soluzioni
- **Percorso file errato** – Verifica la stringa del percorso e assicurati che il file sia accessibile al processo in esecuzione.  
- **Formato non supportato** – Controlla l'elenco dei formati; se un formato manca, considera di convertirlo prima.  
- **Colli di bottiglia delle prestazioni** – Per file molto grandi, abilita le opzioni di streaming o elabora le pagine in batch per limitare l'uso della memoria.

## Applicazioni Pratiche
Comprendere i metadati di un documento consente diversi scenari reali:

1. **Sistemi di Gestione Documentale (DMS)** – Automatizza la categorizzazione e l'indicizzazione basate su tipo, dimensione o numero di pagine.  
2. **Audit di Conformità** – Verifica che i file riservati contengano i metadati richiesti prima dell'archiviazione.  
3. **Migrazione Dati** – Raggruppa i file per proprietà per semplificare le attività di migrazione di massa.

## Considerazioni sulle Prestazioni
- **Uso Efficiente delle Risorse** – Usa l'istanza `Redactor` all'interno di un blocco `using` per garantire una corretta eliminazione.  
- **Pattern Asincroni** – Avvolgi le chiamate ai metadati in `Task.Run` o implementa wrapper async per mantenere reattivi i thread UI in applicazioni desktop o web.

## Domande Frequenti

**Q: Quali formati di documento posso estrarre i metadati?**  
A: GroupDocs.Redaction legge i metadati da più di 50 formati, inclusi PDF, DOCX, XLSX, PPTX, HTML e tipi di immagine comuni.

**Q: Come gestisco i file protetti da password?**  
A: Passa la password al costruttore `Redactor`; l'API decifrerà il file prima di estrarre i metadati.

**Q: Esiste un limite alla dimensione dei file che posso elaborare?**  
A: Sebbene non vi sia un limite rigido, i file più grandi di 2 GB potrebbero richiedere una regolazione aggiuntiva della memoria; le prestazioni rimangono lineari rispetto alla dimensione del file.

**Q: Posso recuperare i metadati in un'operazione batch?**  
A: Sì—itera su una collezione di percorsi file e chiama `GetDocumentInfo()` per ciascuno; la libreria è thread‑safe per l'esecuzione parallela.

**Q: È necessaria una licenza per le build di sviluppo?**  
A: Una licenza di prova gratuita è sufficiente per sviluppo e test; è necessaria una licenza commerciale per le distribuzioni in produzione.

## Risorse
- [Documentazione](https://docs.groupdocs.com/redaction/net/)  
- [Riferimento API](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Forum di Supporto Gratuito](https://forum.groupdocs.com/c/redaction/33)  
- [Informazioni sulla Licenza Temporanea](https://purchase.groupdocs.com/temporary-license/)

## Conclusione
Ora hai una guida completa, passo‑per‑passo, su **come recuperare i metadati** usando GroupDocs.Redaction .NET. Sfruttando il metodo `Redactor.GetDocumentInfo()`, puoi leggere rapidamente i metadati del file, supportare i flussi di lavoro di conformità e migliorare qualsiasi pipeline di elaborazione dei documenti. Esplora le funzionalità aggiuntive di Redaction — come la redazione dei contenuti, il watermarking e la conversione dei documenti — per costruire una soluzione di gestione documentale completa.

---

**Last Updated:** 2026-06-06  
**Testato Con:** GroupDocs.Redaction .NET 21.6 (latest at time of writing)  
**Autore:** GroupDocs  

## Tutorial Correlati
- [Come Estrarre i Metadati del Documento da Stream Usando GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [Come Redigere i Metadati del Documento Usando GroupDocs.Redaction per .NET - Guida Completa](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Tutorial di Caricamento Documenti con GroupDocs.Redaction per .NET](/redaction/net/document-loading/)