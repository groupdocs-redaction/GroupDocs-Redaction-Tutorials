---
date: '2026-08-20'
description: Apprenez à censurer du texte avec GroupDocs.Redaction Java, à enregistrer
  en PDF rasterisé, à remplacer des phrases exactes et à appliquer des paramètres
  PDF personnalisés.
keywords:
- how to redact text
- save pdf as image
- convert pdf to image
lastmod: '2026-08-20'
og_description: Comment censurer du texte avec GroupDocs.Redaction Java. Ce guide
  vous montre le remplacement de phrases exactes, la création de PDF rasterisé et
  la conformité PDF/A‑1a en quelques étapes.
og_image_alt: Guide showing GroupDocs.Redaction Java code to redact text and create
  rasterized PDF
og_title: Comment censurer du texte avec la bibliothèque GroupDocs.Redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  headline: How to redact text with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  name: How to redact text with GroupDocs.Redaction Java
  steps:
  - name: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
    text: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
  - name: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
    text: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
  - name: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
    text: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
  type: HowTo
- questions:
  - answer: Add the GroupDocs repository and the `groupdocs-redaction` dependency
      to your `pom.xml` as shown in the Maven Setup section.
    question: How do I install GroupDocs.Redaction in a Maven project?
  - answer: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.
    question: Can I redact text from PDF files using this library?
  - answer: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s
      spelling and case sensitivity.
    question: What happens if the exact phrase isn’t found?
  - answer: Process them in smaller page ranges, enable rasterization only where needed,
      and always close the `Redactor` to free resources.
    question: How can I handle very large documents efficiently?
  - answer: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()`
      to target the exact pages you want to rasterize.
    question: Is it possible to save rasterized PDFs with specific page ranges?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java PDF processing
title: Comment censurer du texte avec GroupDocs.Redaction Java
type: docs
url: /fr/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# Comment caviarder du texte avec GroupDocs.Redaction Java

Dans les applications modernes, **comment caviarder du texte** dans un document tout en maintenant un flux de travail rapide et conforme est un défi fréquent pour les développeurs, les auditeurs et les responsables de conformité. Ce tutoriel vous guide à travers l'utilisation de GroupDocs.Redaction pour Java afin de localiser des phrases exactes, de les remplacer par des superpositions sécurisées, puis d'exporter le résultat sous forme de document PDF/A‑1a rasterisé — parfait pour l'archivage ou la distribution légale.

## Réponses rapides
- **Quelle est la classe principale pour le caviardage ?** `Redactor`  
- **Puis-je remplacer une phrase par une superposition colorée ?** Oui, en utilisant `ExactPhraseRedaction` et `ReplacementOptions`.  
- **Comment générer un PDF rasterisé ?** Activez la rasterisation via `SaveOptions.getRasterization().setEnabled(true)`.  
- **Quel niveau de conformité PDF est utilisé dans l'exemple ?** `PdfComplianceLevel.PdfA1a`.  
- **Ai-je besoin d'une licence pour une utilisation en production ?** Une licence valide GroupDocs.Redaction est requise pour les déploiements en production.

## Qu'est‑ce que le « caviarder du texte » en Java ?
`Redaction` est la suppression permanente ou l'obscurcissement de contenu sensible d'un fichier afin qu'il ne puisse pas être récupéré ou lu ultérieurement. Avec GroupDocs.Redaction, vous recherchez programmatiquement une phrase exacte — comme un numéro de sécurité sociale ou un code de projet confidentiel — et la remplacez par une superposition rouge, une boîte noire ou tout autre élément visuel personnalisé, garantissant que les données originales sont irrécupérables.

## Pourquoi utiliser GroupDocs.Redaction pour Java ?
GroupDocs.Redaction prend en charge **plus de 30 formats d'entrée et de sortie** (PDF, DOCX, PPTX, XLSX, HTML et types d'images) et peut traiter des documents de plusieurs centaines de pages sans charger le fichier complet en mémoire. Son algorithme de correspondance de phrases exactes réduit les faux positifs de > 95 % par rapport aux recherches génériques de mots‑clés, et le moteur de rasterisation intégré vous permet de produire des fichiers PDF/A‑1a entièrement basés sur des images pour une conservation à long terme.

## Prérequis
- **GroupDocs.Redaction for Java** (v24.9 ou plus récent).  
- **Java Development Kit (JDK) 8+**.  
- Un IDE tel que IntelliJ IDEA, Eclipse ou NetBeans.  
- Maven pour la gestion des dépendances.  

### Bibliothèques et dépendances requises
- GroupDocs.Redaction for Java – ajoutez le dépôt et la dépendance à votre `pom.xml` (voir la section de configuration Maven).  
- Optionnel : tout framework de journalisation que vous préférez (SLF4J, Log4j, etc.).

### Prérequis de connaissances
- Syntaxe Java de base et I/O de fichiers.  
- Familiarité avec la structure `pom.xml` de Maven.

## Configuration de GroupDocs.Redaction pour Java
### Configuration Maven
Add the GroupDocs repository and the `groupdocs-redaction` dependency to your `pom.xml` file:

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
Alternativement, vous pouvez télécharger la dernière version directement depuis [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisition de licence
- **Essai gratuit** – explorez l'API sans clé de licence.  
- **Licence temporaire** – utilisez-la pour une évaluation prolongée.  
- **Licence complète** – requise pour les environnements de production.

### Initialisation et configuration de base
La classe `Redactor` est le point d'entrée pour toutes les opérations de caviardage. Elle charge un document, applique les règles de caviardage et enregistre le résultat.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## Comment caviarder du texte – exemple de phrase exacte
Redactor est la classe principale qui charge un document et applique les règles de caviardage. ExactPhraseRedaction définit une règle qui correspond à une chaîne spécifique. Cet exemple montre comment charger un fichier, créer une règle ExactPhraseRedaction et exécuter le caviardage en une seule étape, offrant un flux de travail concis pour les développeurs tout en garantissant que le contenu original est obscurci de façon permanente.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

## Comment enregistrer en PDF rasterisé
SaveOptions est l'objet de configuration qui contrôle la façon dont un document est enregistré. En activant sa fonction de rasterisation et en sélectionnant la conformité PDF/A‑1a, vous pouvez produire un PDF uniquement image où chaque page est rendue sous forme de bitmap, répondant aux normes d'archivage et empêchant l'extraction de texte.

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

## Applications pratiques
1. **Caviardage de données sensibles** – masquer automatiquement les identifiants personnels avant de partager des contrats.  
2. **Archivage de documents** – convertir les rapports finalisés en PDF/A rasterisé pour une conformité à long terme.  
3. **Mise à jour massive de contenu** – remplacer la terminologie obsolète dans des centaines de fichiers avec un seul script.

## Considérations de performance
- **Fermez le `Redactor`** après chaque opération pour libérer les poignées de fichiers et la mémoire.  
- **Traitement par lots** – chargez une liste de fichiers et parcourez‑les, en réutilisant une seule instance de `Redactor` lorsque c'est possible.  
- **Surveillez les ressources** – utilisez les outils de profilage Java pour observer l'utilisation du CPU et du tas pendant les caviardages à grande échelle.

## Questions fréquemment posées

**Q : Comment installer GroupDocs.Redaction dans un projet Maven ?**  
R : Ajoutez le dépôt GroupDocs et la dépendance `groupdocs-redaction` à votre `pom.xml` comme indiqué dans la section Configuration Maven.

**Q : Puis‑je caviarder du texte à partir de fichiers PDF avec cette bibliothèque ?**  
R : Oui, GroupDocs.Redaction prend en charge PDF, DOCX, PPTX et de nombreux autres formats.

**Q : Que se passe‑t‑il si la phrase exacte n’est pas trouvée ?**  
R : Le `RedactorChangeLog` renverra un statut `Failed`. Vérifiez l’orthographe et la sensibilité à la casse de la phrase.

**Q : Comment gérer efficacement des documents très volumineux ?**  
R : Traitez‑les par plages de pages plus petites, activez la rasterisation uniquement lorsque nécessaire, et fermez toujours le `Redactor` pour libérer les ressources.

**Q : Est‑il possible d’enregistrer des PDF rasterisés avec des plages de pages spécifiques ?**  
R : Absolument. Utilisez `options.getRasterization().setPageIndex()` et `setPageCount()` pour cibler les pages exactes que vous souhaitez rasteriser.

## Conclusion
Vous disposez maintenant d'un guide complet, de bout en bout, sur **comment caviarder du texte** avec GroupDocs.Redaction Java et **l’enregistrer en PDF rasterisé**. En suivant ces étapes, vous pouvez protéger les informations sensibles, respecter des normes de conformité strictes et maintenir vos services Java performants à grande échelle.

**Prochaines étapes**  
- Approfondissez l'API en explorant la [documentation officielle](https://docs.groupdocs.com/redaction/java/).  
- Expérimentez d'autres types de caviardage tels que `RegexRedaction` et `ImageRedaction`.  
- Rejoignez la communauté sur le [Forum de support GroupDocs](https://forum.groupdocs.com/c/redaction/33) pour des astuces et meilleures pratiques.

---

**Dernière mise à jour :** 2026-08-20  
**Testé avec :** GroupDocs.Redaction Java 24.9  
**Auteur :** GroupDocs

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

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

## Tutoriels associés

- [Comment caviarder du texte avec GroupDocs.Redaction pour Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Tutoriel de caviardage de texte Java : guide avec GroupDocs.Redaction](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)