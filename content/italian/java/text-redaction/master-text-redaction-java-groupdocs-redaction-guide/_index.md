---
date: '2026-08-20'
description: Scopri come redigere il testo usando regex in Java con GroupDocs.Redaction.
  Questo tutorial passo‑passo ti mostra come applicare regex, configurare le save
  options e proteggere i dati sensibili.
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: Impara a redigere il testo in Java usando GroupDocs.Redaction. Questa
  guida spiega la redazione con regex, la configurazione delle save‑option e i performance
  tips per proteggere i dati sensibili.
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: Come redigere il testo in Java con GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 'Come redigere il testo in Java con GroupDocs.Redaction: una guida completa'
type: docs
url: /it/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# Come redigere testo in Java con GroupDocs.Redaction: Guida completa

Nel mondo digitale odierno, in rapida evoluzione, **come redigere testo** nei documenti è una domanda che molti sviluppatori si pongono. Che tu stia proteggendo dati personali, rispettando normative, o semplicemente pulendo bozze, questa guida ti accompagna nell'uso di GroupDocs.Redaction per Java per **applicare la redazione basata su regex in modo rapido e sicuro**. Imparerai perché la redazione è importante, come configurare la libreria e consigli pratici per una elaborazione ad alte prestazioni.

## Risposte rapide
- **Qual è lo scopo principale di GroupDocs.Redaction?** Fornisce un'API affidabile per individuare e mascherare testo sensibile in più di 50 formati di documento.  
- **Come applico regex per la redazione?** Crea un oggetto `RegexRedaction` con il tuo pattern e passalo al metodo `Redactor.apply()`.  
- **È necessaria una licenza?** Una prova gratuita è sufficiente per lo sviluppo; una licenza a pagamento sblocca tutte le funzionalità per la produzione.  
- **Posso redigere PDF così come file DOCX?** Sì—GroupDocs.Redaction supporta PDF, DOCX, PPTX e molti altri formati.  
- **Qual è il modo migliore per migliorare le prestazioni?** Chiudi prontamente le istanze di `Redactor`, mantieni i pattern regex semplici e processa i file in batch.

## Che cos'è la redazione del testo e perché è importante?
La redazione del testo rimuove o oscura permanentemente informazioni sensibili da un documento, garantendo che dati riservati—come numeri di previdenza sociale, dettagli di carte di credito o cartelle cliniche—non possano essere recuperati o visualizzati da parti non autorizzate. Funziona sovrascrivendo i caratteri originali o sostituendoli con una maschera, così il contenuto nascosto non può essere estratto tramite copia‑incolla o strumenti OCR. Questo assicura la conformità alle normative sulla privacy e protegge le persone dal furto d'identità o dalle violazioni dei dati.

## Perché usare regex per la redazione del testo?
Le espressioni regolari ti consentono di definire pattern flessibili che corrispondono a una vasta gamma di formati di dati (ad esempio numeri di telefono, numeri di carte di credito). Usare regex con GroupDocs.Redaction ti dà un controllo preciso su ciò che viene nascosto, mantenendo l'implementazione concisa e manutenibile.

## Prerequisiti
Prima di iniziare, assicurati di avere:

- **Java Development Kit (JDK)** installato (Java 8 o versioni successive).  
- Familiarità di base con la sintassi Java e le espressioni regolari.  
- Un IDE come **IntelliJ IDEA** o **Eclipse** per eseguire e fare debug del codice.  

## Configurare GroupDocs.Redaction per Java
Prima, aggiungi la libreria al tuo progetto.

### Configurazione Maven
Se usi Maven, inserisci quanto segue nel tuo `pom.xml`:

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

### Inizializzazione di base
`Redactor` è la classe principale che apre un documento, applica le regole di redazione e scrive l'output.

Una volta che la libreria è disponibile, puoi iniziare a redigere i documenti:

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## Come redigere testo usando regex in Java?
Il processo prevede il caricamento del file sorgente in un'istanza `Redactor`, la creazione di una regola `RegexRedaction` che definisce il pattern da abbinare, l'applicazione della regola con `redactor.apply()` e, infine, il salvataggio del documento modificato usando `SaveOptions`. Seguendo questi passaggi puoi individuare e mascherare in modo affidabile qualsiasi stringa sensibile nei formati supportati.

La classe `Redactor` è il componente centrale che apre un documento, applica le regole di redazione e scrive il file di output. Gestisce le risorse internamente, quindi devi chiuderla dopo l'elaborazione per liberare memoria.

### Passo 1: importare le classi necessarie
Le seguenti importazioni ti danno accesso all'API di redazione:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### Passo 2: inizializzare il redattore e applicare il pattern regex
`RegexRedaction` rappresenta una regola di redazione basata su un pattern di espressione regolare. Il pattern fornito determina quali frammenti di testo vengono sostituiti.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **Spiegazione della regex**: Il pattern `\b\d{3}-\d{2}-\d{4}\b` corrisponde ai numeri di Social Security statunitensi (tre cifre, un trattino, due cifre, un trattino, quattro cifre). `ReplacementOptions` ti permette di scegliere una sovrapposizione nera solida o una maschera di testo personalizzata.

### Passo 3: configurare le opzioni di salvataggio
`SaveOptions` controlla come viene scritto il file redatto. Aggiungere un suffisso rende chiaro quali file sono stati processati, mentre preservare il formato originale evita conversioni indesiderate.

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **Opzioni di salvataggio**: `setAddSuffix(true)` aggiunge automaticamente “_redacted” al nome del file di output, evitando sovrascritture accidentali.

### Passo 4: personalizzare ulteriori impostazioni di salvataggio
Puoi affinare ulteriormente l'output—ad esempio preservando i metadati o appiattendo le annotazioni—regolando l'oggetto `SaveOptions`.

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **Configurazione chiave**: Impostare `setPreserveMetadata(true)` mantiene le proprietà originali del documento, spesso richieste per audit di conformità.

## Applicazioni pratiche
Scenari reali in cui **come redigere testo** è fondamentale:

1. **Documenti legali** – Nascondere gli identificatori dei clienti prima di condividere le bozze con consulenti esterni.  
2. **Cartelle cliniche** – Mascherare nomi dei pazienti, ID o numeri sanitari per rimanere conformi a HIPAA.  
3. **Report finanziari** – Rimuovere numeri di conto confidenziali quando si distribuiscono riepiloghi trimestrali.  

## Considerazioni sulle prestazioni
- **Gestione della memoria**: Chiama sempre `redactor.close()` per rilasciare i handle dei file e le risorse native.  
- **Regex efficiente**: I pattern più semplici sono più veloci; evita back‑tracking eccessivo usando gruppi atomici quando possibile.  
- **Elaborazione in batch**: Per insiemi di documenti di grandi dimensioni, processa i file in batch da 20–50 per mantenere prevedibile l'uso dell'heap.

## Problemi comuni e soluzioni
| Problema | Soluzione |
|----------|-----------|
| **La regex corrisponde a troppo** | Testa il tuo pattern con un tester online di regex e restringi le classi di caratteri. |
| **Conflitto di nome file di output** | Usa `setAddSuffix(true)` o fornisci un percorso di output personalizzato tramite `saveOptions.setOutputPath()`. |
| **Perdita di memoria su PDF di grandi dimensioni** | Processa i PDF pagina per pagina o aumenta la dimensione dell'heap JVM (`-Xmx2g`). |

## Domande frequenti

**D: Qual è lo scopo di `setAddSuffix(true)` in SaveOptions?**  
R: Aggiunge automaticamente un suffisso (ad esempio `_redacted`) al nome del file di output, rendendo evidente quali file sono stati processati.

**D: Posso usare pattern regex diversi dai numeri per la redazione del testo?**  
R: Assolutamente. Qualsiasi espressione regolare Java valida può essere fornita a `RegexRedaction` per mirare a email, numeri di telefono, ID personalizzati, ecc.

**D: Come devo gestire gli errori durante la redazione?**  
R: Avvolgi la logica di redazione in un blocco try‑catch, registra l'eccezione e chiudi sempre il `Redactor` in un finally per rilasciare le risorse.

**D: La redazione dei PDF è supportata?**  
R: Sì. GroupDocs.Redaction funziona con PDF, DOCX, PPTX e molti altri formati.

**D: Quali sono le best practice per progetti di redazione su larga scala?**  
R: Usa l'elaborazione in batch, mantieni i pattern regex semplici e monitora l'uso della memoria con strumenti di profiling.

## Risorse aggiuntive
- **Documentazione**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **Riferimento API**: [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**Ultimo aggiornamento:** 2026-08-20  
**Testato con:** GroupDocs.Redaction 24.9 per Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Mask Sensitive Data Java – GroupDocs.Redaction Guide](/redaction/java/getting-started/)
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [How to Redact PDF with Aspose OCR and Java - Implementing Regex Patterns using GroupDocs.Redaction](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)