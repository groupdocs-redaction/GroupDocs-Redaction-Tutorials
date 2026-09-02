---
date: '2026-06-11'
description: Leer hoe u metadata uit documentstreams kunt extraheren met GroupDocs.Redaction
  voor .NET, inclusief installatie, codevoorbeelden en praktische toepassingen.
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: Hoe metadata uit documentstreams te extraheren met GroupDocs.Redaction .NET
type: docs
url: /nl/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# Hoe metadata uit documentstreams te extraheren met GroupDocs.Redaction .NET

Bent u het beu om handmatig documentinformatie te extraheren of te werken met grote bestanden die uw workflow vertragen? **Hoe metadata te extraheren** is een veelvoorkomende uitdaging, en de GroupDocs.Redaction‑bibliotheek voor .NET biedt een snelle, geheugen‑efficiënte manier om documentdetails rechtstreeks uit streams op te halen. In deze tutorial leert u hoe u de bibliotheek instelt, bestandstype, paginacount en grootte uit een stream haalt, en een uitvoermap voorbereidt voor verdere verwerking.

## Snelle antwoorden
- **Wat betekent “metadata extraheren”?** Het betekent het lezen van eigenschappen zoals bestandstype, paginacount en grootte zonder het volledige document in het geheugen te openen.  
- **Welke bibliotheek behandelt dit?** GroupDocs.Redaction voor .NET biedt een native API voor stream‑gebaseerde metadata‑extractie.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie is vereist voor productie.  
- **Kan ik PDF's groter dan 1 GB verwerken?** Ja – streams laten u bestanden tot 2 GB verwerken zonder het hele bestand te laden.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ en .NET 6+.

## Wat is metadata‑extractie uit streams?
Metadata‑extractie uit streams is het proces waarbij documenteigenschappen direct uit een `Stream`‑object worden gelezen, waardoor volledig laden van het bestand wordt vermeden en geheugen en CPU‑tijd worden bespaard. Deze techniek is ideaal voor batchverwerking of cloud‑gebaseerde services waar middelen beperkt zijn.

## Waarom GroupDocs.Redaction gebruiken voor metadata‑extractie?
GroupDocs.Redaction ondersteunt **30+ bestandsformaten** (inclusief PDF, DOCX, XLSX, PPTX en afbeeldingsformaten) en kan documenten tot **2 GB** verwerken terwijl het geheugenverbruik onder **50 MB** blijft. De `Redactor`‑API biedt één enkele oproep om alle belangrijke documentinformatie op te halen, waardoor meerdere parsers overbodig worden.

## Vereisten

- **GroupDocs.Redaction voor .NET** (nieuwste versie)  
- **.NET Framework** 4.5+ **of** **.NET Core/5+/6+**  
- Basiskennis van C# en vertrouwdheid met bestands‑I/O  
- Visual Studio 2019 of hoger

## Hoe stel ik GroupDocs.Redaction voor .NET in?
Om te beginnen met het gebruik van GroupDocs.Redaction moet u eerst de bibliotheek aan uw project toevoegen. Dit kan via de .NET CLI, de Visual Studio Package Manager of de NuGet‑UI. Kies de aanpak die bij uw workflow past; de CLI is ideaal voor scriptbare builds, terwijl de UI een grafische manier biedt om versies en afhankelijkheden te bekijken.

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**
- Open NuGet Package Manager in Visual Studio.  
- Zoek naar **"GroupDocs.Redaction"** en installeer de nieuwste versie.

### Stappen voor licentie‑acquisitie
1. **Gratis proefversie:** Download een proeflicentie om alle functies zonder beperkingen te verkennen.  
2. **Tijdelijke licentie:** Vraag een tijdelijke licentie aan via [GroupDocs](https://purchase.groupdocs.com/temporary-license/) voor uitgebreid testen.  
3. **Aankoop:** Wanneer u klaar bent voor productie, koop een commerciële licentie.  

Voor meer informatie, bezoek de [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).

### Basisinitialisatie en configuratie
De `Redactor`‑klasse is het toegangspunt voor alle bewerkingen, inclusief metadata‑extractie.

`Redactor` is de kernklasse die een document‑instantie vertegenwoordigt en methoden biedt voor redactie, informatie‑ophaling en bestandsmanipulatie. Na installatie kunt u een `Redactor`‑object maken zoals hieronder weergegeven:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

Nu de bibliotheek klaar is, duiken we in de implementatiedetails.

## Hoe metadata uit een documentstream te extraheren?
Laad het document als een **alleen‑lezen stream**, initialiseert de `Redactor` en roep `GetDocumentInfo()` aan om de metadata in één stap op te halen. Deze aanpak voorkomt het laden van het volledige bestand in het geheugen, wat cruciaal is voor grote PDF's of Office‑documenten met honderden pagina's.

**Direct antwoord:** Open het bestand met `File.OpenRead()`, geef de stream door aan `new Redactor(stream)`, en roep vervolgens `redactor.GetDocumentInfo()` aan – de methode retourneert een object met bestandstype, paginacount en grootte in slechts drie regels code.

### Stap 1: Bereid het bronbestandspad voor
Zorg eerst dat het bronbestand bestaat en dat de uitvoermap klaar is. De onderstaande hulpfunctie controleert de uitvoermap en maakt deze indien nodig aan.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*Waarom?* Dit garandeert een geldig pad voor volgende bestandsbewerkingen en voorkomt `DirectoryNotFoundException`.

### Stap 2: Open de documentstream
Het gebruik van `File.OpenRead()` opent het bestand als een **alleen‑lezen stream**, waardoor het geheugenverbruik laag blijft, zelfs voor bestanden van gigabyte‑grootte.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*Waarom?* Streams maken on‑the‑fly verwerking mogelijk, waardoor u met delen van het bestand kunt werken in plaats van het volledige document.

### Stap 3: Initialiseert de Redactor met de documentstream
`Redactor` is het primaire API‑object dat u toegang geeft tot document‑niveau bewerkingen, inclusief metadata‑extractie.

`Redactor` vertegenwoordigt een enkel document geladen vanuit een stream en biedt methoden zoals `GetDocumentInfo()` voor snelle eigenschap‑ophaling.

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*Waarom?* Het instantieren van `Redactor` met een stream koppelt het object aan het onderliggende bestand zonder het volledig te laden.

### Stap 4: Haal documentmetadata op
Het aanroepen van `GetDocumentInfo()` retourneert een `DocumentInfo`‑object dat het bestandsformaat, paginacount en bestandsgrootte bevat.

`GetDocumentInfo()` extraheert kern‑eigenschappen (formaat, paginacount, grootte) in één oproep, waardoor aparte parsers overbodig worden.

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*Waarom?* Deze stap consolideert alle essentiële metadata, waardoor het eenvoudig is om documenten te loggen, filteren of routeren op basis van hun kenmerken.

## Hoe een uitvoermap voor verwerkte bestanden voor te bereiden?
Voordat u verwerkte bestanden schrijft, moet u ervoor zorgen dat de doelmap bestaat en schrijfbaar is. Door het pad programmatisch te controleren en aan te maken wanneer het ontbreekt, voorkomt u veelvoorkomende runtime‑exceptions zoals `DirectoryNotFoundException` of machtigingsfouten. Deze eenvoudige stap maakt uw code bovendien draagbaar over verschillende omgevingen, of u nu lokaal, op een server of binnen een container draait.

**Direct antwoord:** Gebruik `Directory.Exists()` om de map te controleren en `Directory.CreateDirectory()` om deze aan te maken als deze niet bestaat – deze één‑regelige controle garandeert een geldig pad vóór elke schrijf‑bewerking.

### Implementeer een hulpmethode
De onderstaande methode omvat de controle‑en‑aanmaak‑logica en retourneert het geverifieerde pad voor later gebruik.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*Waarom?* Het centraliseren van deze logica vermindert duplicatie en maakt de codebasis makkelijker te onderhouden.

## Veelvoorkomende problemen en oplossingen
- **Machtigingsfouten:** Zorg ervoor dat de applicatie draait onder een account met schrijfrechten op de doelmap.  
- **Ongeldige paden:** Controleer de pad‑scheidingstekens (`\\` op Windows, `/` op Linux/macOS) om `DirectoryNotFoundException` te voorkomen.  
- **Grote bestanden verwerken:** Maak streams direct vrij (`using`‑statements) om OS‑handles vrij te geven en lekken te voorkomen.

## Praktische toepassingen
1. **Geautomatiseerde documentinname:** Extraheer metadata bij uploaden en sla deze vervolgens op in een database voor snelle zoekopdrachten en compliance‑rapportage.  
2. **Juridische & compliance‑audits:** Haal paginacounts en bestandstypen op om te verifiëren dat documenten voldoen aan regelgeving vóór archivering.  
3. **Enterprise content management:** Gebruik metadata om bestanden automatisch in mappen te categoriseren, waardoor organisatie en ophaalsnelheid verbeteren.

## Prestatie‑overwegingen
- **Geheugenbeheer:** Wikkel streams altijd in `using`‑blokken zodat ze automatisch worden vrijgegeven.  
- **Batchverwerking:** Verwerk documenten in groepen van 10‑20 om doorvoersnelheid en geheugenverbruik in balans te houden, vooral op servers met beperkte middelen.  
- **Parallelisme:** Maak gebruik van `Parallel.ForEach` voor onafhankelijke bestanden, maar houd CPU en I/O in de gaten om conflicten te voorkomen.

## Conclusie
U heeft nu een volledige, productie‑klare gids over **hoe metadata te extraheren** uit documentstreams met GroupDocs.Redaction voor .NET. Door de bovenstaande stappen te volgen, kunt u efficiënt bestandstype, paginacount en grootte ophalen terwijl u het geheugenverbruik laag houdt en grote bestanden soepel verwerkt.

**Volgende stappen**
- Bekijk de volledige API‑referentie in de [documentatie](https://docs.groupdocs.com/redaction/net/).  
- Duik dieper in de [GroupDocs Redaction .NET Documentatie](https://docs.groupdocs.com/redaction/net/) om redactie, watermerken en OCR‑functies te verkennen.  
- Experimenteer met verschillende bestandsformaten (PDF, DOCX, XLSX) om te zien hoe metadata varieert per type.  
- Integreer de geëxtraheerde metadata in uw bestaande document‑beheer‑ of zoekoplossing.

## Veelgestelde vragen

**V: Wat is de primaire use‑case voor metadata‑extractie van GroupDocs.Redaction?**  
A: Het maakt snelle, geheugen‑efficiënte ophalen van documenteigenschappen mogelijk voor indexering, compliance‑controles en geautomatiseerde routering zonder het volledige bestand te openen.

**V: Kan ik metadata extraheren uit met wachtwoord beveiligde bestanden?**  
A: Ja, geef het wachtwoord op bij het construeren van het `Redactor`‑object; de API zal de stream intern ontsleutelen.

**V: Ondersteunt de bibliotheek niet‑PDF‑formaten zoals DOCX of XLSX?**  
A: Absoluut – GroupDocs.Redaction ondersteunt meer dan 30 formaten, inclusief PDF, DOCX, XLSX, PPTX en gangbare afbeeldingsformaten.

**V: Hoe groot een document kan ik verwerken met streams?**  
A: Streams maken verwerking van bestanden tot **2 GB** mogelijk terwijl het geheugenverbruik onder **50 MB** blijft, dankzij on‑the‑fly lezen.

**V: Waar kan ik hulp krijgen als ik problemen ondervind?**  
A: Bezoek het [GroupDocs‑forum](https://forum.groupdocs.com/c/redaction/33) voor community‑ondersteuning, of raadpleeg de officiële documentatie voor tips bij het oplossen van problemen.

---

**Laatst bijgewerkt:** 2026-06-11  
**Getest met:** GroupDocs.Redaction 23.12 voor .NET  
**Auteur:** GroupDocs  

**Bronnen**  
- **Documentatie:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API‑referentie:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Download:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## Gerelateerde tutorials

- [Beheers documentmetadata‑ophaling met GroupDocs.Redaction .NET API](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)  
- [Hoe documentmetadata te redigeren met GroupDocs.Redaction voor .NET – Een uitgebreide gids](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)  
- [Beveiligde documentredactie in .NET met streams: Een gids voor GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)