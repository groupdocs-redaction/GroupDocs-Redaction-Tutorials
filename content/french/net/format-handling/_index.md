---
date: 2026-07-15
description: Apprenez à créer un gestionnaire de rédaction personnalisé et à ajouter
  la prise en charge d’un nouveau format de fichier avec GroupDocs.Redaction pour
  .NET.
keywords:
- create custom redaction handler
- add new file format
- GroupDocs.Redaction format handling
lastmod: 2026-07-15
og_description: Créez un gestionnaire de rédaction personnalisé et ajoutez la prise
  en charge d’un nouveau format de fichier avec GroupDocs.Redaction pour .NET. Découvrez
  des guides étape par étape pour étendre la gestion des formats.
og_image_alt: Guide to creating a custom redaction handler in GroupDocs.Redaction
  for .NET
og_title: Créer un gestionnaire de rédaction personnalisé – GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to create custom redaction handler and add new file format
    support using GroupDocs.Redaction for .NET.
  headline: Create Custom Redaction Handler in GroupDocs.Redaction .NET
  type: TechArticle
tags:
- redaction handler
- GroupDocs.Redaction
- .NET document processing
- custom format extension
title: Créer un gestionnaire de rédaction personnalisé dans GroupDocs.Redaction .NET
type: docs
url: /fr/net/format-handling/
weight: 14
---

# Créer un gestionnaire de rédaction personnalisé dans GroupDocs.Redaction .NET

Étendez les capacités de GroupDocs.Redaction avec nos tutoriels de gestion de formats pour les développeurs .NET. Dans ce hub, vous apprendrez comment **créer un gestionnaire de rédaction personnalisé** et **ajouter la prise en charge d'un nouveau format de fichier**, travailler avec des documents texte brut et gérer programmatiquement divers types de documents. Ces guides incluent des exemples C# prêts à l'exécution, afin que vous puissiez rapidement élargir la gamme de fichiers que votre application peut sécuriser.

## Vue d'ensemble rapide

- **Ce que vous gagnerez :** Capacité de masquer des types de contenu personnalisés et de prendre en charge des extensions de fichiers supplémentaires sans attendre les mises à jour du produit.  
- **À qui cela s'adresse :** Développeurs .NET créant des solutions centrées sur les documents qui nécessitent des contrôles de confidentialité stricts.  
- **Prérequis :** .NET 6+ (ou .NET Framework 4.7.2+), une licence valide de GroupDocs.Redaction et des connaissances de base en C#.  

## Qu'est-ce qu'un gestionnaire de rédaction personnalisé ?

Un **gestionnaire de rédaction personnalisé** est un composant défini par l'utilisateur qui indique à GroupDocs.Redaction comment localiser, interpréter et masquer le contenu qui n'est pas couvert par les modèles intégrés. En implémentant ce gestionnaire, vous obtenez un contrôle total sur les formats de données propriétaires ou les identifiants métier uniques.

## Comment créer un gestionnaire de rédaction personnalisé ?

**IRedactionHandler** est une interface qui définit le contrat pour la logique de rédaction personnalisée.  
**Redactor** est la classe principale qui gère les opérations de rédaction.  
**AddHandler** enregistre un gestionnaire personnalisé auprès de l'instance Redactor.  
**Redact** exécute la rédaction en fonction des gestionnaires configurés.

Chargez le moteur de rédaction, enregistrez votre gestionnaire et lancez le processus de rédaction – le tout en trois étapes concises. Tout d'abord, implémentez l'interface `IRedactionHandler` avec une logique qui parcourt le document à la recherche de vos jetons personnalisés. Ensuite, ajoutez le gestionnaire à l'instance `Redactor` via `AddHandler`. Enfin, appelez `Redact` pour appliquer les modifications. Ce modèle fonctionne pour les PDF, les images et tout format pris en charge, vous permettant de protéger les données que les modèles standards ne détectent pas.

## Comment ajouter un nouveau format de fichier ?

**SupportedFormats** est une collection qui contient les extensions de fichiers reconnues par le moteur de rédaction. Enregistrez une nouvelle extension de fichier avec le moteur de rédaction en étendant la collection `SupportedFormats`. Fournissez un analyseur qui convertit le fichier entrant en un format que GroupDocs.Redaction peut traiter, puis associez l'extension à votre analyseur. Une fois enregistré, le moteur traite le nouveau format comme n'importe quel type natif, permettant une rédaction transparente sur l'ensemble du système.

## Pourquoi utiliser GroupDocs.Redaction pour la gestion de formats personnalisés ?

GroupDocs.Redaction prend en charge **plus de 70 formats d'entrée et de sortie** et peut traiter des fichiers jusqu'à **2 Go** sans charger l'intégralité du document en mémoire, offrant une rédaction à haut débit dans les environnements d'entreprise. Son architecture extensible vous permet d'intégrer des gestionnaires personnalisés en moins de 30 minutes, réduisant le temps de développement et éliminant le besoin d'outils de prétraitement tiers.

## Tutoriels disponibles

### [Étendre les types de fichiers dans GroupDocs.Redaction .NET : Guide étape par étape pour les extensions personnalisées](./extend-groupdocs-redaction-net-custom-extensions/)
Apprenez à étendre les types de fichiers pris en charge avec des extensions personnalisées en utilisant GroupDocs.Redaction pour .NET, garantissant une rédaction sécurisée des documents sur divers formats.

### [Implémentation de la liste des formats de fichiers pris en charge avec GroupDocs.Redaction .NET](./groupdocs-redaction-net-supported-formats-listing/)
Apprenez à utiliser GroupDocs.Redaction .NET pour lister les formats de fichiers pris en charge, rationaliser les systèmes de gestion de documents et optimiser les performances.

## Ressources supplémentaires

- [Documentation GroupDocs.Redaction pour .NET](https://docs.groupdocs.com/redaction/net/)
- [Référence API GroupDocs.Redaction pour .NET](https://reference.groupdocs.com/redaction/net/)
- [Télécharger GroupDocs.Redaction pour .NET](https://releases.groupdocs.com/redaction/net/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Support gratuit](https://forum.groupdocs.com/)
- [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)

**Dernière mise à jour :** 2026-07-15  
**Testé avec :** GroupDocs.Redaction 23.12 pour .NET  
**Auteur :** GroupDocs

## Tutoriels associés

- [Étendre les types de fichiers dans GroupDocs.Redaction .NET : Guide étape par étape pour les extensions personnalisées](/redaction/net/format-handling/extend-groupdocs-redaction-net-custom-extensions/)
- [Implémentation de la liste des formats de fichiers pris en charge avec GroupDocs.Redaction .NET](/redaction/net/format-handling/groupdocs-redaction-net-supported-formats-listing/)
- [Tutoriels de gestion de formats pour GroupDocs.Redaction .NET](/redaction/net/format-handling/)