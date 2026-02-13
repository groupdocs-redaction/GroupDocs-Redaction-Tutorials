---
date: '2026-02-13'
description: Scopri come creare PDF in scala di grigi usando GroupDocs.Redaction per
  Java, converti PDF in scala di grigi in modo sicuro mantenendo la qualità del documento.
keywords:
- GroupDocs.Redaction
- Java
- Document Processing
title: Come creare un PDF in scala di grigi con GroupDocs.Redaction Java – Proteggi
  e ottimizza i tuoi documenti
type: docs
url: /it/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

 maybe.

But keep same heading levels.

Translate content.

Let's write.

# GroupDocs.Redaction Java: Guida alla rasterizzazione in scala di grigi

## Introduzione

Se hai bisogno di **creare PDF in scala di grigi** mantenendo i tuoi documenti sicuri e dall’aspetto professionale, sei nel posto giusto. In questo tutorial percorreremo passo dopo passo le fasi esatte per convertire file DOCX, PDF o altri formati supportati, ricchi di colori, in una versione rasterizzata in scala di grigi pulita, utilizzando GroupDocs.Redaction per Java. Imparerai perché la rasterizzazione aggiunge un ulteriore livello di sicurezza, come configurare la libreria e come gestire le risorse in modo efficiente—tutto in uno stile conversazionale e step‑by‑step.

## Risposte rapide
- **Cosa fa la rasterizzazione in scala di grigi?** Converte ogni pagina di un documento in un’immagine ad alta risoluzione e poi applica un filtro in scala di grigi, rimuovendo tutte le informazioni di colore.  
- **Perché usare GroupDocs.Redaction per questo?** Combina la sicurezza della redazione con potenti opzioni di rasterizzazione in una singola API.  
- **Quali formati sono supportati?** DOCX, PDF, XLSX, PPTX, RTF e molti altri.  
- **È necessaria una licenza?** È richiesta una licenza valida di GroupDocs.Redaction per l’uso in produzione; è disponibile una versione di prova per i test.  
- **Quale versione di Java è necessaria?** JDK 8 o superiore.

## Cos’è **creare PDF in scala di grigi**?

Creare un PDF in scala di grigi significa convertire ogni elemento visivo del documento originale in sfumature di grigio. Il risultato è un file più piccolo, adatto alla stampa, che elimina le distrazioni legate al colore e aggiunge un lieve beneficio di sicurezza perché il contenuto diventa basato su immagine.

## Perché utilizzare la rasterizzazione in scala di grigi con GroupDocs.Redaction?

- **Sicurezza potenziata** – le pagine rasterizzate non possono essere selezionate, copiate o modificate come testo.  
- **Aspetto coerente** – i colori vengono rimossi, garantendo un look uniforme e professionale.  
- **Ampio supporto di formati** – la stessa API funziona per DOCX, PDF, PPTX e altri.  
- **Controllo fine‑tuned** – è possibile regolare DPI, formato di output e opzioni avanzate come la conversione in scala di grigi.

## Prerequisiti

- Java Development Kit (JDK) 8 o più recente. Verifica con `java -version`.  
- Un IDE (IntelliJ IDEA, Eclipse o NetBeans) per semplificare la scrittura e il debug del codice.  
- GroupDocs.Redaction per Java aggiunto tramite Maven o Gradle.  
- Un documento di esempio (ad esempio un DOCX multi‑pagina) su cui sperimentare in sicurezza.  
- Spazio disco sufficiente per l’output rasterizzato (i file raster possono essere più grandi dell’originale).

## Importare i pacchetti

Impostare le importazioni corrette è come organizzare la tua cassetta degli attrezzi prima di un progetto. Le seguenti importazioni ti danno accesso alla classe core `Redactor` e alle opzioni di rasterizzazione di cui avremo bisogno.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Passo 1: Inizializzare l’oggetto Redactor

Creare un’istanza di `Redactor` apre la porta a tutte le capacità di elaborazione dei documenti.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

Sostituisci `Constants.MULTIPAGE_SAMPLE_DOCX` con il percorso del file che desideri convertire in PDF in scala di grigi.

## Passo 2: Configurare le opzioni di salvataggio

`SaveOptions` definisce come verrà scritto il file finale. Aggiungere un suffisso ti aiuta a mantenere intatto il file originale.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

L’output sarà denominato `yourfile_scan.docx` (o il formato che specificherai successivamente).

## Passo 3: Abilitare la rasterizzazione

Attivare la rasterizzazione indica al motore di renderizzare ogni pagina come immagine prima del salvataggio.

```java
so.getRasterization().setEnabled(true);
```

La rasterizzazione è la base per creare un PDF in scala di grigi perché converte il documento in una rappresentazione basata su immagine.

## Passo 4: Applicare la conversione in scala di grigi

Ora aggiungiamo il filtro in scala di grigi alla pipeline di rasterizzazione.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

Questa opzione forza ogni pixel a essere renderizzato in sfumature di grigio, fornendoti il risultato **creare PDF in scala di grigi** desiderato.

## Passo 5: Eseguire la trasformazione del documento

La chiamata `save` esegue l’intera catena di elaborazione.

```java
redactor.save(so);
```

Dopo l’esecuzione di questa riga, troverai un nuovo file su disco completamente rasterizzato, in scala di grigi e salvato con il suffisso `_scan`.

## Passo 6: Gestione corretta delle risorse

Pulire le risorse previene blocchi di file e perdite di memoria.

```java
finally { redactor.close(); }
```

Per Java moderno puoi anche utilizzare il pattern *try‑with‑resources*, che chiude automaticamente il `Redactor`:

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

Entrambi gli approcci sono sicuri; il secondo è più conciso.

## Opzioni di configurazione avanzate

### Regolare il DPI per qualità o dimensione

Un DPI più alto produce immagini più nitide (ideale per la stampa), mentre un DPI più basso riduce le dimensioni del file.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Scegliere un formato di output

Puoi forzare il risultato rasterizzato in un formato contenitore specifico, ad esempio PDF.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Casi d’uso comuni

- **Archiviazione di documenti legali** – crea PDF in scala di grigi immutabili che non possono essere modificati.  
- **Report pronti per la stampa** – garantisci un output coerente in bianco e nero per stampe di massa.  
- **Flussi di lavoro di conformità** – combina la redazione con la rasterizzazione in scala di grigi per soddisfare normative rigorose sulla privacy dei dati.

## Problemi comuni e soluzioni

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| Il file di output è più grande del previsto | DPI impostato troppo alto o compressione immagine disabilitata | Riduci il DPI (es. 150) o abilita la compressione in `RasterizationOptions`. |
| Il testo appare sfocato | DPI insufficiente per la dimensione del carattere originale | Aumenta il DPI a 300 o più. |
| Il processo genera `OutOfMemoryError` su documenti grandi | L’intero documento viene caricato in memoria | Usa le API di streaming o elabora le pagine in batch, se supportato. |
| La scala di grigi non viene applicata | Opzione avanzata non aggiunta correttamente | Verifica che `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` sia chiamato prima di `save()`. |

## Domande frequenti

**D: Posso convertire i documenti in scala di grigi senza rasterizzazione?**  
R: In GroupDocs.Redaction, l’opzione scala di grigi è legata alla rasterizzazione, che garantisce risultati coerenti e aggiunge sicurezza.

**D: Quali formati di documento supportano la rasterizzazione in scala di grigi?**  
R: Tutti i principali formati supportati da GroupDocs.Redaction—including DOCX, PDF, XLSX, PPTX, RTF e altri—possono essere rasterizzati e convertiti in scala di grigi.

**D: La rasterizzazione influirà sulla dimensione dei miei documenti?**  
R: Sì. I file con molto testo possono aumentare, mentre quelli con molte immagini potrebbero ridursi. Le impostazioni DPI hanno l’impatto maggiore.

**D: È possibile invertire il processo di rasterizzazione in scala di grigi?**  
R: No. La rasterizzazione è unidirezionale; conserva una copia di backup dell’originale se devi tornare indietro.

**D: Come posso ottimizzare la qualità dei documenti rasterizzati in scala di grigi?**  
R: Usa un DPI più alto (300 + per qualità di stampa) e scegli un formato di output appropriato (PDF è comune per l’archiviazione).

## Conclusione

Ora disponi di una ricetta completa, pronta per la produzione, per **creare PDF in scala di grigi** usando GroupDocs.Redaction per Java. Abilitando la rasterizzazione, aggiungendo l’opzione avanzata di scala di grigi e gestendo le risorse in modo responsabile, potrai produrre documenti sicuri, pronti per la stampa e conformi agli standard di compliance.

---

**Ultimo aggiornamento:** 2026-02-13  
**Testato con:** GroupDocs.Redaction 23.11 per Java  
**Autore:** GroupDocs  

---