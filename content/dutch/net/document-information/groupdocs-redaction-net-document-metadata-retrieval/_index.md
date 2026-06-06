---
date: '2026-06-06'
description: Leer hoe u metadata kunt ophalen en documentmetadata kunt extraheren
  met GroupDocs.Redaction .NET, waardoor robuust documentbeheer en compliance mogelijk
  worden.
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: Hoe metadata ophalen met de GroupDocs.Redaction .NET API
type: docs
url: /nl/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# Hoe metadata op te halen met GroupDocs.Redaction .NET

In de huidige digitale tijd is **hoe metadata op te halen** uit een bestand een fundamentele stap voor elke document‑gerichte applicatie. Of u nu bestandsmetadata moet lezen voor compliance‑audits, documenteigenschappen moet extraheren voor indexering, of gewoon de documentgrootte in een UI wilt weergeven, GroupDocs.Redaction .NET biedt een beknopte API om dit te doen in slechts een paar regels C#. Deze tutorial leidt u door het volledige proces, van het opzetten van de omgeving tot het weergeven van de opgehaalde informatie, zodat u direct documentmetadata kunt extraheren.

## Snelle antwoorden
- **Wat is de primaire methode om metadata op te halen?** Roep `Redactor.GetDocumentInfo()` aan op een `Redactor`-instance.  
- **Welke formaten worden ondersteund?** Meer dan 50 invoer- en uitvoerformaten, waaronder PDF, DOCX, XLSX, PPTX en afbeeldingsformaten.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis proeflicentie werkt voor testen; een volledige licentie is vereist voor productie.  
- **Kan ik grote bestanden verwerken?** Ja—GroupDocs.Redaction verwerkt documenten van meerdere honderden pagina's zonder het volledige bestand in het geheugen te laden.  
- **Is async-ondersteuning beschikbaar?** De API kan worden gewikkeld in async‑patronen om UI‑threads responsief te houden.

## Wat is metadata‑ophaling in GroupDocs.Redaction?
Metadata‑ophaling is het proces van het benaderen van de ingebouwde eigenschappen van een document—zoals bestandstype, paginatelling en grootte—via de API van de bibliotheek. Door deze eigenschappen te extraheren, kunnen ontwikkelaars programmatisch documentkenmerken beoordelen, indexering ondersteunen, nalevingsregels afdwingen en weloverwogen beslissingen nemen over verdere verwerkingsstappen.

## Hoe documentmetadata op te halen?
De `Redactor`‑klasse is de primaire interface voor het laden en inspecteren van documenten in GroupDocs.Redaction.  
`GetDocumentInfo()` is een methode die een `DocumentInfo`‑object retourneert met de metadata van het document.  

Laad uw bestand met `new Redactor("path/to/file")` en roep `GetDocumentInfo()` aan—de oproep retourneert een `DocumentInfo`‑object met type, paginatelling, grootte en andere eigenschappen. Deze twee‑stappen‑aanpak werkt voor elk ondersteund formaat en vereist geen extra configuratie. U kunt vervolgens velden zoals `FileType`, `PageCount` en `FileSize` lezen om de informatie weer te geven of te loggen.

## Vereisten

- **GroupDocs.Redaction .NET** versie 21.6 of nieuwer.  
- .NET Framework 4.7.2 +, .NET Core 3.1 +, of .NET 5/6+.  
- Basiskennis van C# en een ontwikkel‑IDE (Visual Studio, Rider, enz.).

## GroupDocs.Redaction voor .NET instellen

Aan de slag met GroupDocs.Redaction is eenvoudig. Installeer het pakket met een van de volgende methoden:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

Of gebruik de **NuGet Package Manager UI**: Zoek eenvoudig naar “GroupDocs.Redaction” en klik op **Install**.

### Licentie‑acquisitie

Om GroupDocs.Redaction uit te proberen, kunt u een gratis proeflicentie verkrijgen. Voor voortdurende ontwikkeling of productiegebruik koopt u een volledige licentie of vraagt u een tijdelijke licentie aan via de officiële site.

Zodra geïnstalleerd, initialiseert u de bibliotheek als volgt:

```csharp
using GroupDocs.Redaction;
```

## Implementatie‑gids

### Functie Documentinformatie ophalen

Deze functie richt zich op het extraheren van essentiële metadata uit documenten met GroupDocs.Redaction .NET. Volg deze stappen:

#### Stap 1: Bereid uw documentpad voor

Definieer het absolute of relatieve pad naar het doelbestand:

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

Vervang `YOUR_DOCUMENT_DIRECTORY` door de map die uw document bevat.

#### Stap 2: Initialiseer Redactor‑instance

Maak een `Redactor`‑object dat toegang biedt tot metadata‑methoden:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### Stap 3: Documentinformatie ophalen

Roep `GetDocumentInfo()` aan op de `Redactor`‑instance om alle beschikbare eigenschappen op te halen:

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

Het geretourneerde object bevat bestandstype, aantal pagina's en bestandsgrootte.

#### Stap 4: Documentdetails weergeven

Geef de informatie weer in de console of UI. De voorbeeldcode (gecommentarieerd voor zelfstandige uitvoering) laat zien hoe elke eigenschap kan worden afgedrukt:

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### Waarom GroupDocs.Redaction gebruiken voor metadata‑extractie?
GroupDocs.Redaction ondersteunt **50+ bestandsformaten** en kan documenten tot **2 GB** verwerken terwijl het geheugenverbruik onder **100 MB** blijft voor typische workloads. De bibliotheek extraheert metadata zonder het document volledig te laden, waardoor snelle reacties worden geleverd—vaak onder **200 ms** voor een 100‑pagina‑PDF op standaard serverhardware.

### Veelvoorkomende problemen en oplossingen

- **Onjuist bestandspad** – Controleer de pad‑string en zorg ervoor dat het bestand toegankelijk is voor het draaiende proces.  
- **Niet‑ondersteund formaat** – Controleer de lijst met formaten; als een formaat ontbreekt, overweeg het eerst te converteren.  
- **Prestatieknelpunten** – Voor zeer grote bestanden, schakel streaming‑opties in of verwerk pagina's in batches om het geheugenverbruik te beperken.

## Praktische toepassingen

Het begrijpen van de metadata van een document maakt verschillende real‑world scenario's mogelijk:

1. **Document Management Systems (DMS)** – Automatiseer categorisatie en indexering op basis van type, grootte of paginatelling.  
2. **Compliance‑auditing** – Verifieer dat vertrouwelijke bestanden de vereiste metadata bevatten vóór archivering.  
3. **Data‑migratie** – Groepeer bestanden op basis van eigenschappen om bulk‑migratietaken te stroomlijnen.

## Prestatie‑overwegingen

- **Efficiënt gebruik van bronnen** – Gebruik de `Redactor`‑instance binnen een `using`‑blok om correcte vrijgave te garanderen.  
- **Asynchrone patronen** – Wikkel metadata‑aanroepen in `Task.Run` of implementeer async‑wrappers om UI‑threads responsief te houden in desktop‑ of web‑apps.

## Veelgestelde vragen

**Q: Welke documentformaten kan ik metadata uit extraheren?**  
A: GroupDocs.Redaction leest metadata uit meer dan 50 formaten, waaronder PDF, DOCX, XLSX, PPTX, HTML en gangbare afbeeldingsformaten.

**Q: Hoe ga ik om met wachtwoord‑beveiligde bestanden?**  
A: Geef het wachtwoord door aan de `Redactor`‑constructor; de API zal het bestand ontsleutelen voordat de metadata wordt geëxtraheerd.

**Q: Is er een limiet aan de grootte van bestanden die ik kan verwerken?**  
A: Hoewel er geen harde limiet is, kunnen bestanden groter dan 2 GB extra geheugenafstemming vereisen; de prestaties blijven lineair met de bestandsgrootte.

**Q: Kan ik metadata in een batch‑operatie ophalen?**  
A: Ja—itereer over een collectie pad‑strings en roep `GetDocumentInfo()` voor elk aan; de bibliotheek is thread‑safe voor parallelle uitvoering.

**Q: Heb ik een licentie nodig voor ontwikkel‑builds?**  
A: Een gratis proeflicentie is voldoende voor ontwikkeling en testen; een commerciële licentie is vereist voor productie‑implementaties.

## Bronnen

- [Documentation](https://docs.groupdocs.com/redaction/net/)  
- [API Reference](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)

## Conclusie

U heeft nu een volledige, stap‑voor‑stap gids over **hoe metadata op te halen** met GroupDocs.Redaction .NET. Door gebruik te maken van de `Redactor.GetDocumentInfo()`‑methode kunt u snel bestandsmetadata lezen, compliance‑workflows ondersteunen en elke documentverwerkings‑pipeline verbeteren. Verken aanvullende Redaction‑functies—zoals inhoudsredactie, watermerken en documentconversie—om een volledig uitgeruste documentmanagementoplossing te bouwen.

---

**Last Updated:** 2026-06-06  
**Getest met:** GroupDocs.Redaction .NET 21.6 (latest at time of writing)  
**Auteur:** GroupDocs  

---

## Gerelateerde tutorials

- [How to Extract Document Metadata from Streams Using GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [How to Redact Document Metadata Using GroupDocs.Redaction for .NET - A Comprehensive Guide](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Document Loading Tutorials with GroupDocs.Redaction for .NET](/redaction/net/document-loading/)