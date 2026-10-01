---
date: '2026-10-01'
description: Leer hoe je author metadata kunt verwijderen en redacted document files
  kunt opslaan in Java met GroupDocs Redaction.
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Leer hoe je author metadata kunt verwijderen en redacted document
  files kunt opslaan in Java met GroupDocs Redaction. Volg de step‑by‑step guide.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: Hoe author metadata te verwijderen in Java met GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: Hoe author metadata te verwijderen in Java met GroupDocs
type: docs
url: /nl/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Hoe auteurmetadata te verwijderen in Java met GroupDocs

In het digitale landschap van vandaag is het beschermen van gevoelige informatie die in documenten verborgen zit een onmisbare praktijk. **Het verwijderen van auteurmetadata** voorkomt accidentele openbaarmaking van persoonlijke of bedrijfsidentificatoren. Deze tutorial laat je stap voor stap zien hoe je `EraseMetadataRedaction` van GroupDocs.Redaction voor Java kunt gebruiken om velden zoals *Author* en *Manager* uit Word‑bestanden te verwijderen, en vervolgens **geredigeerde document**‑kopieën veilig kunt opslaan voor delen of archiveren.

## Snelle antwoorden
- **Wat doet EraseMetadataRedaction?** Het verwijdert geselecteerde metadata‑velden uit een document.  
- **Welke bibliotheek biedt deze functie?** GroupDocs.Redaction voor Java.  
- **Heb ik een licentie nodig?** Een gratis trial werkt voor testen; een permanente licentie is vereist voor productie.  
- **Kan ik meerdere velden tegelijk targeten?** Ja, combineer filters met een logische OR.  
- **Is het proces thread‑safe?** Redactor‑instances worden niet gedeeld tussen threads; maak een nieuwe instance per bewerking.

## Wat is EraseMetadataRedaction?
`EraseMetadataRedaction` is een ingebouwde redactieklasse die je laat specificeren welke metadata‑items moeten worden gewist. Het werkt op een breed scala aan documentformaten die door GroupDocs.Redaction worden ondersteund, waardoor verborgen auteurinformatie nooit lekt. Je kunt standaardeigenschappen zoals Author, Manager, en ook aangepaste metadata‑velden targeten, wat uitgebreide privacybescherming biedt.

## Waarom EraseMetadataRedaction gebruiken met GroupDocs?
GroupDocs.Redaction ondersteunt **meer dan 100 invoer‑ en uitvoerformaten** en kan documenten tot 500 pagina's verwerken zonder het volledige bestand in het geheugen te laden. Het gebruik van deze klasse biedt je een enkele, high‑performance API om te voldoen aan GDPR-, HIPAA- of interne compliance‑vereisten, terwijl je codebasis eenvoudig blijft.

## Voorvereisten
- Java 8 of hoger geïnstalleerd.  
- Maven (of de mogelijkheid om JAR‑bestanden handmatig toe te voegen).  
- GroupDocs.Redaction voor Java (versie 24.9 of later).  
- Een geldige GroupDocs‑trial of permanente licentie.

## GroupDocs.Redaction voor Java configureren

### Maven‑installatie
Add the GroupDocs repository and dependency to your **pom.xml**:

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
Alternatively, download the latest JAR from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Licentie‑acquisitie
Verkrijg een gratis trial of koop een tijdelijke licentie via het GroupDocs‑portaal. Het licentiebestand moet worden geplaatst op een locatie waar je applicatie het kan laden (bijv. de classpath‑root).

### Basisinitialisatie en configuratie
Below is a minimal example that creates a `Redactor` instance for a DOCX file:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Hoe EraseMetadataRedaction te gebruiken in Java
De volgende secties splitsen de implementatie op in duidelijke, uitvoerbare stappen.

### Functie: specifieke metadata‑items opschonen

#### Overzicht
We zullen de **Author**- en **Manager**‑metadata‑velden wissen met `EraseMetadataRedaction`. Dit is een veelvoorkomende eis bij het delen van interne rapporten met externe partners.

#### Stapsgewijze implementatie

##### 1️⃣ Initialiseer het Redactor‑object
`Redactor` is the core class that loads a document, applies redaction objects, and writes the result. Create a new instance for each file you process:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ Pas EraseMetadataRedaction toe
`MetadataFilters` provides predefined filters for common metadata keys such as Author and Manager.  
`EraseMetadataRedaction` removes metadata entries that match the supplied `MetadataFilters`. The bitwise OR (`|`) combines the `Author` and `Manager` filters so both fields are removed in one call:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ Configureer opslaan‑opties
`SaveOptions` lets you specify the output file name, format, and other saving parameters.  
`SaveOptions` lets you control the output file name, format, and whether the document should be rasterized to PDF. Adding a suffix keeps the original file untouched:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## Veelvoorkomende gebruikssituaties
1. **Juridische documenten** – Redigeer auteurinformatie voordat contracten naar de tegenpartij worden gestuurd.  
2. **Bedrijfsrapporten** – Verwijder manager‑namen bij het publiceren van kwartaalresultaten aan aandeelhouders.  
3. **Projectbestanden** – Maak interne projectdocumentatie schoon voordat deze wordt gearchiveerd of geüpload naar een openbare repository.

## Probleemoplossingstips
- **Bestand niet gevonden** – Controleer of het pad in `inputFilePath` naar een bestaand bestand wijst en of de applicatie leesrechten heeft.  
- **Ontbrekende metadata‑velden** – Niet alle documenttypen slaan dezelfde metadata‑sleutels op; controleer eerst de eigenschappen van het document in Office.  
- **Licentiefouten** – Zorg ervoor dat het licentiebestand correct is geladen voordat je de `Redactor`‑instance maakt.

## Prestatieoverwegingen
- Sluit het `Redactor`‑object direct (zoals getoond in de `finally`‑block) om native bronnen vrij te geven.  
- Vermijd het rasteren van grote documenten tenzij je een PDF‑preview nodig hebt; rasteren kan het CPU‑ en geheugenverbruik tot wel 3× verhogen voor bestanden van 300 pagina's.

## Veelgestelde vragen

**Q1: Wat is metadata‑redactie?**  
A1: Metadata‑redactie omvat het verwijderen van verborgen documenteigenschappen (zoals auteur, manager of aangepaste tags) om accidentele openbaarmaking van gevoelige informatie te voorkomen.

**Q2: Kan ik GroupDocs.Redaction voor andere bestandstypen gebruiken?**  
A2: Ja, de bibliotheek ondersteunt PDF, DOCX, PPTX, XLSX en nog veel meer formaten — meer dan 100 in totaal.

**Q3: Hoe ga ik om met fouten tijdens redactie?**  
A3: Plaats de `apply`‑aanroep in een try‑catch‑blok en sluit altijd de `Redactor` in een finally‑clausule om ervoor te zorgen dat bronnen worden vrijgegeven.

**Q4: Is het mogelijk om aangepaste metadata‑velden te redigeren?**  
A5: Absoluut. Gebruik `MetadataFilters.Custom("YourFieldName")` om elke aangepaste eigenschap die in het document is opgeslagen te targeten.

**Q5: Wat zijn best practices voor het gebruik van GroupDocs.Redaction?**  
A5:  
- Laad de licentie vroeg in je applicatie.  
- Sluit `Redactor`‑objecten direct.  
- Gebruik `SaveOptions` om een suffix toe te voegen, zodat originele bestanden onaangeroerd blijven.  
- Test redactie op een kopie van het document voordat je batches verwerkt.

**Q6: Ondersteunt EraseMetadataRedaction batch‑operaties?**  
A6: Je kunt over een collectie bestandspaden itereren, voor elk bestand een nieuwe `Redactor` maken en dezelfde redactielogica toepassen.

**Q7: Kan ik EraseMetadataRedaction combineren met andere redactietypen?**  
A7: Ja, je kunt meerdere redactie‑objecten ketenen (bijv. tekstredactie gevolgd door metadata‑redactie) vóór het opslaan.

## Bronnen

- **Documentatie**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API‑referentie**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Gratis ondersteuning**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Tijdelijke licentie**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Laatst bijgewerkt:** 2026-10-01  
**Getest met:** GroupDocs.Redaction 24.9 for Java  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Groupdocs Redaction Java Document Metadata Extractie](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [Hoe metadata te verwijderen in Java met GroupDocs.Redaction](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [Documentinformatie ophalen met Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)