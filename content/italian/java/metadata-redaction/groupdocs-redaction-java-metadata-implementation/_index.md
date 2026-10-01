---
date: '2026-10-01'
description: Scopri come rimuovere i metadati dell'autore e salvare i file di documenti
  redatti in Java utilizzando GroupDocs Redaction.
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Scopri come rimuovere i metadati dell'autore e salvare i file di documenti
  redatti in Java utilizzando GroupDocs Redaction. Segui la guida passo‑passo.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: Come rimuovere i metadati dell'autore in Java con GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: Come rimuovere i metadati dell'autore in Java con GroupDocs
type: docs
url: /it/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Come rimuovere i metadati dell'autore in Java con GroupDocs

Nel panorama digitale odierno, proteggere le informazioni sensibili nascoste all'interno dei documenti è una pratica indispensabile. **Rimuovere i metadati dell'autore** previene la divulgazione accidentale di identificatori personali o aziendali. Questo tutorial ti mostra, passo dopo passo, come utilizzare `EraseMetadataRedaction` da GroupDocs.Redaction per Java per eliminare campi come *Author* e *Manager* dai file Word e quindi **salvare copie del documento redatto** in modo sicuro per la condivisione o l'archiviazione.

## Risposte rapide
- **Che cosa fa EraseMetadataRedaction?** Rimuove i campi di metadati selezionati da un documento.  
- **Quale libreria fornisce questa funzionalità?** GroupDocs.Redaction per Java.  
- **Ho bisogno di una licenza?** Una prova gratuita funziona per i test; è necessaria una licenza permanente per la produzione.  
- **Posso mirare a più campi contemporaneamente?** Sì, combina i filtri con un OR logico.  
- **Il processo è thread‑safe?** Le istanze di Redactor non sono condivise tra thread; crea una nuova istanza per ogni operazione.  

## Cos'è EraseMetadataRedaction?
`EraseMetadataRedaction` è una classe di redazione integrata che ti consente di specificare quali voci di metadati devono essere cancellate. Funziona su un'ampia gamma di formati di documento supportati da GroupDocs.Redaction, garantendo che le informazioni di authoring nascoste non trapelino mai. Puoi mirare a proprietà standard come Author, Manager e anche a campi di metadati personalizzati, fornendo una protezione della privacy completa.

## Perché usare EraseMetadataRedaction con GroupDocs?
GroupDocs.Redaction supporta **oltre 100 formati di input e output** e può elaborare documenti fino a 500 pagine senza caricare l'intero file in memoria. Utilizzare questa classe ti offre un'unica API ad alte prestazioni per soddisfare i requisiti di GDPR, HIPAA o conformità interna, mantenendo il tuo codice semplice.

## Prerequisiti
- Java 8 o superiore installato.  
- Maven (o la possibilità di aggiungere JAR manualmente).  
- GroupDocs.Redaction per Java (versione 24.9 o successiva).  
- Una licenza di prova o permanente valida di GroupDocs.  

## Configurazione di GroupDocs.Redaction per Java

### Installazione Maven
Aggiungi il repository GroupDocs e la dipendenza al tuo **pom.xml**:

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

### Download diretto
In alternativa, scarica l'ultimo JAR da [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisizione della licenza
Ottieni una prova gratuita o acquista una licenza temporanea dal portale GroupDocs. Il file di licenza deve essere posizionato dove la tua applicazione può caricarlo (ad esempio, nella radice del classpath).

### Inizializzazione e configurazione di base
Di seguito è un esempio minimale che crea un'istanza `Redactor` per un file DOCX:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Come usare EraseMetadataRedaction in Java
Le sezioni seguenti suddividono l'implementazione in passaggi chiari e azionabili.

### Funzionalità: pulire elementi di metadati specifici

#### Panoramica
Cancelleremo i campi di metadati **Author** e **Manager** usando `EraseMetadataRedaction`. Questa è una necessità comune quando si condividono report interni con partner esterni.

#### Implementazione passo‑a‑passo

##### 1️⃣ Inizializza l'oggetto Redactor
`Redactor` è la classe principale che carica un documento, applica oggetti di redazione e scrive il risultato. Crea una nuova istanza per ogni file che elabori:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ Applica EraseMetadataRedaction
`MetadataFilters` fornisce filtri predefiniti per chiavi di metadati comuni come Author e Manager.  
`EraseMetadataRedaction` rimuove le voci di metadati che corrispondono ai `MetadataFilters` forniti. L'OR bitwise (`|`) combina i filtri `Author` e `Manager` così entrambi i campi vengono rimossi in una singola chiamata:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ Configura le opzioni di salvataggio
`SaveOptions` ti consente di specificare il nome del file di output, il formato e altri parametri di salvataggio.  
`SaveOptions` ti permette di controllare il nome del file di output, il formato e se il documento deve essere rasterizzato in PDF. Aggiungere un suffisso mantiene intatto il file originale:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## Casi d'uso comuni
1. **Documenti legali** – Redigere le informazioni sull'autore prima di inviare i contratti alla controparte legale.  
2. **Report aziendali** – Rimuovere i nomi dei manager quando si pubblicano i risultati trimestrali agli azionisti.  
3. **File di progetto** – Pulire la documentazione interna del progetto prima di archiviarla o caricarla in un repository pubblico.  

## Suggerimenti per la risoluzione dei problemi
- **File non trovato** – Verifica che il percorso in `inputFilePath` punti a un file esistente e che l'applicazione abbia i permessi di lettura.  
- **Campi di metadati mancanti** – Non tutti i tipi di documento memorizzano le stesse chiavi di metadati; controlla prima le proprietà del documento in Office.  
- **Errori di licenza** – Assicurati che il file di licenza sia caricato correttamente prima di creare l'istanza `Redactor`.  

## Considerazioni sulle prestazioni
- Chiudi l'oggetto `Redactor` prontamente (come mostrato nel blocco `finally`) per liberare le risorse native.  
- Evita di rasterizzare documenti di grandi dimensioni a meno che non ti serva un'anteprima PDF; la rasterizzazione può aumentare l'uso di CPU e memoria fino a 3× per file di 300 pagine.  

## Domande frequenti

**Q1: Cos'è la redazione dei metadati?**  
A1: La redazione dei metadati consiste nel rimuovere le proprietà nascoste del documento (come autore, manager o tag personalizzati) per prevenire la divulgazione accidentale di informazioni sensibili.

**Q2: Posso usare GroupDocs.Redaction per altri tipi di file?**  
A2: Sì, la libreria supporta PDF, DOCX, PPTX, XLSX e molti altri formati—oltre 100 in totale.

**Q3: Come gestisco gli errori durante la redazione?**  
A3: Avvolgi la chiamata `apply` in un blocco try‑catch e chiudi sempre il `Redactor` in una clausola finally per garantire il rilascio delle risorse.

**Q4: È possibile redigere campi di metadati personalizzati?**  
A5: Assolutamente. Usa `MetadataFilters.Custom("YourFieldName")` per mirare a qualsiasi proprietà personalizzata memorizzata nel documento.

**Q5: Quali sono le migliori pratiche per l'uso di GroupDocs.Redaction?**  
A5:  
- Carica la licenza all'inizio della tua applicazione.  
- Chiudi prontamente gli oggetti `Redactor`.  
- Usa `SaveOptions` per aggiungere un suffisso, mantenendo intatti i file originali.  
- Testa la redazione su una copia del documento prima di elaborare i batch.

**Q6: EraseMetadataRedaction supporta operazioni batch?**  
A6: Puoi iterare su una collezione di percorsi file, creando un nuovo `Redactor` per ogni file e applicando la stessa logica di redazione.

**Q7: Posso combinare EraseMetadataRedaction con altri tipi di redazione?**  
A7: Sì, puoi concatenare più oggetti di redazione (ad esempio, redazione del testo seguita da redazione dei metadati) prima di salvare.

## Risorse

- **Documentazione**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **Riferimento API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Supporto gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Licenza temporanea**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Ultimo aggiornamento:** 2026-10-01  
**Testato con:** GroupDocs.Redaction 24.9 for Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Estrazione dei metadati del documento Java con Groupdocs Redaction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [Come rimuovere i metadati in Java usando GroupDocs.Redaction](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [Recuperare le informazioni del documento usando Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)