---
title: Surveiller Microsoft Defender pour l’intégrité et les événements du système d’identité
description: Utilisez le centre d’intégrité pour vérifier le fonctionnement de Microsoft Defender for Identity service et recevoir des alertes en cas de problèmes potentiels et afficher les événements système dans l’observateur d’événements.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: ac03020c559a860fded89a496bc927da06fce3d9
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534291"
---
# <a name="work-with-microsoft-defender-for-identity-health-and-events"></a>Utiliser Microsoft Defender pour l’intégrité et les événements de l’identité

## <a name="microsoft-defender-for-identity-health-center"></a>Microsoft Defender pour Identity Health Center

Le [!INCLUDE [Product long](includes/product-long.md)] Centre d’intégrité vous permet de savoir comment votre [!INCLUDE [Product short](includes/product-short.md)] instance s’exécute et vous avertit en cas de problème.

## <a name="working-with-the-defender-for-identity-health-center"></a>Utilisation de Defender pour Identity Health Center

Le [!INCLUDE [Product short](includes/product-short.md)] Centre d’intégrité vous permet de savoir qu’il y a un problème en déclenchant une alerte (un point rouge) au-dessus de l’icône du centre d’intégrité dans la barre de navigation.

![[! INCLUDe [Product Short] (includes/Product-Short. MD)] barre d’outils du point rouge du centre d’intégrité](media/health-bar.png)

### <a name="managing-defender-for-identity-health"></a>Gestion de Defender pour l’intégrité de l’identité

Pour vérifier l’intégrité globale de votre [!INCLUDE [Product short](includes/product-short.md)] instance, sélectionnez **intégrité** ![ [ ! INCLUDe [Product Short] (includes/Product-Short. MD)] icône du centre d’intégrité](media/red-dot.png)

- Il est possible de gérer tous les problèmes ouverts en leur appliquant l’opération **Fermer** ou **Supprimer**, en cliquant sur les trois points dans l’angle de l’alerte et en sélectionnant l’option correspondante.

- **Ouvert** : Toutes les nouvelles activités suspectes apparaissent dans cette liste.

- **Fermé** : Utilisé pour effectuer le suivi des activités suspectes que vous avez identifiées, examinées et résolues.

    > [!NOTE]
    > [!INCLUDE [Product short](includes/product-short.md)] peut rouvrir une activité fermée si la même activité est détectée à nouveau dans un laps de temps réduit.

- **Ignoré** : La suppression d’une activité signifie que vous voulez l’ignorer pour le moment, et être averti de nouveau seulement en cas de nouvelle instance. Si une alerte similaire ne s' [!INCLUDE [Product short](includes/product-short.md)] ouvre pas à nouveau, Cependant, si l’alerte cesse pendant sept jours puis réapparaît, vous êtes de nouveau averti.

- **Rouvrir** : vous pouvez rouvrir une alerte fermée ou supprimée de sorte qu’elle figure à nouveau à l’état **Ouvert** dans la chronologie.

- **Supprimer** : dans la chronologie des alertes de sécurité, vous avez aussi la possibilité de supprimer un problème d’intégrité. Si vous supprimez une alerte, celle-ci est supprimée de l’instance et vous NE pouvez PAS la restaurer. Si vous cliquez sur Supprimer, vous supprimez toutes les alertes de sécurité du même type.

![[! INCLUDe [Product Short] (includes/Product-Short. MD)] image des problèmes du centre d’intégrité](media/health-issue.png)

## <a name="see-also"></a>Voir aussi

- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
