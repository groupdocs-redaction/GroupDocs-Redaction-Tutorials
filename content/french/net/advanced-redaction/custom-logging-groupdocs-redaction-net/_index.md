---
date: '2026-03-28'
description: Apprenez à implémenter un logger personnalisé C# dans GroupDocs.Redaction
  pour .NET, permettant une journalisation personnalisée détaillée et une génération
  de rapports de conformité plus simple.
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: Implémenter un logger personnalisé C# dans GroupDocs.Redaction pour .NET
type: docs
url: /fr/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# Implémenter un logger personnalisé c# dans GroupDocs.Redaction pour .NET

Gérer les censures de documents de manière efficace est essentiel, surtout lorsqu’il s’agit d’informations sensibles. Dans ce guide, vous apprendrez **comment implémenter un logger personnalisé c#** avec GroupDocs.Redaction pour .NET, vous offrant un contrôle complet sur la journalisation, la gestion des erreurs et les traces d’audit.

## Réponses rapides
- **Que fait un logger personnalisé c# ?** Il capture les erreurs, les avertissements et les messages d'information pendant la censure.  
- **Quelle bibliothèque fournit l'interface ILogger ?** GroupDocs.Redaction pour .NET.  
- **Puis-je enregistrer le document censuré sans rasterisation ?** Oui – utilisez `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`.  
- **Ai-je besoin d'une licence pour une utilisation en production ?** Une licence complète est requise pour la production ; une version d'essai est disponible pour l'évaluation.  
- **Cette approche est‑elle compatible avec .NET Core / .NET 6+ ?** Absolument – la même API fonctionne sur .NET Framework et .NET Core/5/6.

## Qu'est‑ce qu'un logger personnalisé c# ?
Un **logger personnalisé c#** est une classe qui implémente l'interface `ILogger` fournie par GroupDocs.Redaction. Il vous permet d'acheminer les messages de journalisation où vous le souhaitez — console, fichier, base de données ou systèmes de surveillance externes — tout en vous offrant une vue claire du flux de travail de la censure.

## Pourquoi utiliser la journalisation personnalisée .net avec GroupDocs.Redaction ?
- **Conformité & Audit :** Des journaux détaillés répondent aux exigences réglementaires.  
- **Visibilité des erreurs :** `LogError` et `LogWarning` vous donnent un retour immédiat sur les problèmes.  
- **Flexibilité d'intégration :** Transférez les journaux vers les frameworks de journalisation .NET existants (Serilog, NLog, etc.).

## Prérequis
- **GroupDocs.Redaction pour .NET** installé (voir l'installation ci‑dessous).  
- Un environnement de développement .NET (Visual Studio, VS Code ou CLI).  
- Connaissances de base en C# et familiarité avec les flux de fichiers.

## Installation

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Gestionnaire de packages**  
```powershell
Install-Package GroupDocs.Redaction
```

**Interface du gestionnaire de packages NuGet**  
Recherchez **"GroupDocs.Redaction"** et installez la dernière version.

## Acquisition de licence
- **Essai gratuit :** Testez l'API avec une licence temporaire.  
- **Licence temporaire :** Obtenez un accès complet aux fonctionnalités pendant une période limitée.  
- **Achat :** Procurez-vous une licence perpétuelle pour les déploiements en production.

## Guide étape par étape

### Étape 1 : Définir une classe de logger personnalisée (log warnings c#)
Créez une classe qui implémente `ILogger`. Cette classe capturera les erreurs, les avertissements et les messages d'information.

```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```

**Explication :** Le drapeau `HasErrors` vous aide à décider s'il faut poursuivre le traitement. Les trois méthodes correspondent aux trois niveaux de journalisation dont vous aurez besoin dans la plupart des scénarios de censure.

### Étape 2 : Préparer les chemins de fichiers et ouvrir le document source
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**Pourquoi c'est important :** L'utilisation de méthodes utilitaires garde votre code propre et garantit que le dossier de sortie existe avant d'essayer de **enregistrer le document censuré**.

### Étape 3 : Appliquer les censures en utilisant le logger personnalisé
```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```

**Explication :**  
1. Le `Redactor` est instancié avec `RedactorSettings(logger)`, liant votre `CustomLogger`.  
2. Après avoir appliqué une censure, le code vérifie `logger.HasErrors`. S'il n'y a pas eu d'erreurs, le document est enregistré — démontrant la logique de **enregistrement du document censuré** sans rasterisation.

### Pièges courants & Dépannage
- **Sortie de journal manquante :** Vérifiez que chaque méthode `Log*` est correctement surchargée.  
- **Exceptions d'accès aux fichiers :** Assurez‑vous que l'application possède les permissions de lecture/écriture pour les chemins source et de sortie.  
- **Logger non connecté :** Le paramètre `RedactorSettings(logger)` est essentiel ; le omettre désactive la journalisation personnalisée.

## Applications pratiques
1. **Rapports de conformité :** Exportez les entrées de journal vers un CSV ou une base de données pour les traces d'audit.  
2. **Suivi des erreurs :** Localisez rapidement les fichiers problématiques en analysant la sortie de `LogError`.  
3. **Automatisation du flux de travail :** Déclenchez des processus en aval (par ex., notifier un responsable conformité) lorsque `LogWarning` est invoqué.

## Considérations de performance
- **Libérez les flux rapidement** pour libérer la mémoire, surtout lors du traitement de gros lots.  
- **Surveillez le CPU & la mémoire** pendant les censures en masse ; envisagez de traiter les documents en parallèle avec une synchronisation prudente du logger.  
- **Restez à jour :** Les versions plus récentes de GroupDocs.Redaction incluent souvent des optimisations de performance et des points d'extension de journalisation supplémentaires.

## Conclusion
En implémentant un **logger personnalisé c#**, vous obtenez une visibilité granulaire sur chaque étape du pipeline de censure, facilitant le respect des normes de conformité et le débogage des problèmes. L'approche présentée ici fonctionne parfaitement avec GroupDocs.Redaction pour .NET et peut être étendue pour s'intégrer à n'importe quel framework de journalisation .NET que vous utilisez déjà.

---

## Questions fréquemment posées

**Q : Quel est le but de la journalisation personnalisée avec GroupDocs.Redaction ?**  
R : La journalisation personnalisée aide à suivre et gérer les censures pour la conformité, le suivi des erreurs et l'optimisation du flux de travail.

**Q : Comment gérer les erreurs avec un logger personnalisé ?**  
R : Implémentez `LogError` dans votre classe `CustomLogger` ; le drapeau `HasErrors` vous permet d’arrêter le traitement si nécessaire.

**Q : La journalisation personnalisée peut‑elle être intégrée à d'autres systèmes ?**  
R : Oui, vous pouvez transmettre les messages de journalisation à un CRM, ERP ou à des outils de surveillance centralisés en étendant les méthodes du logger.

**Q : Quels sont les pièges courants lors de l'implémentation de la journalisation personnalisée ?**  
R : Des implémentations de méthodes incorrectes, l'absence de `RedactorSettings(logger)` et des problèmes de permissions de fichiers sont les plus fréquents.

**Q : Comment la journalisation personnalisée améliore‑t‑elle les flux de travail de censure de documents ?**  
R : Des journaux détaillés offrent une visibilité en temps réel, simplifient le dépannage et répondent aux exigences d’audit.

## Ressources
- **Documentation :** [Documentation .NET de GroupDocs.Redaction](https://docs.groupdocs.com/redaction/net/)
- **Référence API :** [Référence API de GroupDocs.Redaction](https://reference.groupdocs.com/redaction/net)
- **Téléchargement :** [GroupDocs.Redaction pour .NET](https://downloads.groupdocs.com/redaction/net)

---

**Dernière mise à jour :** 2026-03-28  
**Testé avec :** GroupDocs.Redaction 23.11 pour .NET  
**Auteur :** GroupDocs  

---