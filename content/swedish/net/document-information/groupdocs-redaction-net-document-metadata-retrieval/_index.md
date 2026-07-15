---
date: '2026-06-06'
description: Lär dig hur du hämtar metadata och extraherar dokumentmetadata med GroupDocs.Redaction
  .NET, vilket möjliggör robust dokumenthantering och efterlevnad.
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
title: Hur man hämtar metadata med GroupDocs.Redaction .NET API
type: docs
url: /sv/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# Hur man hämtar metadata med GroupDocs.Redaction .NET

I dagens digitala era är **hur man hämtar metadata** från en fil ett grundläggande steg för alla dokument‑centrerade applikationer. Oavsett om du behöver läsa filmetadata för regelefterlevnadsgranskningar, extrahera dokumentegenskaper för indexering eller helt enkelt visa dokumentets storlek i ett UI, ger GroupDocs.Redaction .NET dig ett koncist API för att göra det på bara några rader C#. Denna handledning guidar dig genom hela processen, från miljöinställning till visning av den hämtade informationen, så att du kan börja extrahera dokumentmetadata omedelbart.

## Snabba svar
- **Vad är den primära metoden för att hämta metadata?** Anropa `Redactor.GetDocumentInfo()` på en `Redactor`‑instans.  
- **Vilka format stöds?** Över 50 in‑ och utdataformat, inklusive PDF, DOCX, XLSX, PPTX och bildtyper.  
- **Behöver jag en licens för utveckling?** En gratis provlicens fungerar för testning; en full licens krävs för produktion.  
- **Kan jag bearbeta stora filer?** Ja—GroupDocs.Redaction hanterar dokument med flera hundra sidor utan att ladda hela filen i minnet.  
- **Finns async‑stöd tillgängligt?** API‑et kan omslutas i async‑mönster för att hålla UI‑trådar responsiva.

## Vad är metadatahämtning i GroupDocs.Redaction?
Metadatahämtning är processen att komma åt ett dokuments inbyggda egenskaper—såsom filtyp, sidantal och storlek—genom bibliotekets API. Genom att extrahera dessa egenskaper kan utvecklare programatiskt bedöma dokumentkarakteristik, stödja indexering, upprätthålla regelefterlevnad och fatta informerade beslut om vidare bearbetningssteg.

## Hur man hämtar dokumentmetadata?
`Redactor`‑klassen är det primära gränssnittet för att ladda och inspektera dokument i GroupDocs.Redaction.  
`GetDocumentInfo()` är en metod som returnerar ett `DocumentInfo`‑objekt som innehåller dokumentets metadata.  

Läs in din fil med `new Redactor("path/to/file")` och anropa `GetDocumentInfo()`—anropet returnerar ett `DocumentInfo`‑objekt med typ, sidantal, storlek och andra egenskaper. Detta tvåstegs‑förfarande fungerar för alla stödjade format och kräver ingen extra konfiguration. Du kan sedan läsa fält som `FileType`, `PageCount` och `FileSize` för att visa eller logga informationen.

## Förutsättningar

- **GroupDocs.Redaction .NET** version 21.6 eller nyare.  
- .NET Framework 4.7.2 +, .NET Core 3.1 +, eller .NET 5/6+.  
- Grundläggande C#‑kunskaper och en utvecklings‑IDE (Visual Studio, Rider, etc.).

## Konfigurera GroupDocs.Redaction för .NET

Att komma igång med GroupDocs.Redaction är enkelt. Installera paketet med någon av följande metoder:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

Eller, använd **NuGet Package Manager UI**: Sök enkelt efter “GroupDocs.Redaction” och klicka på **Install**.

### Licensanskaffning

För att prova GroupDocs.Redaction kan du skaffa en gratis provlicens. För pågående utveckling eller produktionsanvändning, köp en full licens eller begär en tillfällig licens från den officiella webbplatsen.

När paketet är installerat, initiera biblioteket enligt följande:

```csharp
using GroupDocs.Redaction;
```

## Implementeringsguide

### Funktion för att hämta dokumentinformation

Denna funktion fokuserar på att extrahera viktig metadata från dokument med GroupDocs.Redaction .NET. Följ dessa steg:

#### Steg 1: Förbered din dokumentväg

Definiera den absoluta eller relativa sökvägen till målfilen:

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

Ersätt `YOUR_DOCUMENT_DIRECTORY` med den mapp som innehåller ditt dokument.

#### Steg 2: Initiera Redactor‑instans

Skapa ett `Redactor`‑objekt som ger åtkomst till metadata‑metoder:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### Steg 3: Hämta dokumentinformation

Anropa `GetDocumentInfo()` på `Redactor`‑instansen för att hämta alla tillgängliga egenskaper:

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

Det returnerade objektet innehåller filtyp, antal sidor och filstorlek.

#### Steg 4: Visa dokumentdetaljer

Skriv ut informationen till konsolen eller UI. Exempelkoden (kommenterad för fristående körningar) visar hur man skriver ut varje egenskap:

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### Varför använda GroupDocs.Redaction för metadataextraktion?
GroupDocs.Redaction stödjer **50+ filformat** och kan bearbeta dokument upp till **2 GB** i storlek samtidigt som minnesförbrukningen hålls under **100 MB** för typiska arbetsbelastningar. Biblioteket extraherar metadata utan att ladda hela dokumentet, vilket ger snabba svar—ofta under **200 ms** för en 100‑sidig PDF på standardserverutrustning.

### Vanliga problem och lösningar

- **Felaktig filsökväg** – Verifiera söksträngen och säkerställ att filen är åtkomlig för den körande processen.  
- **Format som inte stöds** – Kontrollera formatlistan; om ett format saknas, överväg att konvertera det först.  
- **Prestandaflaskhalsar** – För mycket stora filer, aktivera streamingalternativ eller bearbeta sidor i batcher för att begränsa minnesanvändning.

## Praktiska tillämpningar

Att förstå ett dokuments metadata möjliggör flera verkliga scenarier:

1. **Document Management Systems (DMS)** – Automatisera kategorisering och indexering baserat på typ, storlek eller sidantal.  
2. **Compliance Auditing** – Verifiera att konfidentiella filer innehåller nödvändig metadata innan arkivering.  
3. **Data Migration** – Gruppera filer efter egenskaper för att effektivisera massmigrationsuppgifter.  

## Prestandaöverväganden

- **Efficient Resource Usage** – Använd `Redactor`‑instansen inom ett `using`‑block för att garantera korrekt resurshantering.  
- **Asynchronous Patterns** – Omslut metadata‑anrop i `Task.Run` eller implementera async‑omslag för att hålla UI‑trådar responsiva i skrivbords‑ eller webbappar.

## Vanliga frågor

**Q: Vilka dokumentformat kan jag extrahera metadata från?**  
A: GroupDocs.Redaction läser metadata från mer än 50 format, inklusive PDF, DOCX, XLSX, PPTX, HTML och vanliga bildtyper.

**Q: Hur hanterar jag lösenordsskyddade filer?**  
A: Skicka lösenordet till `Redactor`‑konstruktorn; API‑et kommer att dekryptera filen innan metadata extraheras.

**Q: Finns det någon gräns för storleken på filer jag kan bearbeta?**  
A: Det finns ingen hård gräns, men filer större än 2 GB kan kräva ytterligare minnestuning; prestandan förblir linjär med filstorleken.

**Q: Kan jag hämta metadata i en batch‑operation?**  
A: Ja—iterera över en samling filsökvägar och anropa `GetDocumentInfo()` för var och en; biblioteket är trådsäkert för parallell körning.

**Q: Behöver jag en licens för utvecklingsbyggen?**  
A: En gratis provlicens räcker för utveckling och testning; en kommersiell licens krävs för produktionsdistributioner.

## Resurser

- [Dokumentation](https://docs.groupdocs.com/redaction/net/)  
- [API‑referens](https://reference.groupdocs.com/redaction/net)  
- [Nedladdning](https://releases.groupdocs.com/redaction/net/)  
- [Gratis supportforum](https://forum.groupdocs.com/c/redaction/33)  
- [Information om tillfällig licens](https://purchase.groupdocs.com/temporary-license/)

## Slutsats

Du har nu en komplett, steg‑för‑steg‑guide om **hur man hämtar metadata** med GroupDocs.Redaction .NET. Genom att utnyttja `Redactor.GetDocumentInfo()`‑metoden kan du snabbt läsa filmetadata, stödja regelefterlevnadsarbetsflöden och förbättra vilken dokument‑bearbetningspipeline som helst. Utforska ytterligare Redaction‑funktioner—såsom innehållsmaskering, vattenstämpling och dokumentkonvertering—för att bygga en fullständigt utrustad dokumenthanteringslösning.

---

**Senast uppdaterad:** 2026-06-06  
**Testad med:** GroupDocs.Redaction .NET 21.6 (senaste vid skrivtillfället)  
**Författare:** GroupDocs  

## Relaterade handledningar

- [Hur man extraherar dokumentmetadata från strömmar med GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [Hur man maskerar dokumentmetadata med GroupDocs.Redaction för .NET – En omfattande guide](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Handledningar för dokumentladdning med GroupDocs.Redaction för .NET](/redaction/net/document-loading/)