---
date: '2026-09-26'
description: Scopri come rimuovere i metadati con GroupDocs in Java, eliminando in
  modo sicuro i metadati riservati dei documenti mantenendo intatto il formato originale.
keywords:
- how to redact metadata
- GroupDocs Redaction Java
- secure document processing
- metadata removal Java
lastmod: '2026-09-26'
og_description: Come rimuovere i metadati con GroupDocs in Java – una guida passo‑passo
  che ti mostra come eliminare in modo sicuro i metadati riservati dei documenti e
  mantenere il formato originale.
og_image_alt: Guide showing metadata redaction using GroupDocs in Java
og_title: Come rimuovere i metadati con GroupDocs in Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  headline: How to redact metadata with GroupDocs in Java
  type: TechArticle
- description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  name: How to redact metadata with GroupDocs in Java
  steps:
  - name: import necessary classes
    text: These imports give you access to the redaction engine, save options, and
      metadata utilities.
  - name: initialize redactor
    text: Instantiate the `Redactor` with the path to your source file.
  - name: configure metadata search and redaction
    text: Create a `MetadataSearchRedaction` that looks for the exact string **"Company
      Ltd."** and replaces it with **"--company--"**. The `setFilter` call limits
      the operation to the *Company* metadata field only.
  - name: apply the redaction
    text: Run the redaction against the opened document.
  - name: save with custom options
    text: '`SaveOptions` allows you to specify output format, file naming, and other
      saving parameters for the redacted document. Configure `SaveOptions` so the
      redacted file gets a “_Redacted” suffix while preserving its original format.'
  - name: release resources
    text: Always close the `Redactor` to free native resources and avoid memory leaks.
  type: HowTo
- questions:
  - answer: It’s a powerful library that enables you to redact text, metadata, and
      images in documents using Java applications.
    question: What is GroupDocs.Redaction for Java?
  - answer: Yes, but with limitations. A free trial or temporary license allows full
      access for testing purposes.
    question: Can I use GroupDocs.Redaction without purchasing a license?
  - answer: Use `SaveOptions` to specify your requirements, such as avoiding rasterization
      when saving to PDF.
    question: How do I ensure document formats are preserved during redaction?
  - answer: It supports a wide range, including Word, Excel, PowerPoint, PDF, and
      many more.
    question: What types of documents can be redacted using GroupDocs.Redaction?
  - answer: Visit the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for assistance.
    question: Where can I find support if I run into issues?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document security
- redaction tutorial
title: Come rimuovere i metadati con GroupDocs in Java
type: docs
url: /it/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# Come redigere i metadati con GroupDocs in Java

In questo tutorial completo imparerai **come redigere i metadati** da Word, PDF e molti altri tipi di documento usando GroupDocs.Redaction per Java. Alla fine della guida sarai in grado di incorporare la redazione dei metadati in qualsiasi servizio basato su Java, garantendo che informazioni riservate come nomi di azienda, autori o proprietà personalizzate non escano mai dalla tua organizzazione.

## Risposte rapide
- **Cosa fa MetadataSearchRedaction?** Cerca campi di metadati specifici e sostituisce i loro valori con testo personalizzato.  
- **Quale libreria è necessaria?** GroupDocs.Redaction for Java (v24.9 o successiva).  
- **È necessaria una licenza?** Una prova gratuita funziona per la valutazione; è necessaria una licenza completa per la produzione.  
- **Posso mantenere il formato originale del file?** Sì—usa `SaveOptions` per preservare il formato originale.  
- **Questo approccio è thread‑safe?** Ogni istanza di `Redactor` è indipendente, quindi puoi elaborare i documenti in parallelo.

## Come redigere i metadati con GroupDocs?
`Redactor` è la classe principale che carica un documento e fornisce operazioni di redazione.  
Carica il tuo documento sorgente con un'istanza di `Redactor`, configura un `MetadataSearchRedaction` che mira alla chiave di metadati esatta che desideri pulire, applica la redazione e infine salva il file usando `SaveOptions`. L'intero flusso di lavoro può essere espresso in poche righe e funziona per qualsiasi formato supportato, da DOCX a PDF e oltre.

## Cos'è la redazione dei metadati con GroupDocs?
`MetadataSearchRedaction` è una classe specializzata che ti consente di mirare a una proprietà di metadati specifica (ad es., *Company*, *Author*) e sostituirne il contenuto con un segnaposto. È ideale quando è necessario anonimizzare i dati aziendali prima di condividere i documenti con partner esterni. Il processo di redazione non altera gli altri elementi del documento, garantendo che il layout visivo e il contenuto rimangano intatti dopo la rimozione dei metadati.

## Perché usare la redazione dei metadati con GroupDocs?
La redazione dei metadati con GroupDocs offre un modo affidabile per rimuovere informazioni sensibili dai documenti preservando al contempo l'aspetto e la struttura originali. Concentrandoti sui campi dei metadati, puoi rapidamente rispettare gli standard di privacy senza modificare il contenuto visibile o rischiare perdite accidentali di dati.

- **Precisione** – Redigi solo i campi che specifichi, lasciando il resto del documento intatto.  
- **Conformità** – Aiuta a soddisfare GDPR, HIPAA e altre normative sulla privacy rimuovendo gli identificatori nascosti.  
- **Pronto per l'automazione** – Si integra perfettamente nei pipeline di elaborazione batch o nei micro‑servizi.  
- **Ampio supporto di formati** – GroupDocs.Redaction supporta **50+ formati di input e output** (inclusi DOCX, PDF, PPTX, XLSX e tipi di immagine) e può elaborare file di centinaia di pagine senza caricare l'intero documento in memoria.

## Prerequisiti
- **GroupDocs.Redaction for Java** ≥ 24.9.  
- Java 8 o successiva installata sulla tua macchina.  
- Un IDE come IntelliJ IDEA o Eclipse (opzionale ma consigliato).  
- Familiarità di base con Maven (o capacità di aggiungere JAR manualmente).  

## Configurazione di GroupDocs.Redaction per Java

Aggiungi il repository e la dipendenza al tuo `pom.xml`. Questo passaggio garantisce che Maven possa scaricare automaticamente la libreria.

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

*In alternativa, puoi scaricare il JAR direttamente dalla pagina di rilascio ufficiale:*  
[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)

### Acquisizione della licenza
- **Prova gratuita** – Scarica una licenza di prova per esplorare tutte le funzionalità.  
- **Licenza temporanea** – Usa per test estesi.  
- **Licenza completa** – Necessaria per le distribuzioni in produzione.

## Inizializzazione di base
`Redactor` carica un documento e espone metodi per applicare varie redazioni.  
Crea un'istanza di `Redactor` che punti al documento che desideri elaborare.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Guida all'implementazione

### Passo 1: importare le classi necessarie
Questi import ti danno accesso al motore di redazione, alle opzioni di salvataggio e alle utility dei metadati.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### Passo 2: inizializzare il redactor
Istanzia il `Redactor` con il percorso del tuo file sorgente.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### Passo 3: configurare la ricerca e la redazione dei metadati
Crea un `MetadataSearchRedaction` che cerca la stringa esatta **"Company Ltd."** e la sostituisce con **"--company--"**. La chiamata `setFilter` limita l'operazione solo al campo di metadati *Company*.

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### Passo 4: applicare la redazione
Esegui la redazione sul documento aperto.

```java
redactor.apply(redaction);
```

### Passo 5: salvare con opzioni personalizzate
`SaveOptions` ti consente di specificare il formato di output, la denominazione del file e altri parametri di salvataggio per il documento redatto.  
Configura `SaveOptions` in modo che il file redatto ottenga il suffisso “_Redacted” mantenendo il suo formato originale.

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### Passo 6: rilasciare le risorse
Chiudi sempre il `Redactor` per liberare le risorse native ed evitare perdite di memoria.

```java
finally {
    redactor.close();
}
```

## Problemi comuni e soluzioni
- **FileNotFoundException** – Verifica nuovamente il percorso che passi a `Redactor`. Usa percorsi assoluti o `Paths.get(...)` per maggiore affidabilità.  
- **Nessuna modifica osservata** – Verifica che il campo di metadati che stai mirando contenga effettivamente la stringa di ricerca; i metadati sono sensibili al maiuscolo/minuscolo per impostazione predefinita.  
- **Errori di out‑of‑memory su file di grandi dimensioni** – Elabora i documenti in batch più piccoli e chiama `redactor.close()` prontamente dopo ogni file.

## Applicazioni pratiche
1. **Documentazione legale** – Rimuovi i nomi delle aziende clienti prima di inviare i contratti a terze parti.  
2. **Report finanziari** – Anonimizza gli identificatori interni nei file di audit.  
3. **Progetti collaborativi** – Proteggi le informazioni proprietarie quando condividi bozze con fornitori esterni.

## Considerazioni sulle prestazioni
- **Gestione della memoria** – La libreria mantiene l'intero documento in memoria; chiudere il `Redactor` dopo ogni file è essenziale.  
- **Elaborazione batch** – Per scenari ad alto volume, itera su una collezione di file e riutilizza una singola istanza di `SaveOptions`.  
- **Rimani aggiornato** – Le nuove versioni introducono ottimizzazioni delle prestazioni e correzioni di bug; punta sempre all'ultima versione stabile.

## Domande frequenti

**Q: Cos'è GroupDocs.Redaction per Java?**  
A: È una potente libreria che consente di redigere testo, metadati e immagini nei documenti usando applicazioni Java.

**Q: Posso usare GroupDocs.Redaction senza acquistare una licenza?**  
A: Sì, ma con limitazioni. Una prova gratuita o una licenza temporanea consentono l'accesso completo per scopi di test.

**Q: Come posso garantire che i formati dei documenti siano preservati durante la redazione?**  
A: Usa `SaveOptions` per specificare i tuoi requisiti, ad esempio evitando la rasterizzazione quando salvi in PDF.

**Q: Quali tipi di documenti possono essere redatti usando GroupDocs.Redaction?**  
A: Supporta un'ampia gamma, inclusi Word, Excel, PowerPoint, PDF e molti altri.

**Q: Dove posso trovare supporto se incontro problemi?**  
A: Visita il [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) per assistenza.

**Q: MetadataSearchRedaction funziona con documenti crittografati?**  
A: Sì. Carica il documento con la password appropriata usando il costruttore `Redactor` che accetta un parametro password.

**Q: Posso concatenare più redazioni di metadati in un'unica esecuzione?**  
A: Assolutamente. Crea più oggetti `MetadataSearchRedaction`, imposta filtri diversi e applicali in sequenza prima di salvare.

**Q: È possibile visualizzare in anteprima le redazioni prima di salvare?**  
A: Puoi chiamare `redactor.getRedactions()` per recuperare un elenco di redazioni in sospeso e ispezionarle programmaticamente.

## Risorse aggiuntive
- **Documentazione**: Esplora guide dettagliate su [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **Riferimento API**: Consulta il riferimento completo dell'API su [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Scarica la libreria**: Accedi all'ultima versione su [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **Codice sorgente**: Visualizza e contribuisci su [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).  
- **Supporto**: Ottieni aiuto tramite il canale di supporto gratuito su [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33).

---

**Ultimo aggiornamento:** 2026-09-26  
**Testato con:** GroupDocs.Redaction 24.9 per Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Estrazione dei metadati del documento Java con Groupdocs Redaction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [sostituire testo dei metadati java – Redazione sicura con GroupDocs](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [Recuperare le informazioni del documento usando Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)