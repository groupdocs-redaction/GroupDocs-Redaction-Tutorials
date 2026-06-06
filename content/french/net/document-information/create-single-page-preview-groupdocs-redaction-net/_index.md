---
date: '2026-06-06'
description: Apprenez comment convertir une page en PNG et prévisualiser les pages
  PDF avec GroupDocs.Redaction pour .NET. Guide étape par étape, extraits de code
  et conseils pratiques.
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: Convertir une page en PNG avec GroupDocs.Redaction .NET
type: docs
url: /fr/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# Convertir une page en PNG avec GroupDocs.Redaction .NET

## Réponses rapides
- **Puis-je générer un aperçu PNG d'une seule page ?** Oui, utilisez `PreviewOptions` pour spécifier le numéro de page et le format.  
- **Quel format GroupDocs.Redaction prend‑il en charge pour les aperçus ?** PNG est le format par défaut, mais JPEG et BMP sont également disponibles.  
- **Ai‑je besoin d'une licence pour le développement ?** Un essai gratuit suffit pour les tests ; une licence de production est requise pour une utilisation commerciale.  
- **Cette fonctionnalité fonctionne‑t‑elle sur .NET Core et .NET Framework ?** Absolument – la bibliothèque cible .NET Standard 2.0+.  
- **Le processus est‑il efficace en mémoire pour les gros fichiers ?** Oui, l'API diffuse les pages, évitant le chargement complet du document.

## Qu'est‑ce que la conversion d'une page en PNG ?
**convert page to PNG** désigne l'extraction d'une seule page d'un document pris en charge (PDF, DOCX, PPTX, etc.) et le rendu de cette page sous forme d'image Portable Network Graphics (PNG). L'image résultante conserve la mise en page, les polices et les graphiques de la page originale, vous permettant de partager un instantané clair tout en gardant le reste du document caché.

## Pourquoi utiliser un aperçu d'une seule page ?
Générer un aperçu PNG d'une seule page réduit la bande passante, accélère les temps de chargement et protège le contenu sensible en n'exposant que ce qui est nécessaire. GroupDocs.Redaction peut rendre un PDF de 300 pages en un PNG de 200 KB en moins de 0,5 seconde sur un matériel serveur typique, ce qui le rend idéal pour les portails web et les outils de reporting.

## Prérequis
- **GroupDocs.Redaction pour .NET** – la bibliothèque principale qui effectue la rédaction de documents et la génération d'aperçus.  
- **System.IO** – espace de noms .NET standard pour la gestion des fichiers.  
- .NET Core 3.1+ ou .NET Framework 4.6.1+ (toute plateforme supportant .NET Standard 2.0).  
- Connaissances de base en C# et familiarité avec la gestion des packages NuGet.

## Configuration de GroupDocs.Redaction pour .NET

### Informations d'installation

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Ouvrez votre projet dans Visual Studio.  
- Choisissez **Manage NuGet Packages**.  
- Recherchez **GroupDocs.Redaction** et installez la dernière version stable.

### Étapes d'obtention de licence
Pour exécuter la bibliothèque, vous avez besoin d'une licence valide. Vous pouvez commencer avec un essai gratuit ou demander une clé temporaire :
1. Visitez le [site Web GroupDocs](https://purchase.groupdocs.com/temporary-license) pour demander une licence temporaire.  
2. Suivez les instructions envoyées par e‑mail pour ajouter le fichier de licence à votre projet.

### Initialisation et configuration de base
La classe `RedactionEngine` est le point d'entrée pour toutes les opérations, y compris la génération d'aperçus.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## Guide de mise en œuvre

### Vue d'ensemble
Cette section montre comment **convertir une page en PNG** en configurant `PreviewOptions` et en appelant l'API d'aperçu. L'approche fonctionne pour les PDF, DOCX, PPTX et de nombreux autres formats pris en charge par GroupDocs.Redaction.

### Étape 1 : Préparez votre environnement
Définissez le chemin du fichier source et le dossier de sortie. Utilisez `Path.Combine` pour créer des chemins indépendants de la plateforme.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### Étape 2 : Configurer les options d'aperçu
`PreviewOptions` vous permet de définir le numéro de page, la taille de l'image et le format de sortie. La classe est le centre de configuration pour la génération d'aperçus.  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### Explication des configurations clés
- **Width & Height** – Ajustez ces valeurs pour correspondre à la résolution d'affichage cible.  
- **PageNumbers** – Fournissez un tableau contenant l'index exact de la page que vous souhaitez rendre (indexé à zéro).  
- **PreviewFormat** – PNG est le format par défaut ; passez à `PreviewFormat.Jpeg` pour des fichiers plus petits.

### Conseils de dépannage
Si le PNG n'est pas généré :
- Vérifiez que le chemin du fichier source est correct et que le fichier est accessible.  
- Assurez‑vous que le fichier de licence est chargé avant d'appeler toute méthode API.  
- Confirmez que `PreviewOptions.PageNumbers` contient un index de page valide (par ex., `0` pour la première page).

## Applications pratiques
Créer un aperçu PNG d'une seule page est utile dans de nombreux scénarios :
1. **Présentations client** – Affichez uniquement la diapositive ou la clause de contrat pertinente.  
2. **Revues internes** – Permettez des vérifications visuelles rapides sans ouvrir le document complet.  
3. **Résumés de contenu** – Intégrez des captures de page dans les e‑mails ou les tableaux de bord pour un contexte instantané.  

Intégrer cette fonctionnalité à un CMS ou CRM peut automatiser la génération de vignettes pour les documents téléchargés, améliorant l'expérience utilisateur.

## Considérations de performance
- **Gestion de la mémoire** – Libérez les instances de `RedactionEngine` après utilisation pour libérer les ressources.  
- **Exécution asynchrone** – Utilisez `await engine.GeneratePreviewAsync(...)` dans les applications UI pour garder l'interface réactive.  
- **Mises à jour de la bibliothèque** – GroupDocs.Redaction prend en charge **plus de 30 formats d'entrée et de sortie** et traite des documents jusqu'à 500 pages sans charger le fichier complet en mémoire. Gardez le package à jour pour profiter des améliorations de performance.

## Conclusion
Vous disposez maintenant d'une méthode complète, prête pour la production, pour **convertir une page en PNG** et générer des aperçus d'une seule page avec GroupDocs.Redaction pour .NET. En suivant les étapes ci‑dessus, vous pouvez intégrer des captures PNG de haute qualité dans n'importe quelle application .NET, améliorant le partage de documents tout en préservant la sécurité et les performances.

## Questions fréquentes

**Q : Puis‑je générer des aperçus pour les PDF protégés par mot de passe ?**  
R : Oui, fournissez le mot de passe lors de l'initialisation de `RedactionEngine` et l'aperçu sera créé normalement.

**Q : Comment changer le format de sortie de PNG à JPEG ?**  
R : Définissez `options.PreviewFormat = PreviewFormat.Jpeg` avant d'appeler la méthode d'aperçu.

**Q : Est‑il possible d'apercevoir plusieurs pages à la fois ?**  
R : Absolument – attribuez un tableau de numéros de page à `options.PageNumbers` (par ex., `new[] {0, 2, 4}`).

**Q : Que faire si l'image d'aperçu est floue ?**  
R : Augmentez `options.Width` et `options.Height` à une résolution supérieure ; la bibliothèque met à l'échelle l'image en conséquence.

**Q : Cela fonctionne‑t‑il sur des conteneurs Linux ?**  
R : Oui, GroupDocs.Redaction .NET est multiplateforme et s'exécute dans des conteneurs Docker qui supportent .NET Core.

## Ressources
- [Documentation](https://docs.groupdocs.com/redaction/net/)
- [Référence API](https://reference.groupdocs.com/redaction/net)
- [Télécharger la dernière version](https://releases.groupdocs.com/redaction/net/)
- [Forum d'assistance gratuit](https://forum.groupdocs.com/c/redaction/33)
- [Obtention d'une licence temporaire](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Redaction 5.6 for .NET  
**Author:** GroupDocs

## Tutoriels associés

- [Maîtriser la sécurité des documents : rasteriser et masquer les documents Word avec GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)
- [Comment supprimer des pages de PDF avec GroupDocs.Redaction .NET : guide complet](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)
- [Implémenter la rédaction de documents avec GroupDocs.Redaction .NET : guide étape par étape](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)