---
title: Filtrage d’activités et stratégies d’Azure Advanced Threat Protection dans Microsoft Cloud App Security | Microsoft Docs
description: Vue d’ensemble du filtrage des activités Azure ATP et des stratégies avec Microsoft Cloud App Security.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 07/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 397e5a77-2bc7-454c-9fe5-649ebaab16b3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 97d13dc5780e9cf24955644a9e0493a8434f62cd
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75908060"
---
# <a name="use-activity-filters-and-create-action-policies-with-azure-atp-in-microsoft-cloud-app-security"></a>Utiliser des filtres d’activité et créer des stratégies d’action avec Azure ATP dans Microsoft Cloud App Security 

Cet article est conçu pour vous aider à comprendre comment filtrer et créer des stratégies d’action pour les activités d’Azure ATP à l’aide de Microsoft Cloud App Security. 

Pour plus d’informations sur l’exécution de votre intégration, consultez [Intégration d’Azure ATP Cloud App Security](https://docs.microsoft.com/cloud-app-security/aatp-integration/enable-azure-advanced-threat-protection).  

L’utilisation d’Azure ATP avec Microsoft Cloud App Security permet d’analyser les activités et d’émettre des alertes sur la base du comportement des utilisateurs et des entités (UEBA), donc d’identifier les comportements les plus risqués dans votre entreprise et de fournir un indice de priorité complet ainsi qu’un filtrage des activités et des stratégies d’activité personnalisables. 

## <a name="prerequisites"></a>Prérequis

Pour bénéficier de l’ensemble des fonctionnalités d’examen utilisateur dans l’environnement hybride, les éléments suivants sont nécessaires :
- Une licence valide pour Microsoft Cloud App Security
- Licence valide pour Azure ATP connectée à votre instance Active Directory

>[!NOTE]
>Si vous n’avez pas d’abonnement à Cloud App Security, vous pouvez utiliser le portail Cloud App Security pour examiner les alertes Azure ATP et explorer les utilisateurs et leurs activités managées locales. Cependant, les informations connexes de vos applications cloud ne seront toujours pas disponibles.

## <a name="filter-azure-atp-activities-in-cloud-app-security"></a>Filtrer les activités Azure ATP dans Cloud App Security  
 
Les activités ATP Azure sont accessibles à partir du menu principal **Examiner** de Cloud App Security en sélectionnant le sous-menu **Journal d'activité**, ou à partir du menu **Alertes** par état, par catégorie, par gravité, par application, par nom d’utilisateur ou par stratégie.  

Pour accéder aux activités d’Azure ATP par utilisateur :

1. Filtrez la file d'attente **Alertes** à l’aide du champ USER NAME (nom d’utilisateur). 
    ![File d’attente Alertes](media/atp-mcas-alerts-queue.png)
1. Cliquez sur le nom d’utilisateur d’une alerte dans la liste résultante pour ouvrir la **Page utilisateur** de l’utilisateur que vous souhaitez examiner. 
    
1. Filtrez les activités de l’utilisateur à l’aide des champs disponibles, ou ajoutez une nouvelle règle de filtre à l’aide du bouton +.
    ![File d’attente Alertes](media/atp-mcas-activity-filter.png)

## <a name="create-activity-policies-in-cloud-app-security"></a>Créer des stratégies d’activité dans Cloud App Security

Après avoir filtré des activités et identifié des stratégies d’activité que vous souhaitez peut-être mettre en œuvre, ou une non-conformité au sein de votre organisation, utilisez l’option **Créer une stratégie d’activité** dans le menu de filtre pour créer immédiatement une stratégie personnalisée pour chaque utilisateur, appareil ou locataire. 

Pour créer une stratégie d’activité :

1. À partir d’une page **Journal d’activité** quelconque, appliquez un filtre (application, nom d’utilisateur, type d’activité, etc.). 
    - Pour filtrer les activités d’Azure ATP, sélectionnez l’option **Active Directory** dans le filtre d’application. 
    ![Créez une stratégie d’activité](media/atp-mcas-create-new-policy.png)
1. Cliquez sur le bouton **Nouvelle stratégie à partir de la recherche**.    
1. Ajoutez un **Nom de stratégie**. 
    ![Créez une stratégie d’activité -étape 2](media/atp-mcas-create-policy.png)
1. Ajoutez une **Description** de la stratégie.  
1. Affectez la **gravité** de la stratégie.
1. Sélectionnez une **catégorie** pour la stratégie.
1. Choisissez ou modifiez des filtres pour créer et affecter la stratégie.
1. Affinez ou ajoutez d’autres filtres. 
1. Enregistrez et appliquez la nouvelle stratégie.  


## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur le scoring de priorité d’examen et les fonctionnalités supplémentaires de [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/).
  
## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) dès aujourd’hui !




