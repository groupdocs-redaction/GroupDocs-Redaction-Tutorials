---
additionalTitle: GroupDocs API References
date: 2026-10-06
description: Apprenez à caviarder des pages PDF, supprimer les annotations PDF et
  caviarder les cellules Excel à l'aide de GroupDocs.Redaction for .NET – une API
  sécurisée et multiplateforme pour le caviardage de documents.
keywords:
- how to redact pdf
- remove pdf annotations
- redact excel cells
- redact pdf pages
- load pdf from stream
lastmod: 2026-10-06
linktitle: GroupDocs.Redaction for .NET Tutoriels
og_description: Comment caviarder rapidement des pages PDF avec GroupDocs.Redaction
  for .NET. L'API supprime les annotations PDF, caviarde les cellules Excel et protège
  les données sensibles dans plus de 30 formats.
og_image_alt: Guide to redact PDF pages using GroupDocs.Redaction for .NET
og_title: Comment caviarder des pages PDF – GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  headline: How to redact PDF pages with GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  name: How to redact PDF pages with GroupDocs.Redaction for .NET
  steps:
  - name: load the PDF
    text: You can open a file from disk, a memory stream, or a remote source. The
      API accepts both a file path string and a `Stream` object, which is ideal for
      web services that receive uploads.
  - name: define the pages to redact
    text: Pass a list of zero‑based page indexes or a range string such as `"1-3,5"`
      to the `RemovePages` method. The library validates the range and throws a clear
      exception if a page does not exist.
  - name: save the sanitized document
    text: Call `Save` with the desired output format. You can keep the original PDF,
      export to a rasterized PDF, or stream the result directly to the client response.
  type: HowTo
- questions:
  - answer: Yes, the library removes the specified pages while preserving page numbering,
      bookmarks, and cross‑references for the remaining content.
    question: Can I redact PDF pages without affecting the rest of the document’s
      layout?
  - answer: Absolutely. Use `Redactor.RemoveAnnotations()` to strip all annotation
      objects in a single call.
    question: Is it possible to redact PDF annotations only?
  - answer: Load the workbook with `Redactor.LoadExcel(path)`, then call `Redactor.RedactCell(sheetName,
      cellAddress, RedactionMode.Blackout)` and save.
    question: How do I redact Excel cells directly?
  - answer: Yes, you can pass any `System.IO.Stream` to the `Load` method, which is
      ideal for processing files uploaded via ASP.NET Core controllers.
    question: Does GroupDocs.Redaction support loading PDFs from a stream?
  - answer: Metered licensing lets you pay per‑redaction operation, scaling cost‑effectively
      with usage spikes.
    question: What licensing model is recommended for high‑volume production use?
  type: FAQPage
tags:
- pdf redaction
- groupdocs.redaction
- .net document security
- redact pdf pages
title: Comment caviarder des pages PDF avec GroupDocs.Redaction for .NET
type: docs
url: /fr/net/
weight: 10
---

# Comment masquer les pages PDF avec GroupDocs.Redaction pour .NET

Si vous devez **masquer des pages PDF** rapidement et de manière fiable, GroupDocs.Redaction pour .NET vous offre une API complète, multiplateforme, qui supprime le contenu sensible de plus de 30 formats de fichiers. Que vous construisiez un flux de travail axé sur la conformité, un portail de gestion de documents ou une application priorisant la confidentialité, cette bibliothèque vous permet d’effacer définitivement les données confidentielles tout en préservant le reste de la structure du document.

**GroupDocs.Redaction pour .NET est une bibliothèque .NET qui permet la suppression permanente de contenu sensible de plus de 30 formats de documents.** Elle prend en charge le traitement à haut volume, peut gérer des fichiers de plusieurs centaines de pages sans charger le document entier en mémoire, et offre des options de rasterisation qui transforment le texte en images pour une sécurité supplémentaire.

{{% alert color="primary" %}}
GroupDocs.Redaction pour .NET propose une suite complète de tutoriels et d'exemples pour implémenter la rédaction sécurisée de documents dans vos applications .NET. Des remplacements de texte de base aux nettoyages avancés de métadonnées, ces ressources couvrent les techniques essentielles pour masquer les informations sensibles des documents. Apprenez à supprimer définitivement les données privées de divers formats de documents, y compris PDF, Word, Excel, PowerPoint et images, avec un contrôle précis et une suppression complète du contenu confidentiel. Nos guides étape par étape vous aident à maîtriser les capacités de rédaction standard et avancées afin de répondre aux exigences de conformité et de protéger efficacement les informations sensibles.
{{% /alert %}}

## Réponses rapides
- **GroupDocs.Redaction peut‑il masquer des pages PDF entières ?** Oui, vous pouvez supprimer des pages individuelles ou des plages de pages avec un seul appel d’API.  
- **Prend‑il en charge la suppression des annotations PDF ?** Absolument – les annotations, commentaires et balisages peuvent être supprimés en une seule étape.  
- **Puis‑je masquer des cellules Excel sans les convertir en PDF ?** Oui, la bibliothèque cible directement les feuilles de calcul Excel.  
- **Le chargement d’un PDF depuis un flux est‑il supporté ?** L’API accepte les objets `Stream`, permettant le traitement en mémoire.  
- **Quelles versions de .NET sont compatibles ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Qu’est‑ce que la rédaction dans le contexte des PDF ?
La rédaction consiste en la suppression ou l’obscurcissement permanent du contenu sensible d’un document afin qu’il ne puisse pas être récupéré ou visualisé ultérieurement. Dans les fichiers PDF, la rédaction peut viser le texte, les images, les annotations ou des pages entières, et le résultat est un fichier assaini qui conserve la mise en page originale.

## Pourquoi utiliser GroupDocs.Redaction pour .NET ?
GroupDocs.Redaction pour .NET offre une solution robuste et haute performance capable de gérer de gros documents tout en garantissant la suppression complète des données sensibles, proposant une rasterisation intégrée, une prise en charge étendue des formats et une journalisation d’audit détaillée, ce qui le rend idéal pour les applications axées sur la conformité et les environnements d’entreprise.

- **Plus de 30 formats pris en charge** – notamment PDF, DOCX, XLSX, PPTX, HTML et les types d’images courants.  
- **Performance évolutive** – traite des PDF de 500 pages en moins de 5 secondes sur un serveur typique, sans charger le fichier complet en RAM.  
- **Rasterisation intégrée** – convertit les pages masquées en images, garantissant qu’aucun texte caché ne subsiste.  
- **Conforme aux exigences** – répond aux exigences GDPR, HIPAA et PCI‑DSS avec une journalisation de la traçabilité.

## Prérequis
- .NET Framework 4.5+ **ou** .NET Core 3.1+ installé sur votre machine de développement.  
- Une licence valide GroupDocs.Redaction (essai disponible pour évaluation).  
- Accès aux fichiers PDF, Excel ou Word que vous souhaitez traiter.

## Comment masquer les pages PDF étape par étape

Redactor est la classe principale de GroupDocs.Redaction qui charge, modifie et enregistre les documents. RemovePages supprime les pages spécifiées du document chargé.

Chargez le PDF, définissez les pages que vous souhaitez supprimer, appliquez la rédaction et enregistrez le résultat. La réponse directe suivante explique le modèle de base :

Chargez le PDF cible avec `Redactor.Load(streamOrPath)`, appelez `Redactor.RemovePages(pageNumbers)` pour supprimer les pages indésirables, puis invoquez `Redactor.Save(outputPath)` – ce flux en trois étapes masque les pages en moins d’une seconde pour la plupart des documents.

### Étape 1 : charger le PDF
Vous pouvez ouvrir un fichier depuis le disque, un flux mémoire ou une source distante. L’API accepte à la fois une chaîne de chemin de fichier et un objet `Stream`, ce qui est idéal pour les services web qui reçoivent des téléchargements.

### Étape 2 : définir les pages à masquer
Passez une liste d’index de pages basés sur zéro ou une chaîne de plage telle que `"1-3,5"` à la méthode `RemovePages`. La bibliothèque valide la plage et lève une exception claire si une page n’existe pas.

### Étape 3 : enregistrer le document assaini
Appelez `Save` avec le format de sortie souhaité. Vous pouvez conserver le PDF original, exporter vers un PDF rasterisé, ou diffuser le résultat directement dans la réponse du client.

## Problèmes courants et solutions
- **Problème :** La rédaction semble fonctionner mais le texte original reste recherchable.  
  **Solution :** Activez la rasterisation (`Redactor.Rasterize = true`) avant l’enregistrement ; cela convertit la page en image, supprimant les calques de texte cachés.  

- **Problème :** Les gros PDF provoquent des exceptions OutOfMemory.  
  **Solution :** Utilisez `Redactor.Load(stream, loadOptions => loadOptions.EnableMemoryOptimization = true)` pour traiter le fichier par morceaux.  

- **Problème :** Les annotations ne sont pas supprimées.  
  **Solution :** Appelez `Redactor.RemoveAnnotations()` après le chargement du document ; cette méthode supprime les commentaires, les surlignages et les champs de formulaire.

## Questions fréquemment posées

**Q : Puis‑je masquer des pages PDF sans affecter le reste de la mise en page du document ?**  
R : Oui, la bibliothèque supprime les pages spécifiées tout en préservant la numérotation des pages, les signets et les références croisées du contenu restant.

**Q : Est‑il possible de masquer uniquement les annotations PDF ?**  
R : Absolument. Utilisez `Redactor.RemoveAnnotations()` pour supprimer tous les objets d’annotation en un seul appel.

**Q : Comment masquer directement les cellules Excel ?**  
R : Chargez le classeur avec `Redactor.LoadExcel(path)`, puis appelez `Redactor.RedactCell(sheetName, cellAddress, RedactionMode.Blackout)` et enregistrez.

**Q : GroupDocs.Redaction prend‑il en charge le chargement de PDF depuis un flux ?**  
R : Oui, vous pouvez passer n’importe quel `System.IO.Stream` à la méthode `Load`, ce qui est idéal pour traiter les fichiers téléchargés via les contrôleurs ASP.NET Core.

**Q : Quel modèle de licence est recommandé pour une utilisation en production à haut volume ?**  
R : La licence à la consommation vous permet de payer par opération de rédaction, en adaptant les coûts de manière efficace aux pics d’utilisation.

---

**Dernière mise à jour:** 2026-10-06  
**Testé avec:** GroupDocs.Redaction 23.10 for .NET  
**Auteur:** GroupDocs  

---  

### Tutoriels GroupDocs.Redaction pour .NET – comment masquer les pages PDF

### [Tutoriels de démarrage](./getting-started/)

Commencez ici si vous êtes nouveau avec GroupDocs.Redaction. Ce tutoriel vous guide à travers l’installation, la licence et la création de votre premier projet de rédaction en .NET. Vous verrez comment ouvrir un document, définir une règle de rédaction simple et enregistrer le fichier assaini.

### [Techniques avancées de rédaction](./advanced-redaction/)

Approfondissez avec des gestionnaires de rédaction personnalisés, des politiques, des rappels et une rédaction assistée par IA. Ce guide vous montre comment créer des pipelines flexibles capables de **masquer des pages PDF**, de gérer des structures de documents complexes et d’intégrer des modèles d’apprentissage automatique pour une détection de contenu plus intelligente.

### [Tutoriels de rédaction d’annotations](./annotation-redaction/)

Les annotations contiennent souvent des notes confidentielles. Apprenez à localiser, modifier ou supprimer complètement les annotations, commentaires et balisages de révision des PDF, fichiers Word et autres formats pris en charge.

### [Tutoriels d’information sur les documents](./document-information/)

Comprendre les métadonnées d’un document est la première étape d’une rédaction sécurisée. Ce tutoriel explique comment récupérer les propriétés du document, répertorier les formats pris en charge et générer des images d’aperçu avant d’appliquer une rédaction.

### [Tutoriels de chargement de documents](./document-loading/)

Les documents peuvent résider sur le disque, dans des flux ou derrière des couches d’authentification. Apprenez les meilleures pratiques pour charger en toute sécurité des fichiers locaux, des flux mémoire et des documents protégés par mot de passe.

### [Tutoriels d’enregistrement de documents](./document-saving/)

Après la rédaction, vous devrez conserver le fichier nettoyé. Ce guide couvre l’enregistrement au format original, l’exportation vers un PDF rasterisé et la diffusion des résultats directement vers une application côté client.

### [Tutoriels de gestion des formats](./format-handling/)

GroupDocs.Redaction prend en charge un large éventail de formats. Explorez comment travailler avec différents types de fichiers, créer des gestionnaires de formats personnalisés et étendre la bibliothèque pour couvrir des normes de documents spécialisées.

### [Tutoriels de rédaction d’images](./image-redaction/)

Les images peuvent masquer des données visuelles sensibles. Apprenez à masquer des régions d’image spécifiques, à supprimer les images intégrées et à nettoyer les métadonnées d’image afin de garantir qu’aucune information cachée ne subsiste.

### [Tutoriels de licence et de configuration](./licensing-configuration/)

Une licence appropriée est essentielle pour une utilisation en production. Ce tutoriel vous montre comment appliquer les licences, configurer les paramètres d’exécution et mettre en œuvre une licence à la consommation pour des déploiements évolutifs.

### [Tutoriels de rédaction de métadonnées](./metadata-redaction/)

Les métadonnées divulguent souvent des détails confidentiels. Suivez ce guide pour supprimer les propriétés du document, les commentaires cachés et d’autres métadonnées des fichiers PDF, Word, Excel et PowerPoint.

### [Tutoriels d’intégration OCR](./ocr-integration/)

Lors du traitement de PDF numérisés ou d’images, l’OCR est essentiel. Apprenez à intégrer des moteurs OCR, extraire le texte recherchable, puis **masquer des pages PDF** contenant des informations sensibles.

### [Tutoriels de rédaction de pages](./page-redaction/)

Parfois, vous devez éliminer des pages entières. Ce tutoriel montre comment supprimer des pages individuelles, des plages de pages et supprimer conditionnellement des pages en fonction du contenu.

### [Tutoriels de rédaction spécifiques aux PDF](./pdf-specific-redaction/)

Les PDF possèdent des fonctionnalités uniques comme les calques, les annotations et les champs de formulaire. Maîtrisez les techniques de rédaction propres aux PDF, y compris le filtrage de contenu et la préservation de l’intégrité du document.

### [Tutoriels d’options de rasterisation](./rasterization-options/)

Les PDF rasterisés transforment le contenu en images, rendant l’extraction de données impossible. Apprenez à configurer le bruit, l’inclinaison, le niveau de gris et les bordures, et découvrez comment **enregistrer des PDF rasterisés** pour une sécurité maximale.

### [Tutoriels de rédaction de feuilles de calcul](./spreadsheet-redaction/)

Les feuilles de calcul Excel contiennent souvent des cellules confidentielles. Ce guide vous montre comment cibler et **masquer des cellules Excel**, masquer les formules et protéger les feuilles de calcul sensibles.

### [Tutoriels de rédaction de texte](./text-redaction/)

Le texte est le type de données le plus courant à protéger. Suivez les instructions étape par étape pour la correspondance exacte de phrases, la rédaction par expression régulière et les recherches sensibles à la casse, y compris comment **masquer du texte Word** efficacement.

## Tutoriels associés

- [Comment supprimer les annotations – Tutoriels de rédaction d’annotations pour GroupDocs.Redaction .NET](/redaction/net/annotation-redaction/)
- [Comment supprimer la dernière page d’un PDF en utilisant GroupDocs.Redaction pour .NET](/redaction/net/page-redaction/remove-last-page-pdf-groupdocs-redaction-net/)
- [Comment masquer un PDF et l’enregistrer en PDF rasterisé avec GroupDocs.Redaction pour .NET](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)