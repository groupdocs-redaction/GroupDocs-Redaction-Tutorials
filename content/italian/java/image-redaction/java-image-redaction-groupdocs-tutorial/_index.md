---
date: '2026-03-22'
description: Scopri come redigere immagini scannerizzate in Java con GroupDocs.Redaction.
  Questa guida passo‑passo copre l'installazione, la redazione dell'area dell'immagine
  e la verifica.
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: Come censurare un'immagine scannerizzata in Java usando GroupDocs
type: docs
url: /it/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Come redigere immagini scannerizzate java usando GroupDocs

Nell'odierno panorama digitale, **redact scanned image java** è essenziale per proteggere la privacy e soddisfare i requisiti di conformità. Che tu debba nascondere dati personali in un contratto scannerizzato o oscurare i dettagli di un paziente in un'immagine medica, questo tutorial ti mostra **come redigere l'immagine** rapidamente e in modo affidabile usando **GroupDocs.Redaction for Java**. Ti guideremo passo passo dall'impostazione del progetto alla verifica del successo della redazione, così potrai integrare la soluzione in qualsiasi applicazione Java con fiducia.

## Risposte rapide
- **Quale libreria gestisce la redazione delle immagini in Java?** GroupDocs.Redaction for Java  
- **Posso scegliere il colore della redazione?** Sì – qualsiasi `java.awt.Color` (ad es., `Color.BLUE`)  
- **È necessaria una licenza per la produzione?** Sì, è necessaria una licenza valida di GroupDocs  
- **L'immagine originale verrà sovrascritta?** No – il risultato viene salvato in un nuovo file  
- **Quale versione di Java è supportata?** Java 8+ (compatibile con JDK moderni)

## Cos'è la redazione delle immagini e perché redigere immagini scannerizzate java?
La redazione delle immagini significa oscurare permanentemente informazioni visive sensibili — come nomi, numeri o firme — in modo che non possano essere recuperate. Quando lavori con documenti scannerizzati, i dati sono incorporati come pixel, rendendo inefficaci gli strumenti tradizionali di redazione del testo. Usare GroupDocs.Redaction ti consente di mirare a regioni di pixel precise e sostituirle con un colore solido, garantendo che le informazioni siano davvero rimosse.

## Prerequisiti
- **JDK 8 o successivo** installato  
- **Maven** (o un altro strumento di build) per la gestione delle dipendenze  
- Un IDE come **IntelliJ IDEA**, **Eclipse** o **NetBeans**  
- Conoscenze di base di Java e familiarità con file I/O  

## Configurazione di GroupDocs.Redaction per Java

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

### Download diretto
In alternativa, scarica l'ultimo JAR dalla pagina ufficiale di rilascio: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisizione della licenza
- **Prova gratuita:** Registrati per una prova per esplorare l'API.  
- **Licenza temporanea:** Usa una chiave temporanea per test estesi.  
- **Acquisto completo:** Ottieni una licenza di produzione per uso illimitato.

## Guida all'implementazione

Divideremo l'implementazione in due funzionalità principali: **Image Area Redaction** (la mascheratura effettiva) e **Redaction Status Check** (verifica del successo).

### Come redigere immagini di documenti scannerizzati – Passo 1: Inizializzare il Redactor
Per prima cosa, crea un'istanza di `Redactor` che punti all'immagine da elaborare.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Passo 2: Definire i parametri di redazione
Specifica l'angolo in alto a sinistra (`Point`) e le dimensioni (`Dimension`) del rettangolo da nascondere. In questo esempio usiamo un riempimento blu.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Passo 3: Applicare la redazione
Crea un oggetto `ImageAreaRedaction` con `RegionReplacementOptions` ed eseguilo. Il metodo restituisce un `RedactorChangeLog` che indica se l'operazione è riuscita.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Passo 4: Rilasciare le risorse
Chiudi sempre il `Redactor` al termine per liberare le risorse native.

```java
redactor.close();
```

### Come verificare la redazione – Controllo dello stato
Dopo aver applicato la redazione, puoi ispezionare il `RedactorChangeLog` per confermare che l'operazione non sia fallita.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Applicazioni pratiche
- **Gestione di documenti riservati:** Maschera automaticamente i dati personali nei contratti scannerizzati prima di condividerli con parti esterne.  
- **Documentazione legale:** Garantisce la conformità a GDPR o HIPAA redigendo gli identificatori nelle immagini di prova.  
- **Cartelle cliniche:** Protegge la privacy dei pazienti oscurando volti o note scritte a mano nelle immagini radiologiche.

## Considerazioni sulle prestazioni
- **Elaborazione batch:** Carica e redigi le immagini in piccoli batch per mantenere basso l'uso della memoria.  
- **Strutture dati efficienti:** Riutilizza gli oggetti `Point` e `Dimension` durante l'elaborazione di molte immagini.  
- **Rimani aggiornato:** Aggiorna regolarmente alla versione più recente di GroupDocs.Redaction per miglioramenti delle prestazioni e correzioni di bug.

## Problemi comuni e soluzioni

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| **La redazione fallisce con stato `Failed`** | Percorso file errato o formato immagine non supportato | Verifica che l'immagine esista ed è in un formato supportato (JPG, PNG, BMP). |
| **Il file di output è vuoto** | `redactor.save()` chiamato prima che la redazione sia completata | Assicurati che `apply()` restituisca uno stato di successo prima di salvare. |
| **Il colore non è stato applicato** | Uso di un colore trasparente | Scegli un `Color` opaco (ad es., `Color.BLACK` o `Color.BLUE`). |

## Domande frequenti

**D: Qual è la differenza tra `ImageAreaRedaction` e la redazione del testo?**  
R: `ImageAreaRedaction` opera su coordinate pixel, mentre la redazione del testo analizza i layer OCR per individuare e rimuovere il contenuto testuale.

**D: Posso redigere più regioni in una singola immagine?**  
R: Sì — chiama `redactor.apply()` più volte con diversi oggetti `ImageAreaRedaction` prima di salvare.

**D: GroupDocs.Redaction supporta altri formati immagine come TIFF?**  
R: La libreria supporta i formati raster comuni (JPG, PNG, BMP, GIF). Per TIFF, converti prima in un formato supportato.

**D: Come automatizzare la redazione per una cartella di PDF scannerizzati?**  
R: Itera su ogni immagine di pagina estratta dal PDF, applica la stessa logica di redazione, quindi ricostruisci il PDF usando una libreria PDF.

**D: Esiste un modo per visualizzare l'anteprima della redazione prima di salvare?**  
R: Puoi renderizzare il `Redactor` in un `BufferedImage` e visualizzarlo in un'interfaccia Swing o JavaFX prima di confermare le modifiche.

## Conclusione
Ora hai una guida completa, pronta per la produzione, su **come redigere l'immagine** e, in particolare, su **come redigere immagini scannerizzate java** usando GroupDocs.Redaction per Java. Seguendo i passaggi sopra, puoi proteggere i dati visivi sensibili in un'ampia gamma di settori. Esplora le API aggiuntive — come la redazione del testo o la redazione di pagine PDF — per costruire una soluzione completa di privacy dei dati per la tua organizzazione.

**Risorse**  
- [Documentation](https://docs.groupdocs.com/redaction/java/)  
- [API Reference](https://reference.groupdocs.com/redaction/java)  
- [Download](https://releases.groupdocs.com/redaction/java/)  
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**Ultimo aggiornamento:** 2026-03-22  
**Testato con:** GroupDocs.Redaction 24.9 (Java)  
**Autore:** GroupDocs