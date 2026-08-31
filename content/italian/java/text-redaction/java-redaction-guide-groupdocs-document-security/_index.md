---
date: '2026-03-04'
description: Scopri come redigere il testo, sostituire il testo con colore e garantire
  la sicurezza dei documenti Java utilizzando GroupDocs.Redaction per Java. Guida
  passo passo con esempi di codice.
keywords:
- Java Document Redaction
- GroupDocs.Redaction for Java
- text redaction in Java
title: Come censurare il testo nei documenti Java con GroupDocs.Redaction
type: docs
url: /it/java/text-redaction/java-redaction-guide-groupdocs-document-security/
weight: 1
---

# Come censurare il testo nei documenti Java con GroupDocs.Redaction

Nelle applicazioni moderne, **come censurare il testo** all'interno di PDF, file Word o immagini è una necessità frequente per la conformità e la privacy. Che tu debba nascondere identificatori personali, rimuovere annotazioni riservate o eliminare i metadati, GroupDocs.Redaction per Java ti offre un modo pulito e programmatico per garantire **java document security**. Questo tutorial ti guida attraverso ogni passaggio essenziale—dalla configurazione della libreria all'applicazione di censure basate su frase esatta, regex, colore, annotazione e metadati.

## Risposte rapide
- **Quale libreria gestisce la censura dei documenti Java?** GroupDocs.Redaction for Java.  
- **Posso sostituire il testo con un colore invece di rimuoverlo?** Sì, usando la funzione “replace text with color”.  
- **È necessaria una licenza per l'uso in produzione?** È richiesta una licenza temporanea o a pagamento per la piena funzionalità.  
- **Quali versioni di Java sono supportate?** JDK 8 o superiore.  
- **Maven è l'unico modo per aggiungere la libreria?** Maven è consigliato, ma è anche possibile scaricare il JAR manualmente.

## Cos'è “come censurare il testo” in Java?
La censura è il processo di rimozione permanente o oscuramento di contenuti sensibili da un documento in modo che non possano essere recuperati. In Java, ciò tipicamente comporta il caricamento di un file, la definizione di ciò da nascondere, l'applicazione della censura e il salvataggio della versione sanificata.

## Perché utilizzare GroupDocs.Redaction per Java?
- **Supporto completo dei formati** – funziona con DOCX, PDF, PPTX, immagini e altro.  
- **Controllo granulare** – censura per frase esatta, espressione regolare, colore, annotazione o metadati.  
- **Ottimizzato per le prestazioni** – l'elaborazione basata su stream riduce l'uso di memoria per file di grandi dimensioni.  
- **Conformità integrata** – aiuta a soddisfare GDPR, HIPAA e altre normative sulla privacy.

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
1. **Aggiungi la dipendenza Maven** (oppure includi il JAR).  
2. **Configura la tua licenza** chiamando `License.setLicense("path/to/license.lic")` all'inizio della tua applicazione.  
3. **Crea un'istanza `Redactor`** che punta al documento sorgente.

Ora sei pronto per iniziare a censurare.

## Guida all'implementazione

### Censura per frase esatta
Sostituisci una frase specifica (ad esempio il nome di una persona) con un testo segnaposto.

#### Passo‑per‑passo
1. **Inizializza il Redactor** con il documento che desideri elaborare:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. **Definisci la regola di frase esatta** e applicala:

```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction(
    "John Doe", 
    new ReplacementOptions("[Client]"));

redactor.apply(redaction);
```

3. **Salva il file censurato** nella tua cartella di output:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### Censura con regex e sostituzione del testo
Usa le espressioni regolari per individuare pattern come numeri di serie e sostituirli con un token generico.

#### Passo‑per‑passo
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

### Censura con regex e sostituzione colore
Invece di eliminare il testo, puoi **sostituire il testo con colore** per oscurarlo visivamente mantenendo i caratteri sottostanti.

#### Passo‑per‑passo
1. Carica il documento:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Definisci un pattern regex e imposta il colore di sostituzione (ad esempio, blu):

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

### Censura di eliminazione delle annotazioni
Rimuovi tutte le annotazioni (commenti, evidenziazioni, ecc.) da un documento per una versione finale più pulita.

#### Passo‑per‑passo
1. Carica il tuo file:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Applica la regola di eliminazione delle annotazioni:

```java
DeleteAnnotationRedaction redaction = new DeleteAnnotationRedaction();

redactor.apply(redaction);
```

3. Salva le modifiche:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Annotations deleted successfully.");
}
```

### Censura di cancellazione dei metadati
Rimuovi ogni metadato (autore, data di creazione, proprietà personalizzate) per proteggere la privacy e soddisfare gli standard di conformità.

#### Passo‑per‑passo
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

## Applicazioni pratiche (Perché è importante)
- **Preparazione di documenti legali** – Censura i nomi dei clienti prima di condividere le bozze.  
- **Conformità sanitaria** – Rimuovi gli identificatori dei pazienti per rimanere conformi a HIPAA.  
- **Protezione dei dati aziendali** – Nascondi cifre finanziarie o segreti commerciali nei report interni.  

Integrare questi passaggi di censura nel tuo flusso di lavoro esistente automatizza la protezione della privacy e riduce il rischio di perdite accidentali di dati.

## Considerazioni sulle prestazioni
- **Stream invece di caricare** – Per file di grandi dimensioni, usa i costruttori `Redactor` che accettano `InputStream` per evitare di caricare l'intero documento in memoria.  
- **Pre‑compila i pattern regex** quando esegui la stessa censura più volte; questo riduce il carico CPU.  
- **Monitora l'heap JVM** – La censura può richiedere molta memoria; considera di aumentare la dimensione dell'heap per l'elaborazione batch.

## Problemi comuni e risoluzione

| Sintomo | Probabile causa | Soluzione |
|---------|-----------------|-----------|
| Nessuna modifica dopo `apply` | Percorso del documento errato o file bloccato | Verifica il percorso del file e assicurati che il documento non sia aperto altrove |
| Regex non corrisponde | Errore di sintassi del pattern | Testa la regex con un tester online; escapa correttamente le barre rovesciate |
| Sostituzione colore non visibile | Il formato di output non supporta il colore del testo (ad esempio, testo semplice) | Usa un formato come DOCX o PDF che conserva lo stile |
| Errore di licenza a runtime | File di licenza mancante o non valido | Posiziona il file `.lic` in una directory accessibile e chiama `License.setLicense` prima di qualsiasi utilizzo di Redactor |

## Domande frequenti

**Q: Posso combinare più regole di censura in un unico passaggio?**  
A: Sì. Crea ogni oggetto di censura, chiama `redactor.apply()` per ciascuno, poi salva una sola volta.

**Q: GroupDocs.Redaction supporta i file protetti da password?**  
A: Assolutamente. Passa la password al costruttore `Redactor` che accetta un oggetto `LoadOptions`.

**Q: È possibile visualizzare in anteprima le censure prima di salvare?**  
A: Puoi chiamare `redactor.preview()` per generare una vista temporanea che evidenzia le aree da censurare.

**Q: Quali formati di file sono supportati?**  
A: DOCX, PDF, PPTX, XLSX, immagini (PNG, JPEG, BMP) e molti altri.

**Q: Come posso garantire che il documento censurato sia conforme al GDPR?**  
A: Usa la funzione di cancellazione dei metadati, rimuovi le annotazioni e applica censure per frase esatta o regex a tutti i campi di dati personali.

## Conclusione
Adesso hai una guida completa, end‑to‑end, su **come censurare il testo** nei documenti Java usando GroupDocs.Redaction. Seguendo i passaggi per censure per frase esatta, regex, basate sul colore, annotazioni e metadati, puoi ottenere una solida **java document security** mantenendo il tuo codice pulito e manutenibile. Integra questi snippet nei tuoi servizi esistenti, automatizza l'elaborazione batch e rimani conforme alle normative sulla privacy.

---

**Last Updated:** 2026-03-04  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs