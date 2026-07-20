---
date: '2026-07-20'
description: Naučte se, jak vypsat formáty pomocí GroupDocs.Redaction .NET, integrovat
  tuto funkci do vašeho dokumentového workflow a zlepšit výkon.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Objevte, jak vypsat formáty pomocí GroupDocs.Redaction .NET, podívejte
  se na podrobný návod a získejte tipy pro optimální výkon ve vašich .NET aplikacích.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Jak vypsat formáty pomocí GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: Jak vypsat formáty pomocí GroupDocs.Redaction .NET
type: docs
url: /cs/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Jak vypsat formáty pomocí GroupDocs.Redaction .NET

Správa široké škály typů dokumentů je každodenní realitou pro vývojáře, kteří vytvářejí aplikace zaměřené na dokumenty. V tomto tutoriálu se naučíte **jak vypsat formáty**, které GroupDocs.Redaction .NET dokáže zpracovat, abyste mohli před zpracováním ověřit soubory, uživatelům nabídnout přesné možnosti a udržet svůj pracovní postup efektivní.

## Úvod

Efektivní manipulace s dokumenty začíná tím, že přesně víte, které typy souborů vaše knihovna podporuje. GroupDocs.Redaction poskytuje vestavěnou metodu pro získání těchto informací, což vám umožní vytvářet dynamické UI prvky, vynucovat validační pravidla a vyhnout se chybám za běhu. Níže najdete vše, co potřebujete k zahájení práce, od instalace po praktické úryvky kódu a tipy na výkon.

### Rychlé odpovědi
- **Co znamená „jak vypsat formáty“?** Odkazuje na získání kolekce přípon souborů, které GroupDocs.Redaction dokáže zpracovat.  
- **Potřebuji licenci?** Ano, platná licence GroupDocs.Redaction je vyžadována pro produkční použití.  
- **Které verze .NET jsou podporovány?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Kolik formátů je k dispozici?** Více než 30 vstupních a výstupních formátů je podporováno out‑of‑the‑box.  
- **Je potřeba nějaká speciální konfigurace?** Žádná extra konfigurace není vyžadována nad rámec standardní inicializace knihovny.

## Co je „jak vypsat formáty“?

Jedná se o volání API FileType knihovny, které vrátí kolekci, kde každý záznam obsahuje příponu souboru a čitelný název. Vývojáři mohou tuto kolekci následně iterovat pro tvorbu validačních pravidel, naplnění rozbalovacích nabídek UI nebo zaznamenání podporovaných typů, čímž zajistí, že budou zpracovány jen kompatibilní dokumenty.

## Proč vypsat formáty pomocí GroupDocs.Redaction?

GroupDocs.Redaction podporuje **30+** různých typů souborů — včetně PDF, DOCX, PPTX a formátů obrázků — což vám umožní zpracovávat většinu podnikových dokumentů bez potřeby třetích konvertorů. Programatickým výpisem těchto formátů odstraníte hádání, snížíte počet požadavků na podporu a zajistíte, že do vašeho zpracovatelského řetězce vstoupí jen kompatibilní soubory.

## Požadavky

- **GroupDocs.Redaction pro .NET** – stáhněte nejnovější balíček z oficiálního webu.  
- **.NET Framework nebo .NET Core** – kompatibilní s vaším vývojovým prostředím.  
- **Visual Studio** (nebo jakékoli IDE kompatibilní s C#).  
- Základní znalost syntaxe C#.

## Nastavení GroupDocs.Redaction pro .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Správce balíčků
`Install-Package GroupDocs.Redaction`

### UI správce balíčků NuGet
- Vyhledejte **“GroupDocs.Redaction”** a nainstalujte nejnovější verzi.

### Získání licence
GroupDocs nabízí bezplatnou zkušební verzi, dočasnou licenci pro hodnocení nebo plné zakoupení. Navštivte web GroupDocs a získejte příslušný licenční soubor.

### Základní inicializace a nastavení
Po přidání balíčku odkažte na jmenný prostor a vytvořte instanci `Redactor`:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Průvodce implementací

### Jak vypsat formáty pomocí GroupDocs.Redaction .NET?
Načtěte knihovnu, zavolejte statický pomocník a seřaďte výsledky — získáte připravenou kolekci během dvou řádků kódu. Použijte `FileType.GetSupportedFileFormats()` k získání `IEnumerable<FileType>`, která obsahuje příponu a zobrazovaný název každého formátu, a poté seřaďte podle přípony pro čistý seznam UI.

### Získání podporovaných formátů souborů

#### Přehled
Cílem je získat seznam typů souborů, které GroupDocs.Redaction dokáže zpracovat, což usnadňuje integraci do validační logiky, rozbalovacích nabídek UI nebo logovacích mechanismů.

#### Krok za krokem implementace

**1. Získání podporovaných typů souborů**  
`FileType.GetSupportedFileFormats()` vrací všechny formáty, které knihovna rozpozná. Metoda je součástí třídy `GroupDocs.Redaction.FileType`, která zapouzdřuje metadata jako příponu souboru a přátelský název.

**2. Zobrazení podporovaných typů souborů**  
Iterujte přes kolekci a vypište každou příponu a popis formátu. Příklad kódu vložený inline:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

Úryvek vytiskne přehledně seřazený seznam jako “.pdf – Portable Document Format”, což je ideální pro naplnění UI prvků.

### Tipy pro řešení problémů
- **Missing Package** – Ověřte odkaz na NuGet balíček a v případě potřeby obnovte balíčky.  
- **Incorrect License Path** – Ujistěte se, že licenční soubor je zkopírován do výstupního adresáře nebo poskytněte absolutní cestu.  
- **Unsupported Extension** – Pokud formát není v seznamu, ověřte, že používáte nejnovější verzi knihovny; novější vydání přidávají další formáty.

## Praktické aplikace
Pochopení podporovaných formátů souborů otevírá několik reálných scénářů:

1. **Systémy správy dokumentů** – Ověřujte nahrané soubory proti seznamu podporovaných, aby nedocházelo k selhání zpracování.  
2. **Bezpečnost obsahu** – Používejte pravidla redakce jen na typy souborů, které engine může bezpečně upravit.  
3. **Dávkové zpracování** – Filtrovat velké dávky souborů před voláním redakce, čímž ušetříte CPU a paměť.

## Úvahy o výkonu
- **Paměťová náročnost** – Vypsání formátů je lehká operace; nenačítá žádný dokument do paměti.  
- **Dávkové operace** – Při zpracování stovek souborů načtěte seznam formátů jednou a znovu jej použijte, abyste se vyhnuli nadbytečným voláním.  
- **Bezpečnost vláken** – `FileType.GetSupportedFileFormats()` je bezpečná pro vlákna a může být volána z paralelních úloh bez synchronizace.

## Závěr
Nyní máte kompletní, připravený přístup pro **vypsání formátů** pomocí GroupDocs.Redaction .NET. Integrací této funkce můžete zlepšit validaci, vylepšit uživatelskou zkušenost a udržet své dokumentové pipeline robustní.

### Další kroky
- Prozkoumejte API `Redactor` pro aplikaci pravidel redakce na základě typu souboru.  
- Spojte seznam formátů s rozbalovacím seznamem na frontendu pro plynulé výběry souborů.  
- Projděte si průvodce výkonem pro optimalizaci velkých dávkových úloh.

## Často kladené otázky

**Q: Mohu získat seznam formátů bez inicializace instance Redactor?**  
A: Ano, `FileType.GetSupportedFileFormats()` je statická a nevyžaduje objekt `Redactor`.

**Q: Obsahuje seznam jak vstupní, tak výstupní formáty?**  
A: Metoda vrací všechny formáty, které knihovna dokáže jak číst, tak zapisovat; každý `FileType` obsahuje příznaky `CanRead` a `CanWrite`.

**Q: Jak často je seznam podporovaných formátů aktualizován?**  
A: GroupDocs vydává aktualizace formátů s každou verzí knihovny; kontrola seznamu za běhu zajišťuje, že máte vždy nejnovější sadu.

**Q: Existuje způsob, jak filtrovat jen PDF‑kompatibilní formáty?**  
A: Ano, filtrujte kolekci, kde `format.Extension == ".pdf"` nebo kde `format.Name.Contains("PDF")`.

**Q: Bude tento přístup fungovat na .NET Core 2.1?**  
A: Metoda vyžaduje .NET Core 3.1 nebo novější; starší runtime nejsou podporovány.

## Sekce FAQ
1. **Jak nainstaluji GroupDocs.Redaction pro .NET?**  
   Použijte příkaz CLI `dotnet add package GroupDocs.Redaction` nebo nainstalujte přes uživatelské rozhraní správce balíčků NuGet.  
2. **Jaké jsou běžné problémy při získávání podporovaných formátů?**  
   Ujistěte se, že jsou obnoveny všechny závislosti a že odkazujete na správný jmenný prostor (`GroupDocs.Redaction`).  
3. **Mohu tuto funkci použít s aplikacemi mimo .NET?**  
   Tento tutoriál se zaměřuje na .NET, ale GroupDocs poskytuje podobná API pro Javu, Python a další platformy.  
4. **Jak mohu optimalizovat výkon při používání GroupDocs.Redaction?**  
   Znovu použijte seznam formátů, vyhněte se načítání celých dokumentů, pokud kontrolujete jen kompatibilitu, a sledujte využití paměti během dávkových úloh.  
5. **Jaké typy souborů GroupDocs.Redaction podporuje?**  
   Knihovna podporuje více než 30 formátů, včetně PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG a mnoha dalších. Použijte `FileType.GetSupportedFileFormats()` pro zobrazení úplného seznamu.

## Zdroje
- [Dokumentace](https://docs.groupdocs.com/redaction/net/)
- [Reference API](https://reference.groupdocs.com/redaction/net)
- [Stáhnout GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Bezplatné fórum podpory](https://forum.groupdocs.com/c/redaction/33)
- [Dočasná licence](https://purchase.groupdocs.com/temporary-license/)

---

**Poslední aktualizace:** 2026-07-20  
**Testováno s:** GroupDocs.Redaction 4.2.0 for .NET  
**Autor:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## Související tutoriály

- [Tutoriály pro zpracování formátů pro GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Tutoriály načítání dokumentů s GroupDocs.Redaction pro .NET](/redaction/net/document-loading/)
- [Tutoriály ukládání dokumentů pro GroupDocs.Redaction .NET](/redaction/net/document-saving/)