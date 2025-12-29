---
date: '2025-12-29'
description: Scopri come redigere immagini di documenti scansionati usando GroupDocs.Redaction
  per Java. Guida passo‑passo che copre l'installazione, la redazione dell'area dell'immagine
  e la verifica.
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: Come censurare le immagini di documenti scannerizzati con GroupDocs in Java
type: docs
url: /it/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Come redigere le immagini di documenti scansionati con GroupDocs in Java

Nell'odierno panorama digitale, **redigere le immagini di documenti scansionati** è essenziale per proteggere la privacy e soddisfare i requisiti di conformità. Che tu debba nascondere dati personali in un contratto scansionato o oscurare i dettagli di un paziente in un'immagine medica, questo tutorial ti mostra **come redigere il contenuto di un'immagine** in modo rapido e affidabile usando **GroupDocs.Redaction per Java**. Ti guideremo passo passo, dalla configurazione del progetto alla verifica del successo della redazione, così potrai integrare la soluzione in qualsiasi applicazione Java con fiducia.

## Risposte rapide
- **Quale libreria gestisce la redazione delle immagini in Java?** GroupDocs.Redaction for Java  
- **Posso scegliere il colore della redazione?** Sì – qualsiasi `java.awt.Color` (ad es., `Color.BLUE`)  
- **È necessaria una licenza per la produzione?** Sì, è necessaria una licenza valida di GroupDocs  
- **L'immagine originale verrà sovrascritta?** No – salvi il risultato in un nuovo file  
- **Quale versione di Java è supportata?** Java 8+ (compatibile con JDK moderni)

## Che cos'è la redazione delle immagini e perché redigere le immagini di documenti scansionati?
La redazione delle immagini significa oscurare permanentemente informazioni visive sensibili — come nomi, numeri o firme — in modo che non possano essere recuperate. Quando lavori con documenti scansionati, i dati sono incorporati come pixel, rendendo inefficaci gli strumenti tradizionali di redazione del testo. Usare GroupDocs.Redaction ti consente di mirare a regioni di pixel precise e sostituirle con un colore solido, garantendo che l'informazione sia davvero rimossa.

## Prerequisiti
Prima di iniziare, assicurati di avere:

- **JDK 8 o successivo** installato  
- **Maven** (o un altro strumento di build) per la gestione delle dipendenze  
- Un IDE come **IntelliJ IDEA**, **Eclipse** o **NetBeans**  
- Conoscenze di base di Java e familiarità con I/O di file  

## Configurazione di GroupDocs.Redaction per Java

### Maven Setup
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
- **Licenza temporanea:** Usa una chiave temporanea per test più lunghi.  
- **Acquisto completo:** Ottieni una licenza di produzione per uso illimitato.

## Guida all'implementazione

Divideremo l'implementazione in due funzionalità principali: **Image Area Redaction** (il mascheramento vero e proprio) e **Redaction Status Check** (verifica del successo).

### Come redigere le immagini di documenti scansionati – Passo 1: Inizializzare il Redactor
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
Chiudi sempre il `Redactor` quando hai finito per liberare le risorse native.

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
- **Gestione di documenti riservati:** Maschera automaticamente i dati personali nei contratti scansionati prima di condividerli con parti esterne.  
- **Documentazione legale:** Garantisce la conformità a GDPR o HIPAA redigendo gli identificatori nelle immagini di prove.  
- **Cartelle cliniche:** Proteggi la privacy dei pazienti oscurando volti o note scritte a mano nelle immagini radiologiche.

## Considerazioni sulle prestazioni
- **Elaborazione batch:** Carica e redigi le immagini in piccoli lotti per mantenere basso l'uso della memoria.  
- **Strutture dati efficienti:** Riutilizza gli oggetti `Point` e `Dimension` quando elabori molte immagini.  
- **Rimani aggiornato:** Aggiorna regolarmente alla versione più recente di GroupDocs.Redaction per miglioramenti delle prestazioni e correzioni di bug.

## Problemi comuni e soluzioni
| Problema | Causa | Soluzione |
|----------|-------|-----------|
| **La redazione fallisce con stato `Failed`** | Percorso file errato o formato immagine non supportato | Verifica che l'immagine esista ed è in un formato supportato (JPG, PNG, BMP). |
| **Il file di output è vuoto** | `redactor.save()` chiamato prima che la redazione sia completata | Assicurati che `apply()` restituisca uno stato di successo prima di salvare. |
| **Il colore non viene applicato** | Uso di un colore trasparente | Scegli un `Color` opaco (ad es., `Color.BLACK` o `Color.BLUE`). |

## Domande frequenti

**D: Qual è la differenza tra `ImageAreaRedaction` e la redazione del testo?**  
R: `ImageAreaRedaction` opera su coordinate di pixel, mentre la redazione del testo analizza i layer OCR per individuare e rimuovere il contenuto testuale.

**D: Posso redigere più regioni in una singola immagine?**  
R: Sì — chiama `redactor.apply()` ripetutamente con diversi oggetti `ImageAreaRedaction` prima di salvare.

**D: GroupDocs.Redaction supporta altri formati immagine come TIFF?**  
R: La libreria supporta i formati raster più comuni (JPG, PNG, BMP, GIF). Per TIFF, converti prima in un formato supportato.

**D: Come automatizzare la redazione per una cartella di PDF scansionati?**  
R: Itera su ogni immagine di pagina estratta dal PDF, applica la stessa logica di redazione, quindi ricostruisci il PDF usando una libreria PDF.

**D: È possibile visualizzare un'anteprima della redazione prima di salvare?**  
R: Puoi renderizzare il `Redactor` in un `BufferedImage` e visualizzarlo in un'interfaccia Swing o JavaFX prima di confermare le modifiche.

## Conclusione
Ora disponi di una guida completa e pronta per la produzione su **come redigere il contenuto di un'immagine** e, in particolare, su **come redigere le immagini di documenti scansionati** usando GroupDocs.Redaction per Java. Seguendo i passaggi sopra, potrai proteggere dati visivi sensibili in una vasta gamma di settori. Esplora le API aggiuntive — come la redazione del testo o la redazione di pagine PDF — per costruire una soluzione completa di privacy dei dati per la tua organizzazione.

---

**Ultimo aggiornamento:** 2025-12-29  
**Testato con:** GroupDocs.Redaction 24.9 (Java)  
**Autore:** GroupDocs  

**Risorse**  
- [Documentazione](https://docs.groupdocs.com/redaction/java/)  
- [Riferimento API](https://reference.groupdocs.com/redaction/java)  
- [Download](https://releases.groupdocs.com/redaction/java/)  
- [Repository GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/redaction/33)  
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)