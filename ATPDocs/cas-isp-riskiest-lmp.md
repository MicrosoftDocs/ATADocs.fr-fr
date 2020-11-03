---
title: Évaluations de chemins de mouvement latéral Microsoft Defender for Identity riskiest
description: Cet article fournit une vue d’ensemble de Microsoft Defender pour les entités sensibles de l’identité avec les chemins de mouvement latéral riskiest rapport d’évaluation de la sécurité des identités.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: df369b2a718b1aa2cb552bb42712a6b36275e2ee
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93276669"
---
# <a name="security-assessment-riskiest-lateral-movement-paths-lmp"></a>Évaluation de la sécurité : Chemins de mouvement latéral les plus risqués

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-are-risky-lateral-movement-paths"></a>En quoi consistent les chemins de mouvement latéral risqués ?

[!INCLUDE [Product long](includes/product-long.md)] surveille en permanence votre environnement afin d’identifier les comptes **sensibles** avec les chemins de mouvement latéral riskiest qui présentent un risque de sécurité et fournit des rapports sur ces comptes pour vous aider à gérer votre environnement. Les chemins sont considérés à risque s’ils comptent au moins trois comptes non sensibles susceptibles d’exposer le compte **sensible** à une subtilisation d’informations d’identification par des acteurs malveillants.

Apprenez-en plus sur les chemins de mouvement latéral :

- [[!INCLUDE [Product short](includes/product-short.md)] Chemins de mouvement latéral (LMPs)](use-case-lateral-movement-path.md)
- [MITRE ATT&CK Lateral Movement](https://attack.mitre.org/tactics/TA0008/)

## <a name="what-risk-do-risky-lateral-movement-paths-pose"></a>Quels risques les chemins de mouvement latéral risqués font-ils courir ?

Quand une organisation ne parvient pas à sécuriser ses comptes **sensibles** , elle laisse la porte ouverte aux acteurs malveillants.

Les acteurs malveillants, à l’instar des voleurs, recherchent souvent le moyen le plus simple et le plus silencieux de s’introduire dans un environnement. Les comptes sensibles qui présentent des chemins de mouvement latéral risqués sont une aubaine pour les attaquants et peuvent être exposés à des risques.

Par exemple, les chemins les plus risqués sont mieux repérés par les attaquants et, s’ils sont compromis, peuvent leur donner accès aux entités les plus sensibles de votre organisation.

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez le tableau du rapport pour identifier les comptes **sensibles** qui présentent des chemins de mouvement latéral risqués.
    ![Passer en revue les principales entités impactées et créer un plan d’action](media/cas-isp-riskiest-lmp-1.png)
1. Prenez les mesures adéquates :
    - Supprimez l’entité du groupe comme indiqué dans la recommandation.
    - Supprimez de l’appareil les autorisations d’administrateur local de l’entité comme indiqué dans la recommandation.

    > [!NOTE]
    > Attendez 24 heures, puis vérifiez que la recommandation ne figure plus dans la liste.

> [!NOTE]
> Cette évaluation est mise à jour toutes les 24 heures.

## <a name="see-also"></a>Voir aussi

- [[!INCLUDE [Product short](includes/product-short.md)] filtrage des activités dans Cloud App Security](activities-filtering-mcas.md)
- [Consultez le [!INCLUDE [Product short](includes/product-short.md)] Forum !](https://aka.ms/MDIcommunity)
