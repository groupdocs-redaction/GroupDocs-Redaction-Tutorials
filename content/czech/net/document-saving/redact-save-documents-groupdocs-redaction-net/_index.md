---
date: '2026-07-20'
description: Naučte se, jak redigovat dokumenty, skrýt citlivé informace a uložit
  redigované soubory do paměťového proudu pomocí GroupDocs.Redaction pro .NET.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: Jak redigovat dokumenty pomocí GroupDocs.Redaction pro .NET. Postupujte
  podle tohoto krok‑za‑krokem průvodce, abyste skryli citlivé informace a uložili
  redigovaný soubor do paměťového proudu.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: Jak redigovat dokumenty pomocí GroupDocs.Redaction pro .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: Jak redigovat dokumenty pomocí GroupDocs.Redaction pro .NET – Kompletní průvodce
type: docs
url: /cs/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# Jak redigovat dokumenty pomocí GroupDocs.Redaction pro .NET

V moderních podnikových prostředích je **jak redigovat dokumenty** kritickou dovedností pro ochranu osobních údajů, obchodních tajemství a informací souvisejících s dodržováním předpisů. Tento průvodce vás provede redigováním citlivých informací z Word, PDF nebo obrazových souborů a následným uložením redigovaného výstupu přímo do paměťového proudu — vše pomocí GroupDocs.Redaction pro .NET.

## Rychlé odpovědi
- **Co dělá redakce?** Trvale nahrazuje vybraný obsah zástupným znakem nebo jej odstraňuje, čímž zajišťuje, že data nelze nikdy obnovit.  
- **Jaké formáty jsou podporovány?** Více než 30 typů souborů, včetně PDF, DOCX, PPTX a běžných formátů obrázků.  
- **Mohu redigovat bez zápisu na disk?** Ano — výsledek uložte do `MemoryStream` pro zpracování v paměti.  
- **Potřebuji licenci pro produkci?** Pro produkční použití je vyžadována plná licence; k vyzkoušení je k dispozici bezplatná zkušební verze.  
- **Je kompatibilní s .NET Core?** Naprosto — GroupDocs.Redaction funguje s .NET Framework 4.6+, .NET Core 3.1+ a .NET 5/6/7.

## Co je redakce dokumentu?
Redakce dokumentu trvale odstraňuje nebo zakrývá důvěrný text, obrázky a metadata ze souboru, čímž zajišťuje, že skrytý obsah nelze později obnovit, zobrazit ani extrahovat. Nahrazuje citlivé prvky zástupným znakem, například černým obdélníkem nebo vlastním textem, a aktualizuje strukturu dokumentu tak, aby redigovaná data byla neobnovitelná.

## Proč použít GroupDocs.Redaction k redigování dokumentů?
GroupDocs.Redaction podporuje **více než 30 formátů souborů** a dokáže zpracovávat soubory až do **2 GB** bez načítání celého dokumentu do paměti, což poskytuje **o 30 % rychlejší dobu zpracování** ve srovnání s mnoha konkurenty. Jeho API vám umožňuje aplikovat redakce na základě přesné fráze, regulárního výrazu nebo obrázku jedním voláním metody, což z něj činí nejefektivnější volbu pro .NET vývojáře.

## Předpoklady
- **GroupDocs.Redaction** NuGet balíček (nejnovější verze).  
- .NET Framework 4.6+ **nebo** .NET Core 3.1+ nainstalováno.  
- IDE kompatibilní s C#, například Visual Studio 2022.  
- Základní znalost C# a orientace v práci se soubory I/O.

### Požadované knihovny a verze
- **GroupDocs.Redaction** – vždy používejte nejnovější vydání pro přístup k nejnovějším redakčním algoritmům a bezpečnostním záplatám.  
- **System.IO** – pro práci s proudy (vestavěné v .NET).

### Kroky získání licence
- **Bezplatná zkušební verze:** Zaregistrujte se na webu GroupDocs a získejte 30‑denní zkušební verzi.  
- **Dočasná licence:** Požádejte o dočasný klíč pro testování vývoje.  
- **Plná licence:** Zakupte produkční licenci pro neomezené používání.

## Základní inicializace a nastavení
Třída `Redactor` je vstupním bodem pro všechny operace redakce v GroupDocs.Redaction. Po instalaci NuGet balíčku vytvoříte instanci `Redactor` s cestou ke zdrojovému dokumentu.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## Jak redigovat konkrétní text v dokumentu?
Pro redigování konkrétního textu načtěte zdrojový soubor pomocí instance `Redactor` a poté použijte `ExactPhraseRedaction`, která cílí na přesný řetězec, který chcete skrýt. API prohledá dokument, nahradí každou shodu vybraným překryvem a zaznamená změny do protokolu změn, což vám umožní ověřit redakci před uložením.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

Třída `ExactPhraseRedaction` nahrazuje každé výskyt přesné fráze černým obdélníkem (nebo libovolným vlastním zástupcem, který nakonfigurujete).  

**Krok za krokem:**
1. **Load** – Vytvořte instanci `Redactor`, která ukazuje na váš soubor.  
2. **Apply** – Zavolejte `Apply` s `ExactPhraseRedaction` (nebo jiným typem redakce).  
3. **Inspect** – Prohlédněte `RedactorChangeLog`, abyste potvrdili, kolik shod bylo nalezeno a nahrazeno.  

## Jak uložit redigovaný dokument do Memory Streamu?
`MemoryStream` je .NET proud, který ukládá data v paměti, což umožňuje rychlé čtení/zápis bez diskových I/O operací. Pomocí metody `Save` můžete směrovat redigovaný výstup do `MemoryStream`, který pak může být odeslán přes síť, uložen v databázi nebo vrácen přímo z API koncového bodu bez vytváření dočasných souborů.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**Klíčové body:**
- Metoda `Save` zapisuje redigovaný výstup do jakékoli implementace `Stream`, včetně `MemoryStream`.  
- Nejsou vytvářeny žádné dočasné soubory, což zvyšuje bezpečnost a výkon.  
- Můžete to kombinovat s `FileStreamResult` v ASP.NET Core pro přímé vrácení souboru do prohlížeče.

## Časté problémy a řešení
| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| **Redakce nebyla aplikována** | Velikost písmen ve frázi se liší od zdroje. | Použijte `ExactPhraseRedaction("John Doe", caseSensitive: false)` nebo redakci pomocí regulárního výrazu pro flexibilní shodu. |
| **Velké soubory způsobují OutOfMemory** | Pokus o načtení celého souboru do paměti. | GroupDocs.Redaction streamuje data interně; ujistěte se, že používáte nejnovější verzi, která zpracovává soubory po částech. |
| **Uložený soubor je poškozen** | Proud není před odesláním resetován. | Po `redactor.Save(stream)` nastavte `stream.Position = 0` před čtením nebo vrácením. |

## Často kladené otázky

**Q: Mohu redigovat PDF soubory pomocí stejného API?**  
A: Ano — GroupDocs.Redaction zachází s PDF, DOCX, PPTX a mnoha formáty obrázků jednotně; stačí nasměrovat `Redactor` na PDF soubor.

**Q: Přetrvává redakce po převodu dokumentu do jiného formátu?**  
A: Naprosto — jakmile je redigováno, obsah je trvale odstraněn, bez ohledu na následné konverze.

**Q: Jak mohu přizpůsobit vzhled redakce?**  
A: Použijte `RedactionOptions` k nastavení barvy překryvu, průhlednosti nebo nahrazení textu vlastním řetězcem.

**Q: Je možné redigovat pomocí regulárních výrazů?**  
A: Ano — `RegexRedaction` vám umožní definovat vzory, jako jsou čísla kreditních karet nebo e‑mailové adresy.

**Q: Jaké verze .NET jsou oficiálně podporovány?**  
A: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6 a .NET 7.

---

**Poslední aktualizace:** 2026-07-20  
**Testováno s:** GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## Související tutoriály

- [Jak načíst a redigovat dokumenty pomocí GroupDocs.Redaction .NET&#58; Kompletní průvodce](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Uložit redigované dokumenty v původním formátu pomocí GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Bezpečná redakce dokumentů v .NET pomocí proudů&#58; Průvodce pro GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)