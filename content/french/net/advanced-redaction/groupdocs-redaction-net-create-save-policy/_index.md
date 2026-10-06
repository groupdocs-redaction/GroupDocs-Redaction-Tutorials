---
date: '2026-10-06'
description: Apprenez à caviarder les données sensibles avec GroupDocs.Redaction .NET.
  Ce guide étape par étape vous montre comment créer, appliquer et enregistrer une
  politique de caviardage au format XML.
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: Apprenez à caviarder les données sensibles avec GroupDocs.Redaction
  .NET. Ce guide étape par étape vous montre comment créer, appliquer et enregistrer
  une politique de caviardage au format XML.
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: Comment caviarder les données sensibles avec GroupDocs.Redaction .NET
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
title: Comment caviarder les données sensibles avec GroupDocs.Redaction .NET
type: docs
url: /fr/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# Comment masquer les données sensibles avec GroupDocs.Redaction .NET

Protéger les informations confidentielles contenues dans les contrats, les états financiers ou les dossiers patients est une exigence non négociable pour les applications modernes. Dans ce guide, vous apprendrez **comment masquer les données sensibles** avec GroupDocs.Redaction pour .NET, depuis l'installation du SDK jusqu'à la définition de politiques XML réutilisables pouvant être appliquées à tout type de document.

## Réponses rapides
- **Que signifie « créer une politique de masquage » ?** C’est le processus de définition de règles (texte, regex, images, etc.) qui indique à GroupDocs.Redaction comment masquer ou remplacer le contenu confidentiel.  
- **Quelle bibliothèque faut‑il ?** GroupDocs.Redaction pour .NET, disponible via NuGet.  
- **Ai‑je besoin d’une licence ?** Un essai gratuit suffit pour le développement ; une licence permanente est requise pour la production.  
- **Puis‑je réutiliser la politique ?** Oui—une fois enregistrée en XML, vous pouvez la charger plus tard et l’appliquer à tout document.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Qu’est‑ce qu’une politique de masquage ?

Une politique de masquage est un ensemble de règles qui spécifient *quoi* doit être supprimé ou remplacé et *comment* le remplacement doit apparaître. En créant une politique une fois, vous pouvez appliquer des normes de sécurité cohérentes à chaque document traité par votre application.

## Comment fonctionne une politique de masquage ?

Chargez un document avec le moteur `Redactor`, attachez une ou plusieurs règles de masquage, puis invoquez `Apply`. Le moteur analyse le document, masque le contenu correspondant et peut éventuellement générer un nouveau fichier. Le même ensemble de règles peut être exporté en XML, vous permettant de réutiliser la politique sans recompilation du code.

## Pourquoi utiliser GroupDocs.Redaction pour créer une politique de masquage ?

GroupDocs.Redaction offre un ensemble complet de fonctionnalités qui simplifient la création, la gestion et l’exécution des politiques de masquage, garantissant une protection cohérente des données sur divers types de documents tout en offrant des performances élevées et une intégration facile dans les applications .NET existantes pour les équipes et les organisations.

- **Large prise en charge des formats** – le SDK gère plus de 30 types de fichiers, y compris PDF, DOCX, XLSX, PPTX et les formats d’image, et peut traiter des fichiers jusqu’à 2 Go sans charger le fichier complet en mémoire.  
- **Précision programmatique** – définissez des phrases exactes, des expressions régulières ou une logique personnalisée pour cibler uniquement les données que vous devez masquer.  
- **Politiques XML réutilisables** – exportez vos règles une fois et partagez‑les entre équipes, services ou micro‑services.  
- **Moteur optimisé pour les performances** – la bibliothèque traite des documents de plusieurs centaines de pages en moins d’une seconde sur du matériel serveur typique, ce qui la rend adaptée aux pipelines à haut débit.

## Prérequis
- Bibliothèque GroupDocs.Redaction compatible avec votre runtime .NET.  
- Visual Studio, VS Code ou tout IDE supportant C#.  
- Familiarité de base avec C# et la structure d’un projet .NET.

## Configuration de GroupDocs.Redaction pour .NET

Tout d’abord, ajoutez la bibliothèque à votre projet.

**Utilisation du CLI .NET**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Utilisation du gestionnaire de packages**  
```powershell
Install-Package GroupDocs.Redaction
```  

Ou recherchez « GroupDocs.Redaction » dans l’interface du gestionnaire de packages NuGet et installez‑la depuis là.

### Acquisition de licence
- Commencez avec un **essai gratuit** pour explorer les fonctionnalités.  
- Demandez une **licence temporaire** pour des tests prolongés, puis achetez une licence complète pour la production.

### Initialisation de base
Ajoutez l’espace de noms à votre fichier source :

La classe `Redactor` est le moteur principal qui charge un document et applique les règles de masquage.  
```csharp
using GroupDocs.Redaction;
```  

La classe `Redactor` est le moteur principal de GroupDocs.Redaction qui charge un document et applique les règles de masquage.

## Comment créer une politique de masquage étape par étape

Voici un guide complet qui montre comment construire programmatique une politique de masquage, configurer ses règles, les appliquer à un document, puis enregistrer la politique sous forme de fichier XML pour une réutilisation future, assurant un masquage cohérent sur plusieurs projets et types de documents.

### Étape 1 : préparer votre répertoire de documents
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*Remplacez `"YOUR_DOCUMENT_DIRECTORY"` par le dossier contenant les documents que vous souhaitez protéger.*

### Étape 2 : charger le document
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
L’objet `Redactor` ouvre le fichier et gère son cycle de vie.

### Étape 3 : définir les masquages
`ExactPhraseRedaction` définit une règle qui remplace une phrase spécifique, tandis que `RegexRedaction` utilise une expression régulière pour correspondre à des motifs.  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
Ici, nous créons deux règles :
1. **ExactPhraseRedaction** – remplace une phrase connue par « [REDACTED] ».  
2. **RegexRedaction** – trouve les dates au format `YYYY‑MM‑DD` et les remplace par « [DATE REDACTED] ».

### Étape 4 : appliquer les masquages
```csharp
redactor.Apply(redactions);
```  
Toutes les règles définies sont exécutées sur le document ouvert en une seule passe.

### Étape 5 : enregistrer la politique sous forme de fichier XML
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
Le fichier XML stocke les définitions de masquage, vous permettant de réutiliser la même politique sans réécrire le code.

## Applications pratiques

- **Cabinets d’avocats** peuvent masquer les numéros de dossier et les noms des clients avant de partager les brouillons.  
- **Départements financiers** masquent les numéros de compte ou les dates de transaction dans les rapports.  
- **Prestataires de santé** assurent la conformité HIPAA en supprimant les identifiants des patients.

## Conseils de performance

- Ouvrez **un document à la fois** pour maintenir une faible utilisation de la mémoire.  
- Rédigez des **expressions régulières efficaces** ; évitez les motifs trop larges qui augmentent le temps de traitement.  
- Maintenez la bibliothèque **à jour** pour profiter des améliorations de performance et des nouveaux types de masquage.

## Problèmes courants et solutions

| Problème | Pourquoi cela se produit | Comment résoudre |
|----------|--------------------------|------------------|
| **Exception d'E/S lors de la préparation du répertoire** | Chemin incorrect ou permissions d'écriture manquantes | Vérifiez que le dossier existe et que l’application dispose des droits de lecture/écriture. |
| **Le regex ne correspond pas au texte attendu** | Le motif est trop strict ou il manque des caractères d’échappement | Testez le regex avec un outil en ligne ; ajustez les quantificateurs ou échappez les caractères spéciaux. |
| **Le fichier de politique n’est pas créé** | `SavePolicy` appelé avant d’appliquer les masquages ou avec un chemin invalide | Assurez‑vous que le répertoire de sortie est accessible en écriture et appelez `SavePolicy` après `Apply`. |

## Questions fréquemment posées

**Q : Puis‑je charger une politique XML existante au lieu d’en créer une programmatiquement ?**  
R : Oui—utilisez `redactor.LoadPolicy("policy.xml")` pour importer une politique précédemment enregistrée.

**Q : GroupDocs.Redaction prend‑il en charge les PDF protégés par mot de passe ?**  
R : Absolument. Transmettez le mot de passe au constructeur `Redactor` : `new Redactor(sourceFile, "password")`.

**Q : Est‑il possible de masquer des images ou des métadonnées ?**  
R : Le SDK fournit les classes `ImageRedaction` et `MetadataRedaction` pour ces scénarios.

**Q : Comment gérer de gros documents (des centaines de Mo) ?**  
R : Traitez‑les par morceaux ou utilisez l’API de streaming pour réduire l’empreinte mémoire ; le moteur peut gérer des fichiers jusqu’à 2 Go sans charger le fichier complet en RAM.

**Q : Quel modèle de licence est requis pour une utilisation commerciale ?**  
R : Une licence payante est requise pour les déploiements en production ; une licence d’essai suffit pour le développement et les tests.

## Conclusion

Vous disposez maintenant d’une **politique de masquage** complète et réutilisable que vous pouvez appliquer à tout document avec GroupDocs.Redaction pour .NET. En exportant la politique en XML, vous simplifiez les mises à jour futures et assurez une protection cohérente des données au sein de votre organisation.

### Prochaines étapes
- Expérimentez avec des types de masquage supplémentaires tels que `ImageRedaction` ou `MetadataRedaction`.  
- Intégrez la logique de chargement de la politique dans votre flux de travail de gestion de documents pour un masquage automatisé.  
- Explorez la référence API de **GroupDocs.Redaction** pour des personnalisations avancées.

---

**Dernière mise à jour :** 2026-10-06  
**Testé avec :** GroupDocs.Redaction 5.8 pour .NET  
**Auteur :** GroupDocs  

**Ressources**  
- [Documentation](https://docs.groupdocs.com/redaction/net/)  
- [Référence API](https://reference.groupdocs.com/redaction/net)  
- [Téléchargement](https://releases.groupdocs.com/redaction/net/)  
- [Forum d’assistance gratuit](https://forum.groupdocs.com/c/redaction/33)  
- [Demande de licence temporaire](https://purchase.groupdocs.com/temporary-license/)

## Tutoriels associés

- [Masquer les données sensibles avec GroupDocs.Redaction .NET (C#)](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)
- [Implémenter le masquage de documents avec GroupDocs.Redaction .NET : guide étape par étape](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
- [Comment masquer les documents avec GroupDocs.Redaction .NET – guide complet](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)