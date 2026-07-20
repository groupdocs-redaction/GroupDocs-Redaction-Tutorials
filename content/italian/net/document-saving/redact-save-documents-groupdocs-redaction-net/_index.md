---
date: '2026-07-20'
description: Scopri come oscurare i documenti, nascondere le informazioni sensibili
  e salvare i file oscurati in uno stream di memoria utilizzando GroupDocs.Redaction
  per .NET.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: Come oscurare i documenti con GroupDocs.Redaction per .NET. Segui
  questa guida passo‑passo per nascondere le informazioni sensibili e salvare il file
  oscurato in uno stream di memoria.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: Come oscurare i documenti con GroupDocs.Redaction per .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: Come oscurare i documenti con GroupDocs.Redaction per .NET – Guida completa
type: docs
url: /it/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# Come Redigere Documenti con GroupDocs.Redaction per .NET

Nell'ambiente aziendale moderno, **come redigere documenti** è una competenza fondamentale per proteggere dati personali, segreti commerciali e informazioni relative alla conformità. Questa guida ti accompagna nella redazione di informazioni sensibili da file Word, PDF o immagine e poi nel salvataggio dell'output redatto direttamente in uno stream di memoria—tutto con GroupDocs.Redaction per .NET.

## Risposte Rapide
- **Che cosa fa la redazione?** Sostituisce permanentemente il contenuto selezionato con un segnaposto o lo rimuove, garantendo che i dati non possano mai essere recuperati.  
- **Quali formati sono supportati?** Oltre 30 tipi di file, inclusi PDF, DOCX, PPTX e formati immagine comuni.  
- **Posso redigere senza scrivere su disco?** Sì—salva il risultato in un `MemoryStream` per l'elaborazione in memoria.  
- **Ho bisogno di una licenza per la produzione?** È necessaria una licenza completa per l'uso in produzione; è disponibile una prova gratuita per la valutazione.  
- **È compatibile con .NET Core?** Assolutamente—GroupDocs.Redaction funziona con .NET Framework 4.6+, .NET Core 3.1+ e .NET 5/6/7.

## Cos'è la Redazione di Documenti?
La redazione di documenti rimuove o oscura permanentemente testo, immagini e metadati confidenziali da un file, garantendo che il contenuto nascosto non possa essere recuperato, visualizzato o estratto in seguito. Sostituisce gli elementi sensibili con un segnaposto, ad esempio un rettangolo nero o testo personalizzato, e aggiorna la struttura del documento in modo che i dati redatti siano irrecuperabili.

## Perché Usare GroupDocs.Redaction per Redigere Documenti?
GroupDocs.Redaction supporta **30+ formati di file** e può gestire file fino a **2 GB** senza caricare l'intero documento in memoria, offrendo un **tempo di elaborazione più veloce del 30 %** rispetto a molti concorrenti. La sua API consente di applicare redazioni basate su frase esatta, espressione regolare o immagine con una singola chiamata di metodo, rendendola la scelta più efficiente per gli sviluppatori .NET.

## Prerequisiti
- **GroupDocs.Redaction** pacchetto NuGet (ultima versione).  
- .NET Framework 4.6+ **or** .NET Core 3.1+ installato.  
- Un IDE compatibile con C# come Visual Studio 2022.  
- Conoscenze di base di C# e familiarità con I/O di file.

### Librerie Richieste e Versioni
- **GroupDocs.Redaction** – utilizza sempre l'ultima versione per accedere agli algoritmi di redazione più recenti e alle patch di sicurezza.  
- **System.IO** – per la gestione degli stream (integrato in .NET).

### Passaggi per Ottenere la Licenza
- **Prova Gratuita:** Registrati sul sito di GroupDocs per una prova di 30 giorni.  
- **Licenza Temporanea:** Richiedi una chiave temporanea per i test di sviluppo.  
- **Licenza Completa:** Acquista una licenza di produzione per utilizzo illimitato.

## Inizializzazione e Configurazione di Base
La classe `Redactor` è il punto di ingresso per tutte le operazioni di redazione in GroupDocs.Redaction. Dopo aver installato il pacchetto NuGet, istanzi `Redactor` con il percorso del documento sorgente.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## Come Redigere Testo Specifico in un Documento?
Per redigere testo specifico, carica il file sorgente con un'istanza `Redactor`, quindi applica un `ExactPhraseRedaction` che mira alla stringa esatta che desideri nascondere. L'API analizza il documento, sostituisce ogni corrispondenza con la sovrapposizione scelta e registra le modifiche in un registro dei cambiamenti, consentendoti di verificare la redazione prima di salvare.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

La classe `ExactPhraseRedaction` sostituisce ogni occorrenza della frase esatta con un rettangolo nero (o qualsiasi segnaposto personalizzato che configuri).  

**Step‑by‑Step:**
1. **Carica** – Crea un'istanza `Redactor` che punti al tuo file.  
2. **Applica** – Chiama `Apply` con un `ExactPhraseRedaction` (o altro tipo di redazione).  
3. **Ispeziona** – Esamina `RedactorChangeLog` per confermare quante corrispondenze sono state trovate e sostituite.  

## Come Salvare un Documento Redatto in uno Stream di Memoria?
`MemoryStream` è uno stream .NET che memorizza i dati in memoria, consentendo letture/scritture rapide senza I/O su disco. Utilizzando il metodo `Save`, puoi indirizzare l'output redatto in un `MemoryStream`, che può poi essere inviato su una rete, memorizzato in un database o restituito direttamente da un endpoint API senza creare file temporanei.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**Key Points:**
- Il metodo `Save` scrive l'output redatto su qualsiasi implementazione di `Stream`, inclusa `MemoryStream`.  
- Non vengono creati file temporanei, il che migliora sicurezza e prestazioni.  
- Puoi combinarlo con `FileStreamResult` di ASP.NET Core per restituire il file direttamente al browser.

## Problemi Comuni e Soluzioni
| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Redazione non applicata** | Il caso della frase differisce da quello del sorgente. | Usa `ExactPhraseRedaction("John Doe", caseSensitive: false)` o una redazione con espressione regolare per un matching flessibile. |
| **File di grandi dimensioni causano OutOfMemory** | Tentativo di caricare l'intero file in memoria. | GroupDocs.Redaction trasmette i dati internamente; assicurati di utilizzare l'ultima versione che elabora i file a blocchi. |
| **Il file salvato è corrotto** | Stream non reimpostato prima dell'invio. | Dopo `redactor.Save(stream)`, imposta `stream.Position = 0` prima di leggere o restituirlo. |

## Domande Frequenti

**D: Posso redigere file PDF usando la stessa API?**  
R: Sì—GroupDocs.Redaction tratta PDF, DOCX, PPTX e molti formati immagine in modo uniforme; basta puntare `Redactor` su un file PDF.

**D: La redazione sopravvive dopo la conversione del documento in un altro formato?**  
R: Assolutamente—una volta redatto, il contenuto è rimosso permanentemente, indipendentemente dalle conversioni successive.

**D: Come personalizzo l'aspetto della redazione?**  
R: Usa `RedactionOptions` per impostare il colore della sovrapposizione, l'opacità o sostituire il testo con una stringa personalizzata.

**D: È possibile redigere usando espressioni regolari?**  
R: Sì—`RegexRedaction` consente di definire pattern come numeri di carta di credito o indirizzi email.

**D: Quali versioni .NET sono ufficialmente supportate?**  
R: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6 e .NET 7.

---

**Ultimo Aggiornamento:** 2026-07-20  
**Testato Con:** GroupDocs.Redaction 23.12 per .NET  
**Autore:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## Tutorial Correlati

- [Come Caricare e Redigere Documenti con GroupDocs.Redaction .NET&#58; Guida Completa](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Salva Documenti Redatti nel Formato Originale con GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Redazione Sicura di Documenti in .NET Usando Stream&#58; Guida per GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)