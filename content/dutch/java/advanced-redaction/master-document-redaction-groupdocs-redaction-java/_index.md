---
date: '2026-05-22'
description: Leer hoe je een suffix aan de bestandsnaam java toevoegt met de GroupDocs
  Maven dependency tijdens het redigeren van documenten. Inclusief streaming load,
  annotation deletion en save options.
keywords:
- add suffix filename java
- groupdocs redaction java
- document redaction workflow
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  headline: Add suffix filename java with GroupDocs Maven
  type: TechArticle
- description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  name: Add suffix filename java with GroupDocs Maven
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
title: Voeg suffix toe aan bestandsnaam java met GroupDocs Maven
type: docs
url: /nl/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Voeg suffix toe aan bestandsnaam java met GroupDocs Maven

Het redigeren van vertrouwelijke gegevens is slechts de helft van de strijd—je moet er ook voor zorgen dat het opgeslagen bestand duidelijk aangeeft dat het is verwerkt. **Het gebruik van de GroupDocs Maven‑dependency maakt dit eenvoudig**, waardoor je in slechts een paar regels code een suffix kunt toevoegen aan de bestandsnaam van de uitvoer. De methode om **add suffix filename java** toe te passen is een één‑regelige configuratie die je geredigeerde bestanden onmiddellijk labelt, waardoor je compliant en audit‑klaar blijft.

## Snelle Antwoorden
- **Wat doet “add suffix to filename”?**  
  Het voegt een aangepaste suffix (bijv. “_redacted”) toe aan de bestandsnaam van de uitvoer zodat je onmiddellijk verwerkte bestanden kunt identificeren.  
- **Kan ik een document laden vanuit een stream?**  
  Ja—GroupDocs.Redaction ondersteunt het laden vanuit elke `InputStream`, perfect voor cloudopslag of in‑memory verwerking.  
- **Heb ik een licentie nodig voor deze functie?**  
  Een gratis proefversie werkt voor basisredactie; een tijdelijke of volledige licentie ontgrendelt alle geavanceerde opties, inclusief suffix‑verwerking.  
- **Welke formaten worden ondersteund?**  
  De bibliotheek ondersteunt DOCX, PDF, PPTX, XLSX en nog veel meer.  
- **Is rasterisatie vereist voor PDF-uitvoer?**  
  Rasterisatie is optioneel; schakel het in wanneer je het document moet flatten voor extra beveiliging.

## Wat is add suffix filename java?
De **add suffix filename java**‑techniek voegt een vooraf gedefinieerde tekenreeks toe aan de bestandsnaam tijdens de opslaan‑bewerking, waardoor het document duidelijk als geredigeerd wordt gemarkeerd. Deze eenvoudige conventie voorkomt per ongeluk verspreiden van originele, onge‑redigeerde bestanden en integreert soepel met geautomatiseerde pipelines.

## Waarom GroupDocs.Redaction voor deze taak gebruiken?
GroupDocs.Redaction biedt een vloeiende Java‑API waarmee je redactie‑acties kunt combineren met bestands‑beheeropties—zoals **add suffix filename java**—in slechts een paar regels code. De SDK ondersteunt **50+ invoer‑ en uitvoerformaten** en kan documenten van honderden pagina's verwerken zonder het volledige bestand in het geheugen te laden, waardoor zowel snelheid als een lage geheugengebruik worden geleverd.

## Vereisten

- **Java Development Kit (JDK):** Versie 8 of hoger.  
- **GroupDocs.Redaction Library:** Kernbibliotheek voor redactie‑taken.  
- **IDE:** IntelliJ IDEA, Eclipse, of een andere Java‑compatibele editor.  
- **Maven:** Voor afhankelijkheidsbeheer.  

### Kennisvereisten
Bekendheid met Java I/O en basisobject‑georiënteerde concepten maakt de voorbeelden makkelijker te volgen.

## GroupDocs.Redaction voor Java instellen
### Maven‑configuratie
Voeg de volgende configuratie toe aan je `pom.xml`‑bestand om via Maven toegang te krijgen tot de GroupDocs‑bibliotheken:

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
Of download de nieuwste versie direct van [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Licentie‑acquisitie
1. **Gratis proefversie:** Toegang tot basisfunctionaliteit zonder beperkingen.  
2. **Tijdelijke licentie:** Verkrijg een tijdelijke licentie om geavanceerde functies te verkennen.  
3. **Aankoop:** Overweeg voor langdurig gebruik een volledige licentie aan te schaffen.

#### Basisinitialisatie en -configuratie
Initialiseer je project door de benodigde imports toe te voegen:

```java
import com.groupdocs.redaction.Redactor;
```

Met deze configuratie ben je klaar om document‑redactiefunctionaliteiten te implementeren.

## Implementatie‑gids

### Functie 1: Document laden vanuit stream
**Overzicht:** Leer hoe je documenten in een `InputStream` laadt voor verwerking.

#### Stapsgewijze implementatie
##### Stap 1.1: InputStream maken

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

- **Waarom:** Het gebruik van `InputStream` stelt je in staat documenten te verwerken die op verschillende locaties zijn opgeslagen—cloud‑buckets, databases of in‑memory buffers—zonder ze eerst naar schijf te schrijven. Deze aanpak is essentieel wanneer je **load document from stream** moet gebruiken in micro‑service‑architecturen.

### Functie 2: Toepassen van annotatie‑verwijderings‑redactie
**Overzicht:** Verwijder annotaties uit je document met behulp van de `DeleteAnnotationRedaction`.

#### Stapsgewijze implementatie
##### Stap 2.1: DeleteAnnotationRedaction toepassen

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Waarom:** Deze stap zorgt ervoor dat alle gevoelige annotaties (commentaren, markeringen of verborgen notities) uit het document worden verwijderd, waardoor privacy en naleving worden verbeterd.

### Functie 3: Document opslaan met opties
**Overzicht:** Leer hoe je je verwerkte document opslaat met specifieke opties zoals rasterisatie en **add suffix filename java**.

#### Stapsgewijze implementatie
##### Stap 3.1: SaveOptions configureren

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

- **Waarom:** Het aanpassen van opslaan‑opties biedt flexibele uitvoerformaten en naamgevingsconventies. Het inschakelen van `setAddSuffix(true)` **voegt suffix toe aan bestandsnaam**, waardoor duidelijk is dat het bestand is geredigeerd.

## Hoe add suffix filename java toe te voegen bij het opslaan van een document?
`Redactor` is de hoofdklasse in GroupDocs.Redaction die een document laadt en redactie‑bewerkingen toepast.  
`setAddSuffix` is een methode van `SaveOptions` die automatische toevoeging van een suffix aan de bestandsnaam van de uitvoer mogelijk maakt.

Laad je `Redactor`‑instantie, pas de gewenste redacties toe, en roep vervolgens `save()` aan met `SaveOptions` waarin `setAddSuffix(true)` is ingeschakeld. Deze één‑regelige configuratie voegt automatisch “_redacted” (of de standaard suffix) toe aan de bestandsnaam, waardoor handmatig hernoemen wordt geëlimineerd en menselijke fouten worden verminderd. De bewerking voltooit in O(n) tijd ten opzichte van de documentgrootte en werkt voor alle ondersteunde formaten.

## Overzicht van groupdocs maven dependency
De **groupdocs maven dependency** brengt de volledige Redaction‑SDK in je project met een enkele `<dependency>`‑vermelding. Het behandelt transitieve afhankelijkheden, houdt bibliotheken up‑to‑date en vereenvoudigt build‑automatisering. Door de afhankelijkheid in `pom.xml` te declareren, vermijd je handmatig JAR‑beheer en zorg je voor compatibiliteit met de nieuwste beveiligingspatches.

## Waarom het toevoegen van een suffix belangrijk is
Het toevoegen van een suffix biedt directe visuele bevestiging dat een document is verwerkt, wat essentieel is voor audit‑trails, geautomatiseerde workflows en regelgeving‑naleving in diverse sectoren.

- **Auditbaarheid:** Teams kunnen onmiddellijk zien welke bestanden veilig te distribueren zijn.  
- **Automatisering:** Scripts kunnen bestanden filteren op suffix, waardoor per ongeluk verwerken van originele documenten wordt voorkomen.  
- **Naleving:** Veel regelgeving vereist duidelijke labeling van gesaniteerde documenten.  

## Praktische toepassingen
Bekijk deze praktijkvoorbeelden:

1. **Juridische documentredactie:** Beveilig contracten vóór delen met klanten.  
2. **Medische dossierverwerking:** Bescherm patiëntidentificatoren terwijl klinische gegevens behouden blijven.  
3. **Financiële rapportage:** Houd gevoelige cijfers vertrouwelijk tijdens externe audits.  
4. **CRM‑integratie:** Redigeer automatisch klantgegevens vóór export naar tools van derden.  
5. **Samenwerkingstools:** Zorg ervoor dat gedeelde concepten nooit verborgen commentaren of metadata blootleggen.  

## Prestatie‑overwegingen
### Prestaties optimaliseren
- Gebruik streaming (`load document from stream`) om te voorkomen dat volledige bestanden in het geheugen worden geladen.  
- Sluit `Redactor`‑instanties direct om bronnen vrij te geven.  

### Richtlijnen voor resourcegebruik
- Monitor CPU en geheugen tijdens batch‑runs.  
- Geef de voorkeur aan `ByteArrayOutputStream` voor in‑memory opslagen bij bescheiden bestandsgroottes.  

### Best practices voor Java‑geheugenbeheer
- Hergebruik `Redactor`‑objecten bij het verwerken van meerdere bestanden van hetzelfde type.  
- Roep `close()` aan in een `try‑with‑resources`‑blok om lekken te voorkomen.  

## Veelvoorkomende problemen en oplossingen
| Issue | Cause | Fix |
|-------|-------|-----|
| **Suffix niet zichtbaar** | `setAddSuffix(false)` of ontbrekende aanroep | Zorg ervoor dat `options.setAddSuffix(true)` is ingesteld vóór `save()`. |
| **OutOfMemoryError bij grote DOCX** | Het volledige bestand in het geheugen laden | Schakel over naar `InputStream`‑laden (zie Functie 1). |
| **Annotaties nog zichtbaar** | Redactie niet toegepast vóór opslaan | Roep `redactor.apply(new DeleteAnnotationRedaction())` aan vóór `save()`. |
| **PDF‑rasterisatie niet toegepast** | `setRasterizeToPDF(false)` of weggelaten | Stel `options.setRasterizeToPDF(true)` in wanneer je een geflatte PDF nodig hebt. |

## Veelgestelde vragen

**V: Kan ik PDF‑documenten redigeren met GroupDocs.Redaction?**  
A: Ja, de bibliotheek ondersteunt PDF's, DOCX, PPTX, XLSX en vele andere formaten.

**V: Wat is de beste manier om grote bestanden te verwerken met GroupDocs.Redaction?**  
A: Gebruik streaming (`load document from stream`) en sluit bronnen direct om het geheugengebruik laag te houden.

**V: Is het mogelijk de suffix‑tekst aan te passen?**  
A: De API voegt automatisch een standaard suffix toe (bijv. “_redacted”). Voor aangepaste suffixen, hernoem het uitvoerbestand na het opslaan.

**V: Hoe verkrijg ik een tijdelijke licentie voor GroupDocs.Redaction?**  
A: Bezoek de [Temporary License page](https://purchase.groupdocs.com/temporary-license/) en volg de instructies.

**V: Waar kan ik hulp krijgen als ik problemen ondervind?**  
A: Word lid van het [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) voor deskundige hulp.

## Bronnen
- **Documentatie:** Bekijk gedetailleerde handleidingen op [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API‑referentie:** Toegang tot uitgebreide API‑details op [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Haal de nieuwste versie op van [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub‑repository:** Draag bij of bekijk de broncode op [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Laatst bijgewerkt:** 2026-05-22  
**Getest met:** GroupDocs.Redaction 24.9 voor Java  
**Auteur:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Gerelateerde tutorials

- [Word naar PDF converteren en geredigeerde documenten opslaan met GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Documentpagina's previewen Java laden met GroupDocs.Redaction](/redaction/java/document-loading/)
- [Geavanceerde redactietechnieken voor GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)