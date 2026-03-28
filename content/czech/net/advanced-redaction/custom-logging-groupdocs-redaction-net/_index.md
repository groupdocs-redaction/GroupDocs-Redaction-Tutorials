---
date: '2026-03-28'
description: Naučte se, jak v GroupDocs.Redaction pro .NET implementovat vlastní logger
  v C#, který umožňuje podrobné vlastní protokolování a usnadňuje tvorbu zpráv o souladu.
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: Implementace vlastního loggeru v C# v GroupDocs.Redaction pro .NET
type: docs
url: /cs/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# Implementujte vlastní logger c# v GroupDocs.Redaction pro .NET

Efektivní správa redakcí dokumentů je kritická, zejména při práci s citlivými informacemi. V tomto průvodci se naučíte **jak implementovat vlastní logger c#** s GroupDocs.Redaction pro .NET, což vám poskytne plnou kontrolu nad logováním, zpracováním chyb a auditními stopami.

## Rychlé odpovědi
- **Co dělá vlastní logger c#?** Zachycuje chyby, varování a informační zprávy během redakce.  
- **Která knihovna poskytuje rozhraní ILogger?** GroupDocs.Redaction pro .NET.  
- **Mohu uložit redigovaný dokument bez rasterizace?** Ano – použijte `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`.  
- **Potřebuji licenci pro produkční použití?** Pro produkci je vyžadována plná licence; k vyzkoušení je k dispozici zkušební verze.  
- **Je tento přístup kompatibilní s .NET Core / .NET 6+?** Rozhodně – stejné API funguje napříč .NET Framework a .NET Core/5/6.

## Co je vlastní logger c#?
Vlastní **logger c#** je třída, která implementuje rozhraní `ILogger` poskytované GroupDocs.Redaction. Umožňuje vám směrovat logovací zprávy kamkoli potřebujete – do konzole, souboru, databáze nebo externích monitorovacích systémů – a zároveň vám poskytuje přehled o workflow redakce.

## Proč používat vlastní logování .net s GroupDocs.Redaction?
- **Soulad a audit:** Detailní logy splňují regulatorní požadavky.  
- **Viditelnost chyb:** `LogError` a `LogWarning` vám poskytují okamžitou zpětnou vazbu o problémech.  
- **Flexibilita integrace:** Přeposílejte logy do existujících .NET logovacích frameworků (Serilog, NLog, atd.).

## Předpoklady
- **GroupDocs.Redaction pro .NET** nainstalován (viz instalace níže).  
- Vývojové prostředí .NET (Visual Studio, VS Code nebo CLI).  
- Základní znalost C# a zkušenost se souborovými proudy.

## Instalace

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
Vyhledejte **"GroupDocs.Redaction"** a nainstalujte nejnovější verzi.

## Získání licence
- **Bezplatná zkušební verze:** Otestujte API s dočasnou licencí.  
- **Dočasná licence:** Získejte plný přístup k funkcím na omezenou dobu.  
- **Nákup:** Získejte trvalou licenci pro produkční nasazení.

## Průvodce krok za krokem

### Krok 1: Definujte vlastní třídu loggeru (log warnings c#)

Vytvořte třídu, která implementuje `ILogger`. Tato třída bude zachycovat chyby, varování a informační zprávy.

```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```

**Vysvětlení:** Příznak `HasErrors` vám pomáhá rozhodnout, zda pokračovat ve zpracování. Tři metody odpovídají třem úrovním logování, které budete potřebovat ve většině scénářů redakce.

### Krok 2: Připravte cesty k souborům a otevřete zdrojový dokument

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**Proč je to důležité:** Použití pomocných metod udržuje váš kód čistý a zajišťuje, že výstupní složka existuje, než se pokusíte **uložit redigovaný dokument**.

### Krok 3: Aplikujte redakce při použití vlastního loggeru

```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```

**Vysvětlení:**  
1. `Redactor` je vytvořen s `RedactorSettings(logger)`, čímž se propojí s vaším `CustomLogger`.  
2. Po aplikaci redakce kód kontroluje `logger.HasErrors`. Pokud nedošlo k chybám, dokument se uloží – což demonstruje logiku **uložit redigovaný dokument** bez rasterizace.

### Běžné úskalí a řešení problémů
- **Chybějící výstup logu:** Ověřte, že každá metoda `Log*` je správně přepsána.  
- **Výjimky při přístupu k souborům:** Zajistěte, aby aplikace měla oprávnění číst/zapisovat jak pro zdrojové, tak výstupní cesty.  
- **Logger není připojen:** Parametr `RedactorSettings(logger)` je nezbytný; jeho vynechání zakáže vlastní logování.

## Praktické aplikace
1. **Reportování souladu:** Exportujte záznamy logu do CSV nebo databáze pro auditní stopy.  
2. **Sledování chyb:** Rychle najděte problematické soubory skenováním výstupu `LogError`.  
3. **Automatizace workflow:** Spusťte následné procesy (např. upozornění compliance officeru), když je zavoláno `LogWarning`.

## Úvahy o výkonu
- **Okamžitě uvolňujte proudy** pro uvolnění paměti, zejména při zpracování velkých dávek.  
- **Sledujte CPU a paměť** během hromadných redakcí; zvažte paralelní zpracování dokumentů s opatrnou synchronizací loggeru.  
- **Zůstaňte aktualizováni:** Novější verze GroupDocs.Redaction často obsahují optimalizace výkonu a další logovací háčky.

## Závěr

Implementací **vlastního loggeru c#** získáte podrobný přehled o každém kroku redakčního řetězce, což usnadňuje splnění standardů souladu a ladění problémů. Tento přístup funguje bez problémů s GroupDocs.Redaction pro .NET a lze jej rozšířit tak, aby se integroval s libovolným .NET logovacím frameworkem, který již používáte.

---

## Často kladené otázky

**Q: Jaký je účel vlastního logování s GroupDocs.Redaction?**  
A: Vlastní logování pomáhá sledovat a spravovat redakce pro soulad, sledování chyb a optimalizaci workflow.

**Q: Jak zacházet s chybami pomocí vlastního loggeru?**  
A: Implementujte `LogError` ve své třídě `CustomLogger`; příznak `HasErrors` vám umožní zastavit zpracování, pokud je to potřeba.

**Q: Lze vlastní logování integrovat s jinými systémy?**  
A: Ano, můžete přeposílat logovací zprávy do CRM, ERP nebo centralizovaných monitorovacích nástrojů rozšířením metod loggeru.

**Q: Jaké jsou běžné úskalí při implementaci vlastního logování?**  
A: Nesprávné implementace metod, chybějící `RedactorSettings(logger)` a problémy s oprávněními k souborům jsou nejčastější.

**Q: Jak vlastní logování zlepšuje workflow redakce dokumentů?**  
A: Detailní logy poskytují vizualizaci v reálném čase, usnadňují řešení problémů a splňují požadavky na audit.

## Zdroje

- **Dokumentace:** [Dokumentace GroupDocs.Redaction .NET](https://docs.groupdocs.com/redaction/net/)  
- **Reference API:** [Reference API GroupDocs.Redaction](https://reference.groupdocs.com/redaction/net)  
- **Stáhnout:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**Poslední aktualizace:** 2026-03-28  
**Testováno s:** GroupDocs.Redaction 23.11 pro .NET  
**Autor:** GroupDocs