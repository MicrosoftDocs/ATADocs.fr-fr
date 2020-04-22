---
title: Surveiller les événements et l’intégrité système d’Azure Advanced Threat Protection
description: Le centre d’intégrité Azure ATP vous permet de vérifier le bon fonctionnement du service Azure ATP, d’être alerté sur les problèmes potentiels et de consulter les événements système dans l’observateur d’événements.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 1/3/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 743d2f6c147542ff2b57383e93c75474ea9524b9
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79414537"
---
# <a name="work-with-azure-atp-health-and-events"></a>Utiliser l’intégrité et les événements Azure ATP

## <a name="azure-atp-health-center"></a>Centre d’intégrité Azure ATP 

Le centre d’intégrité Azure ATP vous indique les performances de votre instance Azure ATP et les problèmes éventuellement rencontrés.

## <a name="working-with-the-azure-atp-health-center"></a>Utilisation du centre d’intégrité Azure ATP

Si un problème se produit, le centre d’intégrité Azure ATP déclenche une alerte en affichant un point rouge au-dessus de l’icône du centre d’intégrité dans la barre de menus.

![Barre d’outils avec point rouge pour le centre d’intégrité Azure ATP](media/atp-health-bar.png)

### <a name="managing-azure-atp-health"></a>Gestion de l’intégrité d’Azure ATP
Pour vérifier l’intégrité globale de votre instance Azure ATP, cliquez sur l’icône du centre d’intégrité dans la barre de menus. ![Icône du centre d’intégrité Azure ATP](media/atp-red-dot.png)

-   Il est possible de gérer tous les problèmes ouverts en leur appliquant l’opération **Fermer** ou **Supprimer**, en cliquant sur les trois points dans l’angle de l’alerte et en sélectionnant l’option correspondante.

-   **Ouvert** : Toutes les nouvelles activités suspectes apparaissent dans cette liste.

-   **Fermé** : Utilisé pour effectuer le suivi des activités suspectes que vous avez identifiées, examinées et résolues.

    > [!NOTE]
    > Azure ATP peut rouvrir une activité fermée si celle-ci est détectée à nouveau peu de temps après.
    
-   **Ignoré** : La suppression d’une activité signifie que vous voulez l’ignorer pour le moment, et être averti de nouveau seulement en cas de nouvelle instance. Si une alerte similaire survient, Azure ATP ne la rouvre pas. Cependant, si l’alerte cesse pendant sept jours puis réapparaît, vous êtes de nouveau averti.

-   **Rouvrir** : vous pouvez rouvrir une alerte fermée ou supprimée de sorte qu’elle figure à nouveau à l’état **Ouvert** dans la chronologie.

-   **Supprimer** : dans la chronologie des alertes de sécurité, vous avez aussi la possibilité de supprimer un problème d’intégrité. Si vous supprimez une alerte, celle-ci est supprimée de l’instance et vous NE pouvez PAS la restaurer. Si vous cliquez sur Supprimer, vous supprimez toutes les alertes de sécurité du même type.



![Image montrant des problèmes dans le centre d’intégrité Azure ATP](media/atp-health-issue.png)






## <a name="see-also"></a>Voir aussi

- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
