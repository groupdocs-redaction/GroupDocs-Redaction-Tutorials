---
date: '2025-12-17'
description: Tanulja meg, hogyan adhat hozzá utótagot a fájlnévhez, és hogyan redakálhatja
  a dokumentumok érzékeny információit a GroupDocs.Redaction for Java használatával.
  Hatékonyan növelje a dokumentumok biztonságát és adatvédelmét.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Hogyan adjunk hozzá utótagot a fájlnévhez a dokumentumok Java‑ban történő redakciója
  során a GroupDocs.Redaction használatával
type: docs
url: /hu/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Hogyan adjon hozzá utótagot a fájlnévhez a dokumentumok Java‑ban történő redakciója során a GroupDocs.Redaction használatával

Az érzékeny adatok redakciója csak a harc felét jelenti – biztosítania kell, hogy a mentett fájl egyértelműen jelezze, hogy feldolgozásra került. Ebben az útmutatóban megtanulja, hogyan **adjon hozzá utótagot a fájlnévhez** egy redakciózott dokumentum mentésekor, valamint a betöltést, annotálást és mentést a GroupDocs.Redaction for Java használatával. Akár jogi szerződéseket, orvosi feljegyzéseket vagy pénzügyi jelentéseket véd, ezek a lépések biztonságossá és auditálhatóvá teszik a munkafolyamatot.

## Gyors válaszok
- **Mi a “add suffix to filename” funkció?**  
  A kimeneti fájlnévhez egy egyedi utótagot (pl. „_redacted”) fűz, így azonnal azonosíthatók a feldolgozott fájlok.
- **Betölthetek dokumentumot stream‑ből?**  
  Igen – a GroupDocs.Redaction támogatja a betöltést bármely `InputStream`‑ből, ami tökéletes a felhőalapú tároláshoz vagy memória‑beli feldolgozáshoz.
- **Szükségem van licencre ehhez a funkcióhoz?**  
  Az ingyenes próba verzió alapvető redakcióra működik; egy ideiglenes vagy teljes licenc feloldja az összes fejlett opciót, beleértve az utótag kezelését.
- **Mely formátumok támogatottak?**  
  A könyvtár kezeli a DOCX, PDF, PPTX, XLSX és még sok más formátumot.
- **Szükséges a rasterizálás PDF kimenethez?**  
  A rasterizálás opcionális; engedélyezze, ha a dokumentumot extra biztonság érdekében laposra kell tenni.

## Mi az, hogy utótag hozzáadása a fájlnévhez?
Az utótag hozzáadása egy egyszerű elnevezési konvenció, amely jelzi, hogy a fájlon redakció történt. Megakadályozza az eredeti, nem redakciózott verziók véletlen megoszt, és segíti az automatizált folyamatokat a feldolgozási állapot nyomon követésében.

## Miért használja a GroupDocs.Redaction‑t ehhez a feladathoz?
A GroupDocs.Redaction egy folyékony Java API‑t biztosít, amely lehetővé teszi a redakciós műveletek és a fájlkezelési beállítások – például a **utótag hozzáadása a fájlnévhez** – kombinálását néhány kódsorral. Ez fejlesztési időt takarít meg, és csökkenti a manuális hibák kockázatát.

## Előfeltételek
- **Java Development Kit (JDK):** 8‑as vagy újabb verzió.
- **GroupDocs.Redaction Library:** A redakciós feladatokhoz szükséges alapkönyvtár.
- **IDE:** IntelliJ IDEA, Eclipse vagy bármely Java‑kompatibilis szerkesztő.
- **Maven:** A függőségkezeléshez.

### Tudás előfeltételek
A Java I/O és az alapvető objektum‑orientált koncepciók ismerete megkönnyíti a példák követését.

## A GroupDocs.Redaction beállítása Java‑hoz
### Maven beállítás
Adja hozzá a következő konfigurációt a `pom.xml` fájlhoz a GroupDocs könyvtárak Maven‑on keresztüli eléréséhez:

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

### Licenc megszerzése
1. **Free Trial:** Alapfunkciók korlátozás nélkül elérhetők.  
2. **Temporary License:** Ideiglenes licenc beszerzése a fejlett funkciók kipróbálásához.  
3. **Purchase:** Hosszú távú használathoz fontolja meg a teljes licenc vásárlását.

#### Alapvető inicializálás és beállítás
Inicializálja a projektet a szükséges importok hozzáadásával:

```java
import com.groupdocs.redaction.Redactor;
```

Ezzel a beállítással készen áll a dokumentum redakciós funkciók megvalósítására.

## Implementációs útmutató

### 1. funkció: Dokumentum betöltése stream‑ből
**Áttekintés:** Ismerje meg, hogyan töltsön be dokumentumokat `InputStream`‑be feldolgozáshoz.

#### Lépésről‑lépésre megvalósítás
##### 1.1. lépés: InputStream létrehozása

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

- **Miért:** Az `InputStream` használata lehetővé teszi a különböző formátumokban tárolt dokumentumok zökkenőmentes kezelését, ami elengedhetetlen, ha **dokumentumot kell betölteni stream‑ből** felhő vagy mikro‑szolgáltatás környezetben.

### 2. funkció: Annotáció törlés redakció alkalmazása
**Áttekintés:** Távolítsa el a dokumentum annotációit a `DeleteAnnotationRedaction` használatával.

#### Lépésről‑lépésre megvalósítás
##### 2.1. lépés: DeleteAnnotationRedaction alkalmazása

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Miért:** Ez a lépés biztosítja, hogy minden érzékeny annotáció eltávolításra kerüljön, növelve a dokumentum adatvédelmét.

### 3. funkció: Dokumentum mentése opciókkal
**Áttekintés:** Ismerje meg, hogyan mentse a feldolgozott dokumentumot speciális opciókkal, például rasterizálással és **utótag hozzáadásával a fájlnévhez**.

#### Lépésről‑lépésre megvalósítás
##### 3.1. lépés: SaveOptions konfigurálása

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

- **Miért:** A mentési opciók testreszabása rugalmas kimeneti formátumokat és elnevezési konvenciókat tesz lehetővé. A `setAddSuffix(true)` engedélyezése **utótagot ad a fájlnévhez**, így egyértelmű, hogy a fájl redakcióra került.

## Miért fontos az utótag hozzáadása
- **Auditálhatóság:** A csapatok azonnal felismerhetik, mely fájlok biztonságosak a terjesztéshez.  
- **Automatizálás:** A szkriptek szűrhetik a fájlokat utótag alapján, megakadályozva az eredeti dokumentumok véletlen feldolgozását.  
- **Megfelelőség:** Számos szabályozás megköveteli a tisztított dokumentumok egyértelmű címkézését.

## Gyakorlati alkalmazások
Tekintse meg ezeket a valós példákat:
1. **Jogi dokumentum redakció:** Biztonságos szerződések a kliensnek való megosztás előtt.  
2. **Orvosi feljegyzések kezelése:** A betegazonosítók védelme.  
3. **Pénzügyi jelentés:** Az érzékeny számok bizalmas kezelése.  
4. **CRM integráció:** Ügyféladatok automatikus redakciója export előtt.  
5. **Együttműködési eszközök:** Biztosítsa, hogy a megosztott vázlatok ne mutassanak rejtett megjegyzéseket.

## Teljesítmény szempontok
### Teljesítmény optimalizálása
- Használjon streaminget (`load document from stream`) a teljes fájlok memóriába betöltésének elkerülése érdekében.  
- Zárja le a `Redactor` példányokat gyorsan az erőforrások felszabadításához.

### Erőforrás használati irányelvek
- Figyelje a CPU és memória használatot kötegelt futtatás során.  
- Kisebb fájlméretek esetén részesítse előnyben a `ByteArrayOutputStream` használatát memória‑beli mentéshez.

### Legjobb gyakorlatok a Java memória kezeléshez
- Használja újra a `Redactor` objektumokat több azonos típusú fájl feldolgozásakor.  
- Hívja meg a `close()`‑t egy `finally` blokkban vagy try‑with‑resources szerkezetben a szivárgások elkerülése érdekében.

## Gyakori problémák és megoldások
| Issue | Cause | Fix |
|-------|-------|-----|
| **Az utótag nem jelenik meg** | `setAddSuffix(false)` vagy hiányzó hívás | Győződjön meg róla, hogy a `save()` előtt a `options.setAddSuffix(true)` be van állítva. |
| **OutOfMemoryError nagy DOCX esetén** | A teljes fájl memóriába betöltése | Váltson `InputStream` betöltésre (lásd 1. funkció). |
| **Az annotációk még láthatóak** | A redakció nem lett alkalmazva a mentés előtt | Hívja meg a `redactor.apply(new DeleteAnnotationRedaction())`‑t a `save()` előtt. |
| **PDF rasterizálás nem alkalmazott** | `setRasterizeToPDF(false)` vagy kihagyva | Állítsa `options.setRasterizeToPDF(true)`‑ra, ha lapos PDF‑re van szükség. |

## Gyakran ismételt kérdések

**Q: Redakciózhatok PDF dokumentumokat a GroupDocs.Redaction segítségével?**  
A: Igen, a könyvtár támogatja a PDF, DOCX, PPTX, XLSX és számos egyéb formátumot.

**Q: Mi a legjobb módja a nagy fájlok kezelésének a GroupDocs.Redaction‑nél?**  
A: Használjon streaminget (`load document from stream`) és zárja le gyorsan az erőforrásokat a memóriahasználat alacsonyan tartásához.

**Q: Lehet egyedi utótag szöveget megadni?**  
A: Az API automatikusan hozzáad egy alapértelmezett utótagot (pl. „_redacted”). Egyedi utótagok esetén a mentés után átnevezheti a kimeneti fájlt.

**Q: Hogyan szerezhetek ideiglenes licencet a GroupDocs.Redaction‑hez?**  
A: Látogassa meg a [Temporary License page](https://purchase.groupdocs.com/temporary-license/) oldalt, és kövesse az utasításokat.

**Q: Hol kaphatok segítséget, ha problémáim vannak?**  
A: Csatlakozzon a [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) fórumhoz szakértői támogatásért.

## Források
- **Documentation:** Részletes útmutatókat találsz a [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/) oldalon.  
- **API Reference:** Átfogó API részletek a [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java) oldalon.  
- **Download:** A legújabb verzió letölthető a [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/) oldalról.  
- **GitHub Repository:** Hozzájárulhatsz vagy felfedezheted a forráskódot a [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) oldalon.

---

**Utolsó frissítés:** 2025-12-17  
**Tesztelt verzió:** GroupDocs.Redaction 24.9 for Java  
**Szerző:** GroupDocs