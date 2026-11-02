---
date: '2026-11-02'
description: Ismerje meg, hogyan adhat hozzá utótagot a fájlnévhez egy GroupDocs redaction
  Java útmutatóban Maven, streaming load, annotation deletion és save options használatával.
keywords:
- groupdocs redaction java tutorial
- add suffix filename java
- document redaction workflow
- groupdocs maven dependency
- java inputstream redaction
lastmod: '2026-11-02'
og_description: Ismerje meg, hogyan adhat hozzá utótagot a fájlnévhez egy GroupDocs
  redaction Java útmutatóban. Kövesse a lépésről‑lépésre útmutatót Maven beállításhoz,
  streaming load-hoz és save options-hoz.
og_image_alt: Guide showing Java code to add suffix to redacted filenames using GroupDocs
  Redaction
og_title: Hogyan adjon hozzá utótagot a fájlnévhez a GroupDocs redaction Java-ban
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  headline: How to add suffix to filename in GroupDocs redaction Java
  type: TechArticle
- description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  name: How to add suffix to filename in GroupDocs redaction Java
  steps:
  - name: '1: Create InputStream'
    text: '- **Why:** Using `InputStream` allows you to handle documents stored in
      various locations—cloud buckets, databases, or in‑memory buffers—without first
      writing them to disk. This approach is essential when you need to **load document
      from stream** in micro‑service architectures.'
  - name: '1: Apply DeleteAnnotationRedaction'
    text: '- **Why:** This step ensures that any sensitive annotations (comments,
      highlights, or hidden notes) are stripped from the document, enhancing privacy
      and compliance.'
  - name: '1: Configure SaveOptions'
    text: '- **Why:** Customizing save options allows flexible output formats and
      naming conventions. Enabling `setAddSuffix(true)` **adds suffix to filename**,
      making it clear that the file has been redacted.'
  type: HowTo
- questions:
  - answer: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.
    question: Can I redact PDF documents using GroupDocs.Redaction?
  - answer: Use streaming (`load document from stream`) and close resources promptly
      to keep memory usage low.
    question: What is the best way to handle large files with GroupDocs.Redaction?
  - answer: The API automatically adds a default suffix (e.g., “_redacted”). For custom
      suffixes, rename the output file after saving.
    question: Is it possible to customize the suffix text?
  - answer: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/)
      and follow the instructions.
    question: How do I obtain a temporary license for GroupDocs.Redaction?
  - answer: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for expert assistance.
    question: Where can I get help if I encounter issues?
  type: FAQPage
tags:
- groupdocs redaction
- java tutorial
- maven dependency
- document redaction
title: Hogyan adjon hozzá utótagot a fájlnévhez a GroupDocs redaction Java-ban
type: docs
url: /hu/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Hogyan adjon hozzá utótagot a fájlnévhez a GroupDocs redaction Java-ban

Ebben a **groupdocs redaction java tutorial**-ban megtanulja, hogyan lehet automatikusan hozzáfűzni egy utótagot a kimeneti fájlnévhez a dokumentumok redakciója során a GroupDocs.Redaction használatával. Az utótag hozzáadása megszünteti a kézi átnevezést, csökkenti a nem redaktált fájlok kiszivárgásának kockázatát, és zökkenőmentesen illeszkedik a névadási konvenciókra támaszkodó CI/CD folyamatokba. Az útmutató végigvezeti a Maven beállításon, a dokumentum streaming betöltésén, az annotációk eltávolításán és a mentési beállítások konfigurálásán – mindezt tömör, termelésre kész kóddal.

## Gyors válaszok
- **Mi a “add suffix to filename” funkció?**  
  Amikor engedélyezi az utótag opciót, az SDK automatikusan hozzáfűz egy előre meghatározott karakterláncot (alapértelmezés szerint “_redacted”) a kimeneti fájl alapnevéhez a kiterjesztés előtt. Ez azonnal egyértelművé teszi, mely fájlok lettek feldolgozva, segít megakadályozni az eredeti tartalom véletlen terjesztését, és egyszerűsíti a névadási mintákat használó downstream automatizálást.  
- **Betölthetek dokumentumot streamből?**  
  Igen – a GroupDocs.Redaction támogatja a betöltést bármely `InputStream`‑ből, ami tökéletes a felhőalapú tároláshoz vagy a memória‑beli feldolgozáshoz.  
- **Szükségem van licencre ehhez a funkcióhoz?**  
  Az ingyenes próba a alapvető redakcióhoz működik; egy ideiglenes vagy teljes licenc feloldja az összes fejlett opciót, beleértve az utótag kezelését is.  
- **Mely formátumok támogatottak?**  
  A könyvtár kezeli a DOCX, PDF, PPTX, XLSX és még sok más formátumot.  
- **Szükséges a rasterizálás PDF kimenethez?**  
  A rasterizálás opcionális; engedélyezze, ha a dokumentumot extra biztonság érdekében laposra kell tenni.

## Mit csinál a “add suffix to filename” funkció?

Amikor engedélyezi az utótag opciót, az SDK automatikusan hozzáfűz egy előre meghatározott karakterláncot (alapértelmezés szerint “_redacted”) a kimeneti fájl alapnevéhez a kiterjesztés előtt. Ez azonnal egyértelművé teszi, mely fájlok lettek feldolgozva, segít megakadályozni az eredeti tartalom véletlen terjesztését, és egyszerűsíti a névadási mintákat használó downstream automatizálást.

## Miért használja a GroupDocs.Redaction-t ehhez a feladathoz?

A GroupDocs.Redaction egy nagy teljesítményű Java API‑t kínál, amely a redakciós műveleteket rugalmas fájlkezelési lehetőségekkel, például automatikus utótag hozzáadással, streaming támogatással és kötegelt feldolgozással kombinálja. Több mint 50 bemeneti és kimeneti formátumot támogat, és több száz oldalas dokumentumokat képes feldolgozni anélkül, hogy a teljes fájlt a memóriába töltené, ezáltal alacsony memóriahasználatot és gyors végrehajtást biztosít.

## Előfeltételek

- **Java Development Kit (JDK):** 8-as vagy újabb verzió.  
- **GroupDocs.Redaction Library:** A redakciós feladatokhoz szükséges alapkönyvtár.  
- **IDE:** IntelliJ IDEA, Eclipse vagy bármely Java‑kompatibilis szerkesztő.  
- **Maven:** A függőségkezeléshez.  

### Tudás előfeltételek
A Java I/O és az alapvető objektum‑orientált koncepciók ismerete megkönnyíti a példák követését.

## A GroupDocs.Redaction beállítása Java-hoz

### Maven beállítás
Include the following configuration in your `pom.xml` file to access GroupDocs libraries via Maven:

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

### Közvetlen letöltés
Alternatívaként töltse le a legújabb verziót közvetlenül a [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) oldalról.

### Licenc beszerzése
1. **Free trial:** Alapfunkciók korlátozás nélkül.  
2. **Temporary license:** Ideiglenes licenc beszerzése a fejlett funkciók kipróbálásához.  
3. **Purchase:** Hosszú távú használathoz fontolja meg egy teljes licenc megvásárlását.

#### Alap inicializálás és beállítás
Initialize your project by adding the necessary imports:

```java
import com.groupdocs.redaction.Redactor;
```

With this setup, you're ready to implement document redaction functionalities.

## Implementációs útmutató

### Funkció 1: dokumentum betöltése streamből
**Áttekintés:** Tanulja meg, hogyan töltsön be dokumentumokat egy `InputStream`‑be feldolgozás céljából.

`InputStream` egy Java I/O osztály, amely bájtfolyamot képvisel, lehetővé téve adatok olvasását fájlokból, hálózati kapcsolatokból vagy más forrásokból anélkül, hogy a teljes tartalmat a memóriába töltené.

#### 1.1. lépés: inputstream létrehozása

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

- **Miért:** Az `InputStream` használatával különböző helyeken tárolt dokumentumokat—felhő tárolókat, adatbázisokat vagy memória‑beli puffereket—kezelhet anélkül, hogy előbb lemezre írna. Ez a megközelítés elengedhetetlen, ha **load document from stream**‑et kell végrehajtani mikro‑szolgáltatás architektúrákban.

### Funkció 2: annotáció törlés redakció alkalmazása
**Áttekintés:** Távolítsa el a dokumentum annotációit a `DeleteAnnotationRedaction` használatával.

`DeleteAnnotationRedaction` egy redakciós művelet, amely eltávolítja az összes annotációt—például megjegyzéseket, kiemeléseket és jegyzeteket—a dokumentumból.

#### 2.1. lépés: deleteannotationredaction alkalmazása

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Miért:** Ez a lépés biztosítja, hogy minden érzékeny annotáció (megjegyzések, kiemelések vagy rejtett jegyzetek) eltávolításra kerüljön a dokumentumból, növelve a magánszférát és a megfelelőséget.

### Funkció 3: dokumentum mentése opciókkal
**Áttekintés:** Tanulja meg, hogyan mentse a feldolgozott dokumentumot specifikus opciókkal, például rasterizálással és **add suffix filename java**‑val.

`SaveOptions` tartalmazza azokat a beállításokat, amelyek szabályozzák, hogyan kerül a redaktált dokumentum írásra, beleértve a formátumot, a rasterizálást és a névadási konvenciókat.

#### 3.1. lépés: saveoptions konfigurálása

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

- **Miért:** A mentési opciók testreszabása rugalmas kimeneti formátumokat és névadási konvenciókat tesz lehetővé. A `setAddSuffix(true)` engedélyezése **adds suffix to filename**, így egyértelművé válik, hogy a fájl redaktált.

## Hogyan adjon hozzá utótagot a fájlnévhez Java-ban dokumentum mentésekor?

A `Redactor` osztály a fő komponens, amely betölti a dokumentumot és alkalmazza a redakciós műveleteket. A `SaveOptions` meghatározza, hogyan kerül a redaktált dokumentum mentésre, beleértve a formátumot, a rasterizálást és a névadási konvenciókat. Hozzon létre egy `Redactor` példányt, alkalmazzon minden szükséges redakciót, majd konfiguráljon egy `SaveOptions` objektumot a `setAddSuffix(true)` beállítással. Hívja a `redactor.save(outputPath, options)`‑t. Az SDK automatikusan hozzáfűzi a “_redacted” (vagy a konfigurált) utótagot a fájlnévhez, így soha nem kell kézzel átnevezni a fájlt.

## GroupDocs Maven függőség áttekintése

A **groupdocs maven dependency** egyetlen `<dependency>` bejegyzéssel hozza be a teljes Redaction SDK‑t a projektbe. Kezeli a tranzitív függőségeket, naprakészen tartja a könyvtárakat, és egyszerűsíti a build automatizálást. A `pom.xml`‑ben deklarálva elkerülhető a manuális JAR‑kezelés, és biztosítható a legújabb biztonsági javításokkal való kompatibilitás.

## Miért fontos az utótag hozzáadása

Az utótag hozzáfűzése azonnali vizuális megerősítést nyújt arról, hogy egy fájl feldolgozásra került, ami kritikus az audit nyomvonalak, az automatizált munkafolyamatok és a szabályozási megfelelés szempontjából. Lehetővé teszi a szkriptek számára a redaktált fájlok szűrését, megakadályozza az eredeti tartalom véletlen terjesztését, és megfelel számos iparági szabványnak, amely egyértelmű címkézést követel meg a tisztított dokumentumoknál.

## Gyakorlati alkalmazások

1. **Jogi dokumentum redakció:** Biztonságos szerződések megosztása ügyfelekkel.  
2. **Egészségügyi rekordkezelés:** Betegazonosítók védelme a klinikai adatok megőrzése mellett.  
3. **Pénzügyi jelentés:** Érzékeny számok titokban tartása külső auditok során.  
4. **CRM integráció:** Automatikus ügyféladat-redakció exportálás előtt harmadik fél eszközeibe.  
5. **Együttműködési eszközök:** Biztosítja, hogy a megosztott vázlatok ne fedjék fel a rejtett megjegyzéseket vagy metaadatokat.

## Teljesítmény szempontok

### Teljesítmény optimalizálása
- Használjon streaming‑et (`load document from stream`) a teljes fájlok memóriába töltésének elkerülésére.  
- Zárja be a `Redactor` példányokat gyorsan az erőforrások felszabadításához.  

### Erőforrás használati irányelvek
- Figyelje a CPU‑t és a memóriát kötegelt futtatás során.  
- Kisebb fájlméretek esetén részesítse előnyben a `ByteArrayOutputStream`‑t a memória‑beli mentéshez.

### Legjobb gyakorlatok Java memória kezeléshez
- Használja újra a `Redactor` objektumokat több azonos típusú fájl feldolgozásakor.  
- Hívja a `close()`‑t egy `try‑with‑resources` blokkban a szivárgások megelőzése érdekében.

## Gyakori problémák és megoldások
| Probléma | Ok | Megoldás |
|----------|----|----------|
| **Az utótag nem jelenik meg** | `setAddSuffix(false)` vagy hiányzó hívás | Győződjön meg róla, hogy a `options.setAddSuffix(true)` be van állítva a `save()` előtt. |
| **OutOfMemoryError nagy DOCX esetén** | A teljes fájl betöltése a memóriába | Váltson `InputStream` betöltésre (lásd 1. funkció). |
| **Az annotációk még láthatóak** | A redakció nem lett alkalmazva a mentés előtt | Hívja a `redactor.apply(new DeleteAnnotationRedaction())`‑t a `save()` előtt. |
| **PDF rasterizálás nem alkalmazva** | `setRasterizeToPDF(false)` vagy kihagyva | Állítsa `options.setRasterizeToPDF(true)`‑ra, ha lapos PDF‑re van szükség. |

## Gyakran feltett kérdések

**K: Redaktálhatok PDF dokumentumokat a GroupDocs.Redaction használatával?**  
A: Igen, a könyvtár támogatja a PDF‑eket, DOCX, PPTX, XLSX és sok más formátumot.

**K: Mi a legjobb módja a nagy fájlok kezelésének a GroupDocs.Redaction‑nel?**  
A: Használjon streaming‑et (`load document from stream`) és zárja be a erőforrásokat gyorsan a memóriahasználat alacsonyan tartásához.

**K: Lehetőség van az utótag szövegének testreszabására?**  
A: Az API automatikusan hozzáad egy alapértelmezett utótagot (pl. “_redacted”). Egyedi utótagokhoz a kimeneti fájlt a mentés után kell átnevezni.

**K: Hogyan szerezhetek ideiglenes licencet a GroupDocs.Redaction‑hez?**  
A: Látogassa meg a [Temporary License page](https://purchase.groupdocs.com/temporary-license/) oldalt és kövesse az útmutatót.

**K: Hol kaphatok segítséget, ha problémáim vannak?**  
A: Csatlakozzon a [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) fórumhoz szakértői támogatásért.

## Erőforrások
- **Dokumentáció:** Részletes útmutatókat a [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/) oldalon.  
- **API referencia:** Átfogó API részletek a [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java) oldalon.  
- **Letöltés:** A legújabb verziót a [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/) oldalról szerezheti meg.  
- **GitHub tároló:** Hozzájárulhat vagy felfedezheti a forráskódot a [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) oldalon.

---

**Utolsó frissítés:** 2026-11-02  
**Tesztelve:** GroupDocs.Redaction 24.9 for Java  
**Szerző:** GroupDocs  

## Kapcsolódó oktatóanyagok

- [Word PDF-re konvertálása és redaktált dokumentumok mentése a GroupDocs.Redaction Java-val](/redaction/java/document-saving/)
- [Dokumentum oldalak előnézete Java betöltéssel a GroupDocs.Redaction használatával](/redaction/java/document-loading/)
- [Haladó redakciós technikák a GroupDocs.Redaction Java-hoz](/redaction/java/advanced-redaction/)