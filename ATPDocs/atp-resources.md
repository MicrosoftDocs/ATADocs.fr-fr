---
title: Liste de ressources utiles pour Azure - Protection avancée contre les menaces | Microsoft Docs
description: Cet article fournit une liste de ressources utiles pour Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/15/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 56b74b2e02fcab2b7584afbabd5d4384f066261c
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166376"
---
*S’applique à : Azure Advanced Threat Protection*



# <a name="azure-atp-readiness-guide"></a>Guide de préparation à Azure ATP

Cet article vous fournit un guide de préparation qui vous donne une liste de ressources pour vous aider avec la prise en main d’Azure - Protection avancée contre les menaces. 

## <a name="understanding-azure-atp"></a>Présentation d’Azure ATP

Azure - Protection avancée contre les menaces (ATP) est un service cloud qui vous aide à identifier et protéger votre entreprise contre de nombreux types de cyberattaques ciblées avancées et contre les menaces internes. Utilisez les ressources suivantes pour en savoir plus sur Azure ATP : 
- [Vue d’ensemble d’Azure ATP](what-is-atp.md)
- [Vidéo d’introduction à Azure ATP - version longue](https://www.youtube.com/watch?v=KX-xpFc0sBw) 

## <a name="deployment-decisions"></a>Décisions de déploiement

Azure ATP se compose d’un service cloud résidant dans Azure et de capteurs intégrés qui peuvent être installés sur un contrôleur de domaine ou des capteurs autonomes sur des serveurs dédiés. Avant de commencer à utiliser Azure ATP, il est important de choisir le type de capteurs qui conviennent le mieux à votre déploiement et vos besoins. Les capteurs intégrés Azure ATP permettent d’obtenir une sécurité renforcée, des coûts opérationnels réduits et un déploiement plus facile. Les capteurs autonomes Azure ATP nécessitent un matériel physique, des étapes de configuration supplémentaires et des coûts opérationnels plus lourds. <br>Si vous utilisez des serveurs physiques, il est essentiel de planifier la capacité. Vous pouvez vous aider de l’outil de dimensionnement pour allouer de l’espace à vos capteurs : 
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool) - L’outil de dimensionnement automatise la collecte de la somme de trafic surveillé par Azure ATP. Il fournit automatiquement des recommandations de prise en charge et de ressource pour les capteurs. 
- [Guide de planification de la capacité d’ATA](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Déployer Azure ATP

Ces ressources vous permettent de configurer Azure ATP, de vous connecter à Active Directory, de télécharger le package de capteurs, de configurer la collecte d’événements et éventuellement de procéder à l’intégration avec votre VPN, puis de configurer les exclusions et les comptes honeytoken. 
- [Essayez Azure ATP (compris dans EMS E5)](http://aka.ms/aatptrial)  L’essai est valide pendant 90 jours.
- [Guide de déploiement](install-atp-step1.md)  Déployez Azure ATP dans votre environnement en suivant ces étapes.
- [Intégrer Azure ATP et Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Paramètres Azure ATP

Les paramètres de base nécessaires dans Azure ATP sont configurés lors de la création de l’espace de travail. Toutefois, vous pouvez configurer d’autres paramètres pour ajuster Azure ATP de sorte à obtenir des détections plus précises pour votre environnement, telles que l’intégration SIEM et les paramètres d’audit. 

- [Documentation générale d’Azure ATP](what-is-atp.md)
- [Paramètres d’audit](https://blogs.technet.microsoft.com/positivesecurity/2017/08/18/ata-auditing-auditpol-advanced-audit-settings-enforcement-lightweight-gateway-service-discovery/) – Auditez l’intégrité de votre contrôleur de domaine avant et après un déploiement d’ATP. 

## <a name="work-with-azure-atp"></a>Utiliser Azure ATP

Une fois Azure ATP opérationnel, vous pouvez voir les activités suspectes détectées dans la chronologie des activités du portail Azure ATP. La chronologie des activités est la page d’accueil par défaut une fois que vous êtes connecté au portail Azure ATP. Par défaut, toutes les activités suspectes ouvertes sont affichées dans la chronologie des attaques. Vous pouvez également voir le niveau de gravité attribué à chaque activité. Investiguez sur chaque activité suspecte en explorant les entités (ordinateurs, appareils, utilisateurs) pour ouvrir leurs pages de profil qui contiennent des informations supplémentaires. Ces ressources vous permettent d’utiliser les activités suspectes d’Azure ATP : 

- [Guide des activités suspectes Azure ATP](suspicious-activity-guide.md) Apprenez à trier et passez aux étapes suivantes avec vos détections Azure ATP.
- [Identifier des groupes comme sensibles](sensitive-accounts.md) Gagnez en visibilité dans l’exposition des informations d’identification sur les groupes de sécurité sensibles.

## <a name="security-best-practices"></a>Meilleures pratiques en matière de sécurité

- [Questions fréquentes sur Azure ATP](atp-technical-faq.md) - Cet article fournit des éléments d’informations et des réponses aux questions les plus fréquemment posées sur Azure ATP. 

## <a name="community-resources"></a>Ressources de la communauté

Blog : [Blog sur Azure ATP](https://aka.ms/aatpblog)

Communauté publique : [Communauté technique d’Azure ATP](https://aka.ms/AatpCom)

Communauté privée : [Groupe Yammer sur Azure ATP](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Channel 9 : [Page Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)



## <a name="see-also"></a>Voir aussi

- [Utilisation de comptes sensibles](sensitive-accounts.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)