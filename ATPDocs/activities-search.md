---
title: Filtre et recherche d’activités surveillées Azure-protection avancée contre les menaces
description: Cet article offre une vue d’ensemble du filtrage et de la recherche d’activités supervisées à l’aide d’Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/15/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a546703b-d5a9-404d-9e87-125523bb8421
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 12826a5af178122698cb05725f867914ed3cf775
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912081"
---
# <a name="azure-atp-monitored-activities-search-and-filter"></a>Recherche et filtrage d’activités supervisées dans Azure ATP 

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE]
> Les fonctionnalités Azure ATP expliquées dans cette page sont également accessibles dans le nouveau [portail](https://portal.cloudappsecurity.com).

Les activités détectées par Azure ATP sur votre réseau peuvent faire l’objet de recherches et de filtrages pour en faciliter l’exploration et l’organisation pendant que vous analysez et examinez les alertes de sécurité.  

Dans la chronologie Azure ATP, sélectionnez une entité de votre réseau (contrôleur de domaine, ordinateur ou utilisateur) comme point d’accès de filtre. Ensuite, sélectionnez le type de filtre : **Alerte de sécurité**, **Type d’activité** ou toute combinaison. Une fois le filtre appliqué, la chronologie des menaces de l’entité est mise à jour avec les informations filtrées. Vous pouvez aussi télécharger les alertes et les activités filtrées pour poursuivre l’examen ou le suivi dans d’autres outils. 

![Filtrer les alertes et les activités](media/activities-filter.png)

Pour filtrer les alertes et les activités :
 1. Sélectionnez l’entité à examiner dans la chronologie d’Azure ATP. 
 2. Cliquez sur **Filtrer par**, puis sélectionnez les alertes et/ou les activités à filtrer. 
 3. Cliquez sur **Appliquer**. La chronologie de l’entité est mise à jour en fonction des filtres que vous avez sélectionnés. 
 4. Pour télécharger les activités filtrées, cliquez sur **Télécharger des activités**, puis sélectionnez la période sur laquelle porte votre rapport de téléchargement. 
 5. Pour réinitialiser la chronologie de l’entité et afficher toutes les alertes et activités, cliquez sur **Réinitialiser** ou fermez le filtre. 


## <a name="see-also"></a>Voir aussi
- [Examen des entités](investigate-entity.md)
- [Alertes d’intégrité](health-alerts.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)
