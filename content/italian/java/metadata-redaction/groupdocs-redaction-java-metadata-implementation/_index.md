---
date: '2026-03-22'
description: Impara come cancellare i metadati e rimuovere i metadati dell'autore
  in Java usando GroupDocs. Questo tutorial ti mostra come salvare in modo sicuro
  i file di documenti redatti.
keywords:
- metadata redaction in Java
- GroupDocs Redaction setup
- removing metadata fields
title: 'Come cancellare i metadati in Java con GroupDocs: guida passo passo'
type: docs
url: /it/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Come cancellare i metadati in Java con GroupDocs

Nel mondo digitale di oggi, proteggere le informazioni sensibili all'interno dei documenti è essenziale, e **sapere come cancellare i metadati** è una parte fondamentale di tale protezione. In questa guida imparerai a usare `EraseMetadataRedaction` per rimuovere i metadati come *Author* e *Manager* dai file Word usando GroupDocs.Redaction per Java. Alla fine del tutorial avrai un documento pulito e sicuro dal punto di vista della privacy e saprai come **salvare i documenti redatti** per condivisioni o archiviazioni sicure.

## Risposte rapide
- **Cosa fa EraseMetadataRedaction?** Rimuove i campi di metadati selezionati da un documento.  
- **Quale libreria fornisce questa funzionalità?** GroupDocs.Redaction per Java.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per i test; è necessaria una licenza permanente per la produzione.  
- **Posso mirare a più campi contemporaneamente?** Sì, combina i filtri con un OR logico.  
- **Il processo è thread‑safe?** Le istanze di Redactor non sono condivise tra i thread; crea una nuova istanza per ogni operazione.

## Come cancellare i metadati in Java
Questa sezione ti guida attraverso i passaggi esatti necessari per **rimuovere i metadati dell'autore** e qualsiasi altra proprietà indesiderata dai tuoi file.

### Cos'è EraseMetadataRedaction?
`EraseMetadataRedaction` è una classe di redazione integrata che consente di specificare quali voci di metadati devono essere cancellate. Funziona su un'ampia gamma di formati di documento supportati da GroupDocs.Redaction, garantendo che le informazioni di autore nascoste non trapelino mai.

### Perché usare EraseMetadataRedaction con GroupDocs?
- **Conformità** – Rispettare GDPR, HIPAA o le politiche aziendali rimuovendo identificatori personali.  
- **Coerenza** – Applicare la stessa logica di redazione su PDF, DOCX, PPTX e altri formati.  
- **Prestazioni** – La redazione avviene in memoria senza necessità di strumenti esterni.  
- **Flessibilità** – Combina più `MetadataFilters` per mirare esattamente a ciò di cui hai bisogno.

## Prerequisiti
- Java 8 o versioni successive installate.  
- Maven (o la possibilità di aggiungere JAR manualmente).  
- GroupDocs.Redaction per Java (versione 24.9 o successiva).  
- Una licenza di prova o permanente valida di GroupDocs.

## Configurare GroupDocs.Redaction per Java

### Installazione con Maven
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
Ottieni una prova gratuita o acquista una licenza temporanea dal portale GroupDocs. Il file di licenza deve essere posizionato dove la tua applicazione può caricarlo (ad es., nella radice del classpath).

### Inizializzazione e configurazione di base
Di seguito è riportato un esempio minimale che crea un'istanza `Redactor` per un file DOCX:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Come usare EraseMetadataRedaction in Java
Le sezioni seguenti suddividono l'implementazione in passaggi chiari e azionabili.

### Funzionalità: Pulire voci di metadati specifiche

#### Panoramica
Cancelleremo i campi di metadati **Author** e **Manager** usando `EraseMetadataRedaction`. Questa è una necessità comune quando si condividono report interni con partner esterni.

#### Implementazione passo‑passo

##### 1️⃣ Inizializzare l'oggetto Redactor
Crea un'istanza `Redactor` che punti al documento che desideri pulire:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ Applicare EraseMetadataRedaction
Usa la classe `EraseMetadataRedaction` insieme a `MetadataFilters`. L'OR bitwise (`|`) combina i filtri `Author` e `Manager` così entrambi i campi vengono rimossi in una singola chiamata:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ Configurare le opzioni di salvataggio
Regola le `SaveOptions` per controllare il nome del file di output e se il documento deve essere rasterizzato in PDF:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

### Casi d'uso comuni
1. **Documenti legali** – Redigere le informazioni sull'autore prima di inviare i contratti alla controparte.  
2. **Report aziendali** – Rimuovere i nomi dei manager quando si pubblicano i risultati trimestrali agli azionisti.  
3. **File di progetto** – Pulire la documentazione interna del progetto prima di archiviarla o caricarla in un repository pubblico.

### Suggerimenti per la risoluzione dei problemi
- **File non trovato** – Verifica che il percorso in `inputFilePath` punti a un file esistente e che l'applicazione abbia i permessi di lettura.  
- **Campi di metadati mancanti** – Non tutti i tipi di documento memorizzano le stesse chiavi di metadati; controlla prima le proprietà del documento in Office.  
- **Errori di licenza** – Assicurati che il file di licenza sia caricato correttamente prima di creare l'istanza `Redactor`.

## Considerazioni sulle prestazioni
- Chiudi l'oggetto `Redactor` prontamente (come mostrato nel blocco `finally`) per liberare le risorse native.  
- Evita di rasterizzare documenti di grandi dimensioni a meno che non ti serva un'anteprima PDF; la rasterizzazione può aumentare significativamente l'uso di CPU e memoria.

## Domande frequenti

**Q1: Cos'è la redazione dei metadati?**  
A1: La redazione dei metadati consiste nella rimozione delle proprietà nascoste del documento (come author, manager o tag personalizzati) per prevenire la divulgazione accidentale di informazioni sensibili.

**Q2: Posso usare GroupDocs.Redaction per altri tipi di file?**  
A2: Sì, la libreria supporta PDF, DOCX, PPTX, XLSX e molti altri formati.

**Q3: Come gestisco gli errori durante la redazione?**  
A3: Avvolgi la chiamata `apply` in un blocco try‑catch e chiudi sempre il `Redactor` in una clausola finally per garantire il rilascio delle risorse.

**Q4: È possibile redigere campi di metadati personalizzati?**  
A4: Assolutamente. Usa `MetadataFilters.Custom("YourFieldName")` (o l'enum appropriato) per mirare a qualsiasi proprietà personalizzata.

**Q5: Quali sono le migliori pratiche per l'uso di GroupDocs.Redaction?**  
A5:  
- Carica la licenza all'inizio della tua applicazione.  
- Chiudi gli oggetti `Redactor` prontamente.  
- Usa `SaveOptions` per aggiungere un suffisso, mantenendo intatti i file originali.  
- Testa la redazione su una copia del documento prima di elaborare i batch.

**Q6: EraseMetadataRedaction supporta operazioni batch?**  
A6: Puoi iterare su una collezione di percorsi file, creando un nuovo `Redactor` per ogni file e applicando la stessa logica di redazione.

**Q7: Posso combinare EraseMetadataRedaction con altri tipi di redazione?**  
A7: Sì, puoi concatenare più oggetti di redazione (ad esempio, redazione del testo seguita da redazione dei metadati) prima del salvataggio.

## Risorse

- **Documentazione**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **Riferimento API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Supporto gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Licenza temporanea**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Ultimo aggiornamento:** 2026-03-22  
**Testato con:** GroupDocs.Redaction 24.9 per Java  
**Autore:** GroupDocs  

---