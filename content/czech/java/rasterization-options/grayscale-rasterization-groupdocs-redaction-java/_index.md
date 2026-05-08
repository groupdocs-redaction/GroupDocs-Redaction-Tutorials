---
date: '2026-02-13'
description: Naučte se, jak vytvořit černobílý PDF pomocí GroupDocs.Redaction pro
  Javu, bezpečně převést PDF do odstínů šedi při zachování kvality dokumentu.
keywords:
- GroupDocs.Redaction
- Java
- Document Processing
title: Jak vytvořit šedotónový PDF pomocí GroupDocs.Redaction Java – Zabezpečte a
  optimalizujte své dokumenty
type: docs
url: /cs/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

et zabezpečené, tiskově přívětivé dokumenty, které splňují normy souladu."

Then horizontal rule.

**Last Updated:** 2026-02-13 => same.

**Tested With:** GroupDocs.Redaction 23.11 for Java

**Author:** GroupDocs

All unchanged.

Now produce final markdown with translations.

Make sure placeholders remain unchanged.

Let's assemble.# GroupDocs.Redaction Java: Průvodce stupnicí šedých rasterizací

## Úvod

Pokud potřebujete **vytvořit šedotónové pdf** soubory a zároveň zachovat své dokumenty bezpečné a profesionálně vypadající, jste na správném místě. V tomto tutoriálu vás provedeme přesnými kroky, jak převést barevné soubory DOCX, PDF nebo jiné podporované formáty do čisté šedotónové rasterizované verze pomocí GroupDocs.Redaction pro Java. Dozvíte se, proč rasterizace přidává další vrstvu zabezpečení, jak nakonfigurovat knihovnu a jak efektivně spravovat prostředky – vše v konverzačním, krok‑za‑krokem stylu.

## Rychlé odpovědi
- **Co dělá šedotónová rasterizace?** Převádí každou stránku dokumentu na vysoce rozlišený obrázek a poté na něj aplikuje šedotónový filtr, čímž odstraní veškeré informace o barvě.  
- **Proč použít GroupDocs.Redaction?** Kombinuje zabezpečení redakce s výkonnými možnostmi rasterizace v jediné API.  
- **Jaké formáty jsou podporovány?** DOCX, PDF, XLSX, PPTX, RTF a mnoho dalších.  
- **Potřebuji licenci?** Pro produkční použití je vyžadována platná licence GroupDocs.Redaction; pro testování je k dispozici zkušební verze.  
- **Jaká verze Javy je požadována?** JDK 8 nebo vyšší.

## Co je **vytvořit šedotónové pdf**?

Vytvoření šedotónového PDF znamená převést každý vizuální prvek původního dokumentu na odstíny šedé. Výsledkem je menší, tiskově přívětivý soubor, který eliminuje rušivé barevné prvky a přidává jemný bezpečnostní přínos, protože obsah je nyní založen na obrázku.

## Proč použít šedotónovou rasterizaci s GroupDocs.Redaction?

- **Zvýšené zabezpečení** – rasterizované stránky nelze vybrat, kopírovat ani upravovat jako text.  
- **Konzistentní vzhled** – barvy jsou odstraněny, což poskytuje jednotný, profesionální vzhled.  
- **Široká podpora formátů** – stejné API funguje pro DOCX, PDF, PPTX a další.  
- **Jemně nastavitelná kontrola** – můžete upravit DPI, výstupní formát a pokročilé možnosti, jako je převod na šedotón.

## Předpoklady

- Java Development Kit (JDK) 8 nebo novější. Ověřte pomocí `java -version`.  
- IDE (IntelliJ IDEA, Eclipse nebo NetBeans) pro snadnější kódování a ladění.  
- GroupDocs.Redaction pro Java přidaný přes Maven nebo Gradle.  
- Ukázkový dokument (např. vícestránkový DOCX), na kterém můžete bezpečně experimentovat.  
- Dostatečný volný diskový prostor pro rasterizovaný výstup (raster soubory mohou být větší než zdroj).

## Import balíčků

Nastavení správných importů je jako uspořádání nářadí před projektem. Následující importy vám poskytují přístup ke klíčové třídě Redactor a možnostem rasterizace, které budeme potřebovat.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Krok 1: Inicializace objektu Redactor

Vytvoření instance `Redactor` otevírá dveře ke všem možnostem zpracování dokumentů.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

Nahraďte `Constants.MULTIPAGE_SAMPLE_DOCX` cestou k souboru, který chcete převést na šedotónové PDF.

## Krok 2: Konfigurace možností uložení

`SaveOptions` určuje, jak bude finální soubor zapsán. Přidání přípony vám pomůže zachovat původní soubor nedotčený.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

Výstup bude pojmenován `yourfile_scan.docx` (nebo formát, který později určíte).

## Krok 3: Povolení rasterizace

Zapnutí rasterizace říká enginu, aby před uložením vykreslil každou stránku jako obrázek.

```java
so.getRasterization().setEnabled(true);
```

Rasterizace je základem pro vytvoření šedotónového PDF, protože převádí dokument na obrazovou reprezentaci.

## Krok 4: Aplikace převodu na šedotón

Nyní přidáme šedotónový filtr do pipeline rasterizace.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

Tato možnost vynutí, aby každý pixel byl vykreslen v odstínech šedé, čímž získáte výsledek **vytvořit šedotónové pdf**, který požadujete.

## Krok 5: Spuštění transformace dokumentu

Volání `save` spustí celý řetězec zpracování.

```java
redactor.save(so);
```

Po provedení tohoto řádku najdete na disku nový soubor, který je plně rasterizovaný, šedotónový a uložený s příponou `_scan`.

## Krok 6: Správná správa prostředků

Vyčištění prostředků zabraňuje zamykání souborů a únikům paměti.

```java
finally { redactor.close(); }
```

Pro moderní Javu můžete také použít vzor try‑with‑resources, který automaticky uzavře `Redactor`:

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

Oba přístupy jsou bezpečné; ten druhý je stručnější.

## Pokročilé konfigurační možnosti

### Nastavení DPI pro kvalitu nebo velikost

Vyšší DPI poskytuje ostřejší obrázky (dobré pro tisk), zatímco nižší DPI snižuje velikost souboru.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Volba výstupního formátu

Můžete vynutit, aby rasterizovaný výsledek byl v konkrétním kontejnerovém formátu, například PDF.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Běžné případy použití

- **Archivace právních dokumentů** – vytvořte neměnitelné šedotónové PDF, které nelze upravovat.  
- **Tiskové zprávy** – zajistěte konzistentní černobílý výstup pro hromadný tisk.  
- **Workflowy souladnosti** – kombinujte redakci se šedotónovou rasterizací pro splnění přísných předpisů o ochraně dat.

## Běžné problémy a řešení

| Problém | Proč se to stane | Řešení |
|-------|----------------|-----|
| Výstupní soubor je větší než očekáváno | DPI nastaveno příliš vysoké nebo je vypnuta komprese obrázků | Snižte DPI (např. 150) nebo povolte kompresi v `RasterizationOptions`. |
| Text je rozmazaný | Nedostatečné DPI pro původní velikost písma | Zvyšte DPI na 300 nebo více. |
| Proces vyvolá `OutOfMemoryError` u velkých dokumentů | Celý dokument je načten do paměti | Použijte streaming API nebo zpracovávejte stránky po dávkách, pokud je to podporováno. |
| Šedotón nebyl aplikován | Pokročilá možnost nebyla přidána správně | Ověřte, že `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` je voláno před `save()`. |

## Často kladené otázky

**Q: Mohu převádět dokumenty na šedotón bez rasterizace?**  
A: V GroupDocs.Redaction je možnost šedotónu svázána s rasterizací, která zajišťuje konzistentní výsledky a přidává zabezpečení.

**Q: Jaké formáty dokumentů podporují šedotónovou rasterizaci?**  
A: Všechny hlavní formáty podporované GroupDocs.Redaction – včetně DOCX, PDF, XLSX, PPTX, RTF a dalších – lze rasterizovat a převést na šedotón.

**Q: Ovlivní rasterizace velikost souboru mých dokumentů?**  
A: Ano. Soubory s velkým množstvím textu mohou narůst, zatímco soubory s mnoha obrázky se mohou zmenšit. Nastavení DPI má největší dopad.

**Q: Je možné proces šedotónové rasterizace obrátit?**  
A: Ne. Rasterizace je jednosměrná; pokud potřebujete vrátit změny, uchovejte zálohu originálu.

**Q: Jak mohu optimalizovat kvalitu šedotónových rasterizovaných dokumentů?**  
A: Použijte vyšší DPI (300 + pro tiskovou kvalitu) a zvolte vhodný výstupní formát (PDF je běžný pro archivaci).

## Závěr

Nyní máte kompletní, připravený recept pro **vytvoření šedotónových pdf** souborů pomocí GroupDocs.Redaction pro Java. Povolením rasterizace, přidáním pokročilé možnosti šedotónu a zodpovědným řízením prostředků můžete vytvářet zabezpečené, tiskově přívětivé dokumenty, které splňují normy souladu.

---

**Last Updated:** 2026-02-13  
**Tested With:** GroupDocs.Redaction 23.11 for Java  
**Author:** GroupDocs