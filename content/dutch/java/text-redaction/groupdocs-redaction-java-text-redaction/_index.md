---
date: '2026-08-14'
description: Hoe tekst in Java-documenten te redigeren met GroupDocs.Redaction – persoonlijke
  informatie maskeren en gevoelige tekst efficiënt vervangen.
keywords:
- how to redact text
- GroupDocs Redaction Java
- text redaction Java
- mask personal information
lastmod: '2026-08-14'
og_description: Hoe tekst te redigeren met GroupDocs.Redaction voor Java stelt je
  in staat om persoonlijke gegevens permanent te maskeren en gevoelige strings in
  PDF's, DOCX en meer te vervangen, waardoor naleving van GDPR en HIPAA wordt gegarandeerd.
og_image_alt: 'Guide: redact text in Java using GroupDocs.Redaction library'
og_title: Hoe tekst te redigeren met GroupDocs.Redaction voor Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  headline: How to redact text with GroupDocs.Redaction for Java
  type: TechArticle
- description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  name: How to redact text with GroupDocs.Redaction for Java
  steps:
  - name: initialize the redactor
    text: '`Redactor` is the core class that loads a document, applies redaction rules,
      and writes the output.'
  - name: apply exact‑phrase redaction
    text: '`ExactPhraseRedaction` searches for an exact string match, while `ReplacementOptions`
      defines how the matched text should be replaced. - **Parameters:** - `"John
      Doe"` – the exact text to be redacted. - `ReplacementOptions("[personal]")`
      – the string that will replace the original content, effective'
  - name: save the redacted document
    text: '`Redactor.save` writes the modified document to a new file or overwrites
      the original, preserving the original format.'
  - name: clean up resources
    text: Always call `Redactor.close()` to release native resources and avoid memory
      leaks.
  type: HowTo
- questions:
  - answer: Yes, the library supports PDF, DOCX, XLSX, PPTX, and many other formats.
    question: Can I redact text from PDFs using GroupDocs.Redaction?
  - answer: No. Redactions permanently remove the original content, so keep a backup
      of the source file.
    question: Is a redaction reversible?
  - answer: Process them in chunks, use batch mode, and monitor memory usage with
      profiling tools.
    question: How do I handle very large documents efficiently?
  - answer: Besides DOCX and PDF, you can redact TXT, RTF, XLSX, PPTX, and more.
    question: What other text formats are supported?
  - answer: Absolutely. The API can be called from web services, background jobs,
      or CI/CD pipelines.
    question: Can I integrate GroupDocs.Redaction into existing workflows?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- privacy compliance
- redaction API
title: Hoe tekst te redigeren met GroupDocs.Redaction voor Java
type: docs
url: /nl/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# Hoe tekst te redigeren met GroupDocs.Redaction voor Java

In deze tutorial leer je **hoe je tekst kunt redigeren** in op Java gebaseerde documenten met GroupDocs.Redaction. Je ziet hoe je persoonlijke informatie kunt maskeren, gevoelige tekenreeksen kunt vervangen door veilige tijdelijke aanduidingen, en meerdere bestanden batch‑vriendelijk kunt verwerken. Aan het einde heb je een productie‑klare oplossing die privacy beschermt, voldoet aan GDPR/HIPAA‑vereisten, en naadloos integreert in bestaande Java‑applicaties.

## Snelle antwoorden
- **Welke bibliotheek wordt gebruikt?** GroupDocs.Redaction for Java.  
- **Kan ik persoonlijke informatie maskeren?** Ja – gebruik exacte‑zin redactie met vervangingsopties.  
- **Wordt batchverwerking ondersteund?** Absoluut, je kunt door meerdere bestanden lopen met dezelfde Redactor‑instantie.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een commerciële licentie is vereist voor productie.  
- **Welke Java‑versie is vereist?** JDK 8 of hoger.

## Wat is “tekst redigeren”?

Redactie verwijdert of verduistert vertrouwelijke gegevens permanent uit een document. Met GroupDocs.Redaction kun je specifieke tekenreeksen vinden, ze vervangen door veilige tijdelijke aanduidingen, en het gesaniteerde bestand opslaan — allemaal zonder handmatige bewerking.

## Waarom GroupDocs.Redaction voor Java gebruiken?

GroupDocs.Redaction voor Java ondersteunt **meer dan 50 invoer‑ en uitvoerformaten** (inclusief PDF, DOCX, XLSX, PPTX, TXT, RTF) en kan bestanden met honderden pagina's verwerken zonder het volledige document in het geheugen te laden, waardoor hoge‑doorvoersnelheid batch‑bewerkingen op standaard serverhardware mogelijk is.

## Vereisten
- **Java Development Kit (JDK):** Versie 8 of nieuwer.  
- **IDE:** IntelliJ IDEA, Eclipse, of een andere Java‑compatibele editor.  
- **Maven:** Voor afhankelijkheidsbeheer.  
- **Basiskennis van Java:** Vertrouwdheid met klassen, methoden en foutafhandeling.

## GroupDocs.Redaction voor Java instellen
Om te beginnen, voeg je de bibliotheek toe aan je Maven‑project.

### Maven‑configuratie
Voeg de repository en afhankelijkheid toe aan je `pom.xml`‑bestand:

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

### Directe download
Als je dat liever hebt, download je de nieuwste JAR van [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Licentie‑acquisitie
Je kunt beginnen met een **Free Trial**, een **Temporary License** aanvragen voor uitgebreid testen, of een **Commercial License** aanschaffen voor productiegebruik.

## Hoe tekst te redigeren in documenten met GroupDocs.Redaction

De volgende secties leiden je door de exacte stappen die nodig zijn om **persoonlijke informatie te maskeren** en **gevoelige tekst te vervangen**.

### Stap 1: initialiseert de redactor

`Redactor` is de kernklasse die een document laadt, redactie‑regels toepast en de uitvoer schrijft.  

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### Stap 2: exacte‑zin redactie toepassen

`ExactPhraseRedaction` zoekt naar een exacte tekenreeks‑overeenkomst, terwijl `ReplacementOptions` definieert hoe de gevonden tekst moet worden vervangen.  

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **Parameters:**  
  - `"John Doe"` – de exacte tekst die moet worden geredigeerd.  
  - `ReplacementOptions("[personal]")` – de tekenreeks die de oorspronkelijke inhoud zal vervangen, waardoor **persoonlijke informatie wordt gemaskeerd**.

### Stap 3: sla het geredigeerde document op

`Redactor.save` schrijft het aangepaste document naar een nieuw bestand of overschrijft het origineel, waarbij het oorspronkelijke formaat behouden blijft.  

```java
redactor.save();
```

### Stap 4: resources opruimen

Roep altijd `Redactor.close()` aan om native resources vrij te geven en geheugenlekken te voorkomen.  

```java
finally {
    redactor.close();
}
```

## Hoe persoonlijke informatie te maskeren met een aangepaste callback

Een aangepaste callback stelt je in staat te reageren op elk redactie‑event — handig voor logging, voorwaardelijke vervangingen of audit‑trails.

### Maak een callback‑klasse

`IRedactionCallback` definieert methoden die vóór en na elke redactie‑operatie worden aangeroepen.  

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### Gebruik de callback bij het instantieren van Redactor

Geef je callback‑implementatie door via `RedactorSettings` zodat de engine weet deze tijdens de verwerking aan te roepen.  

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## Praktische toepassingen
- **Juridische contracten:** Automatisch klantnamen, BSN’s of vertrouwelijke clausules verbergen voordat concepten worden gedeeld.  
- **Medische dossiers:** **Persoonlijke informatie maskeren** zoals patiënt‑identificatoren bij het exporteren van dossiers naar onderzoekspartners.  
- **Bedrijfscommunicatie:** **Gevoelige tekst vervangen** zoals interne projectcodes vóór externe distributie, om onbedoelde lekken te voorkomen.

## Prestatie‑overwegingen
Bij het verwerken van grote of vele bestanden, houd deze tips in gedachten:

- **Batchverwerking:** Loop door een collectie bestanden om opstart‑overhead te verminderen.  
- **Geheugenbeheer:** Maak de `Redactor` vrij na elk bestand; vermijd het gelijktijdig in het geheugen houden van veel documenten.  
- **Profilering:** Gebruik Java‑profilers (bijv. VisualVM) om knelpunten in I/O of redactie‑logica te vinden.

## Veelgestelde vragen
**Q: Kan ik tekst uit PDF’s redigeren met GroupDocs.Redaction?**  
A: Ja, de bibliotheek ondersteunt PDF, DOCX, XLSX, PPTX en vele andere formaten.

**Q: Is een redactie omkeerbaar?**  
A: Nee. Redacties verwijderen de oorspronkelijke inhoud permanent, dus bewaar een backup van het bronbestand.

**Q: Hoe verwerk ik zeer grote documenten efficiënt?**  
A: Verwerk ze in delen, gebruik batch‑modus, en monitor het geheugenverbruik met profiling‑tools.

**Q: Welke andere tekstformaten worden ondersteund?**  
A: Naast DOCX en PDF kun je TXT, RTF, XLSX, PPTX en meer redigeren.

**Q: Kan ik GroupDocs.Redaction integreren in bestaande workflows?**  
A: Absoluut. De API kan worden aangeroepen vanuit webservices, achtergrondtaken of CI/CD‑pijplijnen.

## Bronnen
- **Documentatie:** [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API‑referentie:** [GroupDocs API Reference for Java](https://reference.groupdocs.com/redaction/java)  
- **Download:** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub‑repository:** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Gratis ondersteuningsforum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **Aanvraag tijdelijke licentie:** [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Laatst bijgewerkt:** 2026-08-14  
**Getest met:** GroupDocs.Redaction 24.9 for Java  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Gevoelige gegevens maskeren Java – GroupDocs.Redaction gids](/redaction/java/getting-started/)
- [Gevoelige gegevens maskeren Java – Persoonlijke info redigeren met GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Bewerk wachtwoord‑beveiligde documenten Java - Documenten redigeren met GroupDocs.Redaction](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)