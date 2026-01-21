---
date: '2026-01-21'
description: Leer hoe u PDF's kunt redigeren met OCR en gescande documenten kunt redigeren
  met GroupDocs.Redaction voor Java met Azure OCR‑integratie.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: PDF redigeren met OCR met GroupDocs & Azure OCR – Java-gids
type: docs
url: /nl/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# PDF redigeren met OCR met GroupDocs & Azure OCR – Java‑gids

In deze uitgebreide tutorial ontdek je hoe je **PDF's met OCR kunt redigeren** in Java, met behulp van GroupDocs.Redaction in combinatie met Microsoft Azure OCR. Of je nu werkt met native PDF's of gescande afbeeldingen, deze gids laat zien hoe je nauwkeurig gevoelige gegevens kunt lokaliseren en maskeren, zodat je **gescande documenten kunt redigeren** om te voldoen aan privacy‑regelgeving.

## Snelle antwoorden
- **Wat doet OCR‑redactie?** Het extraheert tekst uit afbeeldingen/PDF‑bestanden en past automatisch redactieregels toe.  
- **Welke bibliotheek levert de redactiemotor?** GroupDocs.Redaction voor Java.  
- **Welke OCR‑service wordt gebruikt?** Microsoft Azure OCR‑connector.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor testen; een permanente licentie is vereist voor productie.  
- **Kan ik zowel native als gescande PDF's redigeren?** Ja – OCR maakt redactie van gescande documenten mogelijk.

## Wat betekent “PDF redigeren met OCR”?
PDF redigeren met OCR houdt in dat je optische tekenherkenning gebruikt om visuele tekst om te zetten in doorzoekbare strings, waarna je redactie‑patronen (bijv. regex) toepast om die informatie te verbergen voordat het bestand wordt gedeeld of opgeslagen.

## Waarom GroupDocs.Redaction gebruiken met Azure OCR?
- **Hoge nauwkeurigheid** op gescande pagina’s dankzij Azure’s cloud‑gebaseerde OCR‑engine.  
- **Eenvoudige Java‑API** die direct in je bestaande workflow integreert.  
- **Flexibele redactieregels** – regex, trefwoorden of aangepaste logica.  
- **Compliance‑klaar** output die gevoelige gegevens permanent verwijdert.

## Voorvereisten
- Java Development Kit (JDK) 8 of nieuwer.  
- Maven (of de mogelijkheid om de JAR handmatig te downloaden).  
- Microsoft Azure‑account met OCR‑referenties.  
- Basiskennis van Java en vertrouwdheid met reguliere expressies.

## GroupDocs.Redaction voor Java instellen

### Maven‑configuratie
Voeg de GroupDocs‑repository en afhankelijkheid toe aan uw `pom.xml`:

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
Als u liever geen Maven gebruikt, download dan de nieuwste JAR van de officiële release‑pagina: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Licentie‑acquisitie
- **Gratis proefversie** – verken de kernfuncties zonder verplichtingen.  
- **Tijdelijke licentie** – verleng de proefperiode voor grotere projecten.  
- **Volledige licentie** – ontgrendel onbeperkt gebruik en premium‑ondersteuning.

### Basisinitialisatie en -configuratie
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Hoe PDF met OCR in Java te redigeren

### Stap 1: Document laden met OCR‑instellingen
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Subsequent redaction steps will be placed here
}
```
- **Parameters**  
  - `"YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf"` – pad naar de doel‑PDF.  
  - `new LoadOptions()` – standaard laadconfiguratie.  
  - `settings` – bevat deummers)
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
- **Regex‑uitleg** – `\2}-\d{4}\b` matcht patronen zoals `123-45-6789`.  
- ** de applicatie lees‑/schrijfrechten heeft.  
- **Prestatische use‑cases voor het redigeren vanAdvocatenkantoren** – verberg klant‑identificatoren voordat zaak‑bestanden worden gedeeld.  
2. **Financiële instellingen** – maskeren van rekeningnummers in gescande afschriften.  
3. **Zorgverleners** – beschermen van patiënt‑PHI in gescande medische dossiers.  
4. **Overheidsinstanties** – persoonlijke gegevens verwijderen uit openbare PDF‑registers.  
5. **Enter audits door verkorten.  
- Maak de `Redactor`‑instantie snel vrij (gebruik try‑with‑resources zoals getoond).  
 tekst verwijderen.

**Q: Kan ik GroupDocs.Redaction gebruiken zonder Azure OCR?**  
A: Ja, maar OCR verbetert de nauwkeurigheid voor gescande documenten aanzienlijk, waardoor je **gescande documenten effectief kunt redigeren**.

**Q: Hoeronen?**  
A: Test patronen met voorbeelddata, gebruik woordgrenzen (`\b`) om gedeeltelijke matches te vermijden, en overweeg grote expressies op te splitsen in meerdere eenvoudigere redacties.

**Q: Wat zijn typische prestatie‑knelpunten?**  
A: Zware OCR‑aanroepen op grote bestanden, te brede regex en onvoldoende geheugenallocatie. Optimaliseer door regex af te stemmen en resources kan‑forum: [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33).

## AanGroupDocsGratis ondersteuning**: https.com/temporary-license/

---

**Laatst bijgewerkt:** 2026-01-21  
**Getest met:** GroupDocs.Redaction 24.9 voor Java  
**Auteur:** GroupDocs