---
title: Ressources et guide de préparation Advanced Threat Analytics | Microsoft Docs
description: Fournit une liste de ressources, de vidéos et de liens de démarrage, de déploiement et de guide de préparation pour ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 42a1a34f-ed6b-4538-befb-452168a30e8c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a56a24a2012239ed05f0a2f214dba345a817df39
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010225"
---
*S’applique à : Advanced Threat Analytics version 1.9*

# <a name="ata-readiness-roadmap"></a>Guide de préparation à ATA 
Ce document fournit un guide de préparation qui vous aide à bien démarrer avec Advanced Threat Analytics.

## <a name="understanding-ata"></a>Présentation d’ATA

Advanced Threat Analytics (ATA) est une plateforme locale qui aide à protéger votre entreprise contre plusieurs types d’attaques informatiques ciblées et de menaces internes avancées. Utilisez les ressources suivantes pour en savoir plus sur ATA :

- [Vue d’ensemble d’ATA](https://aka.ms/ATAOverview)

- [Vidéo d’introduction à ATA - version courte](https://aka.ms/ATAShort)

- [Vidéo d’introduction à ATA - version longue](https://aka.ms/ATAVideo) 


## <a name="deployment-decisions"></a>Décisions de déploiement

ATA se compose du Centre ATA que vous pouvez installer sur un serveur, et de passerelles ATA que vous pouvez installer sur des ordinateurs distincts ou utiliser sous forme de passerelle légère directement sur vos contrôleurs de domaine. Avant d’être opérationnel, il est important de prendre les décisions de déploiement suivantes :

|CONFIGURATION|DÉCISION|
|----|----|
|Type de matériel|Physique, virtuel, machine virtuelle Azure|
|Groupe de travail ou domaine|Groupe de travail, domaine|
|Dimensionnement de la passerelle|Passerelle complète, passerelle légère|
|Certificats|PKI, auto-signé|

Si vous utilisez des serveurs physiques, vous devez planifier la capacité. Vous pouvez vous aider de l’outil de dimensionnement pour allouer de l’espace pour ATA :

[Outil de dimensionnement ATA](http://aka.ms/atasizing) -L’outil de dimensionnement automatise la collecte des besoins en trafic d’ATA. Il fournit automatiquement des recommandations de prise en charge et de ressource pour le Centre ATA et les passerelles légères ATA.

[Planification de la capacité d’ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/ata-capacity-planning)

## <a name="deploy-ata"></a>Déployer ATA

Ces ressources vous permettent de télécharger et d’installer le Centre ATA, de vous connecter à Active Directory, de télécharger le package des passerelles ATA, de configurer la collecte d’événements et éventuellement de procéder à l’intégration avec votre VPN, puis de configurer les exclusions et les comptes honeytoken.

[Télécharger ATA](http://aka.ms/ataeval) -Avant de déployer ATA, si vous n’avez pas pris la décision d’acheter ATA, vous pouvez télécharger la version d’évaluation. 

[Manuel ATA POC](http://aka.ms/atapoc) -Vous guide dans toutes les étapes nécessaires pour effectuer un déploiement POC d’ATA.

[Vidéo de déploiement d’ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes) - Cette vidéo fournit une vue d’ensemble des étapes de déploiement d’ATA en moins de 10 minutes.

## <a name="ata-settings"></a>Paramètres ATA

Les paramètres nécessaires de base dans ATA sont configurés dans l’Assistant d’installation. Toutefois, vous pouvez configurer d’autres paramètres pour régler ATA de sorte à obtenir des détections plus précises pour votre environnement, telles que l’intégration SIEM et les paramètres d’audit.

[Paramètres d’audit](https://aka.ms/ataauditingblog) – Auditez l’intégrité de votre contrôleur de domaine avant et après un déploiement d’ATA.

[Documentation générale d’ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/)

## <a name="work-with-ata"></a>Utiliser ATA

Une fois ATA opérationnel, vous pourrez voir les activités suspectes détectées dans la chronologie des attaques. Il s’agit de la page de destination qui s’affiche par défaut quand vous vous connectez à la console ATA. Par défaut, toutes les activités suspectes ouvertes sont affichées dans la chronologie des attaques. Vous pouvez également voir le niveau de gravité attribué à chaque activité. Investiguez sur chaque activité suspecte en explorant les entités (ordinateurs, appareils, utilisateurs) pour ouvrir leurs pages de profil qui contiennent des informations supplémentaires. Ces ressources vous permettent d’utiliser les activités suspectes d’ATA :

[Manuel des activités suspectes d’ATA](http://aka.ms/ataplaybook) -Cet article vous guide tout au long des techniques d’attaque visant à voler des informations d’identification avec des outils de recherche disponibles sur Internet. À chaque point de l’attaque, vous pouvez voir comment ATA vous permet d’y voir plus clair dans ces menaces.

[Guide des activités suspectes d’ATA](http://aka.ms/atasaguide)



## <a name="security-best-practices"></a>Meilleures pratiques en matière de sécurité

[Bonnes pratiques d’ATA](https://aka.ms/atasecbestpractices) - Bonnes pratiques pour la sécurisation d’ATA.

[Questions fréquentes sur ATA](http://aka.ms/atafaq) - Cet article fournit des éléments d’informations et des réponses aux questions les plus fréquemment posées sur ATA.

## <a name="additional-resources"></a>Ressources supplémentaires

[Page Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Ressources de la communauté

[Blog ATA](https://aka.ms/ATABlog)
[Communauté ATA](https://aka.ms/ATACommunity)
[Donner son avis sur ATA](https://aka.ms/ATAUserVoice)
