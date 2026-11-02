---
date: '2026-11-02'
description: Naučte se, jak přidat příponu k názvu souboru v tutoriálu GroupDocs redaction
  Java pomocí Maven, streamovacího načtení, mazání anotací a možností uložení.
keywords:
- groupdocs redaction java tutorial
- add suffix filename java
- document redaction workflow
- groupdocs maven dependency
- java inputstream redaction
lastmod: '2026-11-02'
og_description: Naučte se, jak přidat příponu k názvu souboru v tutoriálu GroupDocs
  redaction Java. Postupujte krok za krokem při nastavení Maven, streamovacím načtení
  a možnostech uložení.
og_image_alt: Guide showing Java code to add suffix to redacted filenames using GroupDocs
  Redaction
og_title: Jak přidat příponu k názvu souboru v GroupDocs redaction Java
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
title: Jak přidat příponu k názvu souboru v GroupDocs redaction Java
type: docs
url: /cs/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Jak přidat příponu k názvu souboru v GroupDocs Redaction Java

V tomto **groupdocs redaction java tutorial** se naučíte, jak automaticky připojit příponu k názvu výstupního souboru při redakci dokumentů pomocí GroupDocs.Redaction. Přidání přípony eliminuje ruční přejmenování, snižuje riziko úniku neredigovaných souborů a hladce zapadá do CI/CD pipeline, které se spoléhají na pojmenovací konvence. Průvodce vás provede nastavením Maven, načítáním dokumentu pomocí streamu, odstraněním anotací a konfigurací možností uložení — vše s stručným, produkčně připraveným kódem.

## Rychlé odpovědi
- **Co dělá „add suffix to filename“?**  
  Když povolíte možnost přípony, SDK automaticky připojí předdefinovaný řetězec (ve výchozím nastavení “_redacted”) k základnímu názvu výstupního souboru před příponou. To okamžitě ukazuje, které soubory byly zpracovány, pomáhá předcházet neúmyslnému šíření původního obsahu a zjednodušuje následnou automatizaci, která se spoléhá na pojmenovací vzory.  
- **Mohu načíst dokument ze streamu?**  
  Ano — GroupDocs.Redaction podporuje načítání z libovolného `InputStream`, což je ideální pro cloudové úložiště nebo zpracování v paměti.  
- **Potřebuji licenci pro tuto funkci?**  
  Bezplatná zkušební verze funguje pro základní redakci; dočasná nebo plná licence odemkne všechny pokročilé možnosti, včetně zpracování přípony.  
- **Jaké formáty jsou podporovány?**  
  Knihovna pracuje s DOCX, PDF, PPTX, XLSX a mnoha dalšími.  
- **Je rasterizace vyžadována pro výstup PDF?**  
  Rasterizace je volitelná; povolte ji, když potřebujete dokument zploštit pro vyšší zabezpečení.

## Co dělá „add suffix to filename“?

Když povolíte možnost přípony, SDK automaticky připojí předdefinovaný řetězec (ve výchozím nastavení “_redacted”) k základnímu názvu výstupního souboru před příponou. To okamžitě ukazuje, které soubory byly zpracovány, pomáhá předcházet neúmyslnému šíření původního obsahu a zjednodušuje následnou automatizaci, která se spoléhá na pojmenovací vzory.

## Proč použít GroupDocs.Redaction pro tento úkol?

GroupDocs.Redaction nabízí vysoce výkonný Java API, který kombinuje redakční akce s flexibilními možnostmi manipulace se soubory, jako je automatické přidání přípony, podpora streamování a dávkové zpracování. Podporuje více než 50 vstupních a výstupních formátů a dokáže zpracovat dokumenty o stovkách stránek bez načítání celého souboru do paměti, což zajišťuje nízkou spotřebu paměti a rychlé provedení.

## Požadavky

- **Java Development Kit (JDK):** Verze 8 nebo vyšší.  
- **GroupDocs.Redaction Library:** Hlavní knihovna pro úlohy redakce.  
- **IDE:** IntelliJ IDEA, Eclipse nebo jakýkoli Java‑kompatibilní editor.  
- **Maven:** Pro správu závislostí.  

### Předpoklady znalostí
Znalost Java I/O a základních objektově orientovaných konceptů usnadní sledování příkladů.

## Nastavení GroupDocs.Redaction pro Java

### Nastavení Maven
Do svého souboru `pom.xml` vložte následující konfiguraci pro přístup ke knihovnám GroupDocs pomocí Maven:

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
Alternativně stáhněte nejnovější verzi přímo z [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Získání licence
1. **Free trial:** Přístup k základní funkčnosti bez omezení.  
2. **Temporary license:** Získejte dočasnou licenci pro prozkoumání pokročilých funkcí.  
3. **Purchase:** Pro dlouhodobé používání zvažte zakoupení plné licence.

#### Základní inicializace a nastavení
Inicializujte svůj projekt přidáním potřebných importů:

```java
import com.groupdocs.redaction.Redactor;
```

S tímto nastavením jste připraveni implementovat funkce redakce dokumentů.

## Průvodce implementací

### Funkce 1: načíst dokument ze streamu
**Přehled:** Naučte se, jak načíst dokumenty do `InputStream` pro zpracování.

`InputStream` je třída Java I/O, která představuje proud bajtů a umožňuje číst data ze souborů, síťových připojení nebo jiných zdrojů, aniž byste načítali celý obsah do paměti.

#### Krok 1.1: vytvořit inputstream

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

- **Proč:** Použití `InputStream` vám umožňuje pracovat s dokumenty uloženými na různých místech — cloudových bucketách, databázích nebo v‑paměťových bufferech — aniž byste je nejprve zapisovali na disk. Tento přístup je nezbytný, když potřebujete **load document from stream** v mikro‑servisních architekturách.

### Funkce 2: aplikovat odstranění anotací redakcí
**Přehled:** Odstraňte anotace ze svého dokumentu pomocí `DeleteAnnotationRedaction`.

`DeleteAnnotationRedaction` je redakční operace, která odstraňuje všechny anotace — jako jsou komentáře, zvýraznění a poznámky — z dokumentu.

#### Krok 2.1: aplikovat deleteannotationredaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Proč:** Tento krok zajišťuje, že všechny citlivé anotace (komentáře, zvýraznění nebo skryté poznámky) jsou z dokumentu odstraněny, což zvyšuje soukromí a soulad s předpisy.

### Funkce 3: uložit dokument s možnostmi
**Přehled:** Naučte se, jak uložit svůj zpracovaný dokument s konkrétními možnostmi, jako je rasterizace a **add suffix filename java**.

`SaveOptions` zapouzdřuje nastavení, která řídí, jak je redigovaný dokument zapsán, včetně formátu, rasterizace a pojmenovacích konvencí.

#### Krok 3.1: nakonfigurovat saveoptions

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

- **Proč:** Přizpůsobení možností uložení umožňuje flexibilní výstupní formáty a pojmenovací konvence. Povolením `setAddSuffix(true)` **adds suffix to filename**, čímž je jasné, že soubor byl redigován.

## Jak přidat příponu k názvu souboru v Java při ukládání dokumentu?

Třída `Redactor` je hlavní komponentou, která načítá dokument a aplikuje redakční operace. `SaveOptions` definuje, jak je redigovaný dokument uložen, včetně formátu, rasterizace a pojmenovacích konvencí. Vytvořte instanci `Redactor`, aplikujte požadované redakce a poté nakonfigurujte objekt `SaveOptions` s `setAddSuffix(true)`. Zavolejte `redactor.save(outputPath, options)`. SDK automaticky připojí “_redacted” (nebo nakonfigurovanou příponu) k názvu souboru, takže jej nikdy nemusíte ručně přejmenovávat.

## Přehled závislosti GroupDocs Maven

**groupdocs maven dependency** přináší celé Redaction SDK do vašeho projektu jedním záznamem `<dependency>`. Spravuje tranzitivní závislosti, udržuje knihovny aktuální a zjednodušuje automatizaci sestavení. Deklarací závislosti v `pom.xml` se vyhnete ručnímu řízení JAR souborů a zajistíte kompatibilitu s nejnovějšími bezpečnostními záplatami.

## Proč je přidání přípony důležité

Přidání přípony poskytuje okamžité vizuální potvrzení, že soubor byl zpracován, což je klíčové pro auditní stopy, automatizované pracovní postupy a regulatorní soulad. Umožňuje skriptům filtrovat redigované soubory, zabraňuje neúmyslnému šíření původního obsahu a splňuje mnoho průmyslových standardů, které vyžadují jasné označení sanitovaných dokumentů.

## Praktické aplikace

1. **Redakce právních dokumentů:** Zabezpečte smlouvy před sdílením s klientem.  
2. **Zpracování lékařských záznamů:** Chraňte identifikátory pacientů při zachování klinických dat.  
3. **Finanční výkaznictví:** Udržujte citlivá čísla důvěrná během externích auditů.  
4. **Integrace CRM:** Automaticky odstraňte zákaznická data před exportem do nástrojů třetích stran.  
5. **Nástroje pro spolupráci:** Zajistěte, aby sdílené koncepty nikdy neodhalily skryté komentáře nebo metadata.

## Úvahy o výkonu

### Optimalizace výkonu
- Používejte streamování (`load document from stream`) k zabránění načítání celých souborů do paměti.  
- Okamžitě uzavřete instance `Redactor`, aby se uvolnily zdroje.  

### Pokyny pro využití zdrojů
- Sledujte CPU a paměť během dávkových běhů.  
- Upřednostňujte `ByteArrayOutputStream` pro ukládání v paměti při práci s menšími velikostmi souborů.  

### Nejlepší postupy pro správu paměti v Java
- Znovu používejte objekty `Redactor` při zpracování více souborů stejného typu.  
- Vyvolejte `close()` v bloku `try‑with‑resources`, aby se zabránilo únikům.  

## Časté problémy a řešení
| Problém | Příčina | Řešení |
|-------|-------|-----|
| **Přípona se nezobrazuje** | `setAddSuffix(false)` nebo chybějící volání | Ujistěte se, že `options.setAddSuffix(true)` je nastaveno před `save()`. |
| **OutOfMemoryError u velkého DOCX** | Načítání celého souboru do paměti | Přepněte na načítání pomocí `InputStream` (viz Funkce 1). |
| **Anotace jsou stále viditelné** | Redakce nebyla aplikována před uložením | Zavolejte `redactor.apply(new DeleteAnnotationRedaction())` před `save()`. |
| **Rasterizace PDF nebyla použita** | `setRasterizeToPDF(false)` nebo vynecháno | Nastavte `options.setRasterizeToPDF(true)`, když potřebujete zploštělý PDF. |

## Často kladené otázky

**Q: Can I redact PDF documents using GroupDocs.Redaction?**  
A: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.

**Q: What is the best way to handle large files with GroupDocs.Redaction?**  
A: Use streaming (`load document from stream`) and close resources promptly to keep memory usage low.

**Q: Is it possible to customize the suffix text?**  
A: The API automatically adds a default suffix (e.g., “_redacted”). For custom suffixes, rename the output file after saving.

**Q: How do I obtain a temporary license for GroupDocs.Redaction?**  
A: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/) and follow the instructions.

**Q: Where can I get help if I encounter issues?**  
A: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) for expert assistance.

## Zdroje
- **Dokumentace:** Prozkoumejte podrobné průvodce na [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **Reference API:** Získejte podrobné informace o API na [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Stáhnout:** Získejte nejnovější verzi z [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub repozitář:** Přispívejte nebo prozkoumejte zdrojový kód na [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Poslední aktualizace:** 2026-11-02  
**Testováno s:** GroupDocs.Redaction 24.9 pro Java  
**Autor:** GroupDocs  

## Související tutoriály

- [Převést Word na PDF a uložit redigované dokumenty pomocí GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Náhled stránek dokumentu Java načítání s GroupDocs.Redaction](/redaction/java/document-loading/)
- [Pokročilé techniky redakce pro GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)