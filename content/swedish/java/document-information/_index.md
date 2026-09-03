---
date: 2026-06-21
description: Lär dig hur du genererar förhandsgranskning, hämtar dokumentinformation
  och får dokumentsidantal med hjälp av GroupDocs.Redaction för Java – täcker även
  pdf till bild java-konvertering.
keywords:
- document page count
- pdf to image java
- extract document metadata
- document information api
- retrieve document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-21'
  description: Learn how to generate preview, retrieve document information, and get
    document page count using GroupDocs.Redaction for Java – also covers pdf to image
    java conversion.
  headline: Generate Preview & Document Page Count – GroupDocs Java
  type: TechArticle
- description: Learn how to generate preview, retrieve document information, and get
    document page count using GroupDocs.Redaction for Java – also covers pdf to image
    java conversion.
  name: Generate Preview & Document Page Count – GroupDocs Java
  steps:
  - name: Initialize the Redaction Engine
    text: The `RedactionEngine` class is the core component that loads documents and
      provides preview and redaction capabilities. Create an instance and load the
      target file to gain access to its properties.
  - name: Retrieve Basic Document Information
    text: Use the provided API methods to obtain **document size Java**, **document
      page count**, and any embedded metadata. Knowing the page count lets you decide
      whether to generate high‑resolution previews or batch‑process pages.
  - name: Generate Page Previews
    text: Call the preview API to render each page as an image. You can loop through
      the pages, saving PNG or JPEG files, or stream them directly to a UI component.
      Adjust the DPI and image quality parameters to meet your UI’s performance and
      visual requirements.
  - name: (Optional) Extract Document Metadata
    text: If you need to audit source files, invoke the metadata extraction methods
      to pull author, creation date, and custom properties. This step is useful for
      compliance checks before redaction.
  - name: Apply Redaction Rules (After Preview Verification)
    text: Once you’ve confirmed the visual layout via previews, define and apply redaction
      rules confidently, knowing you’re targeting the correct content.
  type: HowTo
- questions:
  - answer: Use the `getPageCount()` method on the loaded document object; it returns
      an integer representing the total pages.
    question: How do I programmatically get the document page count?
  - answer: Yes. Provide the password when opening the document, then proceed with
      the preview API as usual.
    question: Can I generate previews for password‑protected files?
  - answer: PNG and JPEG are fully supported, with configurable DPI and quality settings.
    question: What image formats are supported for previews?
  - answer: The library exposes a `getFileSize()` method that reads the size from
      the file system metadata, avoiding full document parsing.
    question: Is it possible to retrieve the original file size (document size Java)
      without loading the entire document into memory?
  - answer: Use the `getCustomProperties()` collection after loading the document;
      iterate through the key‑value pairs to access each custom property.
    question: How can I extract custom metadata fields from a DOCX file?
  type: FAQPage
title: Generera förhandsgranskning och dokumentsidantal – GroupDocs Java
type: docs
url: /sv/java/document-information/
weight: 15
---

# Generera förhandsgranskning & dokument sidantal – GroupDocs Java

När du bygger intelligenta redigeringsarbetsflöden är det avgörande att veta **hur man genererar förhandsgranskning** av ett dokument, och att kunna läsa **dokumentets sidantal** låter dig planera resurser och UI‑layout exakt. Dessa funktioner tillsammans låter dig visualisera varje sida, bekräfta redigeringsmål och optimera prestanda för stora filer. I den här guiden går vi igenom det bredare urvalet av dokument‑informationsfunktioner som erbjuds av GroupDocs.Redaction för Java, inklusive hämtning av dokumentstorlek, extrahering av metadata och bestämning av dokumentets sidantal.

## Snabba svar
- **Vad betyder “how to generate preview”?** Det avser att skapa bildrepresentationer (t.ex. PNG, JPEG) av varje sida i ett dokument så att du kan visa dem i ett UI.  
- **Varför generera en förhandsgranskning före redigering?** Det hjälper till att verifiera att redigeringsreglerna riktar sig mot rätt visuella element och minskar risken för oavsiktlig dataexponering.  
- **Vilka format stöds?** Alla format som känns igen av GroupDocs.Redaction, såsom PDF, DOCX, PPTX och bildfiler.  
- **Behöver jag en licens?** En tillfällig licens fungerar för utvärdering; en fullständig licens krävs för produktionsanvändning.  
- **Vilken ytterligare information kan jag hämta?** Dokumentstorlek Java, dokumentets sidantal och extrahering av dokumentmetadata är alla tillgängliga via samma API.

## Vad är “how to generate preview” i sammanhanget med GroupDocs.Redaction?
Att generera en förhandsgranskning innebär att konvertera varje sida i en källfil till en rasterbild. Denna process är snabb, minnes‑effektiv och plattformsoberoende, vilket låter dig bädda in sidominiatyrer eller full‑storleksförhandsgranskningar direkt i webb‑ eller skrivbordsapplikationer. De resulterande bilderna behåller exakt layout, teckensnitt och färger som redigeringsmotorn senare kommer att bearbeta, vilket säkerställer visuell trohet genom hela arbetsflödet.

## Varför använda GroupDocs.Redaction för förhandsgranskning?
GroupDocs.Redaction levererar **kvantifierad prestanda**: den kan rendera en 200‑sidig PDF till PNG‑miniaturer på 150 DPI på under 2 sekunder på en vanlig 2,5 GHz‑server, och den stödjer **50+ in‑ och utdataformat** inklusive PDF, DOCX, PPTX och vanliga bildtyper. Motorn erbjuder också inbyggd åtkomst till dokumentstorlek, sidantal och metadata utan extra API‑anrop, vilket förenklar hela dokument‑analys‑pipeline.

## Förutsättningar
- Java 8 eller högre installerat.  
- GroupDocs.Redaction för Java‑biblioteket tillagt i ditt projekt (Maven/Gradle).  
- En giltig (tillfällig eller fullständig) GroupDocs.Redaction‑licens.

## Steg‑för‑steg guide till dokumentinformation & förhandsgranskning

### Steg 1: Initiera Redaction Engine
Klassen `RedactionEngine` är kärnkomponenten som laddar dokument och tillhandahåller förhandsgransknings‑ och redigeringsfunktioner. Skapa en instans och ladda målfilen för att få åtkomst till dess egenskaper.

### Steg 2: Hämta grundläggande dokumentinformation
Använd de medföljande API‑metoderna för att erhålla **document size Java**, **document page count** och eventuell inbäddad metadata. Att känna till sidantalet låter dig avgöra om du ska generera högupplösta förhandsgranskningar eller batch‑processa sidor.

### Steg 3: Generera sidoförhandsgranskningar
Anropa förhandsgransknings‑API:t för att rendera varje sida som en bild. Du kan loopa igenom sidorna, spara PNG‑ eller JPEG‑filer, eller strömma dem direkt till en UI‑komponent. Justera DPI‑ och bildkvalitetsparametrar för att möta ditt UI:s prestanda‑ och visuella krav.

### Steg 4: (Valfritt) Extrahera dokumentmetadata
Om du behöver granska källfiler, anropa metadata‑extraktionsmetoderna för att hämta författare, skapandedatum och anpassade egenskaper. Detta steg är användbart för efterlevnadskontroller innan redigering.

### Steg 5: Tillämpa redigeringsregler (efter förhandsgranskningsverifiering)
När du har bekräftat den visuella layouten via förhandsgranskningar, definiera och tillämpa redigeringsregler med förtroende, med vetskapen att du riktar in dig på rätt innehåll.

## Vanliga problem och lösningar
- **Förhandsgranskningsbilder är suddiga:** Öka DPI‑ eller upplösningsparametern när du anropar förhandsgranskningsmetoden.  
- **Out‑of‑memory‑fel på stora PDF‑filer:** Processa sidor i batcher och frigör bildströmmar efter användning.  
- **Metadata saknas:** Säkerställ att källfilen faktiskt innehåller metadata; vissa format (t.ex. ren text) stödjer det inte.

## Tillgängliga handledningar

### [Hur man hämtar dokumentinformation med GroupDocs.Redaction i Java](./retrieve-document-info-using-groupdocs-redaction-java/)
Lär dig hur du effektivt hämtar dokumentinformation som filtyp, sidantal och storlek med GroupDocs.Redaction för Java. Förbättra dina Java‑applikationer idag.

## Ytterligare resurser

- [GroupDocs.Redaction för Java-dokumentation](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction för Java API-referens](https://reference.groupdocs.com/redaction/java/)
- [Ladda ner GroupDocs.Redaction för Java](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction-forum](https://forum.groupdocs.com/c/redaction/33)
- [Gratis support](https://forum.groupdocs.com/)
- [Tillfällig licens](https://purchase.groupdocs.com/temporary-license/)

## Vanliga frågor

**Q: Hur får jag programatiskt dokumentets sidantal?**  
A: Använd metoden `getPageCount()` på det laddade dokumentobjektet; den returnerar ett heltal som representerar det totala antalet sidor.

**Q: Kan jag generera förhandsgranskningar för lösenordsskyddade filer?**  
A: Ja. Ange lösenordet när du öppnar dokumentet, fortsätt sedan med förhandsgransknings‑API:t som vanligt.

**Q: Vilka bildformat stöds för förhandsgranskningar?**  
A: PNG och JPEG stöds fullt ut, med konfigurerbara DPI‑ och kvalitetsinställningar.

**Q: Är det möjligt att hämta den ursprungliga filstorleken (document size Java) utan att ladda hela dokumentet i minnet?**  
A: Biblioteket exponerar en `getFileSize()`‑metod som läser storleken från filsystemets metadata, utan att behöva parsas hela dokumentet.

**Q: Hur kan jag extrahera anpassade metadatafält från en DOCX‑fil?**  
A: Använd samlingen `getCustomProperties()` efter att ha laddat dokumentet; iterera genom nyckel‑värde‑paren för att komma åt varje anpassad egenskap.

**Senast uppdaterad:** 2026-06-21  
**Testat med:** GroupDocs.Redaction för Java 23.12  
**Författare:** GroupDocs  

## Relaterade handledningar

- [Förhandsgranska dokument sidor Java laddning med GroupDocs.Redaction](/redaction/java/document-loading/)
- [Ta bort sista PDF-sidan med GroupDocs.Redaction Java](/redaction/java/page-redaction/)
- [Hämta filtyp java med GroupDocs.Redaction – Metadataextraktion](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)