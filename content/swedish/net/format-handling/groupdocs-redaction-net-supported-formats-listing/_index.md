---
date: '2026-07-20'
description: Lär dig hur du listar format med GroupDocs.Redaction .NET, integrera
  funktionen i ditt dokumentarbetsflöde och förbättra prestandan.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Upptäck hur du listar format med GroupDocs.Redaction .NET, se en steg‑för‑steg‑guide
  och få tips för optimal prestanda i dina .NET‑applikationer.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Hur man listar format med GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: Hur man listar format med GroupDocs.Redaction .NET
type: docs
url: /sv/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Hur man listar format med GroupDocs.Redaction .NET

Att hantera ett brett utbud av dokumenttyper är en daglig verklighet för utvecklare som bygger dokument‑centrerade applikationer. I den här handledningen kommer du att lära dig **hur man listar format** som GroupDocs.Redaction .NET kan hantera, så att du kan validera filer innan de bearbetas, presentera användarna med korrekta alternativ och hålla ditt arbetsflöde effektivt.

## Introduktion

Effektiv dokumenthantering börjar med att exakt veta vilka filtyper ditt bibliotek stödjer. GroupDocs.Redaction tillhandahåller en inbyggd metod för att hämta denna information, vilket låter dig bygga dynamiska UI‑element, upprätthålla valideringsregler och undvika körfel. Nedan hittar du allt du behöver för att komma igång, från installation till praktiska kodexempel och prestandatips.

### Snabba svar
- **Vad betyder “hur man listar format”?** Det avser att hämta samlingen av filändelser som GroupDocs.Redaction kan bearbeta.  
- **Behöver jag en licens?** Ja, en giltig GroupDocs.Redaction‑licens krävs för produktionsanvändning.  
- **Vilka .NET‑versioner stöds?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Hur många format finns tillgängliga?** Över 30 in‑ och utdataformat stöds direkt.  
- **Behövs någon speciell konfiguration?** Ingen extra konfiguration krävs utöver standardbibliotekets initiering.

## Vad är “hur man listar format”?

Det innebär att anropa bibliotekets FileType‑API för att få en samling där varje post innehåller filändelsen och ett mänskligt läsbart namn. Utvecklare kan sedan iterera över denna samling för att bygga valideringsregler, fylla UI‑rullgardinsmenyer eller logga stödda typer, vilket säkerställer att endast kompatibla dokument bearbetas.

## Varför lista format med GroupDocs.Redaction?

GroupDocs.Redaction stödjer **30+** olika filtyper — inklusive PDF, DOCX, PPTX och bildformat — vilket gör att du kan hantera de flesta företagsdokument utan tredjeparts‑konverterare. Genom att programatiskt lista dessa format eliminerar du gissningar, minskar supportärenden och säkerställer att endast kompatibla filer kommer in i din bearbetningspipeline.

## Förutsättningar

- **GroupDocs.Redaction för .NET** – ladda ner det senaste paketet från den officiella webbplatsen.  
- **.NET Framework eller .NET Core** – kompatibel med din utvecklingsmiljö.  
- **Visual Studio** (eller någon C#‑kompatibel IDE).  
- Grundläggande kunskap om C#‑syntax.

## Installera GroupDocs.Redaction för .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Package Manager
`Install-Package GroupDocs.Redaction`

### NuGet Package Manager UI
- Sök efter **“GroupDocs.Redaction”** och installera den senaste versionen.

### Licensanskaffning
GroupDocs erbjuder en gratis provperiod, en tillfällig licens för utvärdering eller fullständiga köpalternativ. Besök GroupDocs webbplats för att skaffa den lämpliga licensfilen.

### Grundläggande initiering och konfiguration
Efter att ha lagt till paketet, referera till namnrymden och skapa en `Redactor`‑instans:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Implementeringsguide

### Hur listar jag format med GroupDocs.Redaction .NET?
Läs in biblioteket, anropa den statiska hjälpfunktionen och sortera resultaten — detta ger dig en färdig att använda samling på bara två kodrader. Använd `FileType.GetSupportedFileFormats()` för att hämta en `IEnumerable<FileType>` som innehåller varje formats filändelse och visningsnamn, och sortera sedan efter filändelse för en ren UI‑lista.

### Hämta stödda filformat

#### Översikt
Målet är att få en lista över filtyper som GroupDocs.Redaction kan hantera, vilket underlättar integration i valideringslogik, UI‑rullgardinsmenyer eller loggningsmekanismer.

#### Steg‑för‑steg‑implementering

**1. Hämta stödda filtyper**  
`FileType.GetSupportedFileFormats()` returnerar alla format som biblioteket känner igen. Metoden är en del av klassen `GroupDocs.Redaction.FileType`, som kapslar metadata såsom filändelse och vänligt namn.

**2. Visa stödda filtyper**  
Iterera över samlingen och skriv ut varje formats filändelse och beskrivning. Exempel på inline‑kod:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

Kodsnutten skriver ut en prydligt sorterad lista som “.pdf – Portable Document Format”, vilket gör den perfekt för att fylla UI‑element.

### Felsökningstips
- **Saknat paket** – Verifiera NuGet‑paketreferensen och återställ paket om det behövs.  
- **Fel licenssökväg** – Säkerställ att licensfilen kopieras till utmatningskatalogen eller ange en absolut sökväg.  
- **Ej stödd filändelse** – Om ett format inte listas, bekräfta att du använder den senaste biblioteksversionen; nyare releaser lägger till ytterligare format.

## Praktiska tillämpningar
Att förstå stödda filformat öppnar upp flera verkliga scenarier:

1. **Dokumenthanteringssystem** – Validera uppladdningar mot den stödda listan för att förhindra bearbetningsfel.  
2. **Innehållssäkerhet** – Tillämpa raderingsregler endast på filtyper som motorn säkert kan modifiera.  
3. **Batch‑bearbetningspipeline** – Filtrera stora filbatchar innan du anropar radering, vilket sparar CPU och minne.

## Prestandaöverväganden
- **Minnesanvändning** – Att lista format är en lätt operation; den laddar inte in något dokument i minnet.  
- **Batch‑operationer** – När du bearbetar hundratals filer, hämta formatlistan en gång och återanvänd den för att undvika onödiga anrop.  
- **Trådsäkerhet** – `FileType.GetSupportedFileFormats()` är trådsäker och kan anropas från parallella uppgifter utan synkronisering.

## Slutsats
Du har nu ett komplett, produktionsklart tillvägagångssätt för **hur man listar format** med GroupDocs.Redaction .NET. Genom att integrera denna funktion kan du förbättra validering, förbättra användarupplevelsen och hålla dina dokumentpipeline robusta.

### Nästa steg
- Utforska `Redactor`‑API:t för att tillämpa raderingsregler baserat på filtyp.  
- Kombinera formatlistan med en front‑end‑rullgardinsmeny för sömlöst filval.  
- Granska prestandaguide:n för att optimera storskaliga batch‑jobb.

## Vanliga frågor

**Q: Kan jag hämta formatlistan utan att initiera en Redactor‑instans?**  
A: Ja, `FileType.GetSupportedFileFormats()` är statisk och kräver ingen `Redactor`‑objekt.

**Q: Inkluderar listan både in‑ och utdataformat?**  
A: Metoden returnerar alla format som biblioteket både kan läsa och skriva; varje `FileType` innehåller en `CanRead`‑ och `CanWrite`‑flagga.

**Q: Hur ofta uppdateras den stödda formatlistan?**  
A: GroupDocs släpper formatuppdateringar med varje biblioteksversion; att kontrollera listan vid körning säkerställer att du alltid har den senaste uppsättningen.

**Q: Finns det ett sätt att filtrera endast PDF‑kompatibla format?**  
A: Ja, filtrera samlingen där `format.Extension == ".pdf"` eller där `format.Name.Contains("PDF")`.

**Q: Kommer detta tillvägagångssätt att fungera på .NET Core 2.1?**  
A: Metoden kräver .NET Core 3.1 eller senare; tidigare runtime‑versioner stöds inte.

## FAQ‑avsnitt
1. **Hur installerar jag GroupDocs.Redaction för .NET?**  
   Använd CLI‑kommandot `dotnet add package GroupDocs.Redaction` eller installera via NuGet Package Manager UI.  
2. **Vilka vanliga problem kan uppstå när man hämtar stödda format?**  
   Säkerställ att alla beroenden är återställda och att du refererar rätt namnrymd (`GroupDocs.Redaction`).  
3. **Kan jag använda denna funktion med icke‑.NET‑applikationer?**  
   Denna handledning fokuserar på .NET, men GroupDocs tillhandahåller liknande API:er för Java, Python och andra plattformar.  
4. **Hur kan jag optimera prestanda när jag använder GroupDocs.Redaction?**  
   Återanvänd formatlistan, undvik att ladda hela dokument när du bara kontrollerar kompatibilitet, och övervaka minnesanvändning under batch‑jobb.  
5. **Vilka filtyper stödjer GroupDocs.Redaction?**  
   Biblioteket stödjer 30+ format, inklusive PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG och många fler. Använd `FileType.GetSupportedFileFormats()` för att se hela listan.

## Resurser
- [Dokumentation](https://docs.groupdocs.com/redaction/net/)
- [API‑referens](https://reference.groupdocs.com/redaction/net)
- [Ladda ner GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Gratis supportforum](https://forum.groupdocs.com/c/redaction/33)
- [Tillfällig licens](https://purchase.groupdocs.com/temporary-license/)

---

**Senast uppdaterad:** 2026-07-20  
**Testad med:** GroupDocs.Redaction 4.2.0 for .NET  
**Författare:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## Relaterade handledningar

- [Handledningar för format‑hantering för GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Handledningar för dokumentladdning med GroupDocs.Redaction för .NET](/redaction/net/document-loading/)
- [Handledningar för dokumentsparning för GroupDocs.Redaction .NET](/redaction/net/document-saving/)