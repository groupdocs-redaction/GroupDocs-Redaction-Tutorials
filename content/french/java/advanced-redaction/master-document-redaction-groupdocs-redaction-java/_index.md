---
date: '2026-11-02'
description: Apprenez comment ajouter un suffixe au nom de fichier dans un tutoriel
  GroupDocs redaction Java en utilisant Maven, streaming load, annotation deletion
  et save options.
keywords:
- groupdocs redaction java tutorial
- add suffix filename java
- document redaction workflow
- groupdocs maven dependency
- java inputstream redaction
lastmod: '2026-11-02'
og_description: Apprenez comment ajouter un suffixe au nom de fichier dans un tutoriel
  GroupDocs redaction Java. Suivez le guide step‑by‑step Maven setup, streaming load
  et save options.
og_image_alt: Guide showing Java code to add suffix to redacted filenames using GroupDocs
  Redaction
og_title: Comment ajouter un suffixe au nom de fichier dans GroupDocs redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  headline: How to add suffix to filename in GroupDocs redaction Java
  type: TechArticle
- description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  name: How to add suffix to filename in GroupDocs redaction Java
  steps:
  - name: '1: Create InputStream'
    text: '- **Why:** Using `InputStream` allows you to handle documents stored in
      various locations—cloud buckets, databases, or in‑memory buffers—without first
      writing them to disk. This approach is essential when you need to **load document
      from stream** in micro‑service architectures.'
  - name: '1: Apply DeleteAnnotationRedaction'
    text: '- **Why:** This step ensures that any sensitive annotations (comments,
      highlights, or hidden notes) are stripped from the document, enhancing privacy
      and compliance.'
  - name: '1: Configure SaveOptions'
    text: '- **Why:** Customizing save options allows flexible output formats and
      naming conventions. Enabling `setAddSuffix(true)` **adds suffix to filename**,
      making it clear that the file has been redacted.'
  type: HowTo
- questions:
  - answer: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.
    question: Can I redact PDF documents using GroupDocs.Redaction?
  - answer: Use streaming (`load document from stream`) and close resources promptly
      to keep memory usage low.
    question: What is the best way to handle large files with GroupDocs.Redaction?
  - answer: The API automatically adds a default suffix (e.g., “_redacted”). For custom
      suffixes, rename the output file after saving.
    question: Is it possible to customize the suffix text?
  - answer: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/)
      and follow the instructions.
    question: How do I obtain a temporary license for GroupDocs.Redaction?
  - answer: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for expert assistance.
    question: Where can I get help if I encounter issues?
  type: FAQPage
tags:
- groupdocs redaction
- java tutorial
- maven dependency
- document redaction
title: Comment ajouter un suffixe au nom de fichier dans GroupDocs redaction Java
type: docs
url: /fr/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Comment ajouter un suffixe au nom de fichier dans GroupDocs Redaction Java

Dans ce **groupdocs redaction java tutorial** vous apprendrez comment ajouter automatiquement un suffixe au nom du fichier de sortie lors de la rédaction de documents avec GroupDocs.Redaction. Ajouter un suffixe élimine le renommage manuel, réduit le risque de fuite de fichiers non masqués, et s’intègre parfaitement aux pipelines CI/CD qui reposent sur des conventions de nommage. Le guide vous accompagne à travers la configuration Maven, le chargement de documents en flux, la suppression d’annotations, et la configuration des options d’enregistrement — le tout avec du code concis, prêt pour la production.

## Réponses rapides
- **Que fait « add suffix to filename » ?**  
  Lorsque vous activez l’option suffixe, le SDK ajoute automatiquement une chaîne prédéfinie (par défaut « _redacted ») au nom de base du fichier de sortie avant l’extension. Cela rend immédiatement visible quels fichiers ont été traités, aide à prévenir la distribution accidentelle du contenu original, et simplifie l’automatisation en aval qui repose sur des modèles de nommage.  
- **Puis-je charger un document depuis un flux ?**  
  Oui — GroupDocs.Redaction prend en charge le chargement depuis n’importe quel `InputStream`, idéal pour le stockage cloud ou le traitement en mémoire.  
- **Ai‑je besoin d’une licence pour cette fonctionnalité ?**  
  Un essai gratuit fonctionne pour la rédaction de base ; une licence temporaire ou complète débloque toutes les options avancées, y compris la gestion du suffixe.  
- **Quels formats sont pris en charge ?**  
  La bibliothèque gère DOCX, PDF, PPTX, XLSX et bien d’autres.  
- **La rasterisation est‑elle requise pour la sortie PDF ?**  
  La rasterisation est optionnelle ; activez‑la lorsque vous devez aplatir le document pour une sécurité supplémentaire.

## Que fait « add suffix to filename » ?

Lorsque vous activez l’option suffixe, le SDK ajoute automatiquement une chaîne prédéfinie (par défaut « _redacted ») au nom de base du fichier de sortie avant l’extension. Cela rend immédiatement visible quels fichiers ont été traités, aide à prévenir la distribution accidentelle du contenu original, et simplifie l’automatisation en aval qui repose sur des modèles de nommage.

## Pourquoi utiliser GroupDocs.Redaction pour cette tâche ?

GroupDocs.Redaction propose une API Java haute performance qui combine les actions de rédaction avec des options flexibles de gestion de fichiers telles que l’ajout automatique de suffixe, la prise en charge du streaming et le traitement par lots. Elle supporte plus de 50 formats d’entrée et de sortie et peut traiter des documents de plusieurs centaines de pages sans charger le fichier complet en mémoire, assurant ainsi une faible consommation de mémoire et une exécution rapide.

## Prérequis

- **Java Development Kit (JDK) :** Version 8 ou supérieure.  
- **GroupDocs.Redaction Library :** Bibliothèque principale pour les tâches de rédaction.  
- **IDE :** IntelliJ IDEA, Eclipse ou tout éditeur compatible Java.  
- **Maven :** Pour la gestion des dépendances.  

### Prérequis de connaissances
Une familiarité avec Java I/O et les concepts de base de la programmation orientée objet facilitera la compréhension des exemples.

## Configuration de GroupDocs.Redaction pour Java

### Configuration Maven
Incluez la configuration suivante dans votre fichier `pom.xml` pour accéder aux bibliothèques GroupDocs via Maven :

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
Alternativement, téléchargez la dernière version directement depuis [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisition de licence
1. **Essai gratuit :** Accédez aux fonctionnalités de base sans restrictions.  
2. **Licence temporaire :** Obtenez une licence temporaire pour explorer les fonctionnalités avancées.  
3. **Achat :** Pour une utilisation à long terme, envisagez d’acheter une licence complète.

#### Initialisation et configuration de base
Initialisez votre projet en ajoutant les imports nécessaires :

```java
import com.groupdocs.redaction.Redactor;
```

Avec cette configuration, vous êtes prêt à implémenter les fonctionnalités de rédaction de documents.

## Guide d'implémentation

### Fonctionnalité 1 : charger le document depuis un flux

**Vue d'ensemble :** Apprenez à charger des documents dans un `InputStream` pour les traiter.

`InputStream` est une classe Java I/O qui représente un flux d’octets, vous permettant de lire des données depuis des fichiers, des connexions réseau ou d’autres sources sans charger l’intégralité du contenu en mémoire.

#### Étape 1.1 : créer InputStream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Pourquoi :** L’utilisation de `InputStream` vous permet de gérer des documents stockés à divers emplacements — seaux cloud, bases de données ou tampons en mémoire — sans les écrire d’abord sur le disque. Cette approche est essentielle lorsque vous devez **load document from stream** dans des architectures micro‑services.

### Fonctionnalité 2 : appliquer la suppression d'annotation

**Vue d'ensemble :** Supprimez les annotations de votre document en utilisant le `DeleteAnnotationRedaction`.

`DeleteAnnotationRedaction` est une opération de rédaction qui élimine toutes les annotations — commentaires, surlignages et notes — du document.

#### Étape 2.1 : appliquer DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Pourquoi :** Cette étape garantit que toutes les annotations sensibles (commentaires, surlignages ou notes cachées) sont retirées du document, renforçant la confidentialité et la conformité.

### Fonctionnalité 3 : enregistrer le document avec des options

**Vue d'ensemble :** Apprenez à enregistrer votre document traité avec des options spécifiques comme la rasterisation et **add suffix filename java**.

`SaveOptions` regroupe les paramètres qui contrôlent la façon dont le document masqué est écrit, incluant le format, la rasterisation et les conventions de nommage.

#### Étape 3.1 : configurer SaveOptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Pourquoi :** Personnaliser les options d’enregistrement permet des formats de sortie flexibles et des conventions de nommage adaptées. Activer `setAddSuffix(true)` **adds suffix to filename**, rendant ainsi évident que le fichier a été masqué.

## Comment ajouter un suffixe au nom de fichier Java lors de l'enregistrement d'un document ?

La classe `Redactor` est le composant central qui charge un document et applique les opérations de rédaction. `SaveOptions` définit comment le document masqué est enregistré, incluant le format, la rasterisation et les conventions de nommage. Créez une instance `Redactor`, appliquez les rédactions nécessaires, puis configurez un objet `SaveOptions` avec `setAddSuffix(true)`. Appelez `redactor.save(outputPath, options)`. Le SDK ajoute automatiquement « _redacted » (ou le suffixe configuré) au nom du fichier, vous n’avez donc jamais besoin de le renommer manuellement.

## Aperçu de la dépendance Maven GroupDocs

La **groupdocs maven dependency** intègre l’ensemble du SDK Redaction dans votre projet via une unique entrée `<dependency>`. Elle gère les dépendances transitives, maintient les bibliothèques à jour et simplifie l’automatisation du build. En déclarant la dépendance dans `pom.xml`, vous évitez la gestion manuelle des JAR et assurez la compatibilité avec les derniers correctifs de sécurité.

## Pourquoi l'ajout d'un suffixe est important

L’ajout d’un suffixe fournit une confirmation visuelle immédiate qu’un fichier a été traité, ce qui est crucial pour les pistes d’audit, les flux de travail automatisés et la conformité réglementaire. Il permet aux scripts de filtrer les fichiers masqués, empêche la distribution accidentelle du contenu original, et satisfait de nombreuses normes industrielles exigeant un marquage clair des documents assainis.

## Applications pratiques

Explorez ces cas d’utilisation réels :

1. **Rédaction de documents juridiques :** Sécurisez les contrats avant de les partager avec les clients.  
2. **Gestion des dossiers médicaux :** Protégez les identifiants des patients tout en conservant les données cliniques.  
3. **Rapports financiers :** Gardez les chiffres sensibles confidentiels lors des audits externes.  
4. **Intégration CRM :** Rédigez automatiquement les données client avant l’exportation vers des outils tiers.  
5. **Outils de collaboration :** Assurez‑vous que les brouillons partagés n’exposent jamais de commentaires ou métadonnées cachés.

## Considérations de performance

### Optimisation des performances
- Utilisez le streaming (**load document from stream**) pour éviter de charger des fichiers entiers en mémoire.  
- Fermez rapidement les instances `Redactor` pour libérer les ressources.  

### Directives d'utilisation des ressources
- Surveillez le CPU et la mémoire pendant les exécutions par lots.  
- Privilégiez `ByteArrayOutputStream` pour les sauvegardes en mémoire lorsque les tailles de fichiers sont modestes.  

### Bonnes pratiques pour la gestion de la mémoire Java
- Réutilisez les objets `Redactor` lors du traitement de plusieurs fichiers du même type.  
- Invoquez `close()` dans un bloc `try‑with‑resources` pour éviter les fuites.

## Problèmes courants et solutions

| Problème | Cause | Solution |
|----------|-------|----------|
| **Suffix absent** | `setAddSuffix(false)` ou appel manquant | Assurez‑vous que `options.setAddSuffix(true)` est défini avant `save()`. |
| **OutOfMemoryError sur un gros DOCX** | Chargement du fichier entier en mémoire | Passez au chargement via `InputStream` (voir Fonctionnalité 1). |
| **Annotations toujours visibles** | Redaction non appliquée avant l'enregistrement | Appelez `redactor.apply(new DeleteAnnotationRedaction())` avant `save()`. |
| **Rasterisation PDF non appliquée** | `setRasterizeToPDF(false)` ou omis | Définissez `options.setRasterizeToPDF(true)` lorsque vous avez besoin d’un PDF aplati. |

## Questions fréquemment posées

**Q : Puis‑je masquer des documents PDF avec GroupDocs.Redaction ?**  
R : Oui, la bibliothèque prend en charge les PDF, DOCX, PPTX, XLSX et de nombreux autres formats.

**Q : Quelle est la meilleure façon de gérer les gros fichiers avec GroupDocs.Redaction ?**  
R : Utilisez le streaming (**load document from stream**) et fermez les ressources rapidement pour maintenir une faible consommation de mémoire.

**Q : Est‑il possible de personnaliser le texte du suffixe ?**  
R : L’API ajoute automatiquement un suffixe par défaut (par ex. « _redacted »). Pour des suffixes personnalisés, renommez le fichier de sortie après l’enregistrement.

**Q : Comment obtenir une licence temporaire pour GroupDocs.Redaction ?**  
R : Visitez la [Temporary License page](https://purchase.groupdocs.com/temporary-license/) et suivez les instructions.

**Q : Où puis‑je obtenir de l’aide en cas de problème ?**  
R : Rejoignez le [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) pour une assistance experte.

## Ressources
- **Documentation :** Explorez les guides détaillés sur [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **Référence API :** Accédez aux détails complets de l’API sur [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Téléchargement :** Obtenez la dernière version depuis [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **Référentiel GitHub :** Contribuez ou explorez le code source sur [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Last Updated:** 2026-11-02  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

## Tutoriels associés

- [Convertir Word en PDF et enregistrer les documents masqués avec GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Aperçu des pages de document Java Chargement avec GroupDocs.Redaction](/redaction/java/document-loading/)
- [Techniques avancées de masquage pour GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)