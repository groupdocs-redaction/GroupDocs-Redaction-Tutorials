---
date: '2026-03-22'
description: Scopri come eseguire la redazione dei metadati con GroupDocs in Java,
  rimuovendo in modo sicuro i metadati riservati dei documenti utilizzando GroupDocs.Redaction.
keywords:
- metadata redaction Java
- GroupDocs Redaction tutorial
- secure document metadata
title: Come eseguire la redazione dei metadati con GroupDocs in Java
type: docs
url: /it/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# Come eseguire la redazione dei metadati con GroupDocs in Java

In questa guida completa scoprirai **come utilizzare la redazione dei metadati con GroupDocs** per rimuovere metadati riservati — come i nomi delle aziende — da Word, PDF e altri formati di documento usando GroupDocs.Redaction per Java. Alla fine del tutorial sarai in grado di integrare la redazione dei metadati in qualsiasi flusso di lavoro basato su Java e mantenere al sicuro le informazioni sensibili.

## Risposte rapide
- **Cosa fa MetadataSearchRedaction?** Cerca campi di metadati specifici e ne sostituisce i valori con testo personalizzato.  
- **Quale libreria è necessaria?** GroupDocs.Redaction per Java (v24.9 o successiva).  
- **È necessaria una licenza?** Una prova gratuita è sufficiente per la valutazione; è richiesta una licenza completa per la produzione.  
- **Posso mantenere il formato file originale?** Sì — usa `SaveOptions` per preservare il formato originale.  
- **Questo approccio è thread‑safe?** Ogni istanza di `Redactor` è indipendente, quindi è possibile elaborare documenti in parallelo.

## Che cos’è la redazione dei metadati con GroupDocs?
`MetadataSearchRedaction` è una classe specializzata che consente di mirare a una proprietà di metadati particolare (ad es., *Company*, *Author*) e sostituirne il contenuto con un segnaposto. È ideale quando è necessario anonimizzare dati aziendali prima di condividere i documenti con partner esterni.

## Perché usare la redazione dei metadati con GroupDocs?
- **Precisione** – Redigi solo i campi che specifichi, lasciando intatto il resto del documento.  
- **Conformità** – Aiuta a soddisfare GDPR, HIPAA e altre normative sulla privacy rimuovendo identificatori nascosti.  
- **Pronta per l’automazione** – Si integra perfettamente in pipeline di elaborazione batch o micro‑servizi.

## Prerequisiti
- **GroupDocs.Redaction per Java** ≥ 24.9.  
- Java 8 o successiva installata sulla tua macchina.  
- Un IDE come IntelliJ IDEA o Eclipse (opzionale ma consigliato).  
- Familiarità di base con Maven (o capacità di aggiungere manualmente i JAR).  

## Configurazione di GroupDocs.Redaction per Java
Aggiungi il repository e la dipendenza al tuo `pom.xml`. Questo passaggio garantisce a Maven di scaricare automaticamente la libreria.

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

*In alternativa, puoi scaricare il JAR direttamente dalla pagina di rilascio ufficiale:*  
[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)

### Acquisizione della licenza
- **Prova gratuita** – Scarica una licenza di prova per esplorare tutte le funzionalità.  
- **Licenza temporanea** – Da utilizzare per test estesi.  
- **Licenza completa** – Necessaria per le distribuzioni in produzione.

## Inizializzazione di base
Crea un'istanza `Redactor` puntando al documento che desideri elaborare.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Guida all’implementazione

### Passo 1: Importare le classi necessarie
Questi import ti danno accesso al motore di redazione, alle opzioni di salvataggio e alle utility dei metadati.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### Passo 2: Inizializzare Redactor
Istanzia il `Redactor` con il percorso del tuo file sorgente.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### Passo 3: Configurare la ricerca e la redazione dei metadati
Crea un `MetadataSearchRedaction` che cerchi la stringa esatta **"Company Ltd."** e la sostituisca con **"--company--"**. La chiamata `setFilter` limita l’operazione al campo di metadati *Company* soltanto.

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### Passo 4: Applicare la redazione
Esegui la redazione sul documento aperto.

```java
redactor.apply(redaction);
```

### Passo 5: Salvare con opzioni personalizzate
Configura `SaveOptions` in modo che il file redatto riceva il suffisso “_Redacted” mantenendo il formato originale.

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### Passo 6: Rilasciare le risorse
Chiudi sempre il `Redactor` per liberare le risorse native ed evitare perdite di memoria.

```java
finally {
    redactor.close();
}
```

## Problemi comuni e soluzioni
- **FileNotFoundException** – Verifica il percorso passato a `Redactor`. Usa percorsi assoluti o `Paths.get(...)` per maggiore affidabilità.  
- **Nessuna modifica osservata** – Controlla che il campo di metadati mirato contenga effettivamente la stringa di ricerca; i metadati sono sensibili al maiuscolo/minuscolo per impostazione predefinita.  
- **Errori di out‑of‑memory su file di grandi dimensioni** – Elabora i documenti in batch più piccoli e chiama `redactor.close()` subito dopo ogni file.

## Applicazioni pratiche
1. **Documentazione legale** – Rimuovi i nomi delle aziende clienti prima di inviare contratti a terze parti.  
2. **Reporting finanziario** – Anonimizza gli identificatori interni nei file di audit.  
3. **Progetti collaborativi** – Proteggi le informazioni proprietarie quando condividi bozze con fornitori esterni.

## Considerazioni sulle prestazioni
- **Gestione della memoria** – La libreria carica l’intero documento in memoria; chiudere il `Redactor` dopo ogni file è fondamentale.  
- **Elaborazione batch** – Per scenari ad alto volume, itera su una collezione di file e riutilizza una singola istanza di `SaveOptions`.  
- **Rimani aggiornato** – Le nuove versioni introducono ottimizzazioni e correzioni; punta sempre all’ultima versione stabile.

## Conclusione
Ora sai **come utilizzare la redazione dei metadati con GroupDocs** per rimuovere in modo sicuro i metadati aziendali dai documenti usando GroupDocs.Redaction per Java. Integra questi passaggi nei tuoi pipeline di elaborazione documenti per rimanere conforme e proteggere le informazioni sensibili.

**Passi successivi**
- Sperimenta con altri campi di metadati come *Author* o *Creator*.  
- Combina la redazione dei metadati con la redazione di testo o immagini per una soluzione a copertura completa.  

## Sezione FAQ
1. **Che cos’è GroupDocs.Redaction per Java?**  
   - È una libreria potente che consente di redigere testo, metadati e immagini nei documenti tramite applicazioni Java.  
2. **Posso usare GroupDocs.Redaction senza acquistare una licenza?**  
   - Sì, ma con limitazioni. Una prova gratuita o una licenza temporanea consentono l’accesso completo per scopi di test.  
3. **Come garantisco che i formati dei documenti siano preservati durante la redazione?**  
   - Usa `SaveOptions` per specificare le tue esigenze, ad esempio evitando la rasterizzazione in PDF.  
4. **Quali tipi di documenti possono essere redatti con GroupDocs.Redaction?**  
   - Supporta un’ampia gamma, inclusi Word, Excel, PowerPoint, PDF e molti altri.  
5. **Dove posso trovare supporto se incontro problemi?**  
   - Visita il [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) per assistenza.

## Domande frequenti
**D: Il MetadataSearchRedaction funziona con documenti crittografati?**  
R: Sì. Carica il documento con la password appropriata usando il costruttore di `Redactor` che accetta un parametro password.

**D: Posso concatenare più redazioni di metadati in un’unica esecuzione?**  
R: Assolutamente. Crea più oggetti `MetadataSearchRedaction`, imposta filtri diversi e applicali sequenzialmente prima di salvare.

**D: È possibile visualizzare in anteprima le redazioni prima del salvataggio?**  
R: Puoi chiamare `redactor.getRedactions()` per ottenere un elenco delle redazioni in sospeso e ispezionarle programmaticamente.

## Risorse
- **Documentazione**: Esplora guide dettagliate su [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **Riferimento API**: Consulta il riferimento completo dell’API su [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download della libreria**: Accedi all’ultima versione su [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **Codice sorgente**: Visualizza e contribuisci su [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).  
- **Supporto**: Ottieni aiuto tramite il canale di supporto gratuito su [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33).

---

**Ultimo aggiornamento:** 2026-03-22  
**Testato con:** GroupDocs.Redaction 24.9 per Java  
**Autore:** GroupDocs  

---