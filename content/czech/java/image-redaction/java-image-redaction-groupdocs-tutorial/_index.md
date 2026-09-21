---
date: '2026-09-21'
description: Naučte se, jak odmazat obrázek pomocí GroupDocs.Redaction for Java. Průvodce
  krok za krokem pokrývá nastavení, pixel‑level redaction, ověření a osvědčené postupy.
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: Jak odmazat obrázek pomocí GroupDocs.Redaction for Java. Postupujte
  podle tohoto průvodce, abyste maskovali pixelová data ve skenovaných souborech,
  vybrali barvy a ověřili výsledky — ideální pro soulad s GDPR a HIPAA.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: Jak odmazat obrázek pomocí GroupDocs.Redaction for Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: Jak odmazat obrázek pomocí GroupDocs.Redaction for Java
type: docs
url: /cs/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Jak redigovat obrázek pomocí GroupDocs.Redaction pro Java

V tomto komplexním tutoriálu se naučíte **jak redigovat obrázek** v Javě pomocí GroupDocs.Redaction. Redigování naskenovaných obrázků je klíčovým krokem pro ochranu osobních údajů, splnění požadavků GDPR, HIPAA nebo jiných předpisů o ochraně soukromí a zajištění, že důvěrné vizuální informace nikdy neuniknou. Provedeme vás nastavením projektu, konfigurací redigování na úrovni pixelů, bezpečným uložením výsledku a ověřením úspěšnosti redigování – vše v konverzačním, krok‑za‑krokem stylu, který můžete zkopírovat do jakékoli Java aplikace.

## Rychlé odpovědi
- **Jaká knihovna provádí redigování obrázků v Javě?** GroupDocs.Redaction for Java.  
- **Mohu si vybrat barvu redigování?** Ano – libovolná neprůhledná `java.awt.Color`, například `Color.BLUE` nebo `Color.BLACK`.  
- **Je pro produkci vyžadována licence?** Ano, platná licence GroupDocs je povinná pro komerční použití.  
- **Bude původní obrázek přepsán?** Ne – API zapíše redigovaný obrázek do nového souboru, který určíte.  
- **Jaká verze Javy je podporována?** Java 8 a novější (až do Java 21 v době psaní).

## Co je redigování obrázku a proč redigovat naskenovaný obrázek v Javě?
Redigování obrázku trvale zakrývá vizuální data—jména, čísla, podpisy—nahrazením oblastí pixelů jednotnou barvou. Na rozdíl od redigování textu, které pracuje s výběrovými znaky, naskenované obrázky ukládají informace jako surové pixely, takže pouze nástroje založené na pixelech mohou zaručit, že data nelze obnovit. Pomocí GroupDocs.Redaction můžete cílit na přesné souřadnice, použít libovolnou neprůhlednou barvu a vytvořit nový obrázek, který trvale odstraní citlivý obsah.

## Proč použít GroupDocs.Redaction pro Java?
GroupDocs.Redaction podporuje **více než 50 formátů obrázků** (včetně JPG, PNG, BMP, GIF) a může zpracovávat dokumenty s mnoha stovkami stránek, aniž by načítal celý soubor do paměti, díky své streamovací architektuře. Benchmarky ukazují, že 300 KB naskenovaný PNG je redigován za méně než 120 ms na typickém 2,8 GHz procesoru, což jej činí vhodným jak pro dávkové úlohy, tak pro služby v reálném čase.

## Předpoklady
- **JDK 8 nebo novější** nainstalováno a nakonfigurováno ve vašem `PATH`.  
- **Maven** (nebo Gradle) pro správu závislostí.  
- IDE, například **IntelliJ IDEA**, **Eclipse** nebo **NetBeans**.  
- Základní znalost Java I/O souborů a balíčku `java.awt`.  

## Nastavení GroupDocs.Redaction pro Java

### Nastavení Maven
Přidejte repozitář GroupDocs a závislost do vašeho `pom.xml`:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### Přímé stažení
Alternativně stáhněte nejnovější JAR z oficiální stránky vydání: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Získání licence
- **Bezplatná zkušební verze:** Zaregistrujte se k vyzkoušení plného API.  
- **Dočasná licence:** Použijte dočasný klíč pro rozšířené testování zdarma.  
- **Plná koupě:** Získejte produkční licenci pro neomezené nasazení.  

## Průvodce implementací

Rozdělíme implementaci na dvě hlavní funkce: **redigování oblasti obrázku** (skutečné maskování) a **kontrola stavu redigování** (ověření úspěchu).

### Jak redigovat naskenované obrázky dokumentů – krok 1: inicializace redaktoru
`Redactor` je centrální třída, která načítá obrázek a poskytuje operace redigování.  
Vytvořte instanci `Redactor`, která ukazuje na zdrojový obrázek, který chcete zpracovat.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Krok 2: definování parametrů redigování
`ImageAreaRedaction` pracuje s `Point` (levý horní roh) a `Dimension` (šířka × výška), které popisují obdélník k zakrytí. V tomto příkladu používáme modrou výplňovou barvu.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Krok 3: aplikace redigování
`RegionReplacementOptions` vám umožňuje specifikovat výplňovou barvu a volitelný okraj. Předáním těchto možností do `ImageAreaRedaction` a voláním `apply()` provede maskování. Metoda vrací `RedactorChangeLog`, který udává úspěch nebo selhání.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Krok 4: uvolnění prostředků
`Redactor` implementuje `AutoCloseable`. Uzavřením uvolní nativní buffery a souborové handly, čímž zabraňuje únikům paměti v dlouhodobě běžících službách.

```java
redactor.close();
```

### Jak ověřit redigování – kontrola stavu
Po aplikaci redigování zkontrolujte `RedactorChangeLog`. Hodnota `Status.SUCCESS` potvrzuje, že oblast pixelů byla nahrazena bez chyby. Můžete také vykreslit obrázek do `BufferedImage` pro vizuální kontrolu před uložením.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Praktické aplikace
- **Zpracování důvěrných dokumentů:** Zakryjte osobní údaje v naskenovaných smlouvách před sdílením s partnery.  
- **Právní dokumentace:** Zajistěte soulad s GDPR nebo HIPAA redigováním identifikátorů na důkazních obrázcích.  
- **Zdravotní záznamy:** Skryjte tváře pacientů nebo ručně psané poznámky na radiologických skenech při zachování diagnostických detailů.  

## Úvahy o výkonu
- **Dávkové zpracování:** Zpracovávejte obrázky ve skupinách po 10–20, aby využití paměti zůstalo pod 200 MB.  
- **Opětovné použití objektů:** Znovu používejte objekty `Point` a `Dimension` napříč iteracemi ke snížení zatížení GC.  
- **Aktualizace verzí:** Aktualizujte na nejnovější vydání GroupDocs.Redaction a využijte 15 % zrychlení, o kterém je hlášeno ve verzi 24.10.  

## Časté problémy a řešení
| Problém | Příčina | Řešení |
|-------|-------|-----|
| **Redigování selže se stavem `Failed`** | Nesprávná cesta k souboru nebo nepodporovaný formát obrázku | Ověřte, že soubor existuje a je podporovaného formátu (JPG, PNG, BMP, GIF). |
| **Výstupní soubor je prázdný** | `redactor.save()` byl zavolán před dokončením redigování | Ujistěte se, že `apply()` vrací `Status.SUCCESS` před voláním `save()`. |
| **Barva nebyla použita** | Použití průhledné `Color` | Zvolte neprůhlednou barvu, například `Color.BLACK` nebo `Color.BLUE`. |

## Často kladené otázky

**Q: Jaký je rozdíl mezi `ImageAreaRedaction` a redigováním textu?**  
A: `ImageAreaRedaction` pracuje s surovými souřadnicemi pixelů, zatímco redigování textu parsuje OCR vrstvy k nalezení a odstranění textového obsahu.

**Q: Mohu redigovat více oblastí v jednom obrázku?**  
A: Ano—voláním `redactor.apply()` opakovaně s různými objekty `ImageAreaRedaction` před uložením finálního souboru.

**Q: Podporuje GroupDocs.Redaction další formáty obrázků, jako je TIFF?**  
A: Knihovna podporuje běžné rastrové formáty (JPG, PNG, BMP, GIF). Pro TIFF nejprve převěďte obrázek do podporovaného formátu.

**Q: Jak mohu automatizovat redigování pro složku naskenovaných PDF?**  
A: Extrahujte každou stránku jako obrázek, aplikujte stejnou logiku redigování a poté znovu vytvořte PDF pomocí PDF knihovny, například GroupDocs.Conversion.

**Q: Existuje způsob, jak si před uložením prohlédnout redigování?**  
A: Vykreslete `Redactor` do `BufferedImage` a zobrazte jej v UI Swing nebo JavaFX, což vám umožní potvrdit zakrytou oblast před potvrzením.

## Závěr
Nyní máte kompletní, připravený průvodce pro produkci o **tom, jak redigovat obrázek** a konkrétně **jak redigovat naskenovaný obrázek v Javě** pomocí GroupDocs.Redaction pro Java. Dodržením výše uvedených kroků můžete chránit citlivá vizuální data ve finančním, právním a zdravotnickém sektoru. Prozkoumejte další API—například redigování textu, redigování stránek PDF nebo hromadné zpracování složek—abyste vytvořili end‑to‑end pipeline pro ochranu dat ve vaší organizaci.

**Zdroje**  
- [Dokumentace](https://docs.groupdocs.com/redaction/java/)  
- [API reference](https://reference.groupdocs.com/redaction/java)  
- [Stáhnout](https://releases.groupdocs.com/redaction/java/)  
- [GitHub repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Bezplatné fórum podpory](https://forum.groupdocs.com/c/redaction/33)  
- [Dočasná licence](https://purchase.groupdocs.com/temporary-license/) 

---

**Poslední aktualizace:** 2026-09-21  
**Testováno s:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs

## Související tutoriály

- [Jak redigovat Java s GroupDocs.Redaction - Komplexní průvodce pro vývojáře](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [Jak redigovat naskenované PDF s OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Jak redigovat text v Javě s GroupDocs.Redaction – Průvodce](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)