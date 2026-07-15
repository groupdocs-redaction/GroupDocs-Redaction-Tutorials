---
date: '2026-06-06'
description: Apprenez comment récupérer les metadata et extraire les metadata des
  documents en utilisant GroupDocs.Redaction .NET, permettant une gestion documentaire
  robuste et la conformité.
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: Comment récupérer les metadata avec l'API GroupDocs.Redaction .NET
type: docs
url: /fr/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# Comment récupérer les métadonnées avec GroupDocs.Redaction .NET

Dans l'ère numérique actuelle, **comment récupérer les métadonnées** d'un fichier est une étape fondamentale pour toute application centrée sur les documents. Que vous ayez besoin de lire les métadonnées d'un fichier pour des audits de conformité, d'extraire les propriétés du document pour l'indexation, ou simplement d'afficher la taille du document dans une interface utilisateur, GroupDocs.Redaction .NET vous offre une API concise pour le faire en quelques lignes de C#. Ce tutoriel vous guide à travers l'ensemble du processus, de la configuration de l'environnement à l'affichage des informations récupérées, afin que vous puissiez commencer à extraire les métadonnées du document immédiatement.

## Réponses rapides
- **Quelle est la méthode principale pour obtenir les métadonnées ?** Appelez `Redactor.GetDocumentInfo()` sur une instance `Redactor`.  
- **Quels formats sont pris en charge ?** Plus de 50 formats d'entrée et de sortie, y compris PDF, DOCX, XLSX, PPTX et les types d'images.  
- **Ai-je besoin d'une licence pour le développement ?** Une licence d'essai gratuite fonctionne pour les tests ; une licence complète est requise pour la production.  
- **Puis-je traiter de gros fichiers ?** Oui — GroupDocs.Redaction gère des documents de plusieurs centaines de pages sans charger le fichier complet en mémoire.  
- **Le support asynchrone est-il disponible ?** L'API peut être encapsulée dans des modèles async pour garder les threads UI réactifs.

## Qu'est-ce que la récupération des métadonnées dans GroupDocs.Redaction ?
La récupération des métadonnées est le processus d'accès aux propriétés intégrées d'un document — telles que le type de fichier, le nombre de pages et la taille — via l'API de la bibliothèque. En extrayant ces propriétés, les développeurs peuvent évaluer programmatiquement les caractéristiques du document, prendre en charge l'indexation, appliquer des règles de conformité et prendre des décisions éclairées concernant les étapes de traitement ultérieures.

## Comment récupérer les métadonnées d'un document ?
La classe `Redactor` est l'interface principale pour charger et inspecter les documents dans GroupDocs.Redaction.  
`GetDocumentInfo()` est une méthode qui renvoie un objet `DocumentInfo` contenant les métadonnées du document.

Chargez votre fichier avec `new Redactor("path/to/file")` et invoquez `GetDocumentInfo()` — l'appel renvoie un objet `DocumentInfo` contenant le type, le nombre de pages, la taille et d'autres propriétés. Cette approche en deux étapes fonctionne pour tout format pris en charge et ne nécessite aucune configuration supplémentaire. Vous pouvez ensuite lire des champs comme `FileType`, `PageCount` et `FileSize` pour afficher ou consigner les informations.

## Prérequis
- **GroupDocs.Redaction .NET** version 21.6 ou plus récente.  
- .NET Framework 4.7.2 +, .NET Core 3.1 +, ou .NET 5/6+.  
- Connaissances de base en C# et un IDE de développement (Visual Studio, Rider, etc.).

## Configuration de GroupDocs.Redaction pour .NET
Commencer avec GroupDocs.Redaction est simple. Installez le package en utilisant l'une des méthodes suivantes :

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

Ou, utilisez l'**interface utilisateur du gestionnaire de packages NuGet** : recherchez simplement « GroupDocs.Redaction » et cliquez sur **Install**.

### Acquisition de licence
Pour essayer GroupDocs.Redaction, vous pouvez obtenir une licence d'essai gratuite. Pour le développement continu ou l'utilisation en production, achetez une licence complète ou demandez une licence temporaire sur le site officiel.

Une fois installé, initialisez la bibliothèque comme suit :

```csharp
using GroupDocs.Redaction;
```

## Guide d'implémentation

### Fonctionnalité d'obtention des informations du document
Cette fonctionnalité se concentre sur l'extraction des métadonnées essentielles des documents à l'aide de GroupDocs.Redaction .NET. Suivez ces étapes :

#### Étape 1 : Préparez le chemin de votre document
Définissez le chemin absolu ou relatif vers le fichier cible :

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

Remplacez `YOUR_DOCUMENT_DIRECTORY` par le dossier contenant votre document.

#### Étape 2 : Initialise l'instance Redactor
Créez un objet `Redactor` qui fournit l'accès aux méthodes de métadonnées :

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### Étape 3 : Récupérez les informations du document
Appelez `GetDocumentInfo()` sur l'instance `Redactor` pour récupérer toutes les propriétés disponibles :

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

L'objet retourné comprend le type de fichier, le nombre de pages et la taille du fichier.

#### Étape 4 : Affichez les détails du document
Affichez les informations dans la console ou l'interface utilisateur. Le code d'exemple (commenté pour les exécutions autonomes) montre comment imprimer chaque propriété :

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### Pourquoi utiliser GroupDocs.Redaction pour l'extraction de métadonnées ?
GroupDocs.Redaction prend en charge **plus de 50 formats de fichiers** et peut traiter des documents jusqu'à **2 Go** tout en maintenant la consommation de mémoire sous **100 Mo** pour des charges de travail typiques. La bibliothèque extrait les métadonnées sans charger entièrement le document, offrant des réponses rapides — souvent moins de **200 ms** pour un PDF de 100 pages sur du matériel serveur standard.

### Problèmes courants et solutions
- **Chemin de fichier incorrect** – Vérifiez la chaîne du chemin et assurez-vous que le fichier est accessible au processus en cours d'exécution.  
- **Format non pris en charge** – Consultez la liste des formats ; si un format manque, envisagez de le convertir d'abord.  
- **Goulots d'étranglement de performance** – Pour des fichiers très volumineux, activez les options de streaming ou traitez les pages par lots afin de limiter l'utilisation de la mémoire.

## Applications pratiques
Comprendre les métadonnées d'un document permet plusieurs scénarios réels :

1. **Systèmes de gestion de documents (DMS)** – Automatisez la catégorisation et l'indexation en fonction du type, de la taille ou du nombre de pages.  
2. **Audit de conformité** – Vérifiez que les fichiers confidentiels contiennent les métadonnées requises avant l'archivage.  
3. **Migration de données** – Regroupez les fichiers par propriétés pour rationaliser les tâches de migration en masse.  

## Considérations de performance
- **Utilisation efficace des ressources** – Utilisez l'instance `Redactor` dans un bloc `using` pour garantir une libération correcte.  
- **Modèles asynchrones** – Enveloppez les appels de métadonnées dans `Task.Run` ou implémentez des wrappers async pour garder les threads UI réactifs dans les applications de bureau ou web.

## Questions fréquentes

**Q : Quels formats de documents puis-je extraire les métadonnées ?**  
R : GroupDocs.Redaction lit les métadonnées de plus de 50 formats, y compris PDF, DOCX, XLSX, PPTX, HTML et les types d'images courants.

**Q : Comment gérer les fichiers protégés par mot de passe ?**  
R : Passez le mot de passe au constructeur `Redactor` ; l'API déchiffrera le fichier avant d'extraire les métadonnées.

**Q : Existe-t-il une limite à la taille des fichiers que je peux traiter ?**  
R : Bien qu'il n'y ait pas de limite stricte, les fichiers supérieurs à 2 Go peuvent nécessiter un réglage supplémentaire de la mémoire ; les performances restent linéaires avec la taille du fichier.

**Q : Puis-je récupérer les métadonnées en opération batch ?**  
R : Oui — parcourez une collection de chemins de fichiers et appelez `GetDocumentInfo()` pour chacun ; la bibliothèque est thread‑safe pour l'exécution parallèle.

**Q : Ai-je besoin d'une licence pour les builds de développement ?**  
R : Une licence d'essai gratuite suffit pour le développement et les tests ; une licence commerciale est requise pour les déploiements en production.

## Ressources
- [Documentation](https://docs.groupdocs.com/redaction/net/)  
- [Référence API](https://reference.groupdocs.com/redaction/net)  
- [Téléchargement](https://releases.groupdocs.com/redaction/net/)  
- [Forum d'assistance gratuit](https://forum.groupdocs.com/c/redaction/33)  
- [Informations sur la licence temporaire](https://purchase.groupdocs.com/temporary-license/)

## Conclusion
Vous disposez maintenant d'un guide complet, étape par étape, sur **comment récupérer les métadonnées** à l'aide de GroupDocs.Redaction .NET. En exploitant la méthode `Redactor.GetDocumentInfo()`, vous pouvez rapidement lire les métadonnées du fichier, soutenir les flux de travail de conformité et améliorer tout pipeline de traitement de documents. Explorez les fonctionnalités supplémentaires de Redaction — telles que la rédaction de contenu, le filigrane et la conversion de documents — pour créer une solution de gestion de documents entièrement fonctionnelle.

---

**Dernière mise à jour :** 2026-06-06  
**Testé avec :** GroupDocs.Redaction .NET 21.6 (dernière version au moment de la rédaction)  
**Auteur :** GroupDocs  

## Tutoriels associés
- [Comment extraire les métadonnées d'un document à partir de flux avec GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [Comment masquer les métadonnées d'un document avec GroupDocs.Redaction pour .NET - Guide complet](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Tutoriels de chargement de documents avec GroupDocs.Redaction pour .NET](/redaction/net/document-loading/)