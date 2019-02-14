---
title: Supervision des contrôleurs de domaine et des capteurs installés sur vos contrôleurs de domaine à l’aide d’Azure Advanced Threat Protection | Microsoft Docs
description: Décrit comment superviser les capteurs Azure ATP et la couverture des capteurs à l’aide d’Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/27/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 92decce8-b3ae-4d32-8407-a95314a66863
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e4e33e79a5ed4dbb80214e50dbccee0f067670fd
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077913"
---
# <a name="monitoring-your-domain-controller-coverage"></a>Superviser la couverture de vos contrôleurs de domaine

Dès que vous avez installé et configuré votre premier capteur Azure ATP sur l’un des contrôleurs de domaine dans votre réseau, Azure ATP démarre la supervision des contrôleurs de domaine de votre environnement. 

Lors de la configuration, il est recommandé de désigner au moins un contrôleur de domaine supervisé par le capteur Azure ATP comme candidat synchronisateur de domaine dans chaque domaine. L’un des rôles du capteur synchronisateur de domaine est de garantir que les contrôleurs de domaine sont activement recherchés par ce capteur spécifique. Après la configuration initiale, il est possible d’activer ou de désactiver l’état de candidat synchronisateur de domaine pour chaque contrôleur de domaine. Consultez [Configurer le capteur Azure ATP](install-atp-step5.md) pour obtenir plus d’informations sur la configuration d’un capteur Azure et sa désignation comme **candidat synchronisateur de domaine**. 

Une fois qu’un capteur Azure ATP est installé et configuré sur un contrôleur de domaine de votre réseau, il communique en permanence avec le service Azure ATP en lui envoyant des informations d’état, des informations sur l’intégrité et la version ainsi que les événements et changements collectés à partir d’Active Directory.  

### <a name="domain-controller-status"></a>État des contrôleurs de domaine

Azure ATP supervise en continu votre environnement afin de détecter l’ajout de contrôleurs de domaine non supervisés dans votre environnement. Le cas échéant, il génère des rapports sur ces derniers pour vous aider à gérer la couverture complète de votre environnement. 

1. Pour vérifier l’état des contrôleurs de domaine supervisés et non supervisés qui ont été détectés, accédez à la zone **Configuration** dans le portail Azure ATP et, sous la section **Système**, sélectionnez **Capteurs**.
   
     ![Supervision de l’état par le capteur Azure ATP](media/atp-sensors-status-monitoring.png)

2. Tous les contrôleurs de domaine supervisés et non supervisés détectés sont listés en haut de l’écran. Pour télécharger les détails de l’état de supervision des contrôleurs de domaine, sélectionnez **Téléchargement des détails**. 

Le fichier Excel téléchargé contient les informations de couverture suivantes pour tous les contrôleurs de domaine détectés dans votre organisation :

|Titre|Description|
|----|----|
|Nom d'hôte|Nom de l'ordinateur|
|Nom du domaine|Nom du domaine|
|Supervisé|État de la supervision Azure ATP|
|Type de capteur|Capteur Azure ATP ou capteur autonome Azure ATP|
|Unité d'organisation|Emplacement dans Active Directory |
|Version du système d'exploitation| Version du système d’exploitation détecté|
|Adresse IP|Adresse IP détectée| 


> [!NOTE]
> Les pages de configuration dans le portail Azure ATP sont modifiables uniquement par les administrateurs Azure ATP.


## <a name="see-also"></a>Voir aussi

- [Architecture Azure ATP](atp-architecture.md)
- [Configurer des capteurs Azure ATP](install-atp-step5.md)
- [Prise en charge de plusieurs forêts](atp-multi-forest.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)