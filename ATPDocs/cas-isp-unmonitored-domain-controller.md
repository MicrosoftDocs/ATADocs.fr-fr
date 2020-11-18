---
title: Évaluation des contrôleurs de domaine Microsoft Defender pour les identités non surveillées
description: Cet article fournit une vue d’ensemble du rapport d’évaluation de l’évaluation de la sécurité des identités des contrôleurs de domaine non surveillés de Microsoft Defender.
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
ms.openlocfilehash: f3cf20aed80167b581a78fea5306916578bbd4c6
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848327"
---
# <a name="security-assessment-unmonitored-domain-controllers"></a>Évaluation de la sécurité : Contrôleurs de domaine non supervisés

## <a name="what-are-unmonitored-domain-controllers"></a>Qu’entend-on par contrôleurs de domaine non supervisés ?

Une partie essentielle de la [!INCLUDE [Product long](includes/product-long.md)] solution requiert que ses capteurs soient déployés sur tous les contrôleurs de domaine de l’organisation, fournissant ainsi une vue complète de toutes les activités des utilisateurs à partir de chaque appareil.

Pour cette raison, [!INCLUDE [Product short](includes/product-short.md)] surveille en permanence votre environnement afin d’identifier les contrôleurs de domaine sans [!INCLUDE [Product short](includes/product-short.md)] capteur installé, et fournit des rapports sur ces serveurs non surveillés pour vous aider à gérer la couverture complète de votre environnement.

## <a name="what-risk-do-unmonitored-domain-controllers-pose-to-an-organization"></a>Quels risques les contrôleurs de domaine non supervisés représentent-ils pour une organisation ?

Pour fonctionner avec une efficacité maximale, tous les contrôleurs de domaine doivent être surveillés avec des [!INCLUDE [Product short](includes/product-short.md)] capteurs. Les organisations qui ne parviennent pas à remédier à des contrôleurs de domaine non contrôlés réduisent la visibilité dans leur environnement et exposent potentiellement leurs ressources à des acteurs malveillants.

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez le tableau du rapport pour découvrir lesquels de vos contrôleurs de domaine ne sont pas supervisés.
    ![Remédier à des contrôleurs de domaine non supervisés](media/cas-isp-unmonitored-domain-controller-1.png)
1. Prenez les mesures appropriées sur ces contrôleurs de domaine en [installant et en configurant des capteurs d’analyse](sensor-monitoring.md#domain-controller-status).

> [!NOTE]
> Cette évaluation est mise à jour en quasi-temps réel.

## <a name="see-also"></a>Voir aussi

- [Superviser la couverture de vos contrôleurs de domaine](sensor-monitoring.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
