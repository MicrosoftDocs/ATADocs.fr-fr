---
title: Liste de ressources utiles pour Azure Advanced Threat Protection | Microsoft Docs
description: Cet article fournit une liste de ressources utiles pour Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 029077455f9b2800984065a10c3e221e62d7c606
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783149"
---
*S’applique à : Azure Advanced Threat Protection*



# <a name="azure-atp-readiness-guide"></a>Guide de préparation à Azure ATP

Cet article vous fournit un guide de préparation qui vous donne une liste de ressources pour vous aider à commencer à utiliser Azure Advanced Threat Protection. 

## <a name="understanding-azure-atp"></a>Présentation d’Azure ATP

Azure Advanced Threat Protection (ATP) est un service cloud qui vous aide à identifier et protéger votre entreprise contre de nombreux types de cyberattaques ciblées avancées et contre les menaces internes. Pour en savoir plus sur Azure ATP : 
- [Vue d’ensemble d’Azure ATP](what-is-atp.md)
- [Vidéo : Introduction à Azure ATP (25 minutes) - Version longue](https://www.youtube.com/watch?v=EGY2m8yU_KE)
- [Vidéo : Présentation approfondie d’Azure ATP (75 minutes) - Version longue](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

## <a name="deployment-decisions"></a>Décisions de déploiement

Azure ATP se compose d’un service cloud résidant dans Azure et de capteurs intégrés qui peuvent être installés sur un contrôleur de domaine ou des capteurs autonomes sur des serveurs dédiés. Avant de commencer à utiliser Azure ATP, il est important de choisir le type de capteurs qui conviennent le mieux à votre déploiement et vos besoins. Par rapport aux capteurs Azure ATP autonomes, les capteurs intégrés Azure ATP (les capteurs Azure ATP) permettent d’obtenir une sécurité renforcée, des coûts opérationnels réduits et un déploiement plus facile. Les capteurs autonomes Azure ATP nécessitent un matériel physique, des étapes de configuration supplémentaires et des coûts opérationnels plus lourds. <br>Si vous utilisez des serveurs physiques, il est essentiel de planifier la capacité. Vous pouvez vous aider de l’outil de dimensionnement pour allouer de l’espace à vos capteurs : 
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool) - L’outil de dimensionnement automatise la collecte de la somme de trafic surveillé par Azure ATP. Il fournit automatiquement des recommandations de prise en charge et de ressource pour les capteurs. 
- [Guide de planification de la capacité ATP](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Déployer Azure ATP

Ces ressources vous permettent de configurer Azure ATP, de vous connecter à Active Directory, de télécharger le package de capteurs, de configurer la collecte d’événements et éventuellement de procéder à l’intégration avec votre VPN, puis de configurer les exclusions et les comptes honeytoken. 
- [Essayez Azure ATP (compris dans EMS E5)](http://aka.ms/aatptrial)  L’essai est valide pendant 90 jours.
- [Installation d’Azure ATP](install-atp-step1.md) : déployez Azure ATP dans votre environnement en suivant ces étapes.
- [Intégrer Azure ATP et Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Paramètres Azure ATP

Les paramètres de base nécessaires dans Azure ATP sont configurés lors de la création de l’espace de travail. Toutefois, vous pouvez configurer d’autres paramètres dans Azure ATP de sorte à obtenir des détections plus précises pour votre environnement, telles que l’intégration VPN, les autorisations SAM et les paramètres avancés de stratégie d’audit. 

- [Intégration VPN](install-atp-step6-vpn.md)
- [Autorisations SAM-R](install-atp-step8-samr.md)
- [Paramètres de stratégie d’audit](atp-advanced-audit-policy.md) : auditez l’intégrité de votre contrôleur de domaine avant et après un déploiement ATP. 

## <a name="work-with-azure-atp"></a>Utiliser Azure ATP

Lorsqu’Azure ATP est opérationnel, vous pouvez voir les alertes de sécurité dans la chronologie des activités du portail Azure ATP. La chronologie des activités est la page d’accueil par défaut une fois que vous êtes connecté au portail Azure ATP. Par défaut, toutes les alertes de sécurité ouvertes sont affichées dans la chronologie des attaques. Vous pouvez également voir le niveau de gravité attribué à chaque alerte. Examinez chaque alerte en explorant les entités (ordinateurs, appareils, utilisateurs) et en ouvrant leurs pages de profil qui contiennent des informations supplémentaires. Les ressources qui suivent expliquent comment utiliser les alertes de sécurité Azure ATP : 

- [Guide relatif aux alertes de sécurité Azure ATP](suspicious-activity-guide.md) Apprenez à trier les alertes pour des détections Azure ATP plus efficaces.
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
- [Consulter le forum Azure ATP](https://aka.ms/azureatpcommunity)