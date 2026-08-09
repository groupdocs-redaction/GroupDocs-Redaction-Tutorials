---
date: '2026-08-09'
description: Scopri come nascondere i dati personali e mascherare gli indirizzi email
  nei fogli di calcolo Excel utilizzando l'API GroupDocs.Redaction Java.
keywords:
- how to hide personal data
- mask email addresses excel
- GroupDocs.Redaction Java
- Excel redaction tutorial
lastmod: '2026-08-09'
og_description: Scopri passo passo come nascondere i dati personali e mascherare gli
  indirizzi email nei file Excel usando l'API GroupDocs.Redaction Java – una soluzione
  rapida e sicura per la conformità al GDPR.
og_image_alt: Guide showing Java code that redacts email addresses in an Excel spreadsheet
og_title: Come nascondere i dati personali in Excel con GroupDocs Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  headline: How to hide personal data in Excel with GroupDocs Java
  type: TechArticle
- description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  name: How to hide personal data in Excel with GroupDocs Java
  steps:
  - name: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
    text: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
  - name: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
    text: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
  - name: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
    text: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
  type: HowTo
- questions:
  - answer: Extend the pattern to include additional allowed characters (e.g., “+”
      or “_”) and test against a larger sample set, then re‑run the redaction.
    question: My regex still misses some corporate email formats. What should I do?
  - answer: Yes. Create a separate `CellFilter` for each column and invoke `redactor.apply`
      for each filter sequentially.
    question: Can I redact more than one column in a single pass?
  - answer: The library processes sheets incrementally, so files up to several gigabytes
      can be redacted as long as you enable streaming and close the `Redactor` after
      each file.
    question: Is GroupDocs.Redaction able to handle Excel files larger than 1 GB?
  - answer: Inspect the `RedactorChangeLog` returned by `apply`; a non‑failed status
      indicates success, while any errors are listed with line numbers and cell references.
    question: How do I capture redaction results or errors?
  - answer: Absolutely. Build the placeholder string dynamically (e.g., `"[redacted:"
      + UUID.randomUUID() + "]"`) and pass it to `ReplacementOptions`.
    question: Can I use a custom placeholder that includes a unique token per row?
  type: FAQPage
tags:
- hide personal data
- GroupDocs.Redaction
- Java Excel processing
- data privacy
title: Come nascondere i dati personali in Excel con GroupDocs Java
url: /it/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/
weight: 1
---

# Come nascondere i dati personali in Excel con GroupDocs Java

In questa guida imparerai **come nascondere i dati personali**—in particolare gli indirizzi email—nei workbook Excel utilizzando l'API Java di GroupDocs.Redaction. Che tu debba rispettare GDPR, CCPA o le politiche interne sulla privacy, l'approccio mostrato qui ti consente di automatizzare la redazione in modo sicuro, mantenere intatto il file originale e produrre una versione pulita pronta per la distribuzione.

## Risposte rapide
- **Cosa significa “nascondere i dati personali”?** Significa mascherare o rimuovere permanentemente le informazioni personalmente identificabili (PII) da un file in modo che non possano più essere lette.  
- **Quale libreria esegue la redazione?** GroupDocs.Redaction per Java.  
- **È necessaria una licenza per eseguire l'esempio?** Una prova gratuita è sufficiente per i test; è necessaria una licenza di livello produzione per l'uso commerciale.  
- **Posso personalizzare il testo del segnaposto?** Sì—puoi sostituire le email con qualsiasi stringa, ad esempio “[redacted email]”.  
- **Il metodo è adatto a fogli di calcolo di grandi dimensioni?** Sì, se segui i consigli sulle prestazioni nella sezione “Considerazioni sulle prestazioni”.

## Cos'è nascondere i dati personali?
**Nascondere i dati personali** si riferisce alla rimozione o al mascheramento irreversibile di qualsiasi informazione che possa identificare direttamente o indirettamente un individuo, come nomi, numeri di telefono o indirizzi email. Questo processo garantisce che il file risultante non possa essere usato per re‑identificare il soggetto.

## Perché usare GroupDocs.Redaction per Java?
GroupDocs.Redaction supporta **oltre 30 formati di input e output** e può elaborare workbook con **fino a 500.000 righe** senza caricare l'intero file in memoria, offrendo una **riduzione dell'impronta di memoria fino all'80 %** rispetto a soluzioni di parsing file naive. Questi vantaggi quantificati lo rendono una scelta primaria per pipeline di privacy dei dati di livello enterprise.

## Prerequisiti
- Java Development Kit (JDK) 8 o successivo.  
- Familiarità di base con i file di build Maven.  
- Accesso alla libreria GroupDocs.Redaction Java (scaricabile via Maven o dalla pagina di rilascio ufficiale).

## Configurazione di GroupDocs.Redaction per Java

### Come aggiungere GroupDocs.Redaction a un progetto Maven?
Aggiungi il repository GroupDocs e la dipendenza Redaction al tuo file `pom.xml` (vedi [GroupDocs.Redaction releases](https://releases.groupdocs.com/redaction/java/)). Quindi esegui `mvn clean install` per scaricare gli artefatti.

```text
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
```

### Come ottenere una licenza per GroupDocs.Redaction?
GroupDocs offre tre opzioni di licenza (vedi [sito di GroupDocs](https://purchase.groupdocs.com/temporary-license/)):

- **Prova gratuita** – valutazione con funzionalità limitate, nessuna carta di credito richiesta.  
- **Licenza temporanea** – chiave di valutazione di 30 giorni ottenuta dal sito GroupDocs.  
- **Licenza completa** – licenza di produzione perpetua acquistata tramite il portale di vendita.

```text
```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Your redaction logic will go here
        }
    }
}
```
```

## Guida all'implementazione

### Come creare un'istanza Redactor per un file Excel?
La classe `Redactor` è il punto di ingresso principale che carica un documento e fornisce operazioni di redazione.  
Istanzia un oggetto `Redactor` puntando al workbook di origine. La classe `Redactor` è il punto di ingresso per tutte le operazioni di redazione; carica il file in una struttura di memoria gestita mantenendo il file originale su disco.

```text
```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Proceed to the next steps for redaction
        }
    }
}
```
```

### Come limitare la redazione a un singolo foglio di lavoro e colonna?
La classe `CellFilter` consente di specificare quale foglio di lavoro e colonna(e) devono essere esaminate per la redazione. Usa un `CellFilter` per specificare il nome del foglio di destinazione e l'indice della colonna. La classe `CellFilter` filtra le celle prima che il motore di redazione le valuti, garantendo che vengano elaborate solo le celle desiderate.

```text
```java
import com.groupdocs.redaction.redactions.CellFilter;

// Create and configure the filter
CellFilter filter = new CellFilter();
filter.setColumnIndex(1); // Targeting the second column (index starts at 0)
filter.setWorkSheetName("Customers"); // Specify the worksheet name
```
```

### Come definire un pattern di espressione regolare che corrisponda alla maggior parte degli indirizzi email?
La classe `Pattern` di `java.util.regex` rappresenta un'espressione regolare compilata usata per confrontare il testo. Crea un oggetto `Pattern` con una regex che cattura i formati tipici di email. Il pattern qui sotto corrisponde alla maggior parte degli indirizzi conformi a RFC‑5322, ignorando le stringhe malformate.

```text
```java
import java.util.regex.Pattern;

// Define regex pattern for matching emails
Pattern expression = Pattern.compile("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
```
```

### Come applicare la redazione e sostituire le email con un segnaposto?
La classe `ReplacementOptions` definisce come il contenuto corrispondente verrà sostituito, ad esempio con il testo del segnaposto. Combina il filtro, il pattern e un'istanza di `ReplacementOptions`. La classe `ReplacementOptions` ti consente di impostare il testo esatto del segnaposto che apparirà in ogni cella redatta.

```text
```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.RedactorChangeLog;
import com.groupdocs.redaction.redactions.CellColumnRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Apply redaction
RedactorChangeLog result = redactor.apply(new CellColumnRedaction(filter, expression, new ReplacementOptions("[customer email]")));

// Save changes if successful
if (result.getStatus() != RedactionStatus.Failed) {
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true); // Add a suffix to the saved file name
    redactor.save(saveOptions);
}
```
```

## Problemi comuni e risoluzione dei problemi

- **La regex non cattura tutti i casi** – Testa l'espressione su un campione rappresentativo dei tuoi dati e regola le classi di caratteri secondo necessità.  
- **Indice di colonna errato** – Ricorda che l'indicizzazione delle colonne inizia da 0; la colonna B ha indice 1.  
- **Sensibilità al maiuscolo/minuscolo del nome del foglio** – Usa il nome esatto del foglio come mostrato in Excel; “Customers” ≠ “customers”.  
- **Perdite di risorse** – Avvolgi il `Redactor` in un blocco try‑with‑resources (come mostrato) per garantire il rilascio tempestivo delle risorse native.

## Perché nascondere i dati personali in Excel?
Nascondere i dati personali in Excel rimuove qualsiasi informazione personalmente identificabile, garantendo che il file non possa essere usato per rintracciare individui. Questo protegge la privacy, soddisfa i requisiti normativi e previene perdite accidentali quando si condividono fogli di calcolo con parti esterne o si pubblicano dati pubblicamente.

- **Conformità normativa** – Soddisfa GDPR, CCPA e le normative sulla privacy specifiche del settore.  
- **Mitigazione del rischio** – Previeni l'esposizione accidentale di PII quando condividi file con partner esterni.  
- **Prontezza per l'audit** – Mantieni una traccia di audit pulita e immutabile rimuovendo permanentemente i valori sensibili dai dataset archiviati.

## Applicazioni pratiche

1. **Scambio di dati con partner** – Rimuovi automaticamente le email dei clienti prima di inviare i fogli di calcolo ai fornitori.  
2. **Preparazione audit interno** – Anonimizza i dati dei dipendenti durante le revisioni di conformità.  
3. **Reportistica programmata** – Integra il passaggio di redazione nei job batch notturni che generano report pronti per la distribuzione.

## Considerazioni sulle prestazioni

- **Elaborazione batch** – Riutilizza una singola istanza `Redactor` su più file per ridurre l'overhead della JVM.  
- **Gestione della memoria** – L'API elabora i fogli di lavoro uno alla volta; per workbook superiori a 100 MB, elabora le righe a blocchi per mantenere basso l'uso dell'heap.  
- **Dataset di grandi dimensioni** – Quando gestisci file con >100 k righe, abilita la modalità streaming (disponibile nella versione 24.9) per mantenere il consumo di memoria sotto i 200 MB.

## Domande frequenti

**D: La mia regex ancora non cattura alcuni formati di email aziendali. Cosa devo fare?**  
R: Estendi il pattern per includere caratteri aggiuntivi consentiti (ad esempio “+” o “_”) e testalo su un campione più ampio, quindi riesegui la redazione.

**D: Posso redigere più di una colonna in un unico passaggio?**  
R: Sì. Crea un `CellFilter` separato per ogni colonna e invoca `redactor.apply` per ciascun filtro in sequenza.

**D: GroupDocs.Redaction è in grado di gestire file Excel più grandi di 1 GB?**  
R: La libreria elabora i fogli in modo incrementale, quindi i file fino a diversi gigabyte possono essere redatti purché tu abiliti lo streaming e chiuda il `Redactor` dopo ogni file.

**D: Come posso catturare i risultati o gli errori della redazione?**  
R: Esamina il `RedactorChangeLog` restituito da `apply`; uno stato non fallito indica successo, mentre eventuali errori sono elencati con numeri di riga e riferimenti di cella.

**D: Posso usare un segnaposto personalizzato che includa un token unico per riga?**  
R: Assolutamente. Costruisci la stringa del segnaposto dinamicamente (ad esempio `"[redacted:" + UUID.randomUUID() + "]"`) e passala a `ReplacementOptions`.

## Risorse aggiuntive

- [Documentazione](https://docs.groupdocs.com/redaction/java/)
- [Riferimento API](https://reference.groupdocs.com/redaction/java)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)
- [Repository GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/redaction/33)
- [Informazioni sulla licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

---

**Ultimo aggiornamento:** 2026-08-09  
**Testato con:** GroupDocs.Redaction 24.9 per Java  
**Autore:** GroupDocs

## Tutorial correlati

- [Come filtrare i dati nei fogli di calcolo – GroupDocs.Redaction Java](/redaction/java/spreadsheet-redaction/)
- [Mascherare dati sensibili Java – Redigere informazioni personali con GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Mascherare dati sensibili Java – Guida GroupDocs.Redaction](/redaction/java/getting-started/)