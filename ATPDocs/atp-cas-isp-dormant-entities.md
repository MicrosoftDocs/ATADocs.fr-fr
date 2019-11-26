---
title: 'Azure Advanced Threat Protection : évaluations de la sécurité des entités dormantes | Microsoft Docs'
description: Cet article propose une vue d’ensemble du rapport d’évaluation de la posture de sécurité des identités fourni par Azure ATP concernant les entités dormantes dans des groupes sensibles.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 158f714602f3add5e23b12a2f3713e9feb4a4bc3
ms.sourcegitcommit: be4525a93601d9356a4e487398262a2ffaf8c202
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/20/2019
ms.locfileid: "74206210"
---
# <a name="security-assessment-dormant-entities-in-sensitive-groups"></a>Évaluation de la sécurité : Entités dormantes dans des groupes **sensibles** 

## <a name="what-are-sensitive-dormant-entities"></a>Qu’entend-on par « entités dormantes **sensibles** » ? 
Azure ATP détecte si des utilisateurs particuliers sont **sensibles** et fournit les attributs exposés s’ils sont inactifs, désactivés ou arrivés à expiration. 

Toutefois, des comptes **sensibles** peuvent également devenir *dormants* s’ils ne sont pas utilisés pendant 180 jours. Les [entités sensibles](sensitive-accounts.md) constituent des cibles privilégiées pour les acteurs malveillants cherchant à accéder aux données sensibles d’une organisation. 

## <a name="what-risk-do-dormant-entities-create-in-sensitive-groups"></a>Quel est le risque associé à la présence d’entités dormantes dans des groupes **sensibles** ? 

Quand une organisation ne parvient pas à sécuriser ses comptes d’utilisateur dormants, elle laisse ouverte la porte de son coffre de données sensibles.  

Les acteurs malveillants, à l’instar des voleurs, recherchent souvent le moyen le plus simple et le plus silencieux de s’introduire dans un environnement. Pour pénétrer au plus profond d’une organisation, ils passent par les comptes d’utilisateur et de service **sensibles** qui ne sont plus utilisés. 

Quelle que soit la cause du problème, comme le roulement du personnel ou la mauvaise gestion des ressources, le fait d’omettre cette étape expose et vulnérabilise les entités les plus sensibles de votre organisation.   

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ? 
1. Utilisez le tableau du rapport pour découvrir les comptes sensibles dormants. 
1. Prenez ensuite les mesures appropriées pour supprimer ces comptes d’utilisateur ou leurs droits d’accès privilégiés.  


## <a name="see-also"></a>Voir aussi
- [Filtrage des activités Azure ATP dans Cloud App Security](atp-activities-filtering-mcas.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
