---
title: Tutoriel sur l’investigation des ordinateurs Microsoft Defender pour Identity
description: Cet article explique comment utiliser les alertes de sécurité Microsoft Defender pour Identity afin d’investiguer un ordinateur suspect.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 72a7f92d6fd77842b8fe34866d8757df8bc9203e
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847681"
---
# <a name="tutorial-investigate-a-computer"></a>Tutoriel : Procéder à une investigation sur un ordinateur

> [!NOTE]
> Les fonctionnalités [!INCLUDE [Product long](includes/product-long.md)] décrites sur cette page sont également accessibles sur le nouveau [portail](https://portal.cloudappsecurity.com).

Les preuves d’alertes [!INCLUDE [Product long](includes/product-long.md)] fournissent des indications claires quand des ordinateurs ont été impliqués dans des activités suspectes ou quand il existe des indications suggérant qu’un ordinateur est compromis. Dans ce tutoriel, vous allez utiliser les suggestions d’investigation afin de déterminer les risques pour votre organisation, choisir le mode de remédiation et déterminer la meilleure façon de prévenir les futures attaques similaires.  

> [!div class="checklist"]
>
> - Vérifiez l’ordinateur pour l’utilisateur connecté.
> - Vérifiez si l’utilisateur accède à normalement aux ordinateurs.
> - Examinez les activités suspectes provenant de l’ordinateur.
> - Y a-t-il eu d’autres alertes au même moment ?

## <a name="investigation-steps-for-suspicious-computers"></a>Étapes d’investigation pour les ordinateurs suspects

Pour accéder à la page de profil d’ordinateur, cliquez sur l’ordinateur mentionné dans l’alerte que vous souhaitez examiner. Pour vous aider dans votre investigation, la preuve d’alerte liste tous les ordinateurs (et [utilisateurs](investigate-a-user.md)) associés à chaque activité suspecte.

Examinez les informations et les activités suivantes dans le profil d’ordinateur :

- Que s’est-il passé au moment de l’activité suspecte ?  
    1. Qui était l’[utilisateur](investigate-a-user.md) connecté à l’ordinateur ?
    1. Cet utilisateur a-t-il l’habitude de se connecter ou d’accéder à l’ordinateur source ou de destination ?
    1. Quelles sont les ressources qui ont été sollicitées ? Par quels utilisateurs ?
      - S’agissait-il de ressources très importantes ?
    1. L’utilisateur était-il supposé accéder à ces ressources ?
    1. L’[utilisateur](investigate-a-user.md) qui a accédé à l’ordinateur a-t-il effectué d’autres activités suspectes ?

- Activités suspectes supplémentaires à examiner :
    1. D’autres alertes ont-elles été ouvertes au même moment que celle-ci dans [!INCLUDE [Product short](includes/product-short.md)], ou dans d’autres outils de sécurité tels que Microsoft Defender pour point de terminaison, Azure Security Center et/ou Microsoft CAS ?
    1. Y a-t-il eu des échecs d’ouverture de session ?

- Si l’intégration Microsoft Defender pour point de terminaison est activée, cliquez sur le badge Microsoft Defender pour point de terminaison afin d’investiguer l’ordinateur plus en détail. Dans Microsoft Defender pour point de terminaison, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte.
    - De nouveaux programmes ont-ils été déployés ou installés ?

## <a name="next-steps"></a>Étapes suivantes

- [Examiner un utilisateur](investigate-a-user.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Utilisation des chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Alertes de reconnaissance](reconnaissance-alerts.md)
- [Alertes indiquant des informations d’identification compromises](compromised-credentials-alerts.md)
- [Alertes de mouvement latéral](lateral-movement-alerts.md)
- [Alertes de dominance du domaine](domain-dominance-alerts.md)
- [Alertes d’exfiltration](exfiltration-alerts.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
