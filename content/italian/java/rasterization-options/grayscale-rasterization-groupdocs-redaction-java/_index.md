---
date: '2026-05-17'
description: Scopri come rasterizzare PDF in scala di grigi usando GroupDocs.Redaction
  per Java, applicare un filtro in scala di grigi e mantenere i tuoi documenti sicuri
  e di alta qualità.
keywords:
- how to rasterize pdf
- java pdf to image
- apply grayscale filter pdf
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to rasterize PDF to grayscale using GroupDocs.Redaction for
    Java, apply a grayscale filter, and keep your documents secure and high‑quality.
  headline: How to rasterize PDF to grayscale with GroupDocs.Redaction Java – Secure
    and Optimize Your Documents
  type: TechArticle
- questions:
  - answer: In GroupDocs.Redaction, the grayscale option is tied to rasterization,
      which ensures consistent results and adds a security layer.
    question: Can I convert documents to grayscale without rasterization?
  - answer: All major formats supported by GroupDocs.Redaction—including DOCX, PDF,
      XLSX, PPTX, RTF, and more than 100 others—can be rasterized and converted to
      grayscale.
    question: What document formats support grayscale rasterization?
  - answer: Yes. Text‑heavy files may grow, while image‑heavy files might shrink.
      DPI settings have the biggest impact.
    question: Will rasterization affect the file size of my documents?
  - answer: No. Rasterization is one‑way; keep a backup of the original if you need
      to revert.
    question: Is it possible to reverse the grayscale rasterization process?
  - answer: Use a higher DPI (300 + for print quality) and choose PDF as the output
      format for best archival results.
    question: How can I optimize the quality of grayscale rasterized documents?
  type: FAQPage
title: Come rasterizzare PDF in scala di grigi con GroupDocs.Redaction Java – Proteggi
  e ottimizza i tuoi documenti
type: docs
url: /it/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# Come rasterizzare PDF in scala di grigi con GroupDocs.Redaction Java

Se hai bisogno di **rasterizzare un PDF** in scala di grigi mantenendo i tuoi documenti sicuri, dall'aspetto professionale e facili da archiviare, sei nel posto giusto. In questo tutorial ti guideremo passo passo nella conversione di file DOCX, PDF o altri supportati, colorati, in una versione rasterizzata pulita in scala di grigi usando GroupDocs.Redaction per Java. Capirai perché la rasterizzazione aggiunge un livello di sicurezza, come configurare la libreria e come gestire le risorse in modo efficiente—tutto presentato in uno stile amichevole, passo dopo passo.

## Risposte rapide
- **Cosa fa la rasterizzazione in scala di grigi?** Converte ogni pagina in un'immagine ad alta risoluzione e poi applica un filtro in scala di grigi, rimuovendo tutte le informazioni di colore.  
- **Perché usare GroupDocs.Redaction per questo?** Unisce la sicurezza della redazione con le opzioni di rasterizzazione in una singola API facile da usare.  
- **Quali formati sono supportati?** DOCX, PDF, XLSX, PPTX, RTF e più di 100 altri formati.  
- **È necessaria una licenza?** È richiesta una licenza valida di GroupDocs.Redaction per la produzione; è disponibile una prova gratuita per i test.  
- **Quale versione di Java è richiesta?** JDK 8 o superiore.

## Come rasterizzare PDF in scala di grigi?

Carica il tuo documento sorgente con `new Redactor("path/to/file")`, abilita la rasterizzazione tramite `RasterizationOptions`, aggiungi l'opzione avanzata per la scala di grigi e chiama `save()` — l'intera conversione avviene in poche righe concise. Questo approccio garantisce che ogni pagina diventi un PDF basato su immagine, in bianco e nero, impedendo la selezione del testo e assicurando un aspetto uniforme pronto per la stampa.

## Cos'è **create grayscale pdf**?

Creare un PDF in scala di grigi significa convertire ogni elemento visivo del documento originale in tonalità di grigio. Il risultato è un file più piccolo, adatto alla stampa, che elimina le distrazioni legate al colore e aggiunge un sottile vantaggio di sicurezza poiché il contenuto è ora basato su immagine.

## Perché usare la rasterizzazione in scala di grigi con GroupDocs.Redaction?

La rasterizzazione trasforma ogni pagina in un'immagine, il che significa che il testo non può essere copiato o modificato, e l'output visivo rimane coerente su stampanti e visualizzatori. GroupDocs.Redaction supporta **oltre 100 formati di input e output** — inclusi DOCX, XLSX, PPTX, HTML e tipi di immagine — così puoi applicare lo stesso flusso di lavoro praticamente a qualsiasi documento.

## Prerequisiti

- Java Development Kit (JDK) 8 o più recente. Verifica con `java -version`.  
- Un IDE (IntelliJ IDEA, Eclipse o NetBeans) per una programmazione e debug più semplici.  
- GroupDocs.Redaction per Java aggiunto tramite Maven o Gradle.  
- Un documento di esempio (ad esempio, un DOCX multipagina) su cui puoi sperimentare in sicurezza.  
- Spazio su disco sufficiente per l'output rasterizzato (i file raster possono essere più grandi dell'originale).

## Importa pacchetti

Le seguenti importazioni includono le classi core Redactor e di rasterizzazione necessarie per l'esempio.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Passo 1: Inizializza l'oggetto Redactor

La classe `Redactor` è il punto di ingresso per tutte le operazioni di elaborazione dei documenti in GroupDocs.Redaction. Creare un'istanza apre la porta al caricamento, alla modifica e al salvataggio dei documenti.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

Sostituisci `Constants.MULTIPAGE_SAMPLE_DOCX` con il percorso del file che desideri convertire in un PDF in scala di grigi.

## Passo 2: Configura le opzioni di salvataggio

La classe `SaveOptions` definisce come il documento elaborato verrà scritto su disco, includendo formato e nome file.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

L'output sarà nominato `yourfile_scan.pdf` (o il formato che specificherai in seguito).

## Passo 3: Abilita la rasterizzazione

L'oggetto `RasterizationOptions` abilita il rendering basato su immagine di ogni pagina prima del salvataggio.

```java
so.getRasterization().setEnabled(true);
```

## Passo 4: Applica la conversione in scala di grigi

`AdvancedRasterizationOptions.Grayscale` è un flag che forza l'immagine rasterizzata a utilizzare solo tonalità di grigio.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

## Passo 5: Esegui la trasformazione del documento

Chiamare `save()` esegue l'intera pipeline di elaborazione e scrive il file di output.

```java
redactor.save(so);
```

Dopo l'esecuzione di questa riga, troverai un nuovo file su disco completamente rasterizzato, in scala di grigi, e salvato con il suffisso `_scan`.

## Passo 6: Gestione corretta delle risorse

Il metodo `close()` rilascia le risorse native ed elimina i file temporanei.

```java
finally { redactor.close(); }
```

Per Java moderno puoi anche usare il pattern try‑with‑resources, che chiude automaticamente il `Redactor`:

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

Entrambi gli approcci sono sicuri; il secondo è più conciso.

## Opzioni di configurazione avanzate

### Regola DPI per qualità o dimensione

Un DPI più alto produce immagini più nitide (buono per la stampa), mentre un DPI più basso riduce la dimensione del file. Un equilibrio comune è 150 DPI per la visualizzazione su schermo e 300 DPI per PDF pronti per la stampa.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Scegli un formato di output

Puoi forzare il risultato rasterizzato in un formato contenitore specifico, come PDF, TIFF o PNG. PDF è il formato di archiviazione più diffuso.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Casi d'uso comuni

- **Archiviazione di documenti legali** – crea PDF in scala di grigi immutabili che non possono essere modificati.  
- **Report pronti per la stampa** – garantisce un output in bianco e nero coerente per stampe di massa.  
- **Flussi di lavoro di conformità** – combina la redazione con la rasterizzazione in scala di grigi per soddisfare normative severe sulla privacy dei dati.

## Problemi comuni e soluzioni

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| Il file di output è più grande del previsto | DPI impostato troppo alto o compressione immagine disabilitata | Riduci DPI (es., 150) o abilita la compressione in `RasterizationOptions`. |
| Il testo appare sfocato | DPI insufficiente per la dimensione del carattere originale | Aumenta DPI a 300 o più. |
| Il processo genera `OutOfMemoryError` su documenti grandi | L'intero documento viene caricato in memoria | Usa API di streaming o elabora le pagine in batch se supportato. |
| La scala di grigi non è applicata | Opzione avanzata non aggiunta correttamente | Verifica che `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` sia chiamato prima di `save()`. |

## Domande frequenti

**D: Posso convertire i documenti in scala di grigi senza rasterizzazione?**  
R: In GroupDocs.Redaction, l'opzione scala di grigi è legata alla rasterizzazione, che garantisce risultati coerenti e aggiunge un livello di sicurezza.

**D: Quali formati di documento supportano la rasterizzazione in scala di grigi?**  
R: Tutti i principali formati supportati da GroupDocs.Redaction — inclusi DOCX, PDF, XLSX, PPTX, RTF e più di 100 altri — possono essere rasterizzati e convertiti in scala di grigi.

**D: La rasterizzazione influenzerà la dimensione dei file dei miei documenti?**  
R: Sì. I file con molto testo possono aumentare di dimensione, mentre quelli con molte immagini potrebbero ridursi. Le impostazioni DPI hanno l'impatto maggiore.

**D: È possibile invertire il processo di rasterizzazione in scala di grigi?**  
R: No. La rasterizzazione è unidirezionale; conserva una copia di backup dell'originale se devi tornare indietro.

**D: Come posso ottimizzare la qualità dei documenti rasterizzati in scala di grigi?**  
R: Usa un DPI più alto (300 + per qualità di stampa) e scegli PDF come formato di output per i migliori risultati di archiviazione.

## Conclusione

Ora hai una ricetta completa, pronta per la produzione, per **rasterizzare PDF in scala di grigi** usando GroupDocs.Redaction per Java. Abilitando la rasterizzazione, aggiungendo l'opzione avanzata per la scala di grigi e gestendo le risorse in modo responsabile, puoi produrre documenti sicuri, adatti alla stampa, che soddisfano gli standard di conformità e hanno un aspetto coerente su qualsiasi visualizzatore.

---

**Ultimo aggiornamento:** 2026-05-17  
**Testato con:** GroupDocs.Redaction 23.11 for Java  
**Autore:** GroupDocs  

---

## PAROLE CHIAVE TARGET:

**Parola chiave primaria (MASSIMA PRIORITÀ):**  
how to rasterize pdf

**Parole chiave secondarie (SUPPORTO):**  
java pdf to image, apply grayscale filter pdf

## Tutorial correlati

- [Tutorial sulle opzioni di rasterizzazione per GroupDocs.Redaction Java](/redaction/java/rasterization-options/)
- [Come usare groupdocs redaction per Java: Pre‑Rasterizzazione nei documenti Word](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)
- [Rasterizzazione di rumore personalizzata in Java: Proteggi le informazioni sensibili con GroupDocs.Redaction](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)