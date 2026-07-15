---
date: '2026-05-22'
description: Naučte se, jak přidat suffix filename java pomocí GroupDocs Maven dependency
  při redacting documents. Includes streaming load, annotation deletion, and save
  options.
keywords:
- add suffix filename java
- groupdocs redaction java
- document redaction workflow
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  headline: Add suffix filename java with GroupDocs Maven
  type: TechArticle
- description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  name: Add suffix filename java with GroupDocs Maven
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
title: Přidat suffix filename java pomocí GroupDocs Maven
type: docs
url: /cs/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Přidání přípony k názvu souboru java pomocí GroupDocs Maven

Redigování důvěrných údajů je jen polovinou boje—musíte také zajistit, aby uložený soubor jasně naznačoval, že byl zpracován. **Použití závislosti GroupDocs Maven to usnadňuje**, umožňuje přidat příponu k názvu výstupního souboru během několika řádků kódu. Metoda pro **add suffix filename java** je jednorázová konfigurace, která okamžitě označí vaše redigované soubory, pomáhá vám zůstat v souladu a připravený na audit.

## Rychlé odpovědi
- **Co dělá “add suffix to filename”?**  
  Přidá vlastní příponu (např. “_redacted”) k názvu výstupního souboru, takže můžete okamžitě identifikovat zpracované soubory.  
- **Mohu načíst dokument ze streamu?**  
  Ano—GroupDocs.Redaction podporuje načítání z libovolného `InputStream`, což je ideální pro cloudové úložiště nebo zpracování v paměti.  
- **Potřebuji licenci pro tuto funkci?**  
  Bezplatná zkušební verze funguje pro základní redigování; dočasná nebo plná licence odemkne všechny pokročilé možnosti, včetně práce s příponou.  
- **Jaké formáty jsou podporovány?**  
  Knihovna zpracovává DOCX, PDF, PPTX, XLSX a mnoho dalších.  
- **Je rasterizace vyžadována pro výstup PDF?**  
  Rasterizace je volitelná; povolte ji, když potřebujete dokument zploštit pro zvýšenou bezpečnost.

## Co je add suffix filename java?
Technika **add suffix filename java** přidává předdefinovaný řetězec k názvu souboru během operace uložení, čímž jasně označuje dokument jako redigovaný. Tento jednoduchý konvencionalismus zabraňuje neúmyslnému šíření původních, neredigovaných souborů a hladce se integruje do automatizovaných pipeline.

## Proč použít GroupDocs.Redaction pro tento úkol?
GroupDocs.Redaction poskytuje plynulé Java API, které vám umožní kombinovat redakční akce s možnostmi manipulace se soubory—jako **add suffix filename java**—během několika řádků kódu. SDK podporuje **50+ vstupních a výstupních formátů** a dokáže zpracovat dokumenty s několika stovkami stránek bez načítání celého souboru do paměti, což přináší jak rychlost, tak nízkou paměťovou stopu.

## Požadavky
- **Java Development Kit (JDK):** Verze 8 nebo vyšší.  
- **GroupDocs.Redaction Library:** Hlavní knihovna pro úlohy redigování.  
- **IDE:** IntelliJ IDEA, Eclipse nebo jakýkoli editor kompatibilní s Javou.  
- **Maven:** Pro správu závislostí.  

### Znalostní požadavky
Znalost Java I/O a základních objektově orientovaných konceptů usnadní pochopení příkladů.

## Nastavení GroupDocs.Redaction pro Java
### Maven nastavení
Do souboru `pom.xml` vložte následující konfiguraci pro přístup k knihovnám GroupDocs přes Maven:

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
Alternativně si stáhněte nejnovější verzi přímo z [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Získání licence
1. **Free Trial:** Přístup k základní funkčnosti bez omezení.  
2. **Temporary License:** Získejte dočasnou licenci pro vyzkoušení pokročilých funkcí.  
3. **Purchase:** Pro dlouhodobé používání zvažte zakoupení plné licence.

#### Základní inicializace a nastavení
Do projektu přidejte potřebné importy:

```java
import com.groupdocs.redaction.Redactor;
```

S tímto nastavením jste připraveni implementovat funkce redigování dokumentů.

## Průvodce implementací

### Funkce 1: Načtení dokumentu ze streamu
**Overview:** Naučte se načíst dokumenty do `InputStream` pro další zpracování.

#### Postupná implementace
##### Krok 1.1: Vytvoření InputStream

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

- **Why:** Použití `InputStream` vám umožní pracovat s dokumenty uloženými na různých místech—cloudových bucketů, databázích nebo v paměti—bez nutnosti je nejprve zapisovat na disk. Tento přístup je nezbytný, když potřebujete **load document from stream** v mikroservisních architekturách.

### Funkce 2: Použití redakce mazání anotací
**Overview:** Odstraňte anotace z dokumentu pomocí `DeleteAnnotationRedaction`.

#### Postupná implementace
##### Krok 2.1: Použití DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Why:** Tento krok zajistí, že všechny citlivé anotace (komentáře, zvýraznění nebo skryté poznámky) budou z dokumentu odstraněny, čímž se zvýší soukromí a shoda s předpisy.

### Funkce 3: Uložení dokumentu s možnostmi
**Overview:** Naučte se uložit zpracovaný dokument s konkrétními možnostmi, jako je rasterizace a **add suffix filename java**.

#### Postupná implementace
##### Krok 3.1: Konfigurace SaveOptions

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

- **Why:** Přizpůsobení možností uložení umožňuje flexibilní výstupní formáty a pojmenování souborů. Povolení `setAddSuffix(true)` **adds suffix to filename**, což jasně ukazuje, že soubor byl redigován.

## Jak přidat suffix filename java při ukládání dokumentu?
`Redactor` je hlavní třída v GroupDocs.Redaction, která načítá dokument a aplikuje redakční operace.  
`setAddSuffix` je metoda třídy `SaveOptions`, která umožňuje automatické přidání přípony k názvu výstupního souboru.  

Načtěte instanci `Redactor`, aplikujte požadované redakce a poté zavolejte `save()` s `SaveOptions`, kde je povoleno `setAddSuffix(true)`. Tato jednorázová konfigurace automaticky připojí “_redacted” (nebo výchozí příponu) k názvu souboru, čímž eliminuje ruční přejmenování a snižuje lidskou chybu. Operace končí v čase O(n) vzhledem k velikosti dokumentu a funguje pro všechny podporované formáty.

## Přehled závislosti groupdocs maven
**groupdocs maven dependency** přináší celé Redaction SDK do vašeho projektu pomocí jediného záznamu `<dependency>`. Spravuje tranzitivní závislosti, udržuje knihovny aktuální a zjednodušuje automatizaci sestavení. Deklarací závislosti v `pom.xml` se vyhnete ručnímu řízení JAR souborů a zajistíte kompatibilitu s nejnovějšími bezpečnostními záplatami.

## Proč je přidání přípony důležité
Přidání přípony poskytuje okamžité vizuální potvrzení, že dokument byl zpracován, což je klíčové pro auditní stopy, automatizované workflow a regulatorní shodu napříč odvětvími.

- **Auditability:** Týmy mohou okamžitě rozpoznat, které soubory jsou bezpečné k distribuci.  
- **Automation:** Skripty mohou filtrovat soubory podle přípony, čímž se zabrání neúmyslnému zpracování originálních dokumentů.  
- **Compliance:** Mnoho předpisů vyžaduje jasné označení sanitovaných dokumentů.  

## Praktické aplikace
1. **Legal Document Redaction:** Zabezpečte smlouvy před sdílením s klienty.  
2. **Medical Record Handling:** Chraňte identifikátory pacientů při zachování klinických dat.  
3. **Financial Reporting:** Udržujte citlivá čísla důvěrná během externích auditů.  
4. **CRM Integration:** Automaticky redigujte zákaznická data před exportem do nástrojů třetích stran.  
5. **Collaboration Tools:** Zajistěte, aby sdílené koncepty nikdy neodhalily skryté komentáře nebo metadata.  

## Úvahy o výkonu
### Optimalizace výkonu
- Používejte streamování (`load document from stream`) k vyhnutí se načítání celých souborů do paměti.  
- Okamžitě uzavírejte instance `Redactor` pro uvolnění zdrojů.  

### Pokyny pro využití zdrojů
- Sledujte CPU a paměť během dávkových běhů.  
- Upřednostňujte `ByteArrayOutputStream` pro ukládání v paměti při práci s menšími soubory.  

### Nejlepší postupy pro správu paměti v Java
- Znovu používejte objekty `Redactor` při zpracování více souborů stejného typu.  
- Volání `close()` provádějte v bloku `try‑with‑resources`, aby nedocházelo k únikům.  

## Časté problémy a řešení
| Problém | Příčina | Řešení |
|-------|-------|-----|
| **Suffix not appearing** | `setAddSuffix(false)` nebo chybějící volání | Ujistěte se, že `options.setAddSuffix(true)` je nastaveno před voláním `save()`. |
| **OutOfMemoryError on large DOCX** | Načítání celého souboru do paměti | Přepněte na načítání pomocí `InputStream` (viz Funkce 1). |
| **Annotations still visible** | Redakce nebyla aplikována před uložením | Zavolejte `redactor.apply(new DeleteAnnotationRedaction())` před `save()`. |
| **PDF rasterization not applied** | `setRasterizeToPDF(false)` nebo vynecháno | Nastavte `options.setRasterizeToPDF(true)`, pokud potřebujete zploštělý PDF. |

## Často kladené otázky

**Q: Mohu redigovat PDF dokumenty pomocí GroupDocs.Redaction?**  
A: Ano, knihovna podporuje PDF, DOCX, PPTX, XLSX a mnoho dalších formátů.

**Q: Jaký je nejlepší způsob, jak zacházet s velkými soubory v GroupDocs.Redaction?**  
A: Používejte streamování (`load document from stream`) a rychle uzavírejte zdroje, aby byl paměťový odběr nízký.

**Q: Je možné přizpůsobit text přípony?**  
A: API automaticky přidá výchozí příponu (např. “_redacted”). Pro vlastní přípony přejmenujte výstupní soubor po uložení.

**Q: Jak získám dočasnou licenci pro GroupDocs.Redaction?**  
A: Navštivte [Temporary License page](https://purchase.groupdocs.com/temporary-license/) a postupujte podle instrukcí.

**Q: Kde mohu získat pomoc, pokud narazím na problémy?**  
A: Připojte se k [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) pro odbornou asistenci.

## Zdroje
- **Documentation:** Prozkoumejte podrobné návody na [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Získejte kompletní informace o API na [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Stáhněte nejnovější verzi z [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Přispívejte nebo prozkoumejte zdrojový kód na [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Last Updated:** 2026-05-22  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Související tutoriály

- [Převod Wordu na PDF a uložení redigovaných dokumentů s GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Náhled stránek dokumentu v Javě načítání s GroupDocs.Redaction](/redaction/java/document-loading/)
- [Pokročilé techniky redigování pro GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)