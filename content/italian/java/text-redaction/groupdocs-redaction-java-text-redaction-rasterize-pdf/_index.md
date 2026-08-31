---
date: '2026-02-24'
description: Scopri come redigere il testo con GroupDocs.Redaction per Java e salvarlo
  come PDF rasterizzato per documenti sicuri e non modificabili.
keywords:
- text redaction Java
- save as rasterized PDF
- GroupDocs.Redaction Java
title: Come censurare il testo e salvare PDF rasterizzati con GroupDocs.Java
type: docs
url: /it/java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/
weight: 1
---

# Come redigere testo e salvare PDF rasterizzati con GroupDocs.Redaction Java

Proteggere le informazioni sensibili nei tuoi documenti è fondamentale. Che tu debba redigere nomi personali o preparare versioni sicure dei tuoi file, GroupDocs.Redaction per Java semplifica queste operazioni. **Come redigere testo** rapidamente e poi **salvare come PDF rasterizzato** è una necessità comune per le applicazioni guidate dalla conformità, e questa guida ti mostra esattamente come farlo.

## Risposte rapide
- **Cosa significa “redact text”?** Sostituisce o rimuove le stringhe sensibili in modo che non possano essere lette o recuperate.  
- **Quale libreria gestisce il lavoro?** GroupDocs.Redaction per Java fornisce funzionalità integrate di redazione e rasterizzazione.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per i test; è necessaria una licenza permanente per la produzione.  
- **Posso convertire DOCX in un PDF rasterizzato in un solo passaggio?** Sì – applica prima la redazione, poi usa `SaveOptions` con la rasterizzazione abilitata.  
- **L'output è davvero non modificabile?** I PDF rasterizzati sono renderizzati come immagini, impedendo l'estrazione o la modifica del testo.

## Cos'è la redazione del testo?
La redazione del testo è il processo di rimozione permanente o oscuramento delle informazioni sensibili — come identificatori personali, dati finanziari o clausole riservate — da un documento. A differenza del semplice trova‑sostituisci, la redazione garantisce che il contenuto nascosto non possa essere recuperato.

## Perché usare GroupDocs.Redaction per Java?
- **Tipi di redazione integrati** (exact phrase, regex, image, ecc.)  
- **Rasterizzazione con un click** per creare PDF sicuri  
- **Supporto multi‑formato** (DOCX, PPTX, XLSX, PDF, ecc.)  
- **API per sviluppatori** che si integra con progetti Java esistenti

## Prerequisiti
Prima di iniziare, assicurati di avere:

1. **Java Development Kit (JDK 11 o successivo)** e un IDE come IntelliJ IDEA o Eclipse.  
2. **Libreria GroupDocs.Redaction** (versione 24.9 o successiva).  
3. **Conoscenze di base di Java** — scriverai alcuni brevi snippet.  

## Configurazione di GroupDocs.Redaction per Java

### Installazione con Maven
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

### Download diretto
Se Maven non è la tua scelta, puoi scaricare il JAR dalla pagina ufficiale di rilascio: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### Acquisizione della licenza
- **Free Trial** – esplora l'API senza costi.  
- **Temporary License** – ideale per test prolungati.  
- **Full License** – necessaria per le distribuzioni in produzione.

### Inizializzazione di base
Apri un documento con la classe `Redactor`:

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Guida all'implementazione

### Come redigere testo in Java
Di seguito mostriamo una redazione per frase esatta, perfetta per rimuovere identificatori noti come il nome di una persona.

#### Passo 1: Importa le classi necessarie
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

#### Passo 2: Applica la redazione per frase esatta
Il frammento seguente sostituisce ogni occorrenza di **“John Doe”** con il segnaposto **[personal]**:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
} finally { 
    redactor.close(); 
}
```

**Perché funziona:**  
- `ExactPhraseRedaction` mira alla stringa letterale “John Doe”.  
- `ReplacementOptions` indica al motore cosa inserire al posto del testo originale.

**Suggerimenti e problemi comuni**  
- Verifica attentamente il percorso del documento; un percorso errato genera una `FileNotFoundException`.  
- Assicurati che il processo Java abbia i permessi di scrittura per la cartella di output.

### Come salvare come PDF rasterizzato
Dopo la redazione, probabilmente vorrai un PDF non modificabile. La rasterizzazione converte ogni pagina in un'immagine, rimuovendo la possibilità di selezionare o modificare il testo.

#### Passo 1: Importa `SaveOptions`
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
```

#### Passo 2: Configura e salva il PDF rasterizzato
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    SaveOptions tmp0 = new SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);

    redactor.save(tmp0);
} finally { 
    redactor.close(); 
}
```

**Spiegazione:**  
- `setAddSuffix(false)` mantiene il nome file originale (puoi abilitarlo per aggiungere “_redacted”).  
- `setRasterizeToPDF(true)` indica a GroupDocs di renderizzare ogni pagina come immagine all'interno di un PDF, garantendo che il documento sia **non modificabile**.

**Risoluzione dei problemi**  
- Se la rasterizzazione fallisce, verifica che il runtime Java includa le dipendenze di rendering PDF (sono incluse nella libreria).  

## Applicazioni pratiche
1. **Elaborazione di documenti legali** – redigere i nomi dei clienti prima di condividerli con la controparte.  
2. **Gestione dei record HR** – nascondere gli ID dei dipendenti nei report interni.  
3. **Reporting finanziario** – proteggere i numeri di conto quando si distribuiscono riepiloghi di audit.  

Puoi concatenare questi passaggi in un flusso di lavoro automatizzato, collegando GroupDocs.Redaction a un sistema di gestione documentale o a un bucket di storage cloud.

## Considerazioni sulle prestazioni
- **Elaborazione batch:** Riutilizza una singola istanza `Redactor` quando gestisci molti file per ridurre l'overhead.  
- **Gestione della memoria:** Per documenti di grandi dimensioni, chiama `System.gc()` dopo ogni `redactor.close()` o esegui il processo in una JVM separata.  
- **Mantieni le dipendenze aggiornate:** Le nuove versioni spesso includono ottimizzazioni delle prestazioni per la rasterizzazione PDF.

## Problemi comuni e soluzioni

| Issue | Solution |
|-------|----------|
| *File not found* | Verifica il percorso assoluto e assicurati che il file esista sul server. |
| *Permission denied* | Esegui la JVM con permessi OS sufficienti o modifica le ACL della cartella di output. |
| *Rasterization produces blank pages* | Conferma che il documento sorgente non sia già un'immagine raster; utilizza l'ultima versione della libreria. |
| *Redaction leaves hidden text* | Usa `ExactPhraseRedaction` con `ReplacementOptions`; evita metodi semplici di trova‑sostituisci. |

## Domande frequenti

**Q: Cos'è una redazione per frase esatta?**  
A: Sostituisce una stringa specifica (ad esempio, un nome) con un segnaposto, garantendo che il testo originale non possa essere recuperato.

**Q: Come migliora la sicurezza la rasterizzazione di un PDF?**  
A: I PDF rasterizzati renderizzano ogni pagina come immagine, impedendo la selezione, la copia o la modifica del testo.

**Q: Posso elaborare più file in un'unica esecuzione?**  
A: Sì — itera su un elenco di percorsi file, riutilizzando la stessa configurazione `Redactor` per ogni documento.

**Q: È possibile l'integrazione con il cloud?**  
A: Assolutamente. Puoi leggere/scrivere stream da AWS S3, Azure Blob o Google Cloud Storage e passarli direttamente all'API.

**Q: Quali sono gli ostacoli tipici per i principianti?**  
A: Dimenticare di chiudere il `Redactor` (che blocca i file) e utilizzare una versione della libreria obsoleta che non supporta la rasterizzazione.

## Risorse

- **Documentazione**: [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **Riferimento API**: [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs.Redaction GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Supporto gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Licenza temporanea**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**Ultimo aggiornamento:** 2026-02-24  
**Testato con:** GroupDocs.Redaction 24.9 per Java  
**Autore:** GroupDocs