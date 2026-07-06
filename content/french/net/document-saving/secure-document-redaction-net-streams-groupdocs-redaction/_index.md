---
date: '2026-07-06'
description: Apprenez comment caviarder des documents .net en utilisant des streams
  avec GroupDocs.Redaction. Ce tutoriel couvre le setup, le load document from stream,
  l'application des redactions, et le saving securely.
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
title: Caviarder les documents .net à l'aide de streams – Guide GroupDocs.Redaction
type: docs
url: /fr/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/
weight: 1
---

# Masquer les documents .net à l'aide de flux – Guide complet

Bienvenue ! Dans ce tutoriel, vous découvrirez comment **redact documents .net** en toute sécurité en exploitant les flux avec GroupDocs.Redaction. Nous parcourrons tout ce dont vous avez besoin — de l'installation de la bibliothèque, le chargement d'un document depuis un flux, l'application de redactions précises, à l'enregistrement du résultat sans laisser de fichiers temporaires sur le disque.

## Réponses rapides
- **Quelle bibliothèque gère la redaction en .NET ?** GroupDocs.Redaction for .NET.  
- **Puis-je charger un fichier directement depuis un flux ?** Yes—use `FileStream` with the Redactor constructor.  
- **Quels formats sont pris en charge ?** Over 70 input and output formats, including PDF, DOCX, XLSX, PPTX.  
- **Ai-je besoin d'une licence pour la production ?** A valid GroupDocs.Redaction license is required for non‑trial use.  
- **Est‑ce sûr pour les gros fichiers ?** Stream‑based processing avoids loading the whole file into memory, enabling handling of multi‑gigabyte documents.

## Qu’est‑ce que “redact documents .net” ?
**“Redact documents .net”** fait référence au processus de suppression ou de masquage permanent du contenu sensible des fichiers à l'aide de bibliothèques .NET telles que GroupDocs.Redaction. Cela garantit que les données confidentielles ne quittent jamais votre système en texte clair. Il est couramment utilisé dans les secteurs juridique, financier et de la santé pour se conformer aux réglementations de confidentialité telles que le RGPD et HIPAA, assurant que les données sensibles ne puissent pas être récupérées après le traitement.

## Pourquoi utiliser les flux pour la redaction ?
GroupDocs.Redaction prend en charge **plus de 70 formats de fichiers** et peut traiter des fichiers jusqu'à **2 GB** sans les charger entièrement en mémoire. Le streaming réduit la surcharge d'E/S, améliore les performances et s'aligne sur les meilleures pratiques de sécurité en ne conservant les données en mémoire que pendant le court laps de temps nécessaire à la transformation.

## Pré‑requis
- **GroupDocs.Redaction for .NET** – installer via NuGet (voir ci‑dessous).  
- **.NET 6+** (ou .NET Framework 4.6.1+).  
- Visual Studio 2022 ou tout IDE compatible.  
- Connaissances de base en C# et familiarité avec les flux .NET.

## Installation de GroupDocs.Redaction
Vous pouvez ajouter le package avec l'une de ces commandes :

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

Ou localisez “GroupDocs.Redaction” dans l'interface du gestionnaire de paquets NuGet et cliquez sur **Install**.

### Étapes d'obtention de licence
1. **Free Trial** – téléchargez une version d'essai depuis [GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
2. **Temporary License** – demandez une clé à court terme pour l'évaluation.  
3. **Full Purchase** – obtenez une licence permanente pour les charges de travail en production.

Une fois installé, initialisez la bibliothèque dans votre code :
```csharp
using GroupDocs.Redaction;
// Initialization code here...
```  

## Comment charger un document depuis un flux ?
Un `FileStream` fournit un flux pour lire et écrire un fichier sur le disque. La classe `Redactor` traite le document et applique les règles de redaction. Chargez votre fichier source dans un `FileStream`, puis transmettez le flux au constructeur `Redactor`. Cette approche évite d'écrire le fichier original dans un emplacement temporaire et ne conserve les données en mémoire que pendant la durée du traitement. Cette méthode fonctionne pour tout format pris en charge, y compris les PDF et les documents Office.
```csharp
// Directly open the source file as a read‑only stream
using var inputStream = new FileStream(inputPath, FileMode.Open, FileAccess.Read);
```

## Comment initialiser le Redactor avec le flux ?
La classe `Redactor` est le moteur principal qui manipule le contenu du document. En fournissant le flux d'entrée, vous activez la redaction en mémoire sans fichiers intermédiaires. Après avoir créé l'instance, vous pouvez chaîner les règles de redaction, prévisualiser les modifications et configurer des options telles que la rasterisation ou le chiffrement avant de valider le document final.
```csharp
// Initialise the Redactor with the input stream
using var redactor = new GroupDocs.Redaction.Redactor(inputStream);
```

**Ancre de définition :** `GroupDocs.Redaction.Redactor` est la classe principale qui fournit des méthodes pour appliquer, prévisualiser et valider les opérations de redaction sur un document chargé depuis un flux.

## Comment appliquer les redactions ?
Vous pouvez ajouter plusieurs actions de redaction ; l'exemple ci‑dessous supprime toutes les annotations, ce qui est une exigence courante pour enlever les commentaires cachés ou les notes de relecteur. Des types de redaction supplémentaires comme `DeleteTextRedaction` ou `ReplaceTextRedaction` peuvent être combinés pour supprimer ou masquer des chaînes, dates ou motifs spécifiques dans le document.
```csharp
// Apply a predefined redaction that removes every annotation
redactor.Apply(new DeleteAnnotationRedaction());
```

**Ancre de définition :** `DeleteAnnotationRedaction` est une règle de redaction intégrée qui efface de façon permanente les objets d'annotation tels que les commentaires, les surlignages et les tampons du document.

## Comment enregistrer le document redacté ?
L'enregistrement directement dans un `FileStream` garantit que la sortie est écrite en un seul passage, éliminant les fichiers temporaires inutiles. Vous pouvez également spécifier le format de sortie, le niveau de compression et une protection par mot de passe optionnelle via l'objet `SaveOptions` pour répondre aux exigences de sécurité. Enfin, fermez le flux de sortie pour libérer les poignées de fichier et vous assurer que le fichier est entièrement écrit sur le disque.
```csharp
// Prepare the output stream for the redacted file
using var outputStream = new FileStream(outputPath, FileMode.Create, FileAccess.Write);

// Save the modified document; RasterizationOptions disabled to keep text editable
redactor.Save(outputStream, new SaveOptions { RasterizationOptions = null });
```

**Ancre de définition :** `SaveOptions` vous permet de contrôler la façon dont le document est persisté, y compris la rasterisation, le chiffrement et la sélection du format.

## Cas d’utilisation courants
- **Legal document handling:** Supprimer les annotations confidentielles avant de partager les brouillons avec les clients.  
- **GDPR compliance:** Supprimer les identifiants personnels des contrats ou des dossiers d'employés.  
- **Internal audit reports:** Masquer les notes du relecteur tout en préservant le contenu principal pour la distribution.

## Conseils de performance pour les gros fichiers
1. **Dispose streams promptly** – les instructions `using` ferment automatiquement les flux, libérant la mémoire.  
2. **Batch processing** – Parcourez une collection de fichiers et réutilisez une seule instance `Redactor` lorsque le format le permet, réduisant la surcharge d'allocation.

## Dépannage
1. **File access denied** – Vérifiez que le compte de l'application possède les permissions de lecture/écriture sur les dossiers cibles.  
2. **Redaction not applied** – Assurez‑vous que le type de redaction choisi est compatible avec le format du document (par ex., `DeleteAnnotationRedaction` fonctionne pour PDF et DOCX).

## Questions fréquentes
**Q : Quels formats de fichiers peuvent être traités avec des flux ?**  
R : GroupDocs.Redaction prend en charge plus de 70 formats — y compris PDF, DOCX, XLSX, PPTX et HTML — lors de l’utilisation des API basées sur les flux.

**Q : Puis‑je prévisualiser les redactions avant l’enregistrement ?**  
R : Oui, appelez `redactor.GetRedactedDocument()` pour obtenir une représentation en mémoire que vous pouvez rendre ou inspecter programmaticalement.

**Q : Comment la bibliothèque gère‑t‑elle les fichiers protégés par mot de passe ?**  
R : Fournissez le mot de passe lors de l'ouverture du flux via les surcharges de `Redactor` qui acceptent `LoadOptions` contenant le mot de passe.

**Q : Existe‑t‑il une limite de taille de document ?**  
R : Le moteur peut traiter des fichiers jusqu’à 2 GB ; les fichiers plus volumineux doivent être découpés ou traités par morceaux pour rester dans les limites de mémoire.

**Q : Ai‑je besoin d’une licence distincte pour chaque environnement de déploiement ?**  
R : Une seule clé de licence peut être utilisée sur plusieurs environnements tant que l’utilisation respecte l’accord de licence.

## Conclusion
Vous disposez maintenant d’une solution complète, étape par étape, pour **redact documents .net** en utilisant des flux avec GroupDocs.Redaction. En chargeant les fichiers directement depuis des flux, en appliquant des redactions ciblées et en enregistrant sans artefacts intermédiaires, vous obtenez à la fois sécurité et performance. Explorez des types de redaction supplémentaires — tels que le remplacement de texte ou la suppression de métadonnées — pour adapter le processus à vos besoins de conformité spécifiques.

---

**Dernière mise à jour :** 2026-07-06  
**Testé avec :** GroupDocs.Redaction 5.0 for .NET  
**Auteur :** GroupDocs  

## Ressources
- [Documentation](https://docs.groupdocs.com/redaction/net/)
- [Référence API](https://reference.groupdocs.com/redaction/net)
- [Téléchargement](https://releases.groupdocs.com/redaction/net/)
- [Forum d'assistance gratuit](https://forum.groupdocs.com/c/redaction/33)
- [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)

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

## Tutoriels associés
- [Comment charger et masquer des documents avec GroupDocs.Redaction .NET&#58; Guide complet](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Masquer et enregistrer des documents avec GroupDocs.Redaction pour .NET&#58; Guide complet](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Comment extraire les métadonnées d’un document depuis des flux avec GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)