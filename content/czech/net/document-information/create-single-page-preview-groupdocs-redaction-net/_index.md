---
date: '2026-06-06'
description: Zjistěte, jak převést stránku na PNG a zobrazit náhled PDF stránek pomocí
  GroupDocs.Redaction pro .NET. Podrobný návod krok za krokem, ukázky kódu a praktické
  tipy.
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: Převést stránku na PNG pomocí GroupDocs.Redaction .NET
type: docs
url: /cs/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# Převod stránky na PNG pomocí GroupDocs.Redaction .NET

Vytvoření náhledu jedné stránky z velkého dokumentu je běžná potřeba, když chcete sdílet jen relevantní část informací. V tomto tutoriálu se naučíte **jak převést stránku na PNG** pomocí GroupDocs.Redaction pro .NET, nakonfigurovat výstup náhledu a integrovat výsledek do vašich aplikací. Provedeme vás předpoklady, instalací, nastavením kódu a praktickými tipy, abyste během několika minut mohli začít generovat náhledy PNG jedné stránky.

## Rychlé odpovědi
- **Mohu vygenerovat PNG náhled pouze jedné stránky?** Ano, použijte `PreviewOptions` k určení čísla stránky a formátu.  
- **Jaký formát GroupDocs.Redaction podporuje pro náhledy?** PNG je výchozí, ale JPEG a BMP jsou také k dispozici.  
- **Potřebuji licenci pro vývoj?** Bezplatná zkušební verze funguje pro testování; pro komerční použití je vyžadována produkční licence.  
- **Bude to fungovat na .NET Core i .NET Framework?** Rozhodně – knihovna cílí na .NET Standard 2.0+.  
- **Je proces paměťově efektivní pro velké soubory?** Ano, API streamuje stránky, čímž se vyhýbá načítání celého dokumentu.

## Co je převod stránky na PNG?
**convert page to PNG** odkazuje na extrakci jedné stránky z podporovaného dokumentu (PDF, DOCX, PPTX atd.) a vykreslení této stránky jako obrázku Portable Network Graphics (PNG). Výsledný obrázek zachovává vizuální rozvržení, písma a grafiku původní stránky, což vám umožní sdílet jasný snímek a zároveň skrýt zbytek dokumentu.

## Proč použít náhled jedné stránky?
Vytvoření PNG náhledu jedné stránky snižuje šířku pásma, urychluje načítání a chrání citlivý obsah tím, že odhalí jen to, co je potřeba. GroupDocs.Redaction dokáže vykreslit 300‑stránkový PDF do 200 KB PNG za méně než 0,5 sekundy na typickém serverovém hardware, což je ideální pro webové portály a nástroje pro reportování.

## Předpoklady

- **GroupDocs.Redaction for .NET** – základní knihovna, která provádí redakci dokumentů a generování náhledů.  
- **System.IO** – standardní .NET jmenný prostor pro práci se soubory.  
- .NET Core 3.1+ nebo .NET Framework 4.6.1+ (jakákoliv platforma podporující .NET Standard 2.0).  
- Základní znalost C# a seznámení s řízením balíčků NuGet.

## Nastavení GroupDocs.Redaction pro .NET

### Informace o instalaci

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**
- Otevřete svůj projekt ve Visual Studiu.  
- Zvolte **Manage NuGet Packages**.  
- Vyhledejte **GroupDocs.Redaction** a nainstalujte nejnovější stabilní verzi.

### Kroky pro získání licence
Pro spuštění knihovny potřebujete platnou licenci. Můžete začít s bezplatnou zkušební verzí nebo požádat o dočasný klíč:

1. Navštivte [GroupDocs website](https://purchase.groupdocs.com/temporary-license) a požádejte o dočasnou licenci.  
2. Postupujte podle instrukcí zaslaných e-mailem a přidejte licenční soubor do svého projektu.

### Základní inicializace a nastavení
Třída `RedactionEngine` je vstupním bodem pro všechny operace, včetně generování náhledů.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## Průvodce implementací

### Přehled
Tato sekce ukazuje, jak **convert page to PNG** pomocí konfigurace `PreviewOptions` a volání preview API. Přístup funguje pro PDF, DOCX, PPTX a mnoho dalších formátů podporovaných GroupDocs.Redaction.

### Krok 1: Připravte své prostředí
Nastavte cestu ke zdrojovému souboru a výstupní složku. Použijte `Path.Combine` pro vytvoření platformně nezávislých cest.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### Krok 2: Nastavte možnosti náhledu
`PreviewOptions` vám umožňuje definovat číslo stránky, velikost obrázku a výstupní formát. Třída je konfiguračním střediskem pro generování náhledů.  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### Vysvětlení klíčových konfigurací
- **Width & Height** – Upravte tyto hodnoty tak, aby odpovídaly cílovému rozlišení displeje.  
- **PageNumbers** – Poskytněte pole s přesným indexem stránky, kterou chcete vykreslit (číslování od nuly).  
- **PreviewFormat** – PNG je výchozí; přepněte na `PreviewFormat.Jpeg` pro menší soubory.

### Tipy pro řešení problémů
Pokud PNG není vygenerováno:

- Ověřte, že cesta ke zdrojovému souboru je správná a soubor je přístupný.  
- Ujistěte se, že licenční soubor je načten před voláním jakékoli metody API.  
- Potvrďte, že `PreviewOptions.PageNumbers` obsahuje platný index stránky (např. `0` pro první stránku).

## Praktické aplikace
Vytvoření PNG náhledu jedné stránky je užitečné v mnoha scénářích:

1. **Client Presentations** – Zobrazte pouze relevantní snímek nebo smluvní ustanovení.  
2. **Internal Reviews** – Umožněte rychlé vizuální kontroly bez otevření celého dokumentu.  
3. **Content Summaries** – Vložte snímky stránek do e‑mailů nebo dashboardů pro okamžitý kontext.  

Integrace této funkce s CMS nebo CRM může automatizovat generování miniatur pro nahrané dokumenty, čímž se zlepší uživatelská zkušenost.

## Úvahy o výkonu
- **Memory Management** – Uvolněte instance `RedactionEngine` po použití, aby se uvolnily zdroje.  
- **Asynchronous Execution** – Použijte `await engine.GeneratePreviewAsync(...)` v UI aplikacích, aby rozhraní zůstalo responzivní.  
- **Library Updates** – GroupDocs.Redaction podporuje **30+ vstupních a výstupních formátů** a zpracovává dokumenty až do 500 stránek bez načítání celého souboru do paměti. Udržujte balíček aktualizovaný, abyste těžili z vylepšení výkonu.

## Závěr
Nyní máte kompletní, připravenou metodu pro **convert page to PNG** a generování náhledů jedné stránky pomocí GroupDocs.Redaction pro .NET. Dodržením výše uvedených kroků můžete vložit vysoce kvalitní PNG snímky do jakékoli .NET aplikace, čímž zlepšíte sdílení dokumentů při zachování bezpečnosti a výkonu.

## Často kladené otázky

**Q: Mohu generovat náhledy pro PDF chráněné heslem?**  
A: Ano, při inicializaci `RedactionEngine` poskytněte heslo a náhled bude vytvořen normálně.

**Q: Jak změním výstupní formát z PNG na JPEG?**  
A: Nastavte `options.PreviewFormat = PreviewFormat.Jpeg` před voláním metody pro náhled.

**Q: Je možné zobrazit více stránek najednou?**  
A: Rozhodně – přiřaďte pole čísel stránek do `options.PageNumbers` (např. `new[] {0, 2, 4}`).

**Q: Co mám dělat, když je obrázek náhledu rozmazaný?**  
A: Zvyšte `options.Width` a `options.Height` na vyšší rozlišení; knihovna obrázek podle toho škáluje.

**Q: Funguje to v Linuxových kontejnerech?**  
A: Ano, GroupDocs.Redaction .NET je multiplatformní a běží v Docker kontejnerech, které podporují .NET Core.

## Zdroje
- [Dokumentace](https://docs.groupdocs.com/redaction/net/)
- [Reference API](https://reference.groupdocs.com/redaction/net)
- [Stáhnout nejnovější verzi](https://releases.groupdocs.com/redaction/net/)
- [Bezplatné fórum podpory](https://forum.groupdocs.com/c/redaction/33)
- [Získání dočasné licence](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Redaction 5.6 for .NET  
**Author:** GroupDocs

## Související tutoriály

- [Ovládání zabezpečení dokumentů: rasterizace a redakce Word dokumentů s GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)
- [Jak odstranit stránky z PDF pomocí GroupDocs.Redaction .NET: komplexní průvodce](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)
- [Implementace redakce dokumentů pomocí GroupDocs.Redaction .NET: krok za krokem](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)