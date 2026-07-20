---
date: '2026-07-20'
description: Ismerje meg, hogyan listázhatja a formátumokat a GroupDocs.Redaction
  .NET használatával, integrálja a funkciót a dokumentumfolyamatába, és javítsa a
  teljesítményt.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Fedezze fel, hogyan listázhatja a formátumokat a GroupDocs.Redaction
  .NET használatával, tekintse meg a lépésről‑lépésre útmutatót, és kapjon tippeket
  a .NET alkalmazások optimális teljesítményéhez.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Hogyan listázzuk a formátumokat a GroupDocs.Redaction .NET segítségével
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: Hogyan listázzuk a formátumokat a GroupDocs.Redaction .NET segítségével
type: docs
url: /hu/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Hogyan listázhatók a formátumok a GroupDocs.Redaction .NET-ben

A különféle dokumentumtípusok kezelése a fejlesztők számára mindennapi valóság, akik dokumentum‑központú alkalmazásokat építenek. Ebben az útmutatóban megtanulja, hogyan **listázhatók a formátumok**, amelyeket a GroupDocs.Redaction .NET képes kezelni, így a fájlokat a feldolgozás előtt ellenőrizheti, a felhasználóknak pontos lehetőségeket mutathat, és hatékonyan tarthatja a munkafolyamatot.

## Bevezetés

A hatékony dokumentumkezelés azzal kezdődik, hogy pontosan tudja, mely fájltípusokat támogatja a könyvtára. A GroupDocs.Redaction beépített módszert biztosít ennek az információnak a lekérésére, lehetővé téve dinamikus UI elemek létrehozását, az érvényesítési szabályok érvényesítését és a futásidejű hibák elkerülését. Az alábbiakban megtalálja mindazt, amire szüksége van a beindításhoz, a telepítéstől a gyakorlati kódrészletekig és a teljesítmény tippekig.

### Gyors válaszok
- **Mi jelent a „hogyan listázhatók a formátumok”?** Azt jelenti, hogy lekéri a fájlkiterjesztések gyűjteményét, amelyeket a GroupDocs.Redaction képes feldolgozni.  
- **Szükségem van licencre?** Igen, egy érvényes GroupDocs.Redaction licenc szükséges a termelésben való használathoz.  
- **Mely .NET verziók támogatottak?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Hány formátum érhető el?** Több mint 30 bemeneti és kimeneti formátum támogatott alapból.  
- **Szükséges-e valamilyen speciális konfiguráció?** Nem szükséges extra konfiguráció a szabványos könyvtár inicializáláson kívül.

## Mi a „hogyan listázhatók a formátumok”?

Ez magában foglalja a könyvtár FileType API-jának meghívását, hogy egy gyűjteményt kapjon, ahol minden bejegyzés tartalmazza a fájlkiterjesztést és egy ember által olvasható nevet. A fejlesztők ezután végigjárhatják ezt a gyűjteményt érvényesítési szabályok létrehozásához, UI legördülő menük feltöltéséhez vagy a támogatott típusok naplózásához, biztosítva, hogy csak kompatibilis dokumentumok legyenek feldolgozva.

## Miért listázzuk a formátumokat a GroupDocs.Redaction-nel?

A GroupDocs.Redaction **30+** különböző fájltípust támogat – beleértve a PDF, DOCX, PPTX és képfájl formátumokat – lehetővé téve, hogy a legtöbb vállalati dokumentumot külső konverterek nélkül kezelje. A formátumok programozott listázásával kiküszöböli a találgatást, csökkenti a támogatási jegyek számát, és biztosítja, hogy csak kompatibilis fájlok kerüljenek a feldolgozási csővezetékbe.

## Előfeltételek

- **GroupDocs.Redaction for .NET** – letöltse a legújabb csomagot a hivatalos oldalról.  
- **.NET Framework or .NET Core** – kompatibilis a fejlesztői környezetével.  
- **Visual Studio** (vagy bármely C#‑kompatibilis IDE).  
- Alapvető ismeretek a C# szintaxisról.

## A GroupDocs.Redaction beállítása .NET-hez

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Csomagkezelő
`Install-Package GroupDocs.Redaction`

### NuGet Csomagkezelő UI
- Keresse meg a **„GroupDocs.Redaction”**-t, és telepítse a legújabb verziót.

### Licenc beszerzése
A GroupDocs ingyenes próbaverziót, értékeléshez ideiglenes licencet vagy teljes vásárlási lehetőséget kínál. Látogassa meg a GroupDocs weboldalát a megfelelő licencfájl beszerzéséhez.

### Alapvető inicializálás és beállítás
A csomag hozzáadása után hivatkozzon a névtérre, és hozza létre a `Redactor` példányt:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Implementációs útmutató

### Hogyan listázhatok formátumokat a GroupDocs.Redaction .NET-ben?
Töltse be a könyvtárat, hívja meg a statikus segédprogramot, és rendezze az eredményeket – ez csak két kódsorral ad egy használatra kész gyűjteményt. Használja a `FileType.GetSupportedFileFormats()` metódust egy `IEnumerable<FileType>` lekéréséhez, amely tartalmazza minden formátum kiterjesztését és megjelenített nevét, majd rendezze kiterjesztés szerint a tiszta UI lista érdekében.

### Támogatott fájlformátumok lekérése

#### Áttekintés
A cél egy olyan lista megszerzése, amely tartalmazza a GroupDocs.Redaction által kezelhető fájltípusokat, megkönnyítve a beépítést az érvényesítési logikába, UI legördülő menükbe vagy naplózási mechanizmusokba.

#### Lépésről‑lépésre megvalósítás

**1. Támogatott fájltípusok lekérése**  
`FileType.GetSupportedFileFormats()` minden formátumot visszaad, amelyet a könyvtár felismer. A metódus a `GroupDocs.Redaction.FileType` osztály része, amely metaadatokat, például fájlkiterjesztést és barátságos nevet tartalmaz.

**2. Támogatott fájltípusok megjelenítése**  
Iteráljon a gyűjteményen, és írja ki minden formátum kiterjesztését és leírását. Inline kódrészlet:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

A kódrészlet egy rendezett listát nyomtat, például „.pdf – Portable Document Format”, ami tökéletes a UI elemek feltöltéséhez.

### Hibaelhárítási tippek
- **Hiányzó csomag** – Ellenőrizze a NuGet csomag hivatkozását, és szükség esetén állítsa vissza a csomagokat.  
- **Helytelen licenc útvonal** – Győződjön meg róla, hogy a licencfájl a kimeneti könyvtárba másolva van, vagy adjon meg egy abszolút útvonalat.  
- **Nem támogatott kiterjesztés** – Ha egy formátum nincs listázva, ellenőrizze, hogy a legújabb könyvtár verziót használja; az újabb kiadások további formátumokat adnak hozzá.

## Gyakorlati alkalmazások

A támogatott fájlformátumok megértése számos valós helyzetet nyit meg:

1. **Dokumentumkezelő rendszerek** – Ellenőrizze a feltöltéseket a támogatott lista alapján, hogy elkerülje a feldolgozási hibákat.  
2. **Tartalombiztonság** – Alkalmazzon redakciós szabályokat csak azokhoz a fájltípusokhoz, amelyeket a motor biztonságosan módosíthat.  
3. **Kötegelt feldolgozási csővezetékek** – Szűrje a nagy fájlkészleteket a redakció meghívása előtt, ezzel CPU‑t és memóriát takarítva meg.

## Teljesítmény szempontok
- **Memory Footprint** – A formátumok listázása könnyű művelet; nem tölt be semmilyen dokumentumot a memóriába.  
- **Batch Operations** – Kötegelt műveletek esetén, amikor több száz fájlt dolgoz fel, egyszer kérje le a formátumlistát, és használja újra a felesleges hívások elkerülése érdekében.  
- **Thread Safety** – `FileType.GetSupportedFileFormats()` szálbiztos, és szinkronizáció nélkül hívható párhuzamos feladatokból.

## Következtetés
Most már rendelkezik egy teljes, termelésre kész megközelítéssel a **hogyan listázhatók a formátumok** használatához a GroupDocs.Redaction .NET-ben. Ennek a funkciónak a beépítésével javíthatja az érvényesítést, növelheti a felhasználói élményt, és erősítheti a dokumentumcsővezetékek megbízhatóságát.

### Következő lépések
- Fedezze fel a `Redactor` API-t, hogy fájltípus alapján alkalmazzon redakciós szabályokat.  
- Kombinálja a formátumlistát egy front‑end legördülő menüvel a zökkenőmentes fájlkiválasztáshoz.  
- Tekintse át a teljesítmény útmutatót a nagyméretű kötegelt feladatok optimalizálásához.

## Gyakran Ismételt Kérdések

**K: Lekérhetem a formátumlistát anélkül, hogy inicializálnám a Redactor példányt?**  
V: Igen, a `FileType.GetSupportedFileFormats()` statikus, és nem igényel `Redactor` objektumot.

**K: A lista tartalmazza mind a bemeneti, mind a kimeneti formátumokat?**  
V: A metódus visszaadja az összes formátumot, amelyet a könyvtár olvasni és írni is tud; minden `FileType` tartalmaz egy `CanRead` és egy `CanWrite` jelzőt.

**K: Milyen gyakran frissül a támogatott formátumlista?**  
V: A GroupDocs minden könyvtárverzióval kiad formátumfrissítéseket; a lista futásidőben történő ellenőrzése biztosítja, hogy mindig a legújabb készlet legyen.

**K: Van mód csak a PDF‑kompatibilis formátumok szűrésére?**  
V: Igen, szűrje a gyűjteményt ahol `format.Extension == ".pdf"` vagy ahol `format.Name.Contains("PDF")`.

**K: Ez a megközelítés működik a .NET Core 2.1‑en?**  
V: A metódus .NET Core 3.1 vagy újabb verziót igényel; a korábbi futtatókörnyezetek nem támogatottak.

## GyIK szekció
1. **Hogyan telepíthetem a GroupDocs.Redaction-t .NET-re?**  
   Használja a CLI parancsot `dotnet add package GroupDocs.Redaction` vagy telepítse a NuGet Package Manager UI-n keresztül.  

2. **Mik a gyakori problémák a támogatott formátumok lekérésekor?**  
   Győződjön meg róla, hogy minden függőség helyreállított, és a megfelelő névteret (`GroupDocs.Redaction`) hivatkozza.  

3. **Használhatom ezt a funkciót nem‑.NET alkalmazásokkal?**  
   Ez az útmutató .NET-re fókuszál, de a GroupDocs hasonló API-kat kínál Java, Python és más platformok számára.  

4. **Hogyan optimalizálhatom a teljesítményt a GroupDocs.Redaction használata során?**  
   Használja újra a formátumlistát, kerülje a teljes dokumentumok betöltését, ha csak a kompatibilitást ellenőrzi, és figyelje a memóriahasználatot a kötegelt feladatok során.  

5. **Milyen fájltípusokat támogat a GroupDocs.Redaction?**  
   A könyvtár 30+ formátumot támogat, beleértve a PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG és sok más formátumot. Használja a `FileType.GetSupportedFileFormats()`-t a teljes lista megtekintéséhez.

## Források
- [Dokumentáció](https://docs.groupdocs.com/redaction/net/)
- [API Referencia](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction letöltése](https://releases.groupdocs.com/redaction/net/)
- [Ingyenes támogatási fórum](https://forum.groupdocs.com/c/redaction/33)
- [Ideiglenes licenc](https://purchase.groupdocs.com/temporary-license/)

---

**Utolsó frissítés:** 2026-07-20  
**Tesztelve ezzel:** GroupDocs.Redaction 4.2.0 for .NET  
**Szerző:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## Kapcsolódó oktatóanyagok

- [Formátumkezelési oktatóanyagok a GroupDocs.Redaction .NET-hez](/redaction/net/format-handling/)
- [Dokumentum betöltési oktatóanyagok a GroupDocs.Redaction .NET-hez](/redaction/net/document-loading/)
- [Dokumentum mentési oktatóanyagok a GroupDocs.Redaction .NET-hez](/redaction/net/document-saving/)