---
date: '2026-07-20'
description: Leer hoe u formaten kunt weergeven met GroupDocs.Redaction .NET, de functie
  in uw documentworkflow kunt integreren en de prestaties kunt verbeteren.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Ontdek hoe u formaten kunt weergeven met GroupDocs.Redaction .NET,
  bekijk een stapsgewijze handleiding en ontvang tips voor optimale prestaties in
  uw .NET‑toepassingen.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Hoe formaten weergeven met GroupDocs.Redaction .NET
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
title: Hoe formaten weergeven met GroupDocs.Redaction .NET
type: docs
url: /nl/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Hoe formaten weergeven met GroupDocs.Redaction .NET

Het beheren van een breed scala aan documenttypen is een dagelijkse realiteit voor ontwikkelaars die document‑gerichte applicaties bouwen. In deze tutorial leer je **hoe formaten te vermelden** die GroupDocs.Redaction .NET kan verwerken, zodat je bestanden kunt valideren vóór verwerking, gebruikers nauwkeurige opties kunt bieden, en je workflow efficiënt houdt.

## Introductie

Efficiënte documentafhandeling begint met precies weten welke bestandstypen je bibliotheek ondersteunt. GroupDocs.Redaction biedt een ingebouwde methode om deze informatie op te halen, zodat je dynamische UI‑elementen kunt bouwen, validatieregels kunt afdwingen en runtime‑fouten kunt voorkomen. Hieronder vind je alles wat je nodig hebt om aan de slag te gaan, van installatie tot praktische code‑fragmenten en prestatie‑tips.

### Snelle antwoorden
- **Wat betekent “how to list formats”?** Het verwijst naar het ophalen van de collectie bestandsextensies die GroupDocs.Redaction kan verwerken.  
- **Heb ik een licentie nodig?** Ja, een geldige GroupDocs.Redaction‑licentie is vereist voor productiegebruik.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Hoeveel formaten zijn er beschikbaar?** Meer dan 30 invoer‑ en uitvoerformaten worden standaard ondersteund.  
- **Is er speciale configuratie nodig?** Geen extra configuratie is vereist naast de standaard bibliotheekinitialisatie.

## Wat is “how to list formats”?

Het omvat het aanroepen van de FileType‑API van de bibliotheek om een collectie te verkrijgen waarbij elk item de bestandsextensie en een mens‑leesbare naam bevat. Ontwikkelaars kunnen vervolgens deze collectie itereren om validatieregels te bouwen, UI‑dropdowns te vullen of ondersteunde types te loggen, zodat alleen compatibele documenten worden verwerkt.

## Waarom formaten vermelden met GroupDocs.Redaction?

GroupDocs.Redaction ondersteunt **30+** verschillende bestandstypen — waaronder PDF, DOCX, PPTX en afbeeldingsformaten — waardoor je de meeste bedrijfsdocumenten kunt afhandelen zonder converters van derden. Door deze formaten programmatisch te vermelden, elimineer je giswerk, verminder je support‑tickets en zorg je ervoor dat alleen compatibele bestanden je verwerkings‑pipeline binnenkomen.

## Vereisten

- **GroupDocs.Redaction for .NET** – download het nieuwste pakket van de officiële site.  
- **.NET Framework of .NET Core** – compatibel met je ontwikkelomgeving.  
- **Visual Studio** (of een andere C#‑compatibele IDE).  
- Basiskennis van C#‑syntaxis.

## GroupDocs.Redaction voor .NET instellen

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Package Manager
`Install-Package GroupDocs.Redaction`

### NuGet Package Manager UI
- Zoek naar **“GroupDocs.Redaction”** en installeer de nieuwste versie.

### Licentie‑acquisitie
GroupDocs biedt een gratis proefversie, een tijdelijke licentie voor evaluatie, of volledige aankoopopties. Bezoek de GroupDocs‑website om het juiste licentiebestand te verkrijgen.

### Basisinitialisatie en configuratie
Na het toevoegen van het pakket, verwijs je naar de namespace en maak je een `Redactor`‑instance aan:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Implementatie‑gids

### Hoe vermeld ik formaten met GroupDocs.Redaction .NET?
Laad de bibliotheek, roep de statische helper aan en sorteer de resultaten — dit geeft je een kant‑klaar te gebruiken collectie in slechts twee regels code. Gebruik `FileType.GetSupportedFileFormats()` om een `IEnumerable<FileType>` op te halen die de extensie en weergavenaam van elk formaat bevat, en sorteer vervolgens op extensie voor een nette UI‑lijst.

### Opvragen van ondersteunde bestandsformaten

#### Overzicht
Het doel is een lijst te verkrijgen van bestandstypen die GroupDocs.Redaction kan verwerken, zodat je deze kunt integreren in validatielogica, UI‑dropdowns of logmechanismen.

#### Stapsgewijze implementatie

**1. Retrieve Supported File Types**  
`FileType.GetSupportedFileFormats()` retourneert elk formaat dat de bibliotheek herkent. De methode maakt deel uit van de `GroupDocs.Redaction.FileType`‑klasse, die metadata bevat zoals bestandsextensie en vriendelijke naam.

**2. Display Supported File Types**  
Itereer over de collectie en geef elke extensie en beschrijving weer. Inline code‑voorbeeld:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

Het fragment print een netjes geordende lijst zoals “.pdf – Portable Document Format”, waardoor het perfect is voor het vullen van UI‑elementen.

### Probleemoplossingstips
- **Missing Package** – Controleer de NuGet‑pakketreferentie en herstel pakketten indien nodig.  
- **Incorrect License Path** – Zorg ervoor dat het licentiebestand naar de output‑directory wordt gekopieerd of geef een absoluut pad op.  
- **Unsupported Extension** – Als een formaat niet wordt vermeld, controleer dan of je de nieuwste bibliotheekversie gebruikt; nieuwere releases voegen extra formaten toe.

## Praktische toepassingen

Het begrijpen van ondersteunde bestandsformaten opent verschillende real‑world scenario's:

1. **Document Management Systems** – Valideer uploads tegen de ondersteunde lijst om verwerkingsfouten te voorkomen.  
2. **Content Security** – Pas redaction‑regels alleen toe op bestandstypen die de engine veilig kan wijzigen.  
3. **Batch Processing Pipelines** – Filter grote bestandsbatches voordat je redaction aanroept, waardoor CPU‑ en geheugenverbruik wordt bespaard.

## Prestatie‑overwegingen
- **Memory Footprint** – Het vermelden van formaten is een lichte bewerking; er wordt geen document in het geheugen geladen.  
- **Batch Operations** – Wanneer je honderden bestanden verwerkt, haal de formatlijst één keer op en hergebruik deze om overbodige aanroepen te vermijden.  
- **Thread Safety** – `FileType.GetSupportedFileFormats()` is thread‑safe en kan vanuit parallelle taken worden aangeroepen zonder synchronisatie.

## Conclusie
Je hebt nu een volledige, productie‑klare aanpak voor **hoe formaten te vermelden** met GroupDocs.Redaction .NET. Door deze functionaliteit te integreren, kun je validatie verbeteren, de gebruikerservaring verhogen en je document‑pipelines robuust houden.

### Volgende stappen
- Verken de `Redactor`‑API om redaction‑regels toe te passen op basis van bestandstype.  
- Combineer de formatlijst met een front‑end dropdown voor naadloze bestandsselectie.  
- Bekijk de prestatie‑gids om grootschalige batch‑taken te optimaliseren.

## Veelgestelde vragen

**Q: Kan ik de formatlijst ophalen zonder een Redactor‑instance te initialiseren?**  
A: Ja, `FileType.GetSupportedFileFormats()` is statisch en vereist geen `Redactor`‑object.

**Q: Bevat de lijst zowel invoer‑ als uitvoerformaten?**  
A: De methode retourneert alle formaten die de bibliotheek zowel kan lezen als schrijven; elk `FileType` bevat een `CanRead`‑ en `CanWrite`‑vlag.

**Q: Hoe vaak wordt de ondersteunde formatlijst bijgewerkt?**  
A: GroupDocs brengt formatupdates uit met elke bibliotheekversie; het controleren van de lijst tijdens runtime zorgt ervoor dat je altijd de nieuwste set hebt.

**Q: Is er een manier om alleen PDF‑compatibele formaten te filteren?**  
A: Ja, filter de collectie waar `format.Extension == ".pdf"` of waar `format.Name.Contains("PDF")`.

**Q: Werkt deze aanpak op .NET Core 2.1?**  
A: De methode vereist .NET Core 3.1 of later; eerdere runtimes worden niet ondersteund.

## FAQ‑sectie
1. **Hoe installeer ik GroupDocs.Redaction voor .NET?**  
   Gebruik de CLI‑opdracht `dotnet add package GroupDocs.Redaction` of installeer via de NuGet Package Manager UI.  
2. **Wat zijn veelvoorkomende problemen bij het ophalen van ondersteunde formaten?**  
   Zorg ervoor dat alle afhankelijkheden zijn hersteld en dat je de juiste namespace (`GroupDocs.Redaction`) gebruikt.  
3. **Kan ik deze functie gebruiken met niet‑.NET‑applicaties?**  
   Deze tutorial richt zich op .NET, maar GroupDocs biedt vergelijkbare API’s voor Java, Python en andere platforms.  
4. **Hoe kan ik de prestaties optimaliseren bij gebruik van GroupDocs.Redaction?**  
   Hergebruik de formatlijst, vermijd het laden van volledige documenten wanneer alleen compatibiliteit wordt gecontroleerd, en monitor het geheugenverbruik tijdens batch‑taken.  
5. **Welke bestandstypen ondersteunt GroupDocs.Redaction?**  
   De bibliotheek ondersteunt 30+ formaten, waaronder PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG en nog veel meer. Gebruik `FileType.GetSupportedFileFormats()` om de volledige lijst te bekijken.

## Bronnen
- [Documentatie](https://docs.groupdocs.com/redaction/net/)
- [API‑referentie](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction downloaden](https://releases.groupdocs.com/redaction/net/)
- [Gratis ondersteuningsforum](https://forum.groupdocs.com/c/redaction/33)
- [Tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/)

---

**Laatst bijgewerkt:** 2026-07-20  
**Getest met:** GroupDocs.Redaction 4.2.0 for .NET  
**Auteur:** GroupDocs  

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

## Gerelateerde tutorials

- [Formaatverwerkingstutorials voor GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Documentlaad‑tutorials met GroupDocs.Redaction voor .NET](/redaction/net/document-loading/)
- [Documentopslagtutorials voor GroupDocs.Redaction .NET](/redaction/net/document-saving/)