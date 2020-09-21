---
title: Évaluations des chemins de mouvement latéral les plus risqués d’Azure Advanced Threat Protection
description: Cet article offre une vue d’ensemble des entités sensibles d’Azure ATP avec le rapport d’évaluation de la posture de sécurité d’identité des chemins de mouvement latéral les plus risqués.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b75f04d4bcb3b4b29deddb59c713874c78b1b974
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828218"
---
# <a name="security-assessment-riskiest-lateral-movement-paths-lmp"></a>Évaluation de la sécurité : Chemins de mouvement latéral les plus risqués

## <a name="what-are-risky-lateral-movement-paths"></a>En quoi consistent les chemins de mouvement latéral risqués ?

Azure ATP supervise en permanence votre environnement pour identifier les comptes **sensibles** dont les chemins de mouvement latéral sont les plus risqués du point de vue de la sécurité. Vous en êtes informé à travers des rapports qui vous aident à gérer votre environnement. Les chemins sont considérés à risque s’ils comptent au moins trois comptes non sensibles susceptibles d’exposer le compte **sensible** à une subtilisation d’informations d’identification par des acteurs malveillants.

Apprenez-en plus sur les chemins de mouvement latéral :

- [Chemins de mouvement latéral d’Azure ATP](use-case-lateral-movement-path.md)
- [MITRE ATT&CK Lateral Movement](https://attack.mitre.org/tactics/TA0008/)

## <a name="what-risk-do-risky-lateral-movement-paths-pose"></a>Quels risques les chemins de mouvement latéral risqués font-ils courir ?

Quand une organisation ne parvient pas à sécuriser ses comptes **sensibles**, elle laisse la porte ouverte aux acteurs malveillants.

Les acteurs malveillants, à l’instar des voleurs, recherchent souvent le moyen le plus simple et le plus silencieux de s’introduire dans un environnement. Les comptes sensibles qui présentent des chemins de mouvement latéral risqués sont une aubaine pour les attaquants et peuvent être exposés à des risques.

Par exemple, les chemins les plus risqués sont mieux repérés par les attaquants et, s’ils sont compromis, peuvent leur donner accès aux entités les plus sensibles de votre organisation.

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez le tableau du rapport pour identifier les comptes **sensibles** qui présentent des chemins de mouvement latéral risqués.
    ![Passer en revue les principales entités impactées et créer un plan d’action](media/atp-cas-isp-riskiest-lmp-1.png)
1. Prenez les mesures adéquates :
    - Supprimez l’entité du groupe comme indiqué dans la recommandation.
    - Supprimez de l’appareil les autorisations d’administrateur local de l’entité comme indiqué dans la recommandation.

    > [!NOTE]
    > Attendez 24 heures, puis vérifiez que la recommandation ne figure plus dans la liste.

> [!NOTE]
> Cette évaluation est mise à jour toutes les 24 heures.

## <a name="see-also"></a>Voir aussi

- [Filtrage des activités Azure ATP dans Cloud App Security](activities-filtering-mcas.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
