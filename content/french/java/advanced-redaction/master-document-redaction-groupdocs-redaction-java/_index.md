---
date: '2026-05-22'
description: Apprenez comment ajouter un suffixe au nom de fichier Java en utilisant
  la dépendance GroupDocs Maven lors de la rédaction de documents. Comprend le chargement
  en streaming, la suppression d'annotations et les options d'enregistrement.
keywords:
- add suffix filename java
- groupdocs redaction java
- document redaction workflow
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  headline: Add suffix filename java with GroupDocs Maven
  type: TechArticle
- description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  name: Add suffix filename java with GroupDocs Maven
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
title: Ajouter un suffixe au nom de fichier Java avec GroupDocs Maven
type: docs
url: /fr/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Ajouter un suffixe au nom de fichier java avec GroupDocs Maven

Masquer les données confidentielles n'est que la moitié du combat — vous devez également vous assurer que le fichier enregistré indique clairement qu'il a été traité. **Utiliser la dépendance GroupDocs Maven rend cela simple**, vous permettant d'ajouter un suffixe au nom du fichier de sortie en quelques lignes de code. La méthode **add suffix filename java** est une configuration en une seule ligne qui étiquette instantanément vos fichiers masqués, vous aidant à rester conforme et prêt pour les audits.

## Réponses rapides
- **Que fait “add suffix to filename” ?**  
  Il ajoute un suffixe personnalisé (par ex., “_redacted”) au nom du fichier de sortie afin que vous puissiez identifier immédiatement les fichiers traités.  
- **Puis-je charger un document depuis un flux ?**  
  Oui — GroupDocs.Redaction prend en charge le chargement depuis n'importe quel `InputStream`, idéal pour le stockage cloud ou le traitement en mémoire.  
- **Ai-je besoin d'une licence pour cette fonctionnalité ?**  
  Un essai gratuit suffit pour la redaction de base ; une licence temporaire ou complète débloque toutes les options avancées, y compris la gestion du suffixe.  
- **Quels formats sont pris en charge ?**  
  La bibliothèque gère DOCX, PDF, PPTX, XLSX et bien d'autres.  
- **La rasterisation est‑elle requise pour la sortie PDF ?**  
  La rasterisation est facultative ; activez‑la lorsque vous devez aplatir le document pour une sécurité supplémentaire.

## Qu'est‑ce que add suffix filename java ?
La technique **add suffix filename java** ajoute une chaîne prédéfinie au nom du fichier lors de l'opération d'enregistrement, marquant clairement le document comme masqué. Cette convention simple empêche la distribution accidentelle des fichiers originaux non masqués et s'intègre parfaitement aux pipelines automatisés.

## Pourquoi utiliser GroupDocs.Redaction pour cette tâche ?
GroupDocs.Redaction offre une API Java fluide qui vous permet de combiner les actions de masquage avec des options de gestion de fichiers — comme **add suffix filename java** — en quelques lignes de code seulement. Le SDK prend en charge **plus de 50 formats d'entrée et de sortie** et peut traiter des documents de plusieurs centaines de pages sans charger le fichier complet en mémoire, offrant à la fois rapidité et faible empreinte mémoire.

## Prérequis
- **Java Development Kit (JDK) :** Version 8 ou supérieure.  
- **GroupDocs.Redaction Library :** Bibliothèque principale pour les tâches de masquage.  
- **IDE :** IntelliJ IDEA, Eclipse ou tout éditeur compatible Java.  
- **Maven :** Pour la gestion des dépendances.  

### Prérequis de connaissances
Une familiarité avec Java I/O et les concepts de base de la programmation orientée objet facilitera la compréhension des exemples.

## Configuration de GroupDocs.Redaction pour Java
### Configuration Maven
Incluez la configuration suivante dans votre fichier `pom.xml` pour accéder aux bibliothèques GroupDocs via Maven :

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
Vous pouvez également télécharger la dernière version directement depuis [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisition de licence
1. **Free Trial :** Accédez aux fonctionnalités de base sans restrictions.  
2. **Temporary License :** Obtenez une licence temporaire pour explorer les fonctionnalités avancées.  
3. **Purchase :** Pour une utilisation à long terme, envisagez d'acheter une licence complète.

#### Initialisation et configuration de base
Initialisez votre projet en ajoutant les imports nécessaires :

```java
import com.groupdocs.redaction.Redactor;
```

Avec cette configuration, vous êtes prêt à implémenter les fonctionnalités de masquage de documents.

## Guide d'implémentation

### Fonctionnalité 1 : Charger le document depuis un flux
**Aperçu :** Apprenez à charger des documents dans un `InputStream` pour le traitement.

#### Implémentation étape par étape
##### Étape 1.1 : Créer un InputStream

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

- **Pourquoi :** Utiliser `InputStream` vous permet de gérer des documents stockés à divers emplacements — seaux cloud, bases de données ou tampons en mémoire — sans les écrire d'abord sur le disque. Cette approche est essentielle lorsque vous devez **load document from stream** dans les architectures micro‑services.

### Fonctionnalité 2 : Appliquer la suppression d'annotation
**Aperçu :** Supprimez les annotations de votre document en utilisant le `DeleteAnnotationRedaction`.

#### Implémentation étape par étape
##### Étape 2.1 : Appliquer DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Pourquoi :** Cette étape garantit que toutes les annotations sensibles (commentaires, surlignages ou notes cachées) sont supprimées du document, améliorant la confidentialité et la conformité.

### Fonctionnalité 3 : Enregistrer le document avec des options
**Aperçu :** Apprenez à enregistrer votre document traité avec des options spécifiques comme la rasterisation et **add suffix filename java**.

#### Implémentation étape par étape
##### Étape 3.1 : Configurer SaveOptions

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

- **Pourquoi :** Personnaliser les options d'enregistrement permet des formats de sortie flexibles et des conventions de nommage. Activer `setAddSuffix(true)` **adds suffix to filename**, rendant évident que le fichier a été masqué.

## Comment ajouter suffix filename java lors de l'enregistrement d'un document ?
`Redactor` est la classe principale de GroupDocs.Redaction qui charge un document et applique des opérations de masquage.  
`setAddSuffix` est une méthode de `SaveOptions` qui active l'ajout automatique d'un suffixe au nom du fichier de sortie.  

Chargez votre instance `Redactor`, appliquez les masquages souhaités, puis appelez `save()` avec `SaveOptions` où `setAddSuffix(true)` est activé. Cette configuration unique ajoute automatiquement “_redacted” (ou le suffixe par défaut) au nom du fichier, éliminant le renommage manuel et réduisant les erreurs humaines. L'opération se termine en temps O(n) proportionnel à la taille du document et fonctionne pour tous les formats pris en charge.

## Aperçu de la dépendance groupdocs Maven
Le **groupdocs maven dependency** intègre l'ensemble du SDK Redaction dans votre projet avec une seule entrée `<dependency>`. Il gère les dépendances transitives, maintient les bibliothèques à jour et simplifie l'automatisation du build. En déclarant la dépendance dans `pom.xml`, vous évitez la gestion manuelle des JAR et assurez la compatibilité avec les derniers correctifs de sécurité.

## Pourquoi ajouter un suffixe est important
Ajouter un suffixe fournit une confirmation visuelle immédiate qu'un document a été traité, ce qui est essentiel pour les pistes d'audit, les flux de travail automatisés et la conformité réglementaire dans tous les secteurs.

- **Auditabilité :** Les équipes peuvent immédiatement identifier quels fichiers sont sûrs à distribuer.  
- **Automatisation :** Les scripts peuvent filtrer les fichiers par suffixe, évitant le traitement accidentel des documents originaux.  
- **Conformité :** De nombreuses réglementations exigent un étiquetage clair des documents assainis.  

## Applications pratiques
Explorez ces cas d'utilisation réels :

1. **Legal Document Redaction :** Sécurisez les contrats avant de les partager avec le client.  
2. **Medical Record Handling :** Protégez les identifiants des patients tout en préservant les données cliniques.  
3. **Financial Reporting :** Gardez les chiffres sensibles confidentiels lors des audits externes.  
4. **CRM Integration :** Masquez automatiquement les données client avant l'exportation vers des outils tiers.  
5. **Collaboration Tools :** Assurez-vous que les brouillons partagés n'exposent jamais de commentaires cachés ou de métadonnées.  

## Considérations de performance
### Optimisation des performances
- Utilisez le streaming (`load document from stream`) pour éviter de charger des fichiers entiers en mémoire.  
- Fermez rapidement les instances `Redactor` pour libérer les ressources.  

### Directives d'utilisation des ressources
- Surveillez le CPU et la mémoire pendant les exécutions par lots.  
- Privilégiez `ByteArrayOutputStream` pour les sauvegardes en mémoire lorsque vous travaillez avec des fichiers de taille modeste.  

### Bonnes pratiques pour la gestion de la mémoire Java
- Réutilisez les objets `Redactor` lors du traitement de plusieurs fichiers du même type.  
- Appelez `close()` dans un bloc `try‑with‑resources` pour éviter les fuites.  

## Problèmes courants et solutions
| Issue | Cause | Fix |
|-------|-------|-----|
| **Suffix absent** | `setAddSuffix(false)` ou appel manquant | Assurez‑vous que `options.setAddSuffix(true)` est défini avant `save()`. |
| **OutOfMemoryError sur un gros DOCX** | Chargement du fichier complet en mémoire | Passez au chargement via `InputStream` (voir Fonctionnalité 1). |
| **Annotations toujours visibles** | Masquage non appliqué avant l'enregistrement | Appelez `redactor.apply(new DeleteAnnotationRedaction())` avant `save()`. |
| **Rasterisation PDF non appliquée** | `setRasterizeToPDF(false)` ou omission | Définissez `options.setRasterizeToPDF(true)` lorsque vous avez besoin d'un PDF aplati. |

## Questions fréquentes

**Q : Puis‑je masquer des documents PDF avec GroupDocs.Redaction ?**  
R : Oui, la bibliothèque prend en charge les PDF, DOCX, PPTX, XLSX et de nombreux autres formats.

**Q : Quelle est la meilleure façon de gérer les gros fichiers avec GroupDocs.Redaction ?**  
R : Utilisez le streaming (`load document from stream`) et fermez rapidement les ressources pour maintenir une faible utilisation de la mémoire.

**Q : Est‑il possible de personnaliser le texte du suffixe ?**  
R : L'API ajoute automatiquement un suffixe par défaut (par ex., “_redacted”). Pour des suffixes personnalisés, renommez le fichier de sortie après l'enregistrement.

**Q : Comment obtenir une licence temporaire pour GroupDocs.Redaction ?**  
R : Consultez la [page Temporary License](https://purchase.groupdocs.com/temporary-license/) et suivez les instructions.

**Q : Où puis‑je obtenir de l'aide en cas de problème ?**  
R : Rejoignez le [Forum d'assistance GroupDocs](https://forum.groupdocs.com/c/redaction/33) pour une assistance experte.

## Ressources
- **Documentation :** Explorez des guides détaillés sur [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **Référence API :** Accédez aux détails complets de l'API sur [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Téléchargement :** Obtenez la dernière version depuis [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **Dépôt GitHub :** Contribuez ou explorez le code source sur [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Dernière mise à jour :** 2026-05-22  
**Testé avec :** GroupDocs.Redaction 24.9 for Java  
**Auteur :** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Tutoriels associés

- [Convertir Word en PDF et enregistrer les documents masqués avec GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Aperçu du chargement des pages de document Java avec GroupDocs.Redaction](/redaction/java/document-loading/)
- [Techniques avancées de masquage pour GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)