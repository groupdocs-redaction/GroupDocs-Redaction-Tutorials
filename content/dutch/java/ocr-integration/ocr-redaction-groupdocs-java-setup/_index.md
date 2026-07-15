---
date: '2026-06-26'
description: Leer hoe u tekst uit een gescande PDF kunt extraheren en gevoelige gegevens
  kunt maskeren met GroupDocs OCR Redaction en Azure OCR. Redact social security number
  en vervang confidential info PDF efficiënt.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Tekst uit gescande PDF extraheren – Gegevens maskeren met GroupDocs OCR
type: docs
url: /nl/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Tekst extraheren uit gescande PDF – Gegevens maskeren met GroupDocs OCR

In de hedendaagse data‑gedreven wereld is **tekst extraheren uit gescande PDF**‑bestanden en het maskeren van vertrouwelijke informatie een niet‑onderhandelbare compliance‑stap. Deze tutorial leidt je door het gebruik van GroupDocs Redaction samen met Microsoft Azure OCR om betrouwbaar verborgen tekst op gescande pagina's te herkennen en te vervangen door een veilig plaatshouder zoals **`[REDACTED]`**. Je zult zien waarom deze combinatie snel, nauwkeurig en klaar voor productie‑klare workloads is.

## Snelle antwoorden
- **Wat betekent “gevoelige gegevens maskeren”?** Het vervangt geïdentificeerde vertrouwelijke tekst door een plaatshouder (bijv. `[REDACTED]`).  
- **Welke bibliotheek verwerkt OCR?** Microsoft Azure OCR‑connector, gebruikt via GroupDocs Redaction.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een permanente licentie is vereist voor productie.  
- **Kan ik gescande PDF's redigeren?** Ja—OCR extraheert de verborgen tekst voordat regex‑redacties worden toegepast.  
- **Is deze oplossing alleen voor Java?** Het voorbeeld is Java‑gebaseerd, maar GroupDocs biedt vergelijkbare API's voor .NET en andere platforms.

## Wat is OCR‑gebaseerde redactie?
OCR‑gebaseerde redactie voert eerst OCR uit op elke pagina, waardoor afbeeldingen worden omgezet in doorzoekbare tekst, en past vervolgens regex‑patronen toe om overeenkomsten te vervangen door een masker zoals `[REDACTED]`. Dit twee‑stappenproces stelt je in staat om betrouwbaar persoonlijke gegevens te verbergen, zelfs in gescande PDF's, en zorgt ervoor dat gevoelige tekenreeksen worden verwijderd voordat het document wordt gedeeld of gearchiveerd.

## Waarom GroupDocs Redaction gebruiken met Azure OCR?
Je moet GroupDocs Redaction met Azure OCR gebruiken omdat het **>98 % OCR‑nauwkeurigheid op gedrukte tekst** levert, **50+ invoer‑ en uitvoerformaten** ondersteunt, en **PDF's met honderden pagina's kan verwerken zonder het volledige bestand in het geheugen te laden**, waardoor snelle, schaalbare redactie voor compliance wordt gegarandeerd. De oplossing **schalend een PDF van 1.000 pagina's in minder dan 2 minuten op een 8‑core server verwerken** maakt batch‑taken praktisch.

## Voorvereisten
- **Java Development Kit (JDK) 8+** geïnstalleerd.  
- **Maven** (als je afhankelijkheidsbeheer verkiest) of de mogelijkheid om JAR‑bestanden handmatig te downloaden.  
- **Microsoft Azure OCR‑referenties** (endpoint en abonnementssleutel).  
- Basiskennis van Java en vertrouwdheid met reguliere expressies.

## GroupDocs Redaction voor Java instellen

### Maven‑configuratie
Voeg de GroupDocs‑repository en afhankelijkheid toe aan je `pom.xml`:

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
Als je handmatig JAR‑beheer verkiest, download dan de nieuwste release van [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Licentie‑acquisitie
- **Gratis proefversie** – verken alle functies zonder kosten.  
- **Tijdelijke licentie** – verleng de evaluatietijd.  
- **Volledige licentie** – ontgrendel productie‑klare mogelijkheden.

### Basisinitialisatie en configuratie
De `Redactor`‑klasse is de kernengine die OCR‑extractie uitvoert en redactieregels toepast op PDF‑documenten.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Hoe gevoelige gegevens maskeren met OCR‑redactie
Het maskeren van gevoelige gegevens met OCR‑redactie omvat het laden van de PDF met Azure OCR‑instellingen, het definiëren van regex‑patronen voor de gegevens die je wilt verbergen, en het aanroepen van de Redactor om elke overeenkomst te vervangen door een plaatshouder zoals `[REDACTED]`. De bibliotheek behandelt OCR, patroonmatching en PDF‑herwerking in één workflow.

### Stap 1: Document laden met OCR‑instellingen
`LoadOptions` configureert hoe GroupDocs een bestand laadt, waardoor je OCR‑connectors zoals Azure kunt doorgeven.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – vervang door het pad naar je PDF.  
- **`settings`** – bevat de Azure OCR‑connector die je eerder hebt gemaakt.

### Stap 2: Regex‑redacties definiëren en toepassen
`ReplacementOptions` specificeert de vervangende tekst die elke regex‑overeenkomst tijdens de redactie zal vervangen.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- Het patroon `\b\d{3}-\d{2}-\d{4}\b` komt overeen met Amerikaanse Social Security‑nummers.  
- `ReplacementOptions("[REDACTED]")` vervangt elke overeenkomst door het masker, waardoor effectief **gevoelige gegevens worden gemaskeerd**.

## Veelvoorkomende use‑cases voor het maskeren van gevoelige gegevens
1. **Beheer van juridische documenten** – verberg klant‑identificatoren voordat concepten worden gedeeld.  
2. **Financiële rapportage** – bescherm rekeningnummers en transactie‑ID's.  
3. **Gezondheidsdossiers** – voldoe aan HIPAA door patiënt‑identificatoren te redigeren.  
4. **Overheidspublicaties** – verwijder persoonlijke gegevens uit openbare registers.  
5. **Bedrijfscontracten** – verberg eigendomsvoorwaarden tijdens externe beoordelingen.

## Prestatietips
- **Regex optimaliseren** – vermijd te brede patronen die de verwerkingstijd verhogen; goed ontworpen expressies kunnen de runtime met tot 40 % verkorten.  
- **Geheugenbeheer** – sluit de `Redactor`‑instantie direct (try‑with‑resources doet dit automatisch).  
- **Asynchrone uitvoering** – voor bulkverwerking, voer redactietaken uit op aparte threads of gebruik een taak‑queue om de UI responsief te houden.

## Probleemoplossing
- **Azure‑referentie‑fout** – controleer de endpoint‑URL en abonnementssleutel in `MicrosoftAzureOcrConnector`.  
- **Document laadt niet** – controleer het bestandspad en zorg ervoor dat de PDF niet met een wachtwoord is beveiligd (of lever het wachtwoord via `LoadOptions`).  
- **Geen redacties toegepast** – test je regex eerst met een eenvoudige string; gebruik `Pattern.compile` in een unit‑test om overeenkomsten te bevestigen.

## Veelgestelde vragen

**Q: Wat is OCR‑redactie?**  
A: OCR‑redactie gebruikt Optical Character Recognition om verborgen tekst uit afbeeldingen of gescande PDF's te extraheren, en past vervolgens redactieregels toe om die tekst te maskeren.

**Q: Kan ik GroupDocs Redaction gebruiken zonder Azure OCR?**  
A: Ja, maar OCR verbetert de nauwkeurigheid aanzienlijk bij gescande documenten waar native tekste­xtractie faalt.

**Q: Hoe ga ik om met complexe regex‑patronen?**  
A: Bouw en test ze stap voor stap, gebruik Java’s `Pattern`‑klasse in een sandbox voordat je ze op grote documenten toepast.

**Q: Wat zijn typische prestatie‑knelpunten?**  
A: Grote PDF's, te complexe regex en synchrone OCR‑aanroepen kunnen de verwerking vertragen; overweeg batchverwerking en geoptimaliseerde patronen.

**Q: Is er ondersteuning beschikbaar voor implementatie‑problemen?**  
A: Zeker—neem contact op via het [GroupDocs‑forum](https://forum.groupdocs.com/c/redaction/33) voor community‑hulp of neem contact op met GroupDocs‑ondersteuning.

## Aanvullende bronnen
- **Documentatie**: https://docs.groupdocs.com/redaction/java/  
- **API‑referentie**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Gratis ondersteuning**: https://forum.groupdocs.com/c/redaction/33  
- **Tijdelijke licentie**: https://purchase.groupdocs.com/temporary-license/

---

**Last Updated:** 2026-06-26  
**Tested With:** GroupDocs.Redaction 24.9 (Java)  
**Author:** GroupDocs  

## Gerelateerde tutorials

- [Beveiligde PDF‑redactie met OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Hoe tekst te redigeren met GroupDocs.Redaction voor Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Gevoelige gegevens maskeren Java – Persoonlijke info redigeren met GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)