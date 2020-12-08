---
title: Tutoriel sur l’investigation des utilisateurs Microsoft Defender pour Identity
description: Cet article explique comment utiliser les alertes de sécurité Microsoft Defender pour Identity afin d’examiner un utilisateur suspect.
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: c9d3cb67ff4eeae0e1f4a0808751d96c67cf326e
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96542819"
---
# <a name="tutorial-investigate-a-user"></a>Tutoriel : Procéder à une investigation sur un utilisateur

> [!NOTE]
> Les fonctionnalités [!INCLUDE [Product long](includes/product-long.md)] décrites sur cette page sont également accessibles sur le nouveau [portail](https://portal.cloudappsecurity.com).

Les preuves d’alertes et les chemins de mouvement latéral [!INCLUDE [Product long](includes/product-long.md)] fournissent des indications claires quand des utilisateurs ont effectué des activités suspectes ou quand il existe des indications suggérant que leur compte a été compromis. Dans ce tutoriel, vous allez utiliser les suggestions d’investigation afin de déterminer les risques pour votre organisation, choisir le mode de remédiation et déterminer la meilleure façon de prévenir les futures attaques similaires.

> [!div class="checklist"]
>
> - Rassemblez des informations sur l’utilisateur.
> - Examinez les activités effectuées par l’utilisateur.
> - Examinez les ressources auxquelles l’utilisateur a accédé.
> - Examinez les chemins de mouvement latéral.

## <a name="recommended-investigation-steps-for-suspicious-users"></a>Étapes d’investigation recommandées pour les utilisateurs suspects

Examinez les informations et les activités suivantes dans le profil utilisateur :

1. Qui est l’[utilisateur](entity-profiles.md) ?
    1. L’utilisateur est-il un [utilisateur sensible](sensitive-accounts.md) (par exemple, est-il administrateur ou figure-t-il sur une liste à surveiller) ?
    1. Quel est son rôle au sein de l’organisation ?
    1. A-t-il une fonction importante dans l’organigramme de l’organisation ?

1. Activités suspectes à [examiner](investigate-entity.md) :
    1. L’utilisateur a-t-il d’autres alertes ouvertes dans [!INCLUDE [Product short](includes/product-short.md)], ou dans d’autres outils de sécurité tels que Microsoft Defender pour point de terminaison, Azure Security Center et/ou Microsoft CAS ?
    1. L’utilisateur a-t-il connu des échecs d’ouverture de session ?
    1. À quelles ressources l’utilisateur a-t-il accédé ?
    1. L’utilisateur a-t-il accédé à des ressources très importantes ?
    1. L’utilisateur était-il censé accéder aux ressources auxquelles il a accédé ?
    1. Sur quels ordinateurs l’utilisateur s’est-il connecté ?
    1. L’utilisateur était-il censé se connecter à ces ordinateurs ?
    1. Existe-t-il un [chemin de mouvement latéral](use-case-lateral-movement-path.md) entre l’utilisateur et un utilisateur sensible ?

## <a name="see-also"></a>Voir aussi

- [Examiner un ordinateur](investigate-a-computer.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Utilisation des chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Alertes de reconnaissance](reconnaissance-alerts.md)
- [Alertes indiquant des informations d’identification compromises](compromised-credentials-alerts.md)
- [Alertes de mouvement latéral](lateral-movement-alerts.md)
- [Alertes de dominance du domaine](domain-dominance-alerts.md)
- [Alertes d’exfiltration](exfiltration-alerts.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
