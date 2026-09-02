---
date: '2026-06-11'
description: Scopri come estrarre i metadati da flussi di documenti usando GroupDocs.Redaction
  per .NET, coprendo l'installazione, esempi di codice e applicazioni pratiche.
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: Come estrarre i metadati da flussi di documenti usando GroupDocs.Redaction
  .NET
type: docs
url: /it/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# Come estrarre i metadati da flussi di documenti usando GroupDocs.Redaction .NET

Se sei stanco di estrarre manualmente le informazioni dei documenti o di gestire file di grandi dimensioni che rallentano il tuo flusso di lavoro, **Come estrarre i metadati** rapidamente è una sfida comune, e la libreria GroupDocs.Redaction per .NET offre un modo veloce ed efficiente in termini di memoria per recuperare i dettagli del documento direttamente dai flussi. In questo tutorial imparerai a configurare la libreria, a ottenere il tipo di file, il conteggio delle pagine e la dimensione da un flusso, e a preparare una cartella di output per ulteriori elaborazioni.

## Risposte rapide
- **Cosa significa “estrarre metadati”?** Significa leggere proprietà come il tipo di file, il conteggio delle pagine e la dimensione senza aprire l'intero documento in memoria.  
- **Quale libreria gestisce questo?** GroupDocs.Redaction per .NET fornisce un'API nativa per l'estrazione di metadati basata su stream.  
- **È necessaria una licenza?** Una prova gratuita funziona per lo sviluppo; è richiesta una licenza commerciale per la produzione.  
- **Posso elaborare PDF più grandi di 1 GB?** Sì – i flussi ti consentono di gestire file fino a 2 GB senza caricare l'intero file.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ e .NET 6+.

## Cos'è l'estrazione di metadati da flussi?
L'estrazione di metadati da flussi è il processo di lettura delle proprietà del documento direttamente da un oggetto `Stream`, evitando il caricamento completo del file e risparmiando così memoria e tempo CPU. Questa tecnica è ideale per l'elaborazione batch o per servizi basati su cloud dove le risorse sono limitate.

## Perché utilizzare GroupDocs.Redaction per l'estrazione di metadati?
GroupDocs.Redaction supporta **oltre 30 formati di file** (inclusi PDF, DOCX, XLSX, PPTX e tipi di immagine) e può elaborare documenti fino a **2 GB** di dimensione mantenendo l'uso della memoria sotto **50 MB**. La sua API `Redactor` fornisce una chiamata singola per recuperare tutte le informazioni chiave del documento, eliminando la necessità di più parser.

## Prerequisiti

- **GroupDocs.Redaction per .NET** (ultima versione)  
- **.NET Framework** 4.5+ **o** **.NET Core/5+/6+**  
- Conoscenza base di C# e familiarità con I/O di file  
- Visual Studio 2019 o versioni successive  

## Come configurare GroupDocs.Redaction per .NET?
Per iniziare a utilizzare GroupDocs.Redaction, devi prima aggiungere la libreria al tuo progetto. Questo può essere fatto tramite la .NET CLI, il Package Manager di Visual Studio o l'interfaccia UI di NuGet. Scegli l'approccio che meglio si adatta al tuo flusso di lavoro; la CLI è ideale per build scriptabili, mentre l'UI offre un modo grafico per navigare versioni e dipendenze.

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**UI del Package Manager NuGet:**
- Apri il NuGet Package Manager in Visual Studio.  
- Cerca **"GroupDocs.Redaction"** e installa l'ultima versione.

### Passaggi per l'acquisizione della licenza
1. **Prova gratuita:** Scarica una licenza di prova per esplorare tutte le funzionalità senza restrizioni.  
2. **Licenza temporanea:** Richiedi una licenza temporanea da [GroupDocs](https://purchase.groupdocs.com/temporary-license/) per test estesi.  
3. **Acquisto:** Quando sei pronto per la produzione, acquista una licenza commerciale.  

Per ulteriori informazioni, visita il [sito web di GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Inizializzazione e configurazione di base
La classe `Redactor` è il punto di ingresso per tutte le operazioni, inclusa l'estrazione di metadati.

`Redactor` è la classe principale che rappresenta un'istanza di documento e fornisce metodi per la redazione, il recupero di informazioni e la manipolazione di file. Una volta installata, puoi creare un oggetto `Redactor` come mostrato di seguito:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

Ora che la libreria è pronta, immergiamoci nei dettagli dell'implementazione.

## Come estrarre i metadati da un flusso di documento?
Carica il documento come **stream di sola lettura**, inizializza il `Redactor` e chiama `GetDocumentInfo()` per recuperare i metadati in un unico passaggio. Questo approccio evita di caricare l'intero file in memoria, il che è fondamentale per PDF di grandi dimensioni o documenti Office con centinaia di pagine.

**Risposta diretta:** Apri il file con `File.OpenRead()`, passa lo stream a `new Redactor(stream)`, quindi chiama `redactor.GetDocumentInfo()` – il metodo restituisce un oggetto contenente il tipo di file, il conteggio delle pagine e la dimensione in sole tre righe di codice.

### Passo 1: Preparare il percorso del file sorgente
Prima, assicurati che il file sorgente esista e che la cartella di output sia pronta. Il metodo di supporto qui sotto verifica la directory di output e la crea se necessario.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*Perché?* Questo garantisce un percorso valido per le successive operazioni sui file e previene `DirectoryNotFoundException`.

### Passo 2: Aprire lo stream del documento
Utilizzare `File.OpenRead()` apre il file come **stream di sola lettura**, mantenendo l'uso della memoria basso anche per file di dimensioni gigabyte.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*Perché?* Gli stream consentono l'elaborazione in tempo reale, permettendoti di lavorare con parti del file anziché con l'intero documento.

### Passo 3: Inizializzare Redactor con lo stream del documento
`Redactor` è l'oggetto API principale che ti dà accesso alle operazioni a livello di documento, inclusa l'estrazione di metadati.

`Redactor` rappresenta un singolo documento caricato da uno stream ed espone metodi come `GetDocumentInfo()` per il rapido recupero delle proprietà.

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*Perché?* Istanziare `Redactor` con uno stream collega l'oggetto al file sottostante senza caricarlo completamente.

### Passo 4: Recuperare i metadati del documento
Chiamare `GetDocumentInfo()` restituisce un oggetto `DocumentInfo` che contiene il formato del file, il conteggio delle pagine e la dimensione del file.

`GetDocumentInfo()` estrae le proprietà principali (formato, conteggio pagine, dimensione) in una singola chiamata, eliminando la necessità di parser separati.

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*Perché?* Questo passo consolida tutti i metadati essenziali, rendendo facile registrare, filtrare o instradare i documenti in base alle loro caratteristiche.

## Come preparare una directory di output per i file elaborati?
Prima di scrivere qualsiasi file elaborato, assicurati che la cartella di destinazione esista e sia scrivibile. Controllando programmaticamente il percorso e creandolo se mancante, eviti comuni eccezioni a runtime come `DirectoryNotFoundException` o errori di permessi. Questo semplice passo rende anche il tuo codice portabile tra ambienti, sia in esecuzione locale, su un server o all'interno di un container.

**Risposta diretta:** Usa `Directory.Exists()` per verificare la presenza della cartella e `Directory.CreateDirectory()` per crearla se non esiste – questo controllo in una sola riga garantisce un percorso valido prima di qualsiasi operazione di scrittura.

### Implementare un metodo di supporto
Il metodo qui sotto incapsula la logica di verifica e creazione, restituendo il percorso verificato per uso successivo.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*Perché?* Centralizzare questa logica riduce la duplicazione e rende il codice più facile da mantenere.

## Problemi comuni e soluzioni
- **Errori di permesso:** Assicurati che l'applicazione venga eseguita con un account che abbia accesso in scrittura alla cartella di destinazione.  
- **Percorsi non validi:** Controlla i separatori di percorso (`\\` su Windows, `/` su Linux/macOS) per evitare `DirectoryNotFoundException`.  
- **Gestione di file grandi:** Rilascia gli stream prontamente (`using` statements) per liberare le handle del sistema operativo e prevenire perdite.

## Applicazioni pratiche
1. **Ingestione automatizzata di documenti:** Estrarre i metadati al caricamento, quindi archiviarli in un database per ricerca veloce e report di conformità.  
2. **Audit legali e di conformità:** Recuperare il conteggio delle pagine e i tipi di file per verificare che i documenti soddisfino gli standard normativi prima dell'archiviazione.  
3. **Gestione dei contenuti aziendali:** Utilizzare i metadati per auto‑classificare i file in cartelle, migliorando l'organizzazione e la velocità di recupero.

## Considerazioni sulle prestazioni
- **Gestione della memoria:** Avvolgi sempre gli stream in blocchi `using` così vengono eliminati automaticamente.  
- **Elaborazione batch:** Elabora i documenti in gruppi di 10‑20 per bilanciare il throughput e l'uso della memoria, specialmente su server con risorse limitate.  
- **Parallelismo:** Sfrutta `Parallel.ForEach` per file indipendenti, ma monitora CPU e I/O per evitare conflitti.

## Conclusione
Ora hai una guida completa e pronta per la produzione su **come estrarre i metadati** da flussi di documenti usando GroupDocs.Redaction per .NET. Seguendo i passaggi sopra, puoi recuperare efficientemente il tipo di file, il conteggio delle pagine e la dimensione mantenendo basso l'uso della memoria e gestendo agevolmente file di grandi dimensioni.

**Passaggi successivi**
- Rivedi il riferimento API completo nella [documentazione](https://docs.groupdocs.com/redaction/net/).  
- Approfondisci la [Documentazione GroupDocs Redaction .NET](https://docs.groupdocs.com/redaction/net/) per esplorare le funzionalità di redazione, filigrana e OCR.  
- Sperimenta con diversi formati di file (PDF, DOCX, XLSX) per vedere come i metadati variano tra i tipi.  
- Integra i metadati estratti nella tua soluzione di gestione documentale o di ricerca esistente.  

## Domande frequenti

**D: Qual è il caso d'uso principale per l'estrazione di metadati di GroupDocs.Redaction?**  
R: Consente un recupero rapido ed efficiente in termini di memoria delle proprietà del documento per indicizzazione, controlli di conformità e instradamento automatico senza aprire l'intero file.

**D: Posso estrarre i metadati da file protetti da password?**  
R: Sì, fornisci la password durante la costruzione dell'oggetto `Redactor`; l'API decritterà lo stream internamente.

**D: La libreria supporta formati non PDF come DOCX o XLSX?**  
R: Assolutamente – GroupDocs.Redaction gestisce oltre 30 formati, inclusi PDF, DOCX, XLSX, PPTX e i comuni tipi di immagine.

**D: Quanto grande può essere un documento che posso elaborare con gli stream?**  
R: Gli stream consentono l'elaborazione di file fino a **2 GB** mantenendo il consumo di memoria sotto **50 MB**, grazie alla lettura in tempo reale.

**D: Dove posso ottenere aiuto se incontro problemi?**  
R: Visita il [forum di GroupDocs](https://forum.groupdocs.com/c/redaction/33) per supporto della community, o consulta la documentazione ufficiale per suggerimenti di risoluzione dei problemi.

---

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs  

**Resources**  
- **Documentazione:** [Documentazione GroupDocs Redaction .NET](https://docs.groupdocs.com/redaction/net/)  
- **Riferimento API:** [Riferimento API GroupDocs Redaction](https://reference.groupdocs.com/redaction/net)  
- **Download:** [Ultime versioni GroupDocs](https://releases.groupdocs.com/redaction/net)

## Tutorial correlati

- [Recupero avanzato dei metadati del documento con l'API GroupDocs.Redaction .NET](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)  
- [Come redigere i metadati del documento usando GroupDocs.Redaction per .NET - Guida completa](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)  
- [Redazione sicura di documenti in .NET usando gli stream: Guida per GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)