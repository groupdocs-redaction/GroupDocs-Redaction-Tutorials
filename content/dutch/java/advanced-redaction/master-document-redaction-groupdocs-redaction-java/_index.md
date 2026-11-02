---
date: '2026-11-02'
description: Leer hoe je een achtervoegsel aan een bestandsnaam toevoegt in een GroupDocs
  redaction Java-tutorial met Maven, streaming load, annotation deletion en save-opties.
keywords:
- groupdocs redaction java tutorial
- add suffix filename java
- document redaction workflow
- groupdocs maven dependency
- java inputstream redaction
lastmod: '2026-11-02'
og_description: Leer hoe je een achtervoegsel aan een bestandsnaam toevoegt in een
  GroupDocs redaction Java-tutorial. Volg stap-voor-stap Maven-setup, streaming load
  en save-opties.
og_image_alt: Guide showing Java code to add suffix to redacted filenames using GroupDocs
  Redaction
og_title: Hoe een achtervoegsel aan een bestandsnaam toevoegen in GroupDocs redaction
  Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  headline: How to add suffix to filename in GroupDocs redaction Java
  type: TechArticle
- description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  name: How to add suffix to filename in GroupDocs redaction Java
  steps:
  - name: '1: Create InputStream'
    text: '- **Why:** Using `InputStream` allows you to handle documents stored in
      various locations—cloud buckets, databases, or in‑memory buffers—without first
      writing them to disk. This approach is essential when you need to **load document
      from stream** in micro‑service architectures.'
  - name: '1: Apply DeleteAnnotationRedaction'
    text: '- **Why:** This step ensures that any sensitive annotations (comments,
      highlights, or hidden notes) are stripped from the document, enhancing privacy
      and compliance.'
  - name: '1: Configure SaveOptions'
    text: '- **Why:** Customizing save options allows flexible output formats and
      naming conventions. Enabling `setAddSuffix(true)` **adds suffix to filename**,
      making it clear that the file has been redacted.'
  type: HowTo
- questions:
  - answer: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.
    question: Can I redact PDF documents using GroupDocs.Redaction?
  - answer: Use streaming (`load document from stream`) and close resources promptly
      to keep memory usage low.
    question: What is the best way to handle large files with GroupDocs.Redaction?
  - answer: The API automatically adds a default suffix (e.g., “_redacted”). For custom
      suffixes, rename the output file after saving.
    question: Is it possible to customize the suffix text?
  - answer: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/)
      and follow the instructions.
    question: How do I obtain a temporary license for GroupDocs.Redaction?
  - answer: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for expert assistance.
    question: Where can I get help if I encounter issues?
  type: FAQPage
tags:
- groupdocs redaction
- java tutorial
- maven dependency
- document redaction
title: Hoe een achtervoegsel aan een bestandsnaam toevoegen in GroupDocs redaction
  Java
type: docs
url: /nl/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Hoe een suffix toe te voegen aan bestandsnaam in GroupDocs Redaction Java

In deze **groupdocs redaction java tutorial** leer je hoe je automatisch een suffix kunt toevoegen aan de uitvoerbestandsnaam bij het redigeren van documenten met GroupDocs.Redaction. Het toevoegen van een suffix elimineert handmatig hernoemen, vermindert het risico op lekken van niet-geredigeerde bestanden, en past netjes in CI/CD‑pipelines die afhankelijk zijn van naamgevingsconventies. De gids leidt je door Maven‑setup, streaming‑documentladen, annotatieverwijdering en het configureren van opslaan‑opties — allemaal met beknopte, productie‑klare code.

## Snelle antwoorden
- **Wat doet “add suffix to filename”?**  
  Wanneer je de suffix‑optie inschakelt, voegt de SDK automatisch een vooraf gedefinieerde tekenreeks (standaard “_redacted”) toe aan de basisnaam van het uitvoerbestand vóór de extensie. Hierdoor is in één oogopslag duidelijk welke bestanden zijn verwerkt, helpt het onbedoelde distributie van originele inhoud te voorkomen, en vereenvoudigt het downstream‑automatisering die afhankelijk is van naamgevingspatronen.  
- **Kan ik een document laden vanuit een stream?**  
  Ja—GroupDocs.Redaction ondersteunt het laden vanuit elke `InputStream`, perfect voor cloudopslag of in‑memory verwerking.  
- **Heb ik een licentie nodig voor deze functie?**  
  Een gratis proefversie werkt voor basisredactie; een tijdelijke of volledige licentie ontgrendelt alle geavanceerde opties, inclusief suffix‑verwerking.  
- **Welke formaten worden ondersteund?**  
  De bibliotheek ondersteunt DOCX, PDF, PPTX, XLSX en nog veel meer.  
- **Is rasterisatie vereist voor PDF‑uitvoer?**  
  Rasterisatie is optioneel; schakel het in wanneer je het document moet flattenen voor extra beveiliging.

## Wat doet “add suffix to filename”?

Wanneer je de suffix‑optie inschakelt, voegt de SDK automatisch een vooraf gedefinieerde tekenreeks (standaard “_redacted”) toe aan de basisnaam van het uitvoerbestand vóór de extensie. Hierdoor is in één oogopslag duidelijk welke bestanden zijn verwerkt, helpt het onbedoelde distributie van originele inhoud te voorkomen, en vereenvoudigt het downstream‑automatisering die afhankelijk is van naamgevingspatronen.

## Waarom GroupDocs.Redaction voor deze taak gebruiken?

GroupDocs.Redaction biedt een high‑performance Java‑API die redactietaken combineert met flexibele bestands‑handlingsopties zoals automatische suffix‑toevoeging, streaming‑ondersteuning en batch‑verwerking. Het ondersteunt meer dan 50 invoer‑ en uitvoerformaten en kan documenten van honderden pagina's verwerken zonder het volledige bestand in het geheugen te laden, wat zorgt voor laag geheugenverbruik en snelle uitvoering.

## Vereisten

- **Java Development Kit (JDK):** Versie 8 of hoger.  
- **GroupDocs.Redaction Library:** Kernbibliotheek voor redactietaken.  
- **IDE:** IntelliJ IDEA, Eclipse, of een andere Java‑compatibele editor.  
- **Maven:** Voor afhankelijkheidsbeheer.  

### Kennisvereisten
Bekendheid met Java I/O en basisobject‑georiënteerde concepten maakt de voorbeelden makkelijker te volgen.

## GroupDocs.Redaction voor Java instellen

### Maven‑configuratie
Voeg de volgende configuratie toe aan je `pom.xml`‑bestand om toegang te krijgen tot GroupDocs‑bibliotheken via Maven:

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
Download anders de nieuwste versie direct van [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Licentie‑acquisitie
1. **Gratis proefversie:** Toegang tot basisfunctionaliteit zonder beperkingen.  
2. **Tijdelijke licentie:** Verkrijg een tijdelijke licentie om geavanceerde functies te verkennen.  
3. **Aankoop:** Overweeg voor langdurig gebruik een volledige licentie aan te schaffen.

#### Basisinitialisatie en configuratie
Initialiseer je project door de benodigde imports toe te voegen:

```java
import com.groupdocs.redaction.Redactor;
```

Met deze configuratie ben je klaar om document‑redactiefuncties te implementeren.

## Implementatie‑gids

### Functie 1: document laden vanuit stream
**Overzicht:** Leer hoe je documenten in een `InputStream` laadt voor verwerking.

`InputStream` is een Java‑I/O‑klasse die een stroom bytes vertegenwoordigt, waardoor je gegevens kunt lezen uit bestanden, netwerkverbindingen of andere bronnen zonder de volledige inhoud in het geheugen te laden.

#### Stap 1.1: inputstream maken

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Waarom:** Met `InputStream` kun je documenten behandelen die op verschillende locaties zijn opgeslagen—cloud‑buckets, databases of in‑memory buffers—zonder ze eerst naar schijf te schrijven. Deze aanpak is essentieel wanneer je **load document from stream** moet gebruiken in micro‑service‑architecturen.

### Functie 2: annotatie‑verwijderings‑redactie toepassen
**Overzicht:** Verwijder annotaties uit je document met behulp van de `DeleteAnnotationRedaction`.

`DeleteAnnotationRedaction` is een redactiebewerking die alle annotaties—zoals opmerkingen, markeringen en notities—uit het document verwijdert.

#### Stap 2.1: deleteannotationredaction toepassen

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Waarom:** Deze stap zorgt ervoor dat gevoelige annotaties (opmerkingen, markeringen of verborgen notities) uit het document worden verwijderd, wat de privacy en naleving verbetert.

### Functie 3: document opslaan met opties
**Overzicht:** Leer hoe je je verwerkte document opslaat met specifieke opties zoals rasterisatie en **add suffix filename java**.

`SaveOptions` omvat instellingen die bepalen hoe het geredigeerde document wordt weggeschreven, inclusief formaat, rasterisatie en naamgevingsconventies.

#### Stap 3.1: saveoptions configureren

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Waarom:** Het aanpassen van opslaan‑opties biedt flexibele uitvoerformaten en naamgevingsconventies. Het inschakelen van `setAddSuffix(true)` **adds suffix to filename**, waardoor duidelijk wordt dat het bestand is geredigeerd.

## Hoe suffix bestandsnaam java toe te voegen bij het opslaan van een document?

`Redactor`‑klasse is het kernonderdeel dat een document laadt en redactiebewerkingen toepast. `SaveOptions` definieert hoe het geredigeerde document wordt opgeslagen, inclusief formaat, rasterisatie en naamgevingsconventies. Maak een `Redactor`‑instantie, pas eventuele benodigde redacties toe, en configureer vervolgens een `SaveOptions`‑object met `setAddSuffix(true)`. Roep `redactor.save(outputPath, options)` aan. De SDK voegt automatisch “_redacted” (of de geconfigureerde suffix) toe aan de bestandsnaam, zodat je het bestand nooit handmatig hoeft te hernoemen.

## Overzicht GroupDocs Maven‑afhankelijkheid

De **groupdocs maven dependency** brengt de volledige Redaction‑SDK in je project met één `<dependency>`‑vermelding. Het behandelt transitieve afhankelijkheden, houdt bibliotheken up‑to‑date en vereenvoudigt build‑automatisering. Door de afhankelijkheid in `pom.xml` te declareren, vermijd je handmatig JAR‑beheer en zorg je voor compatibiliteit met de nieuwste beveiligingspatches.

## Waarom het toevoegen van een suffix belangrijk is

Het toevoegen van een suffix biedt directe visuele bevestiging dat een bestand is verwerkt, wat cruciaal is voor audit‑trails, geautomatiseerde workflows en naleving van regelgeving. Het stelt scripts in staat geredigeerde bestanden te filteren, voorkomt onbedoelde distributie van originele inhoud, en voldoet aan vele industriestandaarden die duidelijke labeling van gesaniteerde documenten vereisen.

## Praktische toepassingen

1. **Legal document redaction:** Beveilig contracten voordat ze met klanten worden gedeeld.  
2. **Medical record handling:** Bescherm patiëntidentificatoren terwijl klinische gegevens behouden blijven.  
3. **Financial reporting:** Houd gevoelige cijfers vertrouwelijk tijdens externe audits.  
4. **CRM integration:** Redigeer automatisch klantgegevens vóór export naar derden.  
5. **Collaboration tools:** Zorg ervoor dat gedeelde concepten nooit verborgen opmerkingen of metadata blootleggen.

## Prestatie‑overwegingen

### Prestaties optimaliseren
- Gebruik streaming (`load document from stream`) om te voorkomen dat volledige bestanden in het geheugen worden geladen.  
- Sluit `Redactor`‑instanties tijdig om bronnen vrij te geven.  

### Richtlijnen voor resourcegebruik
- Houd CPU en geheugen in de gaten tijdens batch‑runs.  
- Geef de voorkeur aan `ByteArrayOutputStream` voor in‑memory opslagen bij bescheiden bestandsgroottes.

### Best practices voor Java‑geheugenbeheer
- Hergebruik `Redactor`‑objecten bij het verwerken van meerdere bestanden van hetzelfde type.  
- Roep `close()` aan in een `try‑with‑resources`‑blok om lekken te voorkomen.

## Veelvoorkomende problemen en oplossingen
| Probleem | Oorzaak | Oplossing |
|----------|---------|-----------|
| **Suffix not appearing** | `setAddSuffix(false)` of ontbrekende aanroep | Zorg ervoor dat `options.setAddSuffix(true)` is ingesteld vóór `save()`. |
| **OutOfMemoryError on large DOCX** | Het volledige bestand wordt in het geheugen geladen | Schakel over naar `InputStream`‑laden (zie Functie 1). |
| **Annotations still visible** | Redactie niet toegepast vóór opslaan | Roep `redactor.apply(new DeleteAnnotationRedaction())` aan vóór `save()`. |
| **PDF rasterization not applied** | `setRasterizeToPDF(false)` of weggelaten | Stel `options.setRasterizeToPDF(true)` in wanneer je een geflatte PDF nodig hebt. |

## Veelgestelde vragen

**V: Kan ik PDF‑documenten redigeren met GroupDocs.Redaction?**  
A: Ja, de bibliotheek ondersteunt PDF’s, DOCX, PPTX, XLSX en vele andere formaten.

**V: Wat is de beste manier om grote bestanden te verwerken met GroupDocs.Redaction?**  
A: Gebruik streaming (`load document from stream`) en sluit bronnen tijdig om het geheugenverbruik laag te houden.

**V: Is het mogelijk de suffix‑tekst aan te passen?**  
A: De API voegt standaard een suffix toe (bijv. “_redacted”). Voor aangepaste suffixen kun je het uitvoerbestand na het opslaan hernoemen.

**V: Hoe verkrijg ik een tijdelijke licentie voor GroupDocs.Redaction?**  
A: Bezoek de [Temporary License page](https://purchase.groupdocs.com/temporary-license/) en volg de instructies.

**V: Waar kan ik hulp krijgen als ik problemen ondervind?**  
A: Word lid van het [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) voor deskundige ondersteuning.

## Bronnen
- **Documentatie:** Bekijk gedetailleerde handleidingen op [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API‑referentie:** Toegang tot uitgebreide API‑details op [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Haal de nieuwste versie op van [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub‑repository:** Draag bij of bekijk de broncode op [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Laatst bijgewerkt:** 2026-11-02  
**Getest met:** GroupDocs.Redaction 24.9 voor Java  
**Auteur:** GroupDocs  

## Gerelateerde tutorials

- [Word naar PDF converteren en geredigeerde documenten opslaan met GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Documentpagina's previewen Java laden met GroupDocs.Redaction](/redaction/java/document-loading/)
- [Geavanceerde redactietechnieken voor GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)