---
title: Microsoft Defender pour l’identité dans Microsoft Cloud App Security
description: Vue d’ensemble de Microsoft Defender pour les fonctionnalités d’identité dans Microsoft Cloud App Security.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/05/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 70a316deaafec0c251c91defbc47ec5281eba617
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848871"
---
# <a name="using-product-long-with-microsoft-cloud-app-security"></a>Utilisation [!INCLUDE [Product long](includes/product-long.md)] de avec Microsoft Cloud App Security

Cet article est conçu pour vous aider à comprendre et à naviguer dans l’expérience d’investigation améliorée lors de l’utilisation du portail Microsoft Cloud App Security avec [!INCLUDE [Product long](includes/product-long.md)] .

En tirant parti des détections sur site existantes et de l’analytique de comportement anormal, l’accès [!INCLUDE [Product short](includes/product-short.md)] à l’aide du portail Microsoft Cloud App Security offre la possibilité de détecter et d’alerter les données sensibles dans l’ensemble de votre entreprise, ainsi que de filtrer les activités et de créer des stratégies exploitables. Cette solution hybride analyse l’activité et les alertes sur la base de l’analyse du comportement des utilisateurs et des entités (UEBA) pour identifier des comportements à risque et fournit un indice de priorité d’examen afin de rationaliser votre réponse incidente concernant des identités compromises.

Dans cet article, vous apprendrez ce qui suit :

> [!div class="checklist"]
>
> - Présentation du service
> - Nouvelles façons d’accéder à [!INCLUDE [Product short](includes/product-short.md)]
> - Conditions préalables à la gestion des licences
> - Où trouver les [!INCLUDE [Product short](includes/product-short.md)] activités suivies dans Cloud App Security

## <a name="service-overview"></a>Présentation du service

En s’intégrant à [!INCLUDE [Product short](includes/product-short.md)] , le portail Cloud App Security fournit des alertes et des informations à partir des éléments suivants :

- Microsoft Cloud App Security, qui identifie les attaques au sein d'une session cloud, couvrant non seulement les produits Microsoft mais aussi les applications tierces
- [!INCLUDE [Product long](includes/product-long.md)], qui utilise Machine Learning et l’analyse comportementale pour identifier les attaques sur votre réseau local
- Azure Active Directory Identity Protection, qui détecte et prévient de manière proactive les risques pouvant affecter les identités dans le cloud au niveau des utilisateurs et des connexions

## <a name="access-product-short"></a>Accéder [!INCLUDE [Product short](includes/product-short.md)]

Choisissez de continuer à utiliser [!INCLUDE [Product short](includes/product-short.md)] dans le [!INCLUDE [Product short](includes/product-short.md)] portail, ou vous pouvez accéder aux [!INCLUDE [Product short](includes/product-short.md)] alertes et au score d’identité à l’aide du portail Microsoft Cloud App Security. Dans l’un ou l’autre flux de travail, [!INCLUDE [Product short](includes/product-short.md)] les tâches d’installation et de configuration continuent à être gérées dans le [!INCLUDE [Product short](includes/product-short.md)] portail.

## <a name="prerequisites"></a>Configuration requise

Pour bénéficier de l’ensemble des fonctionnalités d’examen utilisateur dans l’environnement hybride, les éléments suivants sont nécessaires :

- Une licence valide pour Microsoft Cloud App Security
- Une licence valide pour [!INCLUDE [Product long](includes/product-long.md)] la connexion à votre instance Active Directory

>[!NOTE]
>
> - Si vous n’avez pas d’abonnement pour Cloud App Security, vous serez toujours en mesure d’utiliser le portail Cloud App Security pour examiner les [!INCLUDE [Product short](includes/product-short.md)] alertes et les recherches approfondies sur les utilisateurs et leurs activités gérées sur site, mais vous ne recevrez pas d’informations pertinentes de vos applications Cloud.
> - [!INCLUDE [Product short](includes/product-short.md)] les administrateurs peuvent avoir besoin de nouvelles autorisations pour accéder à Cloud App Security. Pour savoir comment attribuer des autorisations à Cloud App Security, consultez [Gérer l’accès administrateur](/cloud-app-security/manage-admins).

Consultez [ [!INCLUDE [Product short](includes/product-short.md)] intégration](/cloud-app-security/mdi-integration) pour savoir comment activer rapidement [!INCLUDE [Product short](includes/product-short.md)] dans Cloud App Security.

## <a name="product-short-in-cloud-app-security"></a>[!INCLUDE [Product short](includes/product-short.md)] dans Cloud App Security

Consultez le [démarrage rapide de Cloud App Security](/cloud-app-security/getting-started-with-cloud-app-security) pour vous familiariser avec les principes fondamentaux de l’utilisation du portail Cloud App Security.

Accédez à vos [!INCLUDE [Product short](includes/product-short.md)] données et à de nouvelles fonctionnalités hybrides dans Cloud App Security des alertes, des activités et des pages utilisateur.

## <a name="alerts"></a>Alertes

[!INCLUDE [Product short](includes/product-short.md)] les alertes s’affichent dans la file d’attente des **alertes** Cloud App Security. Des options de filtrage d’alertes supplémentaires sont disponibles uniquement lorsque les alertes sont affichées avec Cloud App Security. [!INCLUDE [Product short](includes/product-short.md)] les alertes sont filtrées à l’aide du filtre d’application pour **Active Directory**.

## <a name="alert-management"></a>Gestion des alertes

Lorsque [!INCLUDE [Product short](includes/product-short.md)] vous utilisez avec Cloud App Security, la fermeture des alertes dans un service ne les ferme pas automatiquement dans l’autre service. Décidez où gérer et corriger les alertes pour éviter la duplication des efforts.

## <a name="siem-notification"></a>Notification SIEM

Si vos services ( [!INCLUDE [Product short](includes/product-short.md)] et Cloud App Security) sont actuellement configurés pour envoyer des notifications d’alerte à un serveur Siem après l’activation [!INCLUDE [Product short](includes/product-short.md)] de l’intégration dans Cloud App Security, vous commencerez à recevoir des notifications Siem dupliquées pour la même alerte. Chaque service émet une alerte avec un ID d’alerte différent. Pour éviter la duplication et la confusion, décidez où vous souhaitez gérer les alertes, puis configurez l’autre service pour ne plus envoyer de notifications SIEM.

## <a name="activities"></a>Activités

[!INCLUDE [Product short](includes/product-short.md)] les alertes sont affichées dans le **Journal d’activité** Cloud App Security. Des options et fonctionnalités de filtrage d’activité supplémentaires sont disponibles uniquement lorsque les alertes sont affichées avec Cloud App Security. Consultez [ [!INCLUDE [Product short](includes/product-short.md)] activités à l’aide de Microsoft Cloud App Security](activities-filtering-mcas.md) pour savoir comment filtrer et créer des stratégies d’activité.

## <a name="user-pages"></a>Pages utilisateur

Les pages utilisateur contiennent l’[indice de priorité d’examen](/cloud-app-security/tutorial-ueba) de chaque utilisateur et un journal d’activité de toutes les actions.

Pour accéder à une page utilisateur d’un utilisateur système :

1. Ouvrez **Alertes** dans le menu principal.
1. Sélectionnez et filtrez la file d’attente des alertes pour un utilisateur spécifique à l’aide du champ **Nom d’utilisateur**.

 or

1. À partir du menu **Examiner**, sélectionnez **Journal d’activité**.
1. Filtrez la file d’attente du journal d’activité par utilisateur.

    ![Journal d’activité](media/mcas-activity-filter.png)

## <a name="next-steps"></a>Étapes suivantes

Consultez [ [!INCLUDE [Product short](includes/product-short.md)] activités à l’aide de Microsoft Cloud App Security](activities-filtering-mcas.md) pour savoir comment filtrer et créer des stratégies d’activité.

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter de [!INCLUDE [Product short](includes/product-short.md)] et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté [!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) !
