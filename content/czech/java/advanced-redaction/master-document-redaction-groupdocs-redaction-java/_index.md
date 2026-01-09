---
date: '2025-12-17'
description: Naučte se, jak přidat příponu k názvu souboru a redigovat citlivé informace
  v dokumentech pomocí GroupDocs.Redaction pro Javu. Efektivně zvyšte bezpečnost a
  soukromí dokumentů.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Jak přidat příponu k názvu souboru při redakci dokumentů v Javě s GroupDocs.Redaction
type: docs
url: /cs/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Jak přidat příponu k názvu souboru při redakci dokumentů v Javě s GroupDocs.Redaction

Redakce důvěrných údajů je jen polovina boje—musíte také zajistit, aby uložený soubor jasně naznačoval, že byl zpracován. V tomto průvodci se naučíte **jak přidat příponu k názvu souboru** při ukládání redigovaného dokumentu, spolu s načítáním, anotací a ukládáním pomocí GroupDocs.Redaction pro Javu. Ať už chráníte právní smlouvy, lékařské záznamy nebo finanční zprávy, tyto kroky udrží váš pracovní postup bezpečný a auditovatelný.

## Rychlé odpovědi
- **Co dělá „add suffix to filename“?**  
  Přidá vlastní příponu (např. „_redacted“) k názvu výstupního souboru, takže můžete okamžitě rozpoznat zpracované soubory.
- **Mohu načíst dokument ze streamu?**  
  Ano—GroupDocs.Redaction podporuje načítání z libovolného `InputStream`, ideální pro cloudové úložiště nebo zpracování v paměti.
- **Potřebuji licenci pro tuto funkci?**  
  Bezplatná zkušební verze funguje pro základní redakci; dočasná nebo plná licence odemkne všechny pokročilé možnosti, včetně zpracování přípony.
- **Jaké formáty jsou podporovány?**  
  Knihovna pracuje s DOCX, PDF, PPTX, XLSX a mnoha dalšími.
- **Je rasterizace vyžadována pro výstup PDF?**  
  Rasterizace je volitelná; povolte ji, když potřebujete dokument zploštit pro vyšší zabezpečení.

## Co je přidání přípony k názvu souboru?
Přidání přípony je jednoduchá konvence pojmenování, která signalizuje, že soubor prošel redakcí. Zabraňuje neúmyslnému sdílení původních, neredigovaných verzí a pomáhá automatizovaným pipeline sledovat stav zpracování.

## Proč použít GroupDocs.Redaction pro tento úkol?
GroupDocs.Redaction poskytuje plynulé Java API, které vám umožníovat redakční akce s možnostmi manipulace se soubory—jako **přidání přípony k názvu souboru**—pouze v několika řádcích kódu. To šetří čas vývoje a snižuje riziko manuálních chyb.

## Předpoklady
- **Java Development Kit (JDK):** Verze 8 nebo vyšší.
- **GroupDocs.Redaction Library:** Hlavní knihovna pro úkoly redakce.
- **IDE:** IntelliJ IDEA, Eclipse nebo jakýkoli Java‑kompatibilní editor.
- **Maven:** Pro správu závislostí.

### Znalostní předpoklady
Znalost Java I/O a základních objektově orientovaných konceptů usnadní sledování příkladů.

## Nastavení GroupDocs.Redaction pro Javu
### Maven nastavení
Do souboru `pom.xml` zahrňte následující konfiguraci pro přístup k knihovnám GroupDocs přes Maven:

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
Alternativně stáhněte nejnovější verzi přímo z [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Získání licence
1. **Free Trial:** Přístup k základní funkčnosti bez omezení.  
2. **Temporary License:** Získání dočasné licence pro prozkoumání pokročilých funkcí.  
3. **Purchase:** Pro dlouhodobé používání zvažte zakoupení plné licence.

#### Základní inicializace a nastavení
Inicializujte svůj projekt přidáním potřebných importů:

```java
import com.groupdocs.redaction.Redactor;
```

S tímto nastavením jste připraveni implementovat funkce redakce dokumentů.

## Průvodce implementací

### Funkce 1: Načíst dokument ze streamu
**Přehled:** Naučte se, jak načíst dokumenty do `InputStream` pro zpracování.

#### Krok za krokem implementace
##### Krok 1.1: Vytvořit InputStream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Proč:** Použití `InputStream` vám umožňuje bezproblémově pracovat s dokumenty uloženými v různých formátech, což je nezbytné, když potřebujete **load document from stream** v cloudových nebo mikro‑servisních scénářích.

### Funkce 2: Použít redakci odstranění anotací
**Přehled:** Odstraňte anotace ze svého dokumentu pomocí `DeleteAnnotationRedaction`.

#### Krok za krokem implementace
##### Krok 2.1: Použít DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Proč:** Tento krok zajišťuje, že všechny citlivé anotace jsou odstraněny, čímž se zvyšuje soukromí dokumentu.

### Funkce 3: Uložit dokument s možnostmi
**Přehled:** Naučte se, jak uložit zpracovaný dokument s konkrétními možnostmi, jako je rasterizace a **přidání přípony k názvu souboru**.

#### Krok za krokem implementace
##### Krok 3.1: Konfigurace SaveOptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Proč:** Přizpůsobení možností uložení umožňuje flexibilní výstupní formáty a konvence pojmenování. Povolení `setAddSuffix(true)` **přidá příponu k názvu souboru**, což jasně ukazuje, že soubor byl redigován.

## Proč je přidání přípony důležité
- **Auditovatelnost:** Týmy mohou okamžitě rozpoznat, které soubory jsou bezpečné k distribuci.
- **Automatizace:** Skripty mohou filtrovat soubory podle přípony, čímž se zabrání neúmyslnému zpracování původních dokumentů.
- **Soulad:** Mnoho předpisů vyžaduje jasné označení sanitovaných dokumentů.

## Praktické aplikace
Prozkoumejte tyto reálné příklady použití:
1. **Legal Document Redaction:** Zabezpečte smlouvy před sdílením s klientem.  
2. **Medical Record Handling:** Chraňte identifikátory pacientů.  
3. **Financial Reporting:** Udržujte citlivá čísla důvěrná.  
4. **CRM Integration:** Automaticky odstraňujte zákaznická data před exportem.  
5. **Collaboration Tools:** Zajistěte, aby sdílené koncepty nikdy neodhalily skryté komentáře.

## Úvahy o výkonu
### Optimalizace výkonu
- Používejte streamování (`load document from stream`) k zabránění načítání celých souborů do paměti.  
- Okamžitě uzavřete instance `Redactor`, aby se uvolnily zdroje.

### Pokyny pro využití zdrojů
- Sledujte CPU a paměť během dávkových běhů.  
- Upřednostňujte `ByteArrayOutputStream` pro ukládání v paměti při práci s menšími soubory.

### Nejlepší postupy pro správu paměti v Javě
- Znovu používejte objekty `Redactor` při zpracování více souborů stejného typu.  
- Zavolejte `close()` v bloku `finally` nebo pomocí try‑with‑resources, aby se zabránilo únikům.

## Časté problémy a řešení
| Problém | Příčina | Oprava |
|-------|-------|-----|
| **Suffix not appearing** | `setAddSuffix(false)` nebo chybějící volání | Zajistěte, že `options.setAddSuffix(true)` je nastaveno před `save()`. |
| **OutOfMemoryError on large DOCX** | Načítání celého souboru do paměti | Přepněte na načítání pomocí `InputStream` (viz Funkce 1). |
| **Annotations still visible** | Redakce nebyla aplikována před uložením | Zavolejte `redactor.apply(new DeleteAnnotationRedaction())` před `save()`. |
| **PDF rasterization not applied** | `setRasterizeToPDF(false)` nebo vynecháno | Nastavte `options.setRasterizeToPDF(true)`, když potřebujete zploštělý PDF. |

## Často kladené otázky

**Q: Mohu redigovat PDF dokumenty pomocí GroupDocs.Redaction?**  
A: Ano, knihovna podporuje PDF, DOCX, PPTX, XLSX a mnoho dalších formátů.

**Q: Jaký je nejlepší způsob, jak zacházet s velkými soubory pomocí GroupDocs.Redaction?**  
A: Používejte streamování (`load document from stream`) a rychle uzavírejte zdroje, aby byl nízký odběr paměti.

**Q: Je možné přizpůsobit text přípony?**  
A: API automaticky přidá výchozí příponu (např. „_redacted“). Pro vlastní přípony můžete po uložení soubor přejmenovat.

**Q: Jak získám dočasnou licenci pro GroupDocs.Redaction?**  
A: Navštivte [Temporary License page](https://purchase.groupdocs.com/temporary-license/) a postupujte podle instrukcí.

**Q: Kde mohu získat pomoc, pokud narazím na problémy?**  
A: Připojte se k [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) pro odbornou pomoc.

## Zdroje
- **Documentation:** Prozkoumejte podrobné průvodce na [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Získejte komplexní podrobnosti API na [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Stáhněte nejnovější verzi z [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Přispívejte nebo prozkoumejte zdrojový kód na [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Poslední aktualizace:** 2025-12-17  
**Testováno s:** GroupDocs.Redaction 24.9 pro Javu  
**Autor:** GroupDocs  

---