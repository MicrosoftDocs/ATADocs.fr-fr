---
title: Surveiller les événements et l’intégrité système d’Azure - Protection avancée contre les menaces | Microsoft Docs
description: Le centre d’intégrité d’espace de travail Azure ATP vous permet de vérifier le bon fonctionnement du service Azure ATP, d’être alerté sur les problèmes potentiels et de consulter les événements système dans l’observateur d’événements.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 86eb90f452d5aee2504e525e64bfc62c22207880
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
ms.locfileid: "29444905"
---
*S’applique à : Azure - Protection avancée contre les menaces*


# <a name="working-with-azure-atp-workspace-health-and-events"></a>Utilisation des événements et de l’intégrité d’espace de travail Azure ATP

## <a name="azure-atp-workspace-health-center"></a>Centre d’intégrité d’espace de travail Azure ATP 

Le centre d’intégrité d’espace de travail Azure ATP vous indique les performances de votre espace de travail Azure ATP et les problèmes éventuellement rencontrés.

## <a name="working-with-the-azure-atp-workspace-health-center"></a>Utilisation du centre d’intégrité d’espace de travail Azure ATP

Si un problème se produit, le centre d’intégrité d’espace de travail Azure ATP déclenche une alerte en affichant un point rouge au-dessus de l’icône du centre d’intégrité dans la barre de menus.

![Barre d’outils avec point rouge pour le centre d’intégrité d’espace de travail Azure ATP](media/atp-health-bar.png)

### <a name="managing-azure-atp-workspace-health"></a>Gestion de l’intégrité de l’espace de travail Azure ATP
Pour vérifier l’intégrité globale de votre espace de travail, cliquez sur l’icône du centre d’intégrité dans la barre de menus. ![Icône du centre d’intégrité d’espace de travail Azure ATP](media/atp-red-dot.png)

-   Il est possible de gérer tous les problèmes ouverts en leur appliquant l’opération **Fermer** ou **Supprimer**, en cliquant sur les trois points dans l’angle de l’alerte et en sélectionnant l’option correspondante.

-   **Ouvert** : Toutes les nouvelles activités suspectes apparaissent dans cette liste.

-   **Fermé** : Utilisé pour effectuer le suivi des activités suspectes que vous avez identifiées, examinées et résolues.

    > [!NOTE]
    > Azure ATP peut rouvrir une activité fermée si celle-ci est détectée à nouveau peu de temps après.
    > Chaque espace de travail a son propre centre d’intégrité.

-   **Ignoré** : La suppression d’une activité signifie que vous voulez l’ignorer pour le moment, et être averti de nouveau seulement en cas de nouvelle instance. Si une alerte similaire survient, Azure ATP ne la rouvre pas. Cependant, si l’alerte cesse pendant sept jours puis réapparaît, vous êtes averti à nouveau.

-   **Rouvrir** : si vous fermez ou supprimez un problème, vous pouvez le rouvrir afin qu’il figure de nouveau à l’état Ouvert dans la chronologie.
- 
- **Supprimer** : dans la chronologie des activités suspectes, vous avez également la possibilité de supprimer un problème d’intégrité. Si vous supprimez une alerte, elle est supprimée de l’espace de travail et vous NE pouvez PAS la restaurer. Si vous cliquez sur Supprimer, vous pouvez supprimer toutes les activités suspectes du même type.



![Image de problèmes dans le centre d’intégrité d’espace de travail Azure ATP](media/atp-health-issue.png)






## <a name="see-also"></a>Voir aussi

- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)
