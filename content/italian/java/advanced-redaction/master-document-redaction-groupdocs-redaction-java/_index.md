---
date: '2026-02-16'
description: Scopri come utilizzare la dipendenza GroupDocs Maven per aggiungere un
  suffisso ai nomi dei file durante la redazione di documenti in Java. Include il
  caricamento da stream, la cancellazione delle annotazioni e le opzioni di salvataggio.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Dipendenza Maven di GroupDocs – Aggiungere un suffisso al nome file in Java
type: docs
url: /it/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Come aggiungere un suffisso al nome file durante la redazione di documenti in Java con GroupDocs.Redaction

Redigere dati riservati è solo metà della battaglia—devi anche assicurarti che il file salvato indichi chiaramente di essere stato elaborato. **Using the groupdocs maven dependency makes this straightforward**, consentendoti di aggiungere un suffisso al nome del file di output in poche righe di codice. In questa guida imparerai come aggiungere un suffisso al nome file quando salvi un documento redatto, oltre a caricare, annotare e salvare usando GroupDocs.Redaction per Java. Che tu stia proteggendo contratti legali, cartelle cliniche o report finanziari, questi passaggi manterranno il tuo flusso di lavoro sicuro e verificabile.

## Risposte rapide
- **Cosa fa “add suffix to filename”?**  
  Aggiunge un suffisso personalizzato (ad es., “_redacted”) al nome del file di output così puoi identificare immediatamente i file elaborati.  
- **Posso caricare un documento dallo stream?**  
  Sì—GroupDocs.Redaction supporta il caricamento da qualsiasi `InputStream`, ideale per archiviazione cloud o elaborazione in‑memoria.  
- **È necessaria una licenza per questa funzionalità?**  
  Una prova gratuita funziona per la redazione di base; una licenza temporanea o completa sblocca tutte le opzioni avanzate, incluso la gestione del suffisso.  
- **Quali formati sono supportati?**  
  La libreria gestisce DOCX, PDF, PPTX, XLSX e molti altri.  
- **È necessaria la rasterizzazione per l'output PDF?**  
  La rasterizzazione è opzionale; attivala quando è necessario appiattire il documento per una sicurezza aggiuntiva.

## Che cos'è l'aggiunta di un suffisso al nome file?
Appendere un suffisso è una semplice convenzione di denominazione che indica che un file è stato sottoposto a redazione. Previene la condivisione accidentale delle versioni originali non redatte e aiuta le pipeline automatizzate a tenere traccia dello stato di elaborazione.

## Perché usare GroupDocs.Redaction per questo compito?
GroupDocs.Redaction fornisce un'API Java fluida che consente di combinare le azioni di redazione con le opzioni di gestione dei file—come **l'aggiunta di un suffisso al nome file**—in poche righe di codice. Questo fa risparmiare tempo di sviluppo e riduce il rischio di errori manuali.

## Prerequisiti

- **Java Development Kit (JDK):** Versione 8 o superiore.  
- **GroupDocs.Redaction Library:** Libreria core per le attività di redazione.  
- **IDE:** IntelliJ IDEA, Eclipse o qualsiasi editor compatibile con Java.  
- **Maven:** Per la gestione delle dipendenze.  

### Conoscenze preliminari
Familiarità con Java I/O e i concetti di programmazione orientata agli oggetti di base renderà gli esempi più facili da seguire.

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
In alternativa, scarica l'ultima versione direttamente da [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisizione della licenza
1. **Free Trial:** Accesso alle funzionalità di base senza restrizioni.  
2. **Temporary License:** Ottieni una licenza temporanea per esplorare le funzionalità avanzate.  
3. **Purchase:** Per un utilizzo a lungo termine, considera l'acquisto di una licenza completa.

#### Inizializzazione e configurazione di base
Inizializza il tuo progetto aggiungendo le importazioni necessarie:

```java
import com.groupdocs.redaction.Redactor;
```

Con questa configurazione, sei pronto a implementare le funzionalità di redazione dei documenti.

## Guida all'implementazione

### Funzionalità 1: Caricare documento dallo stream
**Panoramica:** Impara come caricare documenti in un `InputStream` per l'elaborazione.

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

- **Perché:** L'uso di `InputStream` consente di gestire documenti archiviati in vari formati senza interruzioni, il che è essenziale quando è necessario **load document from stream** in scenari cloud o micro‑service.

### Funzionalità 2: Applicare la redazione di cancellazione annotazioni
**Panoramica:** Rimuovi le annotazioni dal tuo documento usando `DeleteAnnotationRedaction`.

#### Implementazione passo‑passo
##### Passo 2.1: Applicare DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Perché:** Questo passaggio garantisce che tutte le annotazioni sensibili vengano rimosse, migliorando la privacy del documento.

### Funzionalità 3: Salvare documento con opzioni
**Panoramica:** Impara come salvare il tuo documento elaborato con opzioni specifiche come la rasterizzazione e **l'aggiunta di un suffisso al nome file**.

#### Implementazione passo‑passo
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

- **Perché:** Personalizzare le opzioni di salvataggio consente formati di output flessibili e convenzioni di denominazione. Abilitando `setAddSuffix(true)` **adds suffix to filename**, rendendo chiaro che il file è stato redatto.

## Panoramica della dipendenza groupdocs maven
**groupdocs maven dependency** porta l'intero Redaction SDK nel tuo progetto con una singola voce `<dependency>`. Gestisce le dipendenze transitive, mantiene le librerie aggiornate e semplifica l'automazione della build. Dichiarando la dipendenza in `pom.xml`, eviti la gestione manuale dei JAR e garantisci la compatibilità con le ultime patch di sicurezza.

## Perché aggiungere un suffisso è importante
- **Auditabilità:** I team possono individuare immediatamente quali file sono sicuri da distribuire.  
- **Automazione:** Gli script possono filtrare i file per suffisso, evitando l'elaborazione accidentale dei documenti originali.  
- **Conformità:** Molte normative richiedono una chiara etichettatura dei documenti sanificati.  

## Applicazioni pratiche
Esplora questi casi d'uso reali:
1. **Legal Document Redaction:** Proteggi i contratti prima della condivisione con il cliente.  
2. **Medical Record Handling:** Proteggi gli identificatori dei pazienti.  
3. **Financial Reporting:** Mantieni riservati i numeri sensibili.  
4. **CRM Integration:** Redigi automaticamente i dati dei clienti prima dell'esportazione.  
5. **Collaboration Tools:** Assicura che le bozze condivise non espongano commenti nascosti.

## Considerazioni sulle prestazioni
### Ottimizzare le prestazioni
- Usa lo streaming (`load document from stream`) per evitare di caricare interi file in memoria.  
- Chiudi prontamente le istanze di `Redactor` per liberare le risorse.

### Linee guida sull'uso delle risorse
- Monitora CPU e memoria durante le esecuzioni batch.  
- Preferisci `ByteArrayOutputStream` per salvataggi in‑memoria quando lavori con file di dimensioni modeste.

### Best practice per la gestione della memoria Java
- Riutilizza gli oggetti `Redactor` quando elabori più file dello stesso tipo.  
- Invoca `close()` in un blocco `try‑with‑resources` per prevenire perdite.

## Problemi comuni e soluzioni
| Problema | Causa | Soluzione |
|----------|-------|-----------|
| **Suffix not appearing** | `setAddSuffix(false)` or missing call | Assicurati che `options.setAddSuffix(true)` sia impostato prima di `save()`. |
| **OutOfMemoryError su DOCX di grandi dimensioni** | Loading whole file into memory | Passa al caricamento tramite `InputStream` (vedi Feature 1). |
| **Annotations still visible** | Redaction not applied before save | Chiama `redactor.apply(new DeleteAnnotationRedaction())` prima di `save()`. |
| **PDF rasterization not applied** | `setRasterizeToPDF(false)` or omitted | Imposta `options.setRasterizeToPDF(true)` quando è necessario un PDF appiattito. |

## Domande frequenti

**Q: Posso redigere documenti PDF usando GroupDocs.Redaction?**  
A: Sì, la libreria supporta PDF, DOCX, PPTX, XLSX e molti altri formati.

**Q: Qual è il modo migliore per gestire file di grandi dimensioni con GroupDocs.Redaction?**  
A: Usa lo streaming (`load document from stream`) e chiudi le risorse prontamente per mantenere basso l'uso della memoria.

**Q: È possibile personalizzare il testo del suffisso?**  
A: L'API aggiunge automaticamente un suffisso predefinito (ad es., “_redacted”). Per suffissi personalizzati, puoi rinominare il file di output dopo il salvataggio.

**Q: Come posso ottenere una licenza temporanea per GroupDocs.Redaction?**  
A: Visita la [Temporary License page](https://purchase.groupdocs.com/temporary-license/) e segui le istruzioni.

**Q: Dove posso ottenere aiuto se incontro problemi?**  
A: Unisciti al [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) per assistenza da esperti.

## Risorse
- **Documentation:** Esplora guide dettagliate su [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Accedi a dettagli completi dell'API su [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Ottieni l'ultima versione da [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Contribuisci o esplora il codice sorgente su [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Ultimo aggiornamento:** 2026-02-16  
**Testato con:** GroupDocs.Redaction 24.9 for Java  
**Autore:** GroupDocs