---
date: '2026-06-26'
description: Lär dig hur du extraherar text från skannad PDF och maskerar känslig
  data med GroupDocs OCR Redaction och Azure OCR. Maskera social security number och
  ersätt confidential info i PDF effektivt.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Extrahera text från skannad PDF – Maskera data med GroupDocs OCR
type: docs
url: /sv/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Extrahera text från skannad PDF – Maskera data med GroupDocs OCR

I dagens datadrivna värld är **extrahering av text från skannade PDF**‑filer och maskering av konfidentiell information ett icke‑förhandlingsbart efterlevnadsteg. Den här handledningen visar hur du använder GroupDocs Redaction tillsammans med Microsoft Azure OCR för att på ett pålitligt sätt känna igen dold text på skannade sidor och ersätta den med en säker platshållare såsom **`[REDACTED]`**. Du kommer att se varför denna kombination är snabb, exakt och klar för produktionsklassade arbetsbelastningar.

## Snabba svar
- **Vad betyder “maskera känslig data”?** Det ersätter identifierad konfidentiell text med en platshållare (t.ex. `[REDACTED]`).  
- **Vilket bibliotek hanterar OCR?** Microsoft Azure OCR‑anslutning, som används via GroupDocs Redaction.  
- **Behöver jag en licens?** En gratis provperiod fungerar för utvärdering; en permanent licens krävs för produktion.  
- **Kan jag maskera skannade PDF‑filer?** Ja—OCR extraherar den dolda texten innan regex‑maskeringar tillämpas.  
- **Är den här lösningen enbart Java?** Exemplet är Java‑baserat, men GroupDocs tillhandahåller liknande API:er för .NET och andra plattformar.

## Vad är OCR‑baserad maskering?
OCR‑baserad maskering kör först OCR på varje sida, omvandlar bilder till sökbar text och tillämpar sedan regex‑mönster för att ersätta träffar med en mask som `[REDACTED]`. Denna tvåstegsprocess låter dig på ett pålitligt sätt dölja personuppgifter även i skannade PDF‑filer, vilket säkerställer att känsliga strängar tas bort innan dokumentet delas eller arkiveras.

## Varför använda GroupDocs Redaction med Azure OCR?
Du bör använda GroupDocs Redaction med Azure OCR eftersom det levererar **>98 % OCR‑noggrannhet på tryckt text**, stödjer **50+ in‑ och utdataformat**, och kan bearbeta **PDF‑filer med hundratals sidor utan att läsa in hela filen i minnet**, vilket säkerställer snabb, skalbar maskering för efterlevnad. Lösningen **skalar också för att bearbeta en 1 000‑sidig PDF på under 2 minuter på en 8‑kärnig server**, vilket gör batch‑jobb praktiska.

## Förutsättningar
- **Java Development Kit (JDK) 8+** installerat.  
- **Maven** (om du föredrar beroendehantering) eller möjlighet att ladda ner JAR‑filer manuellt.  
- **Microsoft Azure OCR‑uppgifter** (slutpunkt och prenumerationsnyckel).  
- Grundläggande kunskaper i Java och bekantskap med reguljära uttryck.

## Konfigurera GroupDocs Redaction för Java

### Maven‑konfiguration
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
Om du föredrar manuell JAR‑hantering, hämta den senaste versionen från [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Licensanskaffning
- **Free Trial** – utforska alla funktioner utan kostnad.  
- **Temporary License** – förläng utvärderingstiden.  
- **Full License** – lås upp produktionsklara funktioner.

### Grundläggande initiering och konfiguration
Klassen `Redactor` är kärnmotorn som utför OCR‑extraktion och tillämpar maskeringsregler på PDF‑dokument.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Hur man maskerar känslig data med OCR‑maskering
Maskering av känslig data med OCR‑maskering innebär att ladda PDF‑filen med Azure OCR‑inställningar, definiera regex‑mönster för den data du vill dölja, och anropa Redactor för att ersätta varje träff med en platshållare som `[REDACTED]`. Biblioteket hanterar OCR, mönstermatchning och PDF‑omskrivning i ett enda arbetsflöde.

### Steg 1: Ladda dokumentet med OCR‑inställningar
`LoadOptions` konfigurerar hur GroupDocs laddar en fil och låter dig skicka OCR‑anslutningar som Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – ersätt med sökvägen till din PDF.  
- **`settings`** – innehåller Azure OCR‑anslutningen du skapade tidigare.

### Steg 2: Definiera och tillämpa regex‑maskeringar
`ReplacementOptions` specificerar ersättningstexten som kommer att ersätta varje regex‑träff under maskering.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- Mönstret `\b\d{3}-\d{2}-\d{4}\b` matchar amerikanska personnummer (Social Security Numbers).  
- `ReplacementOptions("[REDACTED]")` byter ut varje träff mot masken, vilket effektivt **maskerar känslig data**.

## Vanliga användningsfall för maskering av känslig data
1. **Legal Document Management** – dölja kundidentifierare innan utkast delas.  
2. **Financial Reporting** – skydda kontonummer och transaktions‑ID.  
3. **Healthcare Records** – uppfylla HIPAA genom att maskera patientidentifierare.  
4. **Government Publications** – ta bort personuppgifter från offentliga handlingar.  
5. **Corporate Contracts** – dölja proprietära villkor under externa granskningar.

## Prestandatips
- **Optimize regex** – undvik alltför breda mönster som ökar behandlingstiden; välkonstruerade uttryck kan minska körtiden med upp till 40 %.  
- **Memory Management** – stäng `Redactor`‑instansen omedelbart (try‑with‑resources gör detta automatiskt).  
- **Asynchronous Execution** – för massbearbetning, kör maskeringsjobb på separata trådar eller använd en kö för att hålla UI‑responsen.

## Felsökning
- **Azure credentials error** – dubbelkolla slutpunkt‑URL:en och prenumerationsnyckeln i `MicrosoftAzureOcrConnector`.  
- **Document not loading** – verifiera filvägen och säkerställ att PDF‑filen inte är lösenordsskyddad (eller ange lösenordet via `LoadOptions`).  
- **No redactions applied** – testa ditt regex med en enkel sträng först; använd `Pattern.compile` i ett enhetstest för att bekräfta träffar.

## Vanliga frågor

**Q: Vad är OCR‑maskering?**  
A: OCR‑maskering använder optisk teckenigenkänning för att extrahera dold text från bilder eller skannade PDF‑filer, och tillämpar sedan maskeringsregler för att dölja den texten.

**Q: Kan jag använda GroupDocs Redaction utan Azure OCR?**  
A: Ja, men OCR förbättrar avsevärt noggrannheten på skannade dokument där inbyggd textutvinning misslyckas.

**Q: Hur hanterar jag komplexa regex‑mönster?**  
A: Bygg och testa dem stegvis, använd Java:s `Pattern`‑klass i en sandlåda innan du tillämpar dem på stora dokument.

**Q: Vilka är typiska prestandaflaskhalsar?**  
A: Stora PDF‑filer, alltför komplexa regex‑mönster och synkrona OCR‑anrop kan sakta ner bearbetningen; överväg batch‑bearbetning och optimerade mönster.

**Q: Finns support för implementationsproblem?**  
A: Absolut—kontakta via [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) för gemenskapsstöd eller kontakta GroupDocs support.

## Ytterligare resurser
- **Dokumentation**: https://docs.groupdocs.com/redaction/java/  
- **API‑referens**: https://reference.groupdocs.com/redaction/java  
- **Nedladdning**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Gratis support**: https://forum.groupdocs.com/c/redaction/33  
- **Tillfällig licens**: https://purchase.groupdocs.com/temporary-license/

---

**Senast uppdaterad:** 2026-06-26  
**Testad med:** GroupDocs.Redaction 24.9 (Java)  
**Författare:** GroupDocs  

## Relaterade handledningar

- [Säker PDF‑maskering med OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Hur man maskerar text med GroupDocs.Redaction för Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Maskera känslig data Java – Maskera personlig information med GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)