---
date: '2026-08-20'
description: Impara a oscurare il testo con GroupDocs.Redaction Java, salvare come
  PDF rasterizzato, sostituire frasi esatte e applicare impostazioni PDF personalizzate.
keywords:
- how to redact text
- save pdf as image
- convert pdf to image
lastmod: '2026-08-20'
og_description: Come oscurare il testo con GroupDocs.Redaction Java. Questa guida
  mostra la sostituzione di frasi esatte, la creazione di PDF rasterizzati e la conformità
  PDF/A‑1a in pochi passaggi.
og_image_alt: Guide showing GroupDocs.Redaction Java code to redact text and create
  rasterized PDF
og_title: Come oscurare il testo con la libreria GroupDocs.Redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  headline: How to redact text with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  name: How to redact text with GroupDocs.Redaction Java
  steps:
  - name: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
    text: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
  - name: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
    text: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
  - name: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
    text: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
  type: HowTo
- questions:
  - answer: Add the GroupDocs repository and the `groupdocs-redaction` dependency
      to your `pom.xml` as shown in the Maven Setup section.
    question: How do I install GroupDocs.Redaction in a Maven project?
  - answer: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.
    question: Can I redact text from PDF files using this library?
  - answer: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s
      spelling and case sensitivity.
    question: What happens if the exact phrase isn’t found?
  - answer: Process them in smaller page ranges, enable rasterization only where needed,
      and always close the `Redactor` to free resources.
    question: How can I handle very large documents efficiently?
  - answer: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()`
      to target the exact pages you want to rasterize.
    question: Is it possible to save rasterized PDFs with specific page ranges?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java PDF processing
title: Come oscurare il testo con GroupDocs.Redaction Java
type: docs
url: /it/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# Come redigere testo con GroupDocs.Redaction Java

In applicazioni moderne, **come redigere testo** in un documento mantenendo il flusso di lavoro veloce e conforme è una sfida frequente per sviluppatori, revisori e responsabili della conformità. Questo tutorial ti guida nell'uso di GroupDocs.Redaction per Java per individuare frasi esatte, sostituirle con sovrapposizioni sicure e infine esportare il risultato come documento PDF/A‑1a rasterizzato—perfetto per l'archiviazione o la distribuzione legale.

## Risposte rapide
- **Qual è la classe principale per la redazione?** `Redactor`  
- **Posso sostituire una frase con una sovrapposizione colorata?** Sì, usando `ExactPhraseRedaction` e `ReplacementOptions`.  
- **Come genero un PDF rasterizzato?** Abilita la rasterizzazione tramite `SaveOptions.getRasterization().setEnabled(true)`.  
- **Quale livello di conformità PDF è usato nell'esempio?** `PdfComplianceLevel.PdfA1a`.  
- **È necessaria una licenza per l'uso in produzione?** È richiesta una licenza valida di GroupDocs.Redaction per le distribuzioni in produzione.

## Cos'è “come redigere testo” in Java?
`Redaction` è la rimozione permanente o l'oscuramento di contenuti sensibili da un file in modo che non possano essere recuperati o letti in seguito. Con GroupDocs.Redaction puoi cercare programmaticamente una frase esatta—ad esempio un numero di previdenza sociale o un codice di progetto riservato—e sostituirla con una sovrapposizione rossa, una casella nera o qualsiasi elemento visivo personalizzato, garantendo che i dati originali siano irrecuperabili.

## Perché usare GroupDocs.Redaction per Java?
GroupDocs.Redaction supporta **30+ formati di input e output** (PDF, DOCX, PPTX, XLSX, HTML e tipi di immagine) e può elaborare documenti di centinaia di pagine senza caricare l'intero file in memoria. Il suo algoritmo di corrispondenza di frasi esatte riduce i falsi positivi di > 95 % rispetto alle ricerche generiche di parole chiave, e il motore di rasterizzazione integrato ti consente di produrre file PDF/A‑1a completamente basati su immagini per la conservazione a lungo termine.

## Prerequisiti
- **GroupDocs.Redaction per Java** (v24.9 o più recente).  
- **Java Development Kit (JDK) 8+**.  
- Un IDE come IntelliJ IDEA, Eclipse o NetBeans.  
- Maven per la gestione delle dipendenze.  

### Librerie e dipendenze richieste
- GroupDocs.Redaction per Java – aggiungi il repository e la dipendenza al tuo `pom.xml` (vedi la sezione di configurazione Maven).  
- Facoltativo: qualsiasi framework di logging preferisci (SLF4J, Log4j, ecc.).

### Prerequisiti di conoscenza
- Sintassi Java di base e I/O di file.  
- Familiarità con la struttura `pom.xml` di Maven.

## Configurare GroupDocs.Redaction per Java
### Configurazione Maven
Aggiungi il repository GroupDocs e la dipendenza `groupdocs-redaction` al tuo file `pom.xml`:

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
In alternativa, puoi scaricare l'ultima versione direttamente da [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisizione della licenza
- **Prova gratuita** – esplora l'API senza chiave di licenza.  
- **Licenza temporanea** – usa per una valutazione estesa.  
- **Licenza completa** – richiesta per ambienti di produzione.

### Inizializzazione e configurazione di base
La classe `Redactor` è il punto di ingresso per tutte le operazioni di redazione. Carica un documento, applica le regole di redazione e salva il risultato.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## Come redigere testo – esempio di frase esatta
`Redactor` è la classe principale che carica un documento e applica le regole di redazione. `ExactPhraseRedaction` definisce una regola che corrisponde a una stringa specifica. Questo esempio dimostra come caricare un file, creare una regola `ExactPhraseRedaction` ed eseguire la redazione in un unico passaggio, fornendo un flusso di lavoro conciso per gli sviluppatori garantendo che il contenuto originale sia permanentemente oscurato.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

## Come salvare come PDF rasterizzato
`SaveOptions` è l'oggetto di configurazione che controlla come un documento viene salvato. Abilitando la sua funzionalità di rasterizzazione e selezionando la conformità PDF/A‑1a, puoi produrre un PDF solo immagine in cui ogni pagina è renderizzata come bitmap, soddisfacendo gli standard di archiviazione e impedendo l'estrazione del testo.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

## Applicazioni pratiche
1. **Redazione di dati sensibili** – nascondi automaticamente gli identificatori personali prima di condividere i contratti.  
2. **Archiviazione di documenti** – converti i report finalizzati in PDF/A rasterizzato per la conformità a lungo termine.  
3. **Aggiornamento massivo dei contenuti** – sostituisci la terminologia obsoleta in centinaia di file con un unico script.

## Considerazioni sulle prestazioni
- **Chiudi il `Redactor`** dopo ogni operazione per rilasciare i handle dei file e la memoria.  
- **Elaborazione batch** – carica un elenco di file e iterali, riutilizzando una singola istanza di `Redactor` quando possibile.  
- **Monitora le risorse** – usa strumenti di profilazione Java per osservare l'uso della CPU e dell'heap durante redazioni su larga scala.

## Domande frequenti

**Q: Come installo GroupDocs.Redaction in un progetto Maven?**  
A: Aggiungi il repository GroupDocs e la dipendenza `groupdocs-redaction` al tuo `pom.xml` come mostrato nella sezione Configurazione Maven.

**Q: Posso redigere testo da file PDF usando questa libreria?**  
A: Sì, GroupDocs.Redaction supporta PDF, DOCX, PPTX e molti altri formati.

**Q: Cosa succede se la frase esatta non viene trovata?**  
A: Il `RedactorChangeLog` restituirà uno stato `Failed`. Verifica l'ortografia e la sensibilità al maiuscolo/minuscolo della frase.

**Q: Come posso gestire documenti molto grandi in modo efficiente?**  
A: Elaborali in intervalli di pagine più piccoli, abilita la rasterizzazione solo dove necessario e chiudi sempre il `Redactor` per liberare le risorse.

**Q: È possibile salvare PDF rasterizzati con intervalli di pagine specifici?**  
A: Assolutamente. Usa `options.getRasterization().setPageIndex()` e `setPageCount()` per mirare alle pagine esatte che desideri rasterizzare.

## Conclusione
Ora hai una guida completa, end‑to‑end, su **come redigere testo** con GroupDocs.Redaction Java e **salvare come PDF rasterizzato**. Seguendo questi passaggi, puoi proteggere le informazioni sensibili, soddisfare rigorosi standard di conformità e mantenere le tue applicazioni Java performanti su larga scala.

**Passi successivi**  
- Approfondisci l'API esplorando la [documentazione ufficiale](https://docs.groupdocs.com/redaction/java/).  
- Sperimenta con altri tipi di redazione come `RegexRedaction` e `ImageRedaction`.  
- Unisciti alla community sul [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) per suggerimenti e best practice.

---

**Last Updated:** 2026-08-20  
**Tested With:** GroupDocs.Redaction Java 24.9  
**Author:** GroupDocs

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

## Tutorial correlati

- [Come redigere testo con GroupDocs.Redaction per Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Tutorial di redazione testo Java: Guida con GroupDocs.Redaction](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)