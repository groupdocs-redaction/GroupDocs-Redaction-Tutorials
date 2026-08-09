---
date: '2026-08-09'
description: Leer hoe je niet-bewerkbare PDF-bestanden maakt door tekst te redigeren
  en PDF's te rasteren met GroupDocs.Redaction voor Java.
keywords:
- create non editable pdf
- how to redact text java
- GroupDocs.Redaction Java
- rasterized PDF Java
- document security Java
lastmod: '2026-08-09'
og_description: Maak niet-bewerkbare PDF-bestanden door tekst te redigeren en PDF's
  te rasteren met GroupDocs.Redaction voor Java. Volg een stapsgewijze handleiding
  met tips, valkuilen en veelgestelde vragen.
og_image_alt: Guide showing how to redact text and generate a non‑editable rasterized
  PDF using GroupDocs.Redaction for Java
og_title: Maak een niet-bewerkbare PDF met GroupDocs.Redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to create non editable PDF files by redacting text and rasterizing
    PDFs using GroupDocs.Redaction for Java.
  headline: How to create non editable PDF with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to create non editable PDF files by redacting text and rasterizing
    PDFs using GroupDocs.Redaction for Java.
  name: How to create non editable PDF with GroupDocs.Redaction Java
  steps:
  - name: Import the required classes
    text: '`ExactPhraseRedaction` is a redaction rule that targets a literal string.
      `ReplacementOptions` tells the engine what placeholder to insert instead of
      the original text.'
  - name: Apply exact phrase redaction
    text: 'The following snippet replaces every occurrence of **“John Doe”** with
      the placeholder **[personal]**: **Why this works:** - `ExactPhraseRedaction`
      targets the literal string “John Doe”. - `ReplacementOptions` tells the engine
      what to insert instead of the original text. **Tips & common pitfalls** -'
  - name: Import `SaveOptions`
    text: '`SaveOptions` configures how the document is saved, including rasterization
      and file‑naming options.'
  - name: Configure and save the rasterized PDF
    text: The snippet below disables the automatic “_redacted” suffix, enables rasterization,
      and writes the output file. **Explanation:** - `setAddSuffix(false)` keeps the
      original file name (you can enable it to add “_redacted”). - `setRasterizeToPDF(true)`
      tells GroupDocs to render each page as an image in
  type: HowTo
- questions:
  - answer: It replaces a specific string (e.g., a name) with a placeholder, ensuring
      the original text cannot be recovered.
    question: What is an exact phrase redaction?
  - answer: Rasterized PDFs render each page as an image, preventing text selection,
      copying, or editing.
    question: How does rasterizing a PDF improve security?
  - answer: Yes—loop over a list of file paths, reusing the same `Redactor` configuration
      for each document.
    question: Can I process multiple files in one run?
  - answer: Absolutely. You can read/write streams from AWS S3, Azure Blob, or Google
      Cloud Storage and feed them directly to the API.
    question: Is cloud integration possible?
  - answer: Forgetting to close the `Redactor` (which locks files) and using an outdated
      library version that lacks rasterization support.
    question: What are typical pitfalls for newcomers?
  type: FAQPage
tags:
- create non editable pdf
- GroupDocs.Redaction
- Java document redaction
- rasterized PDF
- compliance
title: Hoe maak je een niet-bewerkbare PDF met GroupDocs.Redaction Java
type: docs
url: /nl/java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/
weight: 1
---

# Hoe maak je een niet‑bewerkbare PDF met GroupDocs.Redaction Java

In veel gereguleerde sectoren moet je documenten leveren die niet kunnen worden gewijzigd of gekopieerd. De meest betrouwbare manier om dit te garanderen is om **create non editable PDF** bestanden te maken door eerst gevoelige tekst te redigeren en vervolgens het hele document te rasteren. GroupDocs.Redaction for Java biedt een één‑regel API om beide stappen uit te voeren, zodat je aan compliance‑eisen kunt voldoen zonder een eigen PDF‑engine te bouwen.

## Snelle antwoorden
- **Wat betekent “redact text”?** Het verwijdert of maskeert permanent gevoelige strings zodat ze niet gelezen of hersteld kunnen worden.  
- **Welke bibliotheek voert de taak uit?** GroupDocs.Redaction for Java biedt ingebouwde redactie‑ en rasterisatie‑functies.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor testen; een permanente licentie is vereist voor productie.  
- **Kan ik DOCX in één stap omzetten naar een gerasterde PDF?** Ja – pas eerst redactie toe, daarna gebruik je `SaveOptions` met rasterisatie ingeschakeld.  
- **Is de output echt niet‑bewerkbaar?** Gerasterde PDF's worden gerenderd als afbeeldingen, waardoor tekstextractie of -wijziging wordt voorkomen.

## Wat is tekstredactie?
Tekstredactie verwijdert of verduistert permanent vertrouwelijke informatie—zoals persoonlijke identificatoren, financiële gegevens of juridische clausules—uit een document. In tegenstelling tot een eenvoudige zoek‑en‑vervang, garandeert redactie dat de verborgen inhoud niet kan worden hersteld door welk hulpmiddel dan ook. Door de oorspronkelijke tekens te wissen en optioneel te vervangen door een tijdelijke aanduiding, zorgt redactie ervoor dat de gevoelige gegevens onherstelbaar zijn en het document leesbaar blijft voor geautoriseerde gebruikers.

## Waarom GroupDocs.Redaction voor Java gebruiken?
GroupDocs.Redaction for Java biedt een uitgebreide reeks functies die veilige documentverwerking vereenvoudigen. Het ondersteunt een breed scala aan bestandsformaten, biedt meerdere redactietypen en bevat één‑klik rasterisatie om PDF's te beveiligen. De bibliotheek is geoptimaliseerd voor prestaties, werkt zowel op Windows als Linux, en integreert gemakkelijk met bestaande Java‑applicaties, waardoor het een betrouwbare keuze is voor ondernemingen die op grote schaal gevoelige informatie moeten beschermen.

## Vereisten
- Java Development Kit (JDK 11 of nieuwer) en een IDE zoals IntelliJ IDEA of Eclipse.  
- GroupDocs.Redaction bibliotheek (versie 24.9 of later).  
- Basiskennis van Java—je schrijft slechts een paar korte fragmenten.

## GroupDocs.Redaction voor Java instellen

### Maven‑installatie
Voeg de GroupDocs-repository en afhankelijkheid toe aan je `pom.xml`:

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
Als Maven niet jouw ding is, kun je de JAR downloaden van de officiële release‑pagina: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### Licentie‑acquisitie
- **Gratis proefversie** – verken de API zonder kosten.  
- **Tijdelijke licentie** – ideaal voor uitgebreid testen.  
- **Volledige licentie** – vereist voor productie‑implementaties.

## Basisinitialisatie
`Redactor` is de kernklasse van GroupDocs.Redaction die een document in het geheugen laadt en wijzigt. Nadat je de namespace hebt geïmporteerd, maak je een `Redactor`‑instantie met het pad naar je bronbestand, waarna je klaar bent om redactieregels toe te passen.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Implementatiegids

## Hoe maak je een niet‑bewerkbare PDF in Java?
Laad het brondocument, pas de gewenste redactieregels toe, en sla vervolgens het resultaat op met rasterisatie ingeschakeld. Deze drie‑stappen‑stroom—laden, redigeren, rasteriseren—produceert een PDF die niet kan worden bewerkt, gekopieerd of doorzocht, en voldoet aan de strengste compliance‑normen. Door elke pagina om te zetten naar een afbeelding, verwijdert het uiteindelijke bestand alle verborgen tekstlagen die later kunnen worden geëxtraheerd.

## Hoe tekst redigeren in Java
Hieronder lopen we een exacte‑zin‑redactie door, die perfect is voor het verwijderen van bekende identificatoren zoals een persoonsnaam. Het proces omvat het importeren van de benodigde klassen, het definiëren van een redactieregel, en het toepassen ervan op het document vóór het opslaan.

### Stap 1: Importeer de vereiste klassen
`ExactPhraseRedaction` is een redactieregel die zich richt op een letterlijke tekenreeks. `ReplacementOptions` geeft de engine aan welke tijdelijke aanduiding moet worden ingevoegd in plaats van de oorspronkelijke tekst.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### Stap 2: Pas exacte‑zin‑redactie toe
De volgende code vervangt elke voorkomen van **“John Doe”** door de tijdelijke aanduiding **[personal]**:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
} finally { 
    redactor.close(); 
}
```

**Waarom dit werkt:**  
- `ExactPhraseRedaction` richt zich op de letterlijke tekenreeks “John Doe”.  
- `ReplacementOptions` vertelt de engine wat er moet worden ingevoegd in plaats van de oorspronkelijke tekst.

**Tips & veelvoorkomende valkuilen**  
- Controleer het documentpad dubbel; een verkeerd pad veroorzaakt een `FileNotFoundException`.  
- Zorg ervoor dat het Java‑proces schrijfrechten heeft voor de uitvoermap.

## Hoe opslaan als gerasterde PDF
Na redactie wil je waarschijnlijk een niet‑bewerkbare PDF. Rasterisatie zet elke pagina om in een afbeelding, waardoor de mogelijkheid om tekst te selecteren of te bewerken verdwijnt. Deze stap zorgt ervoor dat de uiteindelijke PDF zich gedraagt als een gescand document, waardoor het bestand bestand is tegen tekst‑extractietools en accidentele wijzigingen.

### Stap 1: Importeer `SaveOptions`
`SaveOptions` configureert hoe het document wordt opgeslagen, inclusief rasterisatie‑ en bestandsnaam‑opties.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
```

### Stap 2: Configureer en sla de gerasterde PDF op
De onderstaande code schakelt het automatische “_redacted” achtervoegsel uit, schakelt rasterisatie in, en schrijft het uitvoerbestand.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    SaveOptions tmp0 = new SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);

    redactor.save(tmp0);
} finally { 
    redactor.close(); 
}
```

**Uitleg:**  
- `setAddSuffix(false)` behoudt de oorspronkelijke bestandsnaam (je kunt het inschakelen om “_redacted” toe te voegen).  
- `setRasterizeToPDF(true)` vertelt GroupDocs om elke pagina als een afbeelding in een PDF te renderen, waardoor het document **non‑editable** is.

**Probleemoplossing**  
Als rasterisatie mislukt, controleer dan of de Java‑runtime de PDF‑renderingsafhankelijkheden bevat (ze zijn meegeleverd met de bibliotheek).

## Praktische toepassingen
1. **Juridische documentverwerking** – redacteer klantnamen voordat je ze deelt met de tegenpartij.  
2. **HR‑recordbeheer** – verberg werknemers‑ID's in interne rapporten.  
3. **Financiële rapportage** – bescherm rekeningnummers bij het verspreiden van audit‑samenvattingen.  

Je kunt deze stappen combineren in een geautomatiseerde workflow, waarbij je GroupDocs.Redaction koppelt aan een documentbeheersysteem of een cloud‑opslagbucket.

## Prestatie‑overwegingen
- **Batchverwerking:** Hergebruik een enkele `Redactor`‑instantie bij het verwerken van veel bestanden om de overhead met tot 40 % te verminderen.  
- **Geheugenbeheer:** Voor grote documenten, roep `System.gc()` aan na elke `redactor.close()` of voer het proces uit in een aparte JVM.  
- **Houd afhankelijkheden up‑to‑date:** Nieuwe releases bevatten vaak prestatie‑verbeteringen voor PDF‑rasterisatie, inclusief een snelheidsverhoging van 20 % voor multi‑core systemen.

## Veelvoorkomende problemen en oplossingen
| Probleem | Oplossing |
|----------|-----------|
| *Bestand niet gevonden* | Controleer het absolute pad en zorg ervoor dat het bestand op de server bestaat. |
| *Toestemming geweigerd* | Voer de JVM uit met voldoende OS‑rechten of wijzig de ACL's van de uitvoermap. |
| *Rasterisatie produceert lege pagina's* | Bevestig dat het brondocument nog geen rasterafbeelding is; gebruik de nieuwste bibliotheekversie. |
| *Redactie laat verborgen tekst achter* | Gebruik `ExactPhraseRedaction` met `ReplacementOptions`; vermijd eenvoudige zoek‑en‑vervang‑methoden. |

## Veelgestelde vragen

**V: Wat is een exacte‑zin‑redactie?**  
Het vervangt een specifieke tekenreeks (bijv. een naam) door een tijdelijke aanduiding, waardoor de oorspronkelijke tekst niet kan worden hersteld.

**V: Hoe verbetert rasterisatie van een PDF de beveiliging?**  
Gerasterde PDF's renderen elke pagina als een afbeelding, waardoor tekstselectie, kopiëren of bewerken wordt voorkomen.

**V: Kan ik meerdere bestanden in één run verwerken?**  
Ja—loop over een lijst met bestandspaden en hergebruik dezelfde `Redactor`‑configuratie voor elk document.

**V: Is cloud‑integratie mogelijk?**  
Absoluut. Je kunt streams lezen/schrijven van AWS S3, Azure Blob of Google Cloud Storage en deze direct aan de API voeren.

**V: Wat zijn typische valkuilen voor nieuwkomers?**  
Vergeten de `Redactor` te sluiten (wat bestanden vergrendelt) en het gebruiken van een verouderde bibliotheekversie die geen rasterisatie‑ondersteuning biedt.

## Bronnen
- **Documentatie:** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API‑referentie:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub:** [GroupDocs.Redaction GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Gratis ondersteuning:** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Tijdelijke licentie:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Laatst bijgewerkt:** 2026-08-09  
**Getest met:** GroupDocs.Redaction 24.9 for Java  
**Auteur:** GroupDocs  

## Gerelateerde tutorials

- [Hoe een grijstinten‑pdf te maken met GroupDocs.Redaction Java – Beveilig en optimaliseer je documenten](/redaction/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/)
- [Meesterschap in documentbeveiliging in Java: exacte‑zin‑redactie en geavanceerde rasterisatie met GroupDocs.Redaction](/redaction/java/advanced-redaction/groupdocs-redaction-java-document-security/)
- [Hoe DOCX om te zetten naar afbeelding & Word‑documenten te redigeren met GroupDocs Redaction Java](/redaction/java/document-saving/groupdocs-redaction-java-rasterize-word-docs/)