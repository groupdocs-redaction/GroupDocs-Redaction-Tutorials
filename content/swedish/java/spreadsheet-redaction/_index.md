---
date: 2026-08-04
description: Lär dig hur du filtrerar kalkylbladsdata java och säkert raderar kolumner
  eller celler i Excel-kalkylblad med hjälp av GroupDocs.Redaction för Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Lär dig hur du filtrerar kalkylbladsdata java och säkert raderar kolumner
  eller celler i Excel-kalkylblad med hjälp av GroupDocs.Redaction för Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Filtrera kalkylbladsdata java – guide med GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Filtrera kalkylbladsdata java – guide med GroupDocs.Redaction
type: docs
url: /sv/java/spreadsheet-redaction/
weight: 12
---

# Filtrera kalkylbladsdata java – GroupDocs.Redaction Java-handledning

Om du behöver **filtrera kalkylbladsdata java** innan du tillämpar maskning, har du hamnat på rätt guide. I den här handledningen kommer du att upptäcka hur du isolerar rader, kolumner eller enskilda celler som innehåller personlig eller konfidentiell information, och sedan maskar dem säkert med GroupDocs.Redaction for Java. Stegen förklaras på ett enkelt språk, innehåller bästa praxis‑tips och visar hur du håller bearbetningen snabb även på stora arbetsböcker.

## Snabba svar
- **Vilket bibliotek hanterar kalkylbladsmaskning i Java?** GroupDocs.Redaction for Java.  
- **Kan jag filtrera rader utan att ladda hela filen i minnet?** Ja – API:et strömmar data och låter dig tillämpa filter i realtid.  
- **Vilka filformat stöds?** Över 30 kalkylbladsformat, inklusive XLS, XLSX, CSV och ODS.  
- **Behöver jag en licens för utveckling?** En tillfällig licens fungerar för testning; en full licens krävs för produktion.  
- **Finns det en gräns för arbetsbokens storlek?** Motorn kan bearbeta filer upp till 500 MB utan överdriven minnesanvändning.

## Vad är filtrering av kalkylbladsdata java?
**Filtrera kalkylbladsdata java** är processen att programatiskt välja specifika rader, kolumner eller celler i en Excel‑liknande arbetsbok med Java‑kod så att endast målrettat innehåll granskas eller maskas. Denna teknik minskar körtiden, begränsar onödiga ändringar och hjälper till att uppfylla GDPR‑liknande efterlevnad.

## Varför filtrera kalkylbladsdata java?
GroupDocs.Redaction Java stöder **30+ kalkylbladsformat** och kan bearbeta arbetsböcker som innehåller **upp till 500 MB** (ungefär 1 miljon rader) samtidigt som minnesanvändningen hålls under **200 MB**. Genom att filtrera först undviker du att röra orelaterad data, vilket minskar behandlingstiden med **40‑60 %** i genomsnitt för typiska scenarier för integritetssanering.

## Förutsättningar
- Java 17 eller senare installerat.  
- Maven- eller Gradle‑byggsystem.  
- GroupDocs.Redaction for Java (nedladdningsbar från den officiella webbplatsen).  
- En tillfällig eller full licensnyckel.  

## Hur filtrerar man data i kalkylblad med GroupDocs.Redaction Java?
Läs in arbetsboken, definiera ett filter som matchar de celler du vill maska, och tillämpa sedan maskningsoperationen. API:et utför filtret i ett strömningsläge, så du behöver aldrig hålla hela filen i RAM.

`RedactionFilter`‑klassen låter dig ange kolumnindex, radintervall eller anpassade predikat. Till exempel kan du rikta in dig på varje cell i kolumn **B** som innehåller ett e‑postadressmönster, eller du kan begränsa maskning till rader där en “Status”-kolumn är lika med “Confidential”.

**Direkt svar (40‑70 ord):**  
Skapa en `RedactionFilter`‑instans, ange kolumnindex och ett reguljärt uttryck‑villkor, och skicka sedan filtret till `Redactor.redact(workbook, filter)`. Detta enradiga filter isolerar exakt de celler som matchar dina kriterier, och maskningsverktyget tar bort eller maskar dem medan resten av bladet förblir orört. Operationen slutförs i linjär tid i förhållande till de filtrerade raderna.

### Steg 1: skapa filtret
`RedactionFilter` är kärnklassen som representerar en filtreringsregel för kalkylbladsmaskning. Den accepterar kolumnnummer, radnummer eller anpassade lambda‑uttryck för att exakt identifiera data.

### Steg 2: konfigurera villkoret
Använd `filter.setColumnIndex(1)` för att rikta in dig på kolumn B (nollbaserad) och `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` för att matcha e‑postmönster. Du kan också kombinera flera villkor med `filter.and(...)` eller `filter.or(...)`.

### Steg 3: tillämpa maskning
`Redactor` är huvudklassen som utför maskningsoperationer på en arbetsbok.  
Skicka arbetsboken och det konfigurerade filtret till `Redactor`‑objektet. API:et strömmar arbetsboken, tillämpar filtret och skriver det maskade resultatet till en ny fil, samtidigt som originalformat och formler bevaras.

## Vanliga problem och lösningar
- **Filtret matchar inga celler:** Verifiera kolumnindex (nollbaserad) och säkerställ att syntaxen för reguljärt uttryck är korrekt för Java.  
- **Out‑of‑memory‑fel på stora filer:** Öka JVM‑heap‑storleken något (t.ex. `-Xmx1g`) eller dela upp arbetsboken i mindre delar innan filtrering.  
- **Maskat resultat förlorar formatering:** `RedactionOptions` låter dig anpassa maskningsbeteendet, exempelvis bevara cellformatering. Använd `RedactionOptions.setPreserveFormatting(true)` för att behålla cellstilar intakta.

## Varför filtrera kalkylbladsdata?
Filtrering före maskning isolerar endast de känsliga delarna av en arbetsbok, vilket innebär att du undviker onödiga ändringar av ren data. Detta selektiva tillvägagångssätt minskar också risken för oavsiktlig dataförlust och påskyndar efterlevnadsgranskningar eftersom revisionsloggen innehåller betydligt färre poster.

## Hur man maskar e‑post i Excel‑kalkylblad med GroupDocs.Redaction Java API
Läs in din Excel‑fil, tillämpa ett filter som söker efter det vanliga e‑postmönstret, och anropa maskningsverktyget. API:et ersätter varje matchad e‑post med en platshållare som exempelvis “***@***.com” samtidigt som den omgivande celllayouten bevaras.

## Hur man filtrerar data – tillgängliga handledningar
- [How to Redact Emails in Excel Spreadsheets Using GroupDocs.Redaction Java API](./redact-emails-excel-groupdocs-redaction-java/)

## Ytterligare resurser

- [GroupDocs.Redaction for Java Documentation](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API Reference](https://reference.groupdocs.com/redaction/java/)
- [Download GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Senast uppdaterad:** 2026-08-04  
**Testad med:** GroupDocs.Redaction 23.11 for Java  
**Författare:** GroupDocs  

## Vanliga frågor

**Q: Kan jag filtrera flera kolumner samtidigt?**  
A: Ja, du kan lägga till ytterligare kolumnindex till samma `RedactionFilter`‑instans eller kedja flera filter med `filter.or(...)`.

**Q: Fungerar filtret på lösenordsskyddade arbetsböcker?**  
A: Ange lösenordet när du öppnar arbetsboken; filtret körs efter avkodning precis som på en oskyddad fil.

**Q: Hur många rader kan API:et hantera i en enda operation?**  
A: Motorn är optimerad för upp till 1 miljon rader (≈500 MB) utan att ladda hela filen i minnet.

**Q: Är det möjligt att förhandsgranska vilka celler som kommer att maskas innan sparning?**  
A: Ja, anropa `filter.preview(workbook)` för att få en lista över celladresser som matchar kriterierna.

**Q: Vilken licensmodell krävs för produktionsanvändning?**  
A: En full kommersiell licens krävs för produktionsdistributioner; en tillfällig licens räcker för testning och utvärdering.

## Relaterade handledningar

- [How to Redact Sensitive Data in Excel Spreadsheets Using GroupDocs.Redaction Java API](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Mask Sensitive Data Java – GroupDocs.Redaction Guide](/redaction/java/getting-started/)
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)