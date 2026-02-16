---
date: '2026-02-16'
description: Lär dig hur du använder GroupDocs Maven‑beroendet för att lägga till
  ett suffix på filnamn när du maskar dokument i Java. Inkluderar inläsning från ström,
  borttagning av annotationer och sparalternativ.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: groupdocs Maven-beroende – Lägg till suffix till filnamn i Java
type: docs
url: /sv/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Hur man lägger till suffix till filnamn när man maskerar dokument i Java med GroupDocs.Redaction

Att maskera konfidentiella data är bara halva striden—du måste också se till att den sparade filen tydligt visar att den har behandlats. **Att använda groupdocs maven‑beroendet gör detta enkelt**, så att du kan lägga till ett suffix till utdatafilens namn på bara några rader kod. I den här guiden lär du dig hur du lägger till suffix till filnamn när du sparar ett maskerat dokument, samt hur du laddar, annoterar och sparar med GroupDocs.Redaction för Java. Oavsett om du skyddar juridiska kontrakt, medicinska journaler eller finansiella rapporter, kommer dessa steg att hålla ditt arbetsflöde både säkert och spårbart.

## Quick Answers
- **Vad gör “add suffix to filename”?**  
  Det lägger till ett anpassat suffix (t.ex. “_redacted”) till utdatafilens namn så att du omedelbart kan identifiera bearbetade filer.  
- **Kan jag ladda ett dokument från en ström?**  
  Ja—GroupDocs.Redaction stödjer laddning från vilken `InputStream` som helst, perfekt för molnlagring eller in‑minnesbearbetning.  
- **Behöver jag en licens för den här funktionen?**  
  En gratis provperiod fungerar för grundläggande maskering; en tillfällig eller full licens låser upp alla avancerade alternativ, inklusive hantering av suffix.  
- **Vilka format stöds?**  
  Biblioteket hanterar DOCX, PDF, PPTX, XLSX och många fler.  
- **Krävs rasterisering för PDF‑utdata?**  
  Rasterisering är valfri; aktivera den när du behöver platta till dokumentet för extra säkerhet.

## Vad är att lägga till ett suffix till ett filnamn?
Att lägga till ett suffix är en enkel namngivningskonvention som signalerar att en fil har genomgått maskering. Det förhindrar oavsiktlig delning av original, omaskerade versioner och hjälper automatiserade pipelines att spåra bearbetningsstatus.

## Varför använda GroupDocs.Redaction för denna uppgift?
GroupDocs.Redaction erbjuder ett flytande Java‑API som låter dig kombinera maskeringsåtgärder med filhanteringsalternativ—som **att lägga till ett suffix till filnamnet**—på bara några rader kod. Detta sparar utvecklingstid och minskar risken för manuella fel.

## Prerequisites
- **Java Development Kit (JDK):** Version 8 eller högre.  
- **GroupDocs.Redaction Library:** Kärnbibliotek för maskeringsuppgifter.  
- **IDE:** IntelliJ IDEA, Eclipse eller någon Java‑kompatibel editor.  
- **Maven:** För beroendehantering.  

### Knowledge Prerequisites
Bekantskap med Java I/O och grundläggande objektorienterade koncept gör exemplen enklare att följa.

## Setting Up GroupDocs.Redaction for Java
### Maven Setup
Inkludera följande konfiguration i din `pom.xml`‑fil för att få åtkomst till GroupDocs‑biblioteken via Maven:

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

### Direct Download
Alternativt, ladda ner den senaste versionen direkt från [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License Acquisition
1. **Free Trial:** Åtkomst till grundläggande funktionalitet utan begränsningar.  
2. **Temporary License:** Skaffa en tillfällig licens för att utforska avancerade funktioner.  
3. **Purchase:** För långsiktig användning, överväg att köpa en full licens.

#### Basic Initialization and Setup
Initiera ditt projekt genom att lägga till nödvändiga importeringar:

```java
import com.groupdocs.redaction.Redactor;
```

Med den här konfigurationen är du redo att implementera funktioner för dokumentmaskering.

## Implementation Guide

### Feature 1: Load Document from Stream
**Översikt:** Lär dig hur du laddar dokument i en `InputStream` för bearbetning.

#### Step-by-Step Implementation
##### Step 1.1: Create InputStream

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

- **Varför:** Att använda `InputStream` låter dig hantera dokument lagrade i olika format sömlöst, vilket är viktigt när du behöver **ladda dokument från en ström** i moln‑ eller mikrotjänstscenario.

### Feature 2: Apply Annotation Deletion Redaction
**Översikt:** Ta bort annotationer från ditt dokument med `DeleteAnnotationRedaction`.

#### Step-by-Step Implementation
##### Step 2.1: Apply DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Varför:** Detta steg säkerställer att känsliga annotationer tas bort, vilket förbättrar dokumentets sekretess.

### Feature 3: Save Document with Options
**Översikt:** Lär dig hur du sparar ditt bearbetade dokument med specifika alternativ som rasterisering och **att lägga till ett suffix till filnamnet**.

#### Step-by-Step Implementation
##### Step 3.1: Configure SaveOptions

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

- **Varför:** Anpassning av sparalternativ möjliggör flexibla utdataformat och namngivningskonventioner. Att aktivera `setAddSuffix(true)` **lägger till suffix till filnamnet**, vilket tydligt visar att filen har maskerats.

## groupdocs maven dependency Overview
**groupdocs maven dependency** för in hela Redaction‑SDK:n i ditt projekt med ett enda `<dependency>`‑element. Det hanterar transitiva beroenden, håller biblioteken uppdaterade och förenklar byggautomatisering. Genom att deklarera beroendet i `pom.xml` undviker du manuell JAR‑hantering och säkerställer kompatibilitet med de senaste säkerhetsuppdateringarna.

## Why Adding a Suffix Matters
- **Auditability:** Team kan omedelbart identifiera vilka filer som är säkra att distribuera.  
- **Automation:** Skript kan filtrera filer efter suffix, vilket förhindrar oavsiktlig bearbetning av originaldokument.  
- **Compliance:** Många regelverk kräver tydlig märkning av sanerade dokument.  

## Practical Applications
Utforska dessa verkliga användningsfall:
1. **Legal Document Redaction:** Säkerställ kontrakt innan de delas med klienten.  
2. **Medical Record Handling:** Skydda patientidentifierare.  
3. **Financial Reporting:** Håll känsliga siffror konfidentiella.  
4. **CRM Integration:** Maskera automatiskt kunddata före export.  
5. **Collaboration Tools:** Säkerställ att delade utkast aldrig avslöjar dolda kommentarer.

## Performance Considerations
### Optimizing Performance
- Använd streaming (`load document from stream`) för att undvika att ladda hela filer i minnet.  
- Stäng `Redactor`‑instanser omedelbart för att frigöra resurser.

### Resource Usage Guidelines
- Övervaka CPU och minne under batchkörningar.  
- Föredra `ByteArrayOutputStream` för in‑memory‑sparningar när du arbetar med måttliga filstorlekar.

### Best Practices for Java Memory Management
- Återanvänd `Redactor`‑objekt när du bearbetar flera filer av samma typ.  
- Anropa `close()` i ett `try‑with‑resources`‑block för att förhindra läckor.

## Common Issues and Solutions
| Problem | Orsak | Lösning |
|-------|-------|-----|
| **Suffix visas inte** | `setAddSuffix(false)` eller saknad anrop | Se till att `options.setAddSuffix(true)` är satt innan `save()`. |
| **OutOfMemoryError på stor DOCX** | Laddar hela filen i minnet | Byt till `InputStream`‑laddning (se Feature 1). |
| **Annotationer fortfarande synliga** | Maskering inte tillämpad före sparning | Anropa `redactor.apply(new DeleteAnnotationRedaction())` före `save()`. |
| **PDF‑rasterisering inte tillämpad** | `setRasterizeToPDF(false)` eller utelämnad | Sätt `options.setRasterizeToPDF(true)` när du behöver en platt PDF. |

## Frequently Asked Questions

**Q: Kan jag maskera PDF‑dokument med GroupDocs.Redaction?**  
A: Ja, biblioteket stödjer PDF, DOCX, PPTX, XLSX och många andra format.

**Q: Vad är det bästa sättet att hantera stora filer med GroupDocs.Redaction?**  
A: Använd streaming (`load document from stream`) och stäng resurser omedelbart för att hålla minnesanvändningen låg.

**Q: Är det möjligt att anpassa suffix‑texten?**  
A: API:n lägger automatiskt till ett standardsuffix (t.ex. “_redacted”). För anpassade suffix kan du byta namn på utdatafilen efter sparning.

**Q: Hur får jag en tillfällig licens för GroupDocs.Redaction?**  
A: Besök [Temporary License page](https://purchase.groupdocs.com/temporary-license/) och följ instruktionerna.

**Q: Var kan jag få hjälp om jag stöter på problem?**  
A: Gå med i [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) för experthjälp.

## Resources
- **Documentation:** Utforska detaljerade guider på [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Få tillgång till omfattande API‑detaljer på [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Hämta den senaste versionen från [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Bidra eller utforska källkoden på [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Last Updated:** 2026-02-16  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs