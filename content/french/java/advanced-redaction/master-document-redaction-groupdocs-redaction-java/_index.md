---
date: '2026-02-16'
description: Apprenez à utiliser la dépendance GroupDocs Maven pour ajouter un suffixe
  aux noms de fichiers lors de la rédaction de documents en Java. Comprend le chargement
  depuis un flux, la suppression d'annotations et les options d’enregistrement.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Dépendance Maven groupdocs – Ajouter un suffixe au nom de fichier en Java
type: docs
url: /fr/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Comment ajouter un suffixe au nom de fichier lors de la rédaction de documents en Java avec GroupDocs.Redaction

La rédaction de données confidentielles n'est que la moitié du combat — vous devez également vous assurer que le fichier enregistré indique clairement qu'il a été traité. **Utiliser la dépendance Maven groupdocs rend cela simple**, vous permettant d'ajouter un suffixe au nom du fichier de sortie en quelques lignes de code seulement. Dans ce guide, vous apprendrez comment ajouter un suffixe au nom de fichier lors de l'enregistrement d'un document rédigé, ainsi que le chargement, l'annotation et l'enregistrement en utilisant GroupDocs.Redaction pour Java. Que vous protégiez des contrats juridiques, des dossiers médicaux ou des rapports financiers, ces étapes garderont votre flux de travail à la fois sécurisé et traçable.

## Réponses rapides
- **Que fait « add suffix to filename » ?**  
  Il ajoute un suffixe personnalisé (par ex., « _redacted ») au nom du fichier de sortie afin que vous puissiez identifier instantanément les fichiers traités.  
- **Puis-je charger un document depuis un flux ?**  
  Oui — GroupDocs.Redaction prend en charge le chargement depuis n'importe quel `InputStream`, idéal pour le stockage cloud ou le traitement en mémoire.  
- **Ai-je besoin d'une licence pour cette fonctionnalité ?**  
  Un essai gratuit suffit pour la rédaction de base ; une licence temporaire ou complète débloque toutes les options avancées, y compris la gestion du suffixe.  
- **Quels formats sont pris en charge ?**  
  La bibliothèque gère DOCX, PDF, PPTX, XLSX et bien d'autres.  
- **La rasterisation est‑elle requise pour la sortie PDF ?**  
  La rasterisation est optionnelle ; activez‑la lorsque vous devez aplatir le document pour une sécurité supplémentaire.  

## Qu'est‑ce que l'ajout d'un suffixe à un nom de fichier ?
Ajouter un suffixe est une convention de nommage simple qui indique qu'un fichier a été rédigé. Cela empêche le partage accidentel des versions originales non rédigées et aide les pipelines automatisés à suivre l'état du traitement.

## Pourquoi utiliser GroupDocs.Redaction pour cette tâche ?
GroupDocs.Redaction fournit une API Java fluide qui vous permet de combiner les actions de rédaction avec des options de gestion de fichiers — comme **l'ajout d'un suffixe au nom de fichier** — en quelques lignes de code seulement. Cela fait gagner du temps de développement et réduit le risque d'erreurs manuelles.

## Prérequis
- **Java Development Kit (JDK) :** Version 8 ou supérieure.  
- **GroupDocs.Redaction Library :** Bibliothèque principale pour les tâches de rédaction.  
- **IDE :** IntelliJ IDEA, Eclipse ou tout éditeur compatible Java.  
- **Maven :** Pour la gestion des dépendances.  

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
Sinon, téléchargez la dernière version directement depuis [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisition de licence
1. **Free Trial :** Accédez aux fonctionnalités de base sans restrictions.  
2. **Temporary License :** Obtenez une licence temporaire pour explorer les fonctionnalités avancées.  
3. **Purchase :** Pour une utilisation à long terme, envisagez d'acheter une licence complète.

#### Initialisation et configuration de base
Initialisez votre projet en ajoutant les imports nécessaires :

```java
import com.groupdocs.redaction.Redactor;
```

Avec cette configuration, vous êtes prêt à implémenter les fonctionnalités de rédaction de documents.

## Guide d'implémentation

### Fonctionnalité 1 : Charger le document depuis un flux
**Aperçu :** Apprenez comment charger des documents dans un `InputStream` pour le traitement.

#### Implémentation étape par étape
##### Étape 1.1 : Créer InputStream

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

- **Pourquoi :** Utiliser `InputStream` vous permet de gérer des documents stockés dans divers formats de manière fluide, ce qui est essentiel lorsque vous devez **load document from stream** dans des scénarios cloud ou micro‑service.

### Fonctionnalité 2 : Appliquer la suppression d'annotation
**Aperçu :** Supprimez les annotations de votre document en utilisant le `DeleteAnnotationRedaction`.

#### Implémentation étape par étape
##### Étape 2.1 : Appliquer DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Pourquoi :** Cette étape garantit que toutes les annotations sensibles sont supprimées, améliorant la confidentialité du document.

### Fonctionnalité 3 : Enregistrer le document avec des options
**Aperçu :** Apprenez comment enregistrer votre document traité avec des options spécifiques comme la rasterisation et **l'ajout d'un suffixe au nom de fichier**.

#### Implémentation étape par étape
##### Étape 3.1 : Configurer SaveOptions

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

- **Pourquoi :** Personnaliser les options d'enregistrement permet des formats de sortie flexibles et des conventions de nommage. Activer `setAddSuffix(true)` **adds suffix to filename**, rendant clair que le fichier a été rédigé.

## Aperçu de la dépendance Maven groupdocs
La **dépendance Maven groupdocs** intègre l'ensemble du SDK Redaction dans votre projet avec une seule entrée `<dependency>`. Elle gère les dépendances transitives, maintient les bibliothèques à jour et simplifie l'automatisation du build. En déclarant la dépendance dans `pom.xml`, vous évitez la gestion manuelle des JAR et assurez la compatibilité avec les derniers correctifs de sécurité.

## Pourquoi l'ajout d'un suffixe est important
- **Auditabilité :** Les équipes peuvent identifier instantanément quels fichiers sont sûrs à distribuer.  
- **Automatisation :** Les scripts peuvent filtrer les fichiers par suffixe, évitant le traitement accidentel des documents originaux.  
- **Conformité :** De nombreuses réglementations exigent un étiquetage clair des documents assainis.  

## Applications pratiques
Explorez ces cas d'utilisation réels :

1. **Legal Document Redaction :** Sécurisez les contrats avant de les partager avec le client.  
2. **Medical Record Handling :** Protégez les identifiants des patients.  
3. **Financial Reporting :** Gardez les chiffres sensibles confidentiels.  
4. **CRM Integration :** Redigez automatiquement les données client avant l'export.  
5. **Collaboration Tools :** Assurez-vous que les brouillons partagés n'exposent jamais les commentaires cachés.  

## Considérations de performance
### Optimisation des performances
- Utilisez le streaming (`load document from stream`) pour éviter de charger des fichiers entiers en mémoire.  
- Fermez rapidement les instances de `Redactor` pour libérer les ressources.

### Directives d'utilisation des ressources
- Surveillez le CPU et la mémoire pendant les exécutions par lots.  
- Privilégiez `ByteArrayOutputStream` pour les sauvegardes en mémoire lorsque vous travaillez avec des fichiers de taille modeste.

### Meilleures pratiques pour la gestion de la mémoire Java
- Réutilisez les objets `Redactor` lors du traitement de plusieurs fichiers du même type.  
- Appelez `close()` dans un bloc `try‑with‑resources` pour éviter les fuites.

## Problèmes courants et solutions
| Problème | Cause | Solution |
|----------|-------|----------|
| **Le suffixe n'apparaît pas** | `setAddSuffix(false)` ou appel manquant | Assurez‑vous que `options.setAddSuffix(true)` est défini avant `save()`. |
| **OutOfMemoryError sur un DOCX volumineux** | Chargement du fichier complet en mémoire | Passez au chargement via `InputStream` (voir Fonctionnalité 1). |
| **Annotations toujours visibles** | Rédaction non appliquée avant l'enregistrement | Appelez `redactor.apply(new DeleteAnnotationRedaction())` avant `save()`. |
| **Rasterisation PDF non appliquée** | `setRasterizeToPDF(false)` ou omis | Définissez `options.setRasterizeToPDF(true)` lorsque vous avez besoin d'un PDF aplati. |

## Questions fréquemment posées

**Q : Puis‑je rédiger des documents PDF avec GroupDocs.Redaction ?**  
R : Oui, la bibliothèque prend en charge les PDF, DOCX, PPTX, XLSX et de nombreux autres formats.

**Q : Quelle est la meilleure façon de gérer les gros fichiers avec GroupDocs.Redaction ?**  
R : Utilisez le streaming (`load document from stream`) et fermez rapidement les ressources pour maintenir une faible utilisation de la mémoire.

**Q : Est‑il possible de personnaliser le texte du suffixe ?**  
R : L'API ajoute automatiquement un suffixe par défaut (par ex., « _redacted »). Pour des suffixes personnalisés, vous pouvez renommer le fichier de sortie après l'enregistrement.

**Q : Comment obtenir une licence temporaire pour GroupDocs.Redaction ?**  
R : Visitez la [Temporary License page](https://purchase.groupdocs.com/temporary-license/) et suivez les instructions.

**Q : Où puis‑je obtenir de l'aide en cas de problème ?**  
R : Rejoignez le [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) pour une assistance experte.

## Ressources
- **Documentation :** Explorez des guides détaillés sur [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference :** Accédez aux détails complets de l'API sur [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download :** Obtenez la dernière version depuis [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository :** Contribuez ou explorez le code source sur [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Dernière mise à jour :** 2026-02-16  
**Testé avec :** GroupDocs.Redaction 24.9 pour Java  
**Auteur :** GroupDocs  

---