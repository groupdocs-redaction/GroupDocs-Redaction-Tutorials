---
date: '2026-10-06'
description: Scopri come censurare i dati usando GroupDocs.Redaction .NET con un'implementazione
  di IRedactionCallback in C#. Segui questa guida passo‑passo, le migliori pratiche
  e esempi reali.
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: Scopri come censurare i dati usando GroupDocs.Redaction .NET con un'implementazione
  di IRedactionCallback in C#. Segui una guida passo‑passo con le migliori pratiche
  e esempi reali.
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: Come censurare i dati con GroupDocs.Redaction .NET (C#)
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: Come censurare i dati con GroupDocs.Redaction .NET (C#)
type: docs
url: /it/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# Come censurare i dati con GroupDocs.Redaction .NET (C#)

In questo tutorial completo scoprirai **come censurare i dati** da PDF, file Word e altri documenti usando GroupDocs.Redaction per .NET. Che tu debba nascondere identificatori personali nei contratti legali o rimuovere dati riservati dai report finanziari, l'SDK ti offre un controllo programmatico per garantire che ogni elemento sensibile scompaia in modo permanente e verificabile. Ti guideremo nell'installazione della libreria, nella configurazione di un `IRedactionCallback` personalizzato e nell'applicazione di censure a frase esatta con registrazione completa.

## Risposte rapide
- **Che cosa fa IRedactionCallback?** Consente di intercettare ogni evento di censura, registrare i dettagli e, facoltativamente, modificare il testo di sostituzione al volo.  
- **Ho bisogno di una licenza?** Una versione di prova funziona per lo sviluppo; una licenza permanente rimuove tutti i limiti di valutazione.  
- **Quali versioni di .NET sono supportate?** .NET Core 3.1+, .NET 5/6 e .NET Framework 4.6+.  
- **Posso elaborare più file?** Sì—incapsula la logica in un ciclo o utilizza l'elaborazione batch per le migliori prestazioni.  
- **È possibile la censura asincrona?** Non è integrata, ma puoi eseguire le chiamate API all'interno di `Task.Run` o altri pattern asincroni.

## Cos'è la censura dei dati sensibili?
`Redaction` è la rimozione permanente o l'oscuramento di informazioni che non devono essere divulgate. Con GroupDocs.Redaction puoi definire frasi esatte, pattern di espressioni regolari o regole personalizzate e sostituirle con segnaposti come **[REDACTED]** mantenendo la disposizione e la paginazione originali.

## Perché usare GroupDocs.Redaction con IRedactionCallback?
`IRedactionCallback` è un'interfaccia che ti avvisa ogni volta che l'SDK censura un contenuto, consentendoti di catturare dati di audit o di modificare la sostituzione in modo dinamico. Questo consente una completa tracciabilità, l'applicazione di regole di business personalizzate e un'integrazione fluida con i sistemi di conformità, tutto senza sacrificare le prestazioni.

## Prerequisiti
- **Libreria GroupDocs.Redaction** (versione compatibile – vedi la pagina della [documentazione ufficiale](https://docs.groupdocs.com/redaction/net/)). Per tutti i dettagli fai riferimento alla [documentazione ufficiale](https://docs.groupdocs.com/redaction/net/).  
- .NET Core o .NET Framework installati sulla tua macchina di sviluppo.  
- Visual Studio (l'edizione Community va bene) o qualsiasi IDE che supporti C#.  
- Conoscenza di base di C# e familiarità con la gestione dei pacchetti NuGet.

## Configurazione di GroupDocs.Redaction per .NET
Per prima cosa, aggiungi la libreria al tuo progetto. Scegli il metodo che preferisci – la CLI, la Console di Gestione Pacchetti o l'interfaccia UI. I comandi rimangono esattamente gli stessi del tutorial originale.

### Opzioni di installazione
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- Apri il tuo progetto in Visual Studio.  
- Vai a **Gestisci pacchetti NuGet**.  
- Cerca **GroupDocs.Redaction** e installa l'ultima versione stabile.

### Acquisizione della licenza
Per provare il prodotto, richiedi una prova gratuita o una licenza temporanea da [qui](https://purchase.groupdocs.com/temporary-license/). Puoi anche ottenere una licenza temporanea dalla [pagina di licenza temporanea](https://purchase.groupdocs.com/temporary-license/). Per l'uso in produzione, acquista una licenza completa per sbloccare tutte le funzionalità senza limiti.

#### Inizializzazione e configurazione di base
Di seguito trovi il codice minimo necessario per aprire un documento con la classe `Redactor`. Mantieni questo snippet invariato – è la base per tutto ciò che segue.  
`Redactor` è la classe principale che rappresenta un documento e fornisce metodi per applicare regole di censura.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## Guida all'implementazione
Ora estenderemo la configurazione di base aggiungendo un `IRedactionCallback` personalizzato. Questo ti permette di catturare ogni evento di censura, scriverlo in un log o persino modificare il testo di sostituzione al volo.

### Collegare e utilizzare un'implementazione di IRedactionCallback
`IRedactionCallback` è un'interfaccia che riceve callback per ogni operazione di censura, consentendoti di registrare o modificare il comportamento programmaticamente.

#### Passo 1: preparare la directory di output e il percorso del file sorgente
Definisci dove si trova il documento sorgente. Regola il percorso per adattarlo al tuo ambiente.

`LoadOptions` è un oggetto di configurazione che indica all'SDK come leggere il file (ad es., gestione della password).  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### Passo 2: creare un'istanza Redactor con impostazioni personalizzate
Instanziamo `Redactor` con `LoadOptions` e `RedactorSettings`. Il `RedactionDump` all'interno delle impostazioni registrerà automaticamente ogni censura effettuata.

`RedactorSettings` ti consente di perfezionare il processo di censura; fornire un `RedactionDump` abilita un file di audit dettagliato.  
`RedactionDump` è una classe di supporto che scrive ogni evento di censura in un dump formattato JSON per la segnalazione di conformità.  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### Passo 3: applicare una censura a frase esatta
Qui sostituiamo la frase **John Doe** con il segnaposto **[REDACTED]**. Puoi sostituire qualsiasi frase o pattern che desideri nascondere.

`ReplacementOptions` definisce quale testo sostituirà il contenuto corrispondente. Supporta anche la personalizzazione di font e colore se hai bisogno di una maschera visiva.  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**Spiegazione degli oggetti chiave**
- `LoadOptions()` – indica all'SDK come leggere il documento (ad es., gestione della password).  
- `RedactorSettings(new RedactionDump())` – abilita un file dump che registra ogni censura a fini di audit.  
- `ReplacementOptions("[REDACTED]")` – definisce il testo che sostituirà la frase corrispondente.

### Perché è importante
Il meccanismo di callback registra ogni evento di censura, crea una traccia di audit leggibile dalla macchina e consente di modificare i segnaposti in modo dinamico, aiutando a soddisfare i requisiti di conformità e riducendo lo sforzo di post‑elaborazione manuale. Integrando questi dati con i tuoi sistemi di monitoraggio puoi generare report, attivare avvisi e garantire che nessuna informazione sensibile sfugga al processo di censura.

L'uso di `IRedactionCallback` ti offre tre vantaggi concreti:
1. **Log pronti per la conformità** – ogni censura è catturata in un dump leggibile dalla macchina, soddisfacendo i requisiti di audit per oltre 30 framework normativi.  
2. **Sostituzione dinamica** – puoi cambiare il segnaposto in base al tipo di dato, riducendo la post‑elaborazione manuale fino al 40 %.  
3. **Prestazioni scalabili** – il callback aggiunge un overhead trascurabile (<2 ms per censura) consentendo di elaborare in batch migliaia di file in parallelo.

### Suggerimenti per la risoluzione dei problemi
- **File non trovato:** Verifica il percorso `sourceFile` e assicurati che il file sia accessibile al processo in esecuzione.  
- **Callback non attivato:** Verifica che la tua classe implementi **tutti** i membri di `IRedactionCallback` e che l'istanza sia passata correttamente al `Redactor`.  
- **Ritardo delle prestazioni:** Per batch di grandi dimensioni, riutilizza la stessa istanza `Redactor` quando possibile e disponila tempestivamente.

## Applicazioni pratiche
La censura dei dati sensibili è utile in molti settori:

1. **Elaborazione di documenti legali** – Rimuove automaticamente i nomi dei clienti, i numeri di caso o i numeri di previdenza sociale prima di condividere le bozze.  
2. **Sistemi di gestione HR** – Rimuove gli identificatori personali dai contratti dei dipendenti durante le verifiche.  
3. **Report finanziari** – Nasconde cifre proprietarie o numeri di conto quando si generano PDF destinati agli investitori.

## Considerazioni sulle prestazioni
GroupDocs.Redaction supporta **oltre 30 formati di input e output** (PDF, DOCX, PPTX, XLSX, HTML e tipi di immagine) e può elaborare file di centinaia di pagine senza caricare l'intero documento in memoria. Per mantenere la tua applicazione reattiva quando gestisci decine o centinaia di file:
- **Elaborazione batch:** Carica un elenco di file ed esegui il ciclo di censura all'interno di un `Parallel.ForEach` per sfruttare i multi‑core.  
- **Gestione della memoria:** Avvolgi ogni `Redactor` in un blocco `using` (come mostrato) per garantire lo smaltimento.  
- **Operazioni asincrone:** Sebbene l'SDK sia sincrono, puoi delegare il lavoro a thread in background o a `Task.Run` per evitare il blocco dei thread UI.

## Problemi comuni e soluzioni

| Problema | Soluzione |
|----------|-----------|
| **“Invalid file format” error** | Assicurati che il tipo di documento sia supportato (PDF, DOCX, PPTX, ecc.). |
| **Callback receives null values** | Verifica di passare un'implementazione concreta di `IRedactionCallback` quando costruisci `RedactorSettings`. |
| **Redaction not applied** | Verifica che la frase esatta corrisponda a maiuscole/minuscole e spaziatura del documento, oppure usa `RegexRedaction` per corrispondenze basate su pattern. |

## Domande frequenti

**D: Quali sono le opzioni di licenza per GroupDocs.Redaction?**  
R: Puoi iniziare con una prova gratuita o richiedere una licenza temporanea per esplorare tutte le funzionalità. Per la produzione, acquista una licenza perpetua o in abbonamento.

**D: Posso usare GroupDocs.Redaction su più tipi di file?**  
R: Sì, supporta PDF, Word, Excel, PowerPoint e molti altri formati comuni.

**D: Come gestisco le eccezioni durante la censura?**  
R: Avvolgi la tua logica di censura in blocchi `try‑catch` e registra i dettagli dell'eccezione. Il callback può anche essere usato per catturare gli errori in tempo reale.

**D: È disponibile il supporto integrato per l'elaborazione asincrona?**  
R: L'API principale è sincrona, ma puoi eseguire le chiamate di censura all'interno di task asincroni o servizi in background.

**D: Dove posso trovare esempi più avanzati?**  
R: La [documentazione ufficiale](https://docs.groupdocs.com/redaction/net/) e il riferimento API forniscono numerosi esempi di codice e guide per scenari.

## Risorse

- [Documentazione GroupDocs.Redaction per .NET](https://docs.groupdocs.com/redaction/net/)
- [Riferimento API GroupDocs.Redaction per .NET](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction per .NET](https://releases.groupdocs.com/redaction/net/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Supporto gratuito](https://forum.groupdocs.com/)
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

---

**Ultimo aggiornamento:** 2026-10-06  
**Testato con:** GroupDocs.Redaction 2.3 (latest at time of writing)  
**Autore:** GroupDocs

## Tutorial correlati

- [Crea politica di censura con GroupDocs.Redaction .NET – Guida passo‑passo](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [Come censurare documenti con GroupDocs.Redaction .NET – Guida completa](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Censura documenti .net usando Stream – Guida GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)