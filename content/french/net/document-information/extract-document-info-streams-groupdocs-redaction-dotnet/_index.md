---
date: '2026-06-11'
description: Apprenez comment extraire les métadonnées des flux de documents en utilisant
  GroupDocs.Redaction pour .NET, couvrant la configuration, des exemples de code et
  des applications pratiques.
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: Comment extraire les métadonnées des flux de documents à l'aide de GroupDocs.Redaction
  .NET
type: docs
url: /fr/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# Comment extraire les métadonnées des flux de documents à l'aide de GroupDocs.Redaction .NET

Êtes‑vous fatigué d'extraire manuellement les informations d'un document ou de gérer de gros fichiers qui ralentissent votre flux de travail ? **Comment extraire les métadonnées** rapidement est un défi courant, et la bibliothèque GroupDocs.Redaction pour .NET offre une méthode rapide et efficace en mémoire pour récupérer les détails d'un document directement à partir des flux. Dans ce tutoriel, vous apprendrez comment configurer la bibliothèque, extraire le type de fichier, le nombre de pages et la taille depuis un flux, et préparer un dossier de sortie pour un traitement ultérieur.

## Réponses rapides
- **Que signifie « extraire les métadonnées » ?** Cela signifie lire des propriétés telles que le type de fichier, le nombre de pages et la taille sans ouvrir le document complet en mémoire.  
- **Quelle bibliothèque gère cela ?** GroupDocs.Redaction pour .NET fournit une API native pour l'extraction de métadonnées basée sur les flux.  
- **Ai‑je besoin d'une licence ?** Un essai gratuit suffit pour le développement ; une licence commerciale est requise pour la production.  
- **Puis‑je traiter des PDF de plus de 1 GB ?** Oui – les flux vous permettent de gérer des fichiers jusqu'à 2 GB sans charger le fichier entier.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ et .NET 6+.

## Qu'est‑ce que l'extraction de métadonnées à partir de flux ?
L'extraction de métadonnées à partir de flux est le processus de lecture des propriétés d'un document directement depuis un objet `Stream`, évitant le chargement complet du fichier et économisant ainsi la mémoire et le temps CPU. Cette technique est idéale pour le traitement par lots ou les services cloud où les ressources sont limitées.

## Pourquoi utiliser GroupDocs.Redaction pour l'extraction de métadonnées ?
GroupDocs.Redaction prend en charge **plus de 30 formats de fichiers** (y compris PDF, DOCX, XLSX, PPTX et les types d'images) et peut traiter des documents jusqu'à **2 GB** tout en maintenant l'utilisation de la mémoire sous **50 MB**. Son API `Redactor` fournit un appel unique pour récupérer toutes les informations clés du document, éliminant le besoin de plusieurs analyseurs.

## Prérequis
- **GroupDocs.Redaction pour .NET** (dernière version)  
- **.NET Framework** 4.5+ **ou** **.NET Core/5+/6+**  
- Connaissances de base en C# et familiarité avec les entrées/sorties de fichiers  
- Visual Studio 2019 ou version ultérieure

## Comment configurer GroupDocs.Redaction pour .NET ?
Pour commencer à utiliser GroupDocs.Redaction, vous devez d'abord ajouter la bibliothèque à votre projet. Cela peut être fait via la CLI .NET, le Gestionnaire de packages Visual Studio ou l'interface NuGet. Choisissez l'approche qui correspond à votre flux de travail ; la CLI est idéale pour les builds scriptables, tandis que l'UI offre une manière graphique de parcourir les versions et les dépendances.

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Gestionnaire de packages**  
```powershell
Install-Package GroupDocs.Redaction
```

**Interface du Gestionnaire de packages NuGet :**  
- Ouvrez le Gestionnaire de packages NuGet dans Visual Studio.  
- Recherchez **"GroupDocs.Redaction"** et installez la dernière version.

### Étapes d'acquisition de licence
1. **Essai gratuit :** Téléchargez une licence d'essai pour explorer toutes les fonctionnalités sans restrictions.  
2. **Licence temporaire :** Demandez une licence temporaire sur [GroupDocs](https://purchase.groupdocs.com/temporary-license/) pour des tests prolongés.  
3. **Achat :** Lorsque vous êtes prêt pour la production, achetez une licence commerciale.  

Pour plus d'informations, consultez le [site Web de GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Initialisation et configuration de base
La classe `Redactor` est le point d'entrée pour toutes les opérations, y compris l'extraction de métadonnées.

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

Maintenant que la bibliothèque est prête, plongeons dans les détails de l'implémentation.

## Comment extraire les métadonnées d'un flux de document ?
Chargez le document en tant que **flux en lecture seule**, initialisez le `Redactor`, et appelez `GetDocumentInfo()` pour récupérer les métadonnées en une seule étape. Cette approche évite de charger le fichier complet en mémoire, ce qui est crucial pour les PDF volumineux ou les documents Office de plusieurs centaines de pages.

**Réponse directe :** Ouvrez le fichier avec `File.OpenRead()`, transmettez le flux à `new Redactor(stream)`, puis appelez `redactor.GetDocumentInfo()` – la méthode renvoie un objet contenant le type de fichier, le nombre de pages et la taille en seulement trois lignes de code.

### Étape 1 : Préparer le chemin du fichier source
Tout d'abord, assurez‑vous que le fichier source existe et que le dossier de sortie est prêt. La méthode d'assistance ci‑dessous vérifie le répertoire de sortie et le crée si nécessaire.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*Pourquoi ?* Cela garantit un chemin valide pour les opérations de fichiers ultérieures et empêche `DirectoryNotFoundException`.

### Étape 2 : Ouvrir le flux du document
L'utilisation de `File.OpenRead()` ouvre le fichier en tant que **flux en lecture seule**, ce qui maintient une faible utilisation de la mémoire même pour des fichiers de plusieurs gigaoctets.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*Pourquoi ?* Les flux permettent un traitement à la volée, vous laissant travailler sur des portions du fichier plutôt que sur le document entier.

### Étape 3 : Initialiser le Redactor avec le flux du document
`Redactor` est l'objet API principal qui vous donne accès aux opérations au niveau du document, y compris l'extraction de métadonnées.

`Redactor` représente un document unique chargé depuis un flux et expose des méthodes telles que `GetDocumentInfo()` pour une récupération rapide des propriétés.  

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*Pourquoi ?* Instancier `Redactor` avec un flux lie l'objet au fichier sous‑jacent sans le charger entièrement.

### Étape 4 : Récupérer les métadonnées du document
Appeler `GetDocumentInfo()` renvoie un objet `DocumentInfo` qui contient le format du fichier, le nombre de pages et la taille du fichier.

`GetDocumentInfo()` extrait les propriétés de base (format, nombre de pages, taille) en un seul appel, éliminant le besoin de parseurs séparés.  

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*Pourquoi ?* Cette étape consolide toutes les métadonnées essentielles, facilitant la journalisation, le filtrage ou le routage des documents selon leurs caractéristiques.

## Comment préparer un répertoire de sortie pour les fichiers traités ?
Avant d'écrire des fichiers traités, assurez‑vous que le dossier de destination existe et est accessible en écriture. En vérifiant le chemin de façon programmatique et en le créant lorsqu'il manque, vous évitez les exceptions d'exécution courantes telles que `DirectoryNotFoundException` ou les erreurs de permission. Cette simple étape rend également votre code portable entre différents environnements, que ce soit localement, sur un serveur ou dans un conteneur.

**Réponse directe :** Utilisez `Directory.Exists()` pour vérifier la présence du dossier et `Directory.CreateDirectory()` pour le créer s'il n'existe pas – cette vérification en une ligne garantit un chemin valide avant toute opération d'écriture.

### Implémenter une méthode d'assistance
La méthode ci‑dessous encapsule la logique de vérification‑et‑création, renvoyant le chemin vérifié pour une utilisation ultérieure.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*Pourquoi ?* Centraliser cette logique réduit la duplication et facilite la maintenance du code.

## Problèmes courants et solutions
- **Erreurs d'autorisation :** Assurez‑vous que l'application s'exécute sous un compte disposant d'un accès en écriture au dossier cible.  
- **Chemins invalides :** Vérifiez les séparateurs de chemin (`\\` sous Windows, `/` sous Linux/macOS) pour éviter `DirectoryNotFoundException`.  
- **Gestion des gros fichiers :** Libérez rapidement les flux (`using` statements) pour libérer les handles OS et éviter les fuites.

## Applications pratiques
1. **Ingestion automatisée de documents :** Extraire les métadonnées lors du téléchargement, puis les stocker dans une base de données pour une recherche rapide et des rapports de conformité.  
2. **Audits juridiques et de conformité :** Extraire le nombre de pages et les types de fichiers pour vérifier que les documents respectent les normes réglementaires avant l'archivage.  
3. **Gestion de contenu d'entreprise :** Utiliser les métadonnées pour auto‑classer les fichiers dans des dossiers, améliorant l'organisation et la vitesse de récupération.

## Considérations de performance
- **Gestion de la mémoire :** Enveloppez toujours les flux dans des blocs `using` afin qu'ils soient libérés automatiquement.  
- **Traitement par lots :** Traitez les documents par groupes de 10‑20 pour équilibrer le débit et l'utilisation de la mémoire, surtout sur des serveurs aux ressources limitées.  
- **Parallélisme :** Utilisez `Parallel.ForEach` pour les fichiers indépendants, mais surveillez le CPU et les I/O pour éviter les contentions.

## Conclusion
Vous disposez maintenant d'un guide complet, prêt pour la production, sur **comment extraire les métadonnées** des flux de documents à l'aide de GroupDocs.Redaction pour .NET. En suivant les étapes ci‑dessus, vous pouvez récupérer efficacement le type de fichier, le nombre de pages et la taille tout en maintenant une faible utilisation de la mémoire et en traitant les gros fichiers de manière fluide.

**Prochaines étapes**
- Passez en revue la référence complète de l'API dans la [documentation](https://docs.groupdocs.com/redaction/net/).  
- Plongez plus profondément dans la [Documentation GroupDocs Redaction .NET](https://docs.groupdocs.com/redaction/net/) pour explorer les fonctionnalités de rédaction, de filigrane et d'OCR.  
- Expérimentez différents formats de fichiers (PDF, DOCX, XLSX) pour voir comment les métadonnées varient selon les types.  
- Intégrez les métadonnées extraites dans votre solution de gestion documentaire ou de recherche existante.

## Questions fréquemment posées

**Q : Quel est le principal cas d'utilisation de l'extraction de métadonnées de GroupDocs.Redaction ?**  
R : Elle permet une récupération rapide et efficace en mémoire des propriétés d'un document pour l'indexation, les contrôles de conformité et le routage automatisé sans ouvrir le fichier complet.

**Q : Puis‑je extraire les métadonnées de fichiers protégés par mot de passe ?**  
R : Oui, fournissez le mot de passe lors de la construction de l'objet `Redactor` ; l'API déchiffrera le flux en interne.

**Q : La bibliothèque prend‑elle en charge les formats non PDF comme DOCX ou XLSX ?**  
R : Absolument – GroupDocs.Redaction gère plus de 30 formats, y compris PDF, DOCX, XLSX, PPTX et les types d'images courants.

**Q : Quelle taille de document puis‑je traiter avec les flux ?**  
R : Les flux permettent le traitement de fichiers jusqu'à **2 GB** tout en maintenant la consommation de mémoire sous **50 MB**, grâce à la lecture à la volée.

**Q : Où puis‑je obtenir de l'aide en cas de problème ?**  
R : Visitez le [forum GroupDocs](https://forum.groupdocs.com/c/redaction/33) pour le support communautaire, ou consultez la documentation officielle pour des conseils de dépannage.

---

**Dernière mise à jour :** 2026-06-11  
**Testé avec :** GroupDocs.Redaction 23.12 for .NET  
**Auteur :** GroupDocs  

**Ressources**  
- **Documentation :** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **Référence API :** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Téléchargement :** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## Tutoriels associés

- [Maîtriser la récupération des métadonnées de document avec l'API GroupDocs.Redaction .NET](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)  
- [Comment masquer les métadonnées d'un document avec GroupDocs.Redaction pour .NET - Guide complet](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)  
- [Rédaction sécurisée de documents en .NET à l'aide de flux : Guide pour GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)