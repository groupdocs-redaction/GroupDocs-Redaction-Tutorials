---
date: '2026-02-08'
description: Naučte se, jak maskovat citlivá data a redigovat PDF soubory v Javě pomocí
  GroupDocs OCR Redaction s Microsoft Azure OCR.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: Maskovat citlivá data v PDF pomocí GroupDocs OCR Redaction
type: docs
url: /cs/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Maskování citlivých údajů v PDF pomocí GroupDocs OCR Redaction

V dnešním digitálním prostředí je ochrana osobních a důvěrných informací nejvyšší prioritou. V tomto tutoriálu **se naučíte, jak maskovat citlivé údaje** v PDF souborech kombinací GroupDocs Redaction s Microsoft Azure OCR. Tento přístup vám poskytuje spolehlivé rozpoznávání textu na naskenovaných stránkách a umožňuje vám **redact PDF Java** dokumenty s přesností, což zajišťuje soulad s předpisy o ochraně soukromí.

## Rychlé odpovědi
- **Co znamená „maskovat citlivé údaje“?** Nahrazuje identifikovaný důvěrný text zástupným znakem (např. `[REDACTED]`).  
- **Která knihovna zpracovává OCR?** Microsoft Azure OCR konektor, používaný přes GroupDocs Redaction.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; pro produkci je vyžadována trvalá licence.  
- **Mohu redigovat naskenované PDF?** Ano — OCR extrahuje skrytý text před aplikací regexových redakcí.  
- **Je toto řešení pouze pro Java?** Příklad je založen na Javě, ale GroupDocs poskytuje podobná API pro .NET a další platformy.

## Co je OCR‑based redaction?
OCR‑based redaction nejprve spustí Optical Character Recognition na každé stránce dokumentu, převádí obrázky textu na prohledávatelné řetězce. Jakmile je text prohledávatelný, můžete použít pravidla regulárních výrazů (regex) k vyhledání citlivých informací — například čísla sociálního zabezpečení, čísla kreditních karet nebo osobní identifikátory — a nahradit je maskou, jako je **`[REDACTED]`**.

## Proč použít GroupDocs Redaction s Azure OCR?
- **Vysoká přesnost** u naskenovaných PDF a obrázků.  
- **Bezproblémová integrace s Java** přes Maven nebo přímé stažení JAR.  
- **Flexibilní regex engine** vám umožní definovat vlastní vzory pro jakýkoli typ dat.  
- **Škálovatelné** pro velké dávky dokumentů, s možnostmi asynchronního zpracování.

## Prerequisites
- **Java Development Kit (JDK) 8+** nainstalován.  
- **Maven** (pokud dáváte přednost správě závislostí) nebo možnost ručně stáhnout JAR soubory.  
- **Microsoft Azure OCR přihlašovací údaje** (endpoint a subscription key).  
- Základní znalost Javy a povědomí o regulárních výrazech.

## Nastavení GroupDocs Redaction pro Java

### Maven Setup
Přidejte repozitář GroupDocs a závislost do vašeho `pom.xml`:

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
Pokud dáváte přednost ruční správě JAR souborů, stáhněte si nejnovější verzi z [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Získání licence
- **Free Trial** – vyzkoušejte všechny funkce zdarma.  
- **Temporary License** – prodlužte dobu hodnocení.  
- **Full License** – odemkněte funkce připravené pro produkci.

### Základní inicializace a nastavení
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Jak maskovat citlivé údaje pomocí OCR redakce

### Krok 1: Načtení dokumentu s OCR nastavením
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
- **`LoadOptions`** – výchozí načítání; můžete přizpůsobit podle potřeby.  
- **`settings`** – obsahuje Azure OCR konektor, který jste vytvořili dříve.

### Krok 2: Definování a aplikace regex redakcí
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
- `ReplacementOptions("[REDACTED]")` nahradí každou shodu maskou, čímž efektivně **maskuje citlivé údaje**.

## Běžné případy použití maskování citlivých údajů
1. **Legal Document Management** – skryjte identifikátory klientů před sdílením návrhů.  
2. **Financial Reporting** – chraňte čísla účtů a ID transakcí.  
3. **Healthcare Records** – splňte požadavky HIPAA redigováním identifikátorů pacientů.  
4. **Government Publications** – odstraňte osobní údaje z veřejných záznamů.  
5. **Corporate Contracts** – skryjte proprietární podmínky během externích revizí.

## Tipy pro výkon
- **Optimalizujte regex** – vyhněte se příliš širokým vzorům, které zvyšují dobu zpracování.  
- **Správa paměti** – uzavřete instanci `Redactor` okamžitě (try‑with‑resources to provede automaticky).  
- **Asynchronní provádění** – pro hromadné zpracování spouštějte úlohy redakce na samostatných vláknech nebo použijte frontu úloh.  

## Troubleshooting
- **Chyba Azure přihlašovacích údajů** – dvakrát zkontrolujte URL endpointu a subscription key v `MicrosoftAzureOcrConnector`.  
- **Dokument se nenačítá** – ověřte cestu k souboru a ujistěte se, že PDF není chráněno heslem (nebo heslo poskytněte přes `LoadOptions`).  
- **Neaplikovaly se žádné redakce** – nejprve otestujte svůj regex na jednoduchém řetězci; použijte `Pattern.compile` v unit testu k potvrzení shod.

## Často kladené otázky

**Q: Co je OCR redakce?**  
A: OCR redakce používá Optical Character Recognition k extrahování skrytého textu z obrázků nebo naskenovaných PDF, poté aplikuje pravidla redakce k maskování tohoto textu.

**Q: Mohu použít GroupDocs Redaction bez Azure OCR?**  
A: Ano, ale OCR výrazně zlepšuje přesnost u naskenovaných dokumentů, kde nativní extrakce textu selže.

**Q: Jak zacházet s komplexními regex vzory?**  
A: Vytvářejte a testujte je postupně, pomocí třídy `Pattern` v Javě v sandboxu před aplikací na velké dokumenty.

**Q: Jaké jsou typické úzké místa výkonu?**  
A: Velké PDF, příliš složité regexy a synchronní OCR volání mohou zpomalit zpracování; zvažte dávkové zpracování a optimalizované vzory.

**Q: Je k dispozici podpora pro implementační problémy?**  
A: Rozhodně — obraťte se přes [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) na komunitu nebo kontaktujte podporu GroupDocs.

## Další zdroje
- **Dokumentace**: https://docs.groupdocs.com/redaction/java/  
- **API Reference**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Bezplatná podpora**: https://forum.groupdocs.com/c/redaction/33  
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

---

**Poslední aktualizace:** 2026-02-08  
**Testováno s:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs