---
date: '2026-08-09'
description: Lär dig hur du skapar icke redigerbara PDF‑filer genom att redacting
  text och rasterizing PDFs med GroupDocs.Redaction för Java.
keywords:
- create non editable pdf
- how to redact text java
- GroupDocs.Redaction Java
- rasterized PDF Java
- document security Java
lastmod: '2026-08-09'
og_description: Skapa icke redigerbara PDF‑filer genom att redacting text och rasterizing
  PDFs med GroupDocs.Redaction för Java. Följ en step‑by‑step guide med tips, pitfalls
  och FAQs.
og_image_alt: Guide showing how to redact text and generate a non‑editable rasterized
  PDF using GroupDocs.Redaction for Java
og_title: Skapa icke redigerbar PDF med GroupDocs.Redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to create non editable PDF files by redacting text and rasterizing
    PDFs using GroupDocs.Redaction for Java.
  headline: How to create non editable PDF with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to create non editable PDF files by redacting text and rasterizing
    PDFs using GroupDocs.Redaction for Java.
  name: How to create non editable PDF with GroupDocs.Redaction Java
  steps:
  - name: Import the required classes
    text: '`ExactPhraseRedaction` is a redaction rule that targets a literal string.
      `ReplacementOptions` tells the engine what placeholder to insert instead of
      the original text.'
  - name: Apply exact phrase redaction
    text: 'The following snippet replaces every occurrence of **“John Doe”** with
      the placeholder **[personal]**: **Why this works:** - `ExactPhraseRedaction`
      targets the literal string “John Doe”. - `ReplacementOptions` tells the engine
      what to insert instead of the original text. **Tips & common pitfalls** -'
  - name: Import `SaveOptions`
    text: '`SaveOptions` configures how the document is saved, including rasterization
      and file‑naming options.'
  - name: Configure and save the rasterized PDF
    text: The snippet below disables the automatic “_redacted” suffix, enables rasterization,
      and writes the output file. **Explanation:** - `setAddSuffix(false)` keeps the
      original file name (you can enable it to add “_redacted”). - `setRasterizeToPDF(true)`
      tells GroupDocs to render each page as an image in
  type: HowTo
- questions:
  - answer: It replaces a specific string (e.g., a name) with a placeholder, ensuring
      the original text cannot be recovered.
    question: What is an exact phrase redaction?
  - answer: Rasterized PDFs render each page as an image, preventing text selection,
      copying, or editing.
    question: How does rasterizing a PDF improve security?
  - answer: Yes—loop over a list of file paths, reusing the same `Redactor` configuration
      for each document.
    question: Can I process multiple files in one run?
  - answer: Absolutely. You can read/write streams from AWS S3, Azure Blob, or Google
      Cloud Storage and feed them directly to the API.
    question: Is cloud integration possible?
  - answer: Forgetting to close the `Redactor` (which locks files) and using an outdated
      library version that lacks rasterization support.
    question: What are typical pitfalls for newcomers?
  type: FAQPage
tags:
- create non editable pdf
- GroupDocs.Redaction
- Java document redaction
- rasterized PDF
- compliance
title: Hur man skapar icke redigerbar PDF med GroupDocs.Redaction Java
type: docs
url: /sv/java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/
weight: 1
---

# Hur man skapar icke redigerbar PDF med GroupDocs.Redaction Java

I många reglerade branscher måste du leverera dokument som inte kan ändras eller kopieras. Det mest pålitliga sättet att garantera detta är att **skapa icke redigerbara PDF**‑filer genom att först maskera känslig text och sedan rasterisera hela dokumentet. GroupDocs.Redaction for Java ger dig ett en‑radigt API för att utföra båda stegen, så att du kan uppfylla efterlevnadskrav utan att bygga en egen PDF‑motor.

## Snabba svar
- **Vad betyder “redact text”?** Det tar permanent bort eller maskerar känsliga strängar så att de inte kan läsas eller återställas.  
- **Vilket bibliotek hanterar uppgiften?** GroupDocs.Redaction for Java provides built‑in redaction and rasterization features.  
- **Behöver jag en licens?** En gratis provperiod fungerar för testning; en permanent licens krävs för produktion.  
- **Kan jag konvertera DOCX till en rasteriserad PDF i ett steg?** Ja – applicera redaction först, sedan använd `SaveOptions` med rasterisering aktiverad.  
- **Är resultatet verkligen icke‑redigerbart?** Rasteriserade PDF‑filer renderas som bilder, vilket förhindrar textutdragning eller modifiering.

## Vad är textredaction?
Textredaction tar permanent bort eller döljer konfidentiell information—såsom personliga identifierare, finansiella data eller juridiska klausuler—från ett dokument. Till skillnad från en enkel sök‑och‑ersätt‑funktion garanterar redaction att det dolda innehållet inte kan återställas av något verktyg. Genom att radera de ursprungliga tecknen och eventuellt ersätta dem med en platshållare säkerställer redaction att den känsliga datan är oåterkallelig och att dokumentet förblir läsbart för behöriga användare.

## Varför använda GroupDocs.Redaction för Java?
GroupDocs.Redaction for Java erbjuder en omfattande uppsättning funktioner som förenklar säker dokumentbehandling. Det stödjer ett brett spektrum av filformat, tillhandahåller flera redaction‑typer och inkluderar ett‑klicks rasterisering för att låsa PDF‑filer. Biblioteket är optimerat för prestanda, fungerar både på Windows och Linux, och integreras enkelt med befintliga Java‑applikationer, vilket gör det till ett pålitligt val för företag som behöver skydda känslig information i stor skala.

## Förutsättningar
- Java Development Kit (JDK 11 eller nyare) och en IDE såsom IntelliJ IDEA eller Eclipse.  
- GroupDocs.Redaction‑biblioteket (version 24.9 eller senare).  
- Grundläggande kunskaper i Java—du kommer bara att skriva några korta kodsnuttar.

## Konfigurera GroupDocs.Redaction för Java

### Maven‑installation
Lägg till GroupDocs‑arkivet och beroendet i din `pom.xml`:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### Direktnedladdning
Om Maven inte är ditt verktyg kan du hämta JAR‑filen från den officiella releasesidan: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### Licensanskaffning
- **Free trial** – utforska API:et utan kostnad.  
- **Temporary license** – idealisk för utökad testning.  
- **Full license** – krävs för produktionsdistributioner.

## Grundläggande initiering
`Redactor` är GroupDocs.Redaction:s kärnklass som laddar och modifierar ett dokument i minnet. Efter att du importerat namnutrymmet, skapa en instans av `Redactor` med sökvägen till din källfil, så är du redo att tillämpa redaction‑regler.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Implementeringsguide

## Hur man skapar icke redigerbar PDF i Java?
Läs in källdokumentet, tillämpa de önskade redaction‑reglerna och spara sedan resultatet med rasterisering aktiverad. Detta trestegsförlopp—läs in, redigera, rasterisera—producerar en PDF som inte kan redigeras, kopieras eller sökas i, vilket uppfyller de striktaste efterlevnadsstandarderna. Genom att konvertera varje sida till en bild eliminerar den slutliga filen eventuella dolda textlager som senare kan extraheras.

## Hur man redigerar text i Java
Nedan går vi igenom en exakt‑fras‑redaction, som är perfekt för att ta bort kända identifierare såsom en persons namn. Processen innebär att importera nödvändiga klasser, definiera en redaction‑regel och tillämpa den på dokumentet innan det sparas.

### Steg 1: Importera de nödvändiga klasserna
`ExactPhraseRedaction` är en redaction‑regel som riktar sig mot en exakt sträng. `ReplacementOptions` talar om för motorn vilken platshållare som ska infogas i stället för den ursprungliga texten.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### Steg 2: Tillämpa exakt fras‑redaction
Följande kodsnutt ersätter varje förekomst av **“John Doe”** med platshållaren **[personal]**:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
} finally { 
    redactor.close(); 
}
```

**Varför detta fungerar:**  
- `ExactPhraseRedaction` riktar sig mot den exakta strängen “John Doe”.  
- `ReplacementOptions` talar om för motorn vad som ska infogas i stället för den ursprungliga texten.

**Tips & vanliga fallgropar**  
- Dubbelkolla dokumentets sökväg; en felaktig sökväg utlöser ett `FileNotFoundException`.  
- Säkerställ att Java‑processen har skrivbehörighet för utdatamappen.

## Hur man sparar som rasteriserad PDF
Efter redaction vill du sannolikt ha en icke‑redigerbar PDF. Rasterisering konverterar varje sida till en bild, vilket tar bort möjligheten att markera eller redigera text. Detta steg säkerställer att den slutliga PDF‑filen beter sig som ett skannat dokument, vilket gör den motståndskraftig mot verktyg för textutdragning och oavsiktliga ändringar.

### Steg 1: Importera `SaveOptions`
`SaveOptions` konfigurerar hur dokumentet sparas, inklusive rasteriserings- och filnamnsalternativ.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
```

### Steg 2: Konfigurera och spara den rasteriserade PDF‑filen
Kodsnutten nedan inaktiverar det automatiska “_redacted”-suffixet, aktiverar rasterisering och skriver utdatafilen.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    SaveOptions tmp0 = new SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);

    redactor.save(tmp0);
} finally { 
    redactor.close(); 
}
```

**Förklaring:**  
- `setAddSuffix(false)` behåller det ursprungliga filnamnet (du kan aktivera det för att lägga till “_redacted”).  
- `setRasterizeToPDF(true)` talar om för GroupDocs att rendera varje sida som en bild i en PDF, vilket garanterar att dokumentet är **icke‑redigerbart**.

**Felsökning**  
- Om rasterisering misslyckas, verifiera att Java‑runtime innehåller PDF‑renderingsberoenden (de är med i biblioteket).

## Praktiska tillämpningar
1. **Juridisk dokumentbehandling** – maskera klientnamn innan delning med motpartens juridiska ombud.  
2. **HR‑registerhantering** – dölja anställdas ID‑nummer i interna rapporter.  
3. **Finansiell rapportering** – skydda kontonummer vid distribution av revisionssammanfattningar.  

Du kan kedja dessa steg i ett automatiserat arbetsflöde genom att länka GroupDocs.Redaction med ett dokumenthanteringssystem eller en molnlagringsbucket.

## Prestandaöverväganden
- **Batch processing:** Återanvänd en enda `Redactor`‑instans när du hanterar många filer för att minska overhead med upp till 40 %.  
- **Memory management:** För stora dokument, anropa `System.gc()` efter varje `redactor.close()` eller kör processen i en separat JVM.  
- **Keep dependencies updated:** Nya releaser innehåller ofta prestandaförbättringar för PDF‑rasterisering, inklusive en 20 % hastighetsökning för fler‑kärnorsystem.

## Vanliga problem och lösningar
| Problem | Lösning |
|-------|----------|
| *File not found* | Verifiera den absoluta sökvägen och säkerställ att filen finns på servern. |
| *Permission denied* | Kör JVM med tillräckliga OS‑behörigheter eller ändra ACL‑inställningarna för utdatamappen. |
| *Rasterization produces blank pages* | Bekräfta att källdokumentet inte redan är en rasterbild; använd den senaste versionen av biblioteket. |
| *Redaction leaves hidden text* | Använd `ExactPhraseRedaction` med `ReplacementOptions`; undvik enkla sök‑och‑ersätt‑metoder. |

## Vanliga frågor

**Q: Vad är en exakt fras‑redaction?**  
A: Den ersätter en specifik sträng (t.ex. ett namn) med en platshållare, vilket säkerställer att den ursprungliga texten inte kan återställas.

**Q: Hur förbättrar rasterisering av en PDF säkerheten?**  
A: Rasteriserade PDF‑filer renderar varje sida som en bild, vilket förhindrar textmarkering, kopiering eller redigering.

**Q: Kan jag bearbeta flera filer i ett kör?**  
A: Ja – loopa över en lista med filsökvägar och återanvänd samma `Redactor`‑konfiguration för varje dokument.

**Q: Är molnintegration möjlig?**  
A: Absolut. Du kan läsa/skriva strömmar från AWS S3, Azure Blob eller Google Cloud Storage och skicka dem direkt till API:et.

**Q: Vilka är vanliga fallgropar för nybörjare?**  
A: Att glömma att stänga `Redactor` (vilket låser filer) och att använda en föråldrad biblioteksversion som saknar rasteriseringsstöd.

## Resurser
- **Documentation:** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API‑referens:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **Nedladdning:** [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub:** [GroupDocs.Redaction GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Gratis support:** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Tillfällig licens:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Senast uppdaterad:** 2026-08-09  
**Testad med:** GroupDocs.Redaction 24.9 for Java  
**Författare:** GroupDocs  

## Relaterade handledningar

- [Hur man skapar gråskala‑pdf med GroupDocs.Redaction Java – Säker och optimera dina dokument](/redaction/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/)
- [Behärska dokumentssäkerhet i Java: Exakt fras‑redaction och avancerad rasterisering med GroupDocs.Redaction](/redaction/java/advanced-redaction/groupdocs-redaction-java-document-security/)
- [Hur man konverterar DOCX till bild & maskerar Word‑dokument med GroupDocs Redaction Java](/redaction/java/document-saving/groupdocs-redaction-java-rasterize-word-docs/)