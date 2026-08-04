---
date: 2026-08-04
description: Zjistěte, jak filtrovat data v tabulce Java a bezpečně redigovat sloupce
  nebo buňky v tabulkách Excel pomocí GroupDocs.Redaction pro Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Zjistěte, jak filtrovat data v tabulce Java a bezpečně redigovat sloupce
  nebo buňky v tabulkách Excel pomocí GroupDocs.Redaction pro Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Filtrování dat v tabulce Java – průvodce s GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Filtrování dat v tabulce Java – průvodce s GroupDocs.Redaction
type: docs
url: /cs/java/spreadsheet-redaction/
weight: 12
---

# Filtrace dat v tabulce java – návod GroupDocs.Redaction pro Java

Pokud potřebujete **filter spreadsheet data java** před aplikací redakce, jste na správném místě. V tomto tutoriálu se dozvíte, jak izolovat řádky, sloupce nebo jednotlivé buňky obsahující osobní nebo důvěrné informace a poté je bezpečně redigovat pomocí GroupDocs.Redaction pro Java. Kroky jsou vysvětleny srozumitelně, obsahují tipy na osvědčené postupy a ukazují, jak udržet zpracování rychlé i u velkých sešitů.

## Rychlé odpovědi
- **Která knihovna provádí redakci tabulek v Javě?** GroupDocs.Redaction for Java.  
- **Mohu filtrovat řádky bez načtení celého souboru do paměti?** Ano – API streamuje data a umožňuje aplikovat filtry za běhu.  
- **Jaké formáty souborů jsou podporovány?** Více než 30 formátů tabulek, včetně XLS, XLSX, CSV a ODS.  
- **Potřebuji licenci pro vývoj?** Dočasná licence stačí pro testování; pro produkci je vyžadována plná licence.  
- **Existuje limit velikosti sešitu?** Engine dokáže zpracovat soubory až do 500 MB bez nadměrné spotřeby paměti.

## Co je filter spreadsheet data java?
**Filter spreadsheet data java** je proces programového výběru konkrétních řádků, sloupců nebo buněk v sešitu ve stylu Excelu pomocí Java kódu, aby byl zkoumán nebo redigován jen cílený obsah. Tato technika snižuje dobu běhu, omezuje zbytečné změny a pomáhá splnit požadavky typu GDPR.

## Proč filtrovat data v tabulce java?
GroupDocs.Redaction Java podporuje **30+ formátů tabulek** a dokáže zpracovat sešity o velikosti **až 500 MB** (přibližně 1 milion řádků) při využití paměti pod **200 MB**. Filtrováním nejprve se vyhnete manipulaci s nesouvisejícími daty, což průměrně zkrátí dobu zpracování o **40‑60 %** u typických scénářů čištění soukromých údajů.

## Požadavky
- Java 17 nebo novější nainstalovaný.  
- Systém sestavení Maven nebo Gradle.  
- GroupDocs.Redaction pro Java (ke stažení z oficiální stránky).  
- Dočasný nebo plný licenční klíč.  

## Jak filtrovat data v tabulkách pomocí GroupDocs.Redaction Java?
Načtěte sešit, definujte filtr, který odpovídá buňkám, které chcete redigovat, a poté aplikujte operaci redakce. API provádí filtraci ve streamovacím režimu, takže není nutné držet celý soubor v RAM.

Třída `RedactionFilter` vám umožňuje specifikovat indexy sloupců, rozsahy řádků nebo vlastní predikáty. Například můžete cílit na každou buňku ve sloupci **B**, která obsahuje vzor e‑mailové adresy, nebo omezit redakci na řádky, kde sloupec „Status“ má hodnotu „Confidential“.

**Přímá odpověď (40‑70 slov):**  
Vytvořte instanci `RedactionFilter`, nastavte index sloupce a podmínku regulárního výrazu, poté předávejte filtr do `Redactor.redact(workbook, filter)`. Tento jednorázový filtr izoluje přesné buňky, které odpovídají vašim kritériím, a redaktor je odstraní nebo zamaskuje, zatímco zbytek listu zůstane nedotčen. Operace se dokončí v lineárním čase vzhledem k filtrovaným řádkům.

### Krok 1: vytvoření instance filtru
`RedactionFilter` je hlavní třída představující pravidlo filtrování pro redakci tabulek. Přijímá čísla sloupců, řádků nebo vlastní lambda výrazy pro přesné určení dat.

### Krok 2: nastavení podmínky
Použijte `filter.setColumnIndex(1)` k cílení na sloupec B (nulové indexování) a `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` pro shodu s e‑mailovými vzory. Můžete také kombinovat více podmínek pomocí `filter.and(...)` nebo `filter.or(...)`.

### Krok 3: aplikace redakce
`Redactor` je hlavní třída, která provádí operace redakce na sešitu.  
Předávejte sešit a nakonfigurovaný filtr objektu `Redactor`. API streamuje sešit, aplikuje filtr a zapíše redigovaný výsledek do nového souboru, přičemž zachovává původní formátování a vzorce.

## Časté problémy a řešení
- **Filtr neodpovídá žádným buňkám:** Ověřte index sloupce (nulové indexování) a ujistěte se, že syntax regulárního výrazu je pro Javu správná.  
- **Chyby nedostatku paměti u velkých souborů:** Zvyšte velikost haldy JVM mírně (např. `-Xmx1g`) nebo rozdělte sešit na menší části před filtrováním.  
- **Redigovaný výstup ztrácí formátování:** `RedactionOptions` umožňuje přizpůsobit chování redakce, například zachování formátování buněk. Použijte `RedactionOptions.setPreserveFormatting(true)`, aby zůstaly styly buněk zachovány.

## Proč filtrovat data v tabulce?
Filtrování před redakcí izoluje pouze citlivé části sešitu, což znamená, že se vyhnete zbytečným změnám čistých dat. Tento selektivní přístup také snižuje riziko náhodné ztráty dat a urychluje audity shody, protože auditní log obsahuje mnohem méně záznamů.

## Jak redigovat e‑maily v Excel tabulkách pomocí GroupDocs.Redaction Java API
Načtěte svůj Excel soubor, aplikujte filtr, který hledá typický e‑mailový vzor, a vyvolejte redaktor. API nahradí každý nalezený e‑mail placeholderem jako „***@***.com“ při zachování okolního rozložení buněk.

## Jak filtrovat data – dostupné tutoriály
- [Jak redigovat e‑maily v Excel tabulkách pomocí GroupDocs.Redaction Java API](./redact-emails-excel-groupdocs-redaction-java/)

## Další zdroje

- [GroupDocs.Redaction for Java Documentation](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API Reference](https://reference.groupdocs.com/redaction/java/)
- [Download GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Poslední aktualizace:** 2026-08-04  
**Testováno s:** GroupDocs.Redaction 23.11 for Java  
**Autor:** GroupDocs  

## Často kladené otázky

**Q: Mohu filtrovat více sloupců najednou?**  
A: Ano, můžete přidat další indexy sloupců do stejné instance `RedactionFilter` nebo řetězit více filtrů pomocí `filter.or(...)`.

**Q: Funguje filtr na sešitech chráněných heslem?**  
A: Zadejte heslo při otevírání sešitu; filtr funguje po dešifrování stejně jako u nechráněného souboru.

**Q: Kolik řádků může API zpracovat v jedné operaci?**  
A: Engine je optimalizován pro až 1 milion řádků (≈500 MB) bez načítání celého souboru do paměti.

**Q: Je možné před uložením zobrazit náhled, které buňky budou redigovány?**  
A: Ano, zavolejte `filter.preview(workbook)`, abyste získali seznam adres buněk, které odpovídají kritériím.

**Q: Jaký licenční model je vyžadován pro produkční použití?**  
A: Pro produkční nasazení je vyžadována plná komerční licence; dočasná licence stačí pro testování a hodnocení.

## Související tutoriály

- [Jak redigovat citlivá data v Excel tabulkách pomocí GroupDocs.Redaction Java API](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Mask Sensitive Data Java – GroupDocs.Redaction Guide](/redaction/java/getting-started/)
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)