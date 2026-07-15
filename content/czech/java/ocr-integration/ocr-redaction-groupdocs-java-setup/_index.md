---
date: '2026-06-26'
description: Zjistěte, jak extrahovat text ze skenovaného PDF a maskovat citlivá data
  pomocí GroupDocs OCR Redaction s Azure OCR. Maskujte číslo sociálního zabezpečení
  a efektivně nahrazujte důvěrné informace v PDF.
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
title: Extrahovat text ze skenovaného PDF – Maskovat data pomocí GroupDocs OCR
type: docs
url: /cs/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Extrahovat text ze skenovaného PDF – Maskovat data pomocí GroupDocs OCR

V dnešním datově řízeném světě je **extrahování textu ze skenovaných PDF** souborů a maskování důvěrných informací nevyjednatelným krokem v souladu s předpisy. Tento tutoriál vás provede používáním GroupDocs Redaction spolu s Microsoft Azure OCR k spolehlivému rozpoznání skrytého textu na skenovaných stránkách a jeho nahrazení bezpečným zástupcem, jako je **`[REDACTED]`**. Uvidíte, proč je tato kombinace rychlá, přesná a připravená pro produkční zátěže.

## Rychlé odpovědi
- **Co znamená „maskovat citlivá data“?** Nahrazuje identifikovaný důvěrný text zástupcem (např. `[REDACTED]`).  
- **Která knihovna zpracovává OCR?** Microsoft Azure OCR konektor, používaný přes GroupDocs Redaction.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; pro produkci je vyžadována trvalá licence.  
- **Mohu redigovat skenovaná PDF?** Ano — OCR extrahuje skrytý text před aplikací regexových redakcí.  
- **Je toto řešení jen pro Javu?** Příklad je založen na Javě, ale GroupDocs poskytuje podobná API pro .NET a další platformy.

## Co je OCR‑založená redakce?
OCR‑Based Redaction nejprve spustí OCR na každé stránce, převádí obrázky na prohledávatelný text a poté aplikuje regexové vzory k nahrazení shod maskou, jako je `[REDACTED]`. Tento dvoustupňový proces vám umožní spolehlivě skrýt osobní data i ve skenovaných PDF, čímž zajistí, že všechny citlivé řetězce jsou odstraněny před sdílením nebo archivací dokumentu.

## Proč používat GroupDocs Redaction s Azure OCR?
Měli byste používat GroupDocs Redaction s Azure OCR, protože poskytuje **>98 % přesnost OCR u tištěného textu**, podporuje **více než 50 vstupních a výstupních formátů** a dokáže zpracovat **PDF s několika stovkami stránek bez načítání celého souboru do paměti**, což zajišťuje rychlou, škálovatelnou redakci pro soulad s předpisy. Řešení také **škáluje tak, že zpracuje 1 000‑stránkové PDF za méně než 2 minuty na 8‑jádrovém serveru**, což dělá dávkové úlohy praktickými.

## Požadavky
- **Java Development Kit (JDK) 8+** nainstalován.  
- **Maven** (pokud dáváte přednost správě závislostí) nebo možnost stáhnout JAR soubory ručně.  
- **Microsoft Azure OCR přihlašovací údaje** (endpoint a klíč předplatného).  
- Základní znalost Javy a povědomí o regulárních výrazech.

## Nastavení GroupDocs Redaction pro Javu

### Nastavení Maven
Add the GroupDocs repository and dependency to your `pom.xml`:

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

### Přímé stažení
Pokud dáváte přednost ruční správě JAR souborů, stáhněte nejnovější verzi z [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Získání licence
- **Free Trial** – prozkoumejte všechny funkce zdarma.  
- **Temporary License** – prodlužte dobu hodnocení.  
- **Full License** – odemkněte produkčně připravené funkce.

### Základní inicializace a nastavení
Třída `Redactor` je jádrový motor, který provádí OCR extrakci a aplikuje pravidla redakce na PDF dokumenty.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Jak maskovat citlivá data pomocí OCR redakce
Maskování citlivých dat pomocí OCR redakce zahrnuje načtení PDF s nastavením Azure OCR, definování regexových vzorů pro data, která chcete skrýt, a volání Redactoru k nahrazení každé shody zástupcem jako `[REDACTED]`. Knihovna zpracovává OCR, shodu vzorů a přepisování PDF v jednom pracovním postupu.

### Krok 1: Načíst dokument s OCR nastavením
`LoadOptions` konfiguruje, jak GroupDocs načítá soubor, což vám umožní předat OCR konektory jako Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – nahraďte cestou k vašemu PDF.  
- **`settings`** – obsahuje Azure OCR konektor, který jste vytvořili dříve.

### Krok 2: Definovat a aplikovat regexové redakce
`ReplacementOptions` určuje náhradní text, který nahradí každou regex shodu během redakce.  
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
- Vzor `\b\d{3}-\d{2}-\d{4}\b` odpovídá americkým číslům sociálního zabezpečení.  
- `ReplacementOptions("[REDACTED]")` vymění každou shodu za masku, čímž efektivně **maskuje citlivá data**.

## Běžné případy použití pro maskování citlivých dat
1. **Správa právních dokumentů** – skrýt identifikátory klientů před sdílením návrhů.  
2. **Finanční výkaznictví** – chránit čísla účtů a ID transakcí.  
3. **Zdravotní záznamy** – dodržet HIPAA redakcí identifikátorů pacientů.  
4. **Vládní publikace** – odstranit osobní data z veřejných záznamů.  
5. **Firemní smlouvy** – skrýt proprietární podmínky během externích revizí.

## Tipy pro výkon
- **Optimalizujte regex** – vyhněte se příliš širokým vzorům, které zvyšují dobu zpracování; dobře navržené výrazy mohou zkrátit dobu běhu až o 40 %.  
- **Správa paměti** – uzavřete instanci `Redactor` okamžitě (try‑with‑resources to provede automaticky).  
- **Asynchronní provádění** – pro hromadné zpracování spouštějte úlohy redakce na samostatných vláknech nebo použijte frontu úloh, aby UI zůstalo responzivní.

## Řešení problémů
- **Chyba Azure přihlašovacích údajů** – zkontrolujte URL endpointu a klíč předplatného v `MicrosoftAzureOcrConnector`.  
- **Dokument se nenačítá** – ověřte cestu k souboru a ujistěte se, že PDF není chráněno heslem (nebo poskytněte heslo pomocí `LoadOptions`).  
- **Nebyla aplikována žádná redakce** – nejprve otestujte svůj regex na jednoduchém řetězci; použijte `Pattern.compile` v unit testu k potvrzení shod.

## Často kladené otázky

**Q: Co je OCR redakce?**  
A: OCR redakce používá optické rozpoznávání znaků (Optical Character Recognition) k extrakci skrytého textu z obrázků nebo skenovaných PDF, poté aplikuje pravidla redakce k maskování tohoto textu.

**Q: Mohu použít GroupDocs Redaction bez Azure OCR?**  
A: Ano, ale OCR výrazně zvyšuje přesnost u skenovaných dokumentů, kde nativní extrakce textu selhává.

**Q: Jak zacházet s komplexními regexovými vzory?**  
A: Vytvářejte a testujte je postupně, pomocí třídy `Pattern` v Javě v sandboxu před aplikací na velké dokumenty.

**Q: Jaké jsou typické úzké místa výkonu?**  
A: Velká PDF, příliš komplexní regex a synchronní OCR volání mohou zpomalit zpracování; zvažte dávkové zpracování a optimalizované vzory.

**Q: Je k dispozici podpora pro implementační problémy?**  
A: Rozhodně — obraťte se přes [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) na komunitní pomoc nebo kontaktujte podporu GroupDocs.

## Další zdroje
- **Dokumentace**: https://docs.groupdocs.com/redaction/java/  
- **API Reference**: https://reference.groupdocs.com/redaction/java  
- **Stáhnout**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Bezplatná podpora**: https://forum.groupdocs.com/c/redaction/33  
- **Dočasná licence**: https://purchase.groupdocs.com/temporary-license/

---

**Poslední aktualizace:** 2026-06-26  
**Testováno s:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs  

## Související tutoriály

- [Bezpečná PDF redakce pomocí OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Jak redigovat text pomocí GroupDocs.Redaction pro Javu](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Maskovat citlivá data Java – Redigovat osobní informace pomocí GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)