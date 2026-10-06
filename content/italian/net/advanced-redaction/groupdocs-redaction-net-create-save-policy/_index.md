---
date: '2026-10-06'
description: Scopri come censurare dati sensibili con GroupDocs.Redaction .NET. Questa
  guida passo‑passo ti mostra come creare, applicare e salvare una policy di censura
  come XML.
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: Scopri come censurare dati sensibili con GroupDocs.Redaction .NET.
  Questa guida passo‑passo ti mostra come creare, applicare e salvare una policy di
  censura come XML.
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: Come censurare dati sensibili usando GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: Come censurare dati sensibili usando GroupDocs.Redaction .NET
type: docs
url: /it/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# Come redigere dati sensibili usando GroupDocs.Redaction .NET

Proteggere le informazioni riservate all'interno di contratti, bilanci finanziari o cartelle cliniche è un requisito imprescindibile per le applicazioni moderne. In questa guida imparerai **come redigere dati sensibili** con GroupDocs.Redaction per .NET, dall'installazione dell'SDK alla definizione di politiche XML riutilizzabili che possono essere applicate a qualsiasi tipo di documento.

## Risposte rapide
- **Cosa significa “create redaction policy”?** È il processo di definire regole (testo, regex, immagini, ecc.) che indicano a GroupDocs.Redaction come nascondere o sostituire contenuti riservati.  
- **Quale libreria è necessaria?** GroupDocs.Redaction per .NET, disponibile tramite NuGet.  
- **È necessaria una licenza?** Una versione di prova gratuita è sufficiente per lo sviluppo; è richiesta una licenza permanente per la produzione.  
- **Posso riutilizzare la politica?** Sì—una volta salvata come XML è possibile caricarla in seguito e applicarla a qualsiasi documento.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Cos'è una politica di redazione?

Una politica di redazione è una raccolta di regole che specificano *cosa* deve essere rimosso o sostituito e *come* deve apparire la sostituzione. Creando una politica una sola volta, è possibile applicare standard di sicurezza coerenti a ogni documento elaborato dalla tua applicazione.

## Come funziona una politica di redazione?

Carica un documento con il motore `Redactor`, allega una o più regole di redazione, quindi invoca `Apply`. Il motore analizza il documento, maschera il contenuto corrispondente e, facoltativamente, genera un nuovo file. Lo stesso insieme di regole può essere esportato in XML, consentendo di riutilizzare la politica senza ricompilare il codice.

## Perché utilizzare GroupDocs.Redaction per creare una politica di redazione?

GroupDocs.Redaction offre un set completo di funzionalità che semplificano la creazione, la gestione e l'esecuzione delle politiche di redazione, garantendo una protezione dei dati coerente su diversi tipi di documento, offrendo alte prestazioni e un'integrazione semplice nelle applicazioni .NET esistenti per team e organizzazioni.

- **Ampio supporto di formati** – l'SDK gestisce più di 30 tipi di file, inclusi PDF, DOCX, XLSX, PPTX e formati immagine, e può elaborare file fino a 2 GB senza caricare l'intero file in memoria.  
- **Precisione programmatica** – definisci frasi esatte, espressioni regolari o logica personalizzata per mirare solo ai dati che devi nascondere.  
- **Politiche XML riutilizzabili** – esporta le tue regole una volta e condividile tra team, servizi o micro‑servizi.  
- **Motore ottimizzato per le prestazioni** – la libreria elabora documenti di centinaia di pagine in meno di un secondo su hardware server tipico, rendendola adatta a pipeline ad alto throughput.

## Prerequisiti
- Libreria GroupDocs.Redaction compatibile con il tuo runtime .NET.  
- Visual Studio, VS Code o qualsiasi IDE che supporti C#.  
- Familiarità di base con C# e la struttura dei progetti .NET.

## Configurare GroupDocs.Redaction per .NET

Per prima cosa, aggiungi la libreria al tuo progetto.

**Utilizzo di .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Utilizzo di Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

Oppure cerca “GroupDocs.Redaction” nell'interfaccia di NuGet Package Manager e installala da lì.

### Acquisizione della licenza
- Inizia con una **prova gratuita** per esplorare le funzionalità.  
- Richiedi una **licenza temporanea** per test estesi, quindi acquista una licenza completa per l'uso in produzione.

### Inizializzazione di base
Aggiungi lo spazio dei nomi al tuo file sorgente:

La classe `Redactor` è il motore principale che carica un documento e applica le regole di redazione.  
```csharp
using GroupDocs.Redaction;
```  

La classe `Redactor` è il motore principale di GroupDocs.Redaction che carica un documento e applica le regole di redazione.

## Come creare una politica di redazione passo dopo passo

Di seguito trovi una guida completa che dimostra come costruire programmaticamente una politica di redazione, configurare le sue regole, applicarle a un documento e infine salvare la politica come file XML per un riutilizzo futuro, garantendo una redazione coerente su più progetti e tipi di documento.

### Passo 1: prepara la directory dei documenti
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*Sostituisci `"YOUR_DOCUMENT_DIRECTORY"` con la cartella che contiene i documenti che desideri proteggere.*

### Passo 2: carica il documento
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
L'oggetto `Redactor` apre il file e ne gestisce il ciclo di vita.

### Passo 3: definisci le redazioni
ExactPhraseRedaction definisce una regola che sostituisce una frase specifica, mentre `RegexRedaction` utilizza un'espressione regolare per corrispondere a pattern.  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
Qui creiamo due regole:  
1. **ExactPhraseRedaction** – sostituisce una frase nota con “[REDACTED]”.  
2. **RegexRedaction** – trova le date nel formato `YYYY‑MM‑DD` e le sostituisce con “[DATE REDACTED]”.

### Passo 4: applica le redazioni
```csharp
redactor.Apply(redactions);
```  
Tutte le regole definite vengono eseguite sul documento aperto in un'unica passata.

### Passo 5: salva la politica come file XML
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
Il file XML memorizza le definizioni di redazione, consentendo di riutilizzare la stessa politica senza riscrivere il codice.

## Applicazioni pratiche

- **Studi legali** possono redigere numeri di caso e nomi dei clienti prima di condividere le bozze.  
- **Dipartimenti finanziari** mascherano numeri di conto o date di transazione nei report.  
- **Fornitori di assistenza sanitaria** garantiscono la conformità HIPAA rimuovendo gli identificatori dei pazienti.

## Suggerimenti sulle prestazioni

- Apri **un documento alla volta** per mantenere basso l'uso della memoria.  
- Scrivi **espressioni regolari efficienti**; evita pattern troppo generici che aumentano il tempo di elaborazione.  
- Mantieni la libreria **aggiornata** per beneficiare di miglioramenti delle prestazioni e di nuovi tipi di redazione.

## Problemi comuni e soluzioni

| Problema | Perché accade | Come risolvere |
|----------|----------------|----------------|
| **Eccezione IO durante la preparazione della directory** | Percorso errato o permessi di scrittura mancanti | Verifica che la cartella esista e che l'applicazione abbia i permessi di lettura/scrittura. |
| **Regex non corrisponde al testo previsto** | Il pattern è troppo restrittivo o mancano caratteri di escape | Testa la regex con un tester online; regola i quantificatori o escapa i caratteri speciali. |
| **File di politica non creato** | `SavePolicy` chiamato prima di applicare le redazioni o con un percorso non valido | Assicurati che la directory di output sia scrivibile e chiama `SavePolicy` dopo `Apply`. |

## Domande frequenti

**D: Posso caricare una politica XML esistente invece di crearne una programmaticamente?**  
R: Sì—usa `redactor.LoadPolicy("policy.xml")` per importare una politica precedentemente salvata.

**D: GroupDocs.Redaction supporta PDF protetti da password?**  
R: Assolutamente. Passa la password al costruttore `Redactor`: `new Redactor(sourceFile, "password")`.

**D: È possibile redigere immagini o metadati?**  
R: L'SDK fornisce le classi `ImageRedaction` e `MetadataRedaction` per questi scenari.

**D: Come gestire documenti di grandi dimensioni (centinaia di MB)?**  
R: Elaborali a blocchi o utilizza l'API di streaming per ridurre l'impronta di memoria; il motore può gestire file fino a 2 GB senza caricare l'intero file in RAM.

**D: Quale modello di licenza è richiesto per l'uso commerciale?**  
R: È necessaria una licenza a pagamento per le distribuzioni in produzione; una licenza di prova è sufficiente per sviluppo e test.

## Conclusione

Ora disponi di una **politica di redazione** completa e riutilizzabile che puoi applicare a qualsiasi documento con GroupDocs.Redaction per .NET. Esportando la politica in XML, semplifichi gli aggiornamenti futuri e garantisci una protezione dei dati coerente in tutta l'organizzazione.

### Prossimi passi
- Sperimenta tipi di redazione aggiuntivi come `ImageRedaction` o `MetadataRedaction`.  
- Integra la logica di caricamento della politica nel tuo flusso di lavoro di gestione dei documenti per una redazione automatizzata.  
- Esplora il riferimento API di **GroupDocs.Redaction** per personalizzazioni avanzate.

**Ultimo aggiornamento:** 2026-10-06  
**Testato con:** GroupDocs.Redaction 5.8 per .NET  
**Autore:** GroupDocs  

**Risorse**  
- [Documentazione](https://docs.groupdocs.com/redaction/net/)  
- [Riferimento API](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/redaction/33)  
- [Applicazione licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

## Tutorial correlati

- [Redigere dati sensibili con GroupDocs.Redaction .NET (C#)](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)
- [Implementare la redazione di documenti usando GroupDocs.Redaction .NET: Guida passo‑passo](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
- [Come redigere documenti con GroupDocs.Redaction .NET – Guida completa](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)