---
date: '2026-07-06'
description: Scopri come censurare documenti .net usando gli stream con GroupDocs.Redaction.
  Questo tutorial copre la configurazione, il caricamento del documento dallo stream,
  l'applicazione delle censure e il salvataggio sicuro.
keywords:
- redact documents .net
- load document from stream
- GroupDocs.Redaction streams
schemas:
- author: GroupDocs
  dateModified: '2026-07-06'
  description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  headline: Redact documents .net using Streams – GroupDocs.Redaction Guide
  type: TechArticle
- description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  name: Redact documents .net using Streams – GroupDocs.Redaction Guide
  steps:
  - name: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Temporary License** – request a short‑term key for evaluation.'
    text: '**Temporary License** – request a short‑term key for evaluation.'
  - name: '**Full Purchase** – obtain a permanent license for production workloads.'
    text: '**Full Purchase** – obtain a permanent license for production workloads.'
  - name: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
    text: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
  - name: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
    text: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
  - name: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
    text: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
  - name: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
    text: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports over 70 formats—including PDF, DOCX, XLSX,
      PPTX, and HTML—when using stream‑based APIs.
    question: Which file formats can be processed with streams?
  - answer: Yes, call `redactor.GetRedactedDocument()` to obtain an in‑memory representation
      that you can render or inspect programmatically.
    question: Can I preview redactions before saving?
  - answer: Supply the password when opening the stream via `Redactor` overloads that
      accept `LoadOptions` containing the password.
    question: How does the library handle password‑protected files?
  - answer: The engine can process files up to 2 GB; larger files should be split
      or processed in chunks to stay within memory limits.
    question: Is there a limit on document size?
  - answer: A single license key can be used across multiple environments as long
      as the usage complies with the licensing agreement.
    question: Do I need a separate license for each deployment environment?
  type: FAQPage
title: Censurare documenti .net usando Streams – Guida GroupDocs.Redaction
type: docs
url: /it/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/
weight: 1
---

# Redigere documenti .net usando Stream – Guida completa

Welcome! In this tutorial you’ll discover how to **redact documents .net** securely by leveraging streams with GroupDocs.Redaction. We’ll walk through everything you need—from installing the library, loading a document from stream, applying precise redactions, to saving the result without leaving temporary files on disk.

## Risposte rapide
- **Quale libreria gestisce la redazione in .NET?** GroupDocs.Redaction for .NET.  
- **Posso caricare un file direttamente da uno stream?** Yes—use `FileStream` with the Redactor constructor.  
- **Quali formati sono supportati?** Over 70 input and output formats, including PDF, DOCX, XLSX, PPTX.  
- **Ho bisogno di una licenza per la produzione?** A valid GroupDocs.Redaction license is required for non‑trial use.  
- **È sicuro per file di grandi dimensioni?** Stream‑based processing avoids loading the whole file into memory, enabling handling of multi‑gigabyte documents.

## Cos'è “redact documents .net”?
**“Redact documents .net”** si riferisce al processo di rimozione permanente o mascheramento di contenuti sensibili da file utilizzando librerie .NET come GroupDocs.Redaction. Questo garantisce che i dati riservati non escano mai dal tuo sistema in chiaro. È comunemente usato nei settori legale, finanziario e sanitario per conformarsi a normative sulla privacy come GDPR e HIPAA, assicurando che i dati sensibili non possano essere recuperati dopo l'elaborazione.

## Perché usare gli stream per la redazione?
GroupDocs.Redaction supporta **70+ formati di file** e può elaborare file fino a **2 GB** senza caricarli completamente in memoria. Lo streaming riduce l'overhead I/O, migliora le prestazioni e si allinea alle migliori pratiche di sicurezza mantenendo i dati in memoria solo per il breve periodo necessario alla trasformazione.

## Prerequisiti

- **GroupDocs.Redaction for .NET** – installare tramite NuGet (vedi sotto).  
- **.NET 6+** (or .NET Framework 4.6.1+).  
- Visual Studio 2022 o qualsiasi IDE compatibile.  
- Conoscenza di base di C# e familiarità con gli stream .NET.

## Installazione di GroupDocs.Redaction

Puoi aggiungere il pacchetto con uno di questi comandi:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

Oppure trova “GroupDocs.Redaction” nell'interfaccia UI del NuGet Package Manager e fai clic su **Install**.

### Passaggi per l'acquisizione della licenza
1. **Free Trial** – scarica una versione di prova da [GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
2. **Temporary License** – richiedi una chiave a breve termine per la valutazione.  
3. **Full Purchase** – ottieni una licenza permanente per carichi di lavoro di produzione.

Una volta installata, inizializza la libreria nel tuo codice:

```csharp
using GroupDocs.Redaction;
// Initialization code here...
```  

## Come caricare un documento dallo stream?

`FileStream` fornisce uno stream per leggere e scrivere un file su disco. La classe `Redactor` elabora il documento e applica le regole di redazione. Carica il tuo file sorgente in un `FileStream`, quindi passa lo stream al costruttore `Redactor`. Questo approccio evita di scrivere il file originale in una posizione temporanea e mantiene i dati in memoria solo per la durata dell'elaborazione. Questo metodo funziona per qualsiasi formato supportato, inclusi PDF e documenti Office.

```csharp
// Directly open the source file as a read‑only stream
using var inputStream = new FileStream(inputPath, FileMode.Open, FileAccess.Read);
```

## Come inizializzare Redactor con lo stream?

La classe `Redactor` è il motore principale che manipola il contenuto del documento. Fornendo lo stream di input, abiliti la redazione in‑memoria senza file intermedi. Dopo aver creato l'istanza, puoi concatenare le regole di redazione, visualizzare in anteprima le modifiche e configurare opzioni come rasterizzazione o crittografia prima di confermare il documento finale.

```csharp
// Initialise the Redactor with the input stream
using var redactor = new GroupDocs.Redaction.Redactor(inputStream);
```

**Definition anchor:** `GroupDocs.Redaction.Redactor` è la classe principale che fornisce metodi per applicare, visualizzare in anteprima e confermare le operazioni di redazione su un documento caricato da uno stream.

## Come applicare le redazioni?

Puoi aggiungere più azioni di redazione; l'esempio sotto elimina tutte le annotazioni, che è una necessità comune per rimuovere commenti nascosti o note dei revisori. Tipi di redazione aggiuntivi come `DeleteTextRedaction` o `ReplaceTextRedaction` possono essere combinati per rimuovere o mascherare stringhe, date o pattern specifici nel documento.

```csharp
// Apply a predefined redaction that removes every annotation
redactor.Apply(new DeleteAnnotationRedaction());
```

**Definition anchor:** `DeleteAnnotationRedaction` è una regola di redazione integrata che elimina permanentemente gli oggetti di annotazione come commenti, evidenziazioni e timbri dal documento.

## Come salvare il documento redatto?

Salvare direttamente su un `FileStream` garantisce che l'output venga scritto in un'unica passata, eliminando file temporanei inutili. Puoi anche specificare il formato di output, il livello di compressione e la protezione opzionale con password tramite l'oggetto `SaveOptions` per soddisfare i requisiti di sicurezza. Infine, chiudi lo stream di output per rilasciare i handle del file e assicurarti che il file sia completamente scritto su disco.

```csharp
// Prepare the output stream for the redacted file
using var outputStream = new FileStream(outputPath, FileMode.Create, FileAccess.Write);

// Save the modified document; RasterizationOptions disabled to keep text editable
redactor.Save(outputStream, new SaveOptions { RasterizationOptions = null });
```

**Definition anchor:** `SaveOptions` ti consente di controllare come il documento viene salvato, includendo rasterizzazione, crittografia e selezione del formato.

## Casi d'uso comuni
- **Gestione di documenti legali:** Rimuovi le annotazioni riservate prima di condividere le bozze con i clienti.  
- **Conformità GDPR:** Rimuovi gli identificatori personali da contratti o registri dei dipendenti.  
- **Report di audit interno:** Nascondi le note dei revisori mantenendo intatto il contenuto principale per la distribuzione.

## Suggerimenti sulle prestazioni per file di grandi dimensioni
1. **Chiudere gli stream tempestivamente** – le istruzioni `using` chiudono automaticamente gli stream, liberando memoria.  
2. **Elaborazione batch** – Scorri una collezione di file e riutilizza una singola istanza `Redactor` quando il formato lo consente, riducendo l'overhead di allocazione.  

## Risoluzione dei problemi

1. **Accesso al file negato** – Verifica che l'account dell'applicazione abbia permessi di lettura/scrittura sulle cartelle di destinazione.  
2. **Redazione non applicata** – Assicurati che il tipo di redazione scelto sia compatibile con il formato del documento (ad es., `DeleteAnnotationRedaction` funziona per PDF e DOCX).  

## Domande frequenti

**Q: Quali formati di file possono essere elaborati con gli stream?**  
A: GroupDocs.Redaction supporta oltre 70 formati—including PDF, DOCX, XLSX, PPTX, and HTML—when using stream‑based APIs.

**Q: Posso visualizzare in anteprima le redazioni prima di salvare?**  
A: Sì, chiama `redactor.GetRedactedDocument()` per ottenere una rappresentazione in‑memoria che puoi renderizzare o ispezionare programmaticamente.

**Q: Come gestisce la libreria i file protetti da password?**  
A: Fornisci la password quando apri lo stream tramite le overload di `Redactor` che accettano `LoadOptions` contenente la password.

**Q: Esiste un limite alle dimensioni del documento?**  
A: Il motore può elaborare file fino a 2 GB; file più grandi dovrebbero essere suddivisi o elaborati a blocchi per rimanere entro i limiti di memoria.

**Q: Ho bisogno di una licenza separata per ogni ambiente di distribuzione?**  
A: Una singola chiave di licenza può essere usata in più ambienti purché l'uso sia conforme al contratto di licenza.

## Conclusione
Ora hai una soluzione completa, passo‑per‑passo, per **redact documents .net** usando gli stream con GroupDocs.Redaction. Caricando i file direttamente dagli stream, applicando redazioni mirate e salvando senza artefatti intermedi, ottieni sia sicurezza che prestazioni. Esplora tipi di redazione aggiuntivi—come la sostituzione di testo o la rimozione dei metadati—per adattare il processo alle tue specifiche esigenze di conformità.

---

**Last Updated:** 2026-07-06  
**Tested With:** GroupDocs.Redaction 5.0 for .NET  
**Author:** GroupDocs  

## Risorse
- [Documentation](https://docs.groupdocs.com/redaction/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download](https://releases.groupdocs.com/redaction/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

```csharp
string sourceFile = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "sample.docx");
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    // Proceed with document processing...
}
```

```csharp
using (var redactor = new GroupDocs.Redaction.Redactor(stream))
{
    // Apply redactions...
}
```

```csharp
redactor.Apply(new GroupDocs.Redaction.Redactions.DeleteAnnotationRedaction());
```

```csharp
string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "redacted_sample.docx");
using (Stream streamOut = File.Open(outputFile, FileMode.Create, FileAccess.Write))
{
    redactor.Save(streamOut, new GroupDocs.Redaction.Options.RasterizationOptions { Enabled = false });
}
```

## Tutorial correlati

- [Come caricare e redigere documenti usando GroupDocs.Redaction .NET: Guida completa](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Redigere e salvare documenti con GroupDocs.Redaction per .NET: Guida completa](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Come estrarre i metadati del documento da stream usando GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)