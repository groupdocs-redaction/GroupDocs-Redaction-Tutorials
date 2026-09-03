---
date: '2026-07-06'
description: Lär dig hur du sparar ett redigerat dokument samtidigt som du bevarar
  dess originalformat med GroupDocs.Redaction för .NET. Följ den här steg-för-steg-guiden
  för snabb och säker redigering.
keywords:
- save redacted document
- GroupDocs.Redaction .NET
- document redaction tutorial
schemas:
- author: GroupDocs
  dateModified: '2026-07-06'
  description: Learn how to save a redacted document while preserving its original
    format with GroupDocs.Redaction for .NET. Follow this step‑by‑step guide for fast,
    secure redaction.
  headline: Save Redacted Document in Original Format Using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to save a redacted document while preserving its original
    format with GroupDocs.Redaction for .NET. Follow this step‑by‑step guide for fast,
    secure redaction.
  name: Save Redacted Document in Original Format Using GroupDocs.Redaction .NET
  steps:
  - name: Initialize the Redactor
    text: 'Create an instance of the `Redactor` class with your document’s file path:'
  - name: Apply Exact Phrase Redaction
    text: '`ExactPhraseRedaction` is a built‑in redaction type that searches for an
      exact string and replaces it with a black rectangle or custom text.'
  - name: Configure Save Options
    text: '`SaveOptions` lets you keep the source file type, specify a suffix, and
      control memory usage.'
  - name: Save and Output
    text: 'Call the `Save` method with the configured options to write the redacted
      file to disk:'
  type: HowTo
- questions:
  - answer: Over 30 formats, including PDF, DOCX, PPTX, XLSX, and common image types
      such as PNG and JPEG.
    question: What file types can GroupDocs.Redaction handle?
  - answer: Yes – the `Redactor` class provides a `GetRedactions()` method that returns
      a collection you can render in a UI.
    question: Is it possible to preview redactions before saving?
  - answer: Absolutely. Supply the password when constructing the `Redactor` instance
      to unlock the file.
    question: Can I redact password‑protected documents?
  - answer: Yes – the NuGet package is compatible with .NET Framework 4.7.2+, .NET
      Core 3.1+, and .NET 5/6+.
    question: Does the library support .NET Core and .NET 5/6?
  - answer: Purchase a license through the GroupDocs website; a temporary trial license
      is available for evaluation.
    question: How do I obtain a production license?
  type: FAQPage
title: Spara redigerat dokument i originalformat med GroupDocs.Redaction .NET
type: docs
url: /sv/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/
weight: 1
---

# Spara raderat dokument i originalformat med GroupDocs.Redaction .NET

Att radera känslig data är ett vanligt efterlevnadskrav, men du vill inte förlora utseendet och känslan av originalfilen. **Denna handledning visar hur du sparar ett raderat dokument samtidigt som du behåller dess originalformat intakt** med hjälp av GroupDocs.Redaction för .NET. Du får en färdig‑att‑köra lösning som fungerar med PDF‑filer, Word‑filer och mer.

## Snabba svar
- **Vad är det snabbaste sättet att spara ett raderat dokument?** Ladda filen med `Redactor`, applicera en `ExactPhraseRedaction`, och anropa sedan `Save` med `SaveOptions` som behåller originalfilens typ.  
- **Vilka format stöds?** Över 30 format, inklusive PDF, DOCX, PPTX och bildtyper.  
- **Behöver jag en licens för provanvändning?** Ja – skaffa en tillfällig licens från GroupDocs‑portalen.  
- **Kan jag lägga till ett eget suffix till den sparade filen?** Absolut – sätt `SaveOptions.Suffix` till en valfri sträng (t.ex. ett datum).  
- **Är bearbetning av stora filer minnes‑effektiv?** Ja – GroupDocs.Redaction strömmar data och laddar aldrig hela filen i minnet.

## Vad är “spara raderat dokument”?
*Att spara ett raderat dokument* innebär att skriva den modifierade filen tillbaka till lagring samtidigt som dess ursprungliga layout, filtyp och metadata bevaras. GroupDocs.Redaction hanterar detta i ett enda anrop, vilket eliminerar behovet av manuell formatkonvertering. Processen behåller också inbäddade resurser såsom typsnitt, bilder och dokumentegenskaper, vilket säkerställer att utdata ser identisk ut som källan förutom det borttagna innehållet.

## Varför använda GroupDocs.Redaction för .NET?
GroupDocs.Redaction stöder **30+ in‑ och utdataformat** och kan bearbeta filer upp till **500 MB** utan att ladda hela dokumentet i minnet, vilket ger en **20‑30 % prestandaförbättring** jämfört med naiva fil‑omskrivningsmetoder. Dess API är helt hanterat, kräver ingen extern programvara och följer GDPR, HIPAA och andra regelverk.

## Förutsättningar
- **GroupDocs.Redaction for .NET** – kärnbiblioteket (senaste stabila versionen).  
- **.NET 6+** eller **.NET Framework 4.7.2+** installerat på din utvecklingsmaskin.  
- Grundläggande C#‑kunskap och bekantskap med Visual Studio eller din föredragna IDE.

### Nödvändiga bibliotek och beroenden
- **GroupDocs.Redaction for .NET**: Nödvändig för att applicera raderingar.

### Krav för miljöinställning
Verifiera att ditt projekt riktar sig mot en stödd .NET‑runtime. Konsultera den officiella GroupDocs‑dokumentationen för exakta versionstabeller.

### Kunskapsförutsättningar
Förståelse för C#‑syntax, fil‑I/O och undantagshantering.

## Konfigurera GroupDocs.Redaction för .NET

### Installationsinstruktioner
**Använd .NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Använd Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**Via NuGet Package Manager UI:**  
- Öppna NuGet Package Manager i Visual Studio.  
- Sök efter **"GroupDocs.Redaction"** och installera den senaste versionen.

### Licensanskaffning
Börja med en gratis provperiod för att testa funktionerna. Besök GroupDocs‑webbplatsen för att begära en tillfällig licens om det behövs. För långsiktig användning, överväg att köpa en licens från deras sida.

När den är installerad och licensierad, referera till GroupDocs.Redaction‑namnrymden i dina kodfiler:  
```csharp
using GroupDocs.Redaction;
```  

## Implementeringsguide

### Skapa och konfigurera Redactor
`Redactor`‑klassen är den centrala komponenten som laddar ett dokument och applicerar raderingsoperationer.

#### Steg 1: Initiera Redactor
Skapa en instans av `Redactor`‑klassen med ditt dokuments filsökväg:  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual path.
using (Redactor redactor = new Redactor(sourceFile))
{
    ...
}
```  

#### Steg 2: Applicera Exact Phrase Redaction
`ExactPhraseRedaction` är en inbyggd raderingstyp som söker efter en exakt sträng och ersätter den med en svart rektangel eller anpassad text.  
```csharp
// This replaces all instances of "John Doe" with "[personal]".
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```  

### Spara det raderade dokumentet
Att bevara originalformatet samtidigt som ett suffix läggs till hanteras av `SaveOptions`.

#### Steg 3: Konfigurera Save Options
`SaveOptions` låter dig behålla källfilens typ, specificera ett suffix och kontrollera minnesanvändning.  
```csharp
var saveOptions = new SaveOptions() 
{
    AddSuffix = true,                  // Adds a suffix like "2023-10-12" to indicate modification.
    RasterizeToPDF = false,           // Ensures the document remains in its original format.
    RedactedFileSuffix = DateTime.Now.ToShortDateString()
};
```  

#### Steg 4: Spara och output
Anropa `Save`‑metoden med de konfigurerade alternativen för att skriva den raderade filen till disk:  
```csharp
var outputFile = redactor.Save(saveOptions);
Console.WriteLine($"\nSource document was redacted successfully.\nFile saved to {outputFile}.\n");
```  

### Hur sparar man ett raderat dokument samtidigt som man bevarar dess originalformat?
Ladda källfilen med `new Redactor("source.pdf")`, applicera en eller flera raderingar, konfigurera `SaveOptions` för att behålla originalformatet och lägga till ett suffix (t.ex. “_redacted”), och anropa sedan `redactor.Save("output.pdf", saveOptions)`. Detta en‑stegs arbetsflöde garanterar att utdata behåller samma layout, typsnitt och metadata som indatafilen, medan det raderade innehållet tas bort permanent.

### Vanliga problem och lösningar
- **Dokumentet laddas inte** – Verifiera filsökvägen och säkerställ att processen har läsbehörighet.  
- **Radering misslyckas** – Dubbelkolla stavningen av den exakta frasen och skiftlägeskänsligheten; använd `IgnoreCase = true` om det behövs.  
- **Utdatafil korrupt** – Se till att `SaveOptions` matchar källformatet; felaktiga typer kan förstöra resultatet.

## Praktiska tillämpningar
GroupDocs.Redaction .NET utmärker sig i reglerade branscher:

1. **Legal Document Management** – Automatisk borttagning av kundnamn, personnummer eller ärendenummer innan kontrakt delas.  
2. **Healthcare Data Privacy** – Maskera patientidentifierare i medicinska journaler för att vara HIPAA‑kompatibel.  
3. **Financial Reporting** – Ta bort konfidentiella kontonummer från kvartalsrapporter innan distribution.

## Prestandaöverväganden
När du hanterar stora filer (hundratals megabyte), följ dessa bästa praxis:

- Använd koncisa sökmönster för att minska CPU‑cykler.  
- Frigör `Redactor`‑instanser omedelbart (`using`‑block) för att frigöra ohanterade resurser.  
- Använd `SaveOptions.Streaming = true` för att hålla minnesavtrycket lågt.

## Slutsats
Du har nu en komplett, produktionsklar metod för att **spara ett raderat dokument** i dess originalformat med hjälp av GroupDocs.Redaction för .NET. Genom att följa stegen ovan kan du integrera säker radering i vilket .NET‑arbetsflöde som helst, vilket säkerställer efterlevnad utan att kompromissa med dokumentets integritet.

Utforska avancerade funktioner som batch‑radering, anpassade raderingsformer och integration med molnlagring för att ytterligare utöka din lösning.

## Vanliga frågor

**Q: Vilka filtyper kan GroupDocs.Redaction hantera?**  
A: Över 30 format, inklusive PDF, DOCX, PPTX, XLSX och vanliga bildtyper som PNG och JPEG.

**Q: Är det möjligt att förhandsgranska raderingar innan sparning?**  
A: Ja – `Redactor`‑klassen tillhandahåller en `GetRedactions()`‑metod som returnerar en samling du kan rendera i ett UI.

**Q: Kan jag radera lösenordsskyddade dokument?**  
A: Absolut. Ange lösenordet när du konstruerar `Redactor`‑instansen för att låsa upp filen.

**Q: Stöder biblioteket .NET Core och .NET 5/6?**  
A: Ja – NuGet‑paketet är kompatibelt med .NET Framework 4.7.2+, .NET Core 3.1+ och .NET 5/6+.

**Q: Hur får jag en produktionslicens?**  
A: Köp en licens via GroupDocs‑webbplatsen; en tillfällig provlicens finns tillgänglig för utvärdering.

## Resurser
- **Dokumentation**: [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)
- **API Reference**: [API Reference](https://reference.groupdocs.com/redaction/net)
- **Nedladdning**: [GroupDocs Releases for .NET](https://releases.groupdocs.com/redaction/net/)
- **Gratis support**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)
- **Tillfällig licens**: [Get a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Senast uppdaterad:** 2026-07-06  
**Testad med:** GroupDocs.Redaction 2.0.0 for .NET  
**Författare:** GroupDocs

## Relaterade handledningar

- [Handledningar för dokumentlagring för GroupDocs.Redaction .NET](/redaction/net/document-saving/)
- [Säker dokumentradering i .NET med strömmar: En guide för GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)
- [Hur man sparar dokument som rasteriserade PDF‑filer med GroupDocs.Redaction för .NET: En komplett guide](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)