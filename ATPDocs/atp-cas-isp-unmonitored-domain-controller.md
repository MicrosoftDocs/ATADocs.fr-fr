---
title: Évaluations des contrôleurs de domaine non supervisés Azure Advanced Threat Protection
description: Cet article propose une vue d’ensemble du rapport d’évaluation de la posture de sécurité des identités des contrôleurs de domaine non supervisés d’Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 878f251c1f2936a9207dc351adc9ae5680abe3c4
ms.sourcegitcommit: 098a20abe62e153372da4c96db256bc63c113bd1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88809054"
---
# <a name="security-assessment-unmonitored-domain-controllers"></a>Évaluation de la sécurité : Contrôleurs de domaine non supervisés

## <a name="what-are-unmonitored-domain-controllers"></a>Qu’entend-on par contrôleurs de domaine non supervisés ?

Une partie essentielle de la solution Azure ATP nécessite que ses capteurs soient déployés sur tous les contrôleurs de domaine de l’organisation, fournissant ainsi une vue complète de toutes les activités des utilisateurs à partir de chaque appareil.

Azure ATP surveille donc en permanence votre environnement pour identifier les contrôleurs de domaine sans capteur Azure ATP installé et génère des rapports sur ces serveurs non supervisés pour vous aider à gérer la couverture complète de votre environnement.

## <a name="what-risk-do-unmonitored-domain-controllers-pose-to-an-organization"></a>Quels risques les contrôleurs de domaine non supervisés représentent-ils pour une organisation ?

Pour fonctionner avec une efficacité maximale, tous les contrôleurs de domaine doivent être surveillés avec des capteurs Azure ATP. Les organisations qui ne parviennent pas à remédier à des contrôleurs de domaine non contrôlés réduisent la visibilité dans leur environnement et exposent potentiellement leurs ressources à des acteurs malveillants.

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez le tableau du rapport pour découvrir lesquels de vos contrôleurs de domaine ne sont pas supervisés.
    ![Remédier à des contrôleurs de domaine non supervisés](media/atp-cas-isp-unmonitored-domain-controller-1.png)
1. Prenez les mesures appropriées sur ces contrôleurs de domaine en [installant et en configurant des capteurs d’analyse](atp-sensor-monitoring.md#domain-controller-status).

> [!NOTE]
> Cette évaluation est mise à jour en quasi-temps réel.

## <a name="see-also"></a>Voir aussi

- [Superviser la couverture de vos contrôleurs de domaine](atp-sensor-monitoring.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
