---
date: '2026-06-26'
description: Scopri come estrarre il testo da PDF scansionati e mascherare i dati
  sensibili utilizzando GroupDocs OCR Redaction con Azure OCR. Redigi il numero di
  previdenza sociale e sostituisci le informazioni riservate nei PDF in modo efficiente.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Estrai testo da PDF scansionato – Maschera i dati con GroupDocs OCR
type: docs
url: /it/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Estrai Testo da PDF Scansionato – Maschera Dati con GroupDocs OCR

Nel mondo odierno guidato dai dati, **estrarre testo da PDF scansionati** e mascherare le informazioni riservate è un passaggio di conformità non negoziabile. Questo tutorial ti guida nell'utilizzo di GroupDocs Redaction insieme a Microsoft Azure OCR per riconoscere in modo affidabile il testo nascosto nelle pagine scansionate e sostituirlo con un segnaposto sicuro come **`[REDACTED]`**. Vedrai perché questa combinazione è veloce, accurata e pronta per carichi di lavoro di livello produttivo.

## Risposte Rapide
- **Cosa significa “mascherare dati sensibili”?** Sostituisce il testo riservato identificato con un segnaposto (ad es., `[REDACTED]`).  
- **Quale libreria gestisce l'OCR?** Il connettore Microsoft Azure OCR, utilizzato tramite GroupDocs Redaction.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per la valutazione; è necessaria una licenza permanente per la produzione.  
- **Posso redigere PDF scansionati?** Sì—l'OCR estrae il testo nascosto prima di applicare le redazioni regex.  
- **Questa soluzione è solo Java?** L'esempio è basato su Java, ma GroupDocs fornisce API simili per .NET e altre piattaforme.

## Cos'è la Redazione Basata su OCR?
La Redazione Basata su OCR esegue prima l'OCR su ogni pagina, trasformando le immagini in testo ricercabile, quindi applica pattern regex per sostituire le corrispondenze con una maschera come `[REDACTED]`. Questo processo a due fasi ti consente di nascondere in modo affidabile i dati personali anche nei PDF scansionati, garantendo che qualsiasi stringa sensibile venga rimossa prima che il documento venga condiviso o archiviato.

## Perché Usare GroupDocs Redaction con Azure OCR?
Dovresti usare GroupDocs Redaction con Azure OCR perché offre **>98 % di precisione OCR su testo stampato**, supporta **oltre 50 formati di input e output**, e può elaborare **PDF di centinaia di pagine senza caricare l'intero file in memoria**, garantendo una redazione rapida e scalabile per la conformità. La soluzione inoltre **scala per elaborare un PDF di 1.000 pagine in meno di 2 minuti su un server a 8 core**, rendendo pratici i lavori batch.

## Prerequisiti
- **Java Development Kit (JDK) 8+** installato.  
- **Maven** (se preferisci la gestione delle dipendenze) o la possibilità di scaricare i JAR manualmente.  
- **Credenziali Microsoft Azure OCR** (endpoint e chiave di sottoscrizione).  
- Conoscenza di base di Java e familiarità con le espressioni regolari.

## Configurazione di GroupDocs Redaction per Java

### Configurazione Maven
Aggiungi il repository GroupDocs e la dipendenza al tuo `pom.xml`:

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

### Download Diretto
Se preferisci la gestione manuale dei JAR, scarica l'ultima versione da [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisizione Licenza
- **Prova Gratuita** – esplora tutte le funzionalità senza costi.  
- **Licenza Temporanea** – estendi il periodo di valutazione.  
- **Licenza Completa** – sblocca le capacità pronte per la produzione.

### Inizializzazione e Configurazione di Base
La classe `Redactor` è il motore principale che esegue l'estrazione OCR e applica le regole di redazione ai documenti PDF.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Come Mascherare Dati Sensibili con la Redazione OCR
Mascherare dati sensibili con la Redazione OCR comporta il caricamento del PDF con le impostazioni Azure OCR, la definizione di pattern regex per i dati da nascondere e l'invocazione del Redactor per sostituire ogni corrispondenza con un segnaposto come `[REDACTED]`. La libreria gestisce OCR, il matching dei pattern e la riscrittura del PDF in un unico flusso di lavoro.

### Passo 1: Carica il Documento con le Impostazioni OCR
`LoadOptions` configura come GroupDocs carica un file, consentendoti di passare connettori OCR come Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – sostituisci con il percorso del tuo PDF.  
- **`settings`** – contiene il connettore Azure OCR creato in precedenza.

### Passo 2: Definisci e Applica Redazioni Regex
`ReplacementOptions` specifica il testo di sostituzione che sostituirà ogni corrispondenza regex durante la redazione.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- Il pattern `\b\d{3}-\d{2}-\d{4}\b` corrisponde ai Numeri di Sicurezza Sociale statunitensi.  
- `ReplacementOptions("[REDACTED]")` sostituisce ogni corrispondenza con la maschera, mascherando efficacemente **dati sensibili**.

## Casi d'Uso Comuni per Mascherare Dati Sensibili
1. **Gestione Documenti Legali** – nascondi gli identificatori dei clienti prima di condividere le bozze.  
2. **Reportistica Finanziaria** – proteggi i numeri di conto e gli ID delle transazioni.  
3. **Cartelle Cliniche** – rispetta l'HIPAA redigendo gli identificatori dei pazienti.  
4. **Pubblicazioni Governative** – rimuovi i dati personali dai registri pubblici.  
5. **Contratti Aziendali** – nascondi i termini proprietari durante le revisioni esterne.

## Suggerimenti sulle Prestazioni
- **Ottimizza le regex** – evita pattern troppo generici che aumentano il tempo di elaborazione; espressioni ben costruite possono ridurre il tempo di esecuzione fino al 40 %.  
- **Gestione della Memoria** – chiudi l'istanza `Redactor` prontamente (try‑with‑resources lo fa automaticamente).  
- **Esecuzione Asincrona** – per l'elaborazione in blocco, esegui i job di redazione su thread separati o utilizza una coda di task per mantenere l'interfaccia reattiva.

## Risoluzione dei Problemi
- **Errore credenziali Azure** – ricontrolla l'URL dell'endpoint e la chiave di sottoscrizione in `MicrosoftAzureOcrConnector`.  
- **Documento non caricato** – verifica il percorso del file e assicurati che il PDF non sia protetto da password (oppure fornisci la password tramite `LoadOptions`).  
- **Nessuna redazione applicata** – testa la tua regex con una stringa semplice prima; usa `Pattern.compile` in un test unitario per confermare le corrispondenze.

## Domande Frequenti

**Q: Cos'è la redazione OCR?**  
A: La redazione OCR utilizza il riconoscimento ottico dei caratteri per estrarre il testo nascosto da immagini o PDF scansionati, quindi applica regole di redazione per mascherare quel testo.

**Q: Posso usare GroupDocs Redaction senza Azure OCR?**  
A: Sì, ma l'OCR migliora notevolmente la precisione sui documenti scansionati dove l'estrazione di testo nativa fallisce.

**Q: Come gestisco pattern regex complessi?**  
A: Costruiscili e testali in modo incrementale, usando la classe `Pattern` di Java in un sandbox prima di applicarli a documenti di grandi dimensioni.

**Q: Quali sono i tipici colli di bottiglia delle prestazioni?**  
A: PDF di grandi dimensioni, regex troppo complesse e chiamate OCR sincrone possono rallentare l'elaborazione; considera l'elaborazione batch e pattern ottimizzati.

**Q: È disponibile supporto per problemi di implementazione?**  
A: Assolutamente—contatta il [forum GroupDocs](https://forum.groupdocs.com/c/redaction/33) per assistenza della community o contatta il supporto GroupDocs.

## Risorse Aggiuntive
- **Documentazione**: https://docs.groupdocs.com/redaction/java/  
- **Riferimento API**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Supporto Gratuito**: https://forum.groupdocs.com/c/redaction/33  
- **Licenza Temporanea**: https://purchase.groupdocs.com/temporary-license/

---

**Ultimo Aggiornamento:** 2026-06-26  
**Testato Con:** GroupDocs.Redaction 24.9 (Java)  
**Autore:** GroupDocs  

## Tutorial Correlati

- [Redazione PDF Sicura usando OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Come Redigere Testo con GroupDocs.Redaction per Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Mascherare Dati Sensibili Java – Redigere Informazioni Personali con GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)