---
date: 2026-08-04
description: Apprenez comment filtrer les données de feuille de calcul java et masquer
  en toute sécurité des colonnes ou des cellules dans les feuilles de calcul Excel
  à l'aide de GroupDocs.Redaction pour Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Apprenez comment filtrer les données de feuille de calcul java et
  masquer en toute sécurité des colonnes ou des cellules dans les feuilles de calcul
  Excel à l'aide de GroupDocs.Redaction pour Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Filtrer les données de feuille de calcul java – guide avec GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Filtrer les données de feuille de calcul java – guide avec GroupDocs.Redaction
type: docs
url: /fr/java/spreadsheet-redaction/
weight: 12
---

# Filtrer les données de feuille de calcul java – Tutoriel GroupDocs.Redaction Java

Si vous devez **filter spreadsheet data java** avant d'appliquer la rédaction, vous êtes au bon endroit. Dans ce tutoriel, vous découvrirez comment isoler les lignes, colonnes ou cellules individuelles contenant des informations personnelles ou confidentielles, puis les rédiger en toute sécurité avec GroupDocs.Redaction pour Java. Les étapes sont expliquées en termes simples, incluent des conseils de bonnes pratiques et montrent comment maintenir un traitement rapide même sur de grands classeurs.

## Réponses rapides
- **Quelle bibliothèque gère la rédaction de feuilles de calcul en Java ?** GroupDocs.Redaction for Java.  
- **Puis-je filtrer les lignes sans charger le fichier complet en mémoire ?** Oui – l'API diffuse les données et vous permet d'appliquer des filtres à la volée.  
- **Quels formats de fichiers sont pris en charge ?** Over 30 spreadsheet formats, including XLS, XLSX, CSV, and ODS.  
- **Ai‑je besoin d'une licence pour le développement ?** A temporary license works for testing; a full license is required for production.  
- **Existe‑t‑il une limite de taille pour le classeur ?** The engine can process files up to 500 MB without excessive memory consumption.

## Qu'est‑ce que filter spreadsheet data java ?
**Filter spreadsheet data java** est le processus de sélection programmatique de lignes, colonnes ou cellules spécifiques dans un classeur de type Excel à l'aide de code Java afin que seul le contenu ciblé soit examiné ou rédigé. Cette technique réduit le temps d'exécution, limite les modifications inutiles et aide à respecter la conformité de type RGPD.

## Pourquoi filter spreadsheet data java ?
GroupDocs.Redaction Java prend en charge **30+ formats de feuilles de calcul** et peut traiter des classeurs contenant **jusqu'à 500 Mo** (environ 1 million de lignes) tout en maintenant l'utilisation de la mémoire en dessous de **200 Mo**. En filtrant d'abord, vous évitez de toucher aux données non pertinentes, ce qui réduit le temps de traitement de **40‑60 %** en moyenne pour les scénarios typiques de nettoyage de la vie privée.

## Prérequis
- Java 17 ou version ultérieure installé.  
- Système de construction Maven ou Gradle.  
- GroupDocs.Redaction pour Java (téléchargeable depuis le site officiel).  
- Une clé de licence temporaire ou complète.  

## Comment filtrer les données dans les feuilles de calcul en utilisant GroupDocs.Redaction Java ?
Chargez le classeur, définissez un filtre qui correspond aux cellules que vous souhaitez rédiger, puis appliquez l'opération de rédaction. L'API effectue le filtrage de manière flux, de sorte que vous n'avez jamais besoin de garder le fichier complet en RAM.

La classe `RedactionFilter` vous permet de spécifier les index de colonnes, les plages de lignes ou des prédicats personnalisés. Par exemple, vous pouvez cibler chaque cellule de la colonne **B** contenant un motif d'adresse e‑mail, ou vous pouvez restreindre la rédaction aux lignes où la colonne « Status » vaut « Confidential ».

**Réponse directe (40‑70 mots) :**  
Créez une instance de `RedactionFilter`, définissez l'index de colonne et une condition d'expression régulière, puis transmettez le filtre à `Redactor.redact(workbook, filter)`. Ce filtre en une seule ligne isole les cellules exactes correspondant à vos critères, et le rédacteur les supprime ou les masque tout en laissant le reste de la feuille intact. L'opération se termine en temps linéaire par rapport aux lignes filtrées.

### Étape 1 : instancier le filtre
`RedactionFilter` est la classe principale qui représente une règle de filtrage pour la rédaction de feuilles de calcul. Elle accepte les numéros de colonnes, les numéros de lignes ou des expressions lambda personnalisées pour cibler les données.

### Étape 2 : configurer la condition
Utilisez `filter.setColumnIndex(1)` pour cibler la colonne B (indice zéro) et `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` pour correspondre aux motifs d'e‑mail. Vous pouvez également combiner plusieurs conditions avec `filter.and(...)` ou `filter.or(...)`.

### Étape 3 : appliquer la rédaction
`Redactor` est la classe principale qui exécute les opérations de rédaction sur un classeur.  
Passez le classeur et le filtre configuré à l'objet `Redactor`. L'API diffuse le classeur, applique le filtre et écrit le résultat rédigé dans un nouveau fichier, en préservant le formatage et les formules d'origine.

## Problèmes courants et solutions
- **Le filtre ne correspond à aucune cellule :** Vérifiez l'index de colonne (indice zéro) et assurez-vous que la syntaxe de l'expression régulière est correcte pour Java.  
- **Erreurs de mémoire insuffisante sur de gros fichiers :** Augmentez modestement la taille du tas JVM (par ex., `-Xmx1g`) ou divisez le classeur en morceaux plus petits avant le filtrage.  
- **La sortie rédigée perd le formatage :** `RedactionOptions` vous permet de personnaliser le comportement de rédaction, comme la préservation du format des cellules. Utilisez `RedactionOptions.setPreserveFormatting(true)` pour conserver les styles de cellules intacts.

## Pourquoi filter spreadsheet data ?
Filtrer avant la rédaction isole uniquement les parties sensibles d'un classeur, ce qui vous évite des modifications inutiles des données propres. Cette approche sélective réduit également le risque de perte accidentelle de données et accélère les audits de conformité car le journal d'audit contient beaucoup moins d'entrées.

## Comment rédiger les e‑mails dans les feuilles de calcul Excel en utilisant l'API GroupDocs.Redaction Java
Chargez votre fichier Excel, appliquez un filtre recherchant le motif d'e‑mail typique, et invoquez le rédacteur. L'API remplace chaque e‑mail correspondant par un espace réservé tel que « ***@***.com » tout en préservant la mise en page des cellules environnantes.

## Comment filtrer les données – tutoriels disponibles
- [Comment rédiger les e‑mails dans les feuilles de calcul Excel en utilisant l'API GroupDocs.Redaction Java](./redact-emails-excel-groupdocs-redaction-java/)

## Ressources supplémentaires
- [Documentation GroupDocs.Redaction pour Java](https://docs.groupdocs.com/redaction/java/)
- [Référence API GroupDocs.Redaction pour Java](https://reference.groupdocs.com/redaction/java/)
- [Télécharger GroupDocs.Redaction pour Java](https://releases.groupdocs.com/redaction/java/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Support gratuit](https://forum.groupdocs.com/)
- [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)

---

**Dernière mise à jour:** 2026-08-04  
**Testé avec:** GroupDocs.Redaction 23.11 for Java  
**Auteur:** GroupDocs  

## Questions fréquemment posées
**Q : Puis‑je filtrer plusieurs colonnes à la fois ?**  
A : Yes, you can add additional column indexes to the same `RedactionFilter` instance or chain multiple filters with `filter.or(...)`.

**Q : Le filtre fonctionne‑t‑il sur des classeurs protégés par mot de passe ?**  
A : Provide the password when opening the workbook; the filter operates after decryption just like on an unprotected file.

**Q : Combien de lignes l'API peut‑elle gérer en une seule opération ?**  
A : The engine is optimized for up to 1 million rows (≈500 MB) without loading the entire file into memory.

**Q : Est‑il possible d'apercevoir quelles cellules seront rédigées avant l'enregistrement ?**  
A : Yes, call `filter.preview(workbook)` to get a list of cell addresses that match the criteria.

**Q : Quel modèle de licence est requis pour une utilisation en production ?**  
A : A full commercial license is required for production deployments; a temporary license is sufficient for testing and evaluation.

## Tutoriels associés
- [Comment rédiger les données sensibles dans les feuilles de calcul Excel en utilisant l'API GroupDocs.Redaction Java](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Masquer les données sensibles Java – Guide GroupDocs.Redaction](/redaction/java/getting-started/)
- [Masquer les données sensibles Java – Rédiger les informations personnelles avec GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)