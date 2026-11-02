---
date: '2026-11-02'
description: Lär dig hur du lägger till suffix till filnamn i en GroupDocs redaction
  Java‑handledning med Maven, streaming load, annotation deletion och save options.
keywords:
- groupdocs redaction java tutorial
- add suffix filename java
- document redaction workflow
- groupdocs maven dependency
- java inputstream redaction
lastmod: '2026-11-02'
og_description: Lär dig hur du lägger till suffix till filnamn i en GroupDocs redaction
  Java‑handledning. Följ step‑by‑step Maven setup, streaming load och save options.
og_image_alt: Guide showing Java code to add suffix to redacted filenames using GroupDocs
  Redaction
og_title: Hur du lägger till suffix till filnamn i GroupDocs redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  headline: How to add suffix to filename in GroupDocs redaction Java
  type: TechArticle
- description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  name: How to add suffix to filename in GroupDocs redaction Java
  steps:
  - name: '1: Create InputStream'
    text: '- **Why:** Using `InputStream` allows you to handle documents stored in
      various locations—cloud buckets, databases, or in‑memory buffers—without first
      writing them to disk. This approach is essential when you need to **load document
      from stream** in micro‑service architectures.'
  - name: '1: Apply DeleteAnnotationRedaction'
    text: '- **Why:** This step ensures that any sensitive annotations (comments,
      highlights, or hidden notes) are stripped from the document, enhancing privacy
      and compliance.'
  - name: '1: Configure SaveOptions'
    text: '- **Why:** Customizing save options allows flexible output formats and
      naming conventions. Enabling `setAddSuffix(true)` **adds suffix to filename**,
      making it clear that the file has been redacted.'
  type: HowTo
- questions:
  - answer: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.
    question: Can I redact PDF documents using GroupDocs.Redaction?
  - answer: Use streaming (`load document from stream`) and close resources promptly
      to keep memory usage low.
    question: What is the best way to handle large files with GroupDocs.Redaction?
  - answer: The API automatically adds a default suffix (e.g., “_redacted”). For custom
      suffixes, rename the output file after saving.
    question: Is it possible to customize the suffix text?
  - answer: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/)
      and follow the instructions.
    question: How do I obtain a temporary license for GroupDocs.Redaction?
  - answer: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for expert assistance.
    question: Where can I get help if I encounter issues?
  type: FAQPage
tags:
- groupdocs redaction
- java tutorial
- maven dependency
- document redaction
title: Hur du lägger till suffix till filnamn i GroupDocs redaction Java
type: docs
url: /sv/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Hur man lägger till suffix till filnamn i GroupDocs redaction Java

I den här **groupdocs redaction java tutorial** lär du dig hur du automatiskt lägger till ett suffix till utdatafilens namn när du maskar dokument med GroupDocs.Redaction. Att lägga till ett suffix eliminerar manuell namnändring, minskar risken för att o‑maskade filer läcker, och passar smidigt in i CI/CD‑pipelines som förlitar sig på namngivningskonventioner. Guiden går igenom Maven‑setup, streaming‑inläsning av dokument, borttagning av annotationer och konfiguration av sparalternativ — allt med koncis, produktionsklar kod.

## Snabba svar
- **Vad gör “add suffix to filename”?**  
  När du aktiverar suffix‑alternativet lägger SDK automatiskt till en fördefinierad sträng (standard “_redacted”) till basnamnet på utdatafilen före filändelsen. Detta gör det omedelbart tydligt vilka filer som har bearbetats, hjälper till att förhindra oavsiktlig distribution av originalinnehåll och förenklar efterföljande automatisering som förlitar sig på namnmönster.  
- **Kan jag läsa in ett dokument från en ström?**  
  Ja—GroupDocs.Redaction stödjer inläsning från vilken `InputStream` som helst, perfekt för molnlagring eller in‑minnesbearbetning.  
- **Behöver jag en licens för den här funktionen?**  
  En gratis provperiod fungerar för grundläggande maskning; en tillfällig eller full licens låser upp alla avancerade alternativ, inklusive hantering av suffix.  
- **Vilka format stöds?**  
  Biblioteket hanterar DOCX, PDF, PPTX, XLSX och många fler.  
- **Krävs rasterisering för PDF‑utdata?**  
  Rasterisering är valfri; aktivera den när du behöver platta till dokumentet för extra säkerhet.

## Vad gör “add suffix to filename”?

När du aktiverar suffix‑alternativet lägger SDK automatiskt till en fördefinierad sträng (standard “_redacted”) till basnamnet på utdatafilen före filändelsen. Detta gör det omedelbart tydligt vilka filer som har bearbetats, hjälper till att förhindra oavsiktlig distribution av originalinnehåll och förenklar efterföljande automatisering som förlitar sig på namnmönster.

## Varför använda GroupDocs.Redaction för denna uppgift?

GroupDocs.Redaction erbjuder ett högpresterande Java‑API som kombinerar maskningsåtgärder med flexibla filhanteringsalternativ såsom automatisk suffix‑tillägg, streaming‑stöd och batch‑bearbetning. Det stödjer över 50 in‑ och utdataformat och kan bearbeta dokument med hundratals sidor utan att läsa in hela filen i minnet, vilket säkerställer låg minnesanvändning och snabb körning.

## Förutsättningar

- **Java Development Kit (JDK):** Version 8 eller högre.  
- **GroupDocs.Redaction Library:** Kärnbibliotek för maskningsuppgifter.  
- **IDE:** IntelliJ IDEA, Eclipse eller någon Java‑kompatibel editor.  
- **Maven:** För beroendehantering.  

### Kunskapsförutsättningar
Bekantskap med Java I/O och grundläggande objektorienterade koncept gör exemplen enklare att följa.

## Installera GroupDocs.Redaction för Java

### Maven‑setup
Inkludera följande konfiguration i din `pom.xml`‑fil för att komma åt GroupDocs‑bibliotek via Maven:

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
Alternativt, ladda ner den senaste versionen direkt från [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Licensförvärv
1. **Free trial:** Få åtkomst till grundfunktionalitet utan begränsningar.  
2. **Temporary license:** Skaffa en tillfällig licens för att utforska avancerade funktioner.  
3. **Purchase:** För långsiktig användning, överväg att köpa en full licens.

#### Grundläggande initiering och setup
Initiera ditt projekt genom att lägga till nödvändiga importeringar:

```java
import com.groupdocs.redaction.Redactor;
```

Med denna setup är du redo att implementera dokumentmaskningsfunktioner.

## Implementeringsguide

### Funktion 1: läsa in dokument från ström
**Översikt:** Lär dig hur du läser in dokument i en `InputStream` för bearbetning.

`InputStream` är en Java I/O‑klass som representerar en byte‑ström, vilket låter dig läsa data från filer, nätverksanslutningar eller andra källor utan att läsa in hela innehållet i minnet.

#### Steg 1.1: skapa inputstream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Varför:** Att använda `InputStream` låter dig hantera dokument lagrade på olika platser — molnbuckets, databaser eller in‑minnesbuffertar — utan att först skriva dem till disk. Detta tillvägagångssätt är avgörande när du behöver **load document from stream** i mikrotjänstarkitekturer.

### Funktion 2: tillämpa annotation deletion redaction
**Översikt:** Ta bort annotationer från ditt dokument med `DeleteAnnotationRedaction`.

`DeleteAnnotationRedaction` är en maskningsoperation som tar bort alla annotationer — såsom kommentarer, markeringar och anteckningar — från dokumentet.

#### Steg 2.1: tillämpa deleteannotationredaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Varför:** Detta steg säkerställer att alla känsliga annotationer (kommentarer, markeringar eller dolda anteckningar) tas bort från dokumentet, vilket förbättrar sekretess och efterlevnad.

### Funktion 3: spara dokument med alternativ
**Översikt:** Lär dig hur du sparar ditt bearbetade dokument med specifika alternativ som rasterisering och **add suffix filename java**.

`SaveOptions` kapslar in inställningar som styr hur det maskade dokumentet skrivs, inklusive format, rasterisering och namngivningskonventioner.

#### Steg 3.1: konfigurera saveoptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Varför:** Anpassning av sparalternativ möjliggör flexibla utdataformat och namngivningskonventioner. Att aktivera `setAddSuffix(true)` **adds suffix to filename**, vilket gör det tydligt att filen har maskats.

## Hur man lägger till suffix filnamn java när man sparar ett dokument?

`Redactor`‑klassen är kärnkomponenten som läser in ett dokument och tillämpar maskningsoperationer. `SaveOptions` definierar hur det maskade dokumentet sparas, inklusive format, rasterisering och namngivningskonventioner. Skapa en `Redactor`‑instans, tillämpa eventuella nödvändiga maskningar, och konfigurera sedan ett `SaveOptions`‑objekt med `setAddSuffix(true)`. Anropa `redactor.save(outputPath, options)`. SDK:n lägger automatiskt till “_redacted” (eller den konfigurerade suffixen) till filnamnet, så du aldrig behöver byta namn på filen manuellt.

## Översikt av GroupDocs Maven‑beroende

**groupdocs maven dependency** för in hela Redaction‑SDK:n i ditt projekt med ett enda `<dependency>`‑element. Det hanterar transitiva beroenden, håller biblioteken uppdaterade och förenklar byggautomatisering. Genom att deklarera beroendet i `pom.xml` undviker du manuell JAR‑hantering och säkerställer kompatibilitet med de senaste säkerhetsuppdateringarna.

## Varför det är viktigt att lägga till ett suffix

Att lägga till ett suffix ger omedelbar visuell bekräftelse på att en fil har bearbetats, vilket är kritiskt för revisionsspår, automatiserade arbetsflöden och regulatorisk efterlevnad. Det låter skript filtrera maskade filer, förhindrar oavsiktlig distribution av originalinnehåll och uppfyller många branschstandarder som kräver tydlig märkning av sanerade dokument.

## Praktiska tillämpningar

Utforska dessa verkliga användningsfall:

1. **Legal document redaction:** Säkerställ kontrakt innan delning med klient.  
2. **Medical record handling:** Skydda patientidentifierare samtidigt som kliniska data bevaras.  
3. **Financial reporting:** Håll känsliga siffror konfidentiella under externa revisioner.  
4. **CRM integration:** Automatisk maskning av kunddata innan export till tredjepartsverktyg.  
5. **Collaboration tools:** Säkerställ att delade utkast aldrig avslöjar dolda kommentarer eller metadata.

## Prestandaöverväganden

### Optimera prestanda
- Använd streaming (`load document from stream`) för att undvika att läsa in hela filer i minnet.  
- Stäng `Redactor`‑instanser omedelbart för att frigöra resurser.  

### Riktlinjer för resursanvändning
- Övervaka CPU och minne under batchkörningar.  
- Föredra `ByteArrayOutputStream` för in‑minneslagring när du arbetar med måttliga filstorlekar.  

### Bästa praxis för Java‑minneshantering
- Återanvänd `Redactor`‑objekt när du bearbetar flera filer av samma typ.  
- Anropa `close()` i ett `try‑with‑resources`‑block för att förhindra läckor.

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|-------|-------|-----|
| **Suffix visas inte** | `setAddSuffix(false)` eller saknad anrop | Se till att `options.setAddSuffix(true)` är satt innan `save()`. |
| **OutOfMemoryError på stor DOCX** | Läser in hela filen i minnet | Byt till `InputStream`‑inläsning (se Funktion 1). |
| **Annotationer fortfarande synliga** | Maskning inte tillämpad före sparning | Anropa `redactor.apply(new DeleteAnnotationRedaction())` innan `save()`. |
| **PDF‑rasterisering inte tillämpad** | `setRasterizeToPDF(false)` eller utelämnad | Sätt `options.setRasterizeToPDF(true)` när du behöver en platt PDF. |

## Vanliga frågor

**Q: Kan jag maska PDF‑dokument med GroupDocs.Redaction?**  
A: Ja, biblioteket stödjer PDF, DOCX, PPTX, XLSX och många andra format.

**Q: Vad är det bästa sättet att hantera stora filer med GroupDocs.Redaction?**  
A: Använd streaming (`load document from stream`) och stäng resurser omedelbart för att hålla minnesanvändningen låg.

**Q: Är det möjligt att anpassa suffix‑texten?**  
A: API:n lägger automatiskt till ett standardsuffix (t.ex. “_redacted”). För anpassade suffix, byt namn på utdatafilen efter sparning.

**Q: Hur får jag en tillfällig licens för GroupDocs.Redaction?**  
A: Besök [Temporary License page](https://purchase.groupdocs.com/temporary-license/) och följ instruktionerna.

**Q: Var kan jag få hjälp om jag stöter på problem?**  
A: Gå med i [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) för experthjälp.

## Resurser
- **Documentation:** Utforska detaljerade guider på [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API reference:** Få tillgång till omfattande API‑detaljer på [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Hämta den senaste versionen från [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub repository:** Bidra eller utforska källkoden på [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Senast uppdaterad:** 2026-11-02  
**Testad med:** GroupDocs.Redaction 24.9 for Java  
**Författare:** GroupDocs  

## Relaterade handledningar

- [Konvertera Word till PDF och spara maskerade dokument med GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Förhandsgranska dokumentsidor Java‑inläsning med GroupDocs.Redaction](/redaction/java/document-loading/)
- [Avancerade maskningstekniker för GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)