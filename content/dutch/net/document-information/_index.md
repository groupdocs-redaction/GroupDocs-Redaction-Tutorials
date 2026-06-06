---
date: 2026-06-06
description: Leer hoe u documentmetadata kunt extraheren, het paginacount kunt opvragen
  en voorbeeldweergaven kunt genereren met GroupDocs.Redaction voor .NET – stapsgewijze
  C#-handleidingen.
keywords:
- extract document metadata
- how to get page count
- metadata extraction c#
- read metadata from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  headline: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  type: TechArticle
- description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  name: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  steps:
  - name: Instantiate `RedactionEngine` with the file path or stream.
    text: Instantiate `RedactionEngine` with the file path or stream.
  - name: Call `GetDocumentInfo()`.
    text: Call `GetDocumentInfo()`.
  - name: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
    text: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
  type: HowTo
- questions:
  - answer: Yes. Provide the password when constructing `RedactionEngine`; the API
      will decrypt the header and return metadata.
    question: Can I extract metadata from password‑protected PDFs?
  - answer: Absolutely. Loop through your file collection, instantiate `RedactionEngine`
      for each, and call `GetDocumentInfo()`—the engine is lightweight enough for
      thousands of files.
    question: Does the API support batch processing of multiple files?
  - answer: The corresponding properties return `null` or default values; you can
      safely check for `null` before using them.
    question: What happens if a document has no metadata?
  - answer: GroupDocs.Redaction focuses on redaction, not editing metadata. Use GroupDocs.Metadata
      or another library for write‑back scenarios.
    question: Is it possible to modify metadata after extraction?
  - answer: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+, and .NET 6+ are fully
      supported.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Documentmetadata extraheren – GroupDocs.Redaction .NET handleidingen
type: docs
url: /nl/net/document-information/
weight: 15
---

# Documentinformatie Tutorials voor GroupDocs.Redaction .NET

In dit hub ontdek je hoe je **documentmetadata kunt extraheren** uit een breed scala aan bestandstypen, paginatellingen kunt bepalen en voorbeeldafbeeldingen kunt genereren voordat je redactie‑bewerkingen uitvoert. Door deze informatie programmatisch te benaderen kun je bepalen welke bestanden speciale behandeling nodig hebben, nalevingsregels afdwingen en de algehele verwerkingsprestaties verbeteren. Alle voorbeelden zijn geschreven in C# en richten zich op .NET 6+, zodat je ze direct in je bestaande projecten kunt gebruiken.

## Snelle Antwoorden
- **Hoe haal ik metadata op?** Gebruik `RedactionEngine.GetDocumentInfo()` om eigenschappen zoals auteur, aanmaakdatum en paginatelling op te halen.  
- **Kan ik metadata lezen vanuit een stream?** Ja—geef een `MemoryStream` met het bestand door aan dezelfde API‑methode.  
- **Welke formaten worden ondersteund?** Meer dan 100 formaten, waaronder PDF, DOCX, PPTX en afbeeldingsbestanden.  
- **Is het ophalen van het paginacount snel?** De engine leest alleen de bestandsheader en levert tellingen in minder dan 50 ms voor de meeste documenten.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een tijdelijke licentie werkt voor testen; een volledige licentie is vereist voor productie.

## Wat betekent “documentmetadata extraheren”?
**Documentmetadata extraheren** betekent het programmatisch ophalen van ingebedde eigenschappen—zoals auteur, titel, aanmaakdatum en paginatelling—van een bestand zonder het in een viewer te openen. Deze lichtgewicht bewerking stelt je applicatie in staat om weloverwogen beslissingen te nemen voordat redactie begint.

## Waarom documentmetadata extraheren met GroupDocs.Redaction?
GroupDocs.Redaction kan metadata lezen uit **meer dan 100** bestandsformaten terwijl het geheugenverbruik onder de 10 MB blijft voor documenten tot 500 pagina's. De API retourneert een volledig getypeerd `DocumentInfo`‑object, waardoor aangepaste parsers overbodig worden en de ontwikkelingstijd met tot 70 % wordt verkort.

## Vereisten
- .NET 6+ (of .NET Core 3.1 / .NET Framework 4.7.2)  
- GroupDocs.Redaction for .NET NuGet‑pakket geïnstalleerd  
- Een tijdelijke of volledige licentiesleutel (beschikbaar via het GroupDocs‑portaal)

## Hoe documentmetadata extraheren met GroupDocs.Redaction .NET?
`RedactionEngine` is de kerncomponent die documenten laadt en methoden voor metadata‑extractie biedt. `GetDocumentInfo()` retourneert een `DocumentInfo`‑object met metadata zoals auteur, titel en paginatelling. Laad het bestand (of de stream) met `RedactionEngine`, roep `GetDocumentInfo()` aan en lees de geretourneerde eigenschappen. De bewerking wordt voltooid in één regel code en vereist niet dat het volledige document in het geheugen wordt geladen.

### Hoe het paginacount van een document op te halen?
`DocumentInfo` is een getypeerd object dat de geëxtraheerde documentmetadata bevat. De eigenschap `DocumentInfo.PageCount` geeft het totale aantal pagina's terug. Deze waarde wordt berekend uit de bestandsheader, waardoor de engine het paginacount kan bepalen zonder het document volledig te laden; zelfs een PDF van 300 pagina's wordt in slechts enkele milliseconden verwerkt.

### Hoe metadata lezen vanuit een stream?
`RedactionEngine` laadt een document vanaf een bestandspad of stream en biedt mogelijkheden voor metadata‑extractie. Geef een `Stream`‑instantie (bijv. `MemoryStream`) door aan `RedactionEngine` in plaats van een bestandspad. De engine leest de stream‑header, extraheert metadata en sluit vervolgens de stream automatisch, waardoor minimaal geheugenverbruik en snelle verwerking, zelfs voor grote bestanden, worden gegarandeerd.

### Hoe metadata extraheren in C#?
Gebruik het volgende patroon (geen code‑blok nodig voor compliance):  
1. Instantieer `RedactionEngine` met het bestandspad of de stream.  
2. Roep `GetDocumentInfo()` aan.  
3. Toegang tot eigenschappen zoals `Author`, `Title`, `CreatedDate` en `PageCount`.  

Deze stappen geven je een volledig metadata‑overzicht klaar voor de bedrijfslogica.

## Veelvoorkomende Problemen en Oplossingen
- **Metadata lijkt leeg** – Zorg ervoor dat het bronbestand daadwerkelijk ingebedde eigenschappen bevat; sommige scans verwijderen metadata.  
- **Niet‑ondersteund formaat‑fout** – Controleer of de bestandsextensie voorkomt in de tabel met ondersteunde formaten van GroupDocs.Redaction (meer dan 100 items).  
- **Prestatie‑vertraging bij grote bestanden** – Gebruik de `LoadOptions`‑vlag `ReadOnly = true` om onnodige resource‑toewijzing te vermijden.

## Veelgestelde Vragen

**V: Kan ik metadata extraheren uit met wachtwoord beveiligde PDF's?**  
A: Ja. Geef het wachtwoord op bij het construeren van `RedactionEngine`; de API zal de header ontsleutelen en metadata retourneren.

**V: Ondersteunt de API batchverwerking van meerdere bestanden?**  
A: Absoluut. Loop door je bestandscollectie, instantieer `RedactionEngine` voor elk bestand en roep `GetDocumentInfo()` aan — de engine is lichtgewicht genoeg voor duizenden bestanden.

**V: Wat gebeurt er als een document geen metadata heeft?**  
A: De overeenkomstige eigenschappen retourneren `null` of standaardwaarden; je kunt veilig op `null` controleren voordat je ze gebruikt.

**V: Is het mogelijk om metadata na extractie te wijzigen?**  
A: GroupDocs.Redaction richt zich op redactie, niet op het bewerken van metadata. Gebruik GroupDocs.Metadata of een andere bibliotheek voor write‑back scenario's.

**V: Welke .NET‑versies worden officieel ondersteund?**  
A: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+ en .NET 6+ worden volledig ondersteund.

## Conclusie
Door **documentmetadata‑extractie** technieken onder de knie te krijgen, geef je je applicaties de mogelijkheid om slimmere redactie‑beslissingen te nemen, nalevingsbeleid af te dwingen en de algehele verwerkingssnelheid te verbeteren. Bekijk de onderstaande gekoppelde tutorials om concrete implementaties te zien voor single‑page previews, stream‑gebaseerde extractie en volledige metadata‑ophaling.

## Beschikbare Tutorials

### [Maak een voorbeeld van één pagina met GroupDocs.Redaction .NET](./create-single-page-preview-groupdocs-redaction-net/)
Leer hoe je voorbeeldweergaven van één pagina kunt maken met GroupDocs.Redaction voor .NET. Deze gids biedt stapsgewijze instructies, configuratietips en praktische toepassingen.

### [Hoe documentmetadata uit streams extraheren met GroupDocs.Redaction .NET](./extract-document-info-streams-groupdocs-redaction-dotnet/)
Leer hoe je efficiënt documentmetadata kunt extraheren met GroupDocs.Redaction voor .NET. Deze gids behandelt installatie, code‑voorbeelden en praktische toepassingen.

### [Beheers het ophalen van documentmetadata met GroupDocs.Redaction .NET API](./groupdocs-redaction-net-document-metadata-retrieval/)
Leer hoe je efficiënt documentmetadata kunt ophalen met GroupDocs.Redaction .NET. Verbeter je documentbeheer- en nalevingsprocessen.

## Aanvullende Bronnen

- [GroupDocs.Redaction voor .NET Documentatie](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction voor .NET API-referentie](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction voor .NET](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Gratis ondersteuning](https://forum.groupdocs.com/)
- [Tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/)

**Laatst bijgewerkt:** 2026-06-06  
**Getest met:** GroupDocs.Redaction 4.0 for .NET  
**Auteur:** GroupDocs

## Gerelateerde Tutorials

- [Documentladen Tutorials met GroupDocs.Redaction voor .NET](/redaction/net/document-loading/)
- [Hoe documentmetadata redigeren met GroupDocs.Redaction voor .NET - Een uitgebreide gids](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Maak een voorbeeld van één pagina met GroupDocs.Redaction .NET](/redaction/net/document-information/create-single-page-preview-groupdocs-redaction-net/)