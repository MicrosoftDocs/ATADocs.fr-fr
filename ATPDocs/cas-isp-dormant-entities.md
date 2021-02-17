---
title: Évaluation de la sécurité des entités dormantes Microsoft Defender for Identity
description: Cet article fournit une vue d’ensemble de Microsoft Defender pour les entités dormantes de l’identité dans les groupes sensibles rapport d’évaluation de la sécurité des identités.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 44d7cc7c7152d95230440eeef45ee42a9e11c55d
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630728"
---
# <a name="security-assessment-dormant-entities-in-sensitive-groups"></a>Évaluation de la sécurité : Entités dormantes dans des groupes **sensibles**

## <a name="what-are-sensitive-dormant-entities"></a>Qu’entend-on par « entités dormantes **sensibles** » ?

[!INCLUDE [Product long](includes/product-long.md)] Découvre si des utilisateurs particuliers sont **sensibles** , et fournissent des attributs qui se trouvent s’ils sont inactifs, désactivés ou arrivés à expiration.

Toutefois, des comptes **sensibles** peuvent également devenir *dormants* s’ils ne sont pas utilisés pendant 180 jours. Les [entités sensibles](manage-sensitive-honeytoken-accounts.md) constituent des cibles privilégiées pour les acteurs malveillants cherchant à accéder aux données sensibles d’une organisation.

## <a name="what-risk-do-dormant-entities-create-in-sensitive-groups"></a>Quel est le risque associé à la présence d’entités dormantes dans des groupes **sensibles** ?

Quand une organisation ne parvient pas à sécuriser ses comptes d’utilisateur dormants, elle laisse ouverte la porte de son coffre de données sensibles.

Les acteurs malveillants, à l’instar des voleurs, recherchent souvent le moyen le plus simple et le plus silencieux de s’introduire dans un environnement. Un chemin d’accès simple et silencieux au sein de votre organisation consiste à utiliser des comptes d’utilisateur et de service **sensibles** qui ne sont plus utilisés.

Quelle que soit la cause du problème, comme le roulement du personnel ou la mauvaise gestion des ressources, le fait d’omettre cette étape expose et vulnérabilise les entités les plus sensibles de votre organisation.

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez le tableau du rapport pour découvrir les comptes sensibles dormants.
    ![Corriger les entités dormantes des groupes sensibles ini](media/cas-isp-dormant-entities-sensitive-groups-1.png)
1. Prenez ensuite les mesures appropriées pour supprimer ces comptes d’utilisateur ou leurs droits d’accès privilégiés.

> [!NOTE]
> Cette évaluation est mise à jour en quasi-temps réel.

## <a name="see-also"></a>Voir aussi

- [[!INCLUDE [Product short](includes/product-short.md)] filtrage des activités dans Cloud App Security](activities-filtering-mcas.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
