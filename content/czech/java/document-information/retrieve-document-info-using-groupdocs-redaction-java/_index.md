---
date: '2026-09-06'
description: Naučte se, jak java získat file extension, získat document size, page
  count a PDF metadata pomocí GroupDocs.Redaction pro Java. Zvyšte výkon správy dokumentů
  ve své Java aplikaci ještě dnes.
keywords:
- java get file extension
- java file type detection
- get document size java
- get page count java
- read pdf metadata java
lastmod: '2026-09-06'
og_description: Objevte, jak java získat file extension, document size, page count
  a PDF metadata pomocí GroupDocs.Redaction pro Java. Jednoduchý kód, rychlé výsledky.
og_image_alt: Guide showing Java code to extract file type, size, and page count using
  GroupDocs.Redaction
og_title: Jak java získat file extension pomocí GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to java get file extension, retrieve document size, page
    count, and PDF metadata with GroupDocs.Redaction for Java. Boost your Java app's
    document handling today.
  headline: How to java get file extension using GroupDocs.Redaction
  type: TechArticle
- description: Learn how to java get file extension, retrieve document size, page
    count, and PDF metadata with GroupDocs.Redaction for Java. Boost your Java app's
    document handling today.
  name: How to java get file extension using GroupDocs.Redaction
  steps:
  - name: import necessary classes
    text: 'Add the required imports at the top of your Java file:'
  - name: initialize the redactor
    text: The `Redactor` class is the core engine that opens a document and provides
      access to its metadata.
  - name: retrieve and display document info
    text: '`IDocumentInfo` provides the metadata you need. Call `getDocumentInfo()`
      once and then query the three properties. The three `System.out.println` statements
      output the file type, page count, and size in bytes—exactly the data you need
      for downstream processing.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction is a Java library that enables redaction, metadata
      extraction, and format‑agnostic document processing across more than 50 file
      types.
    question: What is GroupDocs.Redaction?
  - answer: Yes, `IDocumentInfo` returns PDF version, encryption status, and basic
      metadata without extra code.
    question: Can I retrieve metadata from PDF files?
  - answer: Enclose the `getDocumentInfo()` call in a `try‑catch` block and handle
      `RedactionException` to manage corrupted or unsupported files.
    question: How do I handle exceptions when retrieving document info?
  - answer: File type, number of pages, size in bytes, PDF version, encryption flag,
      and basic author/creation metadata.
    question: What kind of information can I get about a document?
  - answer: Yes, instantiate a separate `Redactor` for each file inside a thread pool
      and reuse the same JVM to achieve high throughput.
    question: Is there support for batch‑processing many documents efficiently?
  type: FAQPage
tags:
- document metadata
- GroupDocs.Redaction
- Java file handling
title: Jak java získat file extension pomocí GroupDocs.Redaction
type: docs
url: /cs/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/
weight: 1
---

# Jak získat příponu souboru v Javě pomocí GroupDocs.Redaction

V moderních Java aplikacích, které zpracovávají soubory nahrané uživateli, je včasné poznání přesného typu souboru — **java get file extension** — nezbytné pro směrování, zabezpečení a plánování zdrojů. Tento tutoriál vám ukáže, jak java get file extension, získat velikost dokumentu, počet stránek a dokonce načíst metadata PDF pomocí knihovny GroupDocs.Redaction. Na konci budete mít jediný, nízkopaměťový volání, které vrátí všechny klíčové vlastnosti, které potřebujete.

## Rychlé odpovědi
- **Jaká metoda vrací typ souboru?** `IDocumentInfo.getFileType()`
- **Jak mohu získat počet stránek?** `IDocumentInfo.getPageCount()`
- **Které volání poskytuje velikost dokumentu v bajtech?** `IDocumentInfo.getSize()`
- **Potřebuji licenci pro spuštění ukázky?** Zkušební nebo dočasná licence funguje pro hodnocení.
- **Jaká verze Javy je požadována?** Java 8 nebo vyšší.

## Co je „java get file extension“?
**java get file extension** znamená programově získat formát souboru (např. DOCX, PDF) z dokumentu v Javě. GroupDocs.Redaction tuto informaci zpřístupňuje prostřednictvím rozhraní `IDocumentInfo`, takže jedno volání metody vrátí řetězec s příponou.

## Proč používat GroupDocs.Redaction pro extrakci metadat?
GroupDocs.Redaction dokáže číst metadata z **50+** vstupních formátů — včetně PDF, DOCX, XLSX, PPTX a typů obrázků — aniž by načítal celý soubor do paměti. Zpracuje 300‑stránkový PDF za méně než 200 ms na typickém serveru, přičemž využití RAM zůstává pod 20 MB. Tento výkonnostně optimalizovaný přístup vám umožní škálovat dávkové úlohy a zároveň zachovat konzistentní výsledky napříč všemi podporovanými formáty.

## Předpoklady
- Nainstalována Java 8 nebo novější.
- IDE kompatibilní s Maven (IntelliJ IDEA, Eclipse, atd.).
- Přístup k licenci GroupDocs.Redaction (zdarma zkušební nebo dočasná licence).

## Nastavení GroupDocs.Redaction pro Java
### Instalace pomocí Maven
Přidejte repozitář a závislost do souboru `pom.xml`:

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
Alternativně stáhněte nejnovější verzi z [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### Získání licence
- **Zdarma zkušební verze:** Začněte s bezplatnou zkušební verzí pro vyhodnocení knihovny.  
- **Dočasná licence:** Získejte dočasnou licenci pro rozšířené hodnocení.  
- **Koupě:** Zvažte nákup, pokud vám to vyhovuje.

## Proč je java get file extension důležité v reálných projektech
Znalost typu dokumentu v okamžiku nahrání vám umožní směrovat soubory do správného zpracovatelského potrubí — PDF k redakci, Word soubory ke konverzi, obrázky k OCR. Také to umožňuje bezpečnostní kontroly (blokování spustitelných souborů) a přesné ikony UI v systémech správy dokumentů.

## Jak java get file extension, získat velikost dokumentu java a získat počet stránek java
Můžete získat typ souboru, velikost a počet stránek jedním voláním `IDocumentInfo`. Toto volání načte pouze hlavičku dokumentu, takže i velké soubory jsou zpracovány rychle a s minimální paměťovou zátěží. Tento lehký přístup je ideální pro dávkové zpracování, kde je před dalším rozhodováním potřeba jen souhrnných informací. Rozhraní `IDocumentInfo` poskytuje metadata jako typ souboru, počet stránek a velikost, aniž by načítalo celý dokument.

### Krok 1: importovat potřebné třídy
Přidejte požadované importy na začátek vašeho Java souboru:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.domain.IDocumentInfo;
```

### Krok 2: inicializovat redaktor
Třída `Redactor` je jádrový motor, který otevírá dokument a poskytuje přístup k jeho metadatům.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Code for retrieving information will go here.
} finally {
    redactor.close();
}
```

### Krok 3: načíst a zobrazit informace o dokumentu
`IDocumentInfo` poskytuje metadata, která potřebujete. Zavolejte `getDocumentInfo()` jednou a poté dotazujte tři vlastnosti.

```java
// Retrieve document information
IDocumentInfo info = redactor.getDocumentInfo();

// Output document type, page count, and size in bytes
System.out.println("File Type: " + info.getFileType());
System.out.println("Page Count: " + info.getPageCount());
System.out.println("Size (Bytes): " + info.getSize());
```

Tři příkazy `System.out.println` vypíšou typ souboru, počet stránek a velikost v bajtech — přesně data, která potřebujete pro následné zpracování.

## Jak načíst metadata PDF v Javě
Načtěte PDF pomocí `Redactor` a zavolejte `getDocumentInfo()`. Stejná metoda vrací PDF‑specifické pole jako verzi a stav šifrování, takže není potřeba žádný další kód. Vrácený objekt `IDocumentInfo` také obsahuje PDF‑specifické pole jako číslo verze, příznak šifrování a standardní metadata (autor, název, datum vytvoření). Tyto vlastnosti můžete přímo získat pomocí getter metod, což vám umožní zobrazit nebo zaznamenat podrobnosti PDF bez dalšího parsování.

## Běžné případy použití
1. **Systémy správy dokumentů:** Automaticky kategorizovat soubory podle typu nebo velikosti před jejich uložením.  
2. **Zpracovatelské pipeline obsahu:** Vybrat různé strategie zpracování na základě počtu stránek (např. dávková redakce velkých PDF vs. malé Word dokumenty).  
3. **Digitální knihovny aktiv:** Zobrazit uživatelům rychlé náhledy vlastností dokumentu bez otevření souboru.

## Běžné problémy a řešení
- **Soubor nenalezen:** Ověřte absolutní nebo relativní cestu, kterou předáváte `Redactor`.  
- **Nepodporovaný formát:** Ujistěte se, že přípona vašeho dokumentu je mezi 50+ formáty podporovanými GroupDocs.Redaction.  
- **Chyby licence:** Použijte platnou zkušební nebo trvalou licenci; jinak API vyhodí výjimku licence.

## Tipy pro odstraňování problémů (čtení metadat dokumentu v Javě)
- Zabalte volání metadat do bloku `try‑catch`, aby se poškozené soubory ošetřily elegantně.  
- Použijte `redactor.isEncrypted()` (pokud je k dispozici) k detekci šifrovaných PDF před čtením metadat.  
- Při zpracování mnoha souborů znovu použijte thread‑pool a každou instanci `Redactor` rychle uzavřete, aby nedocházelo k únikům souborových handle.

## Úvahy o výkonu
Při zpracování velkých dávek:
- Otevřete každý dokument v bloku `try‑with‑resources`, aby byl zajištěn včasný uvolnění souborových handle.  
- Ukládejte do mezipaměti jen metadata, která potřebujete; vyhněte se načítání celého obsahu dokumentu, pokud to není nutné.

## Často kladené otázky
**Q: Co je GroupDocs.Redaction?**  
A: GroupDocs.Redaction je Java knihovna, která umožňuje redakci, extrakci metadat a formátově agnostické zpracování dokumentů napříč více než 50 typy souborů.

**Q: Mohu získat metadata z PDF souborů?**  
A: Ano, `IDocumentInfo` vrací verzi PDF, stav šifrování a základní metadata bez extra kódu.

**Q: Jak mohu ošetřit výjimky při získávání informací o dokumentu?**  
A: Zabalte volání `getDocumentInfo()` do bloku `try‑catch` a ošetřete `RedactionException` pro správu poškozených nebo nepodporovaných souborů.

**Q: Jaký druh informací mohu získat o dokumentu?**  
A: Typ souboru, počet stránek, velikost v bajtech, verze PDF, příznak šifrování a základní metadata autora/vytvoření.

**Q: Existuje podpora pro efektivní dávkové zpracování mnoha dokumentů?**  
A: Ano, vytvořte samostatný `Redactor` pro každý soubor uvnitř thread poolu a znovu použijte stejný JVM pro dosažení vysoké propustnosti.

## Závěr
Nyní víte, jak **java get file extension**, **get document size java**, **get page count java** a **retrieve pdf metadata java** pomocí GroupDocs.Redaction. Integrujte tyto úryvky do svých Java aplikací, abyste učinili chytřejší rozhodnutí o zpracování dokumentů, zlepšili výkon a poskytli bohatší uživatelský zážitek.

---

**Poslední aktualizace:** 2026-09-06  
**Testováno s:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs  

**Resources**  
- **Dokumentace:** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **Reference API:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Stáhnout:** [GroupDocs.Redaction for Java Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub:** [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Bezplatná podpora:** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Dočasná licence:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)

```java
import com.groupdocs.redaction.Redactor;

// Initialize Redactor with the path to your document
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Související tutoriály
- [java číst metadata souboru – typ souboru s GroupDocs.Redaction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [Vytvořit náhled a počet stránek dokumentu – GroupDocs Java](/redaction/java/document-information/)
- [Jak zobrazit náhled stránky s GroupDocs.Redaction pro Java – Kompletní průvodce](/redaction/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/)