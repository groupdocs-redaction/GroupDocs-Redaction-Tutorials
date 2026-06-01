---
date: '2026-02-26'
description: Scopri come redigere il testo usando GroupDocs.Redaction Java e salvarlo
  come PDF rasterizzato con sostituzione esatta della frase e impostazioni PDF personalizzate.
keywords:
- GroupDocs.Redaction Java
- text redaction Java
- rasterized PDF conversion
title: Come censurare il testo con GroupDocs.Redaction Java
type: docs
url: /it/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# Come redigere il testo con GroupDocs.Redaction Java

Nel mondo odierno guidato dai dati, **come redigere il testo** in un documento in modo sicuro ed efficiente è una preoccupazione principale per sviluppatori e responsabili della conformità. Che tu debba nascondere identificatori personali, dettagli riservati dei clienti o codici di progetto interni, GroupDocs.Redaction for Java ti offre un modo affidabile per individuare frasi esatte e sostituirle con sovrapposizioni sicure. Questo tutorial mostra anche **come salvare come PDF rasterizzato**, trasformando ogni pagina in un PDF basato su immagine che soddisfa gli standard di archiviazione.

## Risposte rapide
- **Qual è la classe principale per la redazione?** `Redactor`  
- **Posso sostituire una frase con una sovrapposizione colorata?** Sì, usando `ExactPhraseRedaction` e `ReplacementOptions`.  
- **Come genero un PDF rasterizzato?** Abilita la rasterizzazione tramite `SaveOptions.getRasterization().setEnabled(true)`.  
- **Quale livello di conformità PDF è usato nell'esempio?** `PdfComplianceLevel.PdfA1a`.  
- **È necessaria una licenza per l'uso in produzione?** È richiesta una licenza valida di GroupDocs.Redaction per le distribuzioni in produzione.

## Cos'è “come redigere il testo” in Java?
La redazione è il processo di rimozione permanente o oscuramento di contenuti sensibili da un file. Con GroupDocs.Redaction, è possibile cercare programmaticamente una frase esatta — come un nome o un ID — e sostituirla con una sovrapposizione rossa, una casella nera o qualsiasi elemento visivo personalizzato, garantendo che i dati originali non possano essere recuperati.

## Perché usare GroupDocs.Redaction per Java?
- **Corrispondenza di frase esatta** elimina i falsi positivi.  
- **Rasterizzazione integrata** ti consente di creare PDF/A‑compatibili, PDF solo immagine per l'archiviazione a lungo termine.  
- **Supporto multi‑formato** funziona con DOCX, PDF, PPTX e altri, così puoi applicare lo stesso codice a diversi tipi di documento.  
- **API orientata alle prestazioni** ti permette di elaborare in batch grandi insiemi di documenti mantenendo basso l'uso della memoria.

## Prerequisiti
Prima di iniziare, assicurati di avere quanto segue:

- **GroupDocs.Redaction for Java** (v24.9 o più recente).  
- **Java Development Kit (JDK) 8+**.  
- Un IDE come IntelliJ IDEA, Eclipse o NetBeans.  
- Maven per la gestione delle dipendenze.  

### Librerie e dipendenze richieste
- **GroupDocs.Redaction for Java** – aggiungi il repository e la dipendenza al tuo `pom.xml` (vedi il blocco di codice sotto).  
- **Opzionale**: qualsiasi libreria di logging aggiuntiva che preferisci.

### Prerequisiti di conoscenza
- Sintassi Java di base e I/O di file.  
- Familiarità con la struttura del `pom.xml` di Maven.  

## Configurazione di GroupDocs.Redaction per Java
### Configurazione Maven
Aggiungi il repository e la dipendenza al tuo `pom.xml` file:

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
In alternativa, puoi scaricare l'ultima versione direttamente da [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisizione della licenza
- **Prova gratuita** – esplora l'API senza una chiave di licenza.  
- **Licenza temporanea** – utilizza per una valutazione estesa.  
- **Licenza completa** – richiesta per gli ambienti di produzione.

### Inizializzazione e configurazione di base
Di seguito il codice minimo per creare un'istanza `Redactor` che punta a un file DOCX di esempio:

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## Come redigere il testo – Esempio di frase esatta
### Passo 1: Importa le classi necessarie
Questi import ti danno accesso al motore di redazione e alle opzioni di sostituzione:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

### Passo 2: Crea e applica la redazione
Il frammento seguente cerca la frase **“John Doe”** e la sostituisce con una sovrapposizione rossa:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

**Perché è importante:** `ReplacementOptions` ti consente di controllare lo stile visivo della redazione, garantendo che il contenuto nascosto non possa essere recuperato tramite copia‑incolla o OCR.

## Come salvare come PDF rasterizzato
### Passo 1: Importa le classi SaveOptions
Queste classi ti permettono di configurare l'output PDF, inclusa la rasterizzazione e i livelli di conformità:

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

### Passo 2: Configura e applica le opzioni di salvataggio
Dopo la redazione, puoi esportare il documento come PDF rasterizzato. L'esempio sotto rasterizza solo la pagina 5 e forza la conformità PDF/A‑1a:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

**Punto chiave:** Rasterizzare un PDF **converte ogni pagina in un'immagine**, rimuovendo i livelli di testo nascosti e rendendo il documento a prova di manomissione — ideale per l'archiviazione legale.

## Applicazioni pratiche
1. **Redazione di dati sensibili** – Nascondi automaticamente gli identificatori personali prima di condividere i contratti.  
2. **Archiviazione dei documenti** – Converti i report finalizzati in PDF/A rasterizzato per la conformità a lungo termine.  
3. **Aggiornamento massivo dei contenuti** – Sostituisci la terminologia obsoleta in centinaia di file con un unico script.

## Considerazioni sulle prestazioni
- **Chiudi il `Redactor`** dopo ogni operazione per rilasciare i handle dei file e la memoria.  
- **Elaborazione batch** – Carica un elenco di file e iterali, riutilizzando una singola istanza di `Redactor` quando possibile.  
- **Monitora le risorse** – Usa strumenti di profiling Java per osservare l'uso della CPU e dell'heap durante redazioni su larga scala.

## Domande frequenti

**D: Come installo GroupDocs.Redaction in un progetto Maven?**  
R: Aggiungi il repository GroupDocs e la dipendenza `groupdocs-redaction` al tuo `pom.xml` come mostrato nella sezione Configurazione Maven.

**D: Posso redigere il testo da file PDF usando questa libreria?**  
R: Sì, GroupDocs.Redaction supporta PDF, DOCX, PPTX e molti altri formati.

**D: Cosa succede se la frase esatta non viene trovata?**  
R: Il `RedactorChangeLog` restituirà uno stato `Failed`. Verifica l'ortografia e la sensibilità al maiuscolo/minuscolo della frase.

**D: Come posso gestire documenti molto grandi in modo efficiente?**  
R: Elaborali in intervalli di pagine più piccoli, abilita la rasterizzazione solo dove necessario e chiudi sempre il `Redactor` per liberare le risorse.

**D: È possibile salvare PDF rasterizzati con intervalli di pagine specifici?**  
R: Assolutamente. Usa `options.getRasterization().setPageIndex()` e `setPageCount()` per puntare alle pagine esatte che desideri rasterizzare.

## Conclusione
Ora hai una guida completa, end‑to‑end, su **come redigere il testo** con GroupDocs.Redaction Java e **salvare come PDF rasterizzato**. Seguendo questi passaggi, puoi proteggere le informazioni sensibili, soddisfare i requisiti di conformità e mantenere alte prestazioni nei carichi di lavoro di produzione.

**Passaggi successivi**  
- Approfondisci l'API esplorando la [documentazione ufficiale](https://docs.groupdocs.com/redaction/java/).  
- Sperimenta altri tipi di redazione (ad es., `RegexRedaction`, `ImageRedaction`).  
- Unisciti alla community sul [Forum di supporto GroupDocs](https://forum.groupdocs.com/c/redaction/33) per consigli e best practice.

---

**Ultimo aggiornamento:** 2026-02-26  
**Testato con:** GroupDocs.Redaction Java 24.9  
**Autore:** GroupDocs