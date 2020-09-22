---
title: Utilisation d’activités suspectes dans Advanced Threat Analytics
description: Explique comment passer en revue les activités suspectes identifiées par ATA
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 4/29/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3cd6da729d6401840532f1daf73604f699abbbde
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912135"
---
# <a name="working-with-suspicious-activities"></a>Gestion des activités suspectes

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Cet article explique les principes de base d’Advanced Threat Analytics.

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>Passer en revue les activités suspectes sur la chronologie des attaques
Une fois connecté à la console ATA, la **Chronologie des activités suspectes** s’ouvre automatiquement. Les activités suspectes sont répertoriées par ordre chronologique, avec les plus récentes en haut de la liste.
Chaque activité suspecte comporte les informations suivantes :

- Les entités impliquées, y compris les utilisateurs, les ordinateurs, les serveurs, les contrôleurs de domaine et les ressources

- Les date et heure et la durée des activités suspectes

- Gravité de l’activité suspecte (haute, moyenne ou faible)

- État : Ouvert, fermé ou supprimé.

- La capacité à :

    - Partager l’activité suspecte avec d’autres personnes de votre entreprise par e-mail.

    - Exporter l’activité suspecte dans Excel.

> [!NOTE]
> - Quand vous pointez votre souris sur un utilisateur ou un ordinateur, un mini-profil d’entité s’affiche avec des informations complémentaires sur l’entité, notamment le nombre d’activités suspectes auxquelles est liée l’entité.
> - Quand vous cliquez sur une entité, vous êtes dirigé vers le profil d’entité de l’utilisateur ou l’ordinateur.

![Image de la chronologie des activités suspectes ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## <a name="filter-suspicious-activities-list"></a>Filtrer la liste des activités suspectes
Pour filtrer la liste des activités suspectes :

1. Dans le volet **Filtrer par** sur le côté gauche de l’écran, sélectionnez l’une des options suivantes : **Tout**, **Ouvert**, **Fermé** ou **Ignoré**.

1. Pour filtrer la liste, sélectionnez **haute**, **moyenne**ou **faible**.

**Gravité des activités suspectes**

-   **Low**

    Correspond aux activités suspectes pouvant conduire à des attaques durant lesquelles des utilisateurs ou logiciels malveillants accèdent aux données d’une entreprise.

-   **Moyenne**

    Correspond aux activités suspectes qui peuvent faire courir un risque à certaines identités en permettant des attaques plus graves qui pourraient entraîner une usurpation d’identité ou une élévation des privilèges.

-   **Importante**

    Correspond aux activités suspectes pouvant conduire à une usurpation d’identité, une élévation des privilèges ou d’autres attaques à impact élevé


## <a name="remediating-suspicious-activities"></a>Résolution des activités suspectes
Vous pouvez modifier l’état d’une activité suspecte en cliquant sur l’état actuel de l’activité suspecte, puis en sélectionnant l’une des options suivantes : **ouvrir**, **supprimer**, **Fermer**ou **supprimer**.
Pour cela, cliquez sur les trois points en haut à droite d’une activité suspecte spécifique pour afficher la liste des actions disponibles.

![Actions ATA pour les activités suspectes](media/sa-actions.png)

**État des activités suspectes**

- **Ouvert** : Toutes les nouvelles activités suspectes apparaissent dans cette liste.

- **Fermé** : Utilisé pour effectuer le suivi des activités suspectes que vous avez identifiées, examinées et résolues.

  > [!NOTE]
  > Si celle-ci est détectée à nouveau peu de temps après, ATA peut rouvrir une activité fermée.

- **Ignoré** : La suppression d’une activité signifie que vous voulez l’ignorer pour le moment, et être averti de nouveau seulement en cas de nouvelle instance. Cela signifie que si une alerte similaire survient, ATA ne la rouvre pas. Cependant, si l’alerte cesse pendant sept jours puis réapparaît, vous êtes averti à nouveau.

- **Supprimer** : Si vous supprimez une alerte, elle est supprimée du système et de la base de données, et vous NE pourrez PAS la restaurer. Si vous cliquez sur Supprimer, vous pouvez supprimer toutes les activités suspectes du même type.

- **Exclure** : Possibilité d’empêcher une entité de déclencher un certain type d’alertes. Par exemple, vous pouvez configurer ATA pour empêcher une entité spécifique (un utilisateur ou un ordinateur) d’alerter à nouveau pour un certain type d’activité suspecte, par exemple un administrateur spécifique qui exécute du code à distance ou un scanner de sécurité qui effectue une reconnaissance DNS. Outre ajouter des exclusions directement sur l’activité suspecte lors de sa détection dans la chronologie, vous pouvez également accéder aux **Exclusions** de la page Configuration et, pour chaque activité suspecte, vous pouvez ajouter et supprimer manuellement des entités ou des sous-réseaux exclus (par exemple pour pass-the-ticket). 
  > [!NOTE]
  > Les pages de configuration peuvent être modifiées seulement par des administrateurs d’ATA.


## <a name="related-videos"></a>Vidéos connexes
- [Rejoindre la communauté sur la sécurité](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Voir aussi
- [Scénario d’activité suspecte ATA](https://aka.ms/ataplaybook)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Modification de la configuration d’ATA](modifying-ata-center-configuration.md)
