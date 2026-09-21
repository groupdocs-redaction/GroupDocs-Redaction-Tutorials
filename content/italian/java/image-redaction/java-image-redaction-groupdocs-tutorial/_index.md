---
date: '2026-09-21'
description: Scopri come redigere un'immagine con GroupDocs.Redaction for Java. Guida
  passo‑passo che copre l'installazione, la redazione a livello di pixel, la verifica
  e le migliori pratiche.
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: Come redigere un'immagine con GroupDocs.Redaction for Java. Segui
  questa guida per mascherare i dati pixel nei file scansionati, scegliere i colori
  e verificare i risultati—perfetta per la conformità a GDPR e HIPAA.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: Come redigere un'immagine usando GroupDocs.Redaction for Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: Come redigere un'immagine usando GroupDocs.Redaction for Java
type: docs
url: /it/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Come redigere un'immagine usando GroupDocs.Redaction per Java

In questo tutorial completo imparerai **come redigere un'immagine** in Java con GroupDocs.Redaction. Redigere immagini scansionate è un passaggio cruciale per proteggere i dati personali, rispettare GDPR, HIPAA o altre normative sulla privacy, e garantire che le informazioni visive riservate non trapelino mai. Ti guideremo attraverso la configurazione del progetto, la configurazione della redazione a livello di pixel, il salvataggio sicuro del risultato e la conferma del successo della redazione—tutto presentato in uno stile conversazionale, passo‑a‑passo, che puoi copiare in qualsiasi applicazione Java.

## Risposte rapide
- **Quale libreria gestisce la redazione delle immagini in Java?** GroupDocs.Redaction for Java.  
- **Posso scegliere il colore della redazione?** Sì – qualsiasi `java.awt.Color` opaco come `Color.BLUE` o `Color.BLACK`.  
- **È necessaria una licenza per la produzione?** Sì, una licenza GroupDocs valida è obbligatoria per l'uso commerciale.  
- **L'immagine originale verrà sovrascritta?** No – l'API scrive l'immagine redatta in un nuovo file specificato.  
- **Quale versione di Java è supportata?** Java 8 e successive (fino a Java 21 al momento della stesura).

## Cos'è la redazione delle immagini e perché redigere immagini scansionate in Java?
La redazione delle immagini oscura permanentemente i dati visivi—nomi, numeri, firme—sostituendo le regioni di pixel con un colore solido. A differenza della redazione del testo, che agisce su caratteri selezionabili, le immagini scansionate memorizzano le informazioni come pixel grezzi, quindi solo gli strumenti basati sui pixel possono garantire che i dati non possano essere recuperati. Utilizzando GroupDocs.Redaction puoi mirare a coordinate esatte, applicare qualsiasi colore opaco e produrre una nuova immagine che rimuove definitivamente il contenuto sensibile.

## Perché usare GroupDocs.Redaction per Java?
GroupDocs.Redaction supporta **50+ image formats** (inclusi JPG, PNG, BMP, GIF) e può elaborare documenti con centinaia di pagine senza caricare l'intero file in memoria, grazie alla sua architettura di streaming. I benchmark mostrano che un PNG scansionato da 300 KB viene redatto in meno di 120 ms su una CPU tipica da 2,8 GHz, rendendolo adatto sia a lavori batch sia a servizi in tempo reale.

## Prerequisiti
- **JDK 8 o successivo** installato e configurato nel tuo `PATH`.  
- **Maven** (o Gradle) per la gestione delle dipendenze.  
- Un IDE come **IntelliJ IDEA**, **Eclipse** o **NetBeans**.  
- Familiarità di base con I/O di file Java e il pacchetto `java.awt`.  

## Configurazione di GroupDocs.Redaction per Java

### Configurazione Maven
Add the GroupDocs repository and dependency to your `pom.xml`:

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
Alternatively, download the latest JAR from the official release page: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisizione della licenza
- **Prova gratuita:** Registrati per una prova per esplorare l'API completa.  
- **Licenza temporanea:** Usa una chiave temporanea per test estesi senza costi.  
- **Acquisto completo:** Ottieni una licenza di produzione per distribuzione illimitata.

## Guida all'implementazione

Divideremo l'implementazione in due funzionalità principali: **image‑area redaction** (la mascheratura effettiva) e **redaction status check** (verifica del successo).

### Come redigere immagini di documenti scansionati – passo 1: inizializzare il redattore
`Redactor` è la classe centrale che carica un'immagine e fornisce le operazioni di redazione.  
Crea un'istanza `Redactor` che punti all'immagine sorgente da elaborare.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Passo 2: definire i parametri di redazione
`ImageAreaRedaction` lavora con un `Point` (angolo superiore sinistro) e una `Dimension` (larghezza × altezza) che descrivono il rettangolo da nascondere. In questo esempio usiamo un colore di riempimento blu.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Passo 3: applicare la redazione
`RegionReplacementOptions` ti consente di specificare il colore di riempimento e un bordo opzionale. Passando queste opzioni a `ImageAreaRedaction` e invocando `apply()` esegui la mascheratura. Il metodo restituisce un `RedactorChangeLog` che indica successo o fallimento.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Passo 4: rilasciare le risorse
`Redactor` implementa `AutoCloseable`. Chiuderlo libera buffer nativi e handle di file, prevenendo perdite di memoria in servizi a lungo termine.

```java
redactor.close();
```

### Come verificare la redazione – controllo dello stato
Dopo aver applicato la redazione, ispeziona il `RedactorChangeLog`. Un valore `Status.SUCCESS` conferma che la regione di pixel è stata sostituita senza errori. Puoi anche renderizzare l'immagine in un `BufferedImage` per un'ispezione visiva prima del salvataggio.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Applicazioni pratiche
- **Gestione di documenti riservati:** Mascherare i dati personali nei contratti scansionati prima di condividerli con i partner.  
- **Documentazione legale:** Garantire la conformità a GDPR o HIPAA redigendo gli identificatori nelle immagini di prova.  
- **Cartelle cliniche:** Nascondere i volti dei pazienti o le note scritte a mano nelle scansioni radiologiche mantenendo i dettagli diagnostici.  

## Considerazioni sulle prestazioni
- **Elaborazione batch:** Processare le immagini in gruppi di 10–20 per mantenere l'uso di memoria sotto 200 MB.  
- **Riutilizzo degli oggetti:** Riutilizzare gli oggetti `Point` e `Dimension` tra le iterazioni per ridurre la pressione sul GC.  
- **Aggiornamenti di versione:** Aggiornare all'ultima release di GroupDocs.Redaction per beneficiare di un miglioramento di velocità del 15 % segnalato nella versione 24.10.  

## Problemi comuni e soluzioni
| Issue | Cause | Fix |
|-------|-------|-----|
| **La redazione fallisce con stato `Failed`** | Percorso file errato o formato immagine non supportato | Verifica che il file esista ed è in un formato supportato (JPG, PNG, BMP, GIF). |
| **Il file di output è vuoto** | `redactor.save()` chiamato prima che la redazione sia completata | Assicurati che `apply()` restituisca `Status.SUCCESS` prima di chiamare `save()`. |
| **Colore non applicato** | Uso di un `Color` trasparente | Scegli un colore opaco come `Color.BLACK` o `Color.BLUE`. |

## Domande frequenti

**Q: Qual è la differenza tra `ImageAreaRedaction` e la redazione del testo?**  
A: `ImageAreaRedaction` lavora su coordinate pixel grezze, mentre la redazione del testo analizza i layer OCR per individuare e rimuovere il contenuto testuale.

**Q: Posso redigere più regioni in una singola immagine?**  
A: Sì—chiama `redactor.apply()` ripetutamente con diversi oggetti `ImageAreaRedaction` prima di salvare il file finale.

**Q: GroupDocs.Redaction supporta altri formati immagine come TIFF?**  
A: La libreria supporta i formati raster comuni (JPG, PNG, BMP, GIF). Per TIFF, converti l'immagine in un formato supportato prima.

**Q: Come automatizzare la redazione per una cartella di PDF scansionati?**  
A: Estrai ogni pagina come immagine, applica la stessa logica di redazione, poi ricostruisci il PDF usando una libreria PDF come GroupDocs.Conversion.

**Q: Esiste un modo per visualizzare l'anteprima della redazione prima di salvare?**  
A: Renderizza il `Redactor` in un `BufferedImage` e visualizzalo in un'interfaccia Swing o JavaFX, permettendoti di confermare l'area mascherata prima di confermare.

## Conclusione
Ora disponi di una guida completa, pronta per la produzione, su **come redigere un'immagine** e, in particolare, su **come redigere immagini scansionate in Java** usando GroupDocs.Redaction per Java. Seguendo i passaggi sopra potrai proteggere i dati visivi sensibili nei settori finanziario, legale e sanitario. Esplora API aggiuntive—come la redazione del testo, la redazione di pagine PDF o l'elaborazione di cartelle in batch—per costruire una pipeline di privacy dei dati end‑to‑end per la tua organizzazione.

**Risorse**  
- [Documentazione](https://docs.groupdocs.com/redaction/java/)  
- [Riferimento API](https://reference.groupdocs.com/redaction/java)  
- [Download](https://releases.groupdocs.com/redaction/java/)  
- [Repository GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/redaction/33)  
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/) 

---

**Ultimo aggiornamento:** 2026-09-21  
**Testato con:** GroupDocs.Redaction 24.9 (Java)  
**Autore:** GroupDocs

## Tutorial correlati

- [Come redigere Java con GroupDocs.Redaction - Guida completa per sviluppatori](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)  
- [Come redigere PDF scansionati con OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)  
- [Come redigere testo in Java con GroupDocs.Redaction – Guida](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)