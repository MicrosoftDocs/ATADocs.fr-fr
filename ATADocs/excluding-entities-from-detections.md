---
title: Exclusion d’entités des détections dans Advanced Threat Analytics | Microsoft Docs
description: Explique comment empêcher ATA de détecter comme suspectes les activités d’une entité spécifique
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 21b1d8a4537bb77de120dac4b2f15bc785161749
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010259"
---
*S’applique à : Advanced Threat Analytics version 1.9*



# <a name="excluding-entities-from-detections"></a>Exclusion d’entités des détections
Cet article explique comment empêcher des entités de déclencher des alertes afin de minimiser les vrais positifs sans gravité, tout en vous assurant d’intercepter les vrais positifs. Pour empêcher qu’ATA ne déclenche des alertes sur des activités qui peuvent faire partie de l’activité professionnelle normale d’utilisateurs spécifiques, vous pouvez empêcher des entités spécifiques de déclencher des alertes.

Par exemple, si vous disposez d’un scanneur de sécurité qui effectue le rapprochement DNS ou un administrateur qui exécute à distance des scripts sur le contrôleur de domaine et qu’il s’agit d’activités approuvées faisant partie des opérations informatiques normales de votre organisation.

Pour empêcher des entités de déclencher des alertes dans ATA :

Il existe deux façons d’exclure des entités : à partir de l’activité suspecte elle-même ou à partir de l’onglet **Exclusions** de la page **Configuration**.

- **À partir de l’activité suspecte** : dans la chronologie de l’activité suspecte, lorsque vous recevez une alerte sur une activité pour un utilisateur, un ordinateur ou une adresse IP qui est autorisé(e) à effectuer l’activité spécifique et qui peut l’exécuter fréquemment, cliquez avec le bouton droit sur les points de suspension à la fin de la ligne de l’activité suspecte pour cette entité, puis sélectionnez **Fermer et exclure**. <br></br>Cette opération ajoute l’utilisateur, l’ordinateur ou l’adresse IP à la liste des exclusions pour cette activité suspecte. Elle ferme également l’activité suspecte qui n'est plus répertoriée dans la liste d’événements **ouverts** dans la **chronologie de l’activité suspecte**.

    ![Exclure une entité](./media/exclude-in-sa.png)

- **À partir de la page Configuration** : pour vérifier ou modifier les exclusions : sous **Configuration**, cliquez sur **Exclusions**, puis sélectionnez l’activité suspecte, comme **Informations d’identification de compte sensibles exposées**.

    ![Configuration d’exclusion](./media/exclusions-config-page.png)

Pour supprimer une entité de la configuration **Exclusions** : cliquez sur le signe moins en regard du nom de l’entité, puis cliquez sur **Enregistrer** au bas de la page.

Nous vous recommandons d’ajouter des exclusions aux détections seulement après avoir reçu des alertes et déterminé qu’il s’agit de vrais positifs sans gravité. 

> [!NOTE]
> Pour votre protection, toutes les détections n’offrent pas la possibilité de définir des exclusions. 

Certaines détections fournissent des conseils qui vous aident à déterminer les éléments à exclure. 

Chaque exclusion dépend du contexte. Pour certaines exclusions, vous pouvez définir des utilisateurs tandis que pour d’autres, vous pouvez définir des ordinateurs ou des adresses IP. 

Lorsque vous avez la possibilité d’exclure une adresse IP ou un ordinateur, vous pouvez exclure l’un ou l’autre. Il n’est pas nécessaire de fournir les deux.

> [!NOTE]
> Les pages de configuration peuvent être modifiées seulement par des administrateurs d’ATA.


## <a name="see-also"></a>Voir aussi
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Modification de la configuration d’ATA](modifying-ata-center-configuration.md)
