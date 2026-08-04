---
date: 2026-08-04
description: Leer hoe u spreadsheet data java kunt filteren en veilig kolommen of
  cellen in Excel-spreadsheets kunt redigeren met GroupDocs.Redaction voor Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Leer hoe u spreadsheet data java kunt filteren en veilig kolommen
  of cellen in Excel-spreadsheets kunt redigeren met GroupDocs.Redaction voor Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Filter spreadsheet data java – handleiding met GroupDocs.Redaction
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
title: Filter spreadsheet data java – handleiding met GroupDocs.Redaction
type: docs
url: /nl/java/spreadsheet-redaction/
weight: 12
---

# Filter spreadsheet-gegevens java – GroupDocs.Redaction Java-handleiding

Als je **filter spreadsheet data java** moet uitvoeren voordat je redactie toepast, ben je op de juiste gids terechtgekomen. In deze handleiding ontdek je hoe je rijen, kolommen of individuele cellen die persoonlijke of vertrouwelijke informatie bevatten, kunt isoleren en vervolgens veilig kunt redigeren met GroupDocs.Redaction voor Java. De stappen worden in eenvoudige taal uitgelegd, bevatten best‑practice tips, en laten zien hoe je de verwerking snel houdt, zelfs bij grote werkboeken.

## Snelle antwoorden
- **Welke bibliotheek verwerkt spreadsheet‑redactie in Java?** GroupDocs.Redaction for Java.  
- **Kan ik rijen filteren zonder het hele bestand in het geheugen te laden?** Ja – de API streamt gegevens en laat je filters in realtime toepassen.  
- **Welke bestandsformaten worden ondersteund?** Meer dan 30 spreadsheetformaten, waaronder XLS, XLSX, CSV en ODS.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een tijdelijke licentie werkt voor testen; een volledige licentie is vereist voor productie.  
- **Is er een limiet voor de grootte van een werkboek?** De engine kan bestanden tot 500 MB verwerken zonder buitensporig geheugenverbruik.

## Wat is filter spreadsheet data java?
**Filter spreadsheet data java** is het proces waarbij je programmatisch specifieke rijen, kolommen of cellen in een Excel‑achtige werkmap selecteert met Java‑code, zodat alleen gerichte inhoud wordt onderzocht of geredigeerd. Deze techniek verkort de uitvoeringstijd, beperkt onnodige wijzigingen, en helpt te voldoen aan GDPR‑achtige naleving.

## Waarom filter spreadsheet data java?
GroupDocs.Redaction Java ondersteunt **30+ spreadsheetformaten** en kan werkboeken verwerken die **tot 500 MB** bevatten (ongeveer 1 miljoen rijen) terwijl het geheugengebruik onder **200 MB** blijft. Door eerst te filteren, raak je geen ongerelateerde gegevens, wat de verwerkingstijd gemiddeld met **40‑60 %** verkort voor typische privacy‑scrubbing scenario's.

## Vereisten
- Java 17 of hoger geïnstalleerd.  
- Maven of Gradle build‑systeem.  
- GroupDocs.Redaction for Java (downloadbaar van de officiële site).  
- Een tijdelijke of volledige licentiesleutel.  

## Hoe filter je gegevens in spreadsheets met GroupDocs.Redaction Java?
Laad het werkboek, definieer een filter dat overeenkomt met de cellen die je wilt redigeren, en voer vervolgens de redactiebewerking uit. De API voert het filter uit in een streaming‑modus, zodat je nooit het volledige bestand in RAM hoeft te houden.

De `RedactionFilter`‑klasse stelt je in staat kolomindexen, rijbereiken of aangepaste predicaten op te geven. Bijvoorbeeld, je kunt elke cel in kolom **B** targeten die een e‑mailadres‑patroon bevat, of je kunt redactie beperken tot rijen waar een “Status”‑kolom gelijk is aan “Confidential”.

**Direct antwoord (40‑70 woorden):**  
Maak een `RedactionFilter`‑instantie, stel de kolomindex en een reguliere‑expressie‑conditie in, en geef vervolgens het filter door aan `Redactor.redact(workbook, filter)`. Dit één‑regelige filter isoleert de exacte cellen die aan je criteria voldoen, en de redacteur verwijdert of maskeert ze terwijl de rest van het blad onaangeroerd blijft. De bewerking voltooit in lineaire tijd ten opzichte van de gefilterde rijen.

### Stap 1: instantieer het filter
`RedactionFilter` is de kernklasse die een filterregel voor spreadsheet‑redactie vertegenwoordigt. Het accepteert kolomnummers, rijnummers of aangepaste lambda‑expressies om gegevens te pinpointen.

### Stap 2: configureer de voorwaarde
Gebruik `filter.setColumnIndex(1)` om kolom B (nul‑gebaseerd) te targeten en `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` om e‑mailpatronen te matchen. Je kunt ook meerdere voorwaarden combineren met `filter.and(...)` of `filter.or(...)`.

### Stap 3: pas de redactie toe
`Redactor` is de hoofdklasse die redactiebewerkingen op een werkboek uitvoert.  
Geef het werkboek en het geconfigureerde filter door aan het `Redactor`‑object. De API streamt het werkboek, past het filter toe, en schrijft het geredigeerde resultaat naar een nieuw bestand, waarbij de oorspronkelijke opmaak en formules behouden blijven.

## Veelvoorkomende problemen en oplossingen
- **Filter komt niet overeen met enige cellen:** Controleer de kolomindex (nul‑gebaseerd) en zorg dat de reguliere‑expressie‑syntaxis correct is voor Java.  
- **Out‑of‑memory fouten bij grote bestanden:** Verhoog de JVM‑heap‑grootte bescheiden (bijv. `-Xmx1g`) of splits het werkboek in kleinere delen vóór het filteren.  
- **Geredigeerde output verliest opmaak:** `RedactionOptions` stelt je in staat het redactiegedrag aan te passen, zoals het behouden van celopmaak. Gebruik `RedactionOptions.setPreserveFormatting(true)` om celstijlen intact te houden.

## Waarom spreadsheet‑gegevens filteren?
Filteren vóór redactie isoleert alleen de gevoelige delen van een werkboek, waardoor je onnodige wijzigingen aan schone gegevens vermijdt. Deze selectieve aanpak vermindert ook het risico op accidenteel gegevensverlies en versnelt compliance‑audits omdat het auditlog veel minder vermeldingen bevat.

## Hoe e‑mails te redigeren in Excel‑spreadsheets met GroupDocs.Redaction Java API
Laad je Excel‑bestand, pas een filter toe dat zoekt naar het typische e‑mailpatroon, en roep de redacteur aan. De API vervangt elke overeenkomende e‑mail door een placeholder zoals “***@***.com” terwijl de omliggende celindeling behouden blijft.

## Hoe gegevens filteren – beschikbare tutorials
- [Hoe e‑mails te redigeren in Excel‑spreadsheets met GroupDocs.Redaction Java API](./redact-emails-excel-groupdocs-redaction-java/)

## Aanvullende bronnen
- [GroupDocs.Redaction voor Java Documentatie](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction voor Java API‑referentie](https://reference.groupdocs.com/redaction/java/)
- [Download GroupDocs.Redaction voor Java](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Gratis ondersteuning](https://forum.groupdocs.com/)
- [Tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/)

---

**Laatst bijgewerkt:** 2026-08-04  
**Getest met:** GroupDocs.Redaction 23.11 for Java  
**Auteur:** GroupDocs  

## Veelgestelde vragen

**Q: Kan ik meerdere kolommen tegelijk filteren?**  
A: Ja, je kunt extra kolomindexen toevoegen aan dezelfde `RedactionFilter`‑instantie of meerdere filters chainen met `filter.or(...)`.

**Q: Werkt het filter op met wachtwoord beveiligde werkboeken?**  
A: Geef het wachtwoord op bij het openen van het werkboek; het filter werkt na decryptie net als bij een onbeveiligd bestand.

**Q: Hoeveel rijen kan de API aan in één bewerking?**  
A: De engine is geoptimaliseerd voor tot 1 miljoen rijen (≈500 MB) zonder het volledige bestand in het geheugen te laden.

**Q: Is het mogelijk om een voorbeeld te zien van welke cellen worden geredigeerd vóór het opslaan?**  
A: Ja, roep `filter.preview(workbook)` aan om een lijst van celadressen te krijgen die aan de criteria voldoen.

**Q: Welk licentiemodel is vereist voor productiegebruik?**  
A: Een volledige commerciële licentie is vereist voor productiedeployments; een tijdelijke licentie is voldoende voor testen en evaluatie.

## Gerelateerde tutorials
- [Hoe gevoelige gegevens te redigeren in Excel‑spreadsheets met GroupDocs.Redaction Java API](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Masker gevoelige gegevens Java – GroupDocs.Redaction gids](/redaction/java/getting-started/)
- [Masker gevoelige gegevens Java – Redigeer persoonlijke info met GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)