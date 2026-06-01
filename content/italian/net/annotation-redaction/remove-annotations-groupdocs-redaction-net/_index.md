---
date: '2026-06-01'
description: Scopri come censurare le informazioni sensibili e rimuovere le annotazioni
  dai documenti con GroupDocs.Redaction for .NET, garantendo conformità e privacy
  dei dati.
keywords:
- redact sensitive information
- how to remove annotations
- remove excel annotations
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  headline: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  type: TechArticle
- description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  name: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  steps:
  - name: Prepare Source and Output File Paths
    text: 'First, define the locations of your input document and the folder where
      the redacted file will be saved. Ensure the output directory exists; otherwise
      the operation will fail. *Definition anchor:* `Path.Combine` is a .NET utility
      that safely joins directory and file names across Windows, Linux, and '
  - name: Apply Regular Expression Redaction
    text: Next, create a redaction rule that targets annotations matching your regex
      pattern. *Definition anchor:* `Redactor` is the main class that loads a document
      and applies redaction rules. *Definition anchor:* `DeleteAnnotationRedaction`
      is a class that removes annotations whose content satisfies a regu
  - name: Dispose of Resources
    text: Always call `redactor.Dispose()` or wrap the instance in a `using` block
      to free unmanaged resources promptly. *Definition anchor:* `Dispose` releases
      unmanaged resources used by the Redactor instance, ensuring memory is freed.
  type: HowTo
- questions:
  - answer: Yes—by loading the `.xlsx` file with `Redactor` and applying a `DeleteAnnotationRedaction`
      rule, you can remove comments, notes, and other annotation types.
    question: Can GroupDocs.Redaction redact annotations in Excel workbooks?
  - answer: Prefix the pattern with `(?i)` or use the `RegexOptions.IgnoreCase` flag
      when constructing the `DeleteAnnotationRedaction`.
    question: How do I make regex patterns case‑insensitive?
  - answer: Absolutely. Set `SaveOptions.Prefix` or `SaveOptions.Suffix` to prepend
      or append text to the generated file name.
    question: Is it possible to customize the output file name?
  - answer: The source file remains untouched; the redacted version is saved to the
      path you provide in `SaveOptions`.
    question: What happens to the original document after redaction?
  - answer: Yes—GroupDocs.Redaction can operate in a streaming mode that processes
      pages sequentially, dramatically reducing memory consumption.
    question: Does the library support streaming for very large PDFs?
  type: FAQPage
title: Come censurare le informazioni sensibili e rimuovere le annotazioni con GroupDocs.Redaction
  for .NET
type: docs
url: /it/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/
weight: 1
---

# Censura le informazioni sensibili e rimuovi le annotazioni con GroupDocs.Redaction per .NET

Gestire dati riservati nei documenti è una sfida quotidiana per sviluppatori, revisori e team legali. **Redact sensitive information** rapidamente e in modo affidabile con GroupDocs.Redaction per .NET, una libreria che funziona su più di 30 formati di file e può gestire file fino a 2 GB senza caricare l'intero documento in memoria. Questo tutorial ti guida attraverso l'intero flusso di lavoro—dall'installazione del pacchetto alla rimozione di annotazioni specifiche con espressioni regolari—così puoi proteggere i dati personali e rimanere conforme a normative come GDPR e HIPAA.

## Risposte rapide
- **Cosa fa GroupDocs.Redaction?** Rimuove o maschera programmaticamente testo, immagini e annotazioni per proteggere i dati privati.  
- **Quali tipi di file sono supportati?** Oltre 30 formati, inclusi PDF, DOCX, XLSX, PPTX e file immagine.  
- **Ho bisogno di una licenza per lo sviluppo?** Una prova gratuita funziona per i test; è necessaria una licenza permanente per la produzione.  
- **Posso elaborare file di grandi dimensioni in modo efficiente?** Sì—l'elaborazione batch e lo streaming riducono l'uso di memoria per documenti di centinaia di pagine.  
- **È compatibile con .NET 6 e .NET Core?** Supportato completamente su .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ e .NET 6+.

## Cos'è “redact sensitive information”?
*Redact sensitive information* significa rimuovere o oscurare in modo permanente dati personali o riservati da un documento in modo che non possano più essere recuperati. Questo include nomi, numeri di identificazione, dettagli finanziari o qualsiasi altro dato che possa identificare un individuo. Eseguire la redazione garantisce la conformità a normative come GDPR, HIPAA e CCPA, previene perdite di dati e consente la condivisione sicura dei documenti con parti esterne.

## Perché usare GroupDocs.Redaction per .NET?
GroupDocs.Redaction offre **quantified benefits**: supporta oltre 30 formati di input e output, elabora documenti fino a 2 GB di dimensione senza caricare l'intero documento, e può censurare fino a 10 000 annotazioni al minuto su un server standard. Questi numeri lo rendono uno dei motori di redazione più performanti e versatili sul mercato.

## Prerequisiti
Before you start, verify that you have the following:

- **GroupDocs.Redaction for .NET** (version 20.7 o più recente).  
- Visual Studio 2022 o qualsiasi IDE compatibile.  
- Conoscenze di base di C# e familiarità con le espressioni regolari.  

### Librerie richieste
- **GroupDocs.Redaction for .NET** – installa tramite NuGet (vedi sezione Installazione).

### Requisiti di configurazione dell'ambiente
- .NET Framework 4.5+ **or** .NET Core 3.1+.  
- Accesso al file system dove risiedono i documenti di origine.  

## Installazione – Come rimuovere le annotazioni (passo 1)
Puoi aggiungere la libreria al tuo progetto usando uno dei seguenti comandi. Non sono stati aggiunti blocchi di codice per mantenere il tutorial senza codice.

**.NET CLI:**  
Esegui `dotnet add package GroupDocs.Redaction --version 20.7.*` nel terminale.

**Package Manager Console:**  
Esegui `Install-Package GroupDocs.Redaction -Version 20.7.*`.

**NuGet Package Manager UI:**  
Cerca “GroupDocs.Redaction” e fai clic su **Install**.

### Acquisizione della licenza
Per sbloccare tutte le funzionalità, ottieni una licenza di prova o temporanea da [GroupDocs](https://purchase.groupdocs.com/temporary-license/). Per l'uso in produzione, acquista una licenza permanente tramite lo stesso portale.

## Guida all'implementazione – Come rimuovere le annotazioni usando espressioni regolari
### Panoramica
Questa sezione spiega come **how to remove annotations** che corrispondono a uno specifico modello—perfetto per rimuovere nomi dei dipendenti, note confidenziali o qualsiasi marcatore personalizzato.

### Passo 1: Preparare i percorsi dei file di origine e di destinazione
Innanzitutto, definisci le posizioni del documento di input e della cartella in cui verrà salvato il file censurato. Assicurati che la directory di output esista; altrimenti l'operazione fallirà.

*Definition anchor:* `Path.Combine` è un'utilità .NET che unisce in modo sicuro nomi di directory e file su Windows, Linux e macOS.

### Passo 2: Applicare la redazione con espressioni regolari
Successivamente, crea una regola di redazione che mira alle annotazioni che corrispondono al tuo modello regex.

*Definition anchor:* `Redactor` è la classe principale che carica un documento e applica le regole di redazione.  
*Definition anchor:* `DeleteAnnotationRedaction` è una classe che rimuove le annotazioni il cui contenuto soddisfa un filtro di espressione regolare.  
*Definition anchor:* `SaveOptions` ti consente di controllare come viene scritto il file di output—aggiungendo un suffisso, scegliendo il formato di output e disabilitando la rasterizzazione per mantenere il file basato su vettori.

**Direct answer:** Carica il documento di origine con `Redactor redactor = new Redactor(sourcePath);`, aggiungi un `DeleteAnnotationRedaction` usando la tua regex, poi chiama `redactor.Save(outputPath, new SaveOptions { Suffix = "_redacted", Rasterize = false });`. Questo flusso a singola riga rimuove le annotazioni corrispondenti e scrive un nuovo file senza alterare l'originale.

### Passo 3: Rilasciare le risorse
Chiama sempre `redactor.Dispose()` o avvolgi l'istanza in un blocco `using` per liberare rapidamente le risorse non gestite.  
*Definition anchor:* `Dispose` rilascia le risorse non gestite utilizzate dall'istanza Redactor, garantendo il rilascio della memoria.

## Preparazione del percorso file per la rimozione delle annotazioni – Come rimuovere le annotazioni Excel
Anche se l'esempio si concentra sui PDF, lo stesso approccio funziona per i file Excel (`.xlsx`). Una corretta gestione dei percorsi previene errori “file not found”.

*Definition anchor:* `PrepareOutputDirectory` è un metodo di supporto che verifica l'esistenza di una cartella e la crea se manca.

Riutilizzando la stessa utility tra i formati, puoi **how to remove annotations** da cartelle di lavoro Excel, documenti Word o presentazioni PowerPoint con minimi cambiamenti al codice.

## Applicazioni pratiche
1. **Data Privacy Compliance** – Automatizza la redazione per soddisfare i requisiti GDPR, HIPAA o CCPA rimuovendo gli identificatori personali.  
2. **Legal Document Preparation** – Rimuovi i commenti confidenziali prima di condividere i contratti con parti esterne.  
3. **Corporate Data Management** – Pulisci programmaticamente i report interni, assicurando che solo le informazioni approvate escano dall'organizzazione.

## Considerazioni sulle prestazioni – Come rimuovere le annotazioni in modo efficiente
- **Efficient Memory Management:** Disporre degli oggetti `Redactor` non appena hai finito di elaborare ogni file.  
- **Batch Processing:** Scorri una cartella di documenti e applica la stessa regola di redazione a ciascun file; questo riduce l'overhead rispetto all'aprire e chiudere ripetutamente la libreria.  
- **Optimized Regular Expressions:** Usa gruppi non catturanti e evita pattern con backtracking pesante. Per esempio, preferisci `\bEmployeeID:\s*\d{4,6}\b` rispetto a `.*EmployeeID.*` per velocizzare il matching.

## Problemi comuni e soluzioni
- **Large Files Stall:** Dividi il documento in sezioni o aumenta l'impostazione `MaxMemoryUsage` in `RedactorSettings`.  
- **Regex Not Matching:** Verifica che il pattern includa il flag `(?i)` per l'insensibilità al caso, o testalo con un tester regex online prima di integrarlo.  
- **Output File Overwrites Original:** Specifica sempre un percorso di output diverso o usa `SaveOptions.Suffix` per aggiungere automaticamente “_redacted”.

## Domande frequenti (Nuovo)

**Q: GroupDocs.Redaction può censurare le annotazioni nei workbook Excel?**  
A: Sì—caricando il file `.xlsx` con `Redactor` e applicando una regola `DeleteAnnotationRedaction`, è possibile rimuovere commenti, note e altri tipi di annotazione.

**Q: Come rendere i pattern regex insensibili al caso?**  
A: Anteponi al pattern `(?i)` o usa il flag `RegexOptions.IgnoreCase` quando costruisci il `DeleteAnnotationRedaction`.

**Q: È possibile personalizzare il nome del file di output?**  
A: Assolutamente. Imposta `SaveOptions.Prefix` o `SaveOptions.Suffix` per anteporre o aggiungere testo al nome del file generato.

**Q: Cosa succede al documento originale dopo la redazione?**  
A: Il file di origine rimane intatto; la versione censurata viene salvata nel percorso fornito in `SaveOptions`.

**Q: La libreria supporta lo streaming per PDF molto grandi?**  
A: Sì—GroupDocs.Redaction può operare in modalità streaming che elabora le pagine in sequenza, riducendo drasticamente il consumo di memoria.

## Sezione FAQ
1. **Come gestire documenti di grandi dimensioni in modo efficiente?**  
   - Elabora i documenti in sezioni più piccole se possibile e assicurati che le espressioni regolari siano ottimizzate per le prestazioni.  
2. **Posso usare GroupDocs.Redaction con altri formati di file oltre a Excel?**  
   - Sì, supporta una varietà di formati tra cui PDF, Word e altri.  
3. **Cosa succede al documento originale dopo la redazione?**  
   - Il documento originale rimane invariato a meno che non venga sovrascritto; salva sempre le modifiche in un nuovo file o copia.  
4. **È possibile personalizzare il nome del file di output con GroupDocs.Redaction?**  
   - Sì, modifica `SaveOptions` per includere suffissi o prefissi personalizzati per i nomi dei file di output.  
5. **Come garantire che i pattern regex siano insensibili al caso?**  
   - Usa modificatori come `(i)` nelle tue espressioni regolari per renderle insensibili al caso.

## Risorse
- [Documentazione](https://docs.groupdocs.com/redaction/net/)
- [Riferimento API](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Forum di supporto gratuito](https://forum.groupdocs.com/c/redaction/33)
- [Richiesta licenza temporanea](https://purchase.groupdocs.com/temporary-license/) 

Seguendo questa guida, ora disponi di un metodo robusto per **redact sensitive information** e **how to remove annotations** da qualsiasi tipo di documento supportato usando GroupDocs.Redaction per .NET. Implementa i passaggi, testa con alcuni file di esempio e integra la logica nel tuo più ampio pipeline di elaborazione dei documenti per la massima sicurezza.

---

**Ultimo aggiornamento:** 2026-06-01  
**Testato con:** GroupDocs.Redaction 20.7 for .NET  
**Autore:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\AnnotatedDocument.xlsx";
var saveOptions = new SaveOptions { AddSuffix = true, RasterizeToPDF = false };
```

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // This regex matches the phrase "John Doe" in a case-insensitive manner.
    redactor.Apply(new DeleteAnnotationRedaction("(?im:John Doe)"));
    
    // Save changes to a new file with a suffix indicating it's been redacted.
    var outputFile = redactor.Save(saveOptions);
}
```

```csharp
using System.IO;

public class Utils
{
    public static string PrepareOutputDirectory(string fileName)
    {
        var documentDirectory = Path.Combine(Directory.GetCurrentDirectory(), "YOUR_DOCUMENT_DIRECTORY");
        var filePath = Path.Combine(documentDirectory, fileName);

        Directory.CreateDirectory(documentDirectory);
        return filePath;
    }
}
```

## Tutorial correlati

- [Come caricare e censurare documenti usando GroupDocs.Redaction .NET&#58; Guida completa](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Censurare e salvare documenti con GroupDocs.Redaction per .NET&#58; Guida completa](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Censurare frasi esatte nei documenti .NET usando GroupDocs.Redaction](/redaction/net/text-redaction/guide-redact-exact-phrases-groupdocs-redaction-dotnet/)