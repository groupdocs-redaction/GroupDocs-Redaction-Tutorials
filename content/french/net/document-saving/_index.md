---
date: 2026-06-11
description: Apprenez à exporter des fichiers censurés, à configurer les dossiers
  de sortie, à créer des PDF rasterisés et à enregistrer dans des flux en utilisant
  GroupDocs.Redaction pour .NET.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: Comment exporter des documents censurés avec GroupDocs.Redaction .NET
type: docs
url: /fr/net/document-saving/
weight: 3
---

# Comment exporter des documents expurgés avec GroupDocs.Redaction .NET

Dans ce guide complet, vous découvrirez **comment exporter du contenu expurgé** en toute sécurité et efficacité en utilisant GroupDocs.Redaction pour .NET. Que vous ayez besoin de conserver le type de fichier d'origine, de verrouiller le document sous forme de PDF rasterisé, ou de diffuser le résultat directement en mémoire, nous vous accompagnons à travers chaque option avec des explications claires, conversationnelles et des conseils pratiques. À la fin de ce tutoriel, vous serez capable de choisir la bonne stratégie d'exportation pour tout scénario axé sur la conformité.

## Réponses rapides
- **Quels formats puis‑je exporter ?** N'importe lequel des plus de 30 formats natifs pris en charge par GroupDocs.Redaction, plus le PDF rasterisé pour une sécurité maximale.  
- **Ai‑je besoin d'une licence pour le streaming ?** Oui, une licence valide de GroupDocs.Redaction est requise pour le streaming en production.  
- **Puis‑je définir un dossier de sortie personnalisé ?** Absolument – utilisez la propriété `OutputPath` ou `SaveOptions` pour le configurer.  
- **La rasterisation est‑elle sûre pour les gros fichiers ?** Elle gère les documents jusqu'à 500 pages sans charger le fichier complet en mémoire.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Qu’est‑ce que GroupDocs.Redaction ?
GroupDocs.Redaction est une bibliothèque .NET qui supprime ou masque programmatiquement les informations sensibles des PDF, Word, Excel, PowerPoint, images et de nombreux autres formats. Elle propose une API de haut niveau pour définir les zones d'expurgation, appliquer des politiques, et finalement exporter le document nettoyé. Cela facilite l'intégration des capacités d'expurgation dans toute application .NET.

## Pourquoi exporter les documents expurgés en PDF rasterisés ?
Les PDF rasterisés convertissent chaque page en une image plate, éliminant les couches de texte cachées qui pourraient être extraites ultérieurement. Ce format garantit que le contenu expurgé ne peut pas être récupéré, répondant aux normes réglementaires strictes telles que le RGPD et la HIPAA. GroupDocs.Redaction peut produire des PDF rasterisés jusqu'à 300 dpi, préservant la fidélité visuelle tout en assurant la sécurité.

## Comment exporter les documents expurgés ?
Chargez le fichier source, appliquez vos règles d'expurgation, puis appelez la méthode d'enregistrement appropriée — soit `Save` pour le format original, `SaveAsRasterizedPdf` pour les PDF uniquement image, ou `SaveToStream` pour la gestion en mémoire. Vous trouverez ci‑dessous le flux de travail étape par étape. Chaque méthode garantit que le contenu expurgé est définitivement supprimé tout en conservant le format de sortie souhaité.

### Étape 1 : Installer le package NuGet
Ajoutez le dernier package GroupDocs.Redaction à votre projet :

```bash
dotnet add package GroupDocs.Redaction
```

### Étape 2 : Charger le document et définir les expurgations
Créez une instance `Redactor`, chargez le fichier et spécifiez les zones que vous souhaitez masquer. La classe `Redactor` fournit la fonctionnalité principale pour charger les documents et appliquer les règles d'expurgation.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Étape 3 : Choisir la méthode d'exportation
#### Exporter au format original
```csharp
redactor.Save("RedactedReport.docx");
```

#### Exporter en PDF rasterisé
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Exporter vers un flux mémoire (idéal pour les API web)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

La méthode `Save` écrit le document expurgé dans un fichier au format original. `SaveAsRasterizedPdf` crée un PDF où chaque page est rendue comme une image, supprimant tout texte caché. `SaveToStream` renvoie le fichier expurgé sous forme de flux mémoire, adapté aux réponses web.

## Comment configurer un dossier de sortie ?
Définissez la propriété `OutputPath` sur le `Redactor` ou transmettez un objet `SaveOptions` personnalisé incluant le répertoire souhaité. `OutputPath` est une propriété du `Redactor` qui spécifie le répertoire où les fichiers de sortie sont écrits. `SaveOptions` vous permet de personnaliser divers paramètres d'enregistrement, y compris le dossier de sortie. Cela garantit que tous les fichiers exportés atterrissent dans un emplacement prévisible, simplifiant les pipelines de traitement par lots. Vous pouvez également spécifier des sous‑dossiers par type de document pour garder votre espace de travail organisé.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Problèmes courants et solutions
- **Expurgation non appliquée :** Vérifiez que le motif de recherche correspond exactement au texte du document ; utilisez `RegexOptions.IgnoreCase` si nécessaire. `RegexOptions` est une énumération qui contrôle le comportement de correspondance des expressions régulières, comme la sensibilité à la casse.  
- **Les gros fichiers provoquent une pression mémoire :** Activez le mode streaming en utilisant `SaveToStream` et évitez d’appeler `Save` sur le document complet.  
- **Le PDF rasterisé apparaît flou :** Augmentez le DPI dans `RasterizationOptions` (par ex., 300–600) pour améliorer la qualité de l'image. `RasterizationOptions` vous permet de définir des paramètres tels que le DPI et le format d'image pour la sortie PDF rasterisée.

## Questions fréquemment posées

**Q : Puis‑je exporter vers un format qui n’était pas initialement pris en charge ?**  
R : Oui, GroupDocs.Redaction peut convertir la plupart des types d’entrée en PDF, DOCX, XLSX, PPTX ou PDF rasterisé, couvrant plus de 30 formats.

**Q : Comment la rasterisation protège‑t‑elle les données expurgées ?**  
R : En rendant chaque page sous forme d'image plate, toutes les couches de texte cachées sont supprimées, rendant impossible l'extraction du contenu original.

**Q : Est‑il possible de chaîner plusieurs règles d'expurgation ?**  
R : Absolument – vous pouvez appeler `Apply` à plusieurs reprises ou transmettre une collection de `RedactionOptions` pour traiter de nombreux motifs en une seule passe. `RedactionOptions` définit les paramètres d'une opération d'expurgation unique, comme la région et le type de remplacement.

**Q : Dois‑je fermer l’objet Redactor ?**  
R : Le `Redactor` implémente `IDisposable` ; encapsulez‑le dans un bloc `using` ou appelez `Dispose()` pour libérer rapidement les poignées de fichiers. `IDisposable` est une interface qui fournit un mécanisme de libération des ressources non gérées.

**Q : Quels runtimes .NET sont officiellement testés ?**  
R : GroupDocs.Redaction est validé sur .NET Framework 4.6+, .NET Core 3.1+, et .NET 5/6/7.

## Ressources supplémentaires

### Tutoriels disponibles

- [Comment enregistrer des documents en PDF rasterisés avec GroupDocs.Redaction pour .NET : Guide complet](./groupdocs-redaction-net-rasterized-pdfs/)
- [Implémentation du répertoire de sortie en .NET avec GroupDocs.Redaction : Guide complet](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Expurger et enregistrer des documents avec GroupDocs.Redaction pour .NET : Guide complet](./redact-save-documents-groupdocs-redaction-net/)
- [Enregistrer les documents expurgés au format original avec GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Expurgation sécurisée de documents en .NET avec des flux : Guide pour GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Liens utiles

- [Documentation GroupDocs.Redaction pour .NET](https://docs.groupdocs.com/redaction/net/)
- [Référence API GroupDocs.Redaction pour .NET](https://reference.groupdocs.com/redaction/net/)
- [Télécharger GroupDocs.Redaction pour .NET](https://releases.groupdocs.com/redaction/net/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Support gratuit](https://forum.groupdocs.com/)
- [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)

---

**Dernière mise à jour :** 2026-06-11  
**Testé avec :** GroupDocs.Redaction 23.11 pour .NET  
**Auteur :** GroupDocs  

---

## Tutoriels associés

- [Enregistrer les documents expurgés au format original avec GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Comment enregistrer des documents en PDF rasterisés avec GroupDocs.Redaction pour .NET : Guide complet](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Expurgation sécurisée de documents en .NET avec des flux : Guide pour GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)