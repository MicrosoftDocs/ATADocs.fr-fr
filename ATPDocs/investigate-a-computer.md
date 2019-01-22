---
title: Tutoriel sur l’investigation des ordinateurs Azure ATP | Microsoft Docs
d|Description: This article explains how to use Azure ATP security alerts to investigate a suspicious computer.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/14/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 64424c6c2b2b0f627099ab479831f4b289eb9605
ms.sourcegitcommit: 1ee052c4c6b04b290e2d5384c24b65a108b1f1f3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54253382"
---
# <a name="tutorial-investigate-a-computer"></a>Tutoriel : Procéder à une investigation sur un ordinateur

Les preuves d’alertes Azure ATP fournissent des indications claires quand des ordinateurs ont été impliqués dans des activités suspectes ou quand il existe des indications suggérant qu’un ordinateur est compromis. Utilisez les suggestions d’investigation afin d’aider à déterminer les risques pour votre organisation, à choisir le mode de remédiation et à déterminer la meilleure façon de prévenir toute attaque similaire à l’avenir.  

## <a name="investigation-steps-for-suspicious-computers"></a>Étapes d’investigation pour les ordinateurs suspects

Pour accéder à la page de profil d’ordinateur, cliquez sur l’ordinateur mentionné dans l’alerte que vous souhaitez examiner. Pour vous aider dans votre investigation, la preuve d’alerte liste tous les ordinateurs (et [utilisateurs](investigate-a-user.md)) associés à chaque activité suspecte.

Examinez les informations et les activités suivantes dans le profil d’ordinateur :

- Que s’est-il passé au moment de l’activité suspecte ?  
    1. Qui était l’[utilisateur](investigate-a-user.md) connecté à l’ordinateur ?
    2. Cet utilisateur a-t-il l’habitude de se connecter ou d’accéder à l’ordinateur source ou de destination ?
    3. Quelles sont les ressources qui ont été sollicitées ? Par quels utilisateurs ?
            - Si des ressources ont été sollicitées, s’agissait-il de ressources très importantes ?
    4. L’utilisateur était-il supposé accéder à ces ressources ?
    5. L’[utilisateur](investigate-a-user.md) qui a accédé à l’ordinateur a-t-il effectué d’autres activités suspectes ?


- Activités suspectes supplémentaires à examiner :
    1. D’autres alertes ont-elles été ouvertes au même moment que celle-ci dans Azure ATP, ou dans d’autres outils de sécurité tels que Windows Defender ATP, Azure Security Center et/ou Microsoft CAS ?
    2. Y a-t-il eu des échecs d’ouverture de session ?


- Si l’intégration Windows Defender ATP est activée, cliquez sur le badge Windows Defender ATP pour explorer l’ordinateur plus en détail. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte.
    1. De nouveaux programmes ont-ils été déployés ou installés ?

## <a name="see-also"></a>Voir aussi

- [Examiner un utilisateur](investigate-a-user.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Utilisation des chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Alertes de reconnaissance](atp-reconnaissance-alerts.md)
- [Alertes indiquant des informations d’identification compromises](atp-compromised-credentials-alerts.md)
- [Alertes de mouvement latéral](atp-lateral-movement-alerts.md)
- [Alertes de dominance du domaine](atp-domain-dominance-alerts.md)
- [Alertes d’exfiltration](atp-exfiltration-alerts.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
