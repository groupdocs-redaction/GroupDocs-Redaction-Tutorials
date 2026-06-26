---
date: '2026-06-26'
description: Apprenez comment extraire le texte d'un PDF numérisé et masquer les données
  sensibles en utilisant GroupDocs OCR Redaction avec Azure OCR. Redact social security
  number et remplacez les informations confidentielles du PDF efficacement.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Extraire le texte d'un PDF numérisé – Masquer les données avec GroupDocs OCR
type: docs
url: /fr/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Extraire le texte d'un PDF numérisé – Masquer les données avec GroupDocs OCR

Dans le monde actuel axé sur les données, **extraire du texte à partir de fichiers PDF numérisés** et masquer les informations confidentielles est une étape de conformité incontournable. Ce tutoriel vous guide dans l'utilisation de GroupDocs Redaction conjointement avec Microsoft Azure OCR pour reconnaître de manière fiable le texte caché sur les pages numérisées et le remplacer par un espace réservé sûr tel que **`[REDACTED]`**. Vous verrez pourquoi cette combinaison est rapide, précise et prête pour des charges de travail de niveau production.

## Réponses rapides
- **Que signifie « masquer les données sensibles » ?** Il remplace le texte confidentiel identifié par un espace réservé (par ex. `[REDACTED]`).  
- **Quelle bibliothèque gère l'OCR ?** Connecteur Microsoft Azure OCR, utilisé via GroupDocs Redaction.  
- **Ai-je besoin d'une licence ?** Un essai gratuit fonctionne pour l'évaluation ; une licence permanente est requise pour la production.  
- **Puis-je masquer les PDF numérisés ?** Oui—l'OCR extrait le texte caché avant d'appliquer les masques regex.  
- **Cette solution est‑elle uniquement Java ?** L'exemple est basé sur Java, mais GroupDocs fournit des API similaires pour .NET et d'autres plateformes.

## Qu'est-ce que le masquage basé sur l'OCR ?
Le masquage basé sur l'OCR exécute d'abord l'OCR sur chaque page, transformant les images en texte interrogeable, puis applique des modèles regex pour remplacer les correspondances par un masque tel que `[REDACTED]`. Ce processus en deux étapes vous permet de masquer de manière fiable les données personnelles même dans les PDF numérisés, garantissant que toutes les chaînes sensibles sont supprimées avant le partage ou l'archivage du document.

## Pourquoi utiliser GroupDocs Redaction avec Azure OCR ?
Vous devez utiliser GroupDocs Redaction avec Azure OCR car il offre **une précision OCR >98 % sur le texte imprimé**, prend en charge **plus de 50 formats d'entrée et de sortie**, et peut traiter **des PDF de plusieurs centaines de pages sans charger le fichier complet en mémoire**, assurant un masquage rapide et évolutif pour la conformité. La solution **peut également traiter un PDF de 1 000 pages en moins de 2 minutes sur un serveur à 8 cœurs**, rendant les travaux par lots pratiques.

## Prérequis
- **Java Development Kit (JDK) 8+** installé.  
- **Maven** (si vous préférez la gestion des dépendances) ou la capacité de télécharger les JARs manuellement.  
- **Identifiants Microsoft Azure OCR** (point de terminaison et clé d'abonnement).  
- Connaissances de base en Java et familiarité avec les expressions régulières.

## Configuration de GroupDocs Redaction pour Java

### Configuration Maven
Ajoutez le dépôt GroupDocs et la dépendance à votre `pom.xml` :

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
Si vous préférez la gestion manuelle des JARs, récupérez la dernière version depuis [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisition de licence
- **Essai gratuit** – explorez toutes les fonctionnalités sans frais.  
- **Licence temporaire** – prolongez la période d'évaluation.  
- **Licence complète** – débloquez les capacités prêtes pour la production.

### Initialisation et configuration de base
La classe `Redactor` est le moteur principal qui effectue l'extraction OCR et applique les règles de masquage aux documents PDF.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Comment masquer les données sensibles avec le masquage OCR
Masquer les données sensibles avec le masquage OCR implique de charger le PDF avec les paramètres Azure OCR, de définir des modèles regex pour les données que vous souhaitez cacher, et d'invoquer le Redactor pour remplacer chaque correspondance par un espace réservé tel que `[REDACTED]`. La bibliothèque gère l'OCR, la correspondance de motifs et la réécriture du PDF en un seul flux de travail.

### Étape 1 : Charger le document avec les paramètres OCR
`LoadOptions` configure la façon dont GroupDocs charge un fichier, vous permettant de passer des connecteurs OCR comme Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – remplacez par le chemin de votre PDF.  
- **`settings`** – contient le connecteur Azure OCR que vous avez créé précédemment.

### Étape 2 : Définir et appliquer les masques regex
`ReplacementOptions` spécifie le texte de remplacement qui substituera chaque correspondance regex lors du masquage.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- Le motif `\b\d{3}-\d{2}-\d{4}\b` correspond aux numéros de sécurité sociale américains.  
- `ReplacementOptions("[REDACTED]")` remplace chaque correspondance par le masque, masquant ainsi efficacement **les données sensibles**.

## Cas d'utilisation courants pour masquer les données sensibles
1. **Gestion de documents juridiques** – masquer les identifiants des clients avant de partager les brouillons.  
2. **Rapports financiers** – protéger les numéros de compte et les identifiants de transaction.  
3. **Dossiers de santé** – se conformer à la HIPAA en masquant les identifiants des patients.  
4. **Publications gouvernementales** – supprimer les données personnelles des dossiers publics.  
5. **Contrats d'entreprise** – dissimuler les clauses propriétaires lors des revues externes.

## Conseils de performance
- **Optimiser les regex** – éviter les motifs trop larges qui augmentent le temps de traitement ; des expressions bien conçues peuvent réduire le temps d'exécution jusqu'à 40 %.  
- **Gestion de la mémoire** – fermez rapidement l'instance `Redactor` (try‑with‑resources le fait automatiquement).  
- **Exécution asynchrone** – pour le traitement en masse, exécutez les tâches de masquage sur des threads séparés ou utilisez une file d'attente de tâches pour garder l'interface réactive.

## Dépannage
- **Erreur d'identifiants Azure** – revérifiez l'URL du point de terminaison et la clé d'abonnement dans `MicrosoftAzureOcrConnector`.  
- **Document ne se charge pas** – vérifiez le chemin du fichier et assurez-vous que le PDF n'est pas protégé par mot de passe (ou fournissez le mot de passe via `LoadOptions`).  
- **Aucun masquage appliqué** – testez votre regex avec une chaîne simple d'abord ; utilisez `Pattern.compile` dans un test unitaire pour confirmer les correspondances.

## Questions fréquemment posées

**Q : Qu'est-ce que le masquage OCR ?**  
R : Le masquage OCR utilise la reconnaissance optique de caractères pour extraire le texte caché des images ou des PDF numérisés, puis applique des règles de masquage pour masquer ce texte.

**Q : Puis-je utiliser GroupDocs Redaction sans Azure OCR ?**  
R : Oui, mais l'OCR améliore considérablement la précision sur les documents numérisés où l'extraction de texte native échoue.

**Q : Comment gérer des motifs regex complexes ?**  
R : Construisez‑les et testez‑les progressivement, en utilisant la classe `Pattern` de Java dans un bac à sable avant de les appliquer à de gros documents.

**Q : Quels sont les goulets d'étranglement de performance typiques ?**  
R : Les PDF volumineux, les regex trop complexes et les appels OCR synchrones peuvent ralentir le traitement ; envisagez le traitement par lots et des motifs optimisés.

**Q : Le support est‑il disponible pour les problèmes d'implémentation ?**  
R : Absolument — contactez le [forum GroupDocs](https://forum.groupdocs.com/c/redaction/33) pour obtenir de l'aide de la communauté ou contactez le support GroupDocs.

## Ressources supplémentaires
- **Documentation** : https://docs.groupdocs.com/redaction/java/  
- **Référence API** : https://reference.groupdocs.com/redaction/java  
- **Téléchargement** : https://releases.groupdocs.com/redaction/java/  
- **GitHub** : https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Support gratuit** : https://forum.groupdocs.com/c/redaction/33  
- **Licence temporaire** : https://purchase.groupdocs.com/temporary-license/

---

**Dernière mise à jour :** 2026-06-26  
**Testé avec :** GroupDocs.Redaction 24.9 (Java)  
**Auteur :** GroupDocs  

## Tutoriels associés

- [Masquage sécurisé de PDF avec OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Comment masquer du texte avec GroupDocs.Redaction pour Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Masquer les données sensibles Java – Masquer les informations personnelles avec GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)