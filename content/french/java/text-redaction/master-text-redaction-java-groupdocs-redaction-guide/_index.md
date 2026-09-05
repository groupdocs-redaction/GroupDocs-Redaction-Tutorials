---
date: '2026-08-20'
description: Découvrez comment caviarder du texte avec des regex en Java grâce à GroupDocs.Redaction.
  Ce tutoriel pas à pas vous montre comment appliquer les regex, configurer les options
  d’enregistrement et protéger les données sensibles.
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: Apprenez à caviarder du texte en Java avec GroupDocs.Redaction. Ce
  guide explique la caviardage avec regex, la configuration des options d’enregistrement
  et des conseils de performance pour protéger les données sensibles.
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: Comment caviarder du texte en Java avec GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 'Comment caviarder du texte en Java avec GroupDocs.Redaction : guide complet'
type: docs
url: /fr/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# Comment masquer du texte en Java avec GroupDocs.Redaction : Guide complet

Dans le monde numérique d'aujourd'hui, **how to redact text** dans les documents est une question que de nombreux développeurs se posent. Que vous protégiez des données personnelles, que vous vous conformiez aux réglementations, ou que vous nettoyiez simplement des brouillons, ce guide vous montre comment utiliser GroupDocs.Redaction pour Java afin de **appliquer rapidement et en toute sécurité une rédaction basée sur des expressions régulières**. Vous apprendrez pourquoi la rédaction est importante, comment configurer la bibliothèque, et des conseils de bonnes pratiques pour un traitement haute performance.

## Réponses rapides
- **What is the primary purpose of GroupDocs.Redaction?** Il fournit une API fiable pour localiser et masquer le texte sensible dans plus de 50 formats de documents.  
- **How do I apply regex for redaction?** Créez un objet `RegexRedaction` avec votre motif et passez‑le à la méthode `Redactor.apply()`.  
- **Do I need a license?** Un essai gratuit fonctionne pour le développement ; une licence payante débloque toutes les fonctionnalités pour la production.  
- **Can I redact PDFs as well as DOCX files?** Oui—GroupDocs.Redaction prend en charge PDF, DOCX, PPTX et de nombreux autres formats.  
- **What’s the best way to improve performance?** Fermez rapidement les instances de `Redactor`, gardez les motifs regex simples, et traitez les fichiers par lots.  

## Qu’est-ce que la rédaction de texte et pourquoi est‑elle importante ?
La rédaction de texte supprime ou masque de façon permanente les informations sensibles d'un document, garantissant que les données confidentielles—telles que les numéros de sécurité sociale, les détails de cartes de crédit ou les dossiers médicaux—ne peuvent pas être récupérées ou visualisées par des parties non autorisées. Elle fonctionne en écrasant les caractères originaux ou en les remplaçant par un masque, de sorte que le contenu masqué ne puisse pas être extrait par copier‑coller ou des outils OCR. Cela assure la conformité aux réglementations sur la confidentialité et protège les individus contre le vol d'identité ou les violations de données.

## Pourquoi utiliser les regex pour la rédaction de texte ?
Les expressions régulières vous permettent de définir des motifs flexibles qui correspondent à une large gamme de formats de données (par ex., numéros de téléphone, numéros de cartes de crédit). Utiliser les regex avec GroupDocs.Redaction vous donne un contrôle précis sur ce qui est masqué, tout en gardant l'implémentation concise et maintenable.

## Prérequis
- **Java Development Kit (JDK)** installé (Java 8 ou plus récent).  
- Familiarité de base avec la syntaxe Java et les expressions régulières.  
- Un IDE tel que **IntelliJ IDEA** ou **Eclipse** pour exécuter et déboguer le code.  

## Configuration de GroupDocs.Redaction pour Java
Tout d'abord, ajoutez la bibliothèque à votre projet.

### Configuration Maven
Si vous utilisez Maven, insérez ce qui suit dans votre `pom.xml` :

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
Sinon, téléchargez le dernier JAR depuis [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Initialisation de base
`Redactor` est la classe principale qui ouvre un document, applique les règles de rédaction et écrit la sortie.

Une fois la bibliothèque disponible, vous pouvez commencer à rédiger les documents :

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## Comment rédiger du texte en utilisant des regex en Java ?
Le processus consiste à charger le fichier source dans une instance `Redactor`, créer une règle `RegexRedaction` qui définit le motif à correspondre, appliquer la règle avec `redactor.apply()`, et enfin enregistrer le document modifié à l'aide de `SaveOptions`. En suivant ces étapes, vous pouvez localiser et masquer de façon fiable toute chaîne sensible sur les formats pris en charge.

La classe `Redactor` est le composant central qui ouvre un document, applique les règles de rédaction et écrit le fichier de sortie. Elle gère les ressources en interne, vous devez donc la fermer après le traitement pour libérer la mémoire.

### Étape 1 : importer les classes requises
Les imports suivants vous donnent accès à l'API de rédaction :

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### Étape 2 : initialiser le redactor et appliquer le motif regex
`RegexRedaction` représente une règle de rédaction basée sur un motif d'expression régulière. Le motif que vous fournissez détermine quels fragments de texte sont remplacés.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **Regex explanation** : Le motif `\b\d{3}-\d{2}-\d{4}\b` correspond aux numéros de sécurité sociale américains (trois chiffres, un tiret, deux chiffres, un tiret, quatre chiffres). `ReplacementOptions` vous permet de choisir une superposition noire solide ou un masque de texte personnalisé.

### Étape 3 : configurer les options d'enregistrement
`SaveOptions` contrôle la façon dont le fichier rédigé est écrit. Ajouter un suffixe rend clair quels fichiers ont été traités, tout en préservant le format original pour éviter des conversions indésirables.

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **Save options** : `setAddSuffix(true)` ajoute automatiquement « _redacted » au nom du fichier de sortie, évitant les écrasements accidentels.

### Étape 4 : personnaliser les paramètres d'enregistrement supplémentaires
Vous pouvez affiner davantage la sortie—comme la préservation des métadonnées ou l'aplatissement des annotations—en ajustant l'objet `SaveOptions`.

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **Key configuration** : Le réglage `setPreserveMetadata(true)` conserve les propriétés originales du document, ce qui est souvent requis pour les audits de conformité.

## Applications pratiques
Scénarios réels où **how to redact text** est essentiel :
1. **Documents juridiques** – Masquez les identifiants des clients avant de partager les brouillons avec un conseiller externe.  
2. **Dossiers médicaux** – Masquez les noms des patients, les identifiants ou les numéros de santé pour rester conforme à la HIPAA.  
3. **Rapports financiers** – Supprimez les numéros de compte confidentiels lors de la distribution des résumés trimestriels.  

## Considérations de performance
- **Memory management** : Appelez toujours `redactor.close()` pour libérer les descripteurs de fichiers et les ressources natives.  
- **Efficient regex** : Les motifs plus simples s'exécutent plus rapidement ; évitez le back‑tracking excessif en utilisant des groupes atomiques lorsque c'est possible.  
- **Batch processing** : Pour de grands ensembles de documents, traitez les fichiers par lots de 20 à 50 afin de garder une utilisation du tas prévisible.  

## Problèmes courants et solutions
| Problème | Solution |
|----------|----------|
| **La regex correspond à trop de texte** | Testez votre motif avec un testeur de regex en ligne et restreignez les classes de caractères. |
| **Conflit de nom de fichier de sortie** | Utilisez `setAddSuffix(true)` ou fournissez un chemin de sortie personnalisé via `saveOptions.setOutputPath()`. |
| **Fuite de mémoire sur les gros PDFs** | Traitez les PDFs page par page ou augmentez la taille du tas JVM (`-Xmx2g`). |

## Questions fréquentes

**Q : Quel est le but de `setAddSuffix(true)` dans SaveOptions ?**  
A : Il ajoute automatiquement un suffixe (par ex., `_redacted`) au nom du fichier de sortie, rendant évident quels fichiers ont été traités.

**Q : Puis-je utiliser des motifs regex autres que des nombres pour la rédaction de texte ?**  
A : Absolument. Toute expression régulière Java valide peut être fournie à `RegexRedaction` pour cibler les e‑mails, numéros de téléphone, ID personnalisés, etc.

**Q : Comment devrais‑je gérer les erreurs pendant la rédaction ?**  
A : Enveloppez la logique de rédaction dans un bloc try‑catch, consignez l'exception, et fermez toujours le `Redactor` dans un bloc finally pour libérer les ressources.

**Q : La rédaction de PDF est‑elle prise en charge ?**  
A : Oui. GroupDocs.Redaction fonctionne avec PDF, DOCX, PPTX et de nombreux autres formats.

**Q : Quelles sont les meilleures pratiques pour les projets de rédaction à grande échelle ?**  
A : Utilisez le traitement par lots, gardez les motifs regex simples, et surveillez l'utilisation de la mémoire avec des outils de profilage.

## Ressources supplémentaires
- **Documentation** : [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API reference** : [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**Dernière mise à jour** : 2026-08-20  
**Testé avec** : GroupDocs.Redaction 24.9 for Java  
**Auteur** : GroupDocs

## Tutoriels associés

- [Masquer les données sensibles Java – Guide GroupDocs.Redaction](/redaction/java/getting-started/)
- [Masquer les données sensibles Java – Rédiger les informations personnelles avec GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Comment rédiger un PDF avec Aspose OCR et Java - Implémentation de motifs regex avec GroupDocs.Redaction](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)