---
date: '2026-01-21'
description: Tanulja meg, hogyan lehet OCR-rel kitakarni PDF-et, és hogyan lehet szkennelt
  dokumentumokat kitakarni a GroupDocs.Redaction for Java Azure OCR integrációval.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: PDF redigálása OCR-rel a GroupDocs és az Azure OCR használatával – Java útmutató
type: docs
url: /hu/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# PDF redakció OCR-rel a GroupDocs és Azure OCR használatával – Java útmutató

Ebben az átfogó bemutatóban megtudhatja, hogyan **redact PDF with OCR** Java‑ban, a GroupDocs.Redaction és a Microsoft Azure OCR kombinációjával. Akár natív PDF‑ekkel, akár beolvasott képekkel dolgozik, ez az útmutató megmutatja, hogyan találja meg pontosan és takarja el az érzékeny adatokat, segítve a **redact scanned documents** megfelelve a adatvédelmi előírásoknak.

## Gyors válaszok
- **Mit csinál az OCR redakció?** Képek/PDF‑ek szövegét kinyeri, és automatikusan?** Egy ingyenendő a teszteléshez; a termeléshez állandó licenc szükséges.  
- **Redaktálhatok natív és beolvasott PDF‑eket is?** Igen – az OCR lehetővé teszi a beolvasott dokumentumok redakcióját is.

## Mi az a „redact PDF with OCR”?
A PDF redakció OCR-rel azt jelenti, hogy optikai karakterfelismerést (OCR) használunk a vizuális szöveg kereshető karakterláncokká alakításához, majd redakciós mintákat (pl. regex) alkalmazunk az információ elrejtésére, mielőtt a fájlt megosztanák vagy tárolnák.

## Miért használjuk a GroupDocs.Redaction‑t Azure OCR‑rel?
- **Magas pontosság** a beolvasott oldalak esetén az Azure felhőalapú OCR motorjának köszönhetően.  
- **Egyszerű Java API**, amely közvetlenül integrálható a meglévő munkafolyamatba.  
- **Rugalmas redakciós szabályok** – regex, kulcsszavak vagy egyedi logika.  
- **Megfelelőség‑kész** kimenet, amely véglegesen eltávolítja az érzékeny adatokat.

## Előfeltételek
- Java Development Kit (JDK) 8 vagy újabb.  
- Maven (vagy a JAR manuális letöltésének lehetősége).  
- Microsoft Azure fiók OCR hitelesítő adatokkal.  
- Alapvető Java ismeretek és a reguláris kifejezések ismerete.

## GroupDocs.Redaction for Java beállítása

### Maven beállítás
Adja hozzá a GroupDocs tárolót és függőséget a `pom.xml`‑hez:

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
Ha nem szeretne Maven‑t használni, töltse le a legújabb JAR‑t a hivatalos kiadási oldalról: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Licenc beszerzése
- **Free Trial** – fedezze fel a fő funkciókat kötelezettség nélkül.  
- **Temporary License** – hosszabbítsa meg a próbaidőszakot nagyobb projektekhez.  
- **Full License** – korlátlan használat és prémium támogatás.

### Alapvető inicializálás és beállítás
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Hogyan redaktáljunk PDF‑et OCR-rel Java‑ban

### 1. lépés: Dokumentum betöltése OCR beállításokkal
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Subsequent redaction steps will be placed here
}
```
- **Paraméterek**  
  - `"YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf"` – a cél PDF elérési útja.  
  - `new LoadOptions()` – alapértelmezett betöltési konfiguráció.  
  - `settings` – tartalmazza az Azure OCR connector‑t.

### 2. lépés: Regex redakciók alkalmazása (pl. társadalombiztosítási számok)
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
- **Regex magyarázat** – `\b\d{3}-\d{2}-\d{4}\b` olyan mintákat egyezeti, mint `123-45-6789`.  
- **ReplacementOptions** – a felismert szöveget `[REDACTED]`‑re cseréli.

### Gyakori hibák és hibaelhárítás
- **Azure hitelesítő adatok** – ellenőrizze a feliratkozási kulcsot és a végpontot.  
- **Fájl útvonal** – győződjön meg róla, hogy a PDF létezik, és az alkalmazásnak van olvasási/írási jogosultsága.  
- **Teljesítmény** – nagy PDF‑ek esetén növelni kell a heap méretét vagy aszinkron feldolgozást alkalmazni.

## Gyakorlati felhasználási esetek beolvasott dokumentumok redakciójához
1. **Jogász irodák** – ügyfélazonosítók elrejtése a peres anyagok megosztása előtt.  
2. **Pénzügyi intézmények** – számlaszámok maszkolása beolvasott kimutatásokban.  
3. **Egészségügyi szolgáltatók** – beteg PHI védelme beolvasott orvosi feljegyzésekben.  
4. **Állami ügynökségek** – személyes adatok eltávolítása a nyilvános nyilvánt  
5. **Vállalatok** – szerződések tisztítása harmadik fél auditok előtt.

## Teljesítmény tippek
- A regex mintákat legyenek a lehető legspecifikusabbak, hogy csökkentsék a feldolgozási időt.  
- való futtatását.

## Gyakran ismételt kérdések

** képek vagy beolvasott PDF‑ek szövegének kinyerésére, majd redakciós szabályokat alkalmaz a szöveg végleges eltávolítására.

**Q: Használhatom a GroupDocs.Redaction‑t Azure OCR nélkül?**  
A: Igen, de az OCR jelentősen javítja a pontosságot beolvasott dokumentumok esetén, lehetővé téve a **redact scanned documents** hatékony végrehajtását.

**Q: Hogyan kezeljem a komplex regex mintákat?**  
A: Tesztelje a mintákat mintaadatokkal, használjon szóhatárokat (`\b`) a részleges egyezések elkerülésére, és fontolja meg a nagy kifejezések felosztását több egyszerűbb redakcióra.

**Q: Mik a tipikus teljesítménykorlátok?**  
A: Nehéz OCR hívások nagy fájlokon, túl általános regex, és elégtelen memóriaallokáció. Optimalizáljon regex‑ekkel és skálázza az erőforrásokat.

**Q: Hol kaphatok segítséget, ha problémába ütközöm?**  
A: Tegyen fel kérdéseket a GroupDocs közösségi fórumon: [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33).

## További források
- **Documentation**: https://docs.groupdocs.com/redaction/java/
- **API Reference**: https://reference.groupdocs.com/redaction/java
- **Download**: https://releases.groupdocs.com/redaction/java/
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java
- **Free Support**: https://forum.groupdocs.com/c/redaction/33
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

---

**Legutóbb frissítve:** 2026-01-21  
**Tesztelve a következővel:** GroupDocs.Redaction 24.9 for Java  
**Szerző:** GroupDocs