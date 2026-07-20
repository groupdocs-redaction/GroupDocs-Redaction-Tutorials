---
date: '2026-07-20'
description: Leer hoe u documenten kunt redigeren, gevoelige informatie kunt verbergen
  en geredigeerde bestanden kunt opslaan in een geheugenstroom met GroupDocs.Redaction
  voor .NET.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: Hoe documenten redigeren met GroupDocs.Redaction voor .NET. Volg deze
  stapsgewijze gids om gevoelige informatie te verbergen en het geredigeerde bestand
  op te slaan in een geheugenstroom.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: Hoe documenten redigeren met GroupDocs.Redaction voor .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: Hoe documenten redigeren met GroupDocs.Redaction voor .NET – Een complete gids
type: docs
url: /nl/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# Hoe documenten te redigeren met GroupDocs.Redaction voor .NET

In moderne bedrijfsomgevingen is **hoe documenten te redigeren** een cruciale vaardigheid voor het beschermen van persoonlijke gegevens, handelsgeheimen en compliance‑gerelateerde informatie. Deze gids leidt u door het redigeren van gevoelige informatie uit Word-, PDF- of afbeeldingsbestanden en vervolgens het opslaan van de geredigeerde output direct naar een geheugenstroom — allemaal met GroupDocs.Redaction voor .NET.

## Snelle antwoorden
- **Wat doet redactie?** Het vervangt geselecteerde inhoud permanent door een tijdelijke aanduiding of verwijdert deze, waardoor de gegevens nooit kunnen worden hersteld.  
- **Welke formaten worden ondersteund?** Meer dan 30 bestandstypen, waaronder PDF, DOCX, PPTX en gangbare afbeeldingsformaten.  
- **Kan ik redigeren zonder naar schijf te schrijven?** Ja — sla het resultaat op in een `MemoryStream` voor verwerking in het geheugen.  
- **Heb ik een licentie nodig voor productie?** Een volledige licentie is vereist voor productiegebruik; een gratis proefversie is beschikbaar voor evaluatie.  
- **Is het compatibel met .NET Core?** Absoluut — GroupDocs.Redaction werkt met .NET Framework 4.6+, .NET Core 3.1+ en .NET 5/6/7.

## Wat is documentredactie?
Documentredactie verwijdert of verduistert vertrouwelijke tekst, afbeeldingen en metadata permanent uit een bestand, zodat de verborgen inhoud niet kan worden hersteld, bekeken of later geëxtraheerd. Het vervangt de gevoelige elementen door een tijdelijke aanduiding, zoals een zwart rechthoek of aangepaste tekst, en werkt de documentstructuur bij zodat de geredigeerde gegevens onherroepelijk zijn.

## Waarom GroupDocs.Redaction gebruiken om documenten te redigeren?
GroupDocs.Redaction ondersteunt **30+ bestandsformaten** en kan bestanden tot **2 GB** verwerken zonder het volledige document in het geheugen te laden, wat een **30 % snellere verwerkingstijd** oplevert vergeleken met veel concurrenten. De API stelt u in staat om exacte‑zinnen, reguliere‑expressies of op afbeeldingen gebaseerde redacties toe te passen met één methode‑aanroep, waardoor het de meest efficiënte keuze is voor .NET‑ontwikkelaars.

## Voorvereisten
- **GroupDocs.Redaction** NuGet‑pakket (nieuwste versie).  
- .NET Framework 4.6+ **of** .NET Core 3.1+ geïnstalleerd.  
- Een C#‑compatibele IDE zoals Visual Studio 2022.  
- Basiskennis van C# en vertrouwdheid met bestands‑I/O.

### Vereiste bibliotheken en versies
- **GroupDocs.Redaction** – gebruik altijd de nieuwste release om toegang te krijgen tot de nieuwste redactie‑algoritmen en beveiligingspatches.  
- **System.IO** – voor stream‑verwerking (ingebouwd in .NET).

### Stappen voor het verkrijgen van een licentie
- **Gratis proefversie:** Meld u aan op de GroupDocs‑website voor een proefperiode van 30 dagen.  
- **Tijdelijke licentie:** Vraag een tijdelijke sleutel aan voor ontwikkeltesten.  
- **Volledige licentie:** Koop een productielicentie voor onbeperkt gebruik.

## Basisinitialisatie en -configuratie
De `Redactor`‑klasse is het toegangspunt voor alle redactie‑bewerkingen in GroupDocs.Redaction. Nadat u het NuGet‑pakket hebt geïnstalleerd, maakt u een instantie van `Redactor` met het pad naar het bron‑document.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## Hoe specifieke tekst in een document redigeren?
Om specifieke tekst te redigeren, laadt u het bronbestand met een `Redactor`‑instantie en past u vervolgens een `ExactPhraseRedaction` toe die zich richt op de exacte tekenreeks die u wilt verbergen. De API scant het document, vervangt elke overeenkomst door de gekozen overlay en registreert de wijzigingen in een changelog, zodat u de redacties kunt verifiëren voordat u opslaat.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

De `ExactPhraseRedaction`‑klasse vervangt elke voorkomen van de exacte zin door een zwart rechthoek (of elke aangepaste tijdelijke aanduiding die u configureert).  

**Stap‑voor‑stap:**
1. **Load** – Maak een `Redactor`‑instantie die naar uw bestand wijst.  
2. **Apply** – Roep `Apply` aan met een `ExactPhraseRedaction` (of een ander redactietype).  
3. **Inspect** – Bekijk `RedactorChangeLog` om te bevestigen hoeveel overeenkomsten er zijn gevonden en vervangen.  

## Hoe een geredigeerd document opslaan naar een Memory Stream?
`MemoryStream` is een .NET‑stream die gegevens in het geheugen opslaat, waardoor snel lezen/schrijven mogelijk is zonder schijf‑I/O. Met de `Save`‑methode kunt u de geredigeerde output naar een `MemoryStream` sturen, die vervolgens over een netwerk kan worden verzonden, in een database kan worden opgeslagen, of direct kan worden geretourneerd vanuit een API‑endpoint zonder tijdelijke bestanden te maken.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**Belangrijke punten:**
- De `Save`‑methode schrijft de geredigeerde output naar elke `Stream`‑implementatie, inclusief `MemoryStream`.  
- Er worden geen tijdelijke bestanden aangemaakt, wat de beveiliging en prestaties verbetert.  
- U kunt dit combineren met ASP.NET Core’s `FileStreamResult` om het bestand direct naar een browser te retourneren.

## Veelvoorkomende valkuilen en oplossingen
| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Redactie niet toegepast** | De hoofdlettergevoeligheid van de zin verschilt van de bron. | Gebruik `ExactPhraseRedaction("John Doe", caseSensitive: false)` of een reguliere‑expressie‑redactie voor flexibele matching. |
| **Grote bestanden veroorzaken OutOfMemory** | Poging om het volledige bestand in het geheugen te laden. | GroupDocs.Redaction streamt gegevens intern; zorg ervoor dat u de nieuwste versie gebruikt die bestanden in delen verwerkt. |
| **Opgeslagen bestand is corrupt** | Stream is niet gereset vóór verzending. | Na `redactor.Save(stream)`, stel `stream.Position = 0` in vóór het lezen of retourneren. |

## Veelgestelde vragen

**Q: Kan ik PDF‑bestanden redigeren met dezelfde API?**  
A: Ja — GroupDocs.Redaction behandelt PDF, DOCX, PPTX en vele afbeeldingsformaten uniform; wijs simpelweg `Redactor` op een PDF‑bestand.

**Q: Blijft de redacties behouden na het converteren van het document naar een ander formaat?**  
A: Absoluut — zodra geredigeerd, wordt de inhoud permanent verwijderd, ongeacht latere conversies.

**Q: Hoe kan ik het uiterlijk van de redacties aanpassen?**  
A: Gebruik `RedactionOptions` om de overlay‑kleur, doorzichtigheid in te stellen of tekst te vervangen door een aangepaste string.

**Q: Is het mogelijk om te redigeren met reguliere expressies?**  
A: Ja — `RegexRedaction` laat u patronen definiëren zoals creditcard‑nummers of e‑mailadressen.

**Q: Welke .NET‑versies worden officieel ondersteund?**  
A: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6 en .NET 7.

---

**Laatst bijgewerkt:** 2026-07-20  
**Getest met:** GroupDocs.Redaction 23.12 for .NET  
**Auteur:** GroupDocs  

---

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## Gerelateerde tutorials

- [Hoe documenten te laden en te redigeren met GroupDocs.Redaction .NET&#58; Een volledige gids](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Geredigeerde documenten opslaan in origineel formaat met GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Beveiligde documentredactie in .NET met streams&#58; Een gids voor GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)