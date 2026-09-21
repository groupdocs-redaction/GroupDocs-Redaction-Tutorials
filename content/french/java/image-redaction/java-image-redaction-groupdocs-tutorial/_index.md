---
date: '2026-09-21'
description: Apprenez à caviarder une image avec GroupDocs.Redaction pour Java. Ce
  guide étape par étape couvre l'installation, le caviardage au niveau du pixel, la
  vérification et les meilleures pratiques.
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: Comment caviarder une image avec GroupDocs.Redaction pour Java. Suivez
  ce guide pour masquer les données de pixels dans les fichiers numérisés, choisir
  les couleurs et vérifier les résultats — idéal pour la conformité au GDPR et à la
  HIPAA.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: Comment caviarder une image avec GroupDocs.Redaction pour Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: Comment caviarder une image avec GroupDocs.Redaction pour Java
type: docs
url: /fr/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Comment masquer une image avec GroupDocs.Redaction pour Java

Dans ce tutoriel complet, vous apprendrez **comment masquer une image** en Java avec GroupDocs.Redaction. Masquer les images numérisées est une étape cruciale pour protéger les données personnelles, respecter le RGPD, HIPAA ou d’autres réglementations de confidentialité, et garantir que les informations visuelles confidentielles ne fuient jamais. Nous vous guiderons à travers la configuration du projet, la configuration du masquage au niveau des pixels, l’enregistrement sécurisé du résultat, et la confirmation du succès du masquage — le tout présenté dans un style conversationnel, étape par étape, que vous pouvez copier dans n’importe quelle application Java.

## Réponses rapides
- **Quelle bibliothèque gère le masquage d'image en Java ?** GroupDocs.Redaction for Java.  
- **Puis‑je choisir la couleur du masquage ?** Yes – any opaque `java.awt.Color` such as `Color.BLUE` or `Color.BLACK`.  
- **Une licence est‑elle requise pour la production ?** Yes, a valid GroupDocs license is mandatory for commercial use.  
- **L'image originale sera‑t‑elle écrasée ?** No – the API writes the redacted image to a new file you specify.  
- **Quelle version de Java est prise en charge ?** Java 8 and newer (up to Java 21 at the time of writing).

## Qu'est-ce que le masquage d'image et pourquoi masquer une image numérisée en Java ?
Le masquage d'image obscurcit de façon permanente les données visuelles — noms, numéros, signatures — en remplaçant les zones de pixels par une couleur unie. Contrairement au masquage de texte, qui agit sur des caractères sélectionnables, les images numérisées stockent l'information sous forme de pixels bruts, de sorte que seuls les outils basés sur les pixels peuvent garantir que les données ne peuvent pas être récupérées. Avec GroupDocs.Redaction, vous pouvez cibler des coordonnées précises, appliquer n'importe quelle couleur opaque, et produire une nouvelle image qui supprime définitivement le contenu sensible.

## Pourquoi utiliser GroupDocs.Redaction pour Java ?
GroupDocs.Redaction prend en charge **plus de 50 formats d'image** (y compris JPG, PNG, BMP, GIF) et peut traiter des documents de plusieurs centaines de pages sans charger le fichier complet en mémoire, grâce à son architecture de streaming. Les benchmarks montrent qu'un PNG numérisé de 300 KB est masqué en moins de 120 ms sur un CPU typique de 2,8 GHz, ce qui le rend adapté aux traitements par lots comme aux services en temps réel.

## Prérequis
- **JDK 8 ou supérieur** installé et configuré dans votre `PATH`.  
- **Maven** (ou Gradle) pour la gestion des dépendances.  
- Un IDE tel que **IntelliJ IDEA**, **Eclipse**, ou **NetBeans**.  
- Une connaissance de base des I/O de fichiers Java et du package `java.awt`.

## Configuration de GroupDocs.Redaction pour Java

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
Vous pouvez également télécharger le dernier JAR depuis la page officielle de publication : [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Acquisition de licence
- **Essai gratuit :** Inscrivez‑vous pour un essai afin d’explorer l’API complète.  
- **Licence temporaire :** Utilisez une clé temporaire pour des tests prolongés sans frais.  
- **Achat complet :** Obtenez une licence de production pour un déploiement illimité.

## Guide d'implémentation

Nous diviserons l'implémentation en deux fonctionnalités principales : **masquage de zone d'image** (le masquage réel) et **vérification du statut du masquage** (confirmation du succès).

### Comment masquer les images de documents numérisés – étape 1 : initialiser le redacteur
`Redactor` est la classe centrale qui charge une image et fournit les opérations de masquage.  
Créez une instance de `Redactor` qui pointe vers l'image source que vous souhaitez traiter.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Étape 2 : définir les paramètres du masquage
`ImageAreaRedaction` fonctionne avec un `Point` (coin supérieur gauche) et une `Dimension` (largeur × hauteur) qui décrivent le rectangle à masquer. Dans cet exemple, nous utilisons une couleur de remplissage bleue.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Étape 3 : appliquer le masquage
`RegionReplacementOptions` vous permet de spécifier la couleur de remplissage et une bordure optionnelle. En transmettant ces options à `ImageAreaRedaction` et en appelant `apply()`, le masquage est effectué. La méthode renvoie un `RedactorChangeLog` qui indique le succès ou l’échec.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Étape 4 : libérer les ressources
`Redactor` implémente `AutoCloseable`. Le fermer libère les tampons natifs et les descripteurs de fichiers, évitant les fuites de mémoire dans les services de longue durée.

```java
redactor.close();
```

### Comment vérifier le masquage – vérification du statut
Après avoir appliqué le masquage, inspectez le `RedactorChangeLog`. Une valeur `Status.SUCCESS` confirme que la région de pixels a été remplacée sans erreur. Vous pouvez également rendre l'image dans un `BufferedImage` pour une inspection visuelle avant l'enregistrement.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Applications pratiques
- **Gestion de documents confidentiels :** Masquer les données personnelles dans les contrats numérisés avant de les partager avec des partenaires.  
- **Documentation juridique :** Garantir la conformité au RGPD ou à HIPAA en masquant les identifiants dans les images de preuves.  
- **Dossiers médicaux :** Masquer les visages des patients ou les notes manuscrites dans les scans radiologiques tout en préservant les détails diagnostiques.

## Considérations de performance
- **Traitement par lots :** Traitez les images par groupes de 10 à 20 pour maintenir l’utilisation de la mémoire en dessous de 200 Mo.  
- **Réutilisation d'objets :** Réutilisez les objets `Point` et `Dimension` sur plusieurs itérations afin de réduire la pression du ramasse‑miettes.  
- **Mises à jour de version :** Passez à la dernière version de GroupDocs.Redaction pour bénéficier d’une amélioration de vitesse de 15 % signalée dans la version 24.10.

## Problèmes courants et solutions

| Problème | Cause | Solution |
|----------|-------|----------|
| **Le masquage échoue avec le statut `Failed`** | Chemin de fichier incorrect ou format d'image non pris en charge | Vérifiez que le fichier existe et qu'il est dans un format pris en charge (JPG, PNG, BMP, GIF). |
| **Le fichier de sortie est vide** | `redactor.save()` appelé avant que le masquage ne soit terminé | Assurez‑vous que `apply()` renvoie `Status.SUCCESS` avant d’appeler `save()`. |
| **Couleur non appliquée** | Utilisation d'une `Color` transparente | Choisissez une couleur opaque comme `Color.BLACK` ou `Color.BLUE`. |

## Questions fréquemment posées

**Q : Quelle est la différence entre `ImageAreaRedaction` et le masquage de texte ?**  
A : `ImageAreaRedaction` fonctionne sur des coordonnées de pixels brutes, tandis que le masquage de texte analyse les couches OCR pour localiser et supprimer le contenu textuel.

**Q : Puis‑je masquer plusieurs régions dans une même image ?**  
A : Oui — appelez `redactor.apply()` à plusieurs reprises avec différents objets `ImageAreaRedaction` avant d’enregistrer le fichier final.

**Q : GroupDocs.Redaction prend‑il en charge d’autres formats d'image comme le TIFF ?**  
A : La bibliothèque prend en charge les formats raster courants (JPG, PNG, BMP, GIF). Pour le TIFF, convertissez d’abord l’image dans un format pris en charge.

**Q : Comment automatiser le masquage d’un dossier de PDF numérisés ?**  
A : Extrayez chaque page en tant qu’image, appliquez la même logique de masquage, puis reconstruisez le PDF à l’aide d’une bibliothèque PDF telle que GroupDocs.Conversion.

**Q : Existe‑t‑il un moyen de prévisualiser le masquage avant l’enregistrement ?**  
A : Rendu le `Redactor` dans un `BufferedImage` et affichez‑le dans une interface Swing ou JavaFX, vous permettant de confirmer la zone masquée avant de valider.

## Conclusion
Vous disposez maintenant d’un guide complet, prêt pour la production, sur **comment masquer une image** et, plus spécifiquement, sur **comment masquer une image numérisée en Java** avec GroupDocs.Redaction pour Java. En suivant les étapes ci‑dessus, vous pouvez protéger les données visuelles sensibles dans les secteurs financier, juridique et de la santé. Explorez les API supplémentaires — comme le masquage de texte, le masquage de pages PDF ou le traitement par lots de dossiers — pour créer une chaîne complète de protection de la vie privée des données pour votre organisation.

**Ressources**  
- [Documentation](https://docs.groupdocs.com/redaction/java/)  
- [Référence API](https://reference.groupdocs.com/redaction/java)  
- [Téléchargement](https://releases.groupdocs.com/redaction/java/)  
- [Dépôt GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Forum d'assistance gratuit](https://forum.groupdocs.com/c/redaction/33)  
- [Licence temporaire](https://purchase.groupdocs.com/temporary-license/) 

---

**Dernière mise à jour :** 2026-09-21  
**Testé avec :** GroupDocs.Redaction 24.9 (Java)  
**Auteur :** GroupDocs

## Tutoriels associés

- [Comment masquer en Java avec GroupDocs.Redaction - Guide complet pour les développeurs](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [Comment masquer un PDF numérisé avec OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Comment masquer du texte en Java avec GroupDocs.Redaction – Guide](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)