---
date: '2026-06-11'
description: Tanulja meg, hogyan kell kinyerni a metadata-t a document streams-ből
  a GroupDocs.Redaction for .NET használatával, a setup, code examples és practical
  applications bemutatásával.
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: Hogyan kell kinyerni a metadata-t a document streams-ből a GroupDocs.Redaction
  .NET használatával
type: docs
url: /hu/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# Hogyan lehet metaadatokat kinyerni dokumentumfolyamokból a GroupDocs.Redaction .NET használatával

Unod már a dokumentuminformációk kézi kinyerését vagy a nagy fájlok kezelését, amelyek lelassítják a munkafolyamatot? **A metaadatok gyors kinyerése** gyakori kihívás, és a GroupDocs.Redaction .NET könyvtár gyors, memóriahatékony módot kínál a dokumentum részleteinek közvetlenül a folyamokból való lekérésére. Ebben az oktatóanyagban megtanulod, hogyan állítsd be a könyvtárat, hogyan húzd ki a fájltípust, az oldalszámot és a méretet egy folyamról, valamint hogyan készíts elő egy kimeneti mappát a további feldolgozáshoz.

## Gyors válaszok
- **Mit jelent a „metaadatok kinyerése”?** Azt jelenti, hogy a fájltípus, az oldalszám és a méret tulajdonságait olvasod ki anélkül, hogy a teljes dokumentumot betöltenéd a memóriába.  
- **Melyik könyvtár kezeli ezt?** A GroupDocs.Redaction .NET natív API-t biztosít a folyam‑alapú metaadat‑kinyeréshez.  
- **Szükségem van licencre?** Egy ingyenes próba verzió fejlesztéshez elegendő; a termeléshez kereskedelmi licenc szükséges.  
- **Kezelhetek 1 GB‑nál nagyobb PDF‑eket?** Igen – a folyamok lehetővé teszik akár 2 GB‑os fájlok kezelését a teljes fájl betöltése nélkül.  
- **Mely .NET verziók támogatottak?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, és .NET 6+.

## Mi az a metaadat‑kinyerés folyamokból?
A metaadat‑kinyerés folyamokból a folyamat, amely során egy `Stream` objektumból olvasod ki a dokumentum tulajdonságait, elkerülve a teljes fájl betöltését, ezáltal memóriát és CPU‑időt takarítva meg. Ez a technika ideális kötegelt feldolgozáshoz vagy felhő‑alapú szolgáltatásokhoz, ahol a erőforrások korlátozottak.

## Miért használjuk a GroupDocs.Redaction‑t metaadat‑kinyeréshez?
A GroupDocs.Redaction **30+ fájlformátumot** támogat (köztük PDF, DOCX, XLSX, PPTX és képtípusok), és akár **2 GB** méretű dokumentumokat képes feldolgozni, miközben a memóriahasználat **50 MB** alatt marad. A `Redactor` API egyetlen hívással visszaadja az összes kulcsfontosságú dokumentuminformációt, megszüntetve a több parser használatának szükségességét.

## Előfeltételek

- **GroupDocs.Redaction for .NET** (legújabb verzió)  
- **.NET Framework** 4.5+ **vagy** **.NET Core/5+/6+**  
- Alapvető C# ismeretek és fájl‑I/O tapasztalat  
- Visual Studio 2019 vagy újabb

## Hogyan állítsuk be a GroupDocs.Redaction‑t .NET‑hez?
A GroupDocs.Redaction használatának megkezdéséhez először hozzá kell adni a könyvtárat a projekthez. Ezt megteheted a .NET CLI‑val, a Visual Studio Package Manager‑rel vagy a NuGet UI‑val. Válaszd azt a megközelítést, amely a legjobban illik a munkafolyamatodhoz; a CLI ideális szkriptelhető build‑ekhez, míg a UI grafikus módot biztosít a verziók és függőségek böngészéséhez.

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**  
- Nyisd meg a NuGet Package Manager‑t a Visual Studio‑ban.  
- Keress rá a **"GroupDocs.Redaction"** csomagra, és telepítsd a legújabb verziót.

### Licencbeszerzési lépések
1. **Ingyenes próba:** Tölts le egy próba licencet, hogy korlátozások nélkül felfedezhesd az összes funkciót.  
2. **Ideiglenes licenc:** Kérj ideiglenes licencet a [GroupDocs](https://purchase.groupdocs.com/temporary-license/) oldalról a kiterjesztett teszteléshez.  
3. **Vásárlás:** Amikor a termeléshez készen állsz, vásárolj kereskedelmi licencet.  

További információkért látogasd meg a [GroupDocs weboldal](https://purchase.groupdocs.com/temporary-license/) oldalt.

### Alapvető inicializálás és beállítás
A `Redactor` osztály minden művelet belépési pontja, beleértve a metaadat‑kinyerést is.

A `Redactor` a fő osztály, amely egy dokumentum példányt képvisel, és módszereket biztosít a redakcióhoz, információlekéréshez és fájlmanipulációhoz. A telepítés után a következő módon hozhatsz létre egy `Redactor` objektumot:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

Most, hogy a könyvtár készen áll, merüljünk el a megvalósítás részleteiben.

## Hogyan nyerjünk ki metaadatokat egy dokumentumfolyamból?
Töltsd be a dokumentumot **csak‑olvasás módú folyamként**, inicializáld a `Redactor`‑t, és hívd meg a `GetDocumentInfo()`‑t a metaadatok egyetlen lépésben történő lekéréséhez. Ez a megközelítés elkerüli a teljes fájl memóriába töltését, ami különösen fontos nagy PDF‑ek vagy több száz oldalas Office dokumentumok esetén.

**Közvetlen válasz:** Nyisd meg a fájlt a `File.OpenRead()`‑val, add át a folyamot a `new Redactor(stream)`‑nek, majd hívd meg a `redactor.GetDocumentInfo()`‑t – a metódus egy objektumot ad vissza, amely tartalmazza a fájltípust, az oldalszámot és a méretet mindössze három sor kódban.

### 1. lépés: A forrásfájl útvonalának előkészítése
Először győződj meg róla, hogy a forrásfájl létezik, és a kimeneti mappa készen áll. Az alábbi segédmetódus ellenőrzi a kimeneti könyvtárat, és szükség esetén létrehozza azt.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*Miért?* Ez biztosítja a megfelelő útvonalat a későbbi fájlműveletekhez, és megakadályozza a `DirectoryNotFoundException` kivételt.

### 2. lépés: A dokumentumfolyam megnyitása
A `File.OpenRead()` **csak‑olvasás módú folyamként** nyitja meg a fájlt, ami alacsony memóriahasználatot biztosít még gigabájt‑méretű fájlok esetén is.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*Miért?* A folyamok lehetővé teszik a „helyben” feldolgozást, így a fájl csak részeivel dolgozhatsz, nem a teljes dokumentummal.

### 3. lépés: A Redactor inicializálása a dokumentumfolyammal
A `Redactor` az elsődleges API‑objektum, amely hozzáférést biztosít a dokumentumszintű műveletekhez, beleértve a metaadat‑kinyerést is.

A `Redactor` egyetlen dokumentumot képvisel, amely egy folyamról lett betöltve, és olyan metódusokat exponál, mint a `GetDocumentInfo()` a gyors tulajdonságlekéréshez.  

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*Miért?* A `Redactor` folyammal való példányosítása az objektumot a mögöttes fájlhoz köti anélkül, hogy teljesen betöltené azt.

### 4. lépés: Dokumentum metaadatainak lekérése
A `GetDocumentInfo()` egy `DocumentInfo` objektumot ad vissza, amely tartalmazza a fájlformátumot, az oldalszámot és a fájlméretet.

A `GetDocumentInfo()` egyetlen hívással vonja ki a fő tulajdonságokat (formátum, oldalszám, méret), így nincs szükség külön parser‑ekre.  

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*Miért?* Ez a lépés egyesíti az összes lényeges metaadatot, megkönnyítve a naplózást, szűrést vagy a dokumentumok jellemzőik alapján történő irányítását.

## Hogyan készítsünk elő egy kimeneti könyvtárat a feldolgozott fájlok számára?
Mielőtt bármilyen feldolgozott fájlt írnál, győződj meg arról, hogy a célmappa létezik és írható. Az útvonal programozott ellenőrzése és hiány esetén létrehozása elkerüli a gyakori futásidejű kivételeket, mint a `DirectoryNotFoundException` vagy jogosultsági hibák. Ez az egyszerű lépés a kódot hordozhatóvá teszi különböző környezetekben, legyen szó helyi futtatásról, szerverről vagy konténerről.

**Közvetlen válasz:** Használd a `Directory.Exists()`‑t az mappa ellenőrzéséhez, és a `Directory.CreateDirectory()`‑t a létrehozásához, ha nem létezik – ez az egy‑soros ellenőrzés garantálja a megfelelő útvonalat minden írási művelet előtt.

### Segédmetódus implementálása
Az alábbi metódus a ellenőrzés‑és‑létrehozás logikát egy helyen foglalja össze, és visszaadja a későbbi használatra ellenőrzött útvonalat.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*Miért?* Ennek a logikának a központosítása csökkenti a duplikációt, és könnyebbé teszi a kódkarbantartást.

## Gyakori problémák és megoldások
- **Jogosultsági hibák:** Győződj meg róla, hogy az alkalmazás olyan fiókkal fut, amelynek írási joga van a célmappához.  
- **Érvénytelen útvonalak:** Ellenőrizd a útvonalelválasztókat (`\\` Windows‑on, `/` Linux/macOS‑on), hogy elkerüld a `DirectoryNotFoundException`‑t.  
- **Nagy fájlok kezelése:** A folyamokat azonnal zárd le (`using` blokkok) a rendszer‑handle‑ek felszabadításához és a szivárgások megelőzéséhez.

## Gyakorlati alkalmazások
1. **Automatizált dokumentumfelvétel:** Metaadatok kinyerése feltöltéskor, majd tárolása adatbázisban a gyors keresés és megfelelőségi jelentés érdekében.  
2. **Jogi és megfelelőségi auditok:** Oldalszámok és fájltípusok lekérése a szabályozási előírásoknak való megfelelés ellenőrzéséhez archiválás előtt.  
3. **Vállalati tartalomkezelés:** Metaadatok használata a fájlok automatikus kategorizálásához mappákba, javítva a szervezést és a visszakeresési sebességet.

## Teljesítményfontosságú szempontok
- **Memóriakezelés:** Mindig csomagold a folyamokat `using` blokkokba, hogy automatikusan felszabaduljanak.  
- **Kötegelt feldolgozás:** Dokumentumokat 10‑20 fájlos csoportokban dolgozz fel, hogy egyensúlyba hozd a áteresztőképességet és a memóriahasználatot, különösen korlátozott erőforrású szervereken.  
- **Párhuzamosság:** Használd a `Parallel.ForEach`‑t a független fájlokhoz, de figyeld a CPU‑t és az I/O‑t, hogy elkerüld a versengést.

## Következtetés
Most már egy komplett, termelésre kész útmutatóval rendelkezel arról, **hogyan kell metaadatokat kinyerni** dokumentumfolyamokból a GroupDocs.Redaction .NET segítségével. A fenti lépések követésével hatékonyan lekérheted a fájltípust, az oldalszámot és a méretet, miközben alacsony memóriahasználatot tartasz fenn, és nagy fájlokkal is zökkenőmentesen dolgozol.

**Következő lépések**
- Tekintsd át a teljes API‑referenciát a [dokumentáció](https://docs.groupdocs.com/redaction/net/) oldalon.  
- Mélyedj el a [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/) anyagban, hogy felfedezd a redakciót, vízjelezést és OCR funkciókat.  
- Kísérletezz különböző fájlformátumokkal (PDF, DOCX, XLSX), hogy lásd, hogyan változik a metaadat a típusok között.  
- Integráld a kinyert metaadatokat a meglévő dokumentumkezelő vagy kereső megoldásodba.

## Gyakran ismételt kérdések

**K: Mi a fő felhasználási eset a GroupDocs.Redaction metaadat‑kinyeréséhez?**  
V: Gyors, memóriahatékony dokumentumtulajdonság‑lekérést biztosít indexeléshez, megfelelőségi ellenőrzésekhez és automatizált irányításhoz anélkül, hogy a teljes fájlt megnyitnád.

**K: Kinyerhetek metaadatokat jelszóval védett fájlokból?**  
V: Igen, add meg a jelszót a `Redactor` objektum létrehozásakor; az API belsőleg feloldja a folyamot.

**K: Támogatja a könyvtár a nem‑PDF formátumokat, például DOCX vagy XLSX?**  
V: Teljes mértékben – a GroupDocs.Redaction több mint 30 formátumot kezel, köztük PDF, DOCX, XLSX, PPTX és gyakori képtípusok.

**K: Mekkora dokumentumot dolgozhatok fel folyamokkal?**  
V: A folyamok lehetővé teszik akár **2 GB** méretű fájlok feldolgozását, miközben a memóriafogyasztás **50 MB** alatt marad, köszönhetően a „helyben” olvasásnak.

**K: Hol kaphatok segítséget, ha problémába ütközöm?**  
V: Látogasd meg a [GroupDocs fórum](https://forum.groupdocs.com/c/redaction/33) közösségi támogatásért, vagy nézd meg a hivatalos dokumentációt a hibaelhárítási tippekért.

---

**Utolsó frissítés:** 2026-06-11  
**Tesztelve:** GroupDocs.Redaction 23.12 for .NET  
**Szerző:** GroupDocs  

**Erőforrások**  
- **Dokumentáció:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API referencia:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Letöltés:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## Kapcsolódó oktatóanyagok

- [Master Document Metadata Retrieval with GroupDocs.Redaction .NET API](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)  
- [How to Redact Document Metadata Using GroupDocs.Redaction for .NET - A Comprehensive Guide](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)  
- [Secure Document Redaction in .NET Using Streams: A Guide for GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)