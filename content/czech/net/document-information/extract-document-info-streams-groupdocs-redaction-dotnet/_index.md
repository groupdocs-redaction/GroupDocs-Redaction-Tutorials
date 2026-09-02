---
date: '2026-06-11'
description: Naučte se, jak extrahovat metadata z dokumentových streamů pomocí GroupDocs.Redaction
  pro .NET, včetně nastavení, ukázek kódu a praktických aplikací.
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: Jak extrahovat metadata z dokumentových streamů pomocí GroupDocs.Redaction
  .NET
type: docs
url: /cs/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# Jak extrahovat metadata z dokumentových streamů pomocí GroupDocs.Redaction .NET

Jste unavení z ručního získávání informací o dokumentech nebo z práce s velkými soubory, které zpomalují váš pracovní postup? **Jak rychle extrahovat metadata** je běžná výzva a knihovna GroupDocs.Redaction pro .NET nabízí rychlý, paměťově úsporný způsob, jak získat podrobnosti o dokumentu přímo ze streamů. V tomto tutoriálu se naučíte, jak nastavit knihovnu, získat typ souboru, počet stránek a velikost ze streamu a připravit výstupní složku pro další zpracování.

## Rychlé odpovědi
- **Co znamená „extrahovat metadata“?** Znamená to čtení vlastností, jako je typ souboru, počet stránek a velikost, aniž by se celý dokument načítal do paměti.  
- **Která knihovna to řeší?** GroupDocs.Redaction pro .NET poskytuje nativní API pro extrakci metadat založenou na streamech.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.  
- **Mohu zpracovávat PDF větší než 1 GB?** Ano – streamy vám umožní pracovat se soubory až do 2 GB, aniž byste načetli celý soubor.  
- **Jaké verze .NET jsou podporovány?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ a .NET 6+.

## Co je extrakce metadat ze streamů?
Extrakce metadat ze streamů je proces čtení vlastností dokumentu přímo z objektu `Stream`, čímž se vyhýbá načítání celého souboru a šetří paměť i čas CPU. Tato technika je ideální pro dávkové zpracování nebo cloudové služby, kde jsou zdroje omezené.

## Proč použít GroupDocs.Redaction pro extrakci metadat?
GroupDocs.Redaction podporuje **více než 30 formátů souborů** (včetně PDF, DOCX, XLSX, PPTX a typů obrázků) a může zpracovávat dokumenty až do **2 GB** při zachování využití paměti pod **50 MB**. Jeho API `Redactor` poskytuje jediné volání pro získání všech klíčových informací o dokumentu, čímž eliminuje potřebu více parserů.

## Požadavky

- **GroupDocs.Redaction pro .NET** (nejnovější verze)  
- **.NET Framework** 4.5+ **nebo** **.NET Core/5+/6+**  
- Základní znalost C# a orientace v práci se soubory (I/O)  
- Visual Studio 2019 nebo novější

## Jak nastavit GroupDocs.Redaction pro .NET?
Abyste mohli začít používat GroupDocs.Redaction, musíte nejprve přidat knihovnu do svého projektu. To lze provést pomocí .NET CLI, Správce balíčků ve Visual Studio nebo rozhraní NuGet UI. Vyberte přístup, který vyhovuje vašemu pracovnímu postupu; CLI je ideální pro skriptovatelné sestavení, zatímco UI nabízí grafický způsob procházení verzí a závislostí.

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**
- Otevřete Správce balíčků NuGet ve Visual Studio.  
- Vyhledejte **"GroupDocs.Redaction"** a nainstalujte nejnovější verzi.

### Kroky získání licence
1. **Free Trial:** Stáhněte si zkušební licenci a vyzkoušejte všechny funkce bez omezení.  
2. **Temporary License:** Požádejte o dočasnou licenci na [GroupDocs](https://purchase.groupdocs.com/temporary-license/) pro rozšířené testování.  
3. **Purchase:** Až budete připraveni na produkci, zakupte komerční licenci.  

Pro více informací navštivte [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).

### Základní inicializace a nastavení
Třída `Redactor` je vstupním bodem pro všechny operace, včetně extrakce metadat.

`Redactor` je základní třída, která představuje instanci dokumentu a poskytuje metody pro redakci, získávání informací a manipulaci se soubory. Po instalaci můžete vytvořit objekt `Redactor` tak, jak je uvedeno níže:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

Nyní, když je knihovna připravena, pojďme se ponořit do detailů implementace.

## Jak extrahovat metadata z dokumentového streamu?
Načtěte dokument jako **read‑only stream**, inicializujte `Redactor` a zavolejte `GetDocumentInfo()`, abyste získali metadata v jediném kroku. Tento přístup zabraňuje načítání celého souboru do paměti, což je zásadní pro velké PDF nebo dokumenty Office s několika stovkami stránek.

**Přímá odpověď:** Otevřete soubor pomocí `File.OpenRead()`, předávejte stream do `new Redactor(stream)` a poté zavolejte `redactor.GetDocumentInfo()` – metoda vrátí objekt obsahující typ souboru, počet stránek a velikost pouhými třemi řádky kódu.

### Krok 1: Připravte cestu ke zdrojovému souboru
Nejprve se ujistěte, že zdrojový soubor existuje a že výstupní složka je připravena. Níže uvedená pomocná metoda kontroluje výstupní adresář a vytvoří jej, pokud je potřeba.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*Proč?* To zajišťuje platnou cestu pro následné operace se soubory a zabraňuje `DirectoryNotFoundException`.

### Krok 2: Otevřete stream dokumentu
Použití `File.OpenRead()` otevře soubor jako **read‑only stream**, což udržuje nízkou spotřebu paměti i u souborů o velikosti v gigabajtech.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*Proč?* Streamy umožňují zpracování za běhu, což vám dovoluje pracovat s částmi souboru místo celého dokumentu.

### Krok 3: Inicializujte Redactor s dokumentovým streamem
`Redactor` je hlavní objekt API, který vám poskytuje přístup k operacím na úrovni dokumentu, včetně extrakce metadat.

`Redactor` představuje jeden dokument načtený ze streamu a poskytuje metody jako `GetDocumentInfo()` pro rychlé získání vlastností.  

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*Proč?* Vytvoření instance `Redactor` se streamem spojuje objekt s podkladovým souborem, aniž by se plně načetl.

### Krok 4: Získejte metadata dokumentu
Volání `GetDocumentInfo()` vrací objekt `DocumentInfo`, který obsahuje formát souboru, počet stránek a velikost souboru.

`GetDocumentInfo()` extrahuje základní vlastnosti (formát, počet stránek, velikost) jedním voláním, čímž eliminuje potřebu samostatných parserů.  

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*Proč?* Tento krok konsoliduje všechna důležitá metadata, což usnadňuje jejich logování, filtrování nebo směrování dokumentů podle jejich charakteristik.

## Jak připravit výstupní adresář pro zpracované soubory?
Před zápisem jakýchkoli zpracovaných souborů se ujistěte, že cílová složka existuje a je zapisovatelná. Programovým kontrolováním cesty a jejím vytvořením, pokud chybí, se vyhnete běžným výjimkám za běhu, jako je `DirectoryNotFoundException` nebo chyby oprávnění. Tento jednoduchý krok také činí váš kód přenosným napříč prostředími, ať už běží lokálně, na serveru nebo v kontejneru.

**Přímá odpověď:** Použijte `Directory.Exists()` k ověření existence složky a `Directory.CreateDirectory()` k jejímu vytvoření, pokud neexistuje – tato jednorázová kontrola zajišťuje platnou cestu před jakoukoliv zápisovou operací.

### Implementujte pomocnou metodu
Níže uvedená metoda zapouzdřuje logiku kontroly a vytvoření, vrací ověřenou cestu pro pozdější použití.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*Proč?* Centralizace této logiky snižuje duplicitu a usnadňuje údržbu kódu.

## Časté problémy a řešení
- **Chyby oprávnění:** Ujistěte se, že aplikace běží pod účtem s právy zápisu do cílové složky.  
- **Neplatné cesty:** Dvakrát zkontrolujte oddělovače cest (`\\` ve Windows, `/` na Linux/macOS), aby nedošlo k `DirectoryNotFoundException`.  
- **Zpracování velkých souborů:** Okamžitě uvolněte streamy (`using` bloky), aby se uvolnily OS handly a předešlo se únikům.

## Praktické aplikace
1. **Automatizovaný příjem dokumentů:** Extrahujte metadata při nahrávání a uložte je do databáze pro rychlé vyhledávání a reportování souladu.  
2. **Právní a compliance audity:** Získejte počet stránek a typy souborů k ověření, že dokumenty splňují regulační standardy před archivací.  
3. **Enterprise Content Management:** Použijte metadata k automatickému kategorizování souborů do složek, čímž zlepšíte organizaci a rychlost vyhledávání.

## Úvahy o výkonu
- **Správa paměti:** Vždy obalujte streamy do `using` bloků, aby byly automaticky uvolněny.  
- **Dávkové zpracování:** Zpracovávejte dokumenty ve skupinách po 10‑20, aby se vyvážil průtok a využití paměti, zejména na serverech s omezenými zdroji.  
- **Paralelismus:** Využijte `Parallel.ForEach` pro nezávislé soubory, ale sledujte CPU a I/O, aby nedošlo ke konfliktům.

## Závěr
Nyní máte kompletní, připravený průvodce pro **extrakci metadat** z dokumentových streamů pomocí GroupDocs.Redaction pro .NET. Dodržením výše uvedených kroků můžete efektivně získat typ souboru, počet stránek a velikost při nízké spotřebě paměti a s elegancí zpracovávat velké soubory.

**Další kroky**
- Prohlédněte si kompletní referenci API v [dokumentaci](https://docs.groupdocs.com/redaction/net/).  
- Ponořte se hlouběji do [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/), abyste prozkoumali funkce redakce, vodoznaků a OCR.  
- Experimentujte s různými formáty souborů (PDF, DOCX, XLSX), abyste viděli, jak se metadata liší mezi typy.  
- Integrovat extrahovaná metadata do vašeho stávajícího řešení pro správu dokumentů nebo vyhledávání.

## Často kladené otázky

**Q: Jaký je hlavní případ použití pro extrakci metadat v GroupDocs.Redaction?**  
A: Umožňuje rychlé, paměťově úsporné získání vlastností dokumentu pro indexaci, kontrolu souladu a automatické směrování bez otevření celého souboru.

**Q: Mohu extrahovat metadata z chráněných souborů heslem?**  
A: Ano, při vytváření objektu `Redactor` poskytněte heslo; API dešifruje stream interně.

**Q: Podporuje knihovna ne‑PDF formáty jako DOCX nebo XLSX?**  
A: Rozhodně – GroupDocs.Redaction zpracovává více než 30 formátů, včetně PDF, DOCX, XLSX, PPTX a běžných typů obrázků.

**Q: Jak velký dokument mohu zpracovat pomocí streamů?**  
A: Streamy umožňují zpracování souborů až do **2 GB**, přičemž spotřeba paměti zůstává pod **50 MB**, díky čtení za běhu.

**Q: Kde mohu získat pomoc, pokud narazím na problémy?**  
A: Navštivte [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) pro podporu komunity, nebo si prostudujte oficiální dokumentaci pro tipy na řešení problémů.

---

**Poslední aktualizace:** 2026-06-11  
**Testováno s:** GroupDocs.Redaction 23.12 pro .NET  
**Autor:** GroupDocs  

**Zdroje**  
- **Dokumentace:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **Reference API:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Stáhnout:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## Související tutoriály

- [Ovládání získávání metadat dokumentu pomocí GroupDocs.Redaction .NET API](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)
- [Jak redigovat metadata dokumentu pomocí GroupDocs.Redaction pro .NET – komplexní průvodce](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Bezpečná redakce dokumentů v .NET pomocí streamů: průvodce pro GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)