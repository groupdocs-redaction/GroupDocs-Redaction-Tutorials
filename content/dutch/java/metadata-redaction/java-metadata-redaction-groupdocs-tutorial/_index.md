---
date: '2026-09-26'
description: Leer hoe je metadata kunt redigeren met GroupDocs in Java, waarbij je
  vertrouwelijke documentmetadata veilig verwijdert en het oorspronkelijke formaat
  intact houdt.
keywords:
- how to redact metadata
- GroupDocs Redaction Java
- secure document processing
- metadata removal Java
lastmod: '2026-09-26'
og_description: Hoe metadata te redigeren met GroupDocs in Java – een stapsgewijze
  handleiding die laat zien hoe je vertrouwelijke documentmetadata veilig kunt verwijderen
  en het oorspronkelijke formaat behoudt.
og_image_alt: Guide showing metadata redaction using GroupDocs in Java
og_title: Hoe metadata te redigeren met GroupDocs in Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  headline: How to redact metadata with GroupDocs in Java
  type: TechArticle
- description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  name: How to redact metadata with GroupDocs in Java
  steps:
  - name: import necessary classes
    text: These imports give you access to the redaction engine, save options, and
      metadata utilities.
  - name: initialize redactor
    text: Instantiate the `Redactor` with the path to your source file.
  - name: configure metadata search and redaction
    text: Create a `MetadataSearchRedaction` that looks for the exact string **"Company
      Ltd."** and replaces it with **"--company--"**. The `setFilter` call limits
      the operation to the *Company* metadata field only.
  - name: apply the redaction
    text: Run the redaction against the opened document.
  - name: save with custom options
    text: '`SaveOptions` allows you to specify output format, file naming, and other
      saving parameters for the redacted document. Configure `SaveOptions` so the
      redacted file gets a “_Redacted” suffix while preserving its original format.'
  - name: release resources
    text: Always close the `Redactor` to free native resources and avoid memory leaks.
  type: HowTo
- questions:
  - answer: It’s a powerful library that enables you to redact text, metadata, and
      images in documents using Java applications.
    question: What is GroupDocs.Redaction for Java?
  - answer: Yes, but with limitations. A free trial or temporary license allows full
      access for testing purposes.
    question: Can I use GroupDocs.Redaction without purchasing a license?
  - answer: Use `SaveOptions` to specify your requirements, such as avoiding rasterization
      when saving to PDF.
    question: How do I ensure document formats are preserved during redaction?
  - answer: It supports a wide range, including Word, Excel, PowerPoint, PDF, and
      many more.
    question: What types of documents can be redacted using GroupDocs.Redaction?
  - answer: Visit the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for assistance.
    question: Where can I find support if I run into issues?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document security
- redaction tutorial
title: Hoe metadata te redigeren met GroupDocs in Java
type: docs
url: /nl/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# Hoe metadata redigeren met GroupDocs in Java

In deze uitgebreide tutorial leer je **hoe je metadata kunt redigeren** van Word, PDF en vele andere documenttypen met behulp van GroupDocs.Redaction voor Java. Aan het einde van de gids kun je metadata‑redactie integreren in elke Java‑gebaseerde service, zodat vertrouwelijke informatie zoals bedrijfsnamen, auteurs of aangepaste eigenschappen nooit je organisatie verlaat.

## Snelle antwoorden
- **Wat doet MetadataSearchRedaction?** Het zoekt naar specifieke metadata‑velden en vervangt hun waarden door aangepaste tekst.  
- **Welke bibliotheek is vereist?** GroupDocs.Redaction for Java (v24.9 or newer).  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een volledige licentie is vereist voor productie.  
- **Kan ik het oorspronkelijke bestandsformaat behouden?** Ja—gebruik `SaveOptions` om het oorspronkelijke formaat te behouden.  
- **Is deze aanpak thread‑safe?** Elke `Redactor`‑instantie is onafhankelijk, zodat je documenten parallel kunt verwerken.

## Hoe metadata redigeren met GroupDocs?
`Redactor` is de kernklasse die een document laadt en redactie‑bewerkingen biedt.  
Laad je brondocument met een `Redactor`‑instantie, configureer een `MetadataSearchRedaction` die zich richt op de exacte metadata‑sleutel die je wilt zuiveren, voer de redactie uit, en sla het bestand uiteindelijk op met `SaveOptions`. Deze volledige workflow kan worden uitgedrukt in slechts een handvol regels en werkt voor elk ondersteund formaat, van DOCX tot PDF en verder.

## Wat is metadata‑redactie met GroupDocs?
`MetadataSearchRedaction` is een gespecialiseerde klasse die je in staat stelt een specifieke metadata‑eigenschap (bijv. *Company*, *Author*) te targeten en de inhoud te vervangen door een tijdelijke aanduiding. Het is ideaal wanneer je bedrijfsgegevens moet anonimiseren voordat je documenten deelt met externe partners. Het redactieproces wijzigt geen andere documentelementen, waardoor de visuele lay-out en inhoud intact blijven nadat de metadata is verwijderd.

## Waarom metadata‑redactie gebruiken met GroupDocs?
Metadata‑redactie met GroupDocs biedt een betrouwbare manier om gevoelige informatie uit documenten te verwijderen terwijl hun oorspronkelijke uiterlijk en structuur behouden blijven. Door je te richten op metadata‑velden kun je snel voldoen aan privacy‑normen zonder de zichtbare inhoud te wijzigen of per ongeluk gegevenslekken te riskeren.

- **Precisie** – Redigeer alleen de velden die je opgeeft, en laat de rest van het document onaangeroerd.  
- **Naleving** – Helpt te voldoen aan GDPR, HIPAA en andere privacy‑regelgeving door verborgen identifiers te verwijderen.  
- **Automatisering‑klaar** – Past naadloos in batch‑verwerkingspijplijnen of micro‑services.  
- **Brede formaatondersteuning** – GroupDocs.Redaction ondersteunt **50+ invoer‑ en uitvoerformaten** (inclusief DOCX, PDF, PPTX, XLSX en afbeeldingsformaten) en kan multi‑honderd‑pagina‑bestanden verwerken zonder het volledige document in het geheugen te laden.

## Vereisten
- **GroupDocs.Redaction for Java** ≥ 24.9.  
- Java 8 of nieuwer geïnstalleerd op je machine.  
- Een IDE zoals IntelliJ IDEA of Eclipse (optioneel maar aanbevolen).  
- Basiskennis van Maven (of de mogelijkheid om JAR‑bestanden handmatig toe te voegen).  

## GroupDocs.Redaction voor Java instellen

Voeg de repository en afhankelijkheid toe aan je `pom.xml`. Deze stap zorgt ervoor dat Maven de bibliotheek automatisch kan downloaden.

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

*Alternatief kun je de JAR direct downloaden van de officiële release‑pagina:*  
[GroupDocs.Redaction voor Java releases](https://releases.groupdocs.com/redaction/java/)

### Licentie‑acquisitie
- **Gratis proefversie** – Download een proeflicentie om alle functies te verkennen.  
- **Tijdelijke licentie** – Gebruik voor uitgebreid testen.  
- **Volledige licentie** – Vereist voor productie‑implementaties.

## Basisinitialisatie
`Redactor` laadt een document en biedt methoden om verschillende redacties toe te passen.  
Maak een `Redactor`‑instantie aan die wijst naar het document dat je wilt verwerken.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Implementatie‑gids

### Stap 1: importeer benodigde klassen
Deze imports geven je toegang tot de redactie‑engine, opslaan‑opties en metadata‑hulpmiddelen.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### Stap 2: initialiseert de redactor
Instantieer de `Redactor` met het pad naar je bronbestand.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### Stap 3: configureer metadata‑zoekopdracht en redactie
Maak een `MetadataSearchRedaction` die zoekt naar de exacte tekenreeks **"Company Ltd."** en vervangt deze door **"--company--"**. De `setFilter`‑aanroep beperkt de bewerking tot alleen het *Company*‑metadata‑veld.

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### Stap 4: pas de redactie toe
Voer de redactie uit op het geopende document.

```java
redactor.apply(redaction);
```

### Stap 5: opslaan met aangepaste opties
`SaveOptions` stelt je in staat om het uitvoerformaat, bestandsnaamgeving en andere opslaan‑parameters voor het geredigeerde document op te geven.  
Configureer `SaveOptions` zodat het geredigeerde bestand een “_Redacted”‑achtervoegsel krijgt terwijl het oorspronkelijke formaat behouden blijft.

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### Stap 6: resources vrijgeven
Sluit altijd de `Redactor` om native resources vrij te geven en geheugenlekken te voorkomen.

```java
finally {
    redactor.close();
}
```

## Veelvoorkomende problemen en oplossingen
- **FileNotFoundException** – Dubbel‑controleer het pad dat je aan `Redactor` doorgeeft. Gebruik absolute paden of `Paths.get(...)` voor betrouwbaarheid.  
- **No changes observed** – Controleer of het metadata‑veld dat je target daadwerkelijk de zoekreeks bevat; metadata is standaard hoofdlettergevoelig.  
- **Out‑of‑memory errors on large files** – Verwerk documenten in kleinere batches en roep `redactor.close()` direct aan na elk bestand.

## Praktische toepassingen
1. **Juridische documentatie** – Verwijder klantbedrijfsnamen voordat je contracten naar derden stuurt.  
2. **Financiële rapportage** – Anonimiseer interne identifiers in auditbestanden.  
3. **Samenwerkingsprojecten** – Bescherm eigendomsinformatie bij het delen van concepten met externe leveranciers.

## Prestatie‑overwegingen
- **Geheugenbeheer** – De bibliotheek houdt het volledige document in het geheugen; het sluiten van de `Redactor` na elk bestand is essentieel.  
- **Batchverwerking** – Voor scenario's met hoog volume, loop door een collectie bestanden en hergebruik een enkele `SaveOptions`‑instantie.  
- **Blijf up‑to‑date** – Nieuwe releases brengen prestatie‑verbeteringen en bug‑fixes; richt je altijd op de nieuwste stabiele versie.

## Veelgestelde vragen

**Q: Wat is GroupDocs.Redaction voor Java?**  
A: Het is een krachtige bibliotheek die je in staat stelt tekst, metadata en afbeeldingen in documenten te redigeren met Java‑applicaties.

**Q: Kan ik GroupDocs.Redaction gebruiken zonder een licentie aan te schaffen?**  
A: Ja, maar met beperkingen. Een gratis proefversie of tijdelijke licentie biedt volledige toegang voor testdoeleinden.

**Q: Hoe zorg ik ervoor dat documentformaten behouden blijven tijdens redactie?**  
A: Gebruik `SaveOptions` om je eisen te specificeren, zoals het vermijden van rasterisatie bij het opslaan naar PDF.

**Q: Welke soorten documenten kunnen worden geredigeerd met GroupDocs.Redaction?**  
A: Het ondersteunt een breed scala, inclusief Word, Excel, PowerPoint, PDF en nog veel meer.

**Q: Waar kan ik ondersteuning vinden als ik problemen ondervind?**  
A: Bezoek het [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) voor hulp.

**Q: Werkt MetadataSearchRedaction met versleutelde documenten?**  
A: Ja. Laad het document met het juiste wachtwoord via de `Redactor`‑constructor die een wachtwoordparameter accepteert.

**Q: Kan ik meerdere metadata‑redacties in één run combineren?**  
A: Absoluut. Maak meerdere `MetadataSearchRedaction`‑objecten, stel verschillende filters in, en pas ze opeenvolgend toe vóór het opslaan.

**Q: Is het mogelijk om redactie‑resultaten te bekijken vóór het opslaan?**  
A: Je kunt `redactor.getRedactions()` aanroepen om een lijst van pending redactions op te halen en ze programmatisch te inspecteren.

## Aanvullende bronnen
- **Documentation**: Verken gedetailleerde handleidingen op [GroupDocs Documentatie](https://docs.groupdocs.com/redaction/java/).  
- **API reference**: Bekijk de volledige API‑referentie op [GroupDocs API-referentie](https://reference.groupdocs.com/redaction/java).  
- **Download library**: Download de nieuwste release van [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **Source code**: Bekijk en draag bij op [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).  
- **Support**: Krijg hulp via het gratis supportkanaal op [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33).

---

**Laatst bijgewerkt:** 2026-09-26  
**Getest met:** GroupDocs.Redaction 24.9 for Java  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Groupdocs Redaction Java Document Metadata Extractie](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [metadata-tekst vervangen java – Veilige redactie met GroupDocs](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [Documentinformatie ophalen met Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)