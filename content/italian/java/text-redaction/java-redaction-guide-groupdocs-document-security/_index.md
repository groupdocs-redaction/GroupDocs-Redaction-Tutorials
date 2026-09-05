---
date: '2026-08-20'
description: Scopri come censurare il testo nei documenti Java usando GroupDocs.Redaction,
  coprendo la censura di frasi esatte, regex, sostituzione del colore, annotazione
  e censura dei metadati per una conformità sicura.
keywords:
- how to redact text
- replace text with color
- GroupDocs.Redaction Java
- Java document security
- document redaction library
lastmod: '2026-08-20'
og_description: Scopri come censurare il testo nei documenti Java usando GroupDocs.Redaction,
  coprendo la censura di frasi esatte, regex, sostituzione del colore, annotazione
  e censura dei metadati.
og_image_alt: Guide showing Java code redacting text with GroupDocs.Redaction
og_title: Come censurare il testo nei documenti Java con GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  headline: How to redact text in Java documents with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  name: How to redact text in Java documents with GroupDocs.Redaction
  steps:
  - name: '**Add the Maven dependency** (or include the JAR).'
    text: '**Add the Maven dependency** (or include the JAR).'
  - name: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
    text: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
  - name: '**Create a `Redactor` instance** pointing at the source document.'
    text: '**Create a `Redactor` instance** pointing at the source document.'
  - name: '**Initialize the Redactor** with the document you want to process:'
    text: '**Initialize the Redactor** with the document you want to process:'
  - name: '**Define the exact‑phrase rule** and apply it:'
    text: '**Define the exact‑phrase rule** and apply it:'
  - name: '**Save the redacted file** to your output folder:'
    text: '**Save the redacted file** to your output folder:'
  - name: 'Load the document:'
    text: 'Load the document:'
  - name: 'Create a regex rule and apply it:'
    text: 'Create a regex rule and apply it:'
  - name: 'Save the result:'
    text: 'Save the result:'
  - name: 'Load the document:'
    text: 'Load the document:'
  type: HowTo
- questions:
  - answer: Yes. Create each redaction object, call `redactor.apply()` for each, then
      save once.
    question: Can I combine multiple redaction rules in a single pass?
  - answer: Absolutely. Pass the password to the `Redactor` constructor that accepts
      a `LoadOptions` object.
    question: Does GroupDocs.Redaction support password‑protected files?
  - answer: You can call `redactor.preview()` to generate a temporary view that highlights
      the areas to be redacted.
    question: Is it possible to preview redactions before saving?
  - answer: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP, and many more—over 30 formats in
      total.
    question: What file formats are supported?
  - answer: Use the metadata erasure feature, remove annotations, and apply exact‑phrase
      or regex redactions to all personal data fields.
    question: How do I ensure the redacted document complies with GDPR?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document security
- regex redaction
- metadata removal
title: Come censurare il testo nei documenti Java con GroupDocs.Redaction
type: docs
url: /it/java/text-redaction/java-redaction-guide-groupdocs-document-security/
weight: 1
---

# Come redigere testo in documenti Java con GroupDocs.Redaction

In modern applications, **come redigere testo** inside PDFs, Word files, or images is a frequent requirement for compliance and privacy. Whether you need to hide personal identifiers, remove confidential annotations, or strip metadata, GroupDocs.Redaction for Java gives you a clean, programmatic way to achieve **java document security**. This tutorial walks you through every essential step—from setting up the library to applying exact‑phrase, regex, color‑based, annotation, and metadata redactions—so you can embed redaction directly into your backend services.

## Risposte rapide
- **Quale libreria gestisce la redazione di documenti Java?** GroupDocs.Redaction for Java.  
- **Posso sostituire il testo con un colore invece di rimuoverlo?** Sì, usa la funzione “replace text with color”.  
- **È necessaria una licenza per l'uso in produzione?** È richiesta una licenza temporanea o a pagamento per la piena funzionalità.  
- **Quali versioni di Java sono supportate?** JDK 8 o superiore.  
- **Maven è l'unico modo per aggiungere la libreria?** Maven è consigliato, ma è possibile scaricare il JAR manualmente.

## Cos'è “how to redact text” in Java?
**La redazione rimuove o oscura permanentemente i contenuti sensibili in modo che non possano essere recuperati.** In Java, carichi un file, definisci cosa nascondere, applichi la redazione e salvi la versione sanificata. Questo garantisce che qualsiasi consumatore a valle veda solo il documento pulito.

## Perché usare GroupDocs.Redaction per Java?
Carica il tuo file, definisci una regola e l'SDK gestisce il lavoro pesante. GroupDocs.Redaction supporta **30+ formati** — inclusi DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP — e elabora grandi documenti tramite un'architettura basata su stream. Offre redazione per frase esatta, regex, basata su colore, annotazione e metadati, fornendo un controllo fine per soddisfare GDPR, HIPAA e altre normative.

## Prerequisiti
- **Java Development Kit (JDK) 8+** installato sulla tua macchina.  
- **Maven** per la gestione delle dipendenze (oppure puoi scaricare il JAR manualmente).  

### Librerie e dipendenze richieste
Aggiungi il repository GroupDocs e la dipendenza Redaction al tuo `pom.xml`:

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

Puoi anche scaricare l'ultimo JAR dalla pagina di rilascio ufficiale: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisizione della licenza
Per l'uso in produzione, ottieni una licenza temporanea o completa. È disponibile una prova gratuita per scopi di valutazione.

## Configurazione di GroupDocs.Redaction per Java
1. **Aggiungi la dipendenza Maven** (o includi il JAR).  
2. **Configura la tua licenza** chiamando `License.setLicense("path/to/license.lic")` all'inizio della tua applicazione.  
   `License` è la classe usata per caricare e applicare un file di licenza GroupDocs Redaction.  
3. **Crea un'istanza `Redactor`** che punti al documento sorgente.

**La classe `Redactor` è il motore principale che carica, modifica e salva i documenti in modo efficiente in termini di memoria.** Una volta che hai un oggetto `Redactor`, puoi concatenare più regole di redazione prima di persistere il risultato.

Ora sei pronto per iniziare a redigere.

## Guida all'implementazione

### Redazione per frase esatta
Sostituisci una frase specifica (ad esempio, il nome di una persona) con un testo segnaposto.

#### Come funziona la redazione per frase esatta?
`ExactPhraseRedaction` rappresenta una regola che rimuove o sostituisce una specifica stringa di testo esatta. Carica il documento, crea una regola `ExactPhraseRedaction` che mira alla stringa esatta, applica la regola e salva l'output. L'SDK cancella automaticamente il testo corrispondente mantenendo il layout.

1. **Inizializza il Redactor** con il documento che desideri elaborare:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. **Definisci la regola per frase esatta** e applicala:

```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction(
    "John Doe", 
    new ReplacementOptions("[Client]"));

redactor.apply(redaction);
```

3. **Salva il file redatto** nella tua cartella di output:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### Redazione con regex e sostituzione del testo
Usa le espressioni regolari per individuare pattern come numeri di serie e sostituirli con un token generico.

#### Come funziona la redazione con regex e sostituzione?
`RegexRedaction` definisce una regola basata su un'espressione regolare per trovare e modificare il testo corrispondente. Fornisci un oggetto `RegexRedaction` che contiene il pattern e la stringa di sostituzione. Il motore scansiona il documento, sostituisce ogni corrispondenza e mantiene intatto il formato circostante.

1. Carica il documento:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Crea una regola regex e applicala:

```java
RegexRedaction redaction = new RegexRedaction(
    "Redaction",
    new ReplacementOptions("[Product]"));

redactor.apply(redaction);
```

3. Salva il risultato:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### Redazione con regex e sostituzione colore
Invece di eliminare il testo, puoi **sostituire il testo con colore** per oscurarlo visivamente mantenendo i caratteri sottostanti.

#### In che modo la redazione basata su colore differisce dall'eliminazione?
L'SDK colora il testo corrispondente con il colore scelto, rendendolo illeggibile all'occhio umano ma ancora presente nello stream del file. Questo è utile quando è necessario mantenere la struttura del documento per l'elaborazione a valle.

1. Carica il documento:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Definisci un pattern regex e imposta il colore di sostituzione (ad es., blu):

```java
RegexRedaction redaction = new RegexRedaction(
    "\d{2}\s*\d{2}[^\\d]*\d{6}", 
    new ReplacementOptions(Color.BLUE));

redactor.apply(redaction);
```

3. Salva il file aggiornato:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### Redazione di eliminazione annotazioni
Rimuovi tutte le annotazioni (commenti, evidenziazioni, ecc.) da un documento per una versione finale più pulita.

#### Come rimuovere le annotazioni in un solo passaggio?
`AnnotationRedaction` è una regola che rimuove annotazioni come commenti, evidenziazioni e timbri. Crea una regola `AnnotationRedaction` che mira a ogni tipo di annotazione, applicala e persisti le modifiche.

1. Carica il tuo file:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Applica la regola di eliminazione delle annotazioni:

```java
DeleteAnnotationRedaction redaction = new DeleteAnnotationRedaction();

redactor.apply(redaction);
```

3. Persisti le modifiche:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Annotations deleted successfully.");
}
```

### Redazione cancellazione metadati
Rimuovi ogni elemento di metadati (autore, data di creazione, proprietà personalizzate) per proteggere la privacy e rispettare gli standard di conformità.

#### In che modo la cancellazione dei metadati garantisce la privacy?
`MetadataRedaction` cancella i campi di metadati integrati e personalizzati dal documento. La regola `MetadataRedaction` elimina i campi di metadati integrati e personalizzati, assicurando che nessun identificatore nascosto rimanga nel bag delle proprietà del file.

1. Apri il documento:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Applica la regola di cancellazione dei metadati:

```java
EraseMetadataRedaction redaction = new EraseMetadataRedaction(MetadataFilters.All);

redactor.apply(redaction);
```

3. Salva il documento sanificato:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Metadata erased successfully.");
}
```

## Applicazioni pratiche (perché è importante)
- **Preparazione di documenti legali** – Redigi i nomi dei clienti prima di condividere le bozze con la controparte.  
- **Conformità sanitaria** – Rimuovi gli identificatori dei pazienti per rimanere conformi a HIPAA senza modifiche manuali.  
- **Protezione dei dati aziendali** – Nascondi cifre finanziarie o segreti commerciali nei report interni prima della distribuzione.  

Automatizzare questi passaggi riduce lo sforzo manuale, elimina gli errori umani e garantisce una conformità costante su migliaia di file.

## Considerazioni sulle prestazioni
- **Stream invece di load** – Per file di grandi dimensioni, usa i costruttori `Redactor` che accettano `InputStream` per evitare di caricare l'intero documento in memoria.  
- **Pre‑compila i pattern regex** quando esegui la stessa redazione più volte; questo riduce il carico CPU fino al 30 %.  
- **Monitora l'heap JVM** – La redazione può essere intensiva in memoria; considera di aumentare la dimensione dell'heap (`-Xmx2g`) per l'elaborazione batch di archivi multi‑gigabyte.

## Problemi comuni e risoluzione
| Sintomo | Probabile causa | Soluzione |
|---------|-----------------|-----------|
| Nessuna modifica dopo `apply` | Percorso del documento errato o file bloccato | Verifica il percorso del file e assicurati che il documento non sia aperto altrove |
| Regex non corrisponde | Errore di sintassi del pattern | Testa la regex con un tester online; escapa correttamente le barre rovesciate |
| Sostituzione colore non visibile | Il formato di output non supporta il colore del testo (es. testo semplice) | Usa un formato come DOCX o PDF che conserva lo stile |
| Errore di licenza a runtime | File di licenza mancante o non valido | Posiziona il file `.lic` in una directory accessibile e chiama `License.setLicense` prima di qualsiasi utilizzo di Redactor |

## Domande frequenti

**Q: Posso combinare più regole di redazione in un unico passaggio?**  
A: Sì. Crea ogni oggetto di redazione, chiama `redactor.apply()` per ciascuno, poi salva una sola volta.

**Q: GroupDocs.Redaction supporta file protetti da password?**  
A: Assolutamente. Passa la password al costruttore `Redactor` che accetta un oggetto `LoadOptions`.

**Q: È possibile visualizzare in anteprima le redazioni prima di salvare?**  
A: Puoi chiamare `redactor.preview()` per generare una vista temporanea che evidenzia le aree da redigere.

**Q: Quali formati di file sono supportati?**  
A: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP e molti altri — oltre 30 formati in totale.

**Q: Come posso garantire che il documento redatto sia conforme al GDPR?**  
A: Usa la funzione di cancellazione dei metadati, rimuovi le annotazioni e applica redazioni per frase esatta o regex a tutti i campi di dati personali.

## Conclusione
Ora hai una guida completa, end‑to‑end, su **come redigere testo** nei documenti Java usando GroupDocs.Redaction. Seguendo i passaggi per redazioni per frase esatta, regex, basate su colore, annotazioni e metadati, puoi ottenere una solida **java document security** mantenendo il tuo codice pulito e manutenibile. Integra questi snippet nei tuoi servizi esistenti, automatizza l'elaborazione batch e rimani conforme alle normative sulla privacy.

---

**Ultimo aggiornamento:** 2026-08-20  
**Testato con:** GroupDocs.Redaction 24.9 for Java  
**Autore:** GroupDocs

## Tutorial correlati

- [sostituisci testo metadati java – Redazione sicura con GroupDocs](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [Come redigere immagini nei documenti Word usando GroupDocs.Redaction per Java – Guida completa](/redaction/java/image-redaction/redact-images-word-docs-groupdocs-redaction-java/)
- [Come redigere documenti con licenza GroupDocs Redaction Java da percorso file – Guida passo‑passo](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)