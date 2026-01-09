---
date: '2025-12-17'
description: Leer hoe u een achtervoegsel aan bestandsnamen kunt toevoegen en gevoelige
  informatie uit documenten kunt redigeren met GroupDocs.Redaction voor Java. Verhoog
  de documentbeveiliging en privacy effectief.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Hoe een achtervoegsel aan een bestandsnaam toevoegen tijdens het redigeren
  van documenten in Java met GroupDocs.Redaction
type: docs
url: /nl/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Hoe een suffix aan bestandsnaam toevoegen tijdens het redigeren van documenten in Java met GroupDocs.Redaction

Het redigeren van vertrouwelijke gegevens is slechts de helft van de strijd—je moet er ook voor zorgen dat het opgeslagen bestand duidelijk aangeeft dat het is verwerkt. In deze gids leer je **hoe je een suffix aan de bestandsnaam toevoegt** bij het opslaan van een geredigeerd document, naast het laden, annoteren en opslaan met GroupDocs.Redaction voor Java. Of je nu juridische contracten, medische dossiers of financiële rapporten beschermt, deze stappen houden je workflow zowel veilig als controleerbaar.

## Snelle antwoorden
- **Wat doet “add suffix to filename”?**  
  Het voegt een aangepaste suffix (bijv. “_redacted”) toe aan de uitvoerbestandsnaam zodat je direct verwerkte bestanden kunt identificeren.  
- **Kan ik een document laden vanuit een stream?**  
  Ja—GroupDocs.Redaction ondersteunt het laden vanuit elke `InputStream`, perfect voor cloudopslag of in‑memory verwerking.  
- **Heb ik een licentie nodig voor deze functie?**  
  Een gratis proefversie werkt voor basisredactie; een tijdelijke of volledige licentie ontgrendelt alle geavanceerde opties, inclusief suffix‑afhandeling.  
- **Welke formaten worden ondersteund?**  
  De bibliotheek ondersteunt DOCX, PDF, PPTX, XLSX en nog veel meer.  
- **Is rasterisatie vereist voor PDF-uitvoer?**  
  Rasterisatie is optioneel; schakel het in wanneer je het document moet flatten voor extra beveiliging.  

## Wat is het toevoegen van een suffix aan een bestandsnaam?
Het toevoegen van een suffix is een eenvoudige naamgevingsconventie die aangeeft dat een bestand is geredigeerd. Het voorkomt per ongeluk delen van originele, niet-geredigeerde versies en helpt geautomatiseerde pipelines de verwerkingsstatus bij te houden.

## Waarom GroupDocs.Redaction voor deze taak gebruiken?
GroupDocs.Redaction biedt een vloeiende Java‑API waarmee je redactie‑acties kunt combineren met bestands‑behandelingsopties—zoals **het toevoegen van een suffix aan de bestandsnaam**—in slechts een paar regels code. Dit bespaart ontwikkeltijd en vermindert het op handmatige fouten.

## Voorvereisten
- **Java Development Kit (JDK):** Versie 8 of hoger.  
- **GroupDocs.Redaction Library:** Kernbibliotheek voor redactie‑taken.  
- **IDE:** IntelliJ IDEA, Eclipse, of elke Java‑compatibele editor.  
- **Maven:** Voor afhankelijkheidsbeheer.  

### Kennisvoorvereisten
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
Of download de nieuwste versie direct van [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Licentie‑acquisitie
1. **Free Trial:** Toegang tot basisfunctionaliteit zonder beperkingen.  
2. **Temporary License:** Verkrijg een tijdelijke licentie om geavanceerde functies te verkennen.  
3. **Purchase:** Voor langdurig gebruik, overweeg het aanschaffen van een volledige licentie.  

#### Basisinitialisatie en -configuratie
Initialiseer je project door de benodigde imports toe te voegen:

```java
import com.groupdocs.redaction.Redactor;
```

Met deze configuratie ben je klaar om document‑redactiefunctionaliteit te implementeren.

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

- **Waarom:** Het gebruik van `InputStream` stelt je in staat documenten die in verschillende formaten zijn opgeslagen naadloos te verwerken, wat essentieel is wanneer je een **document moet laden vanuit een stream** in cloud‑ of micro‑service scenario's.

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

- **Waarom:** Deze stap zorgt ervoor dat gevoelige annotaties worden verwijderd, waardoor de privacy van het document wordt verbeterd.

### Functie 3: Document opslaan met opties
**Overzicht:** Leer hoe je je verwerkte document opslaat met specifieke opties zoals rasterisatie en **het toevoegen van een suffix aan de bestandsnaam**.

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

- **Waarom:** Het aanpassen van save‑options biedt flexibele uitvoerformaten en naamgevingsconventies. Het inschakelen van `setAddSuffix(true)` **voegt een suffix toe aan de bestandsnaam**, waardoor duidelijk wordt dat het bestand is geredigeerd.

## Waarom het toevoegen van een suffix belangrijk is
- **Auditbaarheid:** Teams kunnen direct zien welke bestanden veilig zijn om te distribueren.  
- **Automatisering:** Scripts kunnen bestanden filteren op suffix, waardoor per ongeluk verwerken van originele documenten wordt voorkomen.  
- **Naleving:** Veel regelgeving vereist duidelijke labeling van gesaniteerde documenten.

## Praktische toepassingen
Bekijk deze praktijkvoorbeelden:
1. **Legal Document Redaction:** Beveilig contracten vóór het delen met klanten.  
2. **Medical Record Handling:** Bescherm patiëntidentificatoren.  
3. **Financial Reporting:** Houd gevoelige cijfers vertrouwelijk.  
4. **CRM Integration:** Redigeer automatisch klantgegevens vóór export.  
5. **Collaboration Tools:** Zorg ervoor dat gedeelde concepten nooit verborgen opmerkingen blootleggen.

## Prestatie‑overwegingen
### Prestaties optimaliseren
- Gebruik streaming (`load document from stream`) om te voorkomen dat volledige bestanden in het geheugen worden geladen.  
- Sluit `Redactor`‑instanties direct om bronnen vrij te geven.

### Richtlijnen voor resourcegebruik
- Houd CPU en geheugen in de gaten tijdens batch‑runs.  
- Geef de voorkeur aan `ByteArrayOutputStream` voor in‑memory opslagen bij bescheiden bestandsgroottes### Best practices voor Java‑geheugenbeheer
- Hergebruik `Redactor`‑objecten bij het verwerken van meerdere bestanden van hetzelfde type.  
- Roep `close()` aan in een `finally`‑blok of try‑with‑resources om lekken te voorkomen.

## Veelvoorkomende problemen en oplossingen
| Probleem | Oorzaak | Oplossing |
|----------|---------|-----------|
| **Suffix verschijnt niet** | `setAddSuffix(false)` of ontbrekende aanroep | Zorg ervoor dat `options.setAddSuffix(true)` is ingesteld vóór `save()`. |
| **OutOfMemoryError bij grote DOCX** | Het volledige bestand in het geheugen laden | Schakel over naar laden via `InputStream` (zie Functie 1). |
| **Annotaties nog zichtbaar** | Redactie niet toegepast vóór opslaan | Roep `redactor.apply(new DeleteAnnotationRedaction())` aan vóór `save()`. |
| **PDF‑rasterisatie niet toegepast** | `setRasterizeToPDF(false)` of weggelaten | Stel `options.setRasterizeToPDF(true)` in wanneer je een geflatte PDF nodig hebt. |

## Veelgestelde vragen

**Q: Kan ik PDF‑documenten redigeren met GroupDocs.Redaction?**  
A: Ja, de bibliotheek ondersteunt PDF’s, DOCX, PPTX, XLSX en vele andere formaten.

**Q: Wat is de beste manier om grote bestanden te verwerken met GroupDocs.Redaction?**  
A: Gebruik streaming (`load document from stream`) en sluit bronnen direct om het geheugengebruik laag te houden.

**Q: Is het mogelijk om de suffix‑tekst aan te passen?**  
A: De API voegt automatisch een standaard suffix toe (bijv. “_redacted”). Voor aangepaste suffixen kun je het uitvoerbestand na het opslaan hernoemen.

**Q: Hoe verkrijg ik een tijdelijke licentie voor GroupDocs.Redaction?**  
A: Bezoek de [Temporary License page](https://purchase.groupdocs.com/temporary-license/) en volg de instructies.

**Q: Waar kan ik hulp krijgen als ik problemen ondervind?**  
A: Word lid van het [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) voor deskundige ondersteuning.

## Resources
- **Documentatie:** Bekijk gedetailleerde handleidingen op [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API‑referentie:** Toegang tot uitgebreide API‑details op [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Haal de nieuwste versie op van [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub‑repository:** Draag bij of verken de broncode op [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Laatst bijgewerkt:** 2025-12-17  
**Getest met:** GroupDocs.Redaction 24.9 for Java  
**Auteur:** GroupDocs