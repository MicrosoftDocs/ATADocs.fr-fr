---
title: Microsoft Defender pour le filtrage et les stratégies d’activité d’identité dans Microsoft Cloud App Security
description: Vue d’ensemble de Microsoft Defender pour le filtrage et les stratégies d’activité d’identité avec Microsoft Cloud App Security.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 5956ebfb9904465e876a21b918255f44ec651ae9
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544247"
---
# <a name="use-activity-filters-and-create-action-policies-with-product-long-in-microsoft-cloud-app-security"></a>Utilisez les filtres d’activité et créez des stratégies d’action avec [!INCLUDE [Product long](includes/product-long.md)] dans Microsoft Cloud App Security

Cet article est conçu pour vous aider à comprendre comment filtrer et créer des stratégies d’action pour les [!INCLUDE [Product short](includes/product-short.md)] activités à l’aide de Microsoft Cloud App Security.

Pour plus d’informations sur la façon d’effectuer votre intégration, consultez [ [!INCLUDE [Product short](includes/product-short.md)] intégration avec Cloud App Security](/cloud-app-security/aatp-integration).

L’utilisation [!INCLUDE [Product short](includes/product-short.md)] de avec Microsoft Cloud App Security offre une analyse des activités et des alertes basées sur l’analyse du comportement des utilisateurs et des entités (UEBA), l’identification des comportements de riskiest dans votre entreprise, la fourniture d’un score de priorité d’investigation complet, ainsi que le filtrage d’activité et les stratégies d’activité personnalisables.

## <a name="prerequisites"></a>Configuration requise

Pour bénéficier de l’ensemble des fonctionnalités d’examen utilisateur dans l’environnement hybride, les éléments suivants sont nécessaires :

- Une licence valide pour Microsoft Cloud App Security
- Une licence valide pour [!INCLUDE [Product long](includes/product-long.md)] la connexion à votre instance Active Directory

>[!NOTE]
>Si vous n’avez pas d’abonnement pour Cloud App Security, vous pouvez utiliser le portail Cloud App Security pour examiner les [!INCLUDE [Product short](includes/product-short.md)] alertes et les recherches approfondies sur les utilisateurs et leurs activités gérées sur site. Toutefois, les informations relatives à vos applications de Cloud restent indisponibles.

## <a name="filter-product-short-activities-in-cloud-app-security"></a>Filtrer les [!INCLUDE [Product short](includes/product-short.md)] activités dans Cloud App Security

[!INCLUDE [Product short](includes/product-short.md)] les activités sont accessibles à partir du menu principal Cloud App Security **examiner** en sélectionnant le sous-menu **Journal d’activité** , ou à partir du menu **alertes** par État, catégorie, gravité, application, nom d’utilisateur ou stratégie.

Pour accéder aux [!INCLUDE [Product short](includes/product-short.md)] activités par utilisateur :

1. Filtrez la file d'attente **Alertes** à l’aide du champ USER NAME (nom d’utilisateur).
    ![Filtrer les alertes par nom d’utilisateur](media/mcas-alerts-queue.png)
1. Cliquez sur le nom d’utilisateur d’une alerte dans la liste résultante pour ouvrir la **Page utilisateur** de l’utilisateur que vous souhaitez examiner.

1. Filtrez les activités de l’utilisateur à l’aide des champs disponibles, ou ajoutez une nouvelle règle de filtre à l’aide du bouton +.
    ![Filtrer les activités de l’utilisateur](media/mcas-activity-filter.png)

## <a name="create-activity-policies-in-cloud-app-security"></a>Créer des stratégies d’activité dans Cloud App Security

Après avoir filtré des activités et identifié des stratégies d’activité que vous souhaitez peut-être mettre en œuvre, ou une non-conformité au sein de votre organisation, utilisez l’option **Créer une stratégie d’activité** dans le menu de filtre pour créer immédiatement une stratégie personnalisée pour chaque utilisateur, appareil ou locataire.

Pour créer une stratégie d’activité :

1. À partir d’une page **Journal d’activité** quelconque, appliquez un filtre (application, nom d’utilisateur, type d’activité, etc.).
    - Pour filtrer les activités à partir de [!INCLUDE [Product short](includes/product-short.md)] , sélectionnez l’option **Active Directory** dans le filtre d’application.
    ![Créez une stratégie d’activité](media/mcas-create-new-policy.png)
1. Cliquez sur le bouton **Nouvelle stratégie à partir de la recherche**.
1. Ajoutez un **Nom de stratégie**.
    ![Créez une stratégie d’activité -étape 2](media/mcas-create-policy.png)
1. Ajoutez une **Description** de la stratégie.
1. Affectez la **gravité** de la stratégie.
1. Sélectionnez une **catégorie** pour la stratégie.
1. Choisissez ou modifiez des filtres pour créer et affecter la stratégie.
1. Affinez ou ajoutez d’autres filtres.
1. Enregistrez et appliquez la nouvelle stratégie.

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur le scoring de priorité d’examen et les fonctionnalités supplémentaires de [Microsoft Cloud App Security](/cloud-app-security/).

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter de [!INCLUDE [Product short](includes/product-short.md)] et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté [!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) !