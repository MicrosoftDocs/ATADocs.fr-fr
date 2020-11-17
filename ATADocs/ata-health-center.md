---
title: Surveiller l’intégrité et les événements du système Advanced Threat Analytics
description: Le centre d’intégrité ATA vous permet de vérifier le bon fonctionnement du service ATA, d’être alerté en cas de problèmes potentiels et de voir les événements système dans l’observateur d’événements.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: caac51c76334b62250c86e78dbdb5d9193f47f6d
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94691058"
---
# <a name="working-with-ata-system-health-and-events"></a>Utilisation de l’intégrité et des événements système d’ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

## <a name="ata-health-center"></a>Centre d’intégrité ATA

Le centre d’intégrité ATA vous permet d’évaluer les performances de votre service ATA et vous prévient en cas de problèmes.

## <a name="working-with-the-ata-health-center"></a>Utilisation du centre d’intégrité ATA
Si un problème se produit, le centre d’intégrité ATA déclenche une alerte en affichant un point rouge au-dessus de l’icône du centre d’intégrité dans la barre de menus.

![Barre d’outils du point rouge dans le centre d’intégrité ATA](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>Gestion de l’intégrité d’ATA
Pour vérifier l’intégrité globale de votre système, cliquez sur l’icône du centre d’intégrité dans la barre de menus. ![Icône du centre d’intégrité ATA](media/ATA-red-dot.png)

- Il est possible de gérer toutes les alertes actives et de leur appliquer l’opération **Fermer**, **Ignorer** ou **Supprimer** en cliquant sur les trois points dans l’angle de l’alerte et en sélectionnant l’option correspondante.

-   **Ouvert** : Toutes les nouvelles activités suspectes apparaissent dans cette liste.

-   **Fermé** : Utilisé pour effectuer le suivi des activités suspectes que vous avez identifiées, examinées et résolues.

    > [!NOTE]
    > ATA peut rouvrir une activité fermée si celle-ci est détectée à nouveau peu de temps après.

-   **Ignoré** : La suppression d’une activité signifie que vous voulez l’ignorer pour le moment, et être averti de nouveau seulement en cas de nouvelle instance. Si une alerte similaire survient, ATA ne la rouvre pas. Cependant, si l’alerte cesse pendant sept jours puis réapparaît, vous êtes averti à nouveau.

- **Supprimer** : Si vous supprimez une alerte, elle est supprimée du système et de la base de données, et vous NE pourrez PAS la restaurer. Si vous cliquez sur Supprimer, vous pouvez supprimer toutes les activités suspectes du même type.



![Image de problèmes dans le centre d’intégrité ATA](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>Voir aussi

- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
