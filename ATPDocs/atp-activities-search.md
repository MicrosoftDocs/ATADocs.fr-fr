---
title: Filtrer et rechercher des activités supervisées dans Azure Advanced Threat Protection
description: Cet article offre une vue d’ensemble du filtrage et de la recherche d’activités supervisées à l’aide d’Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a546703b-d5a9-404d-9e87-125523bb8421
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 39e9d4c6656d2e55389720ab86690cfcd705423f
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80669537"
---
# <a name="azure-atp-monitored-activities-search-and-filter"></a>Recherche et filtrage d’activités supervisées dans Azure ATP 

> [!NOTE]
> Les fonctionnalités Azure ATP expliquées dans cette page sont également accessibles dans le nouveau [portail](https://portal.cloudappsecurity.com).

Les activités détectées par Azure ATP sur votre réseau peuvent faire l’objet de recherches et de filtrages pour en faciliter l’exploration et l’organisation pendant que vous analysez et examinez les alertes de sécurité.  

Dans la chronologie Azure ATP, sélectionnez une entité de votre réseau (contrôleur de domaine, ordinateur ou utilisateur) comme point d’accès de filtre. Ensuite, sélectionnez le type de filtre : **Alerte de sécurité**, **Type d’activité** ou toute combinaison. Une fois le filtre appliqué, la chronologie des menaces de l’entité est mise à jour avec les informations filtrées. Vous pouvez aussi télécharger les alertes et les activités filtrées pour poursuivre l’examen ou le suivi dans d’autres outils. 

![Filtrer les alertes et les activités](./media/activities-filter.png)

Pour filtrer les alertes et les activités :
 1. Sélectionnez l’entité à examiner dans la chronologie d’Azure ATP. 
 2. Cliquez sur **Filtrer par**, puis sélectionnez les alertes et/ou les activités à filtrer. 
 3. Cliquez sur **Appliquer**. La chronologie de l’entité est mise à jour en fonction des filtres que vous avez sélectionnés. 
 4. Pour télécharger les activités filtrées, cliquez sur **Télécharger des activités**, puis sélectionnez la période sur laquelle porte votre rapport de téléchargement. 
 5. Pour réinitialiser la chronologie de l’entité et afficher toutes les alertes et activités, cliquez sur **Réinitialiser** ou fermez le filtre. 


## <a name="see-also"></a>Voir aussi
- [Examen des entités](investigate-entity.md)
- [Alertes d’intégrité](health-alerts.md)
- [Utilisation d’alertes de sécurité](working-with-suspicious-activities.md)
- [Consultez le forum ATP !](https://aka.ms/azureatpcommunity)
