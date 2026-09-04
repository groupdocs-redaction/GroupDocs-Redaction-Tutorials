---
date: '2026-07-20'
description: Apprenez à caviarder des documents, masquer les informations sensibles
  et enregistrer les fichiers caviardés dans un flux mémoire à l'aide de GroupDocs.Redaction
  for .NET.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: Comment caviarder des documents avec GroupDocs.Redaction for .NET.
  Suivez ce guide étape par étape pour masquer les informations sensibles et enregistrer
  le fichier caviardé dans un flux mémoire.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: Comment caviarder des documents avec GroupDocs.Redaction for .NET
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
title: Comment caviarder des documents avec GroupDocs.Redaction for .NET – Guide complet
type: docs
url: /fr/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# Comment masquer des documents avec GroupDocs.Redaction pour .NET

Dans les environnements d'entreprise modernes, **comment masquer des documents** est une compétence cruciale pour protéger les données personnelles, les secrets commerciaux et les informations liées à la conformité. Ce guide vous explique comment masquer les informations sensibles des fichiers Word, PDF ou image, puis enregistrer la sortie masquée directement dans un flux mémoire — le tout avec GroupDocs.Redaction pour .NET.

## Réponses rapides
- **Que fait le masquage ?** Il remplace définitivement le contenu sélectionné par un espace réservé ou le supprime, garantissant que les données ne pourront jamais être récupérées.  
- **Quels formats sont pris en charge ?** Plus de 30 types de fichiers, y compris PDF, DOCX, PPTX et les formats d'image courants.  
- **Puis-je masquer sans écrire sur le disque ?** Oui — enregistrez le résultat dans un `MemoryStream` pour un traitement en mémoire.  
- **Ai-je besoin d'une licence pour la production ?** Une licence complète est requise pour une utilisation en production ; un essai gratuit est disponible pour l'évaluation.  
- **Est‑il compatible avec .NET Core ?** Absolument — GroupDocs.Redaction fonctionne avec .NET Framework 4.6+, .NET Core 3.1+, et .NET 5/6/7.

## Qu'est‑ce que le masquage de documents ?
Le masquage de documents supprime ou masque de façon permanente le texte confidentiel, les images et les métadonnées d'un fichier, garantissant que le contenu caché ne peut pas être récupéré, visualisé ou extrait ultérieurement. Il remplace les éléments sensibles par un espace réservé tel qu'un rectangle noir ou un texte personnalisé, et met à jour la structure du document afin que les données masquées soient irrécupérables.

## Pourquoi utiliser GroupDocs.Redaction pour masquer des documents ?
GroupDocs.Redaction prend en charge **plus de 30 formats de fichiers** et peut gérer des fichiers jusqu'à **2 Go** sans charger le document complet en mémoire, offrant un **temps de traitement 30 % plus rapide** comparé à de nombreux concurrents. Son API vous permet d'appliquer des masquages par phrase exacte, expression régulière ou image avec un seul appel de méthode, ce qui en fait le choix le plus efficace pour les développeurs .NET.

## Prérequis
- **GroupDocs.Redaction** package NuGet (dernière version).  
- .NET Framework 4.6+ **ou** .NET Core 3.1+ installé.  
- Un IDE compatible C# tel que Visual Studio 2022.  
- Connaissances de base en C# et familiarité avec les entrées/sorties de fichiers.

### Bibliothèques requises et versions
- **GroupDocs.Redaction** – utilisez toujours la dernière version pour accéder aux algorithmes de masquage les plus récents et aux correctifs de sécurité.  
- **System.IO** – pour la gestion des flux (intégré à .NET).

### Étapes d'obtention de licence
- **Free Trial :** Inscrivez‑vous sur le site Web de GroupDocs pour un essai de 30 jours.  
- **Temporary License :** Demandez une clé temporaire pour les tests de développement.  
- **Full License :** Achetez une licence de production pour une utilisation illimitée.

## Initialisation et configuration de base
La classe `Redactor` est le point d'entrée pour toutes les opérations de masquage dans GroupDocs.Redaction. Après avoir installé le package NuGet, vous créez une instance de `Redactor` avec le chemin du document source.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## Comment masquer du texte spécifique dans un document ?
Pour masquer du texte spécifique, chargez le fichier source avec une instance `Redactor`, puis appliquez un `ExactPhraseRedaction` qui cible la chaîne exacte que vous souhaitez masquer. L'API analyse le document, remplace chaque correspondance par la superposition choisie et enregistre les modifications dans un journal des changements, vous permettant de vérifier le masquage avant l'enregistrement.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

La classe `ExactPhraseRedaction` remplace chaque occurrence de la phrase exacte par un rectangle noir (ou tout espace réservé personnalisé que vous configurez).  

**Étape par étape :**
1. **Charger** – Créez une instance `Redactor` pointant vers votre fichier.  
2. **Appliquer** – Appelez `Apply` avec un `ExactPhraseRedaction` (ou un autre type de masquage).  
3. **Inspecter** – Examinez `RedactorChangeLog` pour confirmer le nombre de correspondances trouvées et remplacées.  

## Comment enregistrer un document masqué dans un flux mémoire ?
`MemoryStream` est un flux .NET qui stocke les données en mémoire, permettant une lecture/écriture rapide sans I/O disque. En utilisant la méthode `Save`, vous pouvez diriger la sortie masquée vers un `MemoryStream`, qui peut ensuite être envoyé sur un réseau, stocké dans une base de données, ou renvoyé directement depuis un point de terminaison API sans créer de fichiers temporaires.

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

**Points clés :**
- La méthode `Save` écrit la sortie masquée vers n'importe quelle implémentation de `Stream`, y compris `MemoryStream`.  
- Aucun fichier temporaire n'est créé, ce qui améliore la sécurité et les performances.  
- Vous pouvez combiner cela avec le `FileStreamResult` d'ASP.NET Core pour renvoyer le fichier directement à un navigateur.

## Pièges courants et solutions
| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Masquage non appliqué** | La casse de la phrase diffère de celle du source. | Utilisez `ExactPhraseRedaction("John Doe", caseSensitive: false)` ou un masquage par expression régulière pour une correspondance flexible. |
| **Les gros fichiers provoquent OutOfMemory** | Tentative de charger le fichier complet en mémoire. | GroupDocs.Redaction diffuse les données en interne ; assurez‑vous d'utiliser la dernière version qui traite les fichiers par blocs. |
| **Le fichier enregistré est corrompu** | Le flux n'est pas réinitialisé avant l'envoi. | Après `redactor.Save(stream)`, définissez `stream.Position = 0` avant de le lire ou de le renvoyer. |

## Questions fréquentes

**Q : Puis‑je masquer des fichiers PDF en utilisant la même API ?**  
R : Oui — GroupDocs.Redaction traite PDF, DOCX, PPTX et de nombreux formats d'image de manière uniforme ; il suffit de pointer `Redactor` vers un fichier PDF.

**Q : Le masquage survit‑il après la conversion du document vers un autre format ?**  
R : Absolument — une fois masqué, le contenu est définitivement supprimé, quel que soit les conversions ultérieures.

**Q : Comment personnaliser l'apparence du masquage ?**  
R : Utilisez `RedactionOptions` pour définir la couleur de superposition, l'opacité, ou remplacer le texte par une chaîne personnalisée.

**Q : Est‑il possible de masquer en utilisant des expressions régulières ?**  
R : Oui — `RegexRedaction` vous permet de définir des modèles tels que les numéros de carte de crédit ou les adresses e‑mail.

**Q : Quelles versions de .NET sont officiellement prises en charge ?**  
R : .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6 et .NET 7.

---

**Dernière mise à jour :** 2026-07-20  
**Testé avec :** GroupDocs.Redaction 23.12 for .NET  
**Auteur :** GroupDocs  

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

## Tutoriels associés

- [Comment charger et masquer des documents avec GroupDocs.Redaction .NET : guide complet](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Enregistrer les documents masqués au format original avec GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Masquage sécurisé de documents en .NET avec des flux : guide pour GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)