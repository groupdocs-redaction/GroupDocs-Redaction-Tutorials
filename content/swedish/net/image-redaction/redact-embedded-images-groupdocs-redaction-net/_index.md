---
date: '2026-10-16'
description: Lär dig hur du använder GroupDocs för att maskera inbäddade bilder i
  Word-dokument med GroupDocs.Redaction .NET API, och hålla känslig data säker.
keywords:
- how to use groupdocs
- hide pictures word
- redactor word document
- redact images word
- word image masking
lastmod: '2026-10-16'
og_description: Hur du använder GroupDocs för att maskera inbäddade bilder i Word-dokument
  med .NET API. Skydda konfidentiella bilder snabbt och pålitligt.
og_image_alt: Guide showing GroupDocs.Redaction .NET API redacting images in a Word
  file
og_title: Hur man använder GroupDocs för att maskera bilder i Word med .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  headline: How to use GroupDocs to redact images in Word with .NET
  type: TechArticle
- description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  name: How to use GroupDocs to redact images in Word with .NET
  steps:
  - name: '**Confidential reports:** Redact logos or charts before external distribution.'
    text: '**Confidential reports:** Redact logos or charts before external distribution.'
  - name: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
    text: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
  - name: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
    text: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
  - name: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
    text: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
  type: HowTo
- questions:
  - answer: Yes, iterate over each picture node and call `ImageAreaRedaction` for
      every region you need to hide.
    question: Can I redact multiple pictures in one pass?
  - answer: Absolutely. Provide the password when constructing the `Redactor` object,
      and the library will open the document securely.
    question: Does GroupDocs.Redaction support password‑protected Word files?
  - answer: The API handles DOC, DOCX, RTF, HTML, PDF, and over 20 other formats,
      allowing you to build a universal redaction service.
    question: What file formats can I process besides DOCX?
  - answer: Use a temporary license from the GroupDocs portal; it enables full functionality
      for 30 days without watermarks.
    question: How do I test the redaction without a license?
  - answer: Visit the [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)
      forum for community assistance or contact GroupDocs sales for enterprise support.
    question: Where can I get help if I run into problems?
  type: FAQPage
tags:
- redact images
- GroupDocs.Redaction
- .NET document security
title: Hur man använder GroupDocs för att maskera bilder i Word med .NET
type: docs
url: /sv/net/image-redaction/redact-embedded-images-groupdocs-redaction-net/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder GroupDocs för att radera bilder i Word med .NET

När du behöver skydda konfidentiella bilder i en Microsoft Word‑fil blir **how to use GroupDocs** den första frågan. Denna handledning guidar dig genom varje steg som krävs för att hitta, maskera och permanent ta bort inbäddade bilder så att känslig information aldrig läcker.

## Snabba svar
- **Kan GroupDocs radera alla bilder automatiskt?** Ja, du kan iterera genom varje bild och tillämpa `ImageAreaRedaction`.
- **Vilka .NET‑versioner stöds?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Behöver jag en licens för utveckling?** En gratis provversion fungerar för testning; en permanent licens krävs för produktion.
- **Kommer den ursprungliga layouten att bevaras?** API‑et behåller text och formatering intakta medan bildområdet rensas.
- **Hur snabbt är processen?** GroupDocs.Redaction kan hantera 200‑sidiga dokument på under 2 sekunder på en vanlig server.

## Vad är GroupDocs.Redaction?
GroupDocs.Redaction är ett .NET‑bibliotek som möjliggör programmatisk radering av text, bilder och metadata över mer än 20 dokumentformat. Det bearbetar filer utan att kräva Microsoft Office installerat, vilket gör det idealiskt för server‑sidig automatisering. Det erbjuder API:er för att radera text, bilder och metadata, och stödjer batch‑bearbetning, anpassade raderingsmönster och efterlevnadsrapportering.

## Varför använda GroupDocs för bildradering i Word?
Biblioteket stödjer **20+ in‑ och utdataformat** och kan radera bilder i dokument upp till 500 MB utan att ladda hela filen i minnet. Dess inbyggda `ImageAreaRedaction`‑algoritm garanterar att det raderade området inte kan återställas, vilket uppfyller strikta efterlevnadsstandarder.

## Förutsättningar
- .NET Framework 4.5+ **eller** .NET Core 3.1+ installerat.
- Grundläggande kunskap i C# och bekantskap med Word‑filstrukturer.
- Tillgång till **GroupDocs.Redaction** NuGet‑paketet (gratis provversion eller licensierat).

## Hur man installerar GroupDocs.Redaction för .NET

### Hur installerar man GroupDocs.Redaction via .NET CLI?
Kör följande kommando i din projektmapp: `dotnet add package GroupDocs.Redaction`. Detta lägger till den senaste stabila versionen i din projektfil.

```bash
dotnet add package GroupDocs.Redaction
```

### Hur installerar man GroupDocs.Redaction med Package Manager?
Kör `Install-Package GroupDocs.Redaction` i Package Manager Console.

```powershell
Install-Package GroupDocs.Redaction
```

### Hur får man en tillfällig licens och använder den?
Du kan begära en tillfällig licens från sidan [Temporary License](https://purchase.groupdocs.com/temporary-license/).  
En tillfällig licens låter dig utvärdera hela funktionsuppsättningen utan vattenstämplar. Efter köp placerar du licensfilen i ditt projekt och laddar den som visas:

```csharp
using GroupDocs.Redaction;
```

## Hur man raderar inbäddade bilder i ett Word‑dokument?
För att radera bilder laddar du dokumentet med en Redactor‑instans, lokaliserar varje bild, definierar området som ska döljas och tillämpar ImageAreaRedaction. API‑et skriver över de valda pixlarna, vilket säkerställer att det ursprungliga visuella innehållet inte kan återställas, samtidigt som den omgivande layouten och texten bevaras.

### Hur förbereder man käll- och målvägar?
Definiera de absoluta sökvägarna för originaldokumentet och det raderade resultatet innan du skapar några objekt.

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF";
string outputFile = "YOUR_OUTPUT_DIRECTORY/redacted_output.docx";
```

### Hur skapar och konfigurerar man Redactor‑objektet?
Redactor är kärnklassen som laddar ett dokument och utför raderingsoperationer.  
Skapa en instans av `Redactor` med ditt dokument:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Code for redaction will go here
}
```

### Hur specificerar man koordinater och tillämpar bildområdesradering?
ImageAreaRedaction är en metod som maskerar ett rektangulärt område i en bild med en solid färg.  
Identifiera övre‑vänstra punkten (`samplePoint`) och storleken (`sampleSize`) på området du vill dölja, och anropa sedan `ImageAreaRedaction`. Denna metod skriver över de valda pixlarna med en solid färg.

```csharp
Point samplePoint = new Point(516, 311);
Size sampleSize = new Size(170, 35);

RedactorChangeLog result = redactor.Apply(new ImageAreaRedaction(
    samplePoint,
    new RegionReplacementOptions(Color.Blue, sampleSize)
));
```

### Hur verifierar man raderingsresultatet och sparar filen?
Efter att ha anropat `Redactor.Apply()` inspekterar du `Result`‑objektet. Om `IsSuccess` är true skriver du det modifierade dokumentet till målvägen.

```csharp
if (result.Status != RedactionStatus.Failed)
{
    var savedOutputFile = redactor.Save();
    Console.WriteLine($"Redacted document saved as: {savedOutputFile}");
}
```

## Vanliga problem och felsökningstips
- **Koordinatfel:** Säkerställ att X/Y‑värdena ligger inom bildens gränser; annars kastar API‑et ett `ArgumentOutOfRangeException`.
- **Saknad licens:** En provlicens går ut efter 30 dagar; ersätt den med en permanent för att undvika körfel.
- **Ej stödformat:** Verifiera att filändelsen finns bland de 20+ format som listas i dokumentationen; äldre `.doc`‑filer kan behöva konverteras till `.docx` först.

## Praktiska tillämpningar
1. **Konfidentiella rapporter:** Radera logotyper eller diagram innan extern distribution.
2. **Juridiska sammanfattningar:** Dölj kundfotografier eller skannade ID:n som innehåller personuppgifter.
3. **Affärsavtal:** Maskera proprietära diagram som avslöjar affärshemligheter.
4. **Statliga publikationer:** Ta bort känsliga satellitbilder från offentliga PDF‑filer genererade från Word.

## Prestandaöverväganden
- Bearbeta dokument sekventiellt när du hanterar stora batcher för att hålla minnesanvändningen låg.
- Använd `RedactorOptions` för att begränsa antalet trådar om du kör på en begränsad server.
- Frigör `Redactor`‑instansen omedelbart med `using` för att frigöra ohanterade resurser.

## Slutsats
Du vet nu **how to use GroupDocs** för att på ett tillförlitligt sätt radera inbäddade bilder i Word‑filer med .NET‑API‑et. Genom att följa stegen ovan kan du integrera denna funktion i vilken dokument‑bearbetningspipeline som helst, vilket säkerställer att konfidentiella bilder aldrig lämnar din organisation.

För djupare utforskning, experimentera med andra raderings typer (text, metadata) och integrera biblioteket i webbtjänster, bakgrundsprocesser eller Azure Functions.

## Vanliga frågor

**Q: Kan jag radera flera bilder i ett pass?**  
A: Ja, iterera över varje bildnod och anropa `ImageAreaRedaction` för varje område du behöver dölja.

**Q: Stöder GroupDocs.Redaction lösenordsskyddade Word‑filer?**  
A: Absolut. Ange lösenordet när du konstruerar `Redactor`‑objektet, så öppnar biblioteket dokumentet säkert.

**Q: Vilka filformat kan jag bearbeta förutom DOCX?**  
A: API‑et hanterar DOC, DOCX, RTF, HTML, PDF och över 20 andra format, vilket låter dig bygga en universell raderingstjänst.

**Q: Hur testar jag raderingen utan licens?**  
A: Använd en tillfällig licens från GroupDocs‑portalen; den möjliggör full funktionalitet i 30 dagar utan vattenstämplar.

**Q: Var kan jag få hjälp om jag stöter på problem?**  
A: Besök forumet [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33) för community‑hjälp eller kontakta GroupDocs‑försäljning för företagsstöd.

## Ytterligare resurser
- **Dokumentation:** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/net/)
- **API‑referens:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Nedladdning:** [Latest Releases](https://releases.groupdocs.com/redaction/net/)

---

**Senast uppdaterad:** 2026-10-16  
**Testad med:** GroupDocs.Redaction 23.12 for .NET  
**Författare:** GroupDocs

## Relaterade handledningar
- [Hur man raderar dokument med GroupDocs.Redaction .NET – En komplett guide](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Radera och spara dokument Groupdocs Redaction Net](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Mästra skiftlägeskänslig exakt frasradering med GroupDocs.Redaction .NET för dokumentssäkerhet](/redaction/net/text-redaction/groupdocs-redaction-net-case-sensitive-exact-phrase-redaction/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}