---
title: Supervision des contrôleurs de domaine et des capteurs installés sur vos contrôleurs de domaine à l’aide d’Azure Advanced Threat Protection
description: Décrit comment superviser les capteurs Azure ATP et la couverture des capteurs à l’aide d’Azure ATP
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 04/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 92decce8-b3ae-4d32-8407-a95314a66863
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 022f813ecb999309091a46639a257bac343ee286
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81462164"
---
# <a name="monitoring-your-domain-controller-coverage"></a>Superviser la couverture de vos contrôleurs de domaine

Dès que vous avez installé et configuré le premier capteur Azure ATP sur l’un des contrôleurs de domaine dans votre réseau, Azure ATP démarre la supervision des contrôleurs de domaine de votre environnement.

Une fois qu’un capteur Azure ATP est installé et configuré sur un contrôleur de domaine de votre réseau, il communique en permanence avec le service Azure ATP en lui envoyant des informations d’état, des informations sur l’intégrité et la version ainsi que les événements et changements collectés à partir d’Active Directory.

## <a name="domain-controller-status"></a>État des contrôleurs de domaine

Azure ATP supervise en continu votre environnement afin de détecter l’ajout de contrôleurs de domaine non supervisés dans votre environnement. Le cas échéant, il génère des rapports sur ces derniers pour vous aider à gérer la couverture complète de votre environnement.

1. Pour vérifier l’état des contrôleurs de domaine supervisés et non supervisés qui ont été détectés, accédez à la zone **Configuration** dans le portail Azure ATP et, sous la section **Système**, sélectionnez **Capteurs**.

    ![Supervision de l’état par le capteur Azure ATP](media/atp-sensors-status-monitoring.png)

2. Tous les contrôleurs de domaine supervisés et non supervisés détectés sont listés en haut de l’écran. Pour télécharger les détails de l’état de supervision des contrôleurs de domaine, sélectionnez **Téléchargement des détails**.

Le fichier Excel téléchargé contient les informations de couverture suivantes pour tous les contrôleurs de domaine détectés dans votre organisation :

|Titre|Description|
|----|----|
|Nom d’hôte|Nom de l'ordinateur|
|Nom du domaine|Nom du domaine|
|Supervisé|État de la supervision Azure ATP|
|Type de capteur|Capteur Azure ATP ou capteur autonome Azure ATP|
|Unité d'organisation|Emplacement dans Active Directory |
|Version du système d'exploitation| Version du système d’exploitation détecté|
|Adresse IP|Adresse IP détectée|

## <a name="search-domain-controllers"></a>Rechercher les contrôleurs de domaine

La gestion de votre flotte de capteurs et de contrôleurs de domaine peut constituer un défi. Pour faciliter la recherche et l’identification, les contrôleurs de domaine peuvent être recherchés à l’aide de la fonctionnalité de recherche de la liste de capteurs Azure ATP.

1. Pour rechercher vos contrôleurs de domaine, accédez à la zone **Configuration** du portail Azure ATP et, sous la section **système**, sélectionnez **Capteurs**.
1. Sélectionnez l’option de filtre sur la colonne **contrôleur de domaine** dans la liste de tables du contrôleur de domaine.
1. Entrez le nom que vous souhaitez rechercher. Les caractères génériques ne sont actuellement pas pris en charge dans le champ de recherche.

    ![Recherche de contrôleur de domaine Azure ATP](media/search-sensor.png)

> [!NOTE]
> Les pages de configuration dans le portail Azure ATP sont modifiables uniquement par les administrateurs Azure ATP.

## <a name="see-also"></a>Voir aussi

- [Architecture Azure ATP](atp-architecture.md)
- [Configurer des capteurs Azure ATP](install-atp-step5.md)
- [Prise en charge de plusieurs forêts](atp-multi-forest.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
