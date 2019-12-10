---
title: Tutoriel sur l’investigation des utilisateurs Azure ATP | Microsoft Docs
d|Description: This article explains how to user Azure ATP security alerts to investigate a suspicious user.
keywords: ''
author: mlottner
ms.author: mlottner
ms.date: 09/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fdf0c4cc32137b23f7c2170a2c8dd0132b3b6462
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71004761"
---
# <a name="tutorial-investigate-a-user"></a>Tutoriel : Procéder à une investigation sur un utilisateur

> [!NOTE]
> Les fonctionnalités Azure ATP expliquées dans cette page sont également accessibles dans le nouveau [portail](https://portal.cloudappsecurity.com).

Les preuves d’alertes et les chemins de mouvement latéral ATP Azure fournissent des indications claires quand des utilisateurs ont effectué des activités suspectes ou quand il existe des indications suggérant que leur compte a été compromis. Dans ce tutoriel, vous allez utiliser les suggestions d’investigation afin de déterminer les risques pour votre organisation, choisir le mode de remédiation et déterminer la meilleure façon de prévenir les futures attaques similaires.  

> [!div class="checklist"]
> * Rassemblez des informations sur l’utilisateur.
> * Examinez les activités effectuées par l’utilisateur.
> * Examinez les ressources auxquelles l’utilisateur a accédé.
> * Examinez les chemins de mouvement latéral.

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
