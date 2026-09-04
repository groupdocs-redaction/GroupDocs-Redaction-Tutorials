---
date: 2026-08-04
description: Scopri come filtrare i dati del foglio di calcolo Java e redigere in
  modo sicuro colonne o celle nei fogli di calcolo Excel utilizzando GroupDocs.Redaction
  per Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Scopri come filtrare i dati del foglio di calcolo Java e redigere
  in modo sicuro colonne o celle nei fogli di calcolo Excel utilizzando GroupDocs.Redaction
  per Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Filtra i dati del foglio di calcolo Java – guida con GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Filtra i dati del foglio di calcolo Java – guida con GroupDocs.Redaction
type: docs
url: /it/java/spreadsheet-redaction/
weight: 12
---

# Filtrare i dati del foglio di calcolo java – Guida Java di GroupDocs.Redaction

Se hai bisogno di **filter spreadsheet data java** prima di applicare la redazione, sei atterrato sulla guida giusta. In questo tutorial scoprirai come isolare righe, colonne o celle individuali che contengono informazioni personali o riservate, quindi redigerle in modo sicuro con GroupDocs.Redaction per Java. I passaggi sono spiegati in modo chiaro, includono consigli di best‑practice e mostrano come mantenere l'elaborazione veloce anche su cartelle di lavoro di grandi dimensioni.

## Risposte rapide
- **Quale libreria gestisce la redazione dei fogli di calcolo in Java?** GroupDocs.Redaction for Java.  
- **Posso filtrare le righe senza caricare l'intero file in memoria?** Yes – the API streams data and lets you apply filters on the fly.  
- **Quali formati di file sono supportati?** Over 30 spreadsheet formats, including XLS, XLSX, CSV, and ODS.  
- **Ho bisogno di una licenza per lo sviluppo?** A temporary license works for testing; a full license is required for production.  
- **Esiste un limite alle dimensioni della cartella di lavoro?** The engine can process files up to 500 MB without excessive memory consumption.

## Cos'è filter spreadsheet data java?
**Filter spreadsheet data java** è il processo di selezione programmatica di righe, colonne o celle specifiche in una cartella di lavoro in stile Excel usando codice Java, in modo che solo il contenuto mirato sia esaminato o redatto. Questa tecnica riduce il tempo di esecuzione, limita le modifiche non necessarie e aiuta a soddisfare la conformità di tipo GDPR.

## Perché filtrare i dati del foglio di calcolo java?
GroupDocs.Redaction Java supporta **30+ formati di foglio di calcolo** e può elaborare cartelle di lavoro contenenti **fino a 500 MB** (circa 1 milione di righe) mantenendo l'utilizzo della memoria sotto **200 MB**. Filtrando prima, eviti di toccare dati non correlati, il che riduce il tempo di elaborazione del **40‑60 %** in media per tipici scenari di pulizia della privacy.

## Prerequisiti
- Java 17 o versioni successive installato.  
- Sistema di build Maven o Gradle.  
- GroupDocs.Redaction per Java (scaricabile dal sito ufficiale).  
- Una chiave di licenza temporanea o completa.  

## Come filtrare i dati nei fogli di calcolo usando GroupDocs.Redaction Java?
Carica la cartella di lavoro, definisci un filtro che corrisponda alle celle che desideri redigere, quindi applica l'operazione di redazione. L'API esegue il filtro in modalità streaming, quindi non è mai necessario tenere l'intero file in RAM.

La classe `RedactionFilter` ti consente di specificare gli indici delle colonne, gli intervalli di righe o predicati personalizzati. Ad esempio, puoi mirare a ogni cella nella colonna **B** che contiene un modello di indirizzo email, oppure puoi limitare la redazione alle righe in cui la colonna “Status” è uguale a “Confidential”.

**Risposta diretta (40‑70 parole):**  
Crea un'istanza di `RedactionFilter`, imposta l'indice della colonna e una condizione di espressione regolare, quindi passa il filtro a `Redactor.redact(workbook, filter)`. Questo filtro a riga singola isola le celle esatte che corrispondono ai tuoi criteri, e il redattore le rimuove o le maschera lasciando intatto il resto del foglio. L'operazione si completa in tempo lineare rispetto alle righe filtrate.

### Passo 1: istanziare il filtro
`RedactionFilter` è la classe principale che rappresenta una regola di filtraggio per la redazione dei fogli di calcolo. Accetta numeri di colonna, numeri di riga o espressioni lambda personalizzate per individuare i dati.

### Passo 2: configurare la condizione
Usa `filter.setColumnIndex(1)` per mirare alla colonna B (indice zero‑based) e `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` per corrispondere ai modelli di email. Puoi anche combinare più condizioni con `filter.and(...)` o `filter.or(...)`.

### Passo 3: applicare la redazione
`Redactor` è la classe principale che esegue operazioni di redazione su una cartella di lavoro.  
Passa la cartella di lavoro e il filtro configurato all'oggetto `Redactor`. L'API trasmette in streaming la cartella di lavoro, applica il filtro e scrive il risultato redatto in un nuovo file, preservando la formattazione e le formule originali.

## Problemi comuni e soluzioni
- **Il filtro non corrisponde a nessuna cella:** Verifica l'indice della colonna (indice zero‑based) e assicurati che la sintassi dell'espressione regolare sia corretta per Java.  
- **Errori di out‑of‑memory su file di grandi dimensioni:** Aumenta moderatamente la dimensione dell'heap JVM (ad es., `-Xmx1g`) o suddividi la cartella di lavoro in blocchi più piccoli prima del filtraggio.  
- **L'output redatto perde la formattazione:** `RedactionOptions` consente di personalizzare il comportamento della redazione, ad esempio preservando la formattazione delle celle. Usa `RedactionOptions.setPreserveFormatting(true)` per mantenere intatti gli stili delle celle.

## Perché filtrare i dati del foglio di calcolo?
Filtrare prima della redazione isola solo le parti sensibili di una cartella di lavoro, il che significa che eviti modifiche non necessarie ai dati puliti. Questo approccio selettivo riduce anche il rischio di perdita accidentale di dati e accelera gli audit di conformità perché il registro di audit contiene molte meno voci.

## Come redigere le email nei fogli di calcolo Excel usando l'API Java di GroupDocs.Redaction
Carica il tuo file Excel, applica un filtro che cerca il tipico modello di email e invoca il redattore. L'API sostituisce ogni email corrispondente con un segnaposto come “***@***.com” preservando il layout delle celle circostanti.

## Come filtrare i dati – tutorial disponibili
- [Come redigere le email nei fogli di calcolo Excel usando l'API Java di GroupDocs.Redaction](./redact-emails-excel-groupdocs-redaction-java/)

## Risorse aggiuntive
- [Documentazione di GroupDocs.Redaction per Java](https://docs.groupdocs.com/redaction/java/)
- [Riferimento API di GroupDocs.Redaction per Java](https://reference.groupdocs.com/redaction/java/)
- [Download di GroupDocs.Redaction per Java](https://releases.groupdocs.com/redaction/java/)
- [Forum di GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Supporto gratuito](https://forum.groupdocs.com/)
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

---

**Ultimo aggiornamento:** 2026-08-04  
**Testato con:** GroupDocs.Redaction 23.11 per Java  
**Autore:** GroupDocs  

## Domande frequenti
**D: Posso filtrare più colonne contemporaneamente?**  
R: Sì, puoi aggiungere indici di colonna aggiuntivi alla stessa istanza `RedactionFilter` o concatenare più filtri con `filter.or(...)`.

**D: Il filtro funziona su cartelle di lavoro protette da password?**  
R: Fornisci la password quando apri la cartella di lavoro; il filtro opera dopo la decrittazione proprio come su un file non protetto.

**D: Quante righe può gestire l'API in un'unica operazione?**  
R: Il motore è ottimizzato per fino a 1 milione di righe (≈500 MB) senza caricare l'intero file in memoria.

**D: È possibile visualizzare in anteprima quali celle saranno redatte prima di salvare?**  
R: Sì, chiama `filter.preview(workbook)` per ottenere un elenco di indirizzi di celle che corrispondono ai criteri.

**D: Quale modello di licenza è richiesto per l'uso in produzione?**  
R: È necessaria una licenza commerciale completa per le distribuzioni in produzione; una licenza temporanea è sufficiente per test e valutazione.

## Tutorial correlati
- [Come redigere dati sensibili nei fogli di calcolo Excel usando l'API Java di GroupDocs.Redaction](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Mascherare dati sensibili Java – Guida GroupDocs.Redaction](/redaction/java/getting-started/)
- [Mascherare dati sensibili Java – Redigere informazioni personali con GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)