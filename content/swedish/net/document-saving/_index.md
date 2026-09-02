---
date: 2026-06-11
description: Lär dig hur du exporterar redacted files, configure output folders, create
  rasterized PDFs, and save to streams med GroupDocs.Redaction for .NET.
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
title: Hur man exporterar redacted documents med GroupDocs.Redaction .NET
type: docs
url: /sv/net/document-saving/
weight: 3
---

# Hur man exporterar redigerade dokument med GroupDocs.Redaction .NET

I den här omfattande guiden kommer du att upptäcka **hur man exporterar redigerat** innehåll på ett säkert och effektivt sätt med GroupDocs.Redaction för .NET. Oavsett om du behöver behålla originalfilens typ, låsa dokumentet som en rasteriserad PDF, eller strömma resultatet direkt i minnet, guidar vi dig genom alla alternativ med tydliga, samtalstonade förklaringar och praktiska tips. I slutet av den här tutorialen kommer du att kunna välja rätt exportstrategi för alla efterlevnadsdrivna scenarier.

## Snabba svar
- **Vilka format kan jag exportera till?** Vilket som helst av de 30+ inbyggda formaten som stöds av GroupDocs.Redaction, plus rasteriserad PDF för maximal säkerhet.  
- **Behöver jag en licens för streaming?** Ja, en giltig GroupDocs.Redaction-licens krävs för produktionsstreaming.  
- **Kan jag ange en anpassad utmatningsmapp?** Absolut – använd `OutputPath`-egenskapen eller `SaveOptions` för att konfigurera den.  
- **Är rasterisering säker för stora filer?** Den hanterar dokument upp till 500 sidor utan att ladda hela filen i minnet.  
- **Vilka .NET-versioner stöds?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Vad är GroupDocs.Redaction?
GroupDocs.Redaction är ett .NET‑bibliotek som programatiskt tar bort eller maskerar känslig information från PDF‑filer, Word, Excel, PowerPoint, bilder och många andra format. Det erbjuder ett hög‑nivå API för att definiera redigeringsområden, tillämpa policyer och slutligen exportera det rensade dokumentet. Detta gör det enkelt att integrera redigeringsfunktioner i vilken .NET‑applikation som helst.

## Varför exportera redigerade dokument som rasteriserade PDF‑filer?
Rasteriserade PDF‑filer konverterar varje sida till en platt bild, vilket eliminerar dolda textlager som senare kan extraheras. Detta format garanterar att redigerat innehåll inte kan återställas, och uppfyller strikta regulatoriska standarder som GDPR och HIPAA. GroupDocs.Redaction kan producera rasteriserade PDF‑filer upp till 300 dpi, vilket bevarar den visuella kvaliteten samtidigt som säkerheten säkerställs.

## Hur man exporterar redigerade dokument?
Läs in källfilen, tillämpa dina redigeringsregler och anropa sedan den lämpliga sparmetoden — antingen `Save` för originalformat, `SaveAsRasterizedPdf` för PDF‑filer som endast innehåller bilder, eller `SaveToStream` för hantering i minnet. Nedan följer steg‑för‑steg‑arbetsflödet. Varje metod säkerställer att det redigerade innehållet tas bort permanent samtidigt som önskat utmatningsformat bevaras.

### Steg 1: Installera NuGet‑paketet
Add the latest GroupDocs.Redaction package to your project:

```bash
dotnet add package GroupDocs.Redaction
```

### Steg 2: Läs in dokumentet och definiera redigeringar
Skapa en `Redactor`‑instans, läs in filen och ange de områden du vill dölja. `Redactor`‑klassen tillhandahåller kärnfunktionaliteten för att läsa in dokument och tillämpa redigeringsregler.

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

### Steg 3: Välj exportmetod
#### Exportera i originalformat
```csharp
redactor.Save("RedactedReport.docx");
```

#### Exportera som rasteriserad PDF
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Exportera till ett minnesström (idealiskt för webb‑API:er)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

`Save`‑metoden skriver det redigerade dokumentet till en fil i dess originalformat. `SaveAsRasterizedPdf` skapar en PDF där varje sida renderas som en bild, vilket tar bort eventuella dolda texter. `SaveToStream` returnerar den redigerade filen som ett minnesström, lämplig för webb‑svar.

## Hur man konfigurerar en utmatningsmapp?
Ställ in `OutputPath`‑egenskapen på `Redactor` eller skicka ett anpassat `SaveOptions`‑objekt som inkluderar den önskade katalogen. `OutputPath` är en egenskap i `Redactor` som specificerar den katalog där utdatafiler skrivs. `SaveOptions` låter dig anpassa olika sparparametrar, inklusive utmatningsmappen. Detta säkerställer att alla exporterade filer hamnar på en förutsägbar plats, vilket förenklar batch‑behandlingspipelines. Du kan också ange undermappar per dokumenttyp för att hålla ditt arbetsutrymme organiserat.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Vanliga problem och lösningar
- **Redigering inte tillämpad:** Verifiera att sökmönstret exakt matchar dokumenttexten; använd `RegexOptions.IgnoreCase` om det behövs. `RegexOptions` är en uppräkning som styr beteendet för reguljära uttryck, såsom skiftlägeskänslighet.  
- **Stora filer orsakar minnespress:** Aktivera streaming‑läge genom att använda `SaveToStream` och undvik att anropa `Save` på hela dokumentet.  
- **Rasteriserad PDF ser suddig ut:** Öka DPI i `RasterizationOptions` (t.ex. 300–600) för att förbättra bildkvaliteten. `RasterizationOptions` låter dig ställa in parametrar som DPI och bildformat för rasteriserad PDF‑utmatning.

## Vanliga frågor

**Q: Kan jag exportera till ett format som inte ursprungligen stöddes?**  
A: Ja, GroupDocs.Redaction kan konvertera de flesta inmatningstyper till PDF, DOCX, XLSX, PPTX eller rasteriserad PDF, vilket täcker över 30 format.

**Q: Hur skyddar rasterisering redigerad data?**  
A: Genom att rendera varje sida som en platt bild tas alla dolda textlager bort, vilket gör det omöjligt att extrahera det ursprungliga innehållet.

**Q: Är det möjligt att kedja flera redigeringsregler?**  
A: Absolut – du kan anropa `Apply` upprepade gånger eller skicka en samling av `RedactionOptions` för att bearbeta många mönster i ett pass. `RedactionOptions` definierar inställningarna för en enskild redigeringsoperation, såsom område och ersättningstyp.

**Q: Behöver jag stänga Redactor‑objektet?**  
A: `Redactor` implementerar `IDisposable`; omslut det i ett `using`‑block eller anropa `Dispose()` för att snabbt frigöra filhandtag. `IDisposable` är ett gränssnitt som tillhandahåller en mekanism för att frigöra ohanterade resurser.

**Q: Vilka .NET‑körningar har officiellt testats?**  
A: GroupDocs.Redaction har validerats på .NET Framework 4.6+, .NET Core 3.1+ och .NET 5/6/7.

## Ytterligare resurser

### Tillgängliga handledningar
- [Hur man sparar dokument som rasteriserade PDF‑filer med GroupDocs.Redaction för .NET: En komplett guide](./groupdocs-redaction-net-rasterized-pdfs/)
- [Implementering av utmatningskatalog i .NET med GroupDocs.Redaction: En omfattande guide](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Redigera och spara dokument med GroupDocs.Redaction för .NET: En komplett guide](./redact-save-documents-groupdocs-redaction-net/)
- [Spara redigerade dokument i originalformat med GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Säker dokumentredigering i .NET med Strömmar: En guide för GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Användbara länkar
- [GroupDocs.Redaction för .NET-dokumentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction för .NET API‑referens](https://reference.groupdocs.com/redaction/net/)
- [Ladda ner GroupDocs.Redaction för .NET](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction‑forum](https://forum.groupdocs.com/c/redaction/33)
- [Gratis support](https://forum.groupdocs.com/)
- [Tillfällig licens](https://purchase.groupdocs.com/temporary-license/)

**Senast uppdaterad:** 2026-06-11  
**Testad med:** GroupDocs.Redaction 23.11 for .NET  
**Författare:** GroupDocs  

## Relaterade handledningar
- [Spara redigerade dokument i originalformat med GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Hur man sparar dokument som rasteriserade PDF‑filer med GroupDocs.Redaction för .NET: En komplett guide](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Säker dokumentredigering i .NET med Strömmar: En guide för GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)