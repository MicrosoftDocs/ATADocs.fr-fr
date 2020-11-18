---
title: Analyse des contrôleurs de domaine et des capteurs installés installés sur vos contrôleurs de domaine à l’aide de Microsoft Defender pour l’identité
description: Décrit comment surveiller Microsoft Defender pour les capteurs d’identité et la couverture de capteur à l’aide de Defender pour l’identité
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 20e02b3281480024b67a1ef5908d82586c11f955
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94849018"
---
# <a name="monitoring-your-domain-controller-coverage"></a>Superviser la couverture de vos contrôleurs de domaine

Dès que le premier [!INCLUDE [Product long](includes/product-long.md)] capteur est installé et configuré sur un contrôleur de domaine de votre réseau, [!INCLUDE [Product short](includes/product-short.md)] commence à surveiller votre environnement pour les contrôleurs de domaine.

Une fois qu’un [!INCLUDE [Product short](includes/product-short.md)] capteur est installé et configuré sur un contrôleur de domaine de votre réseau, le capteur communique avec le [!INCLUDE [Product short](includes/product-short.md)] service sur une base constante qui envoie l’état du capteur, les informations sur l’intégrité et la version, ainsi que les événements Active Directory et les modifications collectées.

## <a name="domain-controller-status"></a>État des contrôleurs de domaine

[!INCLUDE [Product short](includes/product-short.md)] surveille en permanence votre environnement pour les contrôleurs de domaine non surveillés introduits dans votre environnement et fournit des rapports sur ceux-ci pour vous aider à gérer la couverture complète de votre environnement.

1. Pour vérifier l’état de vos contrôleurs de domaine détectés et non surveillés et leur état, accédez à la zone **configuration** du [!INCLUDE [Product short](includes/product-short.md)] portail et, sous la section **système** , sélectionnez **capteurs**.

    ![[! INCLUDe [Product Short] (includes/Product-Short. MD)] analyse de l’état du capteur](media/sensors-status-monitoring.png)

1. Tous les contrôleurs de domaine supervisés et non supervisés détectés sont listés en haut de l’écran. Pour télécharger les détails de l’état de supervision des contrôleurs de domaine, sélectionnez **Téléchargement des détails**.

Le fichier Excel téléchargé contient les informations de couverture suivantes pour tous les contrôleurs de domaine détectés dans votre organisation :

|Intitulé|Description|
|----|----|
|HostName|Nom de l'ordinateur|
|Nom de domaine|Nom de domaine|
|Surveillé|[!INCLUDE [Product short](includes/product-short.md)] État de l’analyse|
|Type de capteur|[!INCLUDE [Product short](includes/product-short.md)] capteur ou [!INCLUDE [Product short](includes/product-short.md)] capteur autonome|
|Unité d'organisation|Emplacement dans Active Directory |
|Version du système d'exploitation| Version du système d’exploitation détecté|
|Adresse IP|Adresse IP détectée|

## <a name="search-domain-controllers"></a>Rechercher les contrôleurs de domaine

La gestion de votre flotte de capteurs et de contrôleurs de domaine peut constituer un défi. Pour faciliter la recherche et l’identification, les contrôleurs de domaine peuvent être recherchés à l’aide de la fonctionnalité de recherche dans la [!INCLUDE [Product short](includes/product-short.md)] liste des capteurs.

1. Pour rechercher vos contrôleurs de domaine, accédez à la zone **configuration** du [!INCLUDE [Product short](includes/product-short.md)] portail et, sous la section **système** , sélectionnez **capteurs**.
1. Sélectionnez l’option de filtre sur la colonne **contrôleur de domaine** dans la liste de tables du contrôleur de domaine.
1. Entrez le nom que vous souhaitez rechercher. Les caractères génériques ne sont actuellement pas pris en charge dans le champ de recherche.

    ![[! INCLUDe [Product Short] (includes/Product-Short. MD)] Rechercher dans le contrôleur de domaine](media/search-sensor.png)

> [!NOTE]
> [!INCLUDE [Product short](includes/product-short.md)] les pages de configuration du portail ne peuvent être modifiées que par les [!INCLUDE [Product short](includes/product-short.md)] administrateurs.

## <a name="see-also"></a>Voir aussi

- [Architecture [!INCLUDE [Product short](includes/product-short.md)]](architecture.md)
- [Configuration des [!INCLUDE [Product short](includes/product-short.md)] capteurs](install-step5.md)
- [Prise en charge de plusieurs forêts](multi-forest.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
