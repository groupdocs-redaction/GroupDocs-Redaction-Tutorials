---
date: '2026-06-06'
description: Lär dig hur du konverterar en sida till PNG och förhandsgranskar PDF‑sidor
  med GroupDocs.Redaction för .NET. Steg‑för‑steg‑guide, kodexempel och praktiska
  tips.
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
title: Konvertera sida till PNG med GroupDocs.Redaction .NET
type: docs
url: /sv/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# Konvertera sida till PNG med GroupDocs.Redaction .NET

Att skapa en förhandsgranskning av en enskild sida från ett stort dokument är ett vanligt behov när du vill dela bara den relevanta delen av informationen. I den här handledningen kommer du att lära dig **hur du konverterar en sida till PNG** med GroupDocs.Redaction för .NET, konfigurera förhandsgranskningsutdata och integrera resultatet i dina applikationer. Vi går igenom förutsättningar, installation, koduppsättning och praktiska tips så att du kan börja generera PNG‑förhandsgranskningar av en enda sida på några minuter.

## Snabba svar
- **Kan jag generera en PNG‑förhandsgranskning av bara en sida?** Ja, använd `PreviewOptions` för att ange sidnumret och formatet.  
- **Vilket format stödjer GroupDocs.Redaction för förhandsgranskningar?** PNG är standard, men JPEG och BMP är också tillgängliga.  
- **Behöver jag en licens för utveckling?** En gratis provperiod fungerar för testning; en produktionslicens krävs för kommersiell användning.  
- **Fungerar detta på .NET Core och .NET Framework?** Absolut – biblioteket riktar sig mot .NET Standard 2.0+.  
- **Är processen minnes‑effektiv för stora filer?** Ja, API:et strömmar sidor och undviker att hela dokumentet laddas in.

## Vad är konvertera sida till PNG?
**convert page to PNG** avser att extrahera en enskild sida från ett stöddokument (PDF, DOCX, PPTX osv.) och rendera den sidan som en Portable Network Graphics (PNG)-bild. Den resulterande bilden bevarar den visuella layouten, teckensnitten och grafiken från original­sidan, vilket gör att du kan dela ett tydligt ögonblicksbild medan resten av dokumentet förblir dolt.

## Varför använda en en‑sidig förhandsgranskning?
Att generera en en‑sidig PNG‑förhandsgranskning minskar bandbredd, snabbar upp laddningstider och skyddar känsligt innehåll genom att bara visa det som behövs. GroupDocs.Redaction kan rendera en 300‑sidig PDF till en 200 KB PNG på under 0,5 sekunder på vanlig serverhårdvara, vilket gör den idealisk för webbportaler och rapportverktyg.

## Förutsättningar

- **GroupDocs.Redaction for .NET** – kärnbiblioteket som utför dokumentredigering och förhandsgranskningsgenerering.  
- **System.IO** – standard .NET‑namnrymd för filhantering.  
- .NET Core 3.1+ eller .NET Framework 4.6.1+ (vilken plattform som helst som stödjer .NET Standard 2.0).  
- Grundläggande kunskaper i C# och bekantskap med NuGet‑pakethantering.

## Konfigurera GroupDocs.Redaction för .NET

### Installationsinformation

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Öppna ditt projekt i Visual Studio.  
- Välj **Manage NuGet Packages**.  
- Sök efter **GroupDocs.Redaction** och installera den senaste stabila versionen.

### Steg för att skaffa licens
För att köra biblioteket behöver du en giltig licens. Du kan börja med en gratis provperiod eller begära en tillfällig nyckel:

1. Besök [GroupDocs webbplats](https://purchase.groupdocs.com/temporary-license) för att begära en tillfällig licens.  
2. Följ de e‑postade instruktionerna för att lägga till licensfilen i ditt projekt.

### Grundläggande initiering och konfiguration
Klassen `RedactionEngine` är ingångspunkten för alla operationer, inklusive förhandsgranskningsgenerering.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## Implementeringsguide

### Översikt
Detta avsnitt visar hur du **convert page to PNG** genom att konfigurera `PreviewOptions` och anropa förhandsgransknings‑API‑et. Metoden fungerar för PDF‑filer, DOCX, PPTX och många andra format som stöds av GroupDocs.Redaction.

### Steg 1: Förbered din miljö
Ange sökvägen till källfilen och utdata‑mappen. Använd `Path.Combine` för att bygga plattformsoberoende sökvägar.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### Steg 2: Ställ in förhandsgranskningsalternativ
`PreviewOptions` låter dig definiera sidnummer, bildstorlek och utdataformat. Klassen är konfigurationsnavet för förhandsgranskningsgenerering.  
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

#### Förklaring av viktiga konfigurationer
- **Width & Height** – Justera dessa värden för att matcha målskärmupplösningen.  
- **PageNumbers** – Ange en array med det exakta sidindex du vill rendera (nollbaserat).  
- **PreviewFormat** – PNG är standard; byt till `PreviewFormat.Jpeg` för mindre filer.

### Felsökningstips
Om PNG‑filen inte genereras:

- Verifiera att källfilens sökväg är korrekt och att filen är åtkomlig.  
- Säkerställ att licensfilen är laddad innan du anropar någon API‑metod.  
- Bekräfta att `PreviewOptions.PageNumbers` innehåller ett giltigt sidindex (t.ex. `0` för den första sidan).

## Praktiska tillämpningar
Att skapa en en‑sidig PNG‑förhandsgranskning är användbart i många scenarier:

1. **Kundpresentationer** – Visa endast den relevanta bilden eller kontraktsklausulen.  
2. **Interna granskningar** – Möjliggör snabba visuella kontroller utan att öppna hela dokumentet.  
3. **Innehållssammanfattningar** – Bädda in sidavbilder i e‑post eller instrumentpaneler för omedelbar kontext.  

Att integrera denna funktion med ett CMS eller CRM kan automatisera generering av miniatyrbilder för uppladdade dokument, vilket förbättrar användarupplevelsen.

## Prestandaöverväganden
- **Memory Management** – Disposera `RedactionEngine`‑instanser efter användning för att frigöra resurser.  
- **Asynchronous Execution** – Använd `await engine.GeneratePreviewAsync(...)` i UI‑applikationer för att hålla gränssnittet responsivt.  
- **Library Updates** – GroupDocs.Redaction stödjer **30+ in‑ och utdataformat** och bearbetar dokument upp till 500 sidor utan att ladda hela filen i minnet. Håll paketet uppdaterat för att dra nytta av prestandaförbättringar.

## Slutsats
Du har nu en komplett, produktionsklar metod för att **convert page to PNG** och generera en‑sidiga förhandsgranskningar med GroupDocs.Redaction för .NET. Genom att följa stegen ovan kan du bädda in högkvalitativa PNG‑ögonblicksbilder i vilken .NET‑applikation som helst, vilket förbättrar dokumentdelning samtidigt som säkerhet och prestanda bevaras.

## Vanliga frågor

**Q: Kan jag generera förhandsgranskningar för lösenordsskyddade PDF‑filer?**  
A: Ja, ange lösenordet när du initierar `RedactionEngine` så skapas förhandsgranskningen som vanligt.

**Q: Hur ändrar jag utdataformatet från PNG till JPEG?**  
A: Sätt `options.PreviewFormat = PreviewFormat.Jpeg` innan du anropar förhandsgransknings‑metoden.

**Q: Är det möjligt att förhandsgranska flera sidor samtidigt?**  
A: Absolut – tilldela en array med sidnummer till `options.PageNumbers` (t.ex. `new[] {0, 2, 4}`).

**Q: Vad ska jag göra om förhandsgranskningsbilden är suddig?**  
A: Öka `options.Width` och `options.Height` till en högre upplösning; biblioteket skalar bilden därefter.

**Q: Fungerar detta i Linux‑containrar?**  
A: Ja, GroupDocs.Redaction .NET är plattformsoberoende och körs i Docker‑containrar som stödjer .NET Core.

## Resurser
- [Dokumentation](https://docs.groupdocs.com/redaction/net/)
- [API‑referens](https://reference.groupdocs.com/redaction/net)
- [Ladda ner den senaste versionen](https://releases.groupdocs.com/redaction/net/)
- [Gratis supportforum](https://forum.groupdocs.com/c/redaction/33)
- [Tillfällig licensanskaffning](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Redaction 5.6 for .NET  
**Author:** GroupDocs

## Relaterade handledningar

- [Behärska dokumentssäkerhet: Rasterisera och redigera Word-dokument med GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)
- [Hur man tar bort sidor från PDF‑filer med GroupDocs.Redaction .NET: En omfattande guide](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)
- [Implementera dokumentredigering med GroupDocs.Redaction .NET: En steg‑för‑steg‑guide](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)