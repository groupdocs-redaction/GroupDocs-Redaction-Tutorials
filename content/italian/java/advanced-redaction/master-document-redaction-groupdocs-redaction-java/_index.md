---
date: '2025-12-17'
description: Scopri come aggiungere un suffisso al nome file e redigere le informazioni
  sensibili dai documenti usando GroupDocs.Redaction per Java. Migliora efficacemente
  la sicurezza e la privacy dei documenti.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Come aggiungere un suffisso al nome file durante la redazione dei documenti
  in Java con GroupDocs.Redaction
type: docs
url: /it/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Come aggiungere un suffisso al nome file durante la redazione di documenti in Java con GroupDocs.Redaction

Redigere dati riservati è solo metà della battaglia—devi anche assicurarti che il file salvato indichi chiaramente di essere stato elaborato. In questa guida imparerai **come aggiungere un suffisso al nome file** durante il salvataggio di un documento redatto, oltre a caricare, annotare e salvare usando GroupDocs.Redaction per Java. Che tu stia proteggendo contratti legali, cartelle cliniche o report finanziari, questi passaggi manterranno il tuo flusso di lavoro sicuro e verificabile.

## Risposte rapide
- **Cosa fa “add suffix to filename”?**  
  Aggiunge un suffisso personalizzato (ad es., “_redacted”) al nome del file di output così puoi identificare immediatamente i file elaborati.  
- **Posso caricare un documento dallo stream?**  
  Sì—GroupDocs.Redaction supporta il caricamento da qualsiasi `InputStream`, perfetto per l'archiviazione cloud o l'elaborazione in‑memoria.  
- **È necessaria una licenza per questa funzionalità?**  
  Una prova gratuita funziona per la redazione di base; una licenza temporanea o completa sblocca tutte le opzioni avanzate, incluso la gestione del suffisso.  
- **Quali formati sono supportati?**  
  La libreria gestisce DOCX, PDF, PPTX, XLSX e molti altri.  
- **È necessaria la rasterizzazione per l'output PDF?**  
  La rasterizzazione è opzionale; attivala quando è necessario appiattire il documento per una maggiore sicurezza.  

## Cos'è l'aggiunta di un suffisso al nome file?
Aggiungere un suffisso è una semplice convenzione di denominazione che indica che un file è stato sottoposto a redazione. Previene la condivisione accidentale delle versioni originali non redatte e aiuta le pipeline automatizzate a tenere traccia dello stato di elaborazione.

## Perché usare GroupDocs.Redaction per questo compito?
GroupDocs.Redaction fornisce un'API Java fluida che consente di combinare le azioni di redazione con le opzioni di gestione dei file—come **l'aggiunta di un suffisso al nome file**—in poche righe di codice. Questo fa risparmiare tempo di sviluppo e riduce il rischio di errori manuali.

## Prerequisiti
- **Java Development Kit (JDK):** Versione 8 o superiore.  
- **Libreria GroupDocs.Redaction:** Libreria principale per le attività di redazione.  
- **IDE:** IntelliJ IDEA, Eclipse o qualsiasi editor compatibile con Java.  
- **Maven:** Per la gestione delle dipendenze.  

### Prerequisiti di conoscenza
Familiarità con Java I/O e i concetti di programmazione orientata agli oggetti di base renderà più semplice seguire gli esempi.

## Configurazione di GroupDocs.Redaction per Java
### Configurazione Maven
Includi la seguente configurazione nel tuo file `pom.xml` per accedere alle librerie GroupDocs tramite Maven:

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
In alternativa, scarica l'ultima versione direttamente da [GroupDocs.Redaction for Java releases](https://releases.group.com/redaction/java/).

### Acquisizione della licenza
1. **Free Trial:** Accedi alle funzionalità di base senza restrizioni.  
2. **Temporary License:** Ottieni una licenza temporanea per esplorare le funzionalità avanzate.  
3. **Purchase:** Per un utilizzo a lungo termine, considera l'acquisto di una licenza completa.  

#### Inizializzazione e configurazione di base
Inizializza il tuo progetto aggiungendo le importazioni necessarie:

```java
import com.groupdocs.redaction.Redactor;
```

Con questa configurazione, sei pronto a implementare le funzionalità di redazione dei documenti.

## Guida all'implementazione

### Funzionalità 1: Caricare il documento dallo stream
**Panoramica:** Scopri come caricare i documenti in un `InputStream` per l'elaborazione.

#### Implementazione passo‑passo
##### Passo 1.1: Creare InputStream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Perché:** L'uso di `InputStream` consente di gestire documenti archiviati in vari formati in modo fluido, il che è essenziale quando è necessario **caricare il documento dallo stream** in scenari cloud o micro‑servizio.

### Funzionalità 2: Applicare la redazione di cancellazione delle annotazioni
**Panoramica:** Rimuovi le annotazioni dal tuo documento usando `DeleteAnnotationRedaction`.

##### Passo 2.1: Applicare DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Perché:** Questo passaggio garantisce che tutte le annotazioni sensibili siano rimosse, migliorando la privacy del documento.

### Funzionalità 3: Salvare il documento con opzioni
**Panoramica:** Scopri come salvare il documento elaborato con opzioni specifiche come la rasterizzazione e **l'aggiunta di un suffisso al nome file**.

##### Passo 3.1: Configurare SaveOptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Perché:** Personalizzare le opzioni di salvataggio consente formati di output flessibili e convenzioni di denominazione. Abilitando `setAddSuffix(true)` **aggiunge un suffisso al nome file**, rendendo chiaro che il file è stato redatto.

## Perché aggiungere un suffisso è importante
- **Auditabilità:** I team possono individuare immediatamente quali file sono sicuri da distribuire.  
- **Automazione:** Gli script possono filtrare i file per suffisso, evitando l'elaborazione accidentale dei documenti originali.  
- **Conformità:** Molte normative richiedono una chiara etichettatura dei documenti sanitizzati.  

## Applicazioni pratiche
Esplora questi casi d'uso reali:
1. **Redazione di documenti legali:** Proteggi i contratti prima della condivisione con il cliente.  
2. **Gestione delle cartelle cliniche:** Proteggi gli identificatori dei pazienti.  
3. **Report finanziari:** Mantieni riservati i numeri sensibili.  
4. **Integrazione CRM:** Redigi automaticamente i dati dei clienti prima dell'esportazione.  
5. **Strumenti di collaborazione:** Assicurati che le bozze condivise non espongano commenti nascosti.  

## Considerazioni sulle prestazioni
### Ottimizzazione delle prestazioni
- Usa lo streaming (`load document from stream`) per evitare di caricare interi file in memoria.  
- Chiudi prontamente le istanze di `Redactor` per liberare le risorse.  

### Linee guida sull'uso delle risorse
- Monitora CPU e memoria durante le esecuzioni batch.  
- Preferisci `ByteArrayOutputStream` per salvataggi in‑memoria quando lavori con file di dimensioni modeste.  

### Best practice per la gestione della memoria in Java
- Riutilizza gli oggetti `Redactor` quando elabori più file dello stesso tipo.  
- Invoca `close()` in un blocco `finally` o con try‑with‑resources per prevenire perdite.  

## Problemi comuni e soluzioni
| Problema | Causa | Soluzione |
|----------|-------|-----------|
| **Suffisso non visualizzato** | `setAddSuffix(false)` o chiamata mancante | Assicurati che `options.setAddSuffix(true)` sia impostato prima di `save()`. |
| **OutOfMemoryError su DOCX di grandi dimensioni** | Caricamento dell'intero file in memoria | Passa al caricamento tramite `InputStream` (vedi Funzionalità 1). |
| **Annotazioni ancora visibili** | Redazione non applicata prima del salvataggio | Chiama `redactor.apply(new DeleteAnnotationRedaction())` prima di `save()`. |
| **Rasterizzazione PDF non applicata** | `setRasterizeToPDF(false)` o omessa | Imposta `options.setRasterizeToPDF(true)` quando è necessario un PDF appiattito. |

## Domande frequenti

**D: Posso redigere documenti PDF usando GroupDocs.Redaction?**  
R: Sì, la libreria supporta PDF, DOCX, PPTX, XLSX e molti altri formati.

**D: Qual è il modo migliore per gestire file di grandi dimensioni con GroupDocs.Redaction?**  
R: Usa lo streaming (`load document from stream`) e chiudi le risorse prontamente per mantenere basso l'uso della memoria.

**D: È possibile personalizzare il testo del suffisso?**  
R: L'API aggiunge automaticamente un suffisso predefinito (ad es., “_redacted”). Per suffissi personalizzati, puoi rinominare il file di output dopo il salvataggio.

**D: Come posso ottenere una licenza temporanea per GroupDocs.Redaction?**  
R: Visita la [Temporary License page](https://purchase.groupdocs.com/temporary-license/) e segui le istruzioni.

**D: Dove posso ottenere aiuto se incontro problemi?**  
R: Unisciti al [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) per assistenza da esperti.

## Risorse
- **Documentazione:** Esplora guide dettagliate su [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **Riferimento API:** Accedi a dettagli completi dell'API su [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Ottieni l'ultima versione da [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **Repository GitHub:** Contribuisci o esplora il codice sorgente su [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Ultimo aggiornamento:** 2025-12-17  
**Testato con:** GroupDocs.Redaction 24.9 per Java  
**Autore:** GroupDocs  

---