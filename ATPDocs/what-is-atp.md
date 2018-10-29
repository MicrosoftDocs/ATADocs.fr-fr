---
title: Présentation d’Azure Advanced Threat Protection (Azure ATP) | Microsoft Docs
description: Explique ce qu’est Azure Advanced Threat Protection (Azure ATP) et quels types d’activités suspectes il peut détecter
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 80038b04a95d09c25baf1e2b5d216796cb12c9f6
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783677"
---
*S’applique à : Azure Advanced Threat Protection*

# <a name="what-is-azure-advanced-threat-protection"></a>Qu’est-ce qu’Azure Advanced Threat Protection ?
Azure Advanced Threat Protection (ATP) est une solution de sécurité cloud qui identifie, détecte et vous aide à examiner les menaces avancées, les identités compromises et les actions des utilisateurs internes malveillants dirigées contre votre entreprise. Azure ATP permet aux analystes SecOp et aux professionnels de la sécurité chargés de détecter les attaques avancées dans les environnements hybrides de :  
- Surveiller les utilisateurs, et le comportement et les activités des entités avec une analytique basée sur l’apprentissage  
- Protéger les identités et les informations d’identification des utilisateurs qui sont stockées dans Active Directory  
- Identifier et examiner les activités suspectes des utilisateurs et les attaques avancées tout au long de la chaîne d’annihilation 
- Fournir des informations claires sur les incidents selon une chronologie simple, permettant un triage rapide 
 
## <a name="monitor-and-profile-user-behavior-and-activities"></a>Surveiller et profiler le comportement et les activités des utilisateurs  
Azure ATP surveille et analyse les activités et les informations des utilisateurs sur votre réseau, comme les autorisations et les appartenances aux groupes, créant une base de référence du comportement pour chaque utilisateur. Azure ATP identifie ensuite les anomalies avec une intelligence intégrée adaptative, vous donnant alors des insights sur les activités et les événements suspects, révélant les menaces avancées, les utilisateurs compromis et les menaces internes dans votre organisation. Les capteurs de propriétaires d’Azure ATP surveillent les contrôleurs de domaine de l’organisation et fournissent une vue complète de toutes les activités des utilisateurs sur chaque appareil. 
 
## <a name="protect-user-identities-and-reduce-the-attack-surface"></a>Protéger les identités des utilisateurs et réduire la surface d’attaque   
Azure ATP vous fournit des insights précieux sur les configurations des identités et suggère les bonnes pratiques de sécurité. Grâce à des rapports de sécurité et une analytique des profils utilisateur, Azure ATP vous permet de réduire considérablement la surface d’attaque de l’organisation, rendant plus difficile de compromettre les informations d’identification des utilisateurs et la mise en œuvre d’une attaque. Les chemins de mouvement latéral visuels d’Azure ATP vous aident à comprendre rapidement et exactement comment un attaquant peut se déplacer latéralement au sein de votre organisation pour compromettre des comptes sensibles et vous assistent pour éviter préventivement ces risques. De plus, les rapports de sécurité d’Azure ATP vous aident à identifier les utilisateurs et les appareils qui s’authentifient avec des mots de passe en texte clair, et fournissent des insights supplémentaires pour améliorer la prise en compte et les stratégies de sécurité.  
 
## <a name="identify-suspicious-activities-and-advanced-attacks-across-the-attack-kill-chain"></a>Identifier les activités suspectes et les attaques avancées sur la chaîne d’annihilation des attaques 
En général, les attaques sont lancées contre des entités accessibles, par exemple un utilisateur avec des privilèges peu élevés, puis rapidement, elles se déplacent latéralement jusqu’à ce que l’attaquant parvienne à accéder à des ressources importantes, comme des comptes sensibles, des administrateurs de domaine et des données hautement sensibles. Azure ATP identifie ces menaces avancées à la source tout au long de la chaîne d’annihilation des attaques : 
### <a name="reconnaissance"></a>Reconnaissance 
Identifiez les utilisateurs non autorisés et les tentatives des attaquants pour obtenir des informations sur les noms d’utilisateur, l’appartenance des utilisateurs à des groupes, les adresses IP affectées à des appareils, les ressources, etc., selon différentes méthodes.  
### <a name="compromised-users"></a>Utilisateurs compromis
Identifiez les tentatives de compromission des informations d’identification des utilisateurs via des attaques par force brute, les échecs d’authentification, les changements d’appartenance à des groupes d’utilisateurs et d’autres méthodes.  

### <a name="lateral-movements"></a>Déplacements latéraux
Détectez les tentatives de mouvement latéral au sein du réseau pour obtenir plus de contrôle des utilisateurs sensibles, en utilisant des méthodes comme Pass-the-Ticket, Pass-the-Hash, Overpass-the-Hash, etc.  

### <a name="domain-dominance"></a>Contrôle du domaine
Mise en évidence du comportement des attaquants si la prise de contrôle du domaine est effective, via l’exécution de code à distance sur le contrôleur de domaine et des méthodes comme la mise en mémoire fantôme du contrôleur de domaine, la réplication du contrôleur de domaine malveillant, les activités de Golden Ticket, etc.   

## <a name="investigate-alerts-and-user-activities"></a>Examiner les alertes et les activités des utilisateurs  
Azure ATP est conçu pour réduire le bruit général des alertes, fournissant seulement des alertes de sécurité pertinentes et importantes, selon une chronologie simple et en temps réel des attaques de l’organisation. La vue de la chronologie des attaques d’Azure ATP vous permet de vous concentrer sur ce qui est important, en tirant parti de l’analytique intelligente. Les professionnels de la sécurité utilisant Azure ATP peuvent examiner rapidement les menaces et obtenir des insights sur l’organisation pour les utilisateurs, les appareils et les recours au réseau. L’intégration fluide avec Windows Defender ATP fournit une autre couche de sécurité renforcée via une détection et une protection supplémentaires contre les menaces persistantes avancées sur le système d’exploitation.  

## <a name="additional-resources-for-azure-atp"></a>Ressources supplémentaires pour Azure ATP  
Démarrez un essai gratuit : [https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1](https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1 "Enterprise Mobility + Security E5")
 
Suivez Azure ATP sur Microsoft Tech Community  
[https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection "Azure ATP sur Microsoft Tech Community")
 
Rejoignez la communauté Azure ATP Yammer [https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893 "Communauté Azure ATP Yammer")
 
Visitez la page produit d’Azure ATP.  
[https://azure.microsoft.com/en-us/features/azure-advanced-threat-protection/](https://azure.microsoft.com/en-us/features/azure-advanced-threat-protection/ "Page produit d’Azure ATP")

Pour plus d’informations sur l’architecture Azure ATP, consultez [Architecture Azure ATP](atp-architecture.md).
 
## <a name="whats-next"></a>Étapes suivantes 

Nous vous recommandons de déployer Azure ATP en 3 phases :  

### <a name="phase-1"></a>Phase 1

1. Configurez Azure ATP pour protéger vos environnements principaux. Le modèle de déploiement rapide d’Azure ATP vous permet de protéger votre organisation dès aujourd’hui. [Installer Azure ATP](install-atp-step1.md)  
2. Définissez les [comptes sensibles](sensitive-accounts.md) et les [comptes honeytoken](install-atp-step7.md).   
3. Passez en revue les rapports et [chemins de mouvement latéral](use-case-lateral-movement-path.md).  


### <a name="phase-2"></a>Phase 2

1. Protégez tous les contrôleurs de domaine et les [forêts](atp-multi-forest.md) de votre organisation.  
2.  Surveillez toutes les [alertes](working-with-suspicious-activities.md) : examinez les alertes de mouvement latéral et de prise de contrôle de domaine.  
3. Utilisez le [Guide des alertes de sécurité](suspicious-activity-guide.md) pour comprendre les menaces et trier les attaques potentielles.   


### <a name="phase-3"></a>Phase 3

1. Intégrez les alertes Azure ATP dans votre flux de travail SecOp. 

## <a name="see-also"></a>Voir aussi
- [Questions fréquentes (FAQ) sur Azure ATP](atp-technical-faq.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)