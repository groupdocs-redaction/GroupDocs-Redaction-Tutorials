---
date: '2026-10-06'
description: Naučte se, jak zakrýt citlivá data pomocí GroupDocs.Redaction .NET. Tento
  podrobný návod vám ukáže, jak vytvořit, použít a uložit politiku zakrytí jako XML.
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: Naučte se, jak zakrýt citlivá data pomocí GroupDocs.Redaction .NET.
  Tento podrobný návod vám ukáže, jak vytvořit, použít a uložit politiku zakrytí jako
  XML.
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: Jak zakrýt citlivá data pomocí GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: Jak zakrýt citlivá data pomocí GroupDocs.Redaction .NET
type: docs
url: /cs/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# Jak redigovat citlivá data pomocí GroupDocs.Redaction .NET

Ochrana důvěrných informací v kontraktech, finančních výkazech nebo zdravotních záznamech je nevyjednatelným požadavkem moderních aplikací. V tomto průvodci se naučíte **jak redigovat citlivá data** pomocí GroupDocs.Redaction pro .NET, od instalace SDK po definování znovupoužitelných XML politik, které lze použít na jakýkoli typ dokumentu.

## Rychlé odpovědi
- **Co znamená „vytvořit politiku redakce“?** Jedná se o proces definování pravidel (text, regex, obrázky atd.), která říkají GroupDocs.Redaction, jak skrýt nebo nahradit důvěrný obsah.  
- **Kterou knihovnu potřebuji?** GroupDocs.Redaction pro .NET, dostupná přes NuGet.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována trvalá licence.  
- **Mohu politiku znovu použít?** Ano — po uložení jako XML ji můžete později načíst a použít na jakýkoli dokument.  
- **Jaké verze .NET jsou podporovány?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Co je politika redakce?

Politika redakce je soubor pravidel, která určují *co* má být odstraněno nebo nahrazeno a *jak* má náhrada vypadat. Vytvořením politiky jednou můžete uplatnit konzistentní bezpečnostní standardy na každý dokument zpracovávaný vaší aplikací.

## Jak funguje politika redakce?

Načtěte dokument pomocí enginu `Redactor`, připojte jedno nebo více redakčních pravidel a poté zavolejte `Apply`. Engine prohledá dokument, zakryje odpovídající obsah a volitelně vytvoří nový soubor. Stejná sada pravidel může být exportována do XML, což vám umožní znovu použít politiku bez překládání kódu.

## Proč použít GroupDocs.Redaction k vytvoření politiky redakce?

GroupDocs.Redaction poskytuje komplexní sadu funkcí, které zjednodušují tvorbu, správu a provádění politik redakce, zajišťují konzistentní ochranu dat napříč různými typy dokumentů a zároveň nabízejí vysoký výkon a snadnou integraci do existujících .NET aplikací pro týmy a organizace.

- **Široká podpora formátů** – SDK zpracovává více než 30 typů souborů, včetně PDF, DOCX, XLSX, PPTX a obrazových formátů, a může zpracovávat soubory až do 2 GB bez načítání celého souboru do paměti.  
- **Programová přesnost** – definujte přesné fráze, regulární výrazy nebo vlastní logiku, abyste cíleně skryli pouze data, která potřebujete.  
- **Znovupoužitelné XML politiky** – exportujte svá pravidla jednou a sdílejte je napříč týmy, službami nebo mikro‑službami.  
- **Výkonnostně optimalizovaný engine** – knihovna zpracovává dokumenty o stovkách stránek za méně než sekundu na typickém serverovém hardware, což ji činí vhodnou pro vysokokapacitní pipeline.

## Předpoklady
- Knihovna GroupDocs.Redaction kompatibilní s vaším .NET runtime.  
- Visual Studio, VS Code nebo jakékoli IDE podporující C#.  
- Základní znalost C# a struktury .NET projektů.

## Nastavení GroupDocs.Redaction pro .NET

Nejprve přidejte knihovnu do svého projektu.

**Použití .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Použití Package Manageru**  
```powershell
Install-Package GroupDocs.Redaction
```  

Nebo vyhledejte „GroupDocs.Redaction“ v uživatelském rozhraní NuGet Package Manager a nainstalujte jej odtud.

### Získání licence
- Začněte s **bezplatnou zkušební verzí**, abyste prozkoumali funkce.  
- Požádejte o **dočasnou licenci** pro rozšířené testování, poté zakupte plnou licenci pro produkční použití.

### Základní inicializace
Přidejte jmenný prostor do svého zdrojového souboru:

Třída `Redactor` je jádrový engine, který načte dokument a aplikuje redakční pravidla.  
```csharp
using GroupDocs.Redaction;
```  

Třída `Redactor` je jádrový engine GroupDocs.Redaction, který načte dokument a aplikuje redakční pravidla.

## Jak vytvořit politiku redakce krok za krokem

Níže je kompletní průvodce, který ukazuje, jak programově vytvořit politiku redakce, nakonfigurovat její pravidla, aplikovat je na dokument a nakonec uložit politiku jako XML soubor pro budoucí opětovné použití, čímž zajistíte konzistentní redakci napříč více projekty a typy dokumentů.

### Krok 1: připravte adresář s dokumenty
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*Nahraďte `"YOUR_DOCUMENT_DIRECTORY"` složkou, která obsahuje dokumenty, které chcete chránit.*

### Krok 2: načtěte dokument
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
Objekt `Redactor` otevře soubor a spravuje jeho životní cyklus.

### Krok 3: definujte redakce
ExactPhraseRedaction definuje pravidlo, které nahrazuje konkrétní frázi, zatímco `RegexRedaction` používá regulární výraz k nalezení vzorů.  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
Zde vytváříme dvě pravidla:
1. **ExactPhraseRedaction** — nahrazuje známou frázi textem „[REDACTED]“.
2. **RegexRedaction** — najde data ve formátu `YYYY‑MM‑DD` a nahradí je textem „[DATE REDACTED]“.

### Krok 4: aplikujte redakce
```csharp
redactor.Apply(redactions);
```  
Všechna definovaná pravidla jsou provedena proti otevřenému dokumentu v jednom průchodu.

### Krok 5: uložte politiku jako XML soubor
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
XML soubor ukládá definice redakce, což vám umožní znovu použít stejnou politiku bez přepisování kódu.

## Praktické aplikace

- **Právnické firmy** mohou redigovat čísla případů a jména klientů před sdílením návrhů.  
- **Finanční oddělení** maskují čísla účtů nebo data transakcí v reportech.  
- **Zdravotnická zařízení** zajišťují soulad s HIPAA odstraněním identifikátorů pacientů.

## Tipy pro výkon

- Otevírejte **jeden dokument najednou**, aby byl nízký odběr paměti.  
- Pište **efektivní regulární výrazy**; vyhýbejte se příliš širokým vzorům, které zvyšují dobu zpracování.  
- Udržujte knihovnu **aktuální**, abyste získali výhody z vylepšení výkonu a nových typů redakce.

## Časté problémy a řešení

| Problém | Proč k tomu dochází | Jak opravit |
|-------|----------------|------------|
| **IO výjimka při přípravě adresáře** | Špatná cesta nebo chybějící oprávnění k zápisu | Ověřte, že složka existuje a aplikace má práva čtení/zápisu. |
| **Regex neodpovídá očekávanému textu** | Vzor je příliš přísný nebo chybí únikové znaky | Otestujte regex pomocí online testeru; upravte kvantifikátory nebo escapujte speciální znaky. |
| **Soubor politiky nebyl vytvořen** | `SavePolicy` bylo zavoláno před aplikací redakcí nebo s neplatnou cestou | Ujistěte se, že výstupní adresář je zapisovatelný a zavolejte `SavePolicy` po `Apply`. |

## Často kladené otázky

**Q: Mohu načíst existující XML politiku místo vytváření programově?**  
A: Ano — použijte `redactor.LoadPolicy("policy.xml")` k importu dříve uložené politiky.

**Q: Podporuje GroupDocs.Redaction PDF soubory chráněné heslem?**  
A: Rozhodně. Předávejte heslo konstruktoru `Redactor`: `new Redactor(sourceFile, "password")`.

**Q: Je možné redigovat obrázky nebo metadata?**  
A: SDK poskytuje třídy `ImageRedaction` a `MetadataRedaction` pro tyto scénáře.

**Q: Jak zacházet s velkými dokumenty (stovky MB)?**  
A: Zpracovávejte je po částech nebo použijte streaming API ke snížení paměťové náročnosti; engine dokáže zpracovat soubory až do 2 GB bez načítání celého souboru do RAM.

**Q: Jaký licenční model je vyžadován pro komerční použití?**  
A: Pro produkční nasazení je vyžadována placená licence; zkušební licence stačí pro vývoj a testování.

## Závěr

Nyní máte kompletní, znovupoužitelnou **politiku redakce**, kterou můžete aplikovat na jakýkoli dokument pomocí GroupDocs.Redaction pro .NET. Exportováním politiky do XML zjednodušíte budoucí aktualizace a zajistíte konzistentní ochranu dat napříč vaší organizací.

### Další kroky
- Experimentujte s dalšími typy redakce, jako jsou `ImageRedaction` nebo `MetadataRedaction`.  
- Integrovat logiku načítání politiky do vašeho workflow pro správu dokumentů pro automatizovanou redakci.  
- Prozkoumejte referenci API **GroupDocs.Redaction** pro pokročilé přizpůsobení.

---

**Poslední aktualizace:** 2026-10-06  
**Testováno s:** GroupDocs.Redaction 5.8 for .NET  
**Autor:** GroupDocs  

**Zdroje**  
- [Dokumentace](https://docs.groupdocs.com/redaction/net/)  
- [API reference](https://reference.groupdocs.com/redaction/net)  
- [Stáhnout](https://releases.groupdocs.com/redaction/net/)  
- [Bezplatné fórum podpory](https://forum.groupdocs.com/c/redaction/33)  
- [Žádost o dočasnou licenci](https://purchase.groupdocs.com/temporary-license/)

## Související tutoriály

- [Redigovat citlivá data pomocí GroupDocs.Redaction .NET (C#)](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)
- [Implementovat redakci dokumentů pomocí GroupDocs.Redaction .NET&#58; Průvodce krok za krokem](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
- [Jak redigovat dokumenty pomocí GroupDocs.Redaction .NET – Kompletní průvodce](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)