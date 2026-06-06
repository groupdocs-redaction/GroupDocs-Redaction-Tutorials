---
date: '2026-06-06'
description: Naučte se, jak získat metadata a extrahovat metadata dokumentu pomocí
  GroupDocs.Redaction .NET, což umožňuje robustní správu dokumentů a soulad s předpisy.
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: Jak získat metadata pomocí GroupDocs.Redaction .NET API
type: docs
url: /cs/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# Jak získat metadata pomocí GroupDocs.Redaction .NET

V dnešní digitální éře je **jak získat metadata** ze souboru základním krokem pro každou aplikaci zaměřenou na dokumenty. Ať už potřebujete číst metadata souboru pro audity shody, extrahovat vlastnosti dokumentu pro indexování, nebo jen zobrazit velikost dokumentu v uživatelském rozhraní, GroupDocs.Redaction .NET vám poskytuje stručné API, které to zvládne během několika řádků C#. Tento tutoriál vás provede celým procesem, od nastavení prostředí až po zobrazení získaných informací, takže můžete okamžitě začít extrahovat metadata dokumentů.

## Rychlé odpovědi
- **Jaká je hlavní metoda pro získání metadat?** Zavolejte `Redactor.GetDocumentInfo()` na instanci `Redactor`.  
- **Jaké formáty jsou podporovány?** Více než 50 vstupních a výstupních formátů, včetně PDF, DOCX, XLSX, PPTX a typů obrázků.  
- **Potřebuji licenci pro vývoj?** Licence zdarma pro zkušební verzi funguje pro testování; plná licence je vyžadována pro produkci.  
- **Mohu zpracovávat velké soubory?** Ano—GroupDocs.Redaction zpracovává dokumenty s stovkami stránek, aniž by načítal celý soubor do paměti.  
- **Je k dispozici podpora async?** API lze zabalit do asynchronních vzorů, aby UI vlákna zůstala responzivní.

## Co je získávání metadat v GroupDocs.Redaction?
Získávání metadat je proces přístupu k vestavěným vlastnostem dokumentu — jako je typ souboru, počet stránek a velikost — prostřednictvím API knihovny. Extrahováním těchto vlastností mohou vývojáři programově posoudit charakteristiky dokumentu, podpořit indexování, vynucovat pravidla shody a činit informovaná rozhodnutí o dalších krocích zpracování.

## Jak získat metadata dokumentu?
Třída `Redactor` je hlavním rozhraním pro načítání a inspekci dokumentů v GroupDocs.Redaction.  
`GetDocumentInfo()` je metoda, která vrací objekt `DocumentInfo` obsahující metadata dokumentu.  

Načtěte svůj soubor pomocí `new Redactor("path/to/file")` a zavolejte `GetDocumentInfo()` — volání vrátí objekt `DocumentInfo` obsahující typ, počet stránek, velikost a další vlastnosti. Tento dvoukrokový postup funguje pro jakýkoli podporovaný formát a nevyžaduje žádnou další konfiguraci. Poté můžete číst pole jako `FileType`, `PageCount` a `FileSize` a zobrazit nebo zaznamenat informace.

## Požadavky

- **GroupDocs.Redaction .NET** verze 21.6 nebo novější.  
- .NET Framework 4.7.2 +, .NET Core 3.1 +, nebo .NET 5/6+.  
- Základní znalost C# a vývojové IDE (Visual Studio, Rider, atd.).

## Nastavení GroupDocs.Redaction pro .NET

Začít s GroupDocs.Redaction je jednoduché. Nainstalujte balíček pomocí jedné z následujících metod:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

Nebo použijte **NuGet Package Manager UI**: jednoduše vyhledejte „GroupDocs.Redaction“ a klikněte na **Install**.

### Získání licence

Pro vyzkoušení GroupDocs.Redaction můžete získat bezplatnou zkušební licenci. Pro kontinuální vývoj nebo produkční použití zakupte plnou licenci nebo požádejte o dočasnou licenci na oficiální stránce.

Po instalaci inicializujte knihovnu následovně:

```csharp
using GroupDocs.Redaction;
```

## Průvodce implementací

### Funkce získání informací o dokumentu

Tato funkce se zaměřuje na extrakci klíčových metadat z dokumentů pomocí GroupDocs.Redaction .NET. Postupujte podle těchto kroků:

#### Krok 1: Připravte cestu k dokumentu

Definujte absolutní nebo relativní cestu k cílovému souboru:

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

Nahraďte `YOUR_DOCUMENT_DIRECTORY` složkou, která obsahuje váš dokument.

#### Krok 2: Inicializujte instanci Redactor

Vytvořte objekt `Redactor`, který poskytuje přístup k metodám metadat:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### Krok 3: Získejte informace o dokumentu

Zavolejte `GetDocumentInfo()` na instanci `Redactor`, abyste získali všechny dostupné vlastnosti:

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

Vrácený objekt zahrnuje typ souboru, počet stránek a velikost souboru.

#### Krok 4: Zobrazte podrobnosti dokumentu

Vypište informace do konzole nebo uživatelského rozhraní. Ukázkový kód (okomentovaný pro samostatné spuštění) demonstruje, jak vytisknout každou vlastnost:

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### Proč použít GroupDocs.Redaction pro extrakci metadat?
GroupDocs.Redaction podporuje **50+ formátů souborů** a může zpracovávat dokumenty až do **2 GB** při zachování spotřeby paměti pod **100 MB** pro typické pracovní zatížení. Knihovna extrahuje metadata bez úplného načtení dokumentu, což poskytuje rychlé odpovědi — často pod **200 ms** pro 100‑stránkový PDF na standardním serverovém hardware.

### Časté problémy a řešení

- **Nesprávná cesta k souboru** – Ověřte řetězec cesty a zajistěte, aby byl soubor přístupný běžícímu procesu.  
- **Nepodporovaný formát** – Zkontrolujte seznam formátů; pokud formát chybí, zvažte jeho nejprve konverzi.  
- **Úzká místa ve výkonu** – U velmi velkých souborů povolte streamovací možnosti nebo zpracovávejte stránky po dávkách, aby se omezila spotřeba paměti.

## Praktické aplikace

Pochopení metadat dokumentu umožňuje několik reálných scénářů:

1. **Systémy pro správu dokumentů (DMS)** – Automatizujte kategorizaci a indexování na základě typu, velikosti nebo počtu stránek.  
2. **Audity shody** – Ověřte, že důvěrné soubory obsahují požadovaná metadata před archivací.  
3. **Migrace dat** – Skupinujte soubory podle vlastností, aby se zjednodušily úlohy hromadné migrace.  

## Úvahy o výkonu

- **Efektivní využití zdrojů** – Používejte instanci `Redactor` uvnitř bloku `using`, aby byla zajištěna správná likvidace.  
- **Asynchronní vzory** – Zabalte volání metadat do `Task.Run` nebo implementujte async wrappery, aby UI vlákna zůstala responzivní v desktopových nebo webových aplikacích.

## Často kladené otázky

**Q: Jaké formáty dokumentů mohu použít pro extrakci metadat?**  
A: GroupDocs.Redaction čte metadata z více než 50 formátů, včetně PDF, DOCX, XLSX, PPTX, HTML a běžných typů obrázků.

**Q: Jak zacházet se soubory chráněnými heslem?**  
A: Předávejte heslo konstruktoru `Redactor`; API soubor dešifruje před extrakcí metadat.

**Q: Existuje limit velikosti souborů, které mohu zpracovat?**  
A: Přestože neexistuje pevný limit, soubory větší než 2 GB mohou vyžadovat dodatečné ladění paměti; výkon zůstává lineární s velikostí souboru.

**Q: Mohu získat metadata hromadně?**  
A: Ano — iterujte přes kolekci cest k souborům a pro každý zavolejte `GetDocumentInfo()`; knihovna je thread‑safe pro paralelní provádění.

**Q: Potřebuji licenci pro vývojové sestavení?**  
A: Bezplatná zkušební licence stačí pro vývoj a testování; komerční licence je vyžadována pro produkční nasazení.

## Zdroje

- [Dokumentace](https://docs.groupdocs.com/redaction/net/)  
- [API Reference](https://reference.groupdocs.com/redaction/net)  
- [Stáhnout](https://releases.groupdocs.com/redaction/net/)  
- [Fórum bezplatné podpory](https://forum.groupdocs.com/c/redaction/33)  
- [Informace o dočasné licenci](https://purchase.groupdocs.com/temporary-license/)

## Závěr

Nyní máte kompletní, krok‑za‑krokem průvodce o **jak získat metadata** pomocí GroupDocs.Redaction .NET. Využitím metody `Redactor.GetDocumentInfo()` můžete rychle číst metadata souboru, podpořit workflow shody a vylepšit jakýkoli pipeline pro zpracování dokumentů. Prozkoumejte další funkce Redaction — jako je redakce obsahu, vodoznakování a konverze dokumentů — abyste vytvořili plnohodnotné řešení pro správu dokumentů.

---

**Poslední aktualizace:** 2026-06-06  
**Testováno s:** GroupDocs.Redaction .NET 21.6 (nejnovější v době psaní)  
**Autor:** GroupDocs  

## Související tutoriály

- [Jak extrahovat metadata dokumentu ze streamů pomocí GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [Jak redigovat metadata dokumentu pomocí GroupDocs.Redaction pro .NET — Komplexní průvodce](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Tutoriály načítání dokumentů s GroupDocs.Redaction pro .NET](/redaction/net/document-loading/)