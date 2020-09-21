---
title: Liste des ressources utiles pour Azure-protection avancée contre les menaces
description: Cet article fournit une liste de ressources utiles pour Azure ATP
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 20341bb46ed5c7b1deaf3d7dd79e2934007fda2d
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828408"
---
# <a name="azure-atp-readiness-guide"></a>Guide de préparation à Azure ATP

Cet article liste des ressources utiles qui vous aideront à vous préparer et à bien démarrer avec Azure Advanced Threat Protection.

## <a name="understanding-azure-atp"></a>Présentation d’Azure ATP

Azure Advanced Threat Protection (ATP) est un service cloud qui vous aide à identifier et protéger votre entreprise contre de nombreux types de cyberattaques ciblées avancées et contre les menaces internes.

Pour en savoir plus sur Azure ATP :

- [Vue d’ensemble d’Azure ATP](what-is.md)
- [Vidéo : Introduction à Azure ATP (25 minutes) - Version longue](https://www.youtube.com/watch?v=EGY2m8yU_KE)
- [Vidéo : Présentation approfondie d’Azure ATP (75 minutes) - Version longue](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

## <a name="deployment-decisions"></a>Décisions de déploiement

Azure ATP est constitué d’un service Cloud résidant dans Azure et de capteurs intégrés qui peuvent être installés sur les contrôleurs de domaine. Si vous utilisez des serveurs physiques, il est essentiel de planifier la capacité. Aidez-vous de l’outil de dimensionnement pour allouer de l’espace à vos capteurs :

- [Outil de dimensionnement Azure ATP](https://aka.ms/aatpsizingtool) - L’outil de dimensionnement automatise la collecte de la somme de trafic surveillé par Azure ATP. Il fournit automatiquement des recommandations de prise en charge et de ressource pour les capteurs.
- [Guide de planification de la capacité ATP](capacity-planning.md)

## <a name="deploy-azure-atp"></a>Déployer Azure ATP

Aidez-vous de ces ressources pour configurer Azure ATP, vous connecter à Active Directory, télécharger le package de capteurs, configurer la collecte d’événements, et éventuellement intégrer votre VPN, ainsi que configurer les exclusions et les comptes honeytoken.

- [Essayez Azure ATP (compris dans EMS E5)](https://aka.ms/aatptrial)  L’essai est valide pendant 90 jours.
- [Installation d’Azure ATP](install-step1.md) Suivez ces étapes pour déployer Azure ATP dans votre environnement.
- [Intégrer Azure ATP avec Microsoft Defender ATP](integrate-msde.md)

## <a name="azure-atp-settings"></a>Paramètres Azure ATP

Quand vous créez votre instance Azure ATP, les paramètres de base nécessaires sont configurés automatiquement. Vous pouvez configurer plusieurs autres paramètres dans Azure ATP pour améliorer la précision de détection et d’alerte pour votre environnement, comme l’intégration VPN, les autorisations SAM et les paramètres avancés de stratégie d’audit.

- [Intégration VPN](install-step6-vpn.md)
- [Autorisations SAM-R](install-step8-samr.md)
- [Paramètres de stratégie d’audit](configure-windows-event-collection.md) : auditez l’intégrité de votre contrôleur de domaine avant et après un déploiement ATP.

## <a name="work-with-azure-atp"></a>Utiliser Azure ATP

Dès lors qu’Azure ATP est opérationnel, vous pouvez examiner les alertes de sécurité dans la chronologie des activités du portail Azure ATP. La chronologie des activités est la page d’accueil par défaut qui s’affiche après vous être connecté au portail Azure ATP. Par défaut, toutes les alertes de sécurité ouvertes sont affichées dans la chronologie des activités. Vous pouvez également voir le niveau de gravité attribué à chaque alerte. Examinez chaque alerte en explorant les entités (ordinateurs, appareils, utilisateurs) et en ouvrant leurs pages de profil qui contiennent des informations supplémentaires. Les chemins de mouvement latéral montrent les possibles mouvements dans votre réseau ainsi que les utilisateurs sensibles à risque. Évaluez l’exposition et prenez des mesures correctives en vous aidant des graphiques de détection des chemins de mouvement latéral. Les ressources qui suivent expliquent comment utiliser les alertes de sécurité Azure ATP :

- [Guide relatif aux alertes de sécurité Azure ATP](suspicious-activity-guide.md) Apprenez à trier les alertes pour des détections Azure ATP plus efficaces.
- [Azure ATP les chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Identifier des groupes comme sensibles](sensitive-accounts.md) Gagnez en visibilité dans l’exposition des informations d’identification sur les groupes de sécurité sensibles.

## <a name="security-best-practices"></a>Bonnes pratiques de sécurité

- [Questions fréquentes sur Azure ATP](technical-faq.md) - Cet article fournit des éléments d’informations et des réponses aux questions les plus fréquemment posées sur Azure ATP.

## <a name="community-resources"></a>Ressources de la communauté

Blog : [Blog sur Azure ATP](https://aka.ms/aatpblog)

Communauté publique : [Communauté technique d’Azure ATP](https://aka.ms/AatpCom)

Communauté privée : [Groupe Yammer sur Azure ATP](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all&preserve-view=true)

Channel 9 : [Page Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="see-also"></a>Voir aussi

- [Utilisation de comptes sensibles](sensitive-accounts.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)