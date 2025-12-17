---
date: '2025-12-17'
description: Apprenez à ajouter un suffixe au nom de fichier et à masquer les informations
  sensibles des documents à l'aide de GroupDocs.Redaction pour Java. Renforcez efficacement
  la sécurité et la confidentialité des documents.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Comment ajouter un suffixe au nom de fichier lors de la rédaction de documents
  en Java avec GroupDocs.Redaction
type: docs
url: /fr/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Comment ajouter un suffixe au nom de fichier lors de la rédaction de documents en Java avec GroupDocs.Redaction

Masquer les données confidentielles n’est que la moitié du combat — vous devez également vous assurer que le fichier enregistré indique clairement qu’il a été traité. Dans ce guide, vous apprendrez **comment ajouter un suffixe au nom de fichier** lors de l’enregistrement d’un document masqué, ainsi que le chargement, l’annotation et l’enregistrement à l’aide de GroupDocs.Redaction pour Java. Que vous protégiez des contrats juridiques, des dossiers médicaux ou des rapports financiers, ces étapes garantiront que votre flux de travail reste sécurisé et traçable.

## Réponses rapides
- **Que fait « ajouter un suffixe au nom de fichier » ?**  
  Il ajoute un suffixe personnalisé (par ex. « _redacted ») au nom du fichier de sortie afin que vous puissiez identifier immédiatement les fichiers traités.
- **Puis‑je charger un document depuis un flux ?**  
  Oui — GroupDocs.Redaction prend en charge le chargement depuis n’importe quel `InputStream`, idéal pour le stockage cloud ou le traitement en mémoire.
- **Ai‑je besoin d’une licence pour cette fonctionnalité ?**  
  Un essai gratuit suffit pour les masquages de base ; une licence temporaire ou complète débloque toutes les options avancées, y compris la gestion du suffixe.
- **Quels formats sont pris en charge ?**  
  La bibliothèque gère DOCX, PDF, PPTX, XLSX et bien d’autres.
- **La rasterisation est‑elle requise pour la sortie PDF ?**  
  La rasterisation est optionnelle ; activez‑la lorsque vous devez aplatir le document pour une sécurité supplémentaire.

## Qu’est‑ce que l’ajout d’un suffixe à un nom de fichier ?
Ajouter un suffixe est une convention de nommage simple qui indique qu’un fichier a été masqué. Cela empêche le partage accidentel de versions originales non masquées et aide les pipelines automatisés à suivre l’état du traitement.

## Pourquoi utiliser GroupDocs.Redaction pour cette tâche ?
GroupDocs.Redaction fournit une API Java fluide qui vous permet de combiner les actions de masquage avec des options de gestion de fichiers — comme **ajouter un suffixe au nom de fichier**—en quelques lignes de code seulement. Cela fait gagner du temps de développement et réduit le risque d’erreurs manuelles.

## Prérequis

- **Java Development Kit (JDK) :** Version 8 ou supérieure.
- **Bibliothèque GroupDocs.Redaction :** Bibliothèque principale pour les tâches de masquage.
- **IDE :** IntelliJ IDEA, Eclipse ou tout éditeur compatible Java.
- **Maven :** Pour la gestion des dépendances.

### Prérequis de connaissances
Une familiarité avec les entrées/sorties Java et les concepts de base de la programmation orientée objet facilitera la compréhension des exemples.

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
Vous pouvez également télécharger la dernière version directement depuis [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisition de licence
1. **Essai gratuit :** Accédez aux fonctionnalités de base sans restriction.  
2. **Licence temporaire :** Obtenez une licence temporaire pour explorer les fonctionnalités avancées.  
3. **Achat :** Pour une utilisation à long terme, envisagez d’acheter une licence complète.

#### Initialisation et configuration de base
Initialisez votre projet en ajoutant les imports nécessaires :

```java
import com.groupdocs.redaction.Redactor;
```

Avec cette configuration, vous êtes prêt à implémenter les fonctionnalités de masquage de documents.

## Guide d’implémentation

### Fonctionnalité 1 : Charger le document depuis un flux
**Vue d’ensemble :** Apprenez à charger des documents dans un `InputStream` pour les traiter.

#### Implémentation étape par étape
##### Étape 1.1 : Créer l’`InputStream`

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

- **Pourquoi :** Utiliser `InputStream` vous permet de gérer des documents stockés dans divers formats de manière transparente, ce qui est essentiel lorsque vous devez **charger le document depuis un flux** dans le cloud ou des scénarios de micro‑services.

### Fonctionnalité 2 : Appliquer le masquage de suppression d’annotation
**Vue d’ensemble :** Supprimez les annotations de votre document à l’aide du `DeleteAnnotationRedaction`.

#### Implémentation étape par étape
##### Étape 2.1 : Appliquer `DeleteAnnotationRedaction`

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Pourquoi :** Cette étape garantit que toutes les annotations sensibles sont supprimées, renforçant la confidentialité du document.

### Fonctionnalité 3 : Enregistrer le document avec des options
**Vue d’ensemble :** Apprenez à enregistrer votre document traité avec des options spécifiques comme la rasterisation et **l’ajout d’un suffixe au nom de fichier**.

#### Implémentation étape par étape
##### Étape 3.1 : Configurer `SaveOptions`

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

- **Pourquoi :** Personnaliser les options d’enregistrement permet des formats de sortie flexibles et des conventions de nommage. Activer `setAddSuffix(true)` **ajoute un suffixe au nom de fichier**, rendant clair que le fichier a été masqué.

## Pourquoi le suffixe est‑il important ?
- **Traçabilité :** Les équipes peuvent repérer instantanément quels fichiers sont sûrs à distribuer.
- **Automatisation :** Les scripts peuvent filtrer les fichiers par suffixe, évitant le traitement accidentel des documents originaux.
- **Conformité :** De nombreuses réglementations exigent un marquage clair des documents assainis.

## Applications pratiques
Explorez ces cas d’utilisation réels :
1. **Masquage de documents juridiques :** Sécurisez les contrats avant de les partager avec le client.  
2. **Gestion des dossiers médicaux :** Protégez les identifiants des patients.  
3. **Rapports financiers :** Gardez les chiffres sensibles confidentiels.  
4. **Intégration CRM :** Masquez automatiquement les données client avant l’exportation.  
5. **Outils de collaboration :** Assurez‑vous que les brouillons partagés n’exposent jamais les commentaires cachés.

## Considérations de performance
### Optimisation des performances
- Utilisez le streaming (`load document from stream`) pour éviter de charger des fichiers entiers en mémoire.  
- Fermez rapidement les instances de `Redactor` pour libérer les ressources.

### Directives d’utilisation des ressources
- Surveillez le CPU et la mémoire pendant les exécutions par lots.  
- Privilégiez `ByteArrayOutputStream` pour les sauvegardes en mémoire lorsque vous travaillez avec des fichiers de taille modeste.

### Bonnes pratiques de gestion de la mémoire Java
- Réutilisez les objets `Redactor` lors du traitement de plusieurs fichiers du même type.  
- Appelez `close()` dans un bloc `finally` ou avec try‑with‑resources pour éviter les fuites.

## Problèmes courants et solutions
| Problème | Cause | Solution |
|----------|-------|----------|
| **Le suffixe n’apparaît pas** | `setAddSuffix(false)` ou appel manquant | Assurez‑vous que `options.setAddSuffix(true)` est défini avant `save()`.| **OutOfMemoryError sur un DOCX volumineux** | Chargement du fichier complet en mémoire | Passez au chargement via `InputStream` (voir Fonctionnalité 1). |
| **Annotations toujours visibles** | Masquage non appliqué avant l’enregistrement | Appelez `redactor.apply(new DeleteAnnotationRedaction())` avant `save()`. |
| **Rasterisation PDF non appliquée** | `setRasterizeToPDF(false)` ou omission | Définissez `options.setRasterizeToPDF(true)` lorsque vous avez besoin d’un PDF aplati. |

## Foire aux questions

**Q : Puis‑je masquer des documents PDF avec GroupDocs.Redaction ?**  
R : Oui, la bibliothèque prend en charge les PDF, DOCX, PPTX, XLSX et de nombreux autres formats.

**Q : Quelle est la meilleure façon de gérer les gros fichiers avec GroupDocs.Redaction ?**  
R : Utilisez le streaming (`load document from stream`) et fermez les ressources rapidement afin de maintenir une faible consommation de mémoire.

**Q : Est‑il possible de personnaliser le texte du suffixe ?**  
R : L’API ajoute automatiquement un suffixe par défaut (par ex. « _redacted »). Pour des suffixes personnalisés, vous pouvez renommer le fichier de sortie après l’enregistrement.

**Q : Comment obtenir une licence temporaire pour GroupDocs.Redaction ?**  
R : Visitez la [page Licence temporaire](https://purchase.groupdocs.com/temporary-license/) et suivez les instructions.

**Q : Où puis‑je obtenir de l’aide en cas de problème ?**  
R : Rejoignez le [Forum de support GroupDocs](https://forum.groupdocs.com/c/redaction/33) pour obtenir de l’assistance d’experts.

## Ressources
- **Documentation :** Explorez les guides détaillés sur [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **Référence API :** Accédez aux détails complets de l’API sur [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Téléchargement :** Obtenez la dernière version depuis [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **Référentiel GitHub :** Contribuez ou explorez le code source sur [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Dernière mise à jour :** 2025-12-17  
**Testé avec :** GroupDocs.Redaction 24.9 pour Java  
**Auteur :** GroupDocs  

---