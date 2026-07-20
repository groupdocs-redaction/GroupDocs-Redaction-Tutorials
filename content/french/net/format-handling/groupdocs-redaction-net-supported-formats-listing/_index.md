---
date: '2026-07-20'
description: Apprenez à répertorier les formats avec GroupDocs.Redaction .NET, intégrez
  cette fonctionnalité à votre flux de travail documentaire et améliorez les performances.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Découvrez comment répertorier les formats avec GroupDocs.Redaction
  .NET, consultez un guide étape par étape et obtenez des conseils pour des performances
  optimales dans vos applications .NET.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Comment répertorier les formats avec GroupDocs.Redaction .NET
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
title: Comment répertorier les formats avec GroupDocs.Redaction .NET
type: docs
url: /fr/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Comment répertorier les formats avec GroupDocs.Redaction .NET

Gérer une grande variété de types de documents est une réalité quotidienne pour les développeurs qui créent des applications centrées sur les documents. Dans ce tutoriel, vous apprendrez **comment répertorier les formats** que GroupDocs.Redaction .NET peut gérer, afin de pouvoir valider les fichiers avant le traitement, présenter aux utilisateurs des options précises et maintenir votre flux de travail efficace.

## Introduction

Une gestion efficace des documents commence par connaître exactement quels types de fichiers votre bibliothèque prend en charge. GroupDocs.Redaction fournit une méthode intégrée pour récupérer ces informations, vous permettant de créer des éléments d’interface dynamiques, d’appliquer des règles de validation et d’éviter les erreurs d’exécution. Vous trouverez ci‑dessous tout ce dont vous avez besoin pour démarrer, de l’installation aux extraits de code pratiques et aux conseils de performance.

### Réponses rapides
- **Que signifie « comment répertorier les formats » ?** Il s'agit de récupérer la collection d'extensions de fichiers que GroupDocs.Redaction peut traiter.  
- **Ai‑je besoin d’une licence ?** Oui, une licence valide de GroupDocs.Redaction est requise pour une utilisation en production.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Combien de formats sont disponibles ?** Plus de 30 formats d’entrée et de sortie sont pris en charge immédiatement.  
- **Une configuration spéciale est‑elle nécessaire ?** Aucune configuration supplémentaire n’est requise au‑delà de l’initialisation standard de la bibliothèque.

## Qu'est‑ce que « comment répertorier les formats » ?

Cela consiste à appeler l’API FileType de la bibliothèque pour obtenir une collection où chaque entrée contient l’extension du fichier et un nom lisible par l’homme. Les développeurs peuvent ensuite parcourir cette collection pour créer des règles de validation, remplir des listes déroulantes UI ou consigner les types pris en charge, garantissant que seuls les documents compatibles sont traités.

## Pourquoi répertorier les formats avec GroupDocs.Redaction ?

GroupDocs.Redaction prend en charge **plus de 30** types de fichiers distincts — y compris PDF, DOCX, PPTX et les formats d’image — vous permettant de gérer la plupart des documents d’entreprise sans convertisseurs tiers. En listant ces formats de façon programmatique, vous éliminez les approximations, réduisez les tickets de support et assurez que seuls les fichiers compatibles entrent dans votre pipeline de traitement.

## Prérequis

- **GroupDocs.Redaction for .NET** – téléchargez le dernier package depuis le site officiel.  
- **.NET Framework ou .NET Core** – compatible avec votre environnement de développement.  
- **Visual Studio** (ou tout IDE compatible C#).  
- Familiarité de base avec la syntaxe C#.

## Configuration de GroupDocs.Redaction pour .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Gestionnaire de packages
`Install-Package GroupDocs.Redaction`

### Interface utilisateur du gestionnaire de packages NuGet
- Recherchez **« GroupDocs.Redaction »** et installez la version la plus récente.

### Acquisition de licence
GroupDocs propose un essai gratuit, une licence temporaire pour l’évaluation ou des options d’achat complet. Visitez le site Web de GroupDocs pour obtenir le fichier de licence approprié.

### Initialisation et configuration de base
Après avoir ajouté le package, référencez l’espace de noms et créez une instance `Redactor` :

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Guide d'implémentation

### Comment répertorier les formats avec GroupDocs.Redaction .NET ?
Chargez la bibliothèque, appelez l’aide statique et triez les résultats — cela vous fournit une collection prête à l’emploi en seulement deux lignes de code. Utilisez `FileType.GetSupportedFileFormats()` pour récupérer un `IEnumerable<FileType>` contenant l’extension et le nom affiché de chaque format, puis triez par extension pour obtenir une liste UI propre.

### Récupération des formats de fichiers pris en charge

#### Vue d'ensemble
L’objectif est d’obtenir une liste des types de fichiers que GroupDocs.Redaction peut gérer, facilitant l’intégration dans la logique de validation, les listes déroulantes UI ou les mécanismes de journalisation.

#### Implémentation étape par étape

**1. Récupérer les types de fichiers pris en charge**  
`FileType.GetSupportedFileFormats()` renvoie chaque format reconnu par la bibliothèque. La méthode fait partie de la classe `GroupDocs.Redaction.FileType`, qui encapsule des métadonnées telles que l’extension du fichier et le nom convivial.

**2. Afficher les types de fichiers pris en charge**  
Parcourez la collection et affichez l’extension et la description de chaque format. Exemple de code en ligne :

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

L’extrait affiche une liste ordonnée comme « .pdf – Portable Document Format », idéale pour remplir des éléments d’interface utilisateur.

### Conseils de dépannage
- **Package manquant** – Vérifiez la référence du package NuGet et restaurez les packages si nécessaire.  
- **Chemin de licence incorrect** – Assurez‑vous que le fichier de licence est copié dans le répertoire de sortie ou fournissez un chemin absolu.  
- **Extension non prise en charge** – Si un format n’apparaît pas, confirmez que vous utilisez la dernière version de la bibliothèque ; les versions plus récentes ajoutent des formats supplémentaires.

## Applications pratiques
Comprendre les formats pris en charge ouvre plusieurs scénarios réels :

1. **Systèmes de gestion de documents** – Validez les téléchargements par rapport à la liste prise en charge pour éviter les échecs de traitement.  
2. **Sécurité du contenu** – Appliquez les règles de rédaction uniquement aux types de fichiers que le moteur peut modifier en toute sécurité.  
3. **Pipelines de traitement par lots** – Filtrez de gros lots de fichiers avant d’appeler la rédaction, économisant CPU et mémoire.

## Considérations de performance
- **Empreinte mémoire** – Lister les formats est une opération légère ; aucun document n’est chargé en mémoire.  
- **Opérations par lots** – Lors du traitement de centaines de fichiers, récupérez la liste des formats une fois et réutilisez‑la pour éviter les appels redondants.  
- **Sécurité des threads** – `FileType.GetSupportedFileFormats()` est thread‑safe et peut être appelé depuis des tâches parallèles sans synchronisation.

## Conclusion
Vous disposez maintenant d’une approche complète et prête pour la production afin de **répertorier les formats** avec GroupDocs.Redaction .NET. En intégrant cette fonctionnalité, vous améliorez la validation, l’expérience utilisateur et la robustesse de vos pipelines de documents.

### Prochaines étapes
- Explorez l’API `Redactor` pour appliquer des règles de rédaction en fonction du type de fichier.  
- Combinez la liste des formats avec un menu déroulant front‑end pour une sélection de fichiers fluide.  
- Consultez le guide de performance pour optimiser les travaux par lots à grande échelle.

## Questions fréquentes

**Q : Puis‑je récupérer la liste des formats sans initialiser une instance Redactor ?**  
R : Oui, `FileType.GetSupportedFileFormats()` est statique et ne nécessite pas d’objet `Redactor`.

**Q : La liste comprend‑elle les formats d’entrée et de sortie ?**  
R : La méthode renvoie tous les formats que la bibliothèque peut lire et écrire ; chaque `FileType` possède un indicateur `CanRead` et `CanWrite`.

**Q : À quelle fréquence la liste des formats pris en charge est‑elle mise à jour ?**  
R : GroupDocs publie des mises à jour de formats avec chaque version de la bibliothèque ; vérifier la liste à l’exécution garantit que vous disposez toujours du jeu le plus récent.

**Q : Existe‑t‑il un moyen de filtrer uniquement les formats compatibles PDF ?**  
R : Oui, filtrez la collection où `format.Extension == ".pdf"` ou où `format.Name.Contains("PDF")`.

**Q : Cette approche fonctionnera‑t‑elle sur .NET Core 2.1 ?**  
R : La méthode nécessite .NET Core 3.1 ou ultérieur ; les runtimes antérieurs ne sont pas pris en charge.

## Section FAQ
1. **Comment installer GroupDocs.Redaction pour .NET ?**  
   Utilisez la commande CLI `dotnet add package GroupDocs.Redaction` ou installez via l’interface du gestionnaire de packages NuGet.  

2. **Quels sont les problèmes courants lors de la récupération des formats pris en charge ?**  
   Assurez‑vous que toutes les dépendances sont restaurées et que vous référencez le bon espace de noms (`GroupDocs.Redaction`).  

3. **Puis‑je utiliser cette fonctionnalité avec des applications non‑.NET ?**  
   Ce tutoriel se concentre sur .NET, mais GroupDocs propose des API similaires pour Java, Python et d’autres plateformes.  

4. **Comment optimiser les performances lors de l’utilisation de GroupDocs.Redaction ?**  
   Réutilisez la liste des formats, évitez de charger des documents complets lorsque seule la compatibilité est vérifiée, et surveillez l’utilisation de la mémoire pendant les traitements par lots.  

5. **Quels types de fichiers GroupDocs.Redaction prend‑il en charge ?**  
   La bibliothèque prend en charge plus de 30 formats, dont PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG et bien d’autres. Utilisez `FileType.GetSupportedFileFormats()` pour afficher la liste complète.

## Ressources
- [Documentation](https://docs.groupdocs.com/redaction/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

**Dernière mise à jour :** 2026-07-20  
**Testé avec :** GroupDocs.Redaction 4.2.0 for .NET  
**Auteur :** GroupDocs  

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

## Tutoriels associés

- [Format Handling Tutorials for GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Document Loading Tutorials with GroupDocs.Redaction for .NET](/redaction/net/document-loading/)
- [Document Saving Tutorials for GroupDocs.Redaction .NET](/redaction/net/document-saving/)