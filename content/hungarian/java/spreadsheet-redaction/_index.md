---
date: 2026-08-04
description: Ismerje meg, hogyan szűrheti a Java táblázat-adatokat, és hogyan redigálhat
  biztonságosan oszlopokat vagy cellákat Excel táblázatokban a GroupDocs.Redaction
  for Java segítségével.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Ismerje meg, hogyan szűrheti a Java táblázat-adatokat, és hogyan redigálhat
  biztonságosan oszlopokat vagy cellákat Excel táblázatokban a GroupDocs.Redaction
  for Java segítségével.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Java táblázat-adatok szűrése – útmutató a GroupDocs.Redaction használatával
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Java táblázat-adatok szűrése – útmutató a GroupDocs.Redaction használatával
type: docs
url: /hu/java/spreadsheet-redaction/
weight: 12
---

# Excel táblázat adatok szűrése Java – GroupDocs.Redaction Java útmutató

Ha **filter spreadsheet data java**-t kell alkalmaznia a redakció előtt, jó helyen jár. Ebben az útmutatóban megtudja, hogyan lehet elkülöníteni sorokat, oszlopokat vagy egyedi cellákat, amelyek személyes vagy bizalmas információkat tartalmaznak, majd biztonságosan redakciózni őket a GroupDocs.Redaction for Java segítségével. A lépéseket egyszerű nyelven magyarázzuk, tartalmazzák a legjobb gyakorlat tippeket, és megmutatják, hogyan lehet a feldolgozást gyorsan tartani még nagy munkafüzetek esetén.

## Gyors válaszok
- **Melyik könyvtár kezeli a táblázat redakciót Java-ban?** GroupDocs.Redaction for Java.  
- **Szűrhetek sorokat anélkül, hogy az egész fájlt a memóriába tölteném?** Igen – az API adatfolyamot használ, és lehetővé teszi a szűrők alkalmazását futás közben.  
- **Milyen fájlformátumok támogatottak?** Több mint 30 táblázat formátum, beleértve az XLS, XLSX, CSV és ODS formátumokat.  
- **Szükségem van licencre a fejlesztéshez?** Ideiglenes licenc teszteléshez működik; teljes licenc szükséges a termeléshez.  
- **Van korlátozás a munkafüzet méretére?** A motor képes 500 MB-ig terjedő fájlok feldolgozására túlzott memóriahasználat nélkül.

## Mi az a filter spreadsheet data java?
**Filter spreadsheet data java** a folyamat, amely programozott módon kiválaszt specifikus sorokat, oszlopokat vagy cellákat egy Excel‑szerű munkafüzetben Java kóddal, hogy csak a célzott tartalom legyen vizsgálva vagy redakciózva. Ez a technika csökkenti a futási időt, korlátozza a felesleges módosításokat, és segít megfelelni a GDPR‑szerű megfelelésnek.

## Miért szűrje a filter spreadsheet data java?
A GroupDocs.Redaction Java támogatja a **30+ táblázat formátumot**, és képes olyan munkafüzeteket feldolgozni, amelyek **legfeljebb 500 MB**-ot tartalmaznak (kb. 1 millió sor), miközben a memóriahasználat **200 MB** alatt marad. Először szűrve elkerülhető a nem kapcsolódó adatok érintése, ami átlagosan **40‑60 %**-kal csökkenti a feldolgozási időt a tipikus adatvédelmi tisztítási forgatókönyvekben.

## Előfeltételek
- Java 17 vagy újabb telepítve.  
- Maven vagy Gradle build rendszer.  
- GroupDocs.Redaction for Java (letölthető a hivatalos oldalról).  
- Ideiglenes vagy teljes licenckulcs.  

## Hogyan szűrje az adatokat a táblázatokban a GroupDocs.Redaction Java használatával?
Töltse be a munkafüzetet, határozzon meg egy szűrőt, amely megfelel a redakcióra szánt celláknak, majd alkalmazza a redakció műveletet. Az API streaming módon hajtja végre a szűrést, így soha nem kell az egész fájlt a RAM-ban tartania.

`RedactionFilter` osztály lehetővé teszi oszlopszámok, sorintervallumok vagy egyedi predikátumok megadását. Például célozhat minden **B** oszlopbeli cellát, amely e‑mail cím mintát tartalmaz, vagy korlátozhatja a redakciót olyan sorokra, ahol a „Status” oszlop értéke „Confidential”.

**Közvetlen válasz (40‑70 szó):**  
Hozzon létre egy `RedactionFilter` példányt, állítsa be az oszlopszámot és egy reguláris‑kifejezés feltételt, majd adja át a szűrőt a `Redactor.redact(workbook, filter)` metódusnak. Ez az egy‑soros szűrő izolálja a kritériumainak megfelelő pontos cellákat, és a redaktor eltávolítja vagy maszkolja őket, miközben a munkalap többi része érintetlen marad. A művelet lineáris időben fejeződik be a szűrt sorok számához képest.

### 1. lépés: a szűrő példányosítása
`RedactionFilter` a központi osztály, amely a táblázat redakció szűrési szabályát képviseli. Oszlopszámokat, sor számokat vagy egyedi lambda kifejezéseket fogad el az adatok pontos meghatározásához.

### 2. lépés: a feltétel beállítása
Használja a `filter.setColumnIndex(1)`-et a **B** oszlop (nulla‑alapú) célzásához, és a `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`-t az e‑mail minták egyezéséhez. Több feltételt is kombinálhat a `filter.and(...)` vagy `filter.or(...)` segítségével.

### 3. lépés: a redakció alkalmazása
`Redactor` a fő osztály, amely redakciós műveleteket hajt végre egy munkafüzeten.  
Adja át a munkafüzetet és a beállított szűrőt a `Redactor` objektumnak. Az API streaming módon dolgozza fel a munkafüzetet, alkalmazza a szűrőt, és a redakciózott eredményt egy új fájlba írja, megőrizve az eredeti formázást és képleteket.

## Gyakori problémák és megoldások
- **A szűrő nem egyezik egyetlen cellával sem:** Ellenőrizze az oszlopszámot (nulla‑alapú) és győződjön meg róla, hogy a reguláris‑kifejezés szintaxisa helyes Java számára.  
- **Out‑of‑memory hibák nagy fájlok esetén:** Növelje mérsékelten a JVM heap méretét (pl. `-Xmx1g`), vagy a szűrés előtt ossza fel a munkafüzetet kisebb darabokra.  
- **A redakciózott kimenet elveszíti a formázást:** `RedactionOptions` lehetővé teszi a redakció viselkedésének testreszabását, például a cellaformázás megőrzését. Használja a `RedactionOptions.setPreserveFormatting(true)`-t a cellastílusok érintetlen tartásához.

## Miért szűrje a táblázat adatokat?
A redakció előtti szűrés csak a munkafüzet érzékeny részeit izolálja, ami azt jelenti, hogy elkerülhető a tiszta adatok felesleges módosítása. Ez a szelektív megközelítés csökkenti a véletlen adatvesztés kockázatát, és felgyorsítja a megfelelőségi auditokat, mivel az audit napló jóval kevesebb bejegyzést tartalmaz.

## Hogyan redakciózza az e‑mail címeket Excel táblázatokban a GroupDocs.Redaction Java API használatával
Töltse be az Excel fájlt, alkalmazzon egy szűrőt, amely a tipikus e‑mail mintát keresi, és hívja meg a redaktort. Az API minden egyező e‑mail címet helyettesít egy helykitöltővel, például “***@***.com”, miközben megőrzi a környező cella elrendezését.

## Adatszűrés – elérhető útmutatók
- [Hogyan redakciózza az e‑mail címeket Excel táblázatokban a GroupDocs.Redaction Java API használatával](./redact-emails-excel-groupdocs-redaction-java/)

## További források

- [GroupDocs.Redaction for Java dokumentáció](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API referencia](https://reference.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java letöltése](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction fórum](https://forum.groupdocs.com/c/redaction/33)
- [Ingyenes támogatás](https://forum.groupdocs.com/)
- [Ideiglenes licenc](https://purchase.groupdocs.com/temporary-license/)

---

**Utolsó frissítés:** 2026-08-04  
**Tesztelve ezzel:** GroupDocs.Redaction 23.11 for Java  
**Szerző:** GroupDocs  

## Gyakran feltett kérdések

**K: Szűrhetek több oszlopot egyszerre?**  
V: Igen, további oszlopszámokat adhat hozzá ugyanahhoz a `RedactionFilter` példányhoz, vagy több szűrőt láncolhat a `filter.or(...)` segítségével.

**K: A szűrő működik jelszóval védett munkafüzeteken?**  
V: Adja meg a jelszót a munkafüzet megnyitásakor; a szűrő a dekódolás után működik, ugyanúgy, mint egy nem védett fájlon.

**K: Hány sort képes az API egyetlen műveletben kezelni?**  
V: A motor akár 1 millió sor (≈500 MB) kezelésére is optimalizált, anélkül, hogy az egész fájlt a memóriába töltené.

**K: Lehet előnézetet kapni arról, mely cellák lesznek redakciózva mentés előtt?**  
V: Igen, hívja a `filter.preview(workbook)`-ot, hogy megkapja a kritériumnak megfelelő cellacímek listáját.

**K: Milyen licencmodell szükséges a termeléshez?**  
V: Teljes kereskedelmi licenc szükséges a termeléshez; egy ideiglenes licenc elegendő a teszteléshez és értékeléshez.

## Kapcsolódó útmutatók

- [Hogyan redakciózza az érzékeny adatokat Excel táblázatokban a GroupDocs.Redaction Java API használatával](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Érzékeny adatok maszkolása Java – GroupDocs.Redaction útmutató](/redaction/java/getting-started/)
- [Érzékeny adatok maszkolása Java – Személyes információk redakciója a GroupDocs.Redaction segítségével](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)