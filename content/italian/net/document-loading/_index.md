---
date: 2026-06-11
description: Scopri come caricare un documento, inclusi i flussi e i file protetti
  da password, utilizzando GroupDocs.Redaction per .NET.
keywords:
- how to load document
- redact password protected pdf
- load password protected file
- load document from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to load document, including from streams and password‑protected
    files, using GroupDocs.Redaction for .NET.
  headline: How to Load Document with GroupDocs.Redaction for .NET
  type: TechArticle
- questions:
  - answer: Yes—GroupDocs.Redaction automatically detects the DOCX format when you
      pass the file path or stream, so no extra code is needed.
    question: Can I load DOCX files the same way I load PDFs?
  - answer: Absolutely. Retrieve the blob as a byte array or stream and feed it to
      the `RedactionEngine` constructor.
    question: Does the library support loading files from Azure Blob Storage?
  - answer: The constructor throws a `PasswordIncorrectException`. Catch this exception
      to prompt the user for the correct password.
    question: What happens if I provide the wrong password?
  - answer: Yes—each `RedactionEngine` instance is independent and thread‑safe, allowing
      parallel processing in background services.
    question: Is it possible to load multiple documents simultaneously?
  - answer: The engine implements `IDisposable`. Call `Dispose()` or wrap it in a
      `using` block to release file handles promptly.
    question: Do I need to dispose of the RedactionEngine manually?
  type: FAQPage
title: Come caricare un documento con GroupDocs.Redaction per .NET
type: docs
url: /it/net/document-loading/
weight: 2
---

# Come caricare un documento con GroupDocs.Redaction per .NET

In questa guida scoprirai **come caricare documenti** in GroupDocs.Redaction per .NET da diverse fonti: disco locale, stream di memoria e persino file protetti da password. Che tu stia creando un servizio di redazione, una pipeline di conformità automatizzata o una semplice utility desktop, padroneggiare queste tecniche di caricamento ti consente di preparare qualsiasi documento per una redazione sicura in modo rapido e affidabile.

## Risposte rapide
- **Qual è il primo passo?** Installa il pacchetto NuGet GroupDocs.Redaction e aggiungi lo spazio dei nomi `using GroupDocs.Redaction;`.
- **Posso caricare un PDF da uno stream?** Sì—passa un `MemoryStream` contenente i byte del PDF al costruttore `RedactionEngine`.
- **Come apro un file protetto da password?** Fornisci la password come secondo argomento quando crei il `RedactionEngine`.
- **Esiste un limite di dimensione del file?** GroupDocs.Redaction elabora file fino a 2 GB senza caricare l'intero file in memoria.
- **Ho bisogno di una licenza per lo sviluppo?** Una licenza temporanea funziona per i test; è necessaria una licenza completa per le distribuzioni in produzione.

## Come caricare un documento?
`RedactionEngine` è la classe principale che carica e prepara i documenti per la redazione. Carica un documento creando un'istanza di `RedactionEngine` con il percorso del file (o lo stream) e, se necessario, la password. Questa chiamata a riga singola legge il file, ne valida il formato e costruisce il modello interno del documento pronto per la redazione. Ad esempio, caricare un PDF dal disco è semplice come `new RedactionEngine("sample.pdf")`. Quando è richiesta una password, usa `new RedactionEngine("secret.pdf", "MyPassword")`. Il caricamento da uno stream segue lo stesso schema con un argomento `MemoryStream`.

## Cos'è GroupDocs.Redaction?
GroupDocs.Redaction è una libreria .NET che consente agli sviluppatori di individuare e rimuovere in modo permanente contenuti sensibili da PDF, DOCX, PPTX e oltre 30 altri formati di file. Offre redazione pixel‑perfect, supporto OCR e elaborazione batch, rendendola ideale per applicazioni orientate alla conformità che richiedono una protezione dei dati affidabile e sicura su molti tipi di documento.

## Perché usare GroupDocs.Redaction per il caricamento dei documenti?
GroupDocs.Redaction fornisce un motore di streaming ad alte prestazioni e a basso consumo di memoria che può gestire file di grandi dimensioni fino a 2 GB, supportando anche documenti protetti da password senza configurazioni aggiuntive. Questa combinazione di velocità, flessibilità e sicurezza lo rende la scelta preferita per gli sviluppatori che devono caricare documenti rapidamente e in modo sicuro prima di applicare le regole di redazione.

- **Ampio supporto di formati:** Gestisce **30+** tipi di documento, inclusi PDF, Word, Excel, PowerPoint e file immagine.  
- **Streaming ad alte prestazioni:** Elabora file fino a **2 GB** usando un motore di streaming a basso consumo di memoria, eliminando la necessità di caricare l'intero file.  
- **Gestione delle password:** Apre senza problemi **PDF e file Office protetti da password** con un unico overload del metodo, riducendo la complessità del codice.  
- **API thread‑safe:** Consente il caricamento concorrente di più documenti in servizi multithread senza condizioni di gara.

## Prerequisiti
- .NET 6.0 o versioni successive (la libreria supporta anche .NET Core 3.1 e .NET Framework 4.6.1+).  
- Una licenza valida di GroupDocs.Redaction (licenza temporanea per i test).  
- Accesso ai file di documento che intendi redigere (percorso locale, array di byte o stream).

## Caricamento di documenti da diverse fonti

### Caricamento dal disco locale
Fornisci il percorso assoluto o relativo al file quando costruisci l'engine. La libreria rileva automaticamente il formato e lo prepara per la redazione.

### Caricamento da uno stream di memoria
Leggi il file in un `byte[]`, avvolgilo in un `MemoryStream` e passa lo stream al costruttore. Questo approccio è perfetto per le API web che ricevono file come upload.

### Caricamento di file protetti da password
Quando un documento è crittografato, fornisci la password come secondo argomento. L'engine decritta il file al volo e rende il contenuto disponibile per la redazione senza passaggi aggiuntivi.

## Problemi comuni e soluzioni
- **Errore: “File format not supported.”**  
  Verifica che l'estensione del file corrisponda a un formato supportato e che il file non sia corrotto. GroupDocs.Redaction supporta oltre 30 formati; consulta il riferimento API per l'elenco completo.

- **Eccezione relativa alla password.**  
  Assicurati che la stringa della password sia corretta e che il file richieda effettivamente una password. Passare una stringa vuota a un file protetto genererà un errore di autenticazione.

- **Out‑of‑memory per file molto grandi.**  
  Usa l'overload di streaming (`RedactionEngine(Stream)`) invece di caricare il file tramite percorso. Questo mantiene basso l'uso della memoria anche per PDF di centinaia di pagine.

## Domande frequenti
**Q: Posso caricare file DOCX nello stesso modo in cui carico PDF?**  
A: Sì—GroupDocs.Redaction rileva automaticamente il formato DOCX quando passi il percorso del file o lo stream, quindi non è necessario alcun codice aggiuntivo.

**Q: La libreria supporta il caricamento di file da Azure Blob Storage?**  
A: Assolutamente. Recupera il blob come array di byte o stream e passalo al costruttore `RedactionEngine`.

**Q: Cosa succede se fornisco la password errata?**  
A: Il costruttore lancia una `PasswordIncorrectException`. Cattura questa eccezione per chiedere all'utente la password corretta.

**Q: È possibile caricare più documenti simultaneamente?**  
A: Sì—ogni istanza di `RedactionEngine` è indipendente e thread‑safe, consentendo l'elaborazione parallela nei servizi in background.

**Q: Devo liberare manualmente il RedactionEngine?**  
A: Il motore implementa `IDisposable`. Chiama `Dispose()` o avvolgilo in un blocco `using` per rilasciare rapidamente le handle dei file.

## Risorse aggiuntive
- [Come caricare e redigere documenti usando GroupDocs.Redaction .NET: Guida completa](./groupdocs-redaction-net-load-redact-documents/)
- [Come redigere in modo sicuro documenti protetti da password usando GroupDocs.Redaction in .NET](./secure-redact-password-protected-documents-groupdocs-redaction-net/)
- [Documentazione di GroupDocs.Redaction per .NET](https://docs.groupdocs.com/redaction/net/)
- [Riferimento API di GroupDocs.Redaction per .NET](https://reference.groupdocs.com/redaction/net/)
- [Scarica GroupDocs.Redaction per .NET](https://releases.groupdocs.com/redaction/net/)
- [Forum di GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Supporto gratuito](https://forum.groupdocs.com/)
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)

---

**Ultimo aggiornamento:** 2026-06-11  
**Testato con:** GroupDocs.Redaction 5.5 per .NET  
**Autore:** GroupDocs

## Tutorial correlati
- [Come caricare e redigere documenti usando GroupDocs.Redaction .NET: Guida completa](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Redigere e salvare documenti con GroupDocs.Redaction per .NET: Guida completa](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)