---
date: '2026-02-26'
description: Apprenez à censurer du texte en utilisant GroupDocs.Redaction Java et
  à l’enregistrer en PDF rasterisé avec un remplacement exact de la phrase et des
  paramètres PDF personnalisés.
keywords:
- GroupDocs.Redaction Java
- text redaction Java
- rasterized PDF conversion
title: Comment caviarder du texte avec GroupDocs.Redaction Java
type: docs
url: /fr/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# Comment caviarder du texte avec GroupDocs.Redaction Java

Dans le monde actuel axé sur les données, **comment caviarder du texte** dans un document de manière sûre et efficace est une préoccupation majeure pour les développeurs et les responsables de conformité. Que vous ayez besoin de masquer des identifiants personnels, des détails confidentiels de clients ou des codes de projet internes, GroupDocs.Redaction pour Java vous offre un moyen fiable de localiser des phrases exactes et de les remplacer par des superpositions sécurisées. Ce tutoriel vous montre également **comment enregistrer en PDF rasterisé**, transformant chaque page en un PDF basé sur des images qui répond aux normes d'archivage.

## Réponses rapides
- **Quelle est la classe principale pour la caviature ?** `Redactor`  
- **Puis-je remplacer une phrase par une superposition colorée ?** Oui, en utilisant `ExactPhraseRedaction` et `ReplacementOptions`.  
- **Comment générer un PDF rasterisé ?** Activer la rasterisation via `SaveOptions.getRasterization().setEnabled(true)`.  
- **Quel niveau de conformité PDF est utilisé dans l'exemple ?** `PdfComplianceLevel.PdfA1a`.  
- **Ai-je besoin d'une licence pour une utilisation en production ?** Une licence valide GroupDocs.Redaction est requise pour les déploiements en production.

## Qu’est‑ce que “caviarder du texte” en Java ?
La caviature est le processus de suppression ou d’obscurcissement permanent du contenu sensible d’un fichier. Avec GroupDocs.Redaction, vous pouvez rechercher programmatiquement une phrase exacte — comme un nom ou un identifiant — et la remplacer par une superposition rouge, une boîte noire ou tout élément visuel personnalisé, garantissant que les données originales ne puissent pas être récupérées.

## Pourquoi utiliser GroupDocs.Redaction pour Java ?
- **Correspondance exacte de phrase** élimine les faux positifs.  
- **Rasterisation intégrée** vous permet de créer des PDF conformes PDF/A, uniquement image, pour le stockage à long terme.  
- **Support multi‑format** fonctionne avec DOCX, PDF, PPTX, et plus, vous permettant d’appliquer le même code à différents types de documents.  
- **API axée sur la performance** vous permet de traiter par lots de grands ensembles de documents tout en maintenant une faible utilisation de la mémoire.

## Prérequis
Avant de commencer, assurez-vous de disposer de ce qui suit :
- **GroupDocs.Redaction for Java** (v24.9 ou plus récent).  
- **Java Development Kit (JDK) 8+**.  
- Un IDE tel qu’IntelliJ IDEA, Eclipse ou NetBeans.  
- Maven pour la gestion des dépendances.

### Bibliothèques et dépendances requises
- **GroupDocs.Redaction for Java** – ajoutez le dépôt et la dépendance à votre `pom.xml` (voir le bloc de code ci‑dessous).  
- **Optionnel** : toute bibliothèque de journalisation supplémentaire que vous préférez.

### Prérequis de connaissances
- Syntaxe Java de base et I/O de fichiers.  
- Familiarité avec la structure `pom.xml` de Maven.

## Configuration de GroupDocs.Redaction pour Java
### Configuration Maven
Add the repository and dependency to your `pom.xml` file:

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
Sinon, vous pouvez télécharger la dernière version directement depuis [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisition de licence
- **Essai gratuit** – explorez l’API sans clé de licence.  
- **Licence temporaire** – à utiliser pour une évaluation prolongée.  
- **Licence complète** – requise pour les environnements de production.

### Initialisation et configuration de base
Below is the minimal code to create a `Redactor` instance pointing at a sample DOCX file:

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## Comment caviarder du texte – Exemple de phrase exacte
### Étape 1 : Importer les classes requises
These imports give you access to the redaction engine and replacement options:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

### Étape 2 : Créer et appliquer la caviature
The following snippet searches for the phrase **“John Doe”** and replaces it with a red overlay:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

**Pourquoi c’est important :** `ReplacementOptions` vous permet de contrôler le style visuel de la caviature, garantissant que le contenu masqué ne puisse pas être récupéré par copier‑coller ou OCR.

## Comment enregistrer en PDF rasterisé
### Étape 1 : Importer les classes SaveOptions
These classes let you configure PDF output, including rasterization and compliance levels:

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

### Étape 2 : Configurer et appliquer les options d’enregistrement
After redacting, you can export the document as a rasterized PDF. The example below rasterizes page 5 only and forces PDF/A‑1a compliance:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

**Point clé :** Rasteriser un PDF **convertit chaque page en image**, ce qui supprime les couches de texte cachées et rend le document inviolable—idéal pour l’archivage juridique.

## Applications pratiques
1. **Caviature de données sensibles** – Masquer automatiquement les identifiants personnels avant de partager des contrats.  
2. **Archivage de documents** – Convertir les rapports finalisés en PDF/A rasterisé pour la conformité à long terme.  
3. **Mise à jour massive de contenu** – Remplacer la terminologie obsolète dans des centaines de fichiers avec un seul script.

## Considérations de performance
- **Fermez le `Redactor`** après chaque opération pour libérer les poignées de fichiers et la mémoire.  
- **Traitement par lots** – Chargez une liste de fichiers et parcourez‑les, en réutilisant une seule instance de `Redactor` lorsque c’est possible.  
- **Surveillez les ressources** – Utilisez des outils de profilage Java pour observer l’utilisation du CPU et du tas pendant les caviatures à grande échelle.

## Questions fréquentes

**Q : Comment installer GroupDocs.Redaction dans un projet Maven ?**  
R : Ajoutez le dépôt GroupDocs et la dépendance `groupdocs-redaction` à votre `pom.xml` comme indiqué dans la section Configuration Maven.

**Q : Puis‑je caviarder du texte à partir de fichiers PDF avec cette bibliothèque ?**  
R : Oui, GroupDocs.Redaction prend en charge PDF, DOCX, PPTX et de nombreux autres formats.

**Q : Que se passe‑t‑il si la phrase exacte n’est pas trouvée ?**  
R : Le `RedactorChangeLog` renverra un statut `Failed`. Vérifiez l’orthographe et la sensibilité à la casse de la phrase.

**Q : Comment gérer efficacement des documents très volumineux ?**  
R : Traitez‑les par plages de pages plus petites, activez la rasterisation uniquement où nécessaire, et fermez toujours le `Redactor` pour libérer les ressources.

**Q : Est‑il possible d’enregistrer des PDF rasterisés avec des plages de pages spécifiques ?**  
R : Absolument. Utilisez `options.getRasterization().setPageIndex()` et `setPageCount()` pour cibler les pages exactes que vous souhaitez rasteriser.

## Conclusion
Vous disposez maintenant d’un guide complet, de bout en bout, sur **comment caviarder du texte** avec GroupDocs.Redaction Java et **enregistrer en PDF rasterisé**. En suivant ces étapes, vous pouvez protéger les informations sensibles, respecter les exigences de conformité et maintenir des performances élevées dans les charges de travail de production.

**Prochaines étapes**  
- Approfondissez l’API en explorant la [documentation officielle](https://docs.groupdocs.com/redaction/java/).  
- Expérimentez d’autres types de caviature (p. ex., `RegexRedaction`, `ImageRedaction`).  
- Rejoignez la communauté sur le [Forum d’assistance GroupDocs](https://forum.groupdocs.com/c/redaction/33) pour des astuces et meilleures pratiques.

---

**Dernière mise à jour :** 2026-02-26  
**Testé avec :** GroupDocs.Redaction Java 24.9  
**Auteur :** GroupDocs