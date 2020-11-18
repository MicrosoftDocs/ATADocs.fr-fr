---
title: Surveiller Microsoft Defender pour l’intégrité et les événements du système d’identité
description: Utilisez le centre d’intégrité pour vérifier le fonctionnement de Microsoft Defender for Identity service et recevoir des alertes en cas de problèmes potentiels et afficher les événements système dans l’observateur d’événements.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5bf828278e0223aaaf52b41932b2612c7225dd7f
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847936"
---
# <a name="work-with-product-long-health-and-events"></a>Utiliser l' [!INCLUDE [Product long](includes/product-long.md)] intégrité et les événements

## <a name="product-long-health-center"></a>[!INCLUDE [Product long](includes/product-long.md)] Centre d’intégrité

Le [!INCLUDE [Product long](includes/product-long.md)] Centre d’intégrité vous permet de savoir comment votre [!INCLUDE [Product short](includes/product-short.md)] instance s’exécute et vous avertit en cas de problème.

## <a name="working-with-the-product-short-health-center"></a>Utilisation du [!INCLUDE [Product short](includes/product-short.md)] Centre d’intégrité

Le [!INCLUDE [Product short](includes/product-short.md)] Centre d’intégrité vous permet de savoir qu’il y a un problème en déclenchant une alerte (un point rouge) au-dessus de l’icône du centre d’intégrité dans la barre de navigation.

![[! INCLUDe [Product Short] (includes/Product-Short. MD)] barre d’outils du point rouge du centre d’intégrité](media/health-bar.png)

### <a name="managing-product-short-health"></a>Gestion de l' [!INCLUDE [Product short](includes/product-short.md)] intégrité

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
