---
title: Exclusion d’entités des détections dans Azure Advanced Threat Protection | Microsoft Docs
description: Explique comment empêcher Azure ATP de détecter comme suspectes les activités d’entités spécifiques
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/11/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 77c85c161ac3a62f67a1bc0983544f6dcef5e596
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196958"
---
# <a name="excluding-entities-from-detections"></a>Exclusion d’entités des détections
Cet article explique comment exclure des entités du processus de déclenchement des alertes. Certaines entités sont exclues afin de limiter les vrais positifs sans gravité tout en garantissant la détection des vrais positifs. Pour supprimer le bruit qu’Azure ATP génère à propos d’activités effectuées par des utilisateurs dans le cadre de leur activité professionnelle normale, vous pouvez désactiver, ou exclure, des entités spécifiques du processus de déclenchement des alertes. Par ailleurs, certaines entités courantes sont exclues par défaut. 

Par exemple, les activités approuvées dans le cadre des opérations informatiques normales dans votre organisation, comme la reconnaissance DNS effectuée par un scanneur de sécurité ou l’exécution de scripts à distance sur le contrôleur de domaine par un administrateur, peuvent être exclues. Pour plus d’informations sur chaque détection Azure ATP et le choix des entités à exclure, consultez le [Guide des alertes de sécurité](suspicious-activity-guide.md).

## <a name="entities-excluded-by-default-from-raising-alerts"></a>Entités exclues par défaut du processus de déclenchement des alertes
 Pour certaines alertes, comme **Communication suspecte sur DNS**, des exclusions de domaine automatiques sont ajoutées par Azure ATP sur la base des recherches et des commentaires des clients. 
 
![Exclusions automatiques des alertes Communication suspecte sur DNS](./media/dns-auto-exclusions.png) 

## <a name="exclude-entities-from-raising-alerts"></a>Exclure des entités du processus de déclenchement des alertes

Il y a deux façons d’exclure manuellement des entités : soit directement à partir de l’alerte de sécurité, soit à partir de l’onglet **Exclusions** de la page **Configuration**. 

- **Dans l’alerte de sécurité** : dans la chronologie des activités, quand vous recevez une alerte sur l’activité d’un utilisateur, d’un ordinateur ou d’une adresse IP qui **est** autorisé à effectuer cette activité, même fréquemment, suivez les étapes ci-dessous :
  - Cliquez avec le bouton droit sur les points de suspension à la fin de la ligne de l’alerte de sécurité pour cette entité, puis sélectionnez **Fermer et exclure**. Cette opération ajoute l’utilisateur, l’ordinateur ou l’adresse IP à la liste des exclusions définies pour cette alerte de sécurité. Elle ferme l’alerte de sécurité et la retire de la liste des événements **Ouvert** dans la **chronologie des alertes**.

    ![Exclure une entité](./media/exclude-in-sa.png)

- **Sur la page de configuration** :  pour vérifier ou modifier des exclusions, cliquez sur **Exclusions** sous **Configuration**, puis sélectionnez l’alerte de sécurité à laquelle l’exclusion sera appliquée, comme **Reconnaissance DNS**.

    ![Configuration d’exclusion](./media/exclusions.png)

Pour ajouter une entité à partir de la configuration **Exclusions** : entrez le nom de l’entité, cliquez sur le signe plus, puis cliquez sur **Enregistrer** en bas de la page.

Pour supprimer une entité de la configuration **Exclusions** : cliquez sur le signe moins à côté du nom de l’entité, puis cliquez sur **Enregistrer** en bas de la page.

Nous vous recommandons d’ajouter des exclusions aux détections seulement après avoir reçu des alertes du type en question *et* vérifié qu’il s’agit de vrais positifs sans gravité. 

> [!NOTE]
> Pour votre protection, toutes les détections n’offrent pas la possibilité de définir des exclusions. 

Certaines détections fournissent des conseils qui vous aident à déterminer les éléments à exclure. 

Chaque exclusion dépend du contexte. Pour certaines exclusions, vous pouvez définir des utilisateurs tandis que pour d’autres, vous pouvez définir des ordinateurs ou des adresses IP. 

Lorsque vous avez la possibilité d’exclure une adresse IP ou un ordinateur, vous pouvez exclure l’un ou l’autre. Il n’est pas nécessaire de fournir les deux.

> [!NOTE]
> Les pages de configuration sont modifiables uniquement par les administrateurs Azure ATP.


## <a name="see-also"></a>Voir aussi

- [Guide des alertes de sécurité d’Azure ATP](suspicious-activity-guide.md)
- [Intégration à Windows Defender ATP](integrate-wd-atp.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
