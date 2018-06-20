---
title: Exclusion d’entités des détections dans Azure - Protection avancée contre les menaces | Microsoft Docs
description: Explique comment empêcher Azure ATP de détecter comme suspectes les activités d’entités spécifiques
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 60a2fae0ef044993786fb3b7e2d21a3ac27bb9f0
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
ms.locfileid: "29444915"
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="excluding-entities-from-detections"></a>Exclusion d’entités des détections
Cet article explique comment empêcher des entités de déclencher des alertes afin de minimiser les vrais positifs sans gravité, tout en vous assurant d’intercepter les vrais positifs. Pour empêcher Azure ATP de déclencher des alertes sur des activités qui peuvent faire partie de l’activité professionnelle normale d’utilisateurs spécifiques, vous pouvez empêcher des entités spécifiques de déclencher des alertes.

Par exemple, si vous disposez d’un scanneur de sécurité qui effectue le rapprochement DNS ou un administrateur qui exécute à distance des scripts sur le contrôleur de domaine et qu’il s’agit d’activités approuvées faisant partie des opérations informatiques normales de votre organisation. Afin d’obtenir plus d’informations sur les détections Azure ATP pour mieux déterminer les entités à exclure, consultez le [guide des activités suspectes](suspicious-activity-guide.md).

Pour empêcher des entités de déclencher des alertes dans Azure ATP :

Il existe deux façons d’exclure des entités : à partir de l’activité suspecte elle-même ou à partir de l’onglet **Exclusions** de la page **Configuration**.

- **À partir de l’activité suspecte** : dans la chronologie des activités suspectes, lorsque vous recevez une alerte sur une activité pour un utilisateur, un ordinateur ou une adresse IP qui est autorisé(e) à effectuer l’activité spécifique et qui peut l’exécuter fréquemment, cliquez avec le bouton droit sur les points de suspension à la fin de la ligne de l’activité suspecte pour cette entité, puis sélectionnez **Fermer et exclure**. <br></br>Cette opération ajoute l’utilisateur, l’ordinateur ou l’adresse IP à la liste des exclusions pour cette activité suspecte. Elle ferme également l’activité suspecte qui n'est plus répertoriée dans la liste d’événements **ouverts** dans la **chronologie de l’activité suspecte**.

    ![Exclure une entité](./media/exclude-in-sa.png)

- **À partir de la page Configuration** : pour vérifier ou modifier les exclusions : sous **Configuration**, cliquez sur **Exclusions**, puis sélectionnez l’activité suspecte, comme **Reconnaissance DNS**.

    ![Configuration d’exclusion](./media/exclusions.png)

Pour ajouter une entité à partir de la configuration **Exclusions** : entrez le nom de l’entité, cliquez sur le signe plus, puis cliquez sur **Enregistrer** au bas de la page.

Pour supprimer une entité de la configuration **Exclusions** : cliquez sur le signe moins en regard du nom de l’entité, puis cliquez sur **Enregistrer** au bas de la page.

Nous vous recommandons d’ajouter des exclusions aux détections seulement après avoir reçu des alertes et déterminé qu’il s’agit de vrais positifs sans gravité. 

> [!NOTE]
> Pour votre protection, toutes les détections n’offrent pas la possibilité de définir des exclusions. 

Certaines détections fournissent des conseils qui vous aident à déterminer les éléments à exclure. 

Chaque exclusion dépend du contexte. Pour certaines exclusions, vous pouvez définir des utilisateurs tandis que pour d’autres, vous pouvez définir des ordinateurs ou des adresses IP. 

Lorsque vous avez la possibilité d’exclure une adresse IP ou un ordinateur, vous pouvez exclure l’un ou l’autre. Il n’est pas nécessaire de fournir les deux.

> [!NOTE]
> Les pages de configuration peuvent être modifiées seulement par des administrateurs Azure ATP.


## <a name="see-also"></a>Voir aussi

- [Intégration à Windows Defender ATP](integrate-wd-atp.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)