---
title: Tutoriel sur l’investigation des utilisateurs Azure ATP | Microsoft Docs
d|Description: This article explains how to user Azure ATP security alerts to investigate a suspicious user.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/14/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 126653dd2831e0e3dbd9c777d84d32b1c2e74bd9
ms.sourcegitcommit: 1ee052c4c6b04b290e2d5384c24b65a108b1f1f3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54253399"
---
# <a name="tutorial-investigate-a-user"></a>Tutoriel : Procéder à une investigation sur un utilisateur

Les preuves d’alertes et les chemins de mouvement latéral ATP Azure fournissent des indications claires quand des utilisateurs ont effectué des activités suspectes ou quand il existe des indications suggérant que leur compte a été compromis. Utilisez les suggestions d’investigation afin d’aider à déterminer les risques pour votre organisation, à choisir le mode de remédiation et à déterminer la meilleure façon de prévenir toute attaque ultérieure similaire.  

## <a name="recommended-investigation-steps-for-suspicious-users"></a>Étapes d’investigation recommandées pour les utilisateurs suspects

Examinez les informations et les activités suivantes dans le profil utilisateur :

1. Qui est l’[utilisateur](entity-profiles.md) ?
     1. L’utilisateur est-il un [utilisateur sensible](sensitive-accounts.md) (par exemple, est-il administrateur ou figure-t-il sur une liste à surveiller) ?  
     2. Quel est son rôle au sein de l’organisation ?
     3. A-t-il une fonction importante dans l’organigramme de l’organisation ?

2. Activités suspectes à [examiner](investigate-entity.md) :
     1. L’utilisateur a-t-il d’autres alertes ouvertes dans Azure ATP, ou dans d’autres outils de sécurité tels que Windows Defender-ATP, Azure Security Center et/ou Microsoft CAS ?
     2. L’utilisateur a-t-il connu des échecs d’ouverture de session ?
     3. À quelles ressources l’utilisateur a-t-il accédé ?  
     4. L’utilisateur a-t-il accédé à des ressources très importantes ?  
     5. L’utilisateur était-il censé accéder aux ressources auxquelles il a accédé ?  
     6. Sur quels ordinateurs l’utilisateur s’est-il connecté ? 
     7. L’utilisateur était-il censé se connecter à ces ordinateurs ?
     8. Existe-t-il un [chemin de mouvement latéral](use-case-lateral-movement-path.md) entre l’utilisateur et un utilisateur sensible ?


## <a name="see-also"></a>Voir aussi

- [Examiner un ordinateur](investigate-a-computer.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Utilisation des chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Alertes de reconnaissance](atp-reconnaissance-alerts.md)
- [Alertes indiquant des informations d’identification compromises](atp-compromised-credentials-alerts.md)
- [Alertes de mouvement latéral](atp-lateral-movement-alerts.md)
- [Alertes de dominance du domaine](atp-domain-dominance-alerts.md)
- [Alertes d’exfiltration](atp-exfiltration-alerts.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
