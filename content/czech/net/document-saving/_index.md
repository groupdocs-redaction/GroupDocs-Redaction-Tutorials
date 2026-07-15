---
date: 2026-06-11
description: Zjistěte, jak exportovat redigované soubory, nastavit output folders,
  vytvořit rasterized PDFs a ukládat do streams pomocí GroupDocs.Redaction pro .NET.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: Jak exportovat redigované dokumenty pomocí GroupDocs.Redaction .NET
type: docs
url: /cs/net/document-saving/
weight: 3
---

# Jak exportovat redigované dokumenty pomocí GroupDocs.Redaction .NET

V tomto komplexním průvodci objevíte **jak exportovat redigované** obsahy bezpečně a efektivně pomocí GroupDocs.Redaction pro .NET. Ať už potřebujete zachovat původní typ souboru, uzamknout dokument jako rasterizované PDF nebo streamovat výsledek přímo v paměti, provedeme vás všemi možnostmi s jasnými, konverzačními vysvětleními a praktickými tipy. Na konci tohoto tutoriálu budete schopni vybrat správnou strategii exportu pro jakýkoli scénář řízený shodou.

## Rychlé odpovědi
- **Do jakých formátů mohu exportovat?** Jakýkoli z více než 30 nativních formátů podporovaných GroupDocs.Redaction, plus rasterizovaný PDF pro maximální bezpečnost.  
- **Potřebuji licenci pro streamování?** Ano, platná licence GroupDocs.Redaction je vyžadována pro produkční streamování.  
- **Mohu nastavit vlastní výstupní složku?** Rozhodně – použijte vlastnost `OutputPath` nebo `SaveOptions` pro její nastavení.  
- **Je rasterizace bezpečná pro velké soubory?** Zpracovává dokumenty až do 500 stránek, aniž by načítala celý soubor do paměti.  
- **Které verze .NET jsou podporovány?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Co je GroupDocs.Redaction?
GroupDocs.Redaction je .NET knihovna, která programově odstraňuje nebo maskuje citlivé informace z PDF, Word, Excel, PowerPoint, obrázků a mnoha dalších formátů. Nabízí vysoceúrovňové API pro definování redakčních oblastí, aplikaci zásad a nakonec export vyčištěného dokumentu. To usnadňuje integraci funkcí redakce do jakékoli .NET aplikace.

## Proč exportovat redigované dokumenty jako rasterizované PDF?
Rasterizované PDF převádějí každou stránku na plochý obrázek, čímž odstraňují skryté textové vrstvy, které by mohly být později extrahovány. Tento formát zaručuje, že redigovaný obsah nelze obnovit, a splňuje přísné regulační standardy jako GDPR a HIPAA. GroupDocs.Redaction může vytvářet rasterizované PDF až do 300 dpi, zachovávající vizuální věrnost a zároveň zajišťující bezpečnost.

## Jak exportovat redigované dokumenty?
Načtěte zdrojový soubor, aplikujte své redakční pravidla a poté zavolejte příslušnou metodu uložení – buď `Save` pro původní formát, `SaveAsRasterizedPdf` pro PDF pouze s obrázky, nebo `SaveToStream` pro zpracování v paměti. Níže je krok‑za‑krokem workflow. Každá metoda zajišťuje, že redigovaný obsah je trvale odstraněn při zachování požadovaného výstupního formátu.

### Krok 1: Instalace NuGet balíčku
Add the latest GroupDocs.Redaction package to your project:

```bash
dotnet add package GroupDocs.Redaction
```

### Krok 2: Načtení dokumentu a definování redakcí
Vytvořte instanci `Redactor`, načtěte soubor a určete oblasti, které chcete skrýt. Třída `Redactor` poskytuje základní funkčnost pro načítání dokumentů a aplikaci redakčních pravidel.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Krok 3: Výběr metody exportu
#### Export v původním formátu
```csharp
redactor.Save("RedactedReport.docx");
```

#### Export jako rasterizované PDF
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Export do paměťového proudu (ideální pro webové API)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

Metoda `Save` zapíše redigovaný dokument do souboru v jeho původním formátu. `SaveAsRasterizedPdf` vytvoří PDF, kde je každá stránka vykreslena jako obrázek, čímž odstraní jakýkoli skrytý text. `SaveToStream` vrátí redigovaný soubor jako paměťový proud, vhodný pro webové odpovědi.

## Jak nastavit výstupní složku?
Nastavte vlastnost `OutputPath` na objektu `Redactor` nebo předávejte vlastní objekt `SaveOptions`, který obsahuje požadovaný adresář. `OutputPath` je vlastnost třídy `Redactor`, která určuje adresář, kam jsou zapisovány výstupní soubory. `SaveOptions` vám umožňuje přizpůsobit různé parametry ukládání, včetně výstupní složky. To zajišťuje, že všechny exportované soubory skončí na předvídatelném místě, což zjednodušuje dávkové zpracování. Můžete také specifikovat podadresáře podle typu dokumentu, aby byl váš pracovní prostor uspořádán.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Časté problémy a řešení
- **Redakce nebyla aplikována:** Ověřte, že vyhledávací vzor přesně odpovídá textu v dokumentu; v případě potřeby použijte `RegexOptions.IgnoreCase`. `RegexOptions` je výčtový typ, který řídí chování regulárních výrazů, například rozlišování velkých a malých písmen.  
- **Velké soubory způsobují tlak na paměť:** Aktivujte režim streamování pomocí `SaveToStream` a vyhněte se volání `Save` na celý dokument.  
- **Rasterizované PDF vypadá rozmazaně:** Zvyšte DPI v `RasterizationOptions` (např. 300–600) pro zlepšení kvality obrazu. `RasterizationOptions` umožňuje nastavit parametry jako DPI a formát obrázku pro výstup rasterizovaného PDF.

## Často kladené otázky

**Q: Mohu exportovat do formátu, který nebyl původně podporován?**  
A: Ano, GroupDocs.Redaction může převést většinu vstupních typů na PDF, DOCX, XLSX, PPTX nebo rasterizované PDF, pokrývající více než 30 formátů.

**Q: Jak rasterizace chrání redigovaná data?**  
A: Renderováním každé stránky jako plochého obrazu jsou odstraněny všechny skryté textové vrstvy, což znemožňuje extrahovat původní obsah.

**Q: Je možné řetězit více redakčních pravidel?**  
A: Rozhodně – můžete volat `Apply` opakovaně nebo předat kolekci `RedactionOptions` pro zpracování mnoha vzorů najednou. `RedactionOptions` definuje nastavení pro jednu redakční operaci, jako je oblast a typ nahrazení.

**Q: Musím uzavřít objekt Redactor?**  
A: `Redactor` implementuje `IDisposable`; obalte jej v bloku `using` nebo zavolejte `Dispose()`, aby se rychle uvolnily souborové handle. `IDisposable` je rozhraní, které poskytuje mechanismus pro uvolnění neřízených zdrojů.

**Q: Jaké .NET runtime jsou oficiálně testovány?**  
A: GroupDocs.Redaction je ověřen na .NET Framework 4.6+, .NET Core 3.1+, a .NET 5/6/7.

## Další zdroje

### Dostupné tutoriály

- [Jak uložit dokumenty jako rasterizované PDF pomocí GroupDocs.Redaction pro .NET: Kompletní průvodce](./groupdocs-redaction-net-rasterized-pdfs/)
- [Implementace výstupního adresáře v .NET s GroupDocs.Redaction: Komplexní průvodce](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Redigování a ukládání dokumentů pomocí GroupDocs.Redaction pro .NET: Kompletní průvodce](./redact-save-documents-groupdocs-redaction-net/)
- [Uložení redigovaných dokumentů v původním formátu pomocí GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Bezpečné redigování dokumentů v .NET pomocí streamů: Průvodce pro GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Užitečné odkazy

- [Dokumentace GroupDocs.Redaction pro .NET](https://docs.groupdocs.com/redaction/net/)
- [API reference GroupDocs.Redaction pro .NET](https://reference.groupdocs.com/redaction/net/)
- [Stáhnout GroupDocs.Redaction pro .NET](https://releases.groupdocs.com/redaction/net/)
- [Fórum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Bezplatná podpora](https://forum.groupdocs.com/)
- [Dočasná licence](https://purchase.groupdocs.com/temporary-license/)

---

**Poslední aktualizace:** 2026-06-11  
**Testováno s:** GroupDocs.Redaction 23.11 pro .NET  
**Autor:** GroupDocs  

## Související tutoriály

- [Uložení redigovaných dokumentů v původním formátu pomocí GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Jak uložit dokumenty jako rasterizované PDF pomocí GroupDocs.Redaction pro .NET: Kompletní průvodce](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Bezpečné redigování dokumentů v .NET pomocí streamů: Průvodce pro GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)