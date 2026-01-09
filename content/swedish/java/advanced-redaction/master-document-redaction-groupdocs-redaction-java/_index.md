---
date: '2025-12-17'
description: Lär dig hur du lägger till ett suffix till filnamnet och raderar känslig
  information från dokument med GroupDocs.Redaction för Java. Förbättra dokumentens
  säkerhet och integritet på ett effektivt sätt.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Hur man lägger till ett suffix till filnamnet när man redigerar dokument i
  Java med GroupDocs.Redaction
type: docs
url: /sv/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Så lägger du till suffix i filnamnet när du maskerar dokument i Java med GroupDocs.Redaction

Att maskera konfidentiella data är bara halva striden—du måste också se till att den sparade filen tydligt visar att den har behandlats. I den här guiden lär du dig **hur du lägger till suffix i filnamnet** när du sparar ett maskerat dokument, samt hur du laddar, kommenterar och sparar med GroupDocs.Redaction för Java. Oavsett om du skyddar juridiska kontrakt, medicinska journaler eller finansiella rapporter, kommer dessa steg att hålla ditt arbetsflöde både säkert och spårbart.

## Snabba svar
- **Vad gör “add suffix to filename”?**  
  Det lägger till ett anpassat suffix (t.ex. “_redacted”) till utdatafilens namn så att du omedelbart kan identifiera bearbetade filer.  
- **Kan jag ladda ett dokument från en ström?**  
  Ja—GroupDocs.Redaction stöder inläsning från vilken `InputStream` som helst, perfekt för molnlagring eller in‑minnesbehandling.  
- **Behöver jag en licens för den här funktionen?**  
  En gratis provperiod fungerar för grundläggande maskering; en tillfällig eller full licens låser upp alla avancerade alternativ, inklusive hantering av suffix.  
- **Vilka format stöds?**  
  Biblioteket hanterar DOCX, PDF, PPTX, XLSX och många fler.  
- **Krävs rasterisering för PDF-utdata?**  
  Rasterisering är valfri; aktivera den när du behöver platta till dokumentet för extra säkerhet.

## Vad är att lägga till ett suffix i ett filnamn?
Att lägga till ett suffix är en enkel namngivningskonvention som signalerar att en fil har genomgått maskering. Det förhindrar oavsiktlig delning av original, omaskerade versioner och hjälper automatiserade pipelines att spåra bearbetningsstatus.

## Varför använda GroupDocs.Redaction för denna uppgift?
GroupDocs.Redaction erbjuder ett flytande Java‑API som låter dig kombinera maskeringsåtgärder med filhanteringsalternativ—som **att lägga till ett suffix i filnamnet**—på bara några kodrader. Detta sparar utvecklingstid och minskar risken för manuella fel.

## Förutsättningar
- **Java Development Kit (JDK):** Version 8 eller högre.  
- **GroupDocs.Redaction Library:** Kärnbibliotek för maskeringsuppgifter.  
- **IDE:** IntelliJ IDEA, Eclipse eller någon Java‑kompatibel editor.  
- **Maven:** För beroendehantering.  

### Kunskapsförutsättningar
Bekantskap med Java I/O och grundläggande objektorienterade koncept gör exemplen lättare att följa.

## Konfigurera GroupDocs.Redaction för Java
### Maven‑inställning
Inkludera följande konfiguration i din `pom.xml`‑fil för att komma åt GroupDocs‑biblioteken via Maven:

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

### Direkt nedladdning
Alternativt, ladda ner den senaste versionen direkt från [GroupDocs.Redaction för Java‑utgåvor](https://releases.groupdocs.com/redaction/java/).

### Licensanskaffning
1. **Free Trial:** Få tillgång till grundfunktionalitet utan begränsningar.  
2. **Temporary License Skaffa en tillfällig licens för att utforska avancerade funktioner.  
3. **Purchase:** För långsiktig användning, överväg att köpa en full licens.

#### Grundläggande initiering och konfiguration
Initiera ditt projekt genom att lägga till nödvändiga importeringar:

```java
import com.groupdocs.redaction.Redactor;
```

Med denna konfiguration är du redo att implementera funktioner för dokumentmaskering.

## Implementeringsguide

### Funktion 1: Ladda dokument från ström
**Översikt:** Lär dig hur du laddar dokument i ett `InputStream` för bearbetning.

#### Steg‑för‑steg‑implementering
##### Steg 1.1: Skapa InputStream

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

- **Varför:** Att använda `InputStream` gör att du kan hantera dokument lagrade i olika format sömlöst, vilket är viktigt när du behöver **ladda dokument från ström** i moln‑ eller mikrotjänstscenarier.

### Funktion 2: Tillämpa radering av annotationer
**Översikt:** Ta bort annotationer från ditt dokument med hjälp av `DeleteAnnotationRedaction`.

##### Steg 2.1: Tillämpa DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Varför:** Detta steg säkerställer att eventuella känsliga annotationer tas bort, vilket förbättrar dokumentets sekretess.

### Funktion 3: Spara dokument med alternativ
**Översikt:** Lär dig hur du sparar ditt bearbetade dokument med specifika alternativ som rasterisering och **att lägga till ett suffix i filnamnet**.

##### Steg 3.1: Konfigurera SaveOptions

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

- **Varför:** Anpassning av sparalternativ ger flexibla utdataformat och namngivningskonventioner. Aktivering av `setAddSuffix(true)` **lägger till suffix i filnamnet**, vilket tydligt visar att filen har maskerats.

## Varför ett suffix är viktigt
- **Spårbarhet:** Team kan omedelbart se vilka filer som är säkra att distribuera.  
- **Automation:** Skript kan filtrera filer efter suffix, vilket förhindrar oavsiktlig bearbetning av originaldokument.  
- **Efterlevnad:** Många regelverk kräver tydlig märkning av sanerade dokument.

## Praktiska tillämpningar
Utforska dessa verkliga användningsfall:
1. **Legal Document Redaction:** Säkerställ kontrakt innan delning med klienter.  
2. **Medical Record Handling:** Skydda patientidentifierare.  
3. **Financial Reporting:** Håll känsliga siffror konfidentiella.  
4. **CRM Integration:** Automatisk maskering av kunddata före export.  
5. **Collaboration Tools:** Säkerställ att delade utkast aldrig avslöjar dolda kommentarer.

## Prestandaöverväganden
### Optimera prestanda
- Använd streaming (`load document from stream`) för att undvika att ladda hela filer i minnet.  
- Stäng `Redactor`‑instanser omedelbart för att frigöra resurser.

### Riktlinjer för resursanvändning
- Övervaka CPU och minne under batchkörningar.  
- Föredra `ByteArrayOutputStream` för sparande i minnet när du arbetar med måttliga filstorlekar.

### Bästa praxis för Java‑minneshantering
- Återanvänd `Redactor`‑objekt när du bearbetar flera filer av samma typ.  
- Anropa `close()` i ett `finally`‑block eller med try‑with‑resources för att förhindra läckor.

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|-------|-------|-----|
| **Suffix visas inte** | `setAddSuffix(false)` eller saknad anrop | Se till att `options.setAddSuffix(true)` är satt innan `save()`. |
| **OutOfMemoryError på stora DOCX** | Laddar hela filen i minnet | Byt till inläsning via `InputStream` (se Funktion 1). |
| **Annotationer fortfarande synliga** | Maskering har inte tillämpats före sparning | Anropa `redactor.apply(new DeleteAnnotationRedaction())` före `save()`. |
| **PDF‑rasterisering inte tillämpad** | `setRasterizeToPDF(false)` eller utelämnad | Sätt `options.setRasterizeToPDF(true)` när du behöver ett platt PDF‑dokument. |

## Vanliga frågor

**Q: Kan jag maskera PDF‑dokument med GroupDocs.Redaction?**  
A: Ja, biblioteket stöder PDF, DOCX, PPTX, XLSX och många andra format.

**Q: Vad är det bästa sättet att hantera stora filer med GroupDocs.Redaction?**  
A: Använd streaming (`load document from stream`) och stäng resurser omedelbart för att hålla minnesanvändningen låg.

**Q: Är det möjligt att anpassa suffix‑texten?**  
A: API:t lägger automatiskt till ett standardsuffix (t.ex. “_redacted”). För anpassade suffix kan du byta namn på utdatafilen efter sparning.

**Q: Hur får jag en tillfällig licens för GroupDocs.Redaction?**  
A: Besök [Tillfällig licens‑sida](https://purchase.groupdocs.com/temporary-license/) och följ instruktionerna.

**Q: Var kan jag få hjälp om jag stöter på problem?**  
A: Gå med i [GroupDocs Support‑forumet](https://forum.groupdocs.com/c/redaction/33) för experthjälp.

## Resurser
- **Documentation:** Utforska detaljerade guider på [GroupDocs Dokumentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Få tillgång till omfattande API‑detaljer på [GroupDocs API‑referens](https://reference.groupdocs.com/redaction/java).  
- **Download:** Hämta den senaste versionen från [GroupDocs Nedladdningar](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Bidra eller utforska källkoden på [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Senast uppdaterad:** 2025-12-17  
**Testad med:** GroupDocs.Redaction 24.9 för Java  
**Författare:** GroupDocs