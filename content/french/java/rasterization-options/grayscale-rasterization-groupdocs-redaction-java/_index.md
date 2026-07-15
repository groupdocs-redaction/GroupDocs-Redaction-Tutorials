---
date: '2026-05-17'
description: Apprenez à rasteriser un PDF en niveaux de gris à l'aide de GroupDocs.Redaction
  pour Java, à appliquer un filtre en niveaux de gris, et à garder vos documents sécurisés
  et de haute qualité.
keywords:
- how to rasterize pdf
- java pdf to image
- apply grayscale filter pdf
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to rasterize PDF to grayscale using GroupDocs.Redaction for
    Java, apply a grayscale filter, and keep your documents secure and high‑quality.
  headline: How to rasterize PDF to grayscale with GroupDocs.Redaction Java – Secure
    and Optimize Your Documents
  type: TechArticle
- questions:
  - answer: In GroupDocs.Redaction, the grayscale option is tied to rasterization,
      which ensures consistent results and adds a security layer.
    question: Can I convert documents to grayscale without rasterization?
  - answer: All major formats supported by GroupDocs.Redaction—including DOCX, PDF,
      XLSX, PPTX, RTF, and more than 100 others—can be rasterized and converted to
      grayscale.
    question: What document formats support grayscale rasterization?
  - answer: Yes. Text‑heavy files may grow, while image‑heavy files might shrink.
      DPI settings have the biggest impact.
    question: Will rasterization affect the file size of my documents?
  - answer: No. Rasterization is one‑way; keep a backup of the original if you need
      to revert.
    question: Is it possible to reverse the grayscale rasterization process?
  - answer: Use a higher DPI (300 + for print quality) and choose PDF as the output
      format for best archival results.
    question: How can I optimize the quality of grayscale rasterized documents?
  type: FAQPage
title: Comment rasteriser un PDF en niveaux de gris avec GroupDocs.Redaction Java
  – Sécurisez et optimisez vos documents
type: docs
url: /fr/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# Comment rasteriser un PDF en niveaux de gris avec GroupDocs.Redaction Java

Si vous devez **rasteriser un PDF** en niveaux de gris tout en gardant vos documents sécurisés, d’aspect professionnel et faciles à archiver, vous êtes au bon endroit. Dans ce tutoriel, nous parcourrons les étapes exactes pour convertir des fichiers DOCX, PDF ou autres formats pris en charge, colorés, en une version rasterisée propre en niveaux de gris à l’aide de GroupDocs.Redaction pour Java. Vous comprendrez pourquoi la rasterisation ajoute une couche de sécurité, comment configurer la bibliothèque et comment gérer les ressources efficacement — le tout présenté de manière conviviale, étape par étape.

## Réponses rapides
- **Que fait la rasterisation en niveaux de gris ?** Elle convertit chaque page en une image haute résolution puis applique un filtre en niveaux de gris, supprimant toutes les informations de couleur.  
- **Pourquoi utiliser GroupDocs.Redaction pour cela ?** Il combine la sécurité de la rédaction avec les options de rasterisation dans une API unique et facile à utiliser.  
- **Quels formats sont pris en charge ?** DOCX, PDF, XLSX, PPTX, RTF et plus de 100 autres formats.  
- **Ai‑je besoin d’une licence ?** Une licence valide de GroupDocs.Redaction est requise pour la production ; un essai gratuit est disponible pour les tests.  
- **Quelle version de Java est requise ?** JDK 8 ou supérieur.

## Comment rasteriser un PDF en niveaux de gris ?

Chargez votre document source avec `new Redactor("path/to/file")`, activez la rasterisation via `RasterizationOptions`, ajoutez l’option avancée de niveaux de gris, puis appelez `save()` — la conversion complète s’effectue en quelques lignes concises. Cette approche garantit que chaque page devient un PDF basé sur une image, en noir et blanc, empêchant la sélection de texte et assurant une apparence uniforme prête à l’impression.

## Qu’est‑ce que **create grayscale pdf** ?

Créer un PDF en niveaux de gris signifie convertir chaque élément visuel du document original en nuances de gris. Le résultat est un fichier plus petit, adapté à l’impression, qui élimine les distractions liées aux couleurs et ajoute un léger avantage de sécurité car le contenu devient basé sur une image.

## Pourquoi utiliser la rasterisation en niveaux de gris avec GroupDocs.Redaction ?

La rasterisation transforme chaque page en une image, ce qui signifie que le texte ne peut pas être copié ou modifié, et que le rendu visuel reste cohérent sur les imprimantes et les visionneuses. GroupDocs.Redaction prend en charge **plus de 100 formats d’entrée et de sortie** — y compris DOCX, XLSX, PPTX, HTML et les types d’image — vous permettant d’appliquer le même flux de travail à pratiquement n’importe quel document que vous traitez.

## Prérequis
- Java Development Kit (JDK) 8 ou plus récent. Vérifiez avec `java -version`.  
- Un IDE (IntelliJ IDEA, Eclipse ou NetBeans) pour faciliter le codage et le débogage.  
- GroupDocs.Redaction pour Java ajouté via Maven ou Gradle.  
- Un document d’exemple (par ex., un DOCX multipage) sur lequel vous pouvez expérimenter en toute sécurité.  
- Un espace disque suffisant pour la sortie rasterisée (les fichiers raster peuvent être plus volumineux que la source).

## Importer les packages

Les importations suivantes apportent les classes principales Redactor et rasterisation nécessaires à l’exemple.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Étape 1 : Initialiser l’objet Redactor

La classe `Redactor` est le point d’entrée pour toutes les opérations de traitement de documents dans GroupDocs.Redaction. Créer une instance ouvre la porte au chargement, à l’édition et à l’enregistrement des documents.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

Remplacez `Constants.MULTIPAGE_SAMPLE_DOCX` par le chemin du fichier que vous souhaitez convertir en PDF en niveaux de gris.

## Étape 2 : Configurer les options d’enregistrement

La classe `SaveOptions` définit comment le document traité sera écrit sur le disque, y compris le format et le nom du fichier.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

La sortie sera nommée `yourfile_scan.pdf` (ou le format que vous spécifierez plus tard).

## Étape 3 : Activer la rasterisation

L’objet `RasterizationOptions` active le rendu basé sur image de chaque page avant l’enregistrement.

```java
so.getRasterization().setEnabled(true);
```

## Étape 4 : Appliquer la conversion en niveaux de gris

`AdvancedRasterizationOptions.Grayscale` est un drapeau qui force l’image rasterisée à n’utiliser que des nuances de gris.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

## Étape 5 : Exécuter la transformation du document

Appeler `save()` exécute l’ensemble du pipeline de traitement et écrit le fichier de sortie.

```java
redactor.save(so);
```

Après l’exécution de cette ligne, vous trouverez un nouveau fichier sur le disque qui est entièrement rasterisé, en niveaux de gris, et enregistré avec le suffixe `_scan`.

## Étape 6 : Gestion correcte des ressources

La méthode `close()` libère les ressources natives et supprime les fichiers temporaires.

```java
finally { redactor.close(); }
```

Pour le Java moderne, vous pouvez également utiliser le modèle try‑with‑resources, qui ferme automatiquement le `Redactor` :

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

Les deux approches sont sûres ; la seconde est plus concise.

## Options de configuration avancées

### Ajuster le DPI pour la qualité ou la taille

Un DPI plus élevé produit des images plus nettes (idéal pour l’impression), tandis qu’un DPI plus bas réduit la taille du fichier. Un compromis courant est de 150 DPI pour la visualisation à l’écran et 300 DPI pour les PDF prêts à imprimer.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Choisir un format de sortie

Vous pouvez forcer le résultat rasterisé dans un format de conteneur spécifique, tel que PDF, TIFF ou PNG. Le PDF est le format d’archivage le plus largement utilisé.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Cas d’utilisation courants
- **Archivage de documents juridiques** – créer des PDF en niveaux de gris immuables qui ne peuvent pas être modifiés.  
- **Rapports prêts à imprimer** – garantir une sortie noir et blanc cohérente pour l’impression en masse.  
- **Flux de travail de conformité** – combiner la rédaction avec la rasterisation en niveaux de gris pour répondre aux réglementations strictes de protection des données.

## Problèmes courants et solutions

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Le fichier de sortie est plus grand que prévu | DPI réglé trop haut ou compression d’image désactivée | Réduire le DPI (par ex., 150) ou activer la compression dans `RasterizationOptions`. |
| Le texte apparaît flou | DPI insuffisant pour la taille de police originale | Augmenter le DPI à 300 ou plus. |
| Le processus lance `OutOfMemoryError` sur de gros documents | Le document entier est chargé en mémoire | Utiliser les API de streaming ou traiter les pages par lots si supporté. |
| Le niveau de gris n’est pas appliqué | Option avancée non ajoutée correctement | Vérifier que `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` est appelé avant `save()`. |

## Questions fréquemment posées

**Q : Puis‑je convertir des documents en niveaux de gris sans rasterisation ?**  
R : Dans GroupDocs.Redaction, l’option niveaux de gris est liée à la rasterisation, ce qui garantit des résultats cohérents et ajoute une couche de sécurité.

**Q : Quels formats de documents prennent en charge la rasterisation en niveaux de gris ?**  
R : Tous les principaux formats pris en charge par GroupDocs.Redaction — y compris DOCX, PDF, XLSX, PPTX, RTF et plus de 100 autres — peuvent être rasterisés et convertis en niveaux de gris.

**Q : La rasterisation affectera‑t‑elle la taille des fichiers de mes documents ?**  
R : Oui. Les fichiers contenant beaucoup de texte peuvent augmenter, tandis que les fichiers riches en images peuvent diminuer. Les réglages du DPI ont le plus grand impact.

**Q : Est‑il possible d’inverser le processus de rasterisation en niveaux de gris ?**  
R : Non. La rasterisation est unidirectionnelle ; conservez une sauvegarde de l’original si vous devez revenir en arrière.

**Q : Comment puis‑je optimiser la qualité des documents rasterisés en niveaux de gris ?**  
R : Utilisez un DPI plus élevé (300 + pour une qualité d’impression) et choisissez le PDF comme format de sortie pour les meilleurs résultats d’archivage.

## Conclusion

Vous disposez maintenant d’une procédure complète, prête pour la production, pour **rasteriser un PDF en niveaux de gris** à l’aide de GroupDocs.Redaction pour Java. En activant la rasterisation, en ajoutant l’option avancée de niveaux de gris et en gérant les ressources de manière responsable, vous pouvez produire des documents sécurisés, adaptés à l’impression, qui respectent les normes de conformité et affichent une apparence cohérente sur n’importe quel visualiseur.

---

**Dernière mise à jour :** 2026-05-17  
**Testé avec :** GroupDocs.Redaction 23.11 for Java  
**Auteur :** GroupDocs  

---

## MOTS‑CLÉS CIBLES :

**Mot‑clé principal (PRIORITÉ MAXIMALE) :**  
how to rasterize pdf

**Mots‑clés secondaires (SUPPORTING) :**  
java pdf to image, apply grayscale filter pdf

## Tutoriels associés

- [Tutoriels des options de rasterisation pour GroupDocs.Redaction Java](/redaction/java/rasterization-options/)
- [Comment utiliser groupdocs redaction pour Java : pré‑rasterisation dans les documents Word](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)
- [Rasterisation de bruit personnalisée en Java&#58; sécuriser les informations sensibles avec GroupDocs.Redaction](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)