---
date: '2026-01-24'
description: Impara a redigere PDF con GroupDocs.Redaction per Java, mirare a specifiche
  aree nell'ultima pagina per garantire privacy e conformità.
keywords:
- Java PDF Redaction
- GroupDocs.Redaction
- PDF Area Redaction
title: 'Come redigere PDF con Java e GroupDocs.Redaction: mirare all''ultima pagina
  e a aree specifiche'
type: docs
url: /it/java/page-redaction/java-pdf-redaction-groupdocs-last-page-focus/
weight: 1
---

# Come redigere PDF con Java e GroupDocs.Redaction: mirare all'ultima pagina e aree specifiche

In questo tutorial scoprirai **come redigere PDF** utilizzando la libreria GroupDocs.Redaction per Java, concentrandoti sull'ultima pagina e su aree rettangolari precise. Che tu stia proteggendo dati riservati in contratti legali o sanificando report prima della distribuzione, i passaggi seguenti ti offrono un percorso chiaro e pratico per ottenere redazioni conformi.

## Risposte rapide
- **Quale libreria viene utilizzata?** GroupDocs.Redaction per Java.  
- **Posso mirare solo all'ultima pagina?** Sì, usando `PageRangeFilter` con `PageSeekOrigin.End`.  
- **Come definisco un'area specifica?** Con `PageAreaFilter` che accetta coordinate e dimensioni.  
- **È necessaria una licenza?** Una licenza di prova o temporanea funziona per i test; è richiesta una licenza completa per la produzione.  
- **Il codice è compatibile con Java 17?** Assolutamente – la libreria supporta le versioni moderne di JDK.

## Cos'è la redazione PDF e perché è importante?

La redazione rimuove o maschera permanentemente contenuti sensibili da un PDF, garantendo che i dati nascosti non possano essere recuperati. A differenza di una semplice sovrapposizione o nascondimento, la redazione modifica la struttura sottostante del documento, rendendola uno strumento critico per la conformità a GDPR, HIPAA e altre normative sulla privacy.

## Prerequisiti

Prima di iniziare, assicurati di avere:

1. **Librerie e dipendenze**  
   - Libreria GroupDocs.Redaction (24.9 o successiva)  
   - Java Development Kit (JDK) installato  
   - Un IDE come IntelliJ IDEA o Eclipse  

2. **Configurazione dell'ambiente**  
   - Maven configurato per la gestione delle dipendenze  

3. **Conoscenze di base**  
   - Familiarità con la sintassi Java e la gestione dei file  

## Configurare GroupDocs.Redaction per Java

Puoi aggiungere la libreria al tuo progetto con Maven o scaricando direttamente il JAR.

### Configurazione Maven
Aggiungi quanto segue al tuo file `pom.xml` per includere GroupDocs.Redaction come dipendenza:

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
In alternativa, scarica l'ultima versione da [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### Passaggi per l'acquisizione della licenza
- **Prova gratuita:** Testa l'API senza chiave di licenza.  
- **Licenza temporanea:** Usa una chiave a tempo limitato per l'accesso completo alle funzionalità durante lo sviluppo.  
- **Acquisto:** Ottieni una licenza permanente per le distribuzioni in produzione.

### Inizializzazione di base
Inizia creando un'istanza `Redactor` che punta al PDF da elaborare:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

## Come redigere PDF – Implementazione della redazione basata su area nell'ultima pagina

Di seguito trovi una guida passo‑passo che mostra esattamente **come redigere PDF** nella pagina finale, limitando l'operazione a un rettangolo definito.

### Funzionalità 1: Redazione di aree specifiche su una pagina PDF

**Panoramica:** Questa funzionalità ti consente di mascherare il testo solo all'interno di una regione scelta dell'ultima pagina, lasciando intatto il resto del documento.

#### Passo 1: Caricare il documento PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### Passo 2: Ottenere informazioni sulle pagine del documento
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### Passo 3: Definire le opzioni di sostituzione per la redazione
```java
ReplacementOptions options = new ReplacementOptions("[secret]");
```

#### Passo 4: Configurare i filtri per specificare quali aree redigere
```java
options.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1),
    new PageAreaFilter(
        new java.awt.Point(0, lastPage.getHeight() / 2),
        new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
    )
});
```

#### Passo 5: Applicare la redazione
```java
RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("bibliography", false, options));
```

#### Passo 6: Verificare se la redazione è avvenuta con successo e salvare le modifiche
```java
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.pdf");
}
```

#### Passo 7: Chiudere il Redactor per rilasciare le risorse
```java
redactor.close();
```

### Funzionalità 2: Filtraggio dell'intervallo di pagine per le redazioni

**Panoramica:** Usa questa funzionalità quando devi limitare la redazione a pagine specifiche, ad esempio l'ultima pagina di un contratto multipagina.

#### Passo 1: Caricare il documento PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### Passo 2: Ottenere informazioni sulle pagine del documento
```java
IDocumentInfo info = redactor.getDocumentInfo();
```

#### Passo 3: Definire un filtro di intervallo di pagine per mirare a pagine specifiche
```java
PageRangeFilter pageRangeFilter = new PageRangeFilter(PageSeekOrigin.End, 0, 1);
```

### Funzionalità 3: Redazione basata su area su pagine PDF

**Panoramica:** Questo approccio ti offre un controllo pixel‑perfect specificando il rettangolo esatto da nascondere.

#### Passo 1: Caricare il documento PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### Passo 2: Ottenere informazioni sulle pagine del documento
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### Passo 3: Definire un filtro di area per specificare quale parte di una pagina redigere
```java
PageAreaFilter areaFilter = new PageAreaFilter(
    new java.awt.Point(0, lastPage.getHeight() / 2),
    new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
);
```

#### Passo 4: Chiudere il Redactor per rilasciare le risorse
```java
redactor.close();
```

## Applicazioni pratiche

- **Sanificazione di documenti legali:** Rimuovi nomi dei clienti o numeri di caso prima di condividere le bozze.  
- **Report finanziari:** Maschera numeri di conto o identificatori personali nelle dichiarazioni trimestrali.  
- **Cartelle cliniche:** Assicura che le PHI siano nascoste quando esporti PDF per la ricerca.  
- **Revisione pre‑rilascio:** Nascondi sezioni ancora in sviluppo consentendo ai revisori di vedere il resto del documento.

## Suggerimenti sulle prestazioni

- **Riutilizzare le istanze Redactor:** Se elabori molti PDF in batch, mantieni vivo un singolo oggetto `Redactor` e resettalo tra i file.  
- **Disporre prontamente:** Chiama sempre `close()` per liberare le risorse native.  
- **Validare su un campione:** Esegui la redazione su un piccolo file di test per confermare la geometria dei filtri prima di scalare.

## Problemi comuni e soluzioni

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| Nessun file di output creato | `result.getStatus()` ha restituito `Failed` | Controlla la console per i dettagli dell'eccezione; assicurati che il testo di sostituzione sia valido e che i filtri siano definiti correttamente. |
| La redazione copre l'intera pagina | Dimensioni errate di `PageAreaFilter` | Verifica i valori di `lastPage.getHeight()` e `lastPage.getWidth()`; regola di conseguenza `Point` e `Dimension`. |
| Errore di licenza | Chiave di licenza mancante o scaduta | Applica una licenza di prova o temporanea prima di passare alla produzione. |

## Domande frequenti

**D: Posso redigere immagini o grafiche, non solo testo?**  
R: Sì. Usa `ExactImageRedaction` o combina filtri di testo e immagine per mascherare elementi visivi.

**D: La redazione sopravvive ai visualizzatori PDF che supportano la modifica?**  
R: Assolutamente. La redazione rimuove permanentemente il contenuto sottostante, quindi non può essere recuperata da alcun editor PDF standard.

**D: Come redigo PDF protetti da password?**  
R: Carica il documento con la password usando il costruttore `Redactor` che accetta un oggetto `LoadOptions` contenente la password.

**D: È possibile concatenare più filtri (ad esempio, intervallo di pagine + area)?**  
R: Sì. Passa un array di oggetti `RedactionFilter` a `options.setFilters()` come mostrato nell'esempio.

**D: Quali versioni di Java sono supportate?**  
R: GroupDocs.Redaction 24.9 supporta Java 8 fino a Java 21, incluse le versioni LTS.

## Conclusione

Ora disponi di una guida completa e pronta per la produzione su **come redigere PDF** con Java usando GroupDocs.Redaction. Sfruttando i filtri di intervallo di pagine e di area, puoi rimuovere chirurgicamente i dati sensibili mantenendo intatta la restante parte del documento. Sperimenta con diversi filtri, integra il flusso di lavoro nei tuoi pipeline documentali esistenti e rimani conforme alle normative sulla privacy dei dati.

---

**Ultimo aggiornamento:** 2026-01-24  
**Testato con:** GroupDocs.Redaction 24.9  
**Autore:** GroupDocs