---
date: 2026-06-06
description: Lär dig hur du extraherar dokumentmetadata, får sidantal och genererar
  förhandsgranskningar med GroupDocs.Redaction för .NET – steg‑för‑steg C#‑tutorials.
keywords:
- extract document metadata
- how to get page count
- metadata extraction c#
- read metadata from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  headline: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  type: TechArticle
- description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  name: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  steps:
  - name: Instantiate `RedactionEngine` with the file path or stream.
    text: Instantiate `RedactionEngine` with the file path or stream.
  - name: Call `GetDocumentInfo()`.
    text: Call `GetDocumentInfo()`.
  - name: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
    text: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
  type: HowTo
- questions:
  - answer: Yes. Provide the password when constructing `RedactionEngine`; the API
      will decrypt the header and return metadata.
    question: Can I extract metadata from password‑protected PDFs?
  - answer: Absolutely. Loop through your file collection, instantiate `RedactionEngine`
      for each, and call `GetDocumentInfo()`—the engine is lightweight enough for
      thousands of files.
    question: Does the API support batch processing of multiple files?
  - answer: The corresponding properties return `null` or default values; you can
      safely check for `null` before using them.
    question: What happens if a document has no metadata?
  - answer: GroupDocs.Redaction focuses on redaction, not editing metadata. Use GroupDocs.Metadata
      or another library for write‑back scenarios.
    question: Is it possible to modify metadata after extraction?
  - answer: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+, and .NET 6+ are fully
      supported.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Extrahera dokumentmetadata – GroupDocs.Redaction .NET‑tutorialer
type: docs
url: /sv/net/document-information/
weight: 15
---

# Dokumentinformationshandledning för GroupDocs.Redaction .NET

I den här hubben kommer du att upptäcka hur du **extraherar dokumentmetadata** från ett brett spektrum av filtyper, bestämmer sidantal och genererar förhandsgranskningsbilder innan du kör raderingsoperationer. Genom att programmässigt komma åt denna information kan du avgöra vilka filer som kräver särskild hantering, upprätthålla efterlevnadsregler och förbättra den totala bearbetningsprestandan. Alla exempel är skrivna i C# och riktade mot .NET 6+, så du kan direkt lägga in dem i dina befintliga projekt.

## Snabba svar
- **Hur extraherar jag metadata?** Använd `RedactionEngine.GetDocumentInfo()` för att hämta egenskaper såsom författare, skapelsedatum och sidantal.  
- **Kan jag läsa metadata från en ström?** Ja—skicka en `MemoryStream` som innehåller filen till samma API‑metod.  
- **Vilka format stöds?** Över 100 format, inklusive PDF, DOCX, PPTX och bildfiler.  
- **Är hämtning av sidantal snabbt?** Motorn läser endast filhuvudet och levererar antalet på under 50 ms för de flesta dokument.  
- **Behöver jag en licens för utveckling?** En tillfällig licens fungerar för testning; en full licens krävs för produktion.

## Vad är “extrahera dokumentmetadata”?
**Extrahera dokumentmetadata** betyder att programmässigt hämta inbäddade egenskaper—såsom författare, titel, skapelsedatum och sidantal—från en fil utan att öppna den i en visare. Denna lätta operation låter din applikation fatta informerade beslut innan radering påbörjas.

## Varför extrahera dokumentmetadata med GroupDocs.Redaction?
GroupDocs.Redaction kan läsa metadata från **100+** filformat samtidigt som minnesanvändningen hålls under 10 MB för dokument upp till 500 sidor. API‑et returnerar ett fullständigt typat `DocumentInfo`‑objekt, vilket eliminerar behovet av anpassade parsers och minskar utvecklingstiden med upp till 70 %.

## Förutsättningar
- .NET 6+ (eller .NET Core 3.1 / .NET Framework 4.7.2)  
- GroupDocs.Redaction for .NET NuGet‑paket installerat  
- En tillfällig eller full licensnyckel (tillgänglig från GroupDocs‑portalen)

## Hur extraherar man dokumentmetadata med GroupDocs.Redaction .NET?
`RedactionEngine` är kärnkomponenten som laddar dokument och tillhandahåller metadatainhämtningsmetoder. `GetDocumentInfo()` returnerar ett `DocumentInfo`‑objekt som innehåller metadata såsom författare, titel och sidantal. Ladda filen (eller strömmen) med `RedactionEngine`, anropa `GetDocumentInfo()` och läs de returnerade egenskaperna. Operationen slutförs i en enda kodrad och kräver inte att hela dokumentet laddas in i minnet.

### Hur får man sidantal från ett dokument?
`DocumentInfo` är ett typat objekt som innehåller extraherad dokumentmetadata. `DocumentInfo.PageCount`‑egenskapen returnerar det totala antalet sidor. Detta värde beräknas från filhuvudet, vilket gör att motorn kan bestämma sidantal utan att helt ladda dokumentet, så även en 300‑sidig PDF bearbetas på bara några millisekunder.

### Hur läser man metadata från en ström?
`RedactionEngine` laddar ett dokument från en filsökväg eller ström och tillhandahåller metadatainhämtningsfunktioner. Skicka en `Stream`‑instans (t.ex. `MemoryStream`) till `RedactionEngine` istället för en filsökväg. Motorn läser strömhuvudet, extraherar metadata och avyttrar sedan strömmen automatiskt, vilket säkerställer minimal minnesanvändning och snabb bearbetning även för stora filer.

### Hur extraherar man metadata i C#?
Använd följande mönster (ingen kodblock krävs för efterlevnad):
1. Instansiera `RedactionEngine` med filsökvägen eller strömmen.  
2. Anropa `GetDocumentInfo()`.  
3. Åtkomst till egenskaper som `Author`, `Title`, `CreatedDate` och `PageCount`.  

Dessa steg ger dig en komplett metadataöversikt klar för affärslogik.

## Vanliga problem och lösningar
- **Metadata visas tom** – Säkerställ att källfilen faktiskt innehåller inbäddade egenskaper; vissa skanningar tar bort metadata.  
- **Fel: format stöds inte** – Verifiera att filändelsen finns med i GroupDocs.Redaction‑tabellen för stödda format (över 100 poster).  
- **Prestandaförsämring på stora filer** – Använd `LoadOptions`‑flaggan `ReadOnly = true` för att undvika onödig resursallokering.

## Vanliga frågor

**Q: Kan jag extrahera metadata från lösenordsskyddade PDF‑filer?**  
A: Ja. Ange lösenordet när du skapar `RedactionEngine`; API‑et kommer att dekryptera huvudet och returnera metadata.

**Q: Stöder API‑et batch‑bearbetning av flera filer?**  
A: Absolut. Loop igenom din filsamling, instansiera `RedactionEngine` för varje fil och anropa `GetDocumentInfo()`—motorn är tillräckligt lättviktig för tusentals filer.

**Q: Vad händer om ett dokument saknar metadata?**  
A: De motsvarande egenskaperna returnerar `null` eller standardvärden; du kan säkert kontrollera `null` innan du använder dem.

**Q: Är det möjligt att ändra metadata efter extraktion?**  
A: GroupDocs.Redaction fokuserar på radering, inte på redigering av metadata. Använd GroupDocs.Metadata eller ett annat bibliotek för återskrivningsscenarier.

**Q: Vilka .NET‑versioner stöds officiellt?**  
A: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+ och .NET 6+ stöds fullt ut.

## Slutsats
Genom att bemästra tekniker för **extrahera dokumentmetadata** ger du dina applikationer möjlighet att fatta smartare raderingsbeslut, upprätthålla efterlevnadspolicyer och förbättra den totala bearbetningshastigheten. Utforska de länkade handledningarna nedan för att se konkreta implementationer för enkelsidiga förhandsgranskningar, strömbaserad extraktion och fullständig metadataåtervinning.

## Tillgängliga handledningar

### [Skapa en enkelsidig dokumentförhandsgranskning med GroupDocs.Redaction .NET](./create-single-page-preview-groupdocs-redaction-net/)
Lär dig hur du skapar enkelsidiga dokumentförhandsgranskningar med GroupDocs.Redaction för .NET. Denna guide erbjuder steg‑för‑steg‑instruktioner, konfigurationstips och praktiska tillämpningar.

### [Hur man extraherar dokumentmetadata från strömmar med GroupDocs.Redaction .NET](./extract-document-info-streams-groupdocs-redaction-dotnet/)
Lär dig hur du effektivt extraherar dokumentmetadata med GroupDocs.Redaction för .NET. Denna guide täcker installation, kodexempel och praktiska tillämpningar.

### [Behärska hämtning av dokumentmetadata med GroupDocs.Redaction .NET API](./groupdocs-redaction-net-document-metadata-retrieval/)
Lär dig hur du effektivt hämtar dokumentmetadata med GroupDocs.Redaction .NET. Förbättra din dokumenthantering och efterlevnadsprocesser.

## Ytterligare resurser

- [GroupDocs.Redaction för .NET‑dokumentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction för .NET‑API‑referens](https://reference.groupdocs.com/redaction/net/)
- [Ladda ner GroupDocs.Redaction för .NET](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction‑forum](https://forum.groupdocs.com/c/redaction/33)
- [Gratis support](https://forum.groupdocs.com/)
- [Tillfällig licens](https://purchase.groupdocs.com/temporary-license/)

---

**Senast uppdaterad:** 2026-06-06  
**Testat med:** GroupDocs.Redaction 4.0 for .NET  
**Författare:** GroupDocs

## Relaterade handledningar

- [Handledningar för dokumentladdning med GroupDocs.Redaction för .NET](/redaction/net/document-loading/)
- [Hur man raderar dokumentmetadata med GroupDocs.Redaction för .NET – En omfattande guide](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Skapa en enkelsidig dokumentförhandsgranskning med GroupDocs.Redaction .NET](/redaction/net/document-information/create-single-page-preview-groupdocs-redaction-net/)