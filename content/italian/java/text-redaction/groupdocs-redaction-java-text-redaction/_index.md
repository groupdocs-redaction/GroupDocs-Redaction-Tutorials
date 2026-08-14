---
date: '2026-08-14'
description: Come redigere il testo nei documenti Java usando GroupDocs.Redaction
  – mascherare le informazioni personali e sostituire il testo sensibile in modo efficiente.
keywords:
- how to redact text
- GroupDocs Redaction Java
- text redaction Java
- mask personal information
lastmod: '2026-08-14'
og_description: Come redigere il testo con GroupDocs.Redaction per Java consente di
  mascherare permanentemente i dati personali e sostituire le stringhe sensibili su
  PDF, DOCX e altri formati, garantendo la conformità a GDPR e HIPAA.
og_image_alt: 'Guide: redact text in Java using GroupDocs.Redaction library'
og_title: Come redigere il testo con GroupDocs.Redaction per Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  headline: How to redact text with GroupDocs.Redaction for Java
  type: TechArticle
- description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  name: How to redact text with GroupDocs.Redaction for Java
  steps:
  - name: initialize the redactor
    text: '`Redactor` is the core class that loads a document, applies redaction rules,
      and writes the output.'
  - name: apply exact‑phrase redaction
    text: '`ExactPhraseRedaction` searches for an exact string match, while `ReplacementOptions`
      defines how the matched text should be replaced. - **Parameters:** - `"John
      Doe"` – the exact text to be redacted. - `ReplacementOptions("[personal]")`
      – the string that will replace the original content, effective'
  - name: save the redacted document
    text: '`Redactor.save` writes the modified document to a new file or overwrites
      the original, preserving the original format.'
  - name: clean up resources
    text: Always call `Redactor.close()` to release native resources and avoid memory
      leaks.
  type: HowTo
- questions:
  - answer: Yes, the library supports PDF, DOCX, XLSX, PPTX, and many other formats.
    question: Can I redact text from PDFs using GroupDocs.Redaction?
  - answer: No. Redactions permanently remove the original content, so keep a backup
      of the source file.
    question: Is a redaction reversible?
  - answer: Process them in chunks, use batch mode, and monitor memory usage with
      profiling tools.
    question: How do I handle very large documents efficiently?
  - answer: Besides DOCX and PDF, you can redact TXT, RTF, XLSX, PPTX, and more.
    question: What other text formats are supported?
  - answer: Absolutely. The API can be called from web services, background jobs,
      or CI/CD pipelines.
    question: Can I integrate GroupDocs.Redaction into existing workflows?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- privacy compliance
- redaction API
title: Come redigere il testo con GroupDocs.Redaction per Java
type: docs
url: /it/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# Come redigere testo con GroupDocs.Redaction per Java

In questo tutorial imparerai **come redigere testo** nei documenti basati su Java usando GroupDocs.Redaction. Vedrai come mascherare le informazioni personali, sostituire le stringhe sensibili con segnaposto sicuri e elaborare più file in modo compatibile con il batch. Alla fine avrai una soluzione pronta per la produzione che protegge la privacy, soddisfa i requisiti GDPR/HIPAA e si integra senza problemi nelle applicazioni Java esistenti.

## Risposte rapide
- **Quale libreria è usata?** GroupDocs.Redaction per Java.  
- **Posso mascherare le informazioni personali?** Sì – usa la redazione a frase esatta con opzioni di sostituzione.  
- **È supportata l'elaborazione batch?** Assolutamente, è possibile iterare su più file con la stessa istanza di Redactor.  
- **È necessaria una licenza?** Una prova gratuita funziona per la valutazione; è richiesta una licenza commerciale per la produzione.  
- **Quale versione di Java è richiesta?** JDK 8 o superiore.

## Che cos'è “come redigere testo”?
La redazione rimuove o oscura permanentemente i dati riservati da un documento. Con GroupDocs.Redaction è possibile individuare stringhe specifiche, sostituirle con segnaposto sicuri e salvare il file sanificato—tutto senza modifiche manuali.

## Perché usare GroupDocs.Redaction per Java?
GroupDocs.Redaction per Java supporta **oltre 50 formati di input e output** (inclusi PDF, DOCX, XLSX, PPTX, TXT, RTF) e può elaborare file di centinaia di pagine senza caricare l'intero documento in memoria, offrendo operazioni batch ad alta velocità su hardware server standard.

## Prerequisiti
- **Java Development Kit (JDK):** Version 8 o successiva.  
- **IDE:** IntelliJ IDEA, Eclipse o qualsiasi editor compatibile con Java.  
- **Maven:** Per la gestione delle dipendenze.  
- **Conoscenza di base di Java:** Familiarità con classi, metodi e gestione delle eccezioni.

## Configurare GroupDocs.Redaction per Java
Per iniziare, aggiungi la libreria al tuo progetto Maven.

### Configurazione Maven
Add the repository and dependency to your `pom.xml` file:

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
Se preferisci, scarica l'ultimo JAR da [GroupDocs Redaction Java Releases](https://releases.groupdocs.com/redaction/java/).

### Acquisizione licenza
Puoi iniziare con una **Free Trial**, richiedere una **Temporary License** per test estesi, o acquistare una **Commercial License** per l'uso in produzione.

## Come redigere testo nei documenti con GroupDocs.Redaction
Le sezioni seguenti ti guidano attraverso i passaggi esatti necessari per **mascherare le informazioni personali** e **sostituire il testo sensibile**.

### Passo 1: inizializzare il redattore
`Redactor` è la classe principale che carica un documento, applica le regole di redazione e scrive l'output.  

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### Passo 2: applicare la redazione a frase esatta
`ExactPhraseRedaction` cerca una corrispondenza esatta di stringa, mentre `ReplacementOptions` definisce come il testo corrispondente deve essere sostituito.

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **Parametri:**  
  - `"John Doe"` – il testo esatto da redigere.  
  - `ReplacementOptions("[personal]")` – la stringa che sostituirà il contenuto originale, mascherando efficacemente le **informazioni personali**.

### Passo 3: salvare il documento redatto
`Redactor.save` scrive il documento modificato in un nuovo file o sovrascrive l'originale, preservando il formato originale.

```java
redactor.save();
```

### Passo 4: pulire le risorse
Chiama sempre `Redactor.close()` per rilasciare le risorse native ed evitare perdite di memoria.

```java
finally {
    redactor.close();
}
```

## Come mascherare le informazioni personali con un callback personalizzato
Un callback personalizzato ti consente di reagire a ciascun evento di redazione—utile per il logging, sostituzioni condizionali o tracciamenti di audit.

### Creare una classe di callback
`IRedactionCallback` definisce i metodi che vengono invocati prima e dopo ogni operazione di redazione.

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### Utilizzare il callback durante l'istanziazione di Redactor
Passa la tua implementazione del callback tramite `RedactorSettings` affinché il motore sappia di invocarlo durante l'elaborazione.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## Applicazioni pratiche
- **Contratti legali:** Nascondi automaticamente i nomi dei clienti, i SSN o le clausole riservate prima di condividere le bozze.  
- **Cartelle cliniche:** **Mascherare le informazioni personali** come gli identificatori dei pazienti quando si esportano i record a partner di ricerca.  
- **Comunicazioni aziendali:** **Sostituire il testo sensibile** come i codici di progetto interni prima della distribuzione esterna, garantendo l'assenza di perdite accidentali.

## Considerazioni sulle prestazioni
Durante l'elaborazione di file grandi o numerosi, tieni presente questi consigli:

- **Elaborazione batch:** Itera su una collezione di file per ridurre l'overhead di avvio.  
- **Gestione della memoria:** Rilascia il `Redactor` dopo ogni file; evita di tenere molti documenti in memoria contemporaneamente.  
- **Profilazione:** Usa profiler Java (ad esempio VisualVM) per individuare colli di bottiglia in I/O o nella logica di redazione.

## Domande frequenti
**Q: Posso redigere testo da PDF usando GroupDocs.Redaction?**  
A: Sì, la libreria supporta PDF, DOCX, XLSX, PPTX e molti altri formati.

**Q: Una redazione è reversibile?**  
A: No. Le redazioni rimuovono permanentemente il contenuto originale, quindi conserva un backup del file sorgente.

**Q: Come gestire documenti molto grandi in modo efficiente?**  
A: Elaborali a blocchi, usa la modalità batch e monitora l'uso della memoria con strumenti di profilazione.

**Q: Quali altri formati di testo sono supportati?**  
A: Oltre a DOCX e PDF, è possibile redigere TXT, RTF, XLSX, PPTX e altri.

**Q: Posso integrare GroupDocs.Redaction nei flussi di lavoro esistenti?**  
A: Assolutamente. L'API può essere chiamata da servizi web, job in background o pipeline CI/CD.

## Risorse
- **Documentazione:** [Documentazione GroupDocs Redaction Java](https://docs.groupdocs.com/redaction/java/)  
- **Riferimento API:** [Riferimento API GroupDocs per Java](https://reference.groupdocs.com/redaction/java)  
- **Download:** [Download GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)  
- **Repository GitHub:** [Repository GitHub GroupDocs Redaction](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Forum di supporto gratuito GroupDocs:** [Forum di supporto gratuito GroupDocs](https://forum.groupdocs.com/c/redaction/33)  
- **Richiedi una licenza temporanea:** [Richiedi una licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

---

**Ultimo aggiornamento:** 2026-08-14  
**Testato con:** GroupDocs.Redaction 24.9 per Java  
**Autore:** GroupDocs

## Tutorial correlati
- [Mascherare dati sensibili Java – Guida GroupDocs.Redaction](/redaction/java/getting-started/)
- [Mascherare dati sensibili Java – Redigere informazioni personali con GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Modificare documenti protetti da password Java - Redigere documenti usando GroupDocs.Redaction](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)