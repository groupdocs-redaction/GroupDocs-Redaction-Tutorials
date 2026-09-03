---
date: '2026-07-06'
description: Leer hoe je documenten .net kunt redigeren met streams met GroupDocs.Redaction.
  Deze tutorial behandelt de installatie, het laden van een document vanuit een stream,
  het toepassen van redactie en veilig opslaan.
keywords:
- redact documents .net
- load document from stream
- GroupDocs.Redaction streams
schemas:
- author: GroupDocs
  dateModified: '2026-07-06'
  description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  headline: Redact documents .net using Streams – GroupDocs.Redaction Guide
  type: TechArticle
- description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  name: Redact documents .net using Streams – GroupDocs.Redaction Guide
  steps:
  - name: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Temporary License** – request a short‑term key for evaluation.'
    text: '**Temporary License** – request a short‑term key for evaluation.'
  - name: '**Full Purchase** – obtain a permanent license for production workloads.'
    text: '**Full Purchase** – obtain a permanent license for production workloads.'
  - name: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
    text: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
  - name: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
    text: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
  - name: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
    text: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
  - name: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
    text: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports over 70 formats—including PDF, DOCX, XLSX,
      PPTX, and HTML—when using stream‑based APIs.
    question: Which file formats can be processed with streams?
  - answer: Yes, call `redactor.GetRedactedDocument()` to obtain an in‑memory representation
      that you can render or inspect programmatically.
    question: Can I preview redactions before saving?
  - answer: Supply the password when opening the stream via `Redactor` overloads that
      accept `LoadOptions` containing the password.
    question: How does the library handle password‑protected files?
  - answer: The engine can process files up to 2 GB; larger files should be split
      or processed in chunks to stay within memory limits.
    question: Is there a limit on document size?
  - answer: A single license key can be used across multiple environments as long
      as the usage complies with the licensing agreement.
    question: Do I need a separate license for each deployment environment?
  type: FAQPage
title: Documenten redigeren .net met Streams – GroupDocs.Redaction-gids
type: docs
url: /nl/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/
weight: 1
---

# Documenten redigeren .net met Streams – Een uitgebreide gids

Welkom! In deze tutorial ontdek je hoe je **redact documents .net** veilig kunt uitvoeren door streams te gebruiken met GroupDocs.Redaction. We lopen alles door wat je nodig hebt – van het installeren van de bibliotheek, het laden van een document vanuit een stream, het toepassen van precieze redactioneringen, tot het opslaan van het resultaat zonder tijdelijke bestanden op schijf achter te laten.

## Snelle antwoorden
- **Welke bibliotheek verwerkt redaction in .NET?** GroupDocs.Redaction for .NET.  
- **Kan ik een bestand direct vanuit een stream laden?** Yes—use `FileStream` with the Redactor constructor.  
- **Welke formaten worden ondersteund?** Over 70 input and output formats, including PDF, DOCX, XLSX, PPTX.  
- **Heb ik een licentie nodig voor productie?** A valid GroupDocs.Redaction license is required for non‑trial use.  
- **Is het veilig voor grote bestanden?** Stream‑based processing avoids loading the whole file into memory, enabling handling of multi‑gigabyte documents.

## Wat is “redact documents .net”?
**“Redact documents .net”** verwijst naar het proces van het permanent verwijderen of maskeren van gevoelige inhoud uit bestanden met behulp van .NET‑bibliotheken zoals GroupDocs.Redaction. Dit zorgt ervoor dat vertrouwelijke gegevens nooit in platte tekst je systeem verlaten. Het wordt vaak gebruikt in de juridische, financiële en gezondheidszorgsectoren om te voldoen aan privacy‑regelgeving zoals GDPR en HIPAA, en zorgt ervoor dat gevoelige gegevens niet kunnen worden hersteld na verwerking.

## Waarom streams gebruiken voor redaction?
GroupDocs.Redaction ondersteunt **70+ bestandsformaten** en kan bestanden tot **2 GB** verwerken zonder ze volledig in het geheugen te laden. Streaming vermindert I/O‑overhead, verbetert de prestaties en sluit aan bij beveiligingsbest practices door gegevens alleen gedurende de korte tijd dat ze nodig zijn voor transformatie in het geheugen te houden.

## Voorvereisten
- **GroupDocs.Redaction for .NET** – installeer via NuGet (zie hieronder).  
- **.NET 6+** (of .NET Framework 4.6.1+).  
- Visual Studio 2022 of een compatibele IDE.  
- Basiskennis van C# en vertrouwdheid met .NET‑streams.

## GroupDocs.Redaction installeren
Je kunt het pakket toevoegen met een van deze commando's:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

Of zoek “GroupDocs.Redaction” in de NuGet Package Manager UI en klik op **Install**.

### Stappen voor licentie‑acquisitie
1. **Free Trial** – download een proefversie van [GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
2. **Temporary License** – vraag een kort‑lopende sleutel aan voor evaluatie.  
3. **Full Purchase** – verkrijg een permanente licentie voor productie‑workloads.

Na installatie initialiseert u de bibliotheek in uw code:

```csharp
using GroupDocs.Redaction;
// Initialization code here...
```  

## Hoe een document laden vanuit een stream?
Een `FileStream` biedt een stream voor het lezen van en schrijven naar een bestand op schijf. De `Redactor`‑klasse verwerkt het document en past redaction‑regels toe. Laad je bronbestand in een `FileStream` en geef vervolgens de stream door aan de `Redactor`‑constructor. Deze aanpak voorkomt dat het originele bestand naar een tijdelijke locatie wordt geschreven en houdt de gegevens alleen in het geheugen gedurende de verwerking. Deze methode werkt voor elk ondersteund formaat, inclusief PDF‑s en Office‑documenten.

```csharp
// Directly open the source file as a read‑only stream
using var inputStream = new FileStream(inputPath, FileMode.Open, FileAccess.Read);
```

## Hoe de Redactor initialiseren met de stream?
De `Redactor`‑klasse is de kernengine die documentinhoud bewerkt. Door de invoer‑stream te leveren, maak je in‑memory redaction mogelijk zonder tussenliggende bestanden. Na het aanmaken van de instantie kun je redaction‑regels ketenen, wijzigingen previewen en opties configureren zoals rasterisatie of encryptie voordat je het uiteindelijke document commit.

```csharp
// Initialise the Redactor with the input stream
using var redactor = new GroupDocs.Redaction.Redactor(inputStream);
```

**Definition anchor:** `GroupDocs.Redaction.Redactor` is de primaire klasse die methoden biedt om redaction‑operaties toe te passen, te previewen en te committen op een document geladen vanuit een stream.

## Hoe redactions toepassen?
Je kunt meerdere redaction‑acties toevoegen; het voorbeeld hieronder verwijdert alle annotaties, wat een veelvoorkomende eis is voor het verwijderen van verborgen opmerkingen of reviewer‑notities. Extra redaction‑typen zoals `DeleteTextRedaction` of `ReplaceTextRedaction` kunnen worden gecombineerd om specifieke strings, data of patronen in het document te verwijderen of te maskeren.

```csharp
// Apply a predefined redaction that removes every annotation
redactor.Apply(new DeleteAnnotationRedaction());
```

**Definition anchor:** `DeleteAnnotationRedaction` is een ingebouwde redaction‑regel die annotatie‑objecten zoals opmerkingen, markeringen en stempels permanent verwijdert uit het document.

## Hoe het geredigeerde document opslaan?
Direct opslaan naar een `FileStream` zorgt ervoor dat de output in één keer wordt geschreven, waardoor onnodige tijdelijke bestanden worden geëlimineerd. Je kunt ook het uitvoerformaat, compressieniveau en optionele wachtwoordbeveiliging opgeven via het `SaveOptions`‑object om aan beveiligingseisen te voldoen. Sluit tenslotte de output‑stream om bestands‑handles vrij te maken en ervoor te zorgen dat het bestand volledig naar schijf is geschreven.

```csharp
// Prepare the output stream for the redacted file
using var outputStream = new FileStream(outputPath, FileMode.Create, FileAccess.Write);

// Save the modified document; RasterizationOptions disabled to keep text editable
redactor.Save(outputStream, new SaveOptions { RasterizationOptions = null });
```

**Definition anchor:** `SaveOptions` stelt je in staat te bepalen hoe het document wordt opgeslagen, inclusief rasterisatie, encryptie en formaatselectie.

## Veelvoorkomende gebruikssituaties
- **Legal document handling:** Verwijder vertrouwelijke annotaties voordat concepten met klanten worden gedeeld.  
- **GDPR compliance:** Verwijder persoonlijke identificatoren uit contracten of personeelsdossiers.  
- **Internal audit reports:** Verberg reviewer‑notities terwijl de kerninhoud voor distributie behouden blijft.

## Prestatietips voor grote bestanden
1. **Dispose streams promptly** – `using`‑statements sluiten streams automatisch, waardoor geheugen wordt vrijgemaakt.  
2. **Batch processing** – Loop door een verzameling bestanden en hergebruik een enkele `Redactor`‑instantie wanneer het formaat dit toestaat, waardoor toewijzings‑overhead wordt verminderd.

## Probleemoplossing
1. **File access denied** – Controleer of het account van de applicatie lees‑/schrijfrechten heeft op de doelmappen.  
2. **Redaction not applied** – Zorg ervoor dat het gekozen redaction‑type compatibel is met het documentformaat (bijv. `DeleteAnnotationRedaction` werkt voor PDF en DOCX).

## Veelgestelde vragen
**Q: Welke bestandsformaten kunnen met streams worden verwerkt?**  
A: GroupDocs.Redaction ondersteunt meer dan 70 formaten—waaronder PDF, DOCX, XLSX, PPTX en HTML—bij gebruik van stream‑gebaseerde API's.

**Q: Kan ik redactions previewen voordat ik opsla?**  
A: Ja, roep `redactor.GetRedactedDocument()` aan om een in‑memory representatie te verkrijgen die je programmatisch kunt renderen of inspecteren.

**Q: Hoe gaat de bibliotheek om met wachtwoord‑beveiligde bestanden?**  
A: Geef het wachtwoord op bij het openen van de stream via `Redactor`‑overloads die `LoadOptions` accepteren met het wachtwoord.

**Q: Is er een limiet op de documentgrootte?**  
A: De engine kan bestanden tot 2 GB verwerken; grotere bestanden moeten worden opgesplitst of in delen worden verwerkt om binnen de geheugenlimieten te blijven.

**Q: Heb ik een aparte licentie nodig voor elke implementatie‑omgeving?**  
A: Een enkele licentiesleutel kan worden gebruikt in meerdere omgevingen zolang het gebruik voldoet aan de licentieovereenkomst.

## Conclusie
Je hebt nu een volledige, stap‑voor‑stap oplossing voor **redact documents .net** met streams en GroupDocs.Redaction. Door bestanden direct vanuit streams te laden, gerichte redactions toe te passen en op te slaan zonder tussenliggende artefacten, bereik je zowel beveiliging als prestaties. Verken extra redaction‑typen — zoals tekstvervanging of metadata‑verwijdering — om het proces af te stemmen op jouw specifieke compliance‑behoeften.

---

**Laatst bijgewerkt:** 2026-07-06  
**Getest met:** GroupDocs.Redaction 5.0 for .NET  
**Auteur:** GroupDocs  

## Bronnen
- [Documentatie](https://docs.groupdocs.com/redaction/net/)
- [API-referentie](https://reference.groupdocs.com/redaction/net)
- [Download](https://releases.groupdocs.com/redaction/net/)
- [Gratis ondersteuningsforum](https://forum.groupdocs.com/c/redaction/33)
- [Tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/)

```csharp
string sourceFile = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "sample.docx");
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    // Proceed with document processing...
}
```

```csharp
using (var redactor = new GroupDocs.Redaction.Redactor(stream))
{
    // Apply redactions...
}
```

```csharp
redactor.Apply(new GroupDocs.Redaction.Redactions.DeleteAnnotationRedaction());
```

```csharp
string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "redacted_sample.docx");
using (Stream streamOut = File.Open(outputFile, FileMode.Create, FileAccess.Write))
{
    redactor.Save(streamOut, new GroupDocs.Redaction.Options.RasterizationOptions { Enabled = false });
}
```

## Gerelateerde tutorials
- [Hoe documenten laden en redigeren met GroupDocs.Redaction .NET&#58; Een volledige gids](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Documenten redigeren en opslaan met GroupDocs.Redaction voor .NET&#58; Een volledige gids](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Hoe documentmetadata extraheren uit streams met GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)