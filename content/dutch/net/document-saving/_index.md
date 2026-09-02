---
date: 2026-06-11
description: Leer hoe u redacted files kunt exporteren, output folders kunt configureren,
  rasterized PDFs kunt maken en streams kunt opslaan met GroupDocs.Redaction voor
  .NET.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: Hoe geredigeerde documenten exporteren met GroupDocs.Redaction .NET
type: docs
url: /nl/net/document-saving/
weight: 3
---

# Hoe Redacted Documenten Exporteren met GroupDocs.Redaction .NET

In deze uitgebreide gids ontdek je **hoe je redacted** inhoud veilig en efficiënt exporteert met GroupDocs.Redaction voor .NET. Of je nu het originele bestandstype wilt behouden, het document wilt vergrendelen als een rasterized PDF, of het resultaat direct in het geheugen wilt streamen, wij lopen elke optie met duidelijke, gesprekachtige uitleg en praktijkgerichte tips door. Aan het einde van deze tutorial kun je de juiste exportstrategie kiezen voor elk compliance‑gedreven scenario.

## Snelle Antwoorden
- **Welke formaten kan ik exporteren?** Een van de 30+ native formaten die door GroupDocs.Redaction worden ondersteund, plus rasterized PDF voor maximale beveiliging.  
- **Heb ik een licentie nodig voor streaming?** Ja, een geldige GroupDocs.Redaction-licentie is vereist voor productie‑streaming.  
- **Kan ik een aangepaste output‑map instellen?** Absoluut – gebruik de `OutputPath`‑eigenschap of `SaveOptions` om dit te configureren.  
- **Is rasterisatie veilig voor grote bestanden?** Het verwerkt documenten tot 500 pagina's zonder het volledige bestand in het geheugen te laden.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Wat is GroupDocs.Redaction?
GroupDocs.Redaction is een .NET‑bibliotheek die programmatisch gevoelige informatie verwijdert of maskeert uit PDF‑s, Word, Excel, PowerPoint, afbeeldingen en vele andere formaten. Het biedt een high‑level API voor het definiëren van redactieregio’s, het toepassen van beleidsregels en uiteindelijk het exporteren van het opgeschoonde document. Dit maakt het eenvoudig om redactiefuncties in elke .NET‑applicatie te integreren.

## Waarom Redacted Documenten Exporteren als Rasterized PDFs?
Rasterized PDFs zetten elke pagina om in een plat beeld, waardoor verborgen tekstlagen die later geëxtraheerd zouden kunnen worden, verdwijnen. Dit formaat garandeert dat geredigeerde inhoud niet kan worden hersteld, en voldoet aan strenge regelgeving zoals GDPR en HIPAA. GroupDocs.Redaction kan rasterized PDFs produceren tot 300 dpi, waardoor de visuele kwaliteit behouden blijft terwijl de beveiliging wordt gegarandeerd.

## Hoe Redacted Documenten Exporteren?
Laad het bronbestand, pas je redactieregels toe, en roep vervolgens de juiste opsla‑methode aan – of `Save` voor het originele formaat, `SaveAsRasterizedPdf` voor alleen‑beeld PDF‑s, of `SaveToStream` voor verwerking in het geheugen. Hieronder vind je de stap‑voor‑stap workflow. Elke methode zorgt ervoor dat de geredigeerde inhoud permanent wordt verwijderd terwijl het gewenste outputformaat behouden blijft.

### Stap 1: Installeer het NuGet‑pakket
Add the latest GroupDocs.Redaction package to your project:

```bash
dotnet add package GroupDocs.Redaction
```

### Stap 2: Laad het Document en Definieer Redacties
Create a `Redactor` instance, load the file, and specify the regions you want to hide. The `Redactor` class provides the core functionality for loading documents and applying redaction rules.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Stap 3: Kies de Exportmethode
#### Exporteren in Origineel Formaat
```csharp
redactor.Save("RedactedReport.docx");
```

#### Exporteren als Rasterized PDF
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Exporteren naar een Memory Stream (ideaal voor web‑API's)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

De `Save`‑methode schrijft het geredigeerde document naar een bestand in het originele formaat. `SaveAsRasterizedPdf` maakt een PDF waarbij elke pagina wordt gerenderd als een afbeelding, waardoor eventuele verborgen tekst wordt verwijderd. `SaveToStream` retourneert het geredigeerde bestand als een memory stream, geschikt voor web‑responses.

## Hoe een Output‑Map Configureren?
Set the `OutputPath` property on the `Redactor` or pass a custom `SaveOptions` object that includes the desired directory. `OutputPath` is a property of the `Redactor` that specifies the directory where output files are written. `SaveOptions` allows you to customize various saving parameters, including the output folder. This ensures all exported files land in a predictable location, simplifying batch processing pipelines. You can also specify subfolders per document type to keep your workspace organized.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Veelvoorkomende Problemen en Oplossingen
- **Redaction not applied:** Verify that the search pattern matches the document text exactly; use `RegexOptions.IgnoreCase` if needed. `RegexOptions` is an enumeration that controls regular expression matching behavior, such as case sensitivity.  
- **Large files cause memory pressure:** Enable streaming mode by using `SaveToStream` and avoid calling `Save` on the whole document.  
- **Rasterized PDF looks blurry:** Increase the DPI in `RasterizationOptions` (e.g., 300–600) to improve image quality. `RasterizationOptions` lets you set parameters like DPI and image format for rasterized PDF output.

## Veelgestelde Vragen

**Q: Kan ik exporteren naar een formaat dat oorspronkelijk niet werd ondersteund?**  
A: Ja, GroupDocs.Redaction kan de meeste invoertypen converteren naar PDF, DOCX, XLSX, PPTX of rasterized PDF, waardoor meer dan 30 formaten worden gedekt.

**Q: Hoe beschermt rasterisatie geredigeerde data?**  
A: Door elke pagina als een plat beeld te renderen, worden verborgen tekstlagen verwijderd, waardoor het onmogelijk is de originele inhoud te extraheren.

**Q: Is het mogelijk om meerdere redactieregels te combineren?**  
A: Absoluut – je kunt `Apply` herhaaldelijk aanroepen of een collectie van `RedactionOptions` doorgeven om veel patronen in één keer te verwerken. `RedactionOptions` defines the settings for a single redaction operation, such as region and replacement type.

**Q: Moet ik het Redactor‑object sluiten?**  
A: De `Redactor` implementeert `IDisposable`; wikkel het in een `using`‑block of roep `Dispose()` aan om bestands‑handles tijdig vrij te geven. `IDisposable` is an interface that provides a mechanism for releasing unmanaged resources.

**Q: Welke .NET‑runtimes zijn officieel getest?**  
A: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+, and .NET 5/6/7.

## Aanvullende Bronnen

### Beschikbare Tutorials

- [Hoe Documenten Opslaan als Rasterized PDFs met GroupDocs.Redaction voor .NET: Een Complete Gids](./groupdocs-redaction-net-rasterized-pdfs/)
- [Implementeren van Output‑Directory in .NET met GroupDocs.Redaction: Een Uitgebreide Gids](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Redact en Sla Documenten Op met GroupDocs.Redaction voor .NET: Een Complete Gids](./redact-save-documents-groupdocs-redaction-net/)
- [Sla Redacted Documenten Op in Origineel Formaat met GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Beveiligde Document Redaction in .NET met Streams: Een Gids voor GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Handige Links

- [GroupDocs.Redaction voor .NET Documentatie](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction voor .NET API‑Referentie](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction voor .NET](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Gratis Ondersteuning](https://forum.groupdocs.com/)
- [Tijdelijke Licentie](https://purchase.groupdocs.com/temporary-license/)

---

**Laatst Bijgewerkt:** 2026-06-11  
**Getest Met:** GroupDocs.Redaction 23.11 voor .NET  
**Auteur:** GroupDocs  

---

## Gerelateerde Tutorials

- [Sla Redacted Documenten Op in Origineel Formaat met GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Hoe Documenten Opslaan als Rasterized PDFs met GroupDocs.Redaction voor .NET: Een Complete Gids](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Beveiligde Document Redaction in .NET met Streams: Een Gids voor GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)