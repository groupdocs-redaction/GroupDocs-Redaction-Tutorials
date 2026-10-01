---
date: '2026-10-01'
description: Ismerje meg, hogyan távolíthatja el a szerző metaadatait, és mentheti
  a redaktált dokumentumfájlokat Java-ban a GroupDocs Redaction használatával.
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Ismerje meg, hogyan távolíthatja el a szerző metaadatait, és mentheti
  a redaktált dokumentumfájlokat Java-ban a GroupDocs Redaction használatával. Kövesse
  a lépésről-lépésre útmutatót.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: Hogyan távolítsuk el a szerző metaadatait Java-ban a GroupDocs segítségével
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: Hogyan távolítsuk el a szerző metaadatait Java-ban a GroupDocs segítségével
type: docs
url: /hu/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Hogyan távolítsuk el a szerző metaadatait Java-ban a GroupDocs-szal

A mai digitális környezetben a dokumentumokban rejtett érzékeny információk védelme elengedhetetlen gyakorlat. **A szerző metaadatainak eltávolítása** megakadályozza a személyes vagy vállalati azonosítók véletlen kiszivárgását. Ez az útmutató lépésről lépésre bemutatja, hogyan használhatja a `EraseMetadataRedaction`-t a GroupDocs.Redaction for Java-ból, hogy eltávolítsa az *Author* és *Manager* mezőket a Word fájlokból, majd **elmentse a redakciózott dokumentum** másolatokat biztonságosan a megosztáshoz vagy archiváláshoz.

## Gyors válaszok
- **Mi a EraseMetadataRedaction feladata?** Kiválasztott metaadatmezőket távolít el egy dokumentumból.  
- **Melyik könyvtár biztosítja ezt a funkciót?** GroupDocs.Redaction for Java.  
- **Szükségem van licencre?** Egy ingyenes próba a teszteléshez működik; a termeléshez állandó licenc szükséges.  
- **Célzhatok több mezőt egyszerre?** Igen, kombinálja a szűrőket logikai VAGY operátorral.  
- **A folyamat szálbiztos?** A Redactor példányok nincsenek megosztva szálak között; minden művelethez hozzon létre új példányt.

## Mi az a EraseMetadataRedaction?
`EraseMetadataRedaction` egy beépített redakciós osztály, amely lehetővé teszi, hogy meghatározza, mely metaadatbejegyzéseket kell törölni. Széles körű dokumentumformátumokon működik, amelyeket a GroupDocs.Redaction támogat, biztosítva, hogy a rejtett szerzői információk ne szivárogjanak ki. Célba vehet standard tulajdonságokat, mint az Author, Manager, valamint egyedi metaadatmezőket is, átfogó adatvédelmi védelmet nyújtva.

## Miért használjuk az EraseMetadataRedaction-t a GroupDocs-szal?
A GroupDocs.Redaction **több mint 100 bemeneti és kimeneti formátumot** támogat, és akár 500 oldalas dokumentumokat is képes feldolgozni anélkül, hogy a teljes fájlt a memóriába töltené. Ennek az osztálynak a használata egyetlen, nagy teljesítményű API-t biztosít a GDPR, HIPAA vagy belső megfelelőségi követelmények teljesítéséhez, miközben a kódbázist egyszerűen tartja.

## Előfeltételek
- Java 8 vagy újabb telepítve.  
- Maven (vagy a JAR-ok kézi hozzáadása).  
- GroupDocs.Redaction for Java (24.9 vagy újabb verzió).  
- Érvényes GroupDocs próba vagy állandó licenc.

## A GroupDocs.Redaction for Java beállítása

### Maven telepítés
Adja hozzá a GroupDocs tárolót és függőséget a **pom.xml** fájlhoz:

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
Alternatívaként töltse le a legújabb JAR-t a [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) oldalról.

### Licenc beszerzése
Szerezzen be egy ingyenes próbát vagy vásároljon ideiglenes licencet a GroupDocs portálon. A licencfájlt helyezze el olyan helyen, ahol az alkalmazás betöltheti (pl. a classpath gyökérben).

### Alapvető inicializálás és beállítás
Az alábbi egy minimális példa, amely egy `Redactor` példányt hoz létre egy DOCX fájlhoz:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Hogyan használjuk az EraseMetadataRedaction-t Java-ban
A következő szakaszok részletesen bemutatják a megvalósítást világos, cselekvőképes lépésekben.

### Funkció: adott metaadat elemek tisztítása

#### Áttekintés
A **Author** és **Manager** metaadatmezőket fogjuk eltávolítani a `EraseMetadataRedaction` segítségével. Ez gyakori igény, amikor belső jelentéseket osztunk meg külső partnerekkel.

#### Lépésről‑lépésre megvalósítás

##### 1️⃣ A Redactor objektum inicializálása
`Redactor` a központi osztály, amely betölti a dokumentumot, alkalmazza a redakciós objektumokat, és kiírja az eredményt. Hozzon létre új példányt minden feldolgozott fájlhoz:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ EraseMetadataRedaction alkalmazása
`MetadataFilters` előre definiált szűrőket biztosít a gyakori metaadatkulcsokhoz, mint az Author és a Manager.  
`EraseMetadataRedaction` eltávolítja azokat a metaadatbejegyzéseket, amelyek megfelelnek a megadott `MetadataFilters`-nek. A bitwise OR (`|`) kombinálja az `Author` és `Manager` szűrőket, így mindkét mező egy hívásban eltávolítható:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ Mentési beállítások konfigurálása
`SaveOptions` lehetővé teszi a kimeneti fájlnév, formátum és egyéb mentési paraméterek megadását.  
`SaveOptions` segítségével szabályozhatja a kimeneti fájl nevét, formátumát, és hogy a dokumentum PDF-re legyen-e rasterizálva. Utótag hozzáadásával az eredeti fájl érintetlen marad:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## Gyakori felhasználási esetek
1. **Jogi dokumentumok** – Szerzői információk redakciója a szerződések ellenfél ügyvédjének elküldése előtt.  
2. **Vállalati jelentések** – Menedzser nevek eltávolítása a negyedéves eredmények részvényeseknek való közzétételekor.  
3. **Projektfájlok** – Belső projekt dokumentáció tisztítása archiválás vagy nyilvános tárolóba feltöltés előtt.

## Hibaelhárítási tippek
- **Fájl nem található** – Ellenőrizze, hogy az `inputFilePath` útvonal egy létező fájlra mutat-e, és hogy az alkalmazásnak olvasási jogosultsága van-e.  
- **Hiányzó metaadatmezők** – Nem minden dokumentumtípus tárolja ugyanazokat a metaadatkulcsokat; először ellenőrizze a dokumentum tulajdonságait az Office-ben.  
- **Licenc hibák** – Győződjön meg róla, hogy a licencfájl helyesen be van töltve a `Redactor` példány létrehozása előtt.

## Teljesítménybeli szempontok
- `Redactor` objektumot azonnal zárja le (ahogy a `finally` blokkban látható), hogy felszabadítsa a natív erőforrásokat.  
- Kerülje a nagy dokumentumok rasterizálását, hacsak nem szükséges PDF előnézet; a rasterizálás akár 3‑szorosára is növelheti a CPU és memória használatát 300 oldalas fájlok esetén.

## Gyakran ismételt kérdések

**Q1: Mi a metaadat redakció?**  
A1: A metaadat redakció a rejtett dokumentumtulajdonságok (például szerző, menedzser vagy egyedi címkék) eltávolítását jelenti, hogy megakadályozza a érzékeny információk véletlen kiszivárgását.

**Q2: Használhatom a GroupDocs.Redaction-t más fájltípusokhoz?**  
A2: Igen, a könyvtár támogatja a PDF, DOCX, PPTX, XLSX és még sok más formátumot – összesen több mint 100-at.

**Q3: Hogyan kezeljem a redakció közbeni hibákat?**  
A3: Tegye a `apply` hívást try‑catch blokkba, és mindig zárja le a `Redactor`-t egy finally ágba, hogy biztosan felszabaduljanak az erőforrások.

**Q4: Lehet-e egyedi metaadatmezőket redakciózni?**  
A5: Teljesen lehetséges. Használja a `MetadataFilters.Custom("YourFieldName")`-t bármely egyedi tulajdonság célzásához a dokumentumban.

**Q5: Mik a legjobb gyakorlatok a GroupDocs.Redaction használatához?**  
A5:  
- Töltse be a licencet a program elején.  
- Zárja le a `Redactor` objektumokat gyorsan.  
- Használja a `SaveOptions`-t utótag hozzáadásához, így az eredeti fájlok érintetlenek maradnak.  
- Tesztelje a redakciót a dokumentum másolatán, mielőtt kötegelt feldolgozást végez.

**Q6: Támogatja az EraseMetadataRedaction kötegelt műveleteket?**  
A6: Ciklusba tehet egy fájlútvonal-gyűjteményt, minden fájlhoz új `Redactor` példányt létrehozva, és ugyanazt a redakciós logikát alkalmazva.

**Q7: Kombinálhatom az EraseMetadataRedaction-t más redakciótípusokkal?**  
A7: Igen, több redakciós objektumot is láncolhat (például szövegredakciót követően metaadatredakciót) a mentés előtt.

## Források

- **Documentation**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free support**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary license**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

**Legutóbb frissítve:** 2026-10-01  
**Tesztelve:** GroupDocs.Redaction 24.9 for Java  
**Szerző:** GroupDocs

## Kapcsolódó oktatóanyagok

- [Groupdocs Redaction Java Dokumentum Metaadat Kinyerés](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)  
- [Hogyan távolítsuk el a metaadatokat Java-ban a GroupDocs.Redaction használatával](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)  
- [Dokumentum információ lekérése a Groupdocs Redaction Java használatával](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)