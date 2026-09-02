---
date: 2026-06-11
description: Apprenez à charger un document, y compris depuis des flux et des fichiers
  protégés par mot de passe, en utilisant GroupDocs.Redaction pour .NET.
keywords:
- how to load document
- redact password protected pdf
- load password protected file
- load document from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to load document, including from streams and password‑protected
    files, using GroupDocs.Redaction for .NET.
  headline: How to Load Document with GroupDocs.Redaction for .NET
  type: TechArticle
- questions:
  - answer: Yes—GroupDocs.Redaction automatically detects the DOCX format when you
      pass the file path or stream, so no extra code is needed.
    question: Can I load DOCX files the same way I load PDFs?
  - answer: Absolutely. Retrieve the blob as a byte array or stream and feed it to
      the `RedactionEngine` constructor.
    question: Does the library support loading files from Azure Blob Storage?
  - answer: The constructor throws a `PasswordIncorrectException`. Catch this exception
      to prompt the user for the correct password.
    question: What happens if I provide the wrong password?
  - answer: Yes—each `RedactionEngine` instance is independent and thread‑safe, allowing
      parallel processing in background services.
    question: Is it possible to load multiple documents simultaneously?
  - answer: The engine implements `IDisposable`. Call `Dispose()` or wrap it in a
      `using` block to release file handles promptly.
    question: Do I need to dispose of the RedactionEngine manually?
  type: FAQPage
title: Comment charger un document avec GroupDocs.Redaction pour .NET
type: docs
url: /fr/net/document-loading/
weight: 2
---

# Comment charger un document avec GroupDocs.Redaction pour .NET

Dans ce guide, vous découvrirez **comment charger un document** dans GroupDocs.Redaction pour .NET à partir de diverses sources — disque local, flux mémoire, et même des fichiers protégés par mot de passe. Que vous construisiez un service de rédaction, un pipeline de conformité automatisé, ou une simple utilité de bureau, maîtriser ces techniques de chargement vous permet de préparer rapidement et de manière fiable tout document pour une rédaction sécurisée.

## Réponses rapides
- **Quelle est la première étape ?** Installez le package NuGet GroupDocs.Redaction et ajoutez l'espace de noms `using GroupDocs.Redaction;`.
- **Puis-je charger un PDF depuis un flux ?** Oui — transmettez un `MemoryStream` contenant les octets du PDF au constructeur `RedactionEngine`.
- **Comment ouvrir un fichier protégé par mot de passe ?** Fournissez le mot de passe comme deuxième argument lors de la création du `RedactionEngine`.
- **Existe‑t‑il une limite de taille de fichier ?** GroupDocs.Redaction traite les fichiers jusqu’à 2 GB sans charger le fichier complet en mémoire.
- **Ai‑je besoin d’une licence pour le développement ?** Une licence temporaire fonctionne pour les tests ; une licence complète est requise pour les déploiements en production.

## Comment charger un document ?
`RedactionEngine` est la classe principale qui charge et prépare les documents pour la rédaction. Chargez un document en créant une instance de `RedactionEngine` avec le chemin du fichier (ou le flux) et, si nécessaire, le mot de passe. Cet appel en une seule ligne lit le fichier, valide le format et construit le modèle interne du document prêt pour la rédaction. Par exemple, charger un PDF depuis le disque est aussi simple que `new RedactionEngine("sample.pdf")`. Lorsqu’un mot de passe est requis, utilisez `new RedactionEngine("secret.pdf", "MyPassword")`. Le chargement depuis un flux suit le même modèle avec un argument `MemoryStream`.

## Qu’est‑ce que GroupDocs.Redaction ?
GroupDocs.Redaction est une bibliothèque .NET qui permet aux développeurs de localiser et de supprimer de façon permanente le contenu sensible des PDF, DOCX, PPTX et de plus de 30 autres formats de fichiers. Elle offre une rédaction pixel‑parfait, la prise en charge de l’OCR et le traitement par lots, ce qui la rend idéale pour les applications axées sur la conformité qui nécessitent une protection des données fiable et sécurisée sur de nombreux types de documents.

## Pourquoi utiliser GroupDocs.Redaction pour le chargement de documents ?
GroupDocs.Redaction fournit un moteur de streaming haute performance et à faible consommation de mémoire capable de gérer de gros fichiers jusqu’à 2 GB, tout en prenant en charge les documents protégés par mot de passe dès le départ. Cette combinaison de rapidité, de flexibilité et de sécurité en fait le choix privilégié des développeurs qui doivent charger des documents rapidement et en toute sécurité avant d’appliquer les règles de rédaction.

- **Large prise en charge des formats :** Gère **30+** types de documents, y compris PDF, Word, Excel, PowerPoint et les fichiers image.
- **Streaming haute performance :** Traite les fichiers jusqu’à **2 GB** en utilisant un moteur de streaming à faible consommation de mémoire, éliminant ainsi le besoin de charger le fichier complet.
- **Gestion des mots de passe :** Ouvre sans effort les **PDF et fichiers Office protégés par mot de passe** avec une surcharge de méthode unique, réduisant la complexité du code.
- **API thread‑safe :** Permet le chargement concurrent de plusieurs documents dans des services multithread sans conditions de concurrence.

## Prérequis
- .NET 6.0 ou ultérieur (la bibliothèque prend également en charge .NET Core 3.1 et .NET Framework 4.6.1+).
- Une licence valide GroupDocs.Redaction (licence temporaire pour les tests).
- Accès aux fichiers de documents que vous souhaitez rédiger (chemin local, tableau d’octets ou flux).

## Chargement de documents à partir de différentes sources

### Chargement depuis le disque local
Fournissez le chemin absolu ou relatif du fichier lors de la construction du moteur. La bibliothèque détecte automatiquement le format et le prépare pour la rédaction.

### Chargement depuis un flux mémoire
Lisez le fichier dans un `byte[]`, encapsulez‑le dans un `MemoryStream` et passez le flux au constructeur. Cette approche est parfaite pour les API web qui reçoivent des fichiers en tant que téléchargements.

### Chargement de fichiers protégés par mot de passe
Lorsqu’un document est chiffré, fournissez le mot de passe comme deuxième argument. Le moteur déchiffre le fichier à la volée et rend le contenu disponible pour la rédaction sans étapes supplémentaires.

## Problèmes courants et solutions
- **Erreur : « File format not supported. »**  
  Vérifiez que l’extension du fichier correspond à un format pris en charge et que le fichier n’est pas corrompu. GroupDocs.Redaction prend en charge plus de 30 formats ; consultez la référence API pour la liste complète.
- **Exception liée au mot de passe.**  
  Assurez‑vous que la chaîne du mot de passe est correcte et que le fichier nécessite réellement un mot de passe. Passer une chaîne vide à un fichier protégé déclenchera une erreur d’authentification.
- **Manque de mémoire pour des fichiers très volumineux.**  
  Utilisez la surcharge de streaming (`RedactionEngine(Stream)`) au lieu de charger le fichier par chemin. Cela maintient une faible utilisation de la mémoire même pour des PDF de plusieurs centaines de pages.

## Questions fréquemment posées
**Q : Puis‑je charger des fichiers DOCX de la même manière que les PDF ?**  
A : Oui—GroupDocs.Redaction détecte automatiquement le format DOCX lorsque vous passez le chemin du fichier ou le flux, donc aucun code supplémentaire n’est nécessaire.

**Q : La bibliothèque prend‑elle en charge le chargement de fichiers depuis Azure Blob Storage ?**  
A : Absolument. Récupérez le blob sous forme de tableau d’octets ou de flux et transmettez‑le au constructeur `RedactionEngine`.

**Q : Que se passe‑t‑il si je fournis un mauvais mot de passe ?**  
A : Le constructeur lève une `PasswordIncorrectException`. Capturez cette exception pour inviter l’utilisateur à saisir le bon mot de passe.

**Q : Est‑il possible de charger plusieurs documents simultanément ?**  
A : Oui—chaque instance de `RedactionEngine` est indépendante et thread‑safe, permettant le traitement parallèle dans les services en arrière‑plan.

**Q : Dois‑je disposer manuellement du RedactionEngine ?**  
A : Le moteur implémente `IDisposable`. Appelez `Dispose()` ou encapsulez‑le dans un bloc `using` pour libérer rapidement les poignées de fichiers.

## Ressources supplémentaires
- [Comment charger et rédiger des documents avec GroupDocs.Redaction .NET : guide complet](./groupdocs-redaction-net-load-redact-documents/)
- [Comment rédiger en toute sécurité des documents protégés par mot de passe avec GroupDocs.Redaction en .NET](./secure-redact-password-protected-documents-groupdocs-redaction-net/)
- [Documentation GroupDocs.Redaction pour .NET](https://docs.groupdocs.com/redaction/net/)
- [Référence API GroupDocs.Redaction pour .NET](https://reference.groupdocs.com/redaction/net/)
- [Télécharger GroupDocs.Redaction pour .NET](https://releases.groupdocs.com/redaction/net/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Support gratuit](https://forum.groupdocs.com/)
- [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)

---

**Dernière mise à jour :** 2026-06-11  
**Testé avec :** GroupDocs.Redaction 5.5 for .NET  
**Auteur :** GroupDocs

## Tutoriels associés
- [Comment charger et rédiger des documents avec GroupDocs.Redaction .NET : guide complet](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Rédiger et enregistrer des documents avec GroupDocs.Redaction pour .NET : guide complet](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)