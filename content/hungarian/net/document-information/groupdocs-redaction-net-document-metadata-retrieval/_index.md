---
date: '2026-06-06'
description: Ismerje meg, hogyan lehet lekérni a metadata-t és kinyerni a dokumentum
  metadata-t a GroupDocs.Redaction .NET használatával, amely lehetővé teszi a robusztus
  dokumentumkezelést és a megfelelőséget.
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: Hogyan lehet lekérni a metadata-t a GroupDocs.Redaction .NET API-val
type: docs
url: /hu/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# Hogyan lehet metaadatokat lekérni a GroupDocs.Redaction .NET segítségével

A mai digitális korban a fájlból **metaadatok lekérdezése** alapvető lépés minden dokumentum‑központú alkalmazás számára. Akár a fájl metaadatait kell olvasnia megfelelőségi auditokhoz, akár a dokumentum tulajdonságait kell kinyernie indexeléshez, vagy egyszerűen csak a dokumentum méretét szeretné megjeleníteni egy felhasználói felületen, a GroupDocs.Redaction .NET egy tömör API-t biztosít, amellyel mindezt néhány C# sorban megteheti. Ez az útmutató végigvezeti Önt a teljes folyamaton, a környezet beállításától a lekért információk megjelenítéséig, így azonnal elkezdheti a dokumentum metaadatok kinyerését.

## Gyors válaszok
- **Mi a fő módszer a metaadatok lekérésére?** Hívja a `Redactor.GetDocumentInfo()`-t egy `Redactor` példányon.  
- **Mely formátumok támogatottak?** Több mint 50 bemeneti és kimeneti formátum, beleértve a PDF, DOCX, XLSX, PPTX és képtípusokat.  
- **Szükségem van licencre fejlesztéshez?** Egy ingyenes próbalicenc elegendő a teszteléshez; a teljes licenc a termeléshez kötelező.  
- **Feldolgozhatok nagy fájlokat?** Igen — a GroupDocs.Redaction több száz oldalas dokumentumokat kezel anélkül, hogy a teljes fájlt a memóriába töltené.  
- **Elérhető az aszinkron támogatás?** Az API aszinkron mintákba csomagolható, hogy a UI szálak reagálók maradjanak.

## Mi a metaadatlekérdezés a GroupDocs.Redaction-ben?
A metaadatlekérdezés a dokumentum beépített tulajdonságainak—például fájltípus, oldalszám és méret—könyvtári API-n keresztüli elérésének folyamata. Ezeknek a tulajdonságoknak a kinyerésével a fejlesztők programozott módon felmérhetik a dokumentum jellemzőit, támogatják az indexelést, érvényesítik a megfelelőségi szabályokat, és megalapozott döntéseket hozhatnak a további feldolgozási lépésekről.

## Hogyan lehet dokumentum metaadatokat lekérni?
A `Redactor` osztály a fő interfész a dokumentumok betöltéséhez és vizsgálatához a GroupDocs.Redaction-ben.  
`GetDocumentInfo()` egy olyan metódus, amely egy `DocumentInfo` objektumot ad vissza, amely a dokumentum metaadatait tartalmazza.  

Töltse be a fájlt a `new Redactor("path/to/file")` használatával, majd hívja meg a `GetDocumentInfo()`‑t — a hívás egy `DocumentInfo` objektumot ad vissza, amely tartalmazza a típust, az oldalszámot, a méretet és egyéb tulajdonságokat. Ez a kéts lépéses megközelítés minden támogatott formátumra működik, és nem igényel további konfigurációt. Ezután olvashatja a `FileType`, `PageCount` és `FileSize` mezőket a információk megjelenítéséhez vagy naplózásához.

## Előfeltételek

- **GroupDocs.Redaction .NET** verzió 21.6 vagy újabb.  
- .NET Framework 4.7.2 +, .NET Core 3.1 +, vagy .NET 5/6+.  
- Alap C# ismeretek és egy fejlesztői IDE (Visual Studio, Rider, stb.).

## A GroupDocs.Redaction beállítása .NET-hez

A GroupDocs.Redaction használatának megkezdése egyszerű. Telepítse a csomagot az alábbi módszerek egyikével:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

Vagy használja a **NuGet Package Manager UI**-t: egyszerűen keresse meg a „GroupDocs.Redaction” kifejezést, és kattintson a **Install** gombra.

### Licenc beszerzése

A GroupDocs.Redaction kipróbálásához ingyenes próbalicencet szerezhet. Folyamatos fejlesztéshez vagy termelési használathoz vásároljon teljes licencet, vagy kérjen ideiglenes licencet a hivatalos weboldalon.

A telepítés után inicializálja a könyvtárat a következő módon:

```csharp
using GroupDocs.Redaction;
```

## Implementációs útmutató

### Dokumentuminformáció lekérdezése funkció

Ez a funkció a dokumentumok létfontosságú metaadatainak kinyerésére összpontosít a GroupDocs.Redaction .NET használatával. Kövesse ezeket a lépéseket:

#### 1. lépés: Készítse elő a dokumentum útvonalát

Adja meg a célfájl abszolút vagy relatív útvonalát:

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

`YOUR_DOCUMENT_DIRECTORY`-t cserélje le arra a mappára, amely a dokumentumot tartalmazza.

#### 2. lépés: Redactor példány inicializálása

Hozzon létre egy `Redactor` objektumot, amely hozzáférést biztosít a metaadat metódusokhoz:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### 3. lépés: Dokumentuminformáció lekérése

Hívja meg a `GetDocumentInfo()`-t a `Redactor` példányon, hogy lekérje az összes elérhető tulajdonságot:

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

A visszaadott objektum tartalmazza a fájltípust, az oldalak számát és a fájlméretet.

#### 4. lépés: Dokumentum részleteinek megjelenítése

Írja ki az információkat a konzolra vagy a felhasználói felületre. A mintakód (kommentált a önálló futtatáshoz) bemutatja, hogyan lehet kiírni minden egyes tulajdonságot:

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### Miért használja a GroupDocs.Redaction-t metaadat kinyeréshez?
A GroupDocs.Redaction **50+ fájlformátumot** támogat, és akár **2 GB** méretű dokumentumokat is képes feldolgozni, miközben a memóriahasználat a tipikus terhelés esetén **100 MB** alatt marad. A könyvtár a dokumentum teljes betöltése nélkül nyeri ki a metaadatokat, gyors válaszokat biztosítva — gyakran **200 ms** alatt egy 100 oldalas PDF esetén standard szerverhardveren.

### Gyakori problémák és megoldások

- **Helytelen fájlútvonal** — Ellenőrizze az útvonal karakterláncot, és győződjön meg róla, hogy a fájl elérhető a futó folyamat számára.  
- **Nem támogatott formátum** — Ellenőrizze a formátumlistát; ha egy formátum hiányzik, fontolja meg először a konvertálást.  
- **Teljesítménybeli szűk keresztmetszet** — Nagyon nagy fájlok esetén engedélyezze a streaming opciókat, vagy dolgozza fel az oldalakat kötegekben a memóriahasználat korlátozása érdekében.

## Gyakorlati alkalmazások

A dokumentum metaadatainak megértése több valós helyzetet tesz lehetővé:

1. **Dokumentumkezelő rendszerek (DMS)** — Automatizálja a kategorizálást és az indexelést típus, méret vagy oldalszám alapján.  
2. **Megfelelőségi audit** — Ellenőrizze, hogy a bizalmas fájlok tartalmazzák-e a szükséges metaadatokat archiválás előtt.  
3. **Adatmigráció** — Csoportosítsa a fájlokat tulajdonságok szerint a tömeges migrációs feladatok egyszerűsítése érdekében.

## Teljesítményfontosságú szempontok

- **Hatékony erőforrás-használat** — Használja a `Redactor` példányt egy `using` blokkban a megfelelő felszabadítás biztosítása érdekében.  
- **Aszinkron minták** — Csomagolja a metaadat hívásokat `Task.Run`-ba, vagy valósítson meg aszinkron burkolókat, hogy a UI szálak reagálók maradjanak asztali vagy webalkalmazásokban.

## Gyakran feltett kérdések

**K: Mely dokumentumformátumokból tudok metaadatot kinyerni?**  
A: A GroupDocs.Redaction több mint 50 formátumból olvas metaadatokat, beleértve a PDF, DOCX, XLSX, PPTX, HTML és a gyakori képtípusokat.

**K: Hogyan kezeljem a jelszóval védett fájlokat?**  
A: Adja meg a jelszót a `Redactor` konstruktorának; az API a metaadatok kinyerése előtt visszafejti a fájlt.

**K: Van korláta a feldolgozható fájlok méretének?**  
A: Bár nincs szigorú korlát, a 2 GB-nál nagyobb fájlokhoz további memóriahangolásra lehet szükség; a teljesítmény lineárisan nő a fájlmérettel.

**K: Lekérhetem a metaadatokat kötegelt műveletben?**  
A: Igen — iteráljon a fájlútvonalak gyűjteményén, és hívja meg minden egyesre a `GetDocumentInfo()`‑t; a könyvtár szálbiztos a párhuzamos végrehajtáshoz.

**K: Szükségem van licencre a fejlesztői buildekhez?**  
A: Egy ingyenes próbalicenc elegendő fejlesztéshez és teszteléshez; a kereskedelmi licenc a termelési telepítésekhez kötelező.

## Erőforrások

- [Dokumentáció](https://docs.groupdocs.com/redaction/net/)  
- [API referencia](https://reference.groupdocs.com/redaction/net)  
- [Letöltés](https://releases.groupdocs.com/redaction/net/)  
- [Ingyenes támogatási fórum](https://forum.groupdocs.com/c/redaction/33)  
- [Ideiglenes licenc információk](https://purchase.groupdocs.com/temporary-license/)

## Következtetés

Most már rendelkezik egy teljes, lépésről‑lépésre útmutatóval a **metaadatok lekérdezésére** a GroupDocs.Redaction .NET használatával. A `Redactor.GetDocumentInfo()` metódus kihasználásával gyorsan beolvashatja a fájl metaadatait, támogatja a megfelelőségi munkafolyamatokat, és bővítheti bármely dokumentumfeldolgozó csővezetékét. Fedezze fel a Redaction további funkcióit — például a tartalom redakciót, vízjelezést és dokumentumkonverziót — hogy teljes körű dokumentumkezelő megoldást építsen.

---

**Utoljára frissítve:** 2026-06-06  
**Tesztelve ezzel:** GroupDocs.Redaction .NET 21.6 (a legújabb a írás időpontjában)  
**Szerző:** GroupDocs  

## Kapcsolódó oktatóanyagok

- [Hogyan nyerjünk ki dokumentum metaadatokat adatfolyamokból a GroupDocs.Redaction .NET használatával](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [Hogyan redakciózzuk a dokumentum metaadatait a GroupDocs.Redaction for .NET segítségével – Átfogó útmutató](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Dokumentum betöltési oktatóanyagok a GroupDocs.Redaction for .NET használatával](/redaction/net/document-loading/)