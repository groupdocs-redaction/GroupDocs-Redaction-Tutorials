---
date: '2026-10-06'
description: Leer hoe u gevoelige gegevens kunt redigeren met GroupDocs.Redaction
  .NET. Deze stapsgewijze handleiding laat zien hoe u een redactiebeleid maakt, toepast
  en opslaat als XML.
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: Leer hoe u gevoelige gegevens kunt redigeren met GroupDocs.Redaction
  .NET. Deze stapsgewijze handleiding laat zien hoe u een redactiebeleid maakt, toepast
  en opslaat als XML.
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: Hoe gevoelige gegevens te redigeren met GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: Hoe gevoelige gegevens te redigeren met GroupDocs.Redaction .NET
type: docs
url: /nl/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# Hoe gevoelige gegevens te redigeren met GroupDocs.Redaction .NET

Het beschermen van vertrouwelijke informatie in contracten, financiële overzichten of patiëntendossiers is een niet‑onderhandelbare vereiste voor moderne applicaties. In deze gids leer je **hoe je gevoelige gegevens kunt redigeren** met GroupDocs.Redaction voor .NET, van het installeren van de SDK tot het definiëren van herbruikbare XML‑beleid die op elk documenttype kunnen worden toegepast.

## Snelle antwoorden
- **Wat betekent “create redaction policy”?** Het is het proces van het definiëren van regels (tekst, regex, afbeeldingen, enz.) die GroupDocs.Redaction vertellen hoe vertrouwelijke inhoud te verbergen of te vervangen.  
- **Welke bibliotheek heb ik nodig?** GroupDocs.Redaction voor .NET, beschikbaar via NuGet.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een permanente licentie is vereist voor productie.  
- **Kan ik het beleid hergebruiken?** Ja—eenmaal opgeslagen als XML kun je het later laden en toepassen op elk document.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Wat is een redactiebeleid?

Een redactiebeleid is een verzameling regels die specificeren *wat* moet worden verwijderd of vervangen en *hoe* de vervanging eruit moet zien. Door één keer een beleid te maken, kun je consistente beveiligingsnormen toepassen op elk document dat door je applicatie wordt verwerkt.

## Hoe werkt een redactiebeleid?

Laad een document met de `Redactor`‑engine, voeg een of meer redactie‑regels toe en roep vervolgens `Apply` aan. De engine scant het document, maskeert de overeenkomende inhoud en kan optioneel een nieuw bestand genereren. dezelfde set regels kan worden geëxporteerd naar XML, waardoor je het beleid kunt hergebruiken zonder de code opnieuw te compileren.

## Waarom GroupDocs.Redaction gebruiken om een redactiebeleid te maken?

GroupDocs.Redaction biedt een uitgebreide reeks functies die het maken, beheren en uitvoeren van redactiebeleid vereenvoudigen, waardoor consistente gegevensbescherming over verschillende documenttypen wordt gegarandeerd, terwijl hoge prestaties en eenvoudige integratie in bestaande .NET‑applicaties voor teams en organisaties worden geleverd.

- **Brede bestandsondersteuning** – de SDK verwerkt 30+ bestandstypen, waaronder PDF, DOCX, XLSX, PPTX en afbeeldingsformaten, en kan bestanden tot 2 GB verwerken zonder het volledige bestand in het geheugen te laden.  
- **Programmeerbare precisie** – definieer exacte zinnen, reguliere expressies of aangepaste logica om alleen de gegevens te targeten die je wilt verbergen.  
- **Herbruikbare XML‑beleid** – exporteer je regels één keer en deel ze met teams, services of micro‑services.  
- **Prestaties‑geoptimaliseerde engine** – de bibliotheek verwerkt documenten van honderden pagina's in minder dan een seconde op typische serverhardware, waardoor het geschikt is voor high‑throughput‑pijplijnen.

## Vereisten
- GroupDocs.Redaction‑bibliotheek die compatibel is met je .NET‑runtime.  
- Visual Studio, VS Code, of een IDE die C# ondersteunt.  
- Basiskennis van C# en .NET‑projectstructuur.

## GroupDocs.Redaction voor .NET instellen

Eerst voeg je de bibliotheek toe aan je project.

**Gebruik .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Gebruik Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

Of zoek naar “GroupDocs.Redaction” in de NuGet Package Manager UI en installeer het vanaf daar.

### Licentie‑acquisitie
- Begin met een **gratis proefversie** om de functies te verkennen.  
- Vraag een **tijdelijke licentie** aan voor uitgebreid testen, en koop daarna een volledige licentie voor productiegebruik.

### Basisinitialisatie
Voeg de namespace toe aan je bronbestand:

De `Redactor`‑klasse is de kernengine die een document laadt en redactie‑regels toepast.  
```csharp
using GroupDocs.Redaction;
```  

De `Redactor`‑klasse is de kernengine van GroupDocs.Redaction die een document laadt en redactie‑regels toepast.

## Hoe een redactiebeleid stap voor stap te maken

Hieronder vind je een volledige walkthrough die laat zien hoe je programmatisch een redactiebeleid kunt opbouwen, de regels configureert, toepast op een document, en tenslotte het beleid opslaat als een XML‑bestand voor toekomstig hergebruik, waardoor consistente redactie over meerdere projecten en documenttypen wordt gegarandeerd.

### Stap 1: bereid je documentmap voor
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*Vervang `"YOUR_DOCUMENT_DIRECTORY"` door de map die de documenten bevat die je wilt beschermen.*

### Stap 2: laad het document
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
Het `Redactor`‑object opent het bestand en beheert de levenscyclus.

### Stap 3: definieer de redacties
ExactPhraseRedaction definieert een regel die een specifieke zin vervangt, terwijl `RegexRedaction` een reguliere expressie gebruikt om patronen te matchen.  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
Hier maken we twee regels:
1. **ExactPhraseRedaction** – vervangt een bekende zin door “[REDACTED]”.  
2. **RegexRedaction** – vindt datums in `YYYY‑MM‑DD`‑formaat en vervangt ze door “[DATE REDACTED]”.

### Stap 4: pas de redacties toe
```csharp
redactor.Apply(redactions);
```  
Alle gedefinieerde regels worden in één doorgang uitgevoerd op het geopende document.

### Stap 5: sla het beleid op als een XML‑bestand
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
Het XML‑bestand slaat de redactie‑definities op, waardoor je hetzelfde beleid kunt hergebruiken zonder de code opnieuw te schrijven.

## Praktische toepassingen
- **Juridische kantoren** kunnen zaaknummers en klantnamen redigeren voordat ze concepten delen.  
- **Financiële afdelingen** maskeren rekeningnummers of transactiedata in rapporten.  
- **Zorgverleners** zorgen voor HIPAA‑naleving door patiëntidentificatoren te verwijderen.

## Prestatietips
- Open **een document tegelijk** om het geheugenverbruik laag te houden.  
- Schrijf **efficiënte reguliere expressies**; vermijd te brede patronen die de verwerkingstijd verhogen.  
- Houd de bibliotheek **up‑to‑date** om te profiteren van prestatieverbeteringen en nieuwe redactie‑typen.

## Veelvoorkomende problemen en oplossingen
| Probleem | Waarom het gebeurt | Hoe op te lossen |
|----------|--------------------|------------------|
| **IO‑exception bij het voorbereiden van de map** | Verkeerd pad of ontbrekende schrijfrechten | Controleer of de map bestaat en de applicatie lees‑/schrijfrechten heeft. |
| **Regex komt niet overeen met verwachte tekst** | Patroon is te strikt of er ontbreken escape‑tekens | Test de regex met een online tester; pas kwantoren aan of escape speciale tekens. |
| **Beleidsbestand niet aangemaakt** | `SavePolicy` aangeroepen vóór het toepassen van redacties of met een ongeldig pad | Zorg dat de uitvoermap schrijfbaar is en roep `SavePolicy` aan na `Apply`. |

## Veelgestelde vragen

**V: Kan ik een bestaand XML‑beleid laden in plaats van er een programmatisch te bouwen?**  
A: Ja—gebruik `redactor.LoadPolicy("policy.xml")` om een eerder opgeslagen beleid te importeren.

**V: Ondersteunt GroupDocs.Redaction wachtwoord‑beveiligde PDF’s?**  
A: Absoluut. Geef het wachtwoord door aan de `Redactor`‑constructor: `new Redactor(sourceFile, "password")`.

**V: Is het mogelijk om afbeeldingen of metadata te redigeren?**  
A: De SDK biedt de klassen `ImageRedaction` en `MetadataRedaction` voor die scenario’s.

**V: Hoe ga ik om met grote documenten (honderden MB)?**  
A: Verwerk ze in delen of gebruik de streaming‑API om de geheugenvoetafdruk te verkleinen; de engine kan bestanden tot 2 GB verwerken zonder het volledige bestand in RAM te laden.

**V: Welk licentiemodel is vereist voor commercieel gebruik?**  
A: Een betaalde licentie is vereist voor productie‑implementaties; een proeflicentie is voldoende voor ontwikkeling en testen.

## Conclusie

Je hebt nu een compleet, herbruikbaar **redactiebeleid** dat je op elk document kunt toepassen met GroupDocs.Redaction voor .NET. Door het beleid naar XML te exporteren, vereenvoudig je toekomstige updates en zorg je voor consistente gegevensbescherming binnen je organisatie.

### Volgende stappen
- Experimenteer met extra redactie‑typen zoals `ImageRedaction` of `MetadataRedaction`.  
- Integreer de logica voor het laden van het beleid in je document‑beheerworkflow voor geautomatiseerde redactie.  
- Verken de **GroupDocs.Redaction**‑API‑referentie voor geavanceerde aanpassingen.

---

**Laatst bijgewerkt:** 2026-10-06  
**Getest met:** GroupDocs.Redaction 5.8 voor .NET  
**Auteur:** GroupDocs  

**Bronnen**  
- [Documentatie](https://docs.groupdocs.com/redaction/net/)  
- [API‑referentie](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Gratis ondersteuningsforum](https://forum.groupdocs.com/c/redaction/33)  
- [Aanvraag tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/)

## Gerelateerde tutorials
- [Gevoelige gegevens redigeren met GroupDocs.Redaction .NET (C#)](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)
- [Documentredactie implementeren met GroupDocs.Redaction .NET&#58; Een stap‑voor‑stap gids](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
- [Hoe documenten te redigeren met GroupDocs.Redaction .NET – Een complete gids](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)