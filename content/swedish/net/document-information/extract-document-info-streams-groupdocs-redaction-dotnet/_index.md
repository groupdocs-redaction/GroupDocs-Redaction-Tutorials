---
date: '2026-06-11'
description: Lär dig hur du extraherar metadata från dokumentströmmar med GroupDocs.Redaction
  för .NET, inklusive installation, kodexempel och praktiska tillämpningar.
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
title: Hur man extraherar metadata från dokumentströmmar med GroupDocs.Redaction .NET
type: docs
url: /sv/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# Hur man extraherar metadata från dokumentströmmar med GroupDocs.Redaction .NET

Är du trött på att manuellt extrahera dokumentinformation eller hantera stora filer som saktar ner ditt arbetsflöde? **Hur man extraherar metadata** snabbt är en vanlig utmaning, och GroupDocs.Redaction‑biblioteket för .NET erbjuder ett snabbt, minnes‑effektivt sätt att hämta dokumentdetaljer direkt från strömmar. I den här handledningen lär du dig hur du installerar biblioteket, hämtar filtyp, sidantal och storlek från en ström, samt förbereder en utmatningsmapp för vidare bearbetning.

## Snabba svar
- **Vad betyder “extract metadata”?** Det betyder att läsa egenskaper som filtyp, sidantal och storlek utan att öppna hela dokumentet i minnet.  
- **Vilket bibliotek hanterar detta?** GroupDocs.Redaction för .NET tillhandahåller ett inbyggt API för strömbaserad metadataextraktion.  
- **Behöver jag en licens?** En gratis provperiod fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Kan jag bearbeta PDF-filer större än 1 GB?** Ja – strömmar låter dig hantera filer upp till 2 GB utan att ladda hela filen.  
- **Vilka .NET-versioner stöds?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ och .NET 6+.

## Vad är metadataextraktion från strömmar?
Metadataextraktion från strömmar är processen att läsa dokumentegenskaper direkt från ett `Stream`‑objekt, vilket undviker fullständig filinläsning och därmed sparar minne och CPU‑tid. Denna teknik är idealisk för batch‑behandling eller molnbaserade tjänster där resurser är begränsade.

## Varför använda GroupDocs.Redaction för metadataextraktion?
GroupDocs.Redaction stödjer **30+ filformat** (inklusive PDF, DOCX, XLSX, PPTX och bildtyper) och kan bearbeta dokument upp till **2 GB** i storlek samtidigt som minnesanvändningen hålls under **50 MB**. Dess `Redactor`‑API erbjuder ett enda anrop för att hämta all viktig dokumentinformation, vilket eliminerar behovet av flera parsers.

## Förutsättningar

- **GroupDocs.Redaction for .NET** (latest version)  
- **.NET Framework** 4.5+ **or** **.NET Core/5+/6+**  
- Grundläggande C#‑kunskaper och bekantskap med fil‑I/O  
- Visual Studio 2019 eller senare

## Hur installerar jag GroupDocs.Redaction för .NET?
För att börja använda GroupDocs.Redaction måste du först lägga till biblioteket i ditt projekt. Detta kan göras via .NET CLI, Visual Studio Package Manager eller NuGet‑UI. Välj den metod som passar ditt arbetsflöde; CLI är idealiskt för skriptbara byggen, medan UI erbjuder ett grafiskt sätt att bläddra bland versioner och beroenden.

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**
- Öppna NuGet Package Manager i Visual Studio.  
- Sök efter **"GroupDocs.Redaction"** och installera den senaste versionen.

### Steg för att skaffa licens
1. **Gratis provperiod:** Ladda ner en provlicens för att utforska alla funktioner utan begränsningar.  
2. **Tillfällig licens:** Begär en tillfällig licens från [GroupDocs](https://purchase.groupdocs.com/temporary-license/) för förlängd testning.  
3. **Köp:** När du är redo för produktion, köp en kommersiell licens.  

För mer information, besök [GroupDocs webbplats](https://purchase.groupdocs.com/temporary-license/).

### Grundläggande initiering och konfiguration
`Redactor`‑klassen är ingångspunkten för alla operationer, inklusive metadataextraktion.

`Redactor` är kärnklassen som representerar ett dokumentobjekt och tillhandahåller metoder för radering, informationshämtning och filmanipulation. När den är installerad kan du skapa ett `Redactor`‑objekt som visas nedan:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

Nu när biblioteket är klart, låt oss dyka in i implementationsdetaljerna.

## Hur extraherar man metadata från ett dokumentflöde?
Läs in dokumentet som ett **skrivskyddat flöde**, initiera `Redactor` och anropa `GetDocumentInfo()` för att hämta metadata i ett enda steg. Detta tillvägagångssätt undviker att ladda hela filen i minnet, vilket är avgörande för stora PDF‑filer eller Office‑dokument med hundratals sidor.

**Direkt svar:** Öppna filen med `File.OpenRead()`, skicka flödet till `new Redactor(stream)`, och anropa sedan `redactor.GetDocumentInfo()` – metoden returnerar ett objekt som innehåller filtyp, sidantal och storlek i bara tre kodrader.

### Steg 1: Förbered källfilens sökväg
Först, säkerställ att källfilen finns och att målmappen är redo. Hjälpmetoden nedan kontrollerar utmatningskatalogen och skapar den om den behövs.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*Varför?* Detta garanterar en giltig sökväg för efterföljande filoperationer och förhindrar `DirectoryNotFoundException`.

### Steg 2: Öppna dokumentflödet
Att använda `File.OpenRead()` öppnar filen som ett **skrivskyddat flöde**, vilket håller minnesanvändningen låg även för gigabyte‑stora filer.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*Varför?* Strömmar möjliggör bearbetning i farten, så att du kan arbeta med delar av filen snarare än hela dokumentet.

### Steg 3: Initiera Redactor med dokumentflödet
`Redactor` är det primära API‑objektet som ger dig åtkomst till dokumentnivåoperationer, inklusive metadataextraktion.

`Redactor` representerar ett enskilt dokument laddat från ett flöde och exponerar metoder som `GetDocumentInfo()` för snabb egenskapshämtning.  

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*Varför?* Att instansiera `Redactor` med ett flöde binder objektet till den underliggande filen utan att helt ladda den.

### Steg 4: Hämta dokumentmetadata
Att anropa `GetDocumentInfo()` returnerar ett `DocumentInfo`‑objekt som innehåller filformat, sidantal och filstorlek.

`GetDocumentInfo()` extraherar kärnegenskaper (format, sidantal, storlek) i ett enda anrop, vilket eliminerar behovet av separata parsers.  

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*Varför?* Detta steg konsoliderar all väsentlig metadata, vilket gör det enkelt att logga, filtrera eller dirigera dokument baserat på deras egenskaper.

## Hur förbereder man en utmatningskatalog för bearbetade filer?
Innan du skriver några bearbetade filer, säkerställ att destinationsmappen finns och är skrivbar. Genom att programatiskt kontrollera sökvägen och skapa den när den saknas undviker du vanliga körningsexceptioner som `DirectoryNotFoundException` eller behörighetsfel. Detta enkla steg gör också din kod portabel över miljöer, oavsett om den körs lokalt, på en server eller i en container.

**Direkt svar:** Använd `Directory.Exists()` för att kontrollera om mappen finns och `Directory.CreateDirectory()` för att skapa den om den inte finns – denna enradskontroll garanterar en giltig sökväg innan någon skrivoperation.

### Implementera en hjälpfunktion
Metoden nedan kapslar in logiken för kontroll‑och‑skapa, och returnerar den verifierade sökvägen för senare användning.

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

*Varför?* Att centralisera denna logik minskar duplicering och gör kodbasen lättare att underhålla.

## Vanliga problem och lösningar
- **Behörighetsfel:** Säkerställ att applikationen körs under ett konto med skrivbehörighet till målmappen.  
- **Ogiltiga sökvägar:** Dubbelkolla sökseparatorer (`\\` på Windows, `/` på Linux/macOS) för att undvika `DirectoryNotFoundException`.  
- **Hantering av stora filer:** Frigör strömmar omedelbart (`using`‑satser) för att släppa OS‑handtag och förhindra läckor.

## Praktiska tillämpningar
1. **Automatiserad dokumentintagning:** Extrahera metadata vid uppladdning och lagra dem sedan i en databas för snabb sökning och efterlevnadsrapportering.  
2. **Juridiska & efterlevnadsrevisioner:** Hämta sidantal och filtyper för att verifiera att dokument uppfyller regulatoriska standarder innan arkivering.  
3. **Enterprise Content Management:** Använd metadata för att automatiskt kategorisera filer i mappar, vilket förbättrar organisation och hämtningstid.

## Prestandaöverväganden
- **Minneshantering:** Omslut alltid strömmar i `using`‑block så att de frigörs automatiskt.  
- **Batch‑behandling:** Bearbeta dokument i grupper om 10‑20 för att balansera genomströmning och minnesanvändning, särskilt på resurssvaga servrar.  
- **Parallellism:** Använd `Parallel.ForEach` för oberoende filer, men övervaka CPU och I/O för att undvika konkurrens.

## Slutsats
Du har nu en komplett, produktionsklar guide om **hur man extraherar metadata** från dokumentströmmar med GroupDocs.Redaction för .NET. Genom att följa stegen ovan kan du effektivt hämta filtyp, sidantal och storlek samtidigt som minnesanvändningen hålls låg och stora filer hanteras smidigt.

**Nästa steg**
- Granska den fullständiga API‑referensen i [dokumentationen](https://docs.groupdocs.com/redaction/net/).  
- Gå djupare in i [GroupDocs Redaction .NET-dokumentationen](https://docs.groupdocs.com/redaction/net/) för att utforska radering, vattenstämpling och OCR‑funktioner.  
- Experimentera med olika filformat (PDF, DOCX, XLSX) för att se hur metadata varierar mellan typer.  
- Integrera den extraherade metadata i din befintliga dokumenthanterings- eller söklösning.

## Vanliga frågor

**Q:** Vad är det primära användningsfallet för GroupDocs.Redaction’s metadataextraktion?  
**A:** Det möjliggör snabb, minnes‑effektiv hämtning av dokumentegenskaper för indexering, efterlevnadskontroller och automatiserad dirigering utan att öppna hela filen.

**Q:** Kan jag extrahera metadata från lösenordsskyddade filer?  
**A:** Ja, ange lösenordet när du konstruerar `Redactor`‑objektet; API‑t kommer att dekryptera strömmen internt.

**Q:** Stöder biblioteket icke‑PDF‑format som DOCX eller XLSX?  
**A:** Absolut – GroupDocs.Redaction hanterar över 30 format, inklusive PDF, DOCX, XLSX, PPTX och vanliga bildtyper.

**Q:** Hur stor en dokument kan jag bearbeta med strömmar?  
**A:** Strömmar tillåter bearbetning av filer upp till **2 GB** medan minnesförbrukningen hålls under **50 MB**, tack vare läsning i farten.

**Q:** Var kan jag få hjälp om jag stöter på problem?  
**A:** Besök [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) för community‑stöd, eller konsultera den officiella dokumentationen för felsökningstips.

---

**Senast uppdaterad:** 2026-06-11  
**Testad med:** GroupDocs.Redaction 23.12 för .NET  
**Författare:** GroupDocs  

**Resurser**  
- **Dokumentation:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API‑referens:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Nedladdning:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## Relaterade handledningar

- [Mästra dokumentmetadatahämtning med GroupDocs.Redaction .NET API](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)
- [Hur man raderar dokumentmetadata med GroupDocs.Redaction för .NET – En omfattande guide](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Säker dokumentradering i .NET med strömmar: En guide för GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)