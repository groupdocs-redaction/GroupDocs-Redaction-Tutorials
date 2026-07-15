---
date: '2026-06-26'
description: Ismerje meg, hogyan lehet kinyerni a szkennelt PDF szövegét és maszkolni
  az érzékeny adatokat a GroupDocs OCR Redaction és az Azure OCR segítségével. Redact
  social security number és cserélje le a bizalmas információkat a PDF-ben hatékonyan.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Szkennelt PDF szövegének kinyerése – Adatok maszkolása a GroupDocs OCR-rel
type: docs
url: /hu/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Szkennelt PDF szövegének kinyerése – Adatok maszkolása a GroupDocs OCR-rel

A mai adatközpontú világban a **szkennelt PDF‑ből szöveg kinyerése** és a bizalmas információk maszkolása elengedhetetlen megfelelőségi lépés. Ez az útmutató bemutatja, hogyan használhatja a GroupDocs Redaction‑t a Microsoft Azure OCR-rel, hogy megbízhatóan felismerje a szkennelt oldalak rejtett szövegét, és egy biztonságos helyettesítővel, például **`[REDACTED]`** cserélje le. Meg fogja látni, miért gyors, pontos, és készen áll a termelési szintű munkaterhelésekre.

## Gyors válaszok
- **Mi jelent a „érzékeny adatok maszkolása”?** A felismert bizalmas szöveget egy helyettesítővel cseréli (pl. `[REDACTED]`).  
- **Melyik könyvtár kezeli az OCR‑t?** Microsoft Azure OCR csatlakozó, a GroupDocs Redaction‑ön keresztül használva.  
- **Szükségem van licencre?** Egy ingyenes próba a kiértékeléshez működik; a termeléshez állandó licenc szükséges.  
- **Lehet szkennelt PDF‑eket redigálni?** Igen—az OCR kinyeri a rejtett szöveget, mielőtt a regex‑alapú redigálás alkalmazásra kerül.  
- **Ez a megoldás csak Java‑ra korlátozódik?** A példa Java‑alapú, de a GroupDocs hasonló API‑kat kínál .NET‑hez és más platformokhoz is.

## Mi az OCR‑alapú redigálás?
Az OCR‑alapú redigálás először OCR‑t futtat minden oldalon, a képeket kereshető szöveggé alakítja, majd regex‑mintákat alkalmaz a találatok helyettesítésére egy, például `[REDACTED]` maszkkal. Ez a kétszakaszos folyamat lehetővé teszi, hogy megbízhatóan elrejtse a személyes adatokat még szkennelt PDF‑ekben is, biztosítva, hogy minden érzékeny karakterlánc eltávolításra kerüljön a dokumentum megosztása vagy archiválása előtt.

## Miért használja a GroupDocs Redaction‑t az Azure OCR-rel?
A GroupDocs Redaction‑t Azure OCR-rel érdemes használni, mert **>98 % OCR pontosságot biztosít nyomtatott szövegre**, támogat **50+ bemeneti és kimeneti formátumot**, és képes **több száz oldalas PDF‑eket feldolgozni anélkül, hogy a teljes fájlt a memóriába töltené**, ezáltal gyors, skálázható redigálást biztosít a megfelelőséghez. A megoldás továbbá **képes egy 1 000 oldalas PDF‑et 2 percen belül feldolgozni egy 8‑magos szerveren**, így a kötegelt feladatok is gyakorlatiasak.

## Előfeltételek
- **Java Development Kit (JDK) 8+** telepítve.  
- **Maven** (ha a függőségkezelést részesíti előnyben) vagy a JAR‑ok kézi letöltésének lehetősége.  
- **Microsoft Azure OCR hitelesítő adatok** (végpont és előfizetési kulcs).  
- Alapvető Java ismeretek és a reguláris kifejezésekkel való jártaság.

## A GroupDocs Redaction beállítása Java‑hoz

### Maven beállítás
Adja hozzá a GroupDocs tárolót és függőséget a `pom.xml` fájlhoz:

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
Ha a JAR‑ok kézi kezelését részesíti előnyben, töltse le a legújabb kiadást a [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)-ról.

### Licenc beszerzése
- **Free Trial** – minden funkció kipróbálása költség nélkül.  
- **Temporary License** – a kiértékelési idő meghosszabbítása.  
- **Full License** – a termelésre kész képességek feloldása.

### Alapvető inicializálás és beállítás
A `Redactor` osztály a központi motor, amely OCR‑kivonást végez és redigálási szabályokat alkalmaz PDF dokumentumokra.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Hogyan maszkoljuk az érzékeny adatokat OCR redigálással
Az érzékeny adatok OCR redigálással történő maszkolása magában foglalja a PDF betöltését Azure OCR beállításokkal, a rejtendő adatok regex‑mintáinak meghatározását, és a Redactor meghívását, hogy minden egyezést egy, például `[REDACTED]` helyettesítővel cseréljen. A könyvtár egyetlen munkafolyamatban kezeli az OCR‑t, a minták egyezését és a PDF újraírását.

### 1. lépés: Dokumentum betöltése OCR beállításokkal
`LoadOptions` konfigurálja, hogyan tölti be a GroupDocs a fájlt, lehetővé téve OCR csatlakozók, például az Azure átadását.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – cserélje le a PDF elérési útjára.  
- **`settings`** – tartalmazza a korábban létrehozott Azure OCR csatlakozót.

### 2. lépés: Regex redigálások meghatározása és alkalmazása
`ReplacementOptions` határozza meg a helyettesítő szöveget, amely a redigálás során minden regex egyezést lecserél.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- A `\b\d{3}-\d{2}-\d{4}\b` minta az USA társadalombiztosítási számokat (Social Security Numbers) egyezteti.  
- `ReplacementOptions("[REDACTED]")` minden egyezést a maszkkal cserél, hatékonyan **maszkolva az érzékeny adatokat**.

## Gyakori felhasználási esetek az érzékeny adatok maszkolására
1. **Jogi dokumentumkezelés** – ügyfélazonosítók elrejtése a vázlatok megosztása előtt.  
2. **Pénzügyi jelentés** – számlaszámok és tranzakcióazonosítók védelme.  
3. **Egészségügyi nyilvántartások** – HIPAA megfelelés érdekében a betegazonosítók redigálása.  
4. **Kormányzati kiadványok** – személyes adatok eltávolítása a nyilvános nyilvántartásokból.  
5. **Vállalati szerződések** – a tulajdonosi feltételek elrejtése külső felülvizsgálatok során.

## Teljesítmény tippek
- **Regex optimalizálása** – kerülje a túl általános mintákat, amelyek növelik a feldolgozási időt; a jól megtervezett kifejezések akár 40 %-kal is csökkenthetik a futási időt.  
- **Memória kezelés** – zárja le a `Redactor` példányt gyorsan (a try‑with‑resources ezt automatikusan megteszi).  
- **Aszinkron végrehajtás** – kötegelt feldolgozás esetén futtassa a redigálási feladatokat külön szálakon vagy használjon feladatlistát a UI válaszkészségének fenntartásához.

## Hibaelhárítás
- **Azure hitelesítő hiba** – ellenőrizze újra a végpont URL‑t és az előfizetési kulcsot a `MicrosoftAzureOcrConnector`‑ban.  
- **Dokumentum nem töltődik be** – ellenőrizze a fájl útvonalát, és győződjön meg róla, hogy a PDF nincs jelszóval védve (vagy adja meg a jelszót a `LoadOptions`‑on keresztül).  
- **Nincs alkalmazott redigálás** – először tesztelje a regex‑et egyszerű karakterlánccal; használja a `Pattern.compile`‑t egységtesztben a találatok megerősítéséhez.

## Gyakran feltett kérdések

**Q: Mi az OCR redigálás?**  
A: Az OCR redigálás az Optikai Karakterfelismerést (Optical Character Recognition) használja a képek vagy szkennelt PDF‑ek rejtett szövegének kinyerésére, majd redigálási szabályokat alkalmaz a szöveg maszkolására.

**Q: Használhatom a GroupDocs Redaction‑t Azure OCR nélkül?**  
A: Igen, de az OCR jelentősen javítja a pontosságot szkennelt dokumentumok esetén, ahol a natív szövegkinyerés nem működik.

**Q: Hogyan kezelem a komplex regex mintákat?**  
A: Építse és tesztelje őket fokozatosan, a Java `Pattern` osztályt egy sandbox környezetben használva, mielőtt nagy dokumentumokra alkalmazná.

**Q: Mik a tipikus teljesítménybeli szűk keresztmetszetek?**  
A: Nagy PDF‑ek, túl komplex regex‑ek és szinkron OCR hívások lassíthatják a feldolgozást; fontolja meg a kötegelt feldolgozást és optimalizált mintákat.

**Q: Elérhető támogatás a megvalósítási problémákhoz?**  
A: Teljes mértékben—lépjen kapcsolatba a [GroupDocs fórumon](https://forum.groupdocs.com/c/redaction/33) közösségi segítségért vagy vegye fel a kapcsolatot a GroupDocs támogatással.

## További források
- **Documentation**: https://docs.groupdocs.com/redaction/java/  
- **API Reference**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Free Support**: https://forum.groupdocs.com/c/redaction/33  
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

---

**Utoljára frissítve:** 2026-06-26  
**Tesztelve:** GroupDocs.Redaction 24.9 (Java)  
**Szerző:** GroupDocs  

## Kapcsolódó oktatóanyagok

- [Secure PDF Redaction using OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [How to Redact Text with GroupDocs.Redaction for Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)