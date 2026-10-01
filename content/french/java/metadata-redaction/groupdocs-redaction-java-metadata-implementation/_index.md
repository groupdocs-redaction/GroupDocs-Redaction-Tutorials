---
date: '2026-10-01'
description: Apprenez à supprimer les métadonnées d'auteur et à enregistrer des fichiers
  de documents censurés en Java avec GroupDocs Redaction.
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Apprenez à supprimer les métadonnées d'auteur et à enregistrer des
  fichiers de documents censurés en Java avec GroupDocs Redaction. Suivez le guide
  étape par étape.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: Comment supprimer les métadonnées d'auteur en Java avec GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: Comment supprimer les métadonnées d'auteur en Java avec GroupDocs
type: docs
url: /fr/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Comment supprimer les métadonnées d'auteur en Java avec GroupDocs

Dans le paysage numérique actuel, protéger les informations sensibles cachées dans les documents est une pratique indispensable. **Supprimer les métadonnées d'auteur** empêche la divulgation accidentelle d'identifiants personnels ou d'entreprise. Ce tutoriel vous montre, étape par étape, comment utiliser `EraseMetadataRedaction` de GroupDocs.Redaction pour Java afin de supprimer les champs tels que *Author* et *Manager* des fichiers Word, puis **enregistrer des copies du document redacté** en toute sécurité pour le partage ou l'archivage.

## Réponses rapides
- **Que fait EraseMetadataRedaction ?** Elle supprime les champs de métadonnées sélectionnés d'un document.  
- **Quelle bibliothèque fournit cette fonctionnalité ?** GroupDocs.Redaction pour Java.  
- **Ai-je besoin d'une licence ?** Un essai gratuit suffit pour les tests ; une licence permanente est requise pour la production.  
- **Puis-je cibler plusieurs champs à la fois ?** Oui, combinez les filtres avec un OU logique.  
- **Le processus est‑il thread‑safe ?** Les instances de Redactor ne sont pas partagées entre les threads ; créez une nouvelle instance par opération.

## Qu'est‑ce que EraseMetadataRedaction ?
`EraseMetadataRedaction` est une classe de rédaction intégrée qui vous permet de spécifier quelles entrées de métadonnées doivent être effacées. Elle fonctionne sur une large gamme de formats de documents pris en charge par GroupDocs.Redaction, garantissant que les informations d'auteur cachées ne fuient jamais. Vous pouvez cibler des propriétés standard telles que Author, Manager, ainsi que des champs de métadonnées personnalisés, offrant une protection complète de la vie privée.

## Pourquoi utiliser EraseMetadataRedaction avec GroupDocs ?
GroupDocs.Redaction prend en charge **plus de 100 formats d'entrée et de sortie** et peut traiter des documents jusqu'à 500 pages sans charger le fichier complet en mémoire. L'utilisation de cette classe vous fournit une API unique et haute performance pour répondre aux exigences du RGPD, HIPAA ou de conformité interne tout en gardant votre base de code simple.

## Prérequis
- Java 8 ou supérieur installé.  
- Maven (ou la possibilité d'ajouter les JAR manuellement).  
- GroupDocs.Redaction pour Java (version 24.9 ou ultérieure).  
- Une licence d'essai ou permanente valide de GroupDocs.

## Configurer GroupDocs.Redaction pour Java

### Installation Maven
Ajoutez le dépôt GroupDocs et la dépendance à votre **pom.xml** :

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### Téléchargement direct
Sinon, téléchargez le dernier JAR depuis [GroupDocs Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Obtention de licence
Obtenez un essai gratuit ou achetez une licence temporaire via le portail GroupDocs. Le fichier de licence doit être placé à un emplacement où votre application peut le charger (par ex., à la racine du classpath).

### Initialisation et configuration de base
Voici un exemple minimal qui crée une instance `Redactor` pour un fichier DOCX :

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Comment utiliser EraseMetadataRedaction en Java
Les sections suivantes détaillent l'implémentation en étapes claires et concrètes.

### Fonctionnalité : nettoyer des éléments de métadonnées spécifiques

#### Vue d'ensemble
Nous allons supprimer les champs de métadonnées **Author** et **Manager** à l'aide de `EraseMetadataRedaction`. C'est une exigence courante lors du partage de rapports internes avec des partenaires externes.

#### Mise en œuvre étape par étape

##### 1️⃣ Initialiser l'objet Redactor
`Redactor` est la classe principale qui charge un document, applique les objets de rédaction et écrit le résultat. Créez une nouvelle instance pour chaque fichier que vous traitez :

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ Appliquer EraseMetadataRedaction
`MetadataFilters` fournit des filtres prédéfinis pour les clés de métadonnées courantes telles que Author et Manager.  
`EraseMetadataRedaction` supprime les entrées de métadonnées qui correspondent aux `MetadataFilters` fournis. L'opérateur OU bit à bit (`|`) combine les filtres `Author` et `Manager` afin que les deux champs soient supprimés en un seul appel :

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ Configurer les options d'enregistrement
`SaveOptions` vous permet de spécifier le nom du fichier de sortie, le format et d'autres paramètres d'enregistrement.  
`SaveOptions` vous permet de contrôler le nom du fichier de sortie, le format et si le document doit être rasterisé en PDF. Ajouter un suffixe préserve le fichier original intact :

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## Cas d'utilisation courants
1. **Documents juridiques** – Rédiger les informations d'auteur avant d'envoyer les contrats à la partie adverse.  
2. **Rapports d'entreprise** – Supprimer les noms des managers lors de la publication des résultats trimestriels aux actionnaires.  
3. **Fichiers de projet** – Nettoyer la documentation interne du projet avant l'archivage ou le téléchargement vers un dépôt public.

## Conseils de dépannage
- **Fichier non trouvé** – Vérifiez que le chemin dans `inputFilePath` pointe vers un fichier existant et que l'application dispose des permissions de lecture.  
- **Champs de métadonnées manquants** – Tous les types de documents ne stockent pas les mêmes clés de métadonnées ; vérifiez d'abord les propriétés du document dans Office.  
- **Erreurs de licence** – Assurez-vous que le fichier de licence est correctement chargé avant de créer l'instance `Redactor`.

## Considérations de performance
- Fermez rapidement l'objet `Redactor` (comme montré dans le bloc `finally`) pour libérer les ressources natives.  
- Évitez de rasteriser les gros documents sauf si vous avez besoin d'un aperçu PDF ; la rasterisation peut augmenter l'utilisation du CPU et de la mémoire jusqu'à 3 fois pour des fichiers de 300 pages.

## Questions fréquentes

**Q1 : Qu'est‑ce que la rédaction de métadonnées ?**  
A1 : La rédaction de métadonnées consiste à supprimer les propriétés cachées d'un document (comme l'auteur, le manager ou des balises personnalisées) afin d'éviter la divulgation accidentelle d'informations sensibles.

**Q2 : Puis‑je utiliser GroupDocs.Redaction pour d'autres types de fichiers ?**  
A2 : Oui, la bibliothèque prend en charge PDF, DOCX, PPTX, XLSX et de nombreux autres formats—plus de 100 au total.

**Q3 : Comment gérer les erreurs pendant la rédaction ?**  
A3 : Enveloppez l'appel `apply` dans un bloc try‑catch et fermez toujours le `Redactor` dans une clause finally pour garantir la libération des ressources.

**Q4 : Est‑il possible de rédiger des champs de métadonnées personnalisés ?**  
A5 : Absolument. Utilisez `MetadataFilters.Custom("YourFieldName")` pour cibler toute propriété personnalisée stockée dans le document.

**Q5 : Quelles sont les meilleures pratiques pour utiliser GroupDocs.Redaction ?**  
A5 :  
- Chargez la licence dès le démarrage de votre application.  
- Fermez rapidement les objets `Redactor`.  
- Utilisez `SaveOptions` pour ajouter un suffixe, afin de laisser les fichiers originaux intacts.  
- Testez la rédaction sur une copie du document avant de traiter des lots.

**Q6 : EraseMetadataRedaction prend‑il en charge les opérations par lots ?**  
A6 : Vous pouvez parcourir une collection de chemins de fichiers, créer un nouveau `Redactor` pour chaque fichier et appliquer la même logique de rédaction.

**Q7 : Puis‑je combiner EraseMetadataRedaction avec d'autres types de rédaction ?**  
A7 : Oui, vous pouvez enchaîner plusieurs objets de rédaction (par ex., rédaction de texte suivie de rédaction de métadonnées) avant l'enregistrement.

## Ressources

- **Documentation** : [Documentation](https://docs.groupdocs.com/redaction/java/)  
- **Référence API** : [Référence API](https://reference.groupdocs.com/redaction/java)  
- **Dernières versions** : [Dernières versions](https://releases.groupdocs.com/redaction/java/)  
- **Dépôt GitHub GroupDocs** : [Dépôt GitHub GroupDocs](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Forum GroupDocs** : [Forum GroupDocs](https://forum.groupdocs.com/c/redaction/33)  
- **Obtenir une licence temporaire** : [Obtenir une licence temporaire](https://purchase.groupdocs.com/temporary-license)

---

**Dernière mise à jour :** 2026-10-01  
**Testé avec :** GroupDocs.Redaction 24.9 for Java  
**Auteur :** GroupDocs

## Tutoriels associés

- [Extraction des métadonnées de document Java GroupDocs Redaction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [Comment supprimer les métadonnées Java avec GroupDocs.Redaction](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [Récupérer les informations du document avec GroupDocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)