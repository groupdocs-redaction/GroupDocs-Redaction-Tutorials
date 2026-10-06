---
date: '2026-10-06'
description: Lär dig hur du maskerar data med GroupDocs.Redaction .NET och en IRedactionCallback-implementation
  i C#. Följ den här steg‑för‑steg‑guiden, bästa praxis och verkliga exempel.
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: Lär dig hur du maskerar data med GroupDocs.Redaction .NET och en IRedactionCallback-implementation
  i C#. Följ den här steg‑för‑steg‑guiden, bästa praxis och verkliga exempel.
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: Hur man maskerar data med GroupDocs.Redaction .NET (C#)
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: Hur man maskerar data med GroupDocs.Redaction .NET (C#)
type: docs
url: /sv/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# Så maskerar du data med GroupDocs.Redaction .NET (C#)

I den här omfattande handledningen kommer du att upptäcka **hur du maskerar data** från PDF‑filer, Word‑dokument och andra dokument med GroupDocs.Redaction för .NET. Oavsett om du behöver dölja personliga identifierare i juridiska kontrakt eller rensa konfidentiella siffror från finansiella rapporter, ger SDK:n dig programmatisk kontroll för att säkerställa att varje känsligt element försvinner permanent och kan auditera. Vi går igenom hur du installerar biblioteket, konfigurerar en anpassad `IRedactionCallback` och tillämpar exakta fras‑maskeringar med full loggning.

## Snabba svar
- **Vad gör IRedactionCallback?** Den låter dig avlyssna varje maskerings‑händelse, logga detaljer och valfritt modifiera ersättningstexten i realtid.  
- **Behöver jag en licens?** En provversion fungerar för utveckling; en permanent licens tar bort alla utvärderingsbegränsningar.  
- **Vilka .NET‑versioner stöds?** .NET Core 3.1+, .NET 5/6 och .NET Framework 4.6+.  
- **Kan jag bearbeta flera filer?** Ja — omslut logiken i en loop eller använd batch‑bearbetning för bästa prestanda.  
- **Är asynkron maskering möjlig?** Inte inbyggt, men du kan köra API‑anropen inom `Task.Run` eller andra asynkrona mönster.

## Vad är maskering av känslig data?
`Redaction` är den permanenta borttagningen eller dölja av information som inte får avslöjas. Med GroupDocs.Redaction definierar du exakta fraser, reguljära uttrycksmönster eller anpassade regler och ersätter dem med platshållare som **[REDACTED]** samtidigt som du bevarar originallayouten och pagineringen.

## Varför använda GroupDocs.Redaction med IRedactionCallback?
`IRedactionCallback` är ett gränssnitt som meddelar dig varje gång SDK:n maskerar ett innehåll, så att du kan fånga audit‑data eller justera ersättningen dynamiskt. Detta möjliggör full audit‑spårbarhet, anpassad affärsregel‑implementering och sömlös integration med efterlevnadssystem — utan att offra prestanda.

## Förutsättningar
- **GroupDocs.Redaction**‑biblioteket (kompatibel version – se den officiella [dokumentationssidan](https://docs.groupdocs.com/redaction/net/)). För fullständig information, se den [officiella dokumentationen](https://docs.groupdocs.com/redaction/net/).  
- .NET Core eller .NET Framework installerat på din utvecklingsmaskin.  
- Visual Studio (Community‑editionen räcker) eller någon IDE som stödjer C#.  
- Grundläggande kunskap i C# och bekantskap med NuGet‑pakethantering.

## Konfigurera GroupDocs.Redaction för .NET
Först, lägg till biblioteket i ditt projekt. Välj den metod du föredrar – CLI, Package Manager Console eller UI. Kommandona förblir exakt desamma som i den ursprungliga handledningen.

### Installationsalternativ
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- Öppna ditt projekt i Visual Studio.  
- Navigera till **Manage NuGet Packages**.  
- Sök efter **GroupDocs.Redaction** och installera den senaste stabila versionen.

### Licensanskaffning
För att prova produkten, begär en gratis provperiod eller en tillfällig licens från [här](https://purchase.groupdocs.com/temporary-license/). Du kan också skaffa en tillfällig licens från [temporary‑license‑sidan](https://purchase.groupdocs.com/temporary-license/). För produktionsbruk, köp en full licens för att låsa upp alla funktioner utan begränsningar.

#### Grundläggande initiering och konfiguration
Nedan är den minsta koden du behöver för att öppna ett dokument med `Redactor`‑klassen. Behåll detta kodsnutt oförändrat – det är grunden för allt som följer.  
`Redactor` är huvudklassen som representerar ett dokument och tillhandahåller metoder för att tillämpa maskeringsregler.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## Implementeringsguide
Nu kommer vi att utöka den grundläggande konfigurationen genom att lägga till en anpassad `IRedactionCallback`. Detta låter dig fånga varje maskerings‑händelse, skriva den till en logg eller till och med modifiera ersättningstexten i realtid.

### Anslut och använd en IRedactionCallback‑implementation
`IRedactionCallback` är ett gränssnitt som tar emot callbacks för varje maskeringsoperation, vilket gör att du kan logga eller ändra beteendet programmässigt.

#### Steg 1: förbered utmatningskatalog och källfilssökväg
Definiera var ditt källdokument finns. Anpassa sökvägen så att den matchar din miljö.

`LoadOptions` är ett konfigurationsobjekt som talar om för SDK:n hur filen ska läsas (t.ex. hantering av lösenord).  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### Steg 2: skapa en Redactor‑instans med anpassade inställningar
Vi instansierar `Redactor` med `LoadOptions` och `RedactorSettings`. `RedactionDump` i inställningarna kommer automatiskt att registrera varje maskering som sker.

`RedactorSettings` låter dig finjustera maskeringsprocessen; att skicka en `RedactionDump` aktiverar en detaljerad audit‑fil.  
`RedactionDump` är en hjälparklass som skriver varje maskerings‑händelse till en JSON‑formaterad dump för efterlevnadsrapportering.  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### Steg 3: tillämpa en exakt fras‑maskering
Här ersätter vi frasen **John Doe** med platshållaren **[REDACTED]**. Du kan byta ut vilken fras eller vilket mönster som helst som du behöver dölja.

`ReplacementOptions` definierar vilken text som ska ersätta det matchade innehållet. Den stödjer även anpassning av teckensnitt och färg om du behöver en visuell mask.  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**Förklaring av nyckelobjekten**
- `LoadOptions()` – talar om för SDK:n hur dokumentet ska läsas (t.ex. hantering av lösenord).
- `RedactorSettings(new RedactionDump())` – aktiverar en dump‑fil som loggar varje maskering för audit‑ändamål.
- `ReplacementOptions("[REDACTED]")` – definierar texten som kommer att ersätta den matchade frasen.

### Varför detta är viktigt
Callback‑mekanismen registrerar varje maskerings‑händelse, skapar ett maskinläsbart audit‑spår och låter dig modifiera platshållare dynamiskt, vilket hjälper till att uppfylla efterlevnadskrav och minskar manuellt efterbearbetningsarbete. Genom att integrera dessa data med dina övervakningssystem kan du generera rapporter, utlösa larm och säkerställa att ingen känslig information läcker genom maskerings‑pipeline:n.

Att använda `IRedactionCallback` ger dig tre konkreta fördelar:
1. **Compliance‑klara loggar** – varje maskering fångas i en maskinläsbar dump, vilket uppfyller audit‑krav för upp till 30 + regelverk.
2. **Dynamisk ersättning** – du kan ändra platshållaren baserat på datatypen, vilket minskar manuellt efterbearbetning med upp till 40 %.
3. **Skalbar prestanda** – callbacken lägger till försumbar overhead (<2 ms per maskering) samtidigt som du kan batch‑processa tusentals filer parallellt.

### Felsökningstips
- **Fil ej hittad:** Dubbelkolla `sourceFile`‑sökvägen och säkerställ att filen är åtkomlig för den körande processen.  
- **Callback avfyras inte:** Verifiera att din klass implementerar **alla** medlemmar i `IRedactionCallback` och att instansen korrekt skickas till `Redactor`.  
- **Prestandafördröjning:** För stora batcher, återanvänd samma `Redactor`‑instans när det är möjligt och disponera den omedelbart.

## Praktiska tillämpningar
Maskering av känslig data är användbart i många branscher:
1. **Juridisk dokumenthantering** – Automatisk borttagning av kundnamn, ärendenummer eller personnummer innan utkast delas.  
2. **HR‑hanteringssystem** – Ta bort personliga identifierare från anställningskontrakt under revisioner.  
3. **Finansiell rapportering** – Dölja proprietära siffror eller kontonummer när investerarinriktade PDF‑filer genereras.

## Prestandaöverväganden
GroupDocs.Redaction stödjer **30+ in‑ och utdataformat** (PDF, DOCX, PPTX, XLSX, HTML och bildtyper) och kan bearbeta filer med hundratals sidor utan att ladda hela dokumentet i minnet. För att hålla din applikation snabb när du hanterar dussintals eller hundratals filer:
- **Batch‑bearbetning:** Ladda en lista med filer och kör maskeringsloopen inom en `Parallel.ForEach` för multi‑core‑utnyttjande.  
- **Minneshantering:** Omslut varje `Redactor` i ett `using`‑block (som visat) för att garantera korrekt disponering.  
- **Asynkrona operationer:** Även om SDK:n är synkron kan du avlasta arbetet till bakgrundstrådar eller `Task.Run` för att undvika att UI‑trådar blockeras.

## Vanliga problem och lösningar

| Problem | Lösning |
|-------|----------|
| **“Invalid file format” fel** | Säkerställ att dokumenttypen stöds (PDF, DOCX, PPTX, etc.). |
| **Callback får null‑värden** | Kontrollera att du skickar en konkret implementation av `IRedactionCallback` när du konstruerar `RedactorSettings`. |
| **Maskering tillämpas inte** | Verifiera att den exakta frasen matchar dokumentets versal-/gemener och mellanslag, eller använd `RegexRedaction` för mönsterbaserad matchning. |

## Vanliga frågor

**Q: Vilka licensalternativ finns för GroupDocs.Redaction?**  
A: Du kan börja med en gratis provperiod eller begära en tillfällig licens för att utforska alla funktioner. För produktion, köp en evig eller prenumerationslicens.

**Q: Kan jag använda GroupDocs.Redaction på flera filtyper?**  
A: Ja, den stödjer PDF, Word, Excel, PowerPoint och många andra vanliga format.

**Q: Hur hanterar jag undantag under maskering?**  
A: Omslut din maskeringslogik i `try‑catch`‑block och logga undantagsdetaljerna. Callbacken kan också användas för att fånga fel i realtid.

**Q: Finns det inbyggt stöd för asynkron bearbetning?**  
A: Kärn‑API:n är synkron, men du kan köra maskeringsanrop inom asynkrona uppgifter eller bakgrundstjänster.

**Q: Var kan jag hitta mer avancerade exempel?**  
A: Den [officiella dokumentationen](https://docs.groupdocs.com/redaction/net/) och API‑referensen erbjuder omfattande kodexempel och scenarioguider.

## Resurser

- [GroupDocs.Redaction för .NET‑dokumentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction för .NET API‑referens](https://reference.groupdocs.com/redaction/net/)
- [Ladda ner GroupDocs.Redaction för .NET](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction‑forum](https://forum.groupdocs.com/c/redaction/33)
- [Gratis support](https://forum.groupdocs.com/)
- [Tillfällig licens](https://purchase.groupdocs.com/temporary-license/)

---

**Senast uppdaterad:** 2026-10-06  
**Testat med:** GroupDocs.Redaction 2.3 (senaste vid skrivande)  
**Författare:** GroupDocs

## Relaterade handledningar

- [Skapa maskeringspolicy med GroupDocs.Redaction .NET – Steg‑för‑steg‑guide](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [Hur man maskerar dokument med GroupDocs.Redaction .NET – En komplett guide](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Maskera dokument .net med Strömmar – GroupDocs.Redaction‑guide](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)