---
title: Guide de disponibilité et des ressources Advanced Threat Analytics
description: Fournit une liste de ressources, de vidéos et de liens de démarrage, de déploiement et de guide de préparation pour ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 7/15/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 42a1a34f-ed6b-4538-befb-452168a30e8c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7f8413ba144196a4f64e21dfd688583a05b874ed
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/18/2021
ms.locfileid: "101096988"
---
# <a name="ata-readiness-roadmap"></a>Guide de préparation à ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Cet article fournit un guide de préparation qui vous aide à bien démarrer avec Advanced Threat Analytics.

## <a name="understanding-ata"></a>Présentation d’ATA

Advanced Threat Analytics (ATA) est une plateforme locale qui aide à protéger votre entreprise contre de nombreux types de cyberattaques ciblés et de menaces internes. Utilisez les ressources suivantes pour en savoir plus sur ATA :

- [Vue d’ensemble d’ATA](what-is-ata.md)

- [Vidéo d’introduction à ATA - version courte](https://aka.ms/ATAShort)

- [Vidéo d’introduction à ATA - version longue](https://aka.ms/ATAVideo)

## <a name="deployment-decisions"></a>Décisions de déploiement

ATA se compose du Centre ATA que vous pouvez installer sur un serveur, et de passerelles ATA que vous pouvez installer sur des ordinateurs distincts ou utiliser sous forme de passerelles légères directement sur vos contrôleurs de domaine. Avant d’être opérationnel, il est important de prendre les décisions de déploiement suivantes :

|Configuration | Décision |
|----|----|
|Type de matériel|Physique, virtuel, machine virtuelle Azure|
|Groupe de travail ou domaine|Groupe de travail, domaine|
|Dimensionnement de la passerelle|Passerelle complète, passerelle légère|
|Certificats|PKI, auto-signé|

Si vous utilisez des serveurs physiques, vous devez planifier la capacité. Vous pouvez vous aider de l’outil de dimensionnement pour allouer de l’espace pour ATA :

[Outil de dimensionnement ATA](ata-capacity-planning.md) : l’outil de dimensionnement automatise la collecte de la quantité de trafic ATA nécessaire. Il fournit automatiquement des recommandations de prise en charge et de ressource pour le Centre ATA et les passerelles légères ATA.

[Planification de la capacité ATA](ata-capacity-planning.md)

## <a name="deploy-ata"></a>Déployer ATA

Ces ressources vous permettent de télécharger et d’installer le Centre ATA, de vous connecter à Active Directory, de télécharger le package des passerelles ATA, de configurer la collecte d’événements et éventuellement de procéder à l’intégration avec votre VPN, puis de configurer les exclusions et les comptes honeytoken.

[Télécharger ATA](https://aka.ms/ataeval) -Avant de déployer ATA, si vous n’avez pas pris la décision d’acheter ATA, vous pouvez télécharger la version d’évaluation.

[Manuel ATA POC](/samples/browse/?redirectedfrom=TechNet-Gallery) -Vous guide dans toutes les étapes nécessaires pour effectuer un déploiement POC d’ATA.

[Vidéo de déploiement d’ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes) - Cette vidéo fournit une vue d’ensemble des étapes de déploiement d’ATA en moins de 10 minutes.

## <a name="ata-settings"></a>Paramètres ATA

Les paramètres nécessaires de base dans ATA sont configurés dans l’Assistant d’installation. Toutefois, vous pouvez configurer d’autres paramètres pour régler ATA de sorte à obtenir des détections plus précises pour votre environnement, telles que l’intégration SIEM et les paramètres d’audit.

[Paramètres d’audit](https://aka.ms/ataauditingblog) – Auditez l’intégrité de votre contrôleur de domaine avant et après un déploiement d’ATA.

[Documentation générale d’ATA](index.yml)

## <a name="work-with-ata"></a>Utiliser ATA

Une fois qu’ATA est opérationnel, vous pouvez voir les activités suspectes détectées dans la chronologie des attaques. Il s’agit de la page de destination qui s’affiche par défaut quand vous vous connectez à la console ATA. Par défaut, toutes les activités suspectes ouvertes sont affichées dans la chronologie des attaques. Vous pouvez également voir le niveau de gravité attribué à chaque activité. Investiguez sur chaque activité suspecte en explorant les entités (ordinateurs, appareils, utilisateurs) pour ouvrir leurs pages de profil qui contiennent des informations supplémentaires. Ces ressources vous permettent d’utiliser les activités suspectes d’ATA :

[Manuel sur les activités suspectes d’ATA](/samples/browse/?redirectedfrom=TechNet-Gallery) : cet article vous guide dans les techniques d’attaque contre le vol d’informations d’identification à l’aide d’outils de recherche facilement disponibles sur Internet. À chaque point de l’attaque, vous pouvez voir comment ATA vous permet d’y voir plus clair dans ces menaces.

[Guide des activités suspectes d’ATA](suspicious-activity-guide.md)

## <a name="security-best-practices"></a>Bonnes pratiques de sécurité

[Bonnes pratiques d’ATA](https://aka.ms/atasecbestpractices) - Bonnes pratiques pour la sécurisation d’ATA.

[Questions fréquentes sur ATA](ata-technical-faq.md) - Cet article fournit des éléments d’informations et des réponses aux questions les plus fréquemment posées sur ATA.

## <a name="additional-resources"></a>Ressources supplémentaires

[Page Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Ressources communautaires

[Blog ATA](https://aka.ms/ATABlog) 
 [Communauté ATA](https://aka.ms/ATACommunity)