---
title: Exclusion d’entités des détections dans Microsoft Defender pour Identity
description: Explique comment empêcher Microsoft Defender pour Identity de détecter comme suspectes des activités d’entités spécifiques.
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
ms.openlocfilehash: e87d71ead236d36e032a43c825980f98f7f15eb4
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93277176"
---
# <a name="excluding-entities-from-detections"></a>Exclusion d’entités des détections

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Cet article explique comment exclure des entités du processus de déclenchement des alertes. Certaines entités sont exclues afin de limiter les vrais positifs sans gravité tout en garantissant la détection des vrais positifs. Pour supprimer le bruit généré par [!INCLUDE [Product long](includes/product-long.md)] à propos d’activités effectuées par des utilisateurs spécifiques dans le cadre de leur activité professionnelle normale, vous pouvez désactiver (ou exclure) des entités spécifiques du processus de déclenchement des alertes. Par ailleurs, certaines entités courantes sont exclues par défaut.

Par exemple, les activités approuvées dans le cadre des opérations informatiques normales dans votre organisation, comme la reconnaissance DNS effectuée par un scanneur de sécurité ou l’exécution de scripts à distance sur le contrôleur de domaine par un administrateur, peuvent être exclues. Pour plus d’informations sur chaque détection [!INCLUDE [Product short](includes/product-short.md)] afin de choisir les entités à exclure, consultez le [Guide des alertes de sécurité](suspicious-activity-guide.md).

## <a name="entities-excluded-by-default-from-raising-alerts"></a>Entités exclues par défaut du processus de déclenchement des alertes

 Pour certaines alertes (par exemple, **Communication suspecte sur DNS** ), des exclusions de domaine automatiques sont ajoutées par [!INCLUDE [Product short](includes/product-short.md)] sur la base des recherches et des commentaires des clients.

![Exclusions automatiques des alertes Communication suspecte sur DNS](media/dns-auto-exclusions.png)

## <a name="exclude-entities-from-raising-alerts"></a>Exclure des entités du processus de déclenchement des alertes

Il y a deux façons d’exclure manuellement des entités : soit directement à partir de l’alerte de sécurité, soit à partir de l’onglet **Exclusions** de la page **Configuration**.

- **À partir de l’alerte de sécurité** : dans la chronologie des activités, quand vous recevez une alerte sur une activité associée à un utilisateur, un ordinateur ou une adresse IP qui **est** autorisé à effectuer cette activité, même fréquemment, effectuez les étapes suivantes :
  - Cliquez avec le bouton droit sur les points de suspension à la fin de la ligne de l’alerte de sécurité pour cette entité, puis sélectionnez **Fermer et exclure**. Cette opération ajoute l’utilisateur, l’ordinateur ou l’adresse IP à la liste des exclusions définies pour cette alerte de sécurité. Elle ferme l’alerte de sécurité et la retire de la liste des événements **Ouvert** dans la **chronologie des alertes**.

    ![Exclure une entité](media/exclude-in-sa.png)

- **Sur la page de configuration** :  pour vérifier ou modifier des exclusions, cliquez sur **Exclusions** sous **Configuration** > **Détection** , puis sélectionnez l’alerte de sécurité à laquelle l’exclusion sera appliquée (par exemple, **Reconnaissance DNS** ).

    ![Configuration d’exclusion](media/exclusions.png)

Pour ajouter une entité à partir de la configuration **Exclusions** : entrez le nom de l’entité, cliquez sur le signe plus, puis cliquez sur **Enregistrer** en bas de la page.

Pour supprimer une entité de la configuration **Exclusions** : cliquez sur le signe moins à côté du nom de l’entité, puis cliquez sur **Enregistrer** en bas de la page.

Nous vous recommandons d’ajouter des exclusions aux détections seulement après avoir reçu des alertes du type en question *et* vérifié qu’il s’agit de vrais positifs sans gravité.

> [!NOTE]
> Pour votre protection, toutes les détections n’offrent pas la possibilité de définir des exclusions.

Certaines détections fournissent des conseils qui vous aident à déterminer les éléments à exclure.

Chaque exclusion dépend du contexte. Pour certaines exclusions, vous pouvez définir des utilisateurs tandis que pour d’autres, vous pouvez définir des ordinateurs ou des adresses IP.

Lorsque vous avez la possibilité d’exclure une adresse IP ou un ordinateur, vous pouvez exclure l’un ou l’autre. Il n’est pas nécessaire de fournir les deux.

> [!NOTE]
> Les pages de configuration ne sont modifiables que par les administrateurs [!INCLUDE [Product short](includes/product-short.md)].

## <a name="see-also"></a>Voir aussi

- [Guide des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)]](suspicious-activity-guide.md)
- [Intégration avec Microsoft Defender pour point de terminaison](integrate-mde.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
