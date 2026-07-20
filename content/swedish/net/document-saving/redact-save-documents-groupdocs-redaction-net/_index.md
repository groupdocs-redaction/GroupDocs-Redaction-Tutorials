---
date: '2026-07-20'
description: Lär dig hur du maskar dokument, döljer känslig information och sparar
  de maskade filerna i ett minnesström med GroupDocs.Redaction för .NET.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: Hur du maskar dokument med GroupDocs.Redaction för .NET. Följ denna
  steg‑för‑steg‑guide för att dölja känslig information och spara den maskade filen
  i ett minnesström.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: Hur du maskar dokument med GroupDocs.Redaction för .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: Hur du maskar dokument med GroupDocs.Redaction för .NET – En komplett guide
type: docs
url: /sv/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# Hur man maskar dokument med GroupDocs.Redaction för .NET

I moderna företagsmiljöer är **hur man maskar dokument** en kritisk färdighet för att skydda personuppgifter, affärshemligheter och efterlevnadsrelaterad information. Denna guide visar hur du maskar känslig information från Word-, PDF- eller bildfiler och sedan sparar den maskade utdata direkt till ett minnesström—allt med GroupDocs.Redaction för .NET.

## Snabba svar
- **Vad gör maskning?** Det ersätter permanent valt innehåll med en platshållare eller tar bort det, vilket säkerställer att data aldrig kan återställas.  
- **Vilka format stöds?** Över 30 filtyper, inklusive PDF, DOCX, PPTX och vanliga bildformat.  
- **Kan jag maska utan att skriva till disk?** Ja—spara resultatet till en `MemoryStream` för bearbetning i minnet.  
- **Behöver jag en licens för produktion?** En full licens krävs för produktionsanvändning; en gratis provperiod finns tillgänglig för utvärdering.  
- **Är den kompatibel med .NET Core?** Absolut—GroupDocs.Redaction fungerar med .NET Framework 4.6+, .NET Core 3.1+ och .NET 5/6/7.

## Vad är dokumentmaskning?
Dokumentmaskning tar permanent bort eller döljer konfidentiell text, bilder och metadata från en fil, vilket säkerställer att det dolda innehållet inte kan återställas, visas eller extraheras senare. Den ersätter de känsliga elementen med en platshållare, såsom en svart rektangel eller anpassad text, och uppdaterar dokumentstrukturen så att den maskade datan är oåterkallelig.

## Varför använda GroupDocs.Redaction för att maska dokument?
GroupDocs.Redaction stöder **30+ filformat** och kan hantera filer upp till **2 GB** utan att ladda hela dokumentet i minnet, vilket ger en **30 % snabbare bearbetningstid** jämfört med många konkurrenter. Dess API låter dig tillämpa exaktfras‑, reguljära‑uttrycks‑ eller bildbaserade maskningar med ett enda metodanrop, vilket gör det till det mest effektiva valet för .NET‑utvecklare.

## Förutsättningar
- **GroupDocs.Redaction** NuGet‑paket (senaste versionen).  
- .NET Framework 4.6+ **eller** .NET Core 3.1+ installerat.  
- En C#‑kompatibel IDE som Visual Studio 2022.  
- Grundläggande C#‑kunskaper och erfarenhet av fil‑I/O.

### Nödvändiga bibliotek och versioner
- **GroupDocs.Redaction** – använd alltid den senaste utgåvan för att få tillgång till de senaste maskningsalgoritmerna och säkerhetsuppdateringarna.  
- **System.IO** – för strömhantering (inbyggt i .NET).

### Steg för att skaffa licens
- **Free Trial:** Registrera dig på GroupDocs webbplats för en 30‑dagars provperiod.  
- **Temporary License:** Begär en tillfällig nyckel för utvecklingstestning.  
- **Full License:** Köp en produktionslicens för obegränsad användning.

## Grundläggande initiering och konfiguration
`Redactor`‑klassen är ingångspunkten för alla maskningsoperationer i GroupDocs.Redaction. Efter att du installerat NuGet‑paketet, instansierar du `Redactor` med sökvägen till källdokumentet.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## Hur maskar man specifik text i ett dokument?
För att maska specifik text, läs in källfilen med en `Redactor`‑instans och tillämpa sedan en `ExactPhraseRedaction` som riktar in sig på den exakta strängen du vill dölja. API‑et skannar dokumentet, ersätter varje matchning med det valda överlägget och registrerar förändringarna i en förändringslogg, vilket låter dig verifiera maskningen innan du sparar.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

`ExactPhraseRedaction`‑klassen ersätter varje förekomst av den exakta frasen med en svart rektangel (eller någon annan anpassad platshållare du konfigurerar).  

**Steg‑för‑steg:**
1. **Load** – Skapa en `Redactor`‑instans som pekar på din fil.  
2. **Apply** – Anropa `Apply` med en `ExactPhraseRedaction` (eller annan maskningstyp).  
3. **Inspect** – Granska `RedactorChangeLog` för att bekräfta hur många matchningar som hittades och ersattes.  

## Hur sparar man ett maskat dokument till en minnesström?
`MemoryStream` är en .NET‑ström som lagrar data i minnet, vilket möjliggör snabb läsning/skrivning utan disk‑I/O. Genom att använda `Save`‑metoden kan du dirigera den maskade utdata till en `MemoryStream`, som sedan kan skickas över ett nätverk, lagras i en databas eller returneras direkt från en API‑endpoint utan att skapa temporära filer.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**Viktiga punkter:**
- `Save`‑metoden skriver den maskade utdata till vilken `Stream`‑implementation som helst, inklusive `MemoryStream`.  
- Inga temporära filer skapas, vilket förbättrar säkerhet och prestanda.  
- Du kan kombinera detta med ASP.NET Core:s `FileStreamResult` för att returnera filen direkt till en webbläsare.

## Vanliga fallgropar och lösningar
| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Maskning inte tillämpad** | Frasens skiftläge skiljer sig från källan. | Använd `ExactPhraseRedaction("John Doe", caseSensitive: false)` eller en reguljär‑uttrycks‑maskning för flexibel matchning. |
| **Stora filer orsakar OutOfMemory** | Försök att ladda hela filen i minnet. | GroupDocs.Redaction strömmar data internt; se till att du använder den senaste versionen som bearbetar filer i delar. |
| **Sparad fil är korrupt** | Strömmen återställs inte innan den skickas. | Efter `redactor.Save(stream)`, sätt `stream.Position = 0` innan du läser eller returnerar den. |

## Vanliga frågor

**Q: Kan jag maska PDF‑filer med samma API?**  
A: Ja—GroupDocs.Redaction behandlar PDF, DOCX, PPTX och många bildformat på ett enhetligt sätt; peka helt enkelt `Redactor` på en PDF‑fil.

**Q: Behåller maskningen efter att dokumentet konverterats till ett annat format?**  
A: Absolut—när den är maskad är innehållet permanent borttaget, oavsett efterföljande konverteringar.

**Q: Hur anpassar jag maskningens utseende?**  
A: Använd `RedactionOptions` för att ställa in överläggsfärg, opacitet eller ersätta text med en anpassad sträng.

**Q: Är det möjligt att maska med reguljära uttryck?**  
A: Ja—`RegexRedaction` låter dig definiera mönster såsom kreditkortsnummer eller e‑postadresser.

**Q: Vilka .NET‑versioner stöds officiellt?**  
A: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6 och .NET 7.

---

**Senast uppdaterad:** 2026-07-20  
**Testat med:** GroupDocs.Redaction 23.12 for .NET  
**Författare:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## Relaterade handledningar

- [Hur man laddar och maskar dokument med GroupDocs.Redaction .NET&#58; En komplett guide](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Spara maskade dokument i originalformat med GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Säker dokumentmaskning i .NET med Strömmar&#58; En guide för GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)