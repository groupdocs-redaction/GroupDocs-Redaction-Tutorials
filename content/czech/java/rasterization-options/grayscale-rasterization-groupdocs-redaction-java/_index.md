---
date: '2026-05-17'
description: Zjistěte, jak rasterizovat PDF do odstínů šedi pomocí GroupDocs.Redaction
  pro Java, aplikovat filtr šedých odstínů a udržet své dokumenty zabezpečené a vysoce
  kvalitní.
keywords:
- how to rasterize pdf
- java pdf to image
- apply grayscale filter pdf
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to rasterize PDF to grayscale using GroupDocs.Redaction for
    Java, apply a grayscale filter, and keep your documents secure and high‑quality.
  headline: How to rasterize PDF to grayscale with GroupDocs.Redaction Java – Secure
    and Optimize Your Documents
  type: TechArticle
- questions:
  - answer: In GroupDocs.Redaction, the grayscale option is tied to rasterization,
      which ensures consistent results and adds a security layer.
    question: Can I convert documents to grayscale without rasterization?
  - answer: All major formats supported by GroupDocs.Redaction—including DOCX, PDF,
      XLSX, PPTX, RTF, and more than 100 others—can be rasterized and converted to
      grayscale.
    question: What document formats support grayscale rasterization?
  - answer: Yes. Text‑heavy files may grow, while image‑heavy files might shrink.
      DPI settings have the biggest impact.
    question: Will rasterization affect the file size of my documents?
  - answer: No. Rasterization is one‑way; keep a backup of the original if you need
      to revert.
    question: Is it possible to reverse the grayscale rasterization process?
  - answer: Use a higher DPI (300 + for print quality) and choose PDF as the output
      format for best archival results.
    question: How can I optimize the quality of grayscale rasterized documents?
  type: FAQPage
title: Jak rasterizovat PDF do odstínů šedi pomocí GroupDocs.Redaction Java – Zabezpečte
  a optimalizujte své dokumenty
type: docs
url: /cs/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# Jak rasterizovat PDF do odstínů šedi pomocí GroupDocs.Redaction Java

Chtěli byste **rasterizovat PDF** do odstínů šedi a zároveň zachovat bezpečnost, profesionální vzhled a snadnou archivaci dokumentů, jste na správném místě. V tomto tutoriálu projdeme přesné kroky, jak převést barevné DOCX, PDF nebo jiné podporované soubory do čisté, šedé rasterizované verze pomocí GroupDocs.Redaction pro Java. Pochopíte, proč rasterizace přidává bezpečnostní vrstvu, jak nakonfigurovat knihovnu a jak efektivně spravovat zdroje – vše představeno přátelským, krok‑za‑krokem stylem.

## Rychlé odpovědi
- **Co dělá rasterizace do odstínů šedi?** Převádí každou stránku na vysoce rozlišený obrázek a poté aplikuje filtr šedé, odstraňující veškeré informace o barvě.  
- **Proč použít GroupDocs.Redaction?** Spojuje bezpečnost redakce s možnostmi rasterizace v jediné, snadno použitelném API.  
- **Jaké formáty jsou podporovány?** DOCX, PDF, XLSX, PPTX, RTF a více než 100 dalších formátů.  
- **Potřebuji licenci?** Pro produkční nasazení je vyžadována platná licence GroupDocs.Redaction; pro testování je k dispozici bezplatná zkušební verze.  
- **Jaká verze Javy je požadována?** JDK 8 nebo vyšší.

## Jak rasterizovat PDF do odstínů šedi?

Načtěte svůj zdrojový dokument pomocí `new Redactor("path/to/file")`, povolte rasterizaci pomocí `RasterizationOptions`, přidejte pokročilou možnost šedé a zavolejte `save()` — celá konverze proběhne v několika stručných řádcích. Tento přístup zaručuje, že každá stránka se stane obrázkovým, černobílým PDF, což zabraňuje výběru textu a zajišťuje jednotný vzhled připravený k tisku.

## Co je **create grayscale pdf**?

Vytvoření šedého PDF znamená převod každého vizuálního prvku původního dokumentu do odstínů šedi. Výsledkem je menší, tiskově přátelský soubor, který odstraňuje rušivé barvy a přidává jemný bezpečnostní přínos, protože obsah je nyní založen na obrázku.

## Proč použít rasterizaci do odstínů šedi s GroupDocs.Redaction?

Rasterizace převádí každou stránku na obrázek, což znamená, že text nelze kopírovat ani upravovat, a vizuální výstup zůstává konzistentní napříč tiskárnami a prohlížeči. GroupDocs.Redaction podporuje **více než 100 vstupních a výstupních formátů** — včetně DOCX, XLSX, PPTX, HTML a typů obrázků — takže můžete použít stejný postup téměř na jakýkoli dokument.

## Požadavky

- Java Development Kit (JDK) 8 nebo novější. Ověřte pomocí `java -version`.  
- IDE (IntelliJ IDEA, Eclipse nebo NetBeans) pro snadnější kódování a ladění.  
- GroupDocs.Redaction pro Java přidaný přes Maven nebo Gradle.  
- Vzorek dokumentu (např. více‑stránkový DOCX), na kterém můžete bezpečně experimentovat.  
- Dostatečný volný diskový prostor pro rasterizovaný výstup (raster soubory mohou být větší než zdroj).

## Import balíčků

Následující importy přinášejí jádro třídy Redactor a rasterizační třídy potřebné pro příklad.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Krok 1: Inicializace objektu Redactor

Třída `Redactor` je vstupním bodem pro všechny operace zpracování dokumentů v GroupDocs.Redaction. Vytvoření instance otevírá možnost načítání, úprav a ukládání dokumentů.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

Nahraďte `Constants.MULTIPAGE_SAMPLE_DOCX` cestou k souboru, který chcete převést na šedé PDF.

## Krok 2: Konfigurace možností uložení

Třída `SaveOptions` určuje, jak bude zpracovaný dokument zapsán na disk, včetně formátu a názvu souboru.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

Výstup bude pojmenován `yourfile_scan.pdf` (nebo formát, který později určíte).

## Krok 3: Povolení rasterizace

Objekt `RasterizationOptions` umožňuje obrázkový rendering každé stránky před uložením.

```java
so.getRasterization().setEnabled(true);
```

## Krok 4: Aplikace převodu na šedou

`AdvancedRasterizationOptions.Grayscale` je příznak, který vynutí, aby rasterizovaný obrázek používal pouze odstíny šedi.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

## Krok 5: Provedení transformace dokumentu

Volání `save()` spustí celý zpracovatelský řetězec a zapíše výstupní soubor.

```java
redactor.save(so);
```

Po provedení tohoto řádku najdete na disku nový soubor, který je plně rasterizovaný, šedý a uložený s příponou `_scan`.

## Krok 6: Správná správa zdrojů

Metoda `close()` uvolňuje nativní zdroje a maže dočasné soubory.

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

Vyšší DPI poskytuje ostřejší obrázky (dobré pro tisk), zatímco nižší DPI snižuje velikost souboru. Běžná rovnováha je 150 DPI pro zobrazení na obrazovce a 300 DPI pro tiskové PDF.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Výběr výstupního formátu

Můžete vynutit, aby rasterizovaný výsledek byl v konkrétním kontejnerovém formátu, jako je PDF, TIFF nebo PNG. PDF je nejčastěji používaný archivní formát.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Běžné případy použití

- **Archivace právních dokumentů** – vytvořte neměnitelné šedé PDF, které nelze upravovat.  
- **Reporty připravené k tisku** – zajistěte konzistentní černobílý výstup pro hromadný tisk.  
- **Workflowy pro soulad** – kombinujte redakci s rasterizací do šedé, aby vyhovovaly přísným předpisům o ochraně dat.

## Běžné problémy a řešení

| Problém | Proč k tomu dochází | Řešení |
|-------|----------------|-----|
| Výstupní soubor je větší, než se očekává | DPI nastaveno příliš vysoké nebo je vypnuta komprese obrázků | Snižte DPI (např. 150) nebo povolte kompresi v `RasterizationOptions`. |
| Text je rozmazaný | Nedostatečné DPI pro původní velikost písma | Zvyšte DPI na 300 nebo více. |
| Proces vyhodí `OutOfMemoryError` u velkých dokumentů | Celý dokument je načten do paměti | Použijte streamingové API nebo zpracovávejte stránky po dávkách, pokud je to podporováno. |
| Šedá barva není aplikována | Pokročilá možnost nebyla správně přidána | Ověřte, že `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` je zavoláno před `save()`. |

## Často kladené otázky

**Q: Mohu převést dokumenty na šedou bez rasterizace?**  
A: V GroupDocs.Redaction je možnost šedé spojena s rasterizací, která zajišťuje konzistentní výsledky a přidává bezpečnostní vrstvu.

**Q: Jaké formáty dokumentů podporují rasterizaci do odstínů šedi?**  
A: Všechny hlavní formáty podporované GroupDocs.Redaction — včetně DOCX, PDF, XLSX, PPTX, RTF a více než 100 dalších — lze rasterizovat a převést do šedé.

**Q: Ovlivní rasterizace velikost souboru mých dokumentů?**  
A: Ano. Soubory s velkým množstvím textu mohou narůst, zatímco soubory s mnoha obrázky se mohou zmenšit. Nastavení DPI má největší dopad.

**Q: Je možné proces rasterizace do šedé obrátit?**  
A: Ne. Rasterizace je jednosměrná; pokud potřebujete vrátit změny, uchovejte zálohu originálu.

**Q: Jak mohu optimalizovat kvalitu šedých rasterizovaných dokumentů?**  
A: Použijte vyšší DPI (300 + pro tiskovou kvalitu) a zvolte PDF jako výstupní formát pro nejlepší archivní výsledek.

## Závěr

Nyní máte kompletní, připravený recept pro **rasterizaci PDF do odstínů šedi** pomocí GroupDocs.Redaction pro Java. Povolením rasterizace, přidáním pokročilé možnosti šedé a zodpovědným řízením zdrojů můžete vytvářet bezpečné, tiskové dokumenty, které splňují normy souladu a vypadají konzistentně ve všech prohlížečích.

---

**Poslední aktualizace:** 2026-05-17  
**Testováno s:** GroupDocs.Redaction 23.11 pro Java  
**Autor:** GroupDocs  

---

## CÍLOVÉ KLÍČOVÉ SLOVA:

**Primární klíčové slovo (NEJVYŠŠÍ PRIORITA):**  
how to rasterize pdf

**Sekundární klíčová slova (PODPŮRÁ):**  
java pdf to image, apply grayscale filter pdf

## Související tutoriály

- [Tutoriály možností rasterizace pro GroupDocs.Redaction Java](/redaction/java/rasterization-options/)
- [Jak používat groupdocs redaction pro Java: Před‑rasterizace ve Word dokumentech](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)
- [Vlastní šumová rasterizace v Java&#58; Zabezpečení citlivých informací pomocí GroupDocs.Redaction](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)