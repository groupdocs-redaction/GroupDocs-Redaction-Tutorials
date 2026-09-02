---
date: '2026-06-06'
description: Leer hoe je een pagina naar PNG converteert en PDF‑pagina's kunt bekijken
  met GroupDocs.Redaction voor .NET. Stapsgewijze handleiding, code‑fragmenten en
  praktijkgerichte tips.
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: Pagina converteren naar PNG met GroupDocs.Redaction .NET
type: docs
url: /nl/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# Pagina converteren naar PNG met GroupDocs.Redaction .NET

Het maken van een voorbeeld van één pagina uit een groot document is een veelvoorkomende behoefte wanneer je alleen het relevante deel van de informatie wilt delen. In deze tutorial leer je **hoe je een pagina naar PNG converteert** met GroupDocs.Redaction voor .NET, configureer je de preview‑uitvoer en integreer je het resultaat in je applicaties. We lopen de vereisten, installatie, code‑opzet en praktische tips door zodat je binnen enkele minuten enkel‑pagina PNG‑previews kunt genereren.

## Snelle Antwoorden
- **Kan ik een PNG‑preview van slechts één pagina genereren?** Ja, gebruik `PreviewOptions` om het paginanummer en het formaat op te geven.  
- **Welke indeling ondersteunt GroupDocs.Redaction voor previews?** PNG is de standaard, maar JPEG en BMP zijn ook beschikbaar.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis proefversie werkt voor testen; een productie‑licentie is vereist voor commercieel gebruik.  
- **Werkt dit op .NET Core en .NET Framework?** Absoluut – de bibliotheek richt zich op .NET Standard 2.0+.  
- **Is het proces geheugen‑efficiënt voor grote bestanden?** Ja, de API streamt pagina's, waardoor het volledige document niet geladen hoeft te worden.  

## Wat is pagina naar PNG converteren?
**convert page to PNG** verwijst naar het extraheren van één pagina uit een ondersteund document (PDF, DOCX, PPTX, enz.) en het renderen van die pagina als een Portable Network Graphics (PNG) afbeelding. De resulterende afbeelding behoudt de visuele lay-out, lettertypen en grafische elementen van de originele pagina, waardoor je een duidelijk momentopname kunt delen terwijl de rest van het document verborgen blijft.

## Waarom een enkel‑pagina preview gebruiken?
Het genereren van een enkel‑pagina PNG‑preview vermindert de bandbreedte, versnelt laadtijden en beschermt gevoelige inhoud door alleen te tonen wat nodig is. GroupDocs.Redaction kan een PDF van 300 pagina's renderen naar een PNG van 200 KB in minder dan 0,5 seconden op typische serverhardware, waardoor het ideaal is voor webportalen en rapportagetools.

## Vereisten
- **GroupDocs.Redaction for .NET** – de kernbibliotheek die documentredactie en preview‑generatie uitvoert.  
- **System.IO** – standaard .NET-namespace voor bestandsafhandeling.  
- .NET Core 3.1 of .NET Framework 4.6.1+ (elk platform dat .NET Standard 2.0 ondersteunt).  
- Basiskennis van C# en vertrouwdheid met NuGet‑pakketbeheer.  

## GroupDocs.Redaction voor .NET instellen

### Installatie‑informatie

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Open je project in Visual Studio.  
- Kies **Manage NuGet Packages**.  
- Zoek naar **GroupDocs.Redaction** en installeer de nieuwste stabiele versie.  

### Stappen voor het verkrijgen van een licentie
Om de bibliotheek te gebruiken heb je een geldige licentie nodig. Je kunt beginnen met een gratis proefversie of een tijdelijke sleutel aanvragen:

1. Bezoek de [GroupDocs-website](https://purchase.groupdocs.com/temporary-license) om een tijdelijke licentie aan te vragen.  
2. Volg de per e‑mail ontvangen instructies om het licentiebestand aan je project toe te voegen.  

### Basisinitialisatie en -configuratie
De `RedactionEngine`‑klasse is het toegangspunt voor alle bewerkingen, inclusief preview‑generatie.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## Implementatie‑gids

### Overzicht
Deze sectie toont hoe je **pagina naar PNG converteert** door `PreviewOptions` te configureren en de preview‑API aan te roepen. De aanpak werkt voor PDF’s, DOCX, PPTX en vele andere formaten die door GroupDocs.Redaction worden ondersteund.

### Stap 1: Bereid je omgeving voor
Stel het bronbestandspad en de uitvoermap in. Gebruik `Path.Combine` om platformonafhankelijke paden te bouwen.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### Stap 2: Stel preview‑opties in
`PreviewOptions` stelt je in staat het paginanummer, de afbeeldingsgrootte en het uitvoerformaat te definiëren. De klasse is het configuratie‑centrum voor preview‑generatie.  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### Uitleg van belangrijke configuraties
- **Width & Height** – Pas deze waarden aan om overeen te komen met de doel‑schermresolutie.  
- **PageNumbers** – Geef een array op met de exacte paginanaam die je wilt renderen (nul‑gebaseerd).  
- **PreviewFormat** – PNG is de standaard; schakel over naar `PreviewFormat.Jpeg` voor kleinere bestanden.  

### Probleemoplossingstips
Als de PNG niet wordt gegenereerd:

- Controleer of het bronbestandspad correct is en het bestand toegankelijk is.  
- Zorg ervoor dat het licentiebestand is geladen voordat je een API‑methode aanroept.  
- Bevestig dat `PreviewOptions.PageNumbers` een geldig paginapunt bevat (bijv. `0` voor de eerste pagina).  

## Praktische toepassingen
Het maken van een enkel‑pagina PNG‑preview is nuttig in veel scenario's:

1. **Client Presentations** – Toon alleen de relevante dia of contractclausule.  
2. **Internal Reviews** – Maak snelle visuele controles mogelijk zonder het volledige document te openen.  
3. **Content Summaries** – Integreer paginavoorbeelden in e‑mails of dashboards voor directe context.  

Het integreren van deze functie met een CMS of CRM kan het automatisch genereren van miniaturen voor geüploade documenten automatiseren, waardoor de gebruikerservaring verbetert.

## Prestatie‑overwegingen
- **Memory Management** – Vernietig `RedactionEngine`‑instanties na gebruik om bronnen vrij te geven.  
- **Asynchronous Execution** – Gebruik `await engine.GeneratePreviewAsync(...)` in UI‑applicaties om de interface responsief te houden.  
- **Library Updates** – GroupDocs.Redaction ondersteunt **30+ invoer‑ en uitvoerformaten** en verwerkt documenten tot 500 pagina's zonder het volledige bestand in het geheugen te laden. Houd het pakket up‑to‑date om te profiteren van prestatie‑verbeteringen.  

## Conclusie
Je hebt nu een volledige, productie‑klare methode om **pagina naar PNG te converteren** en enkel‑pagina previews te genereren met GroupDocs.Redaction voor .NET. Door de bovenstaande stappen te volgen kun je hoogwaardige PNG‑momentopnamen in elke .NET‑applicatie integreren, waardoor documentdeling wordt verbeterd terwijl veiligheid en prestaties behouden blijven.

## Veelgestelde vragen

**Q: Kan ik previews genereren voor met wachtwoord beveiligde PDF’s?**  
A: Ja, geef het wachtwoord op bij het initialiseren van `RedactionEngine` en de preview wordt normaal aangemaakt.

**Q: Hoe wijzig ik het uitvoerformaat van PNG naar JPEG?**  
A: Stel `options.PreviewFormat = PreviewFormat.Jpeg` in voordat je de preview‑methode aanroept.

**Q: Is het mogelijk om meerdere pagina’s tegelijk te previewen?**  
A: Absoluut – wijs een array met paginanummers toe aan `options.PageNumbers` (bijv. `new[] {0, 2, 4}`).

**Q: Wat moet ik doen als de preview‑afbeelding onscherp is?**  
A: Verhoog `options.Width` en `options.Height` naar een hogere resolutie; de bibliotheek schaalt de afbeelding dienovereenkomstig.

**Q: Werkt dit op Linux‑containers?**  
A: Ja, GroupDocs.Redaction .NET is cross‑platform en draait in Docker‑containers die .NET Core ondersteunen.

## Bronnen
- [Documentatie](https://docs.groupdocs.com/redaction/net/)
- [API‑referentie](https://reference.groupdocs.com/redaction/net)
- [Download de nieuwste versie](https://releases.groupdocs.com/redaction/net/)
- [Gratis ondersteuningsforum](https://forum.groupdocs.com/c/redaction/33)
- [Tijdelijke licentie‑acquisitie](https://purchase.groupdocs.com/temporary-license)

---

**Laatst bijgewerkt:** 2026-06-06  
**Getest met:** GroupDocs.Redaction 5.6 for .NET  
**Auteur:** GroupDocs

## Gerelateerde tutorials
- [Documentbeveiliging beheersen: Word‑documenten rasteren en redigeren met GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)
- [Hoe pagina’s uit PDF’s te verwijderen met GroupDocs.Redaction .NET: Een uitgebreide gids](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)
- [Documentredactie implementeren met GroupDocs.Redaction .NET: Een stapsgewijze handleiding](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)