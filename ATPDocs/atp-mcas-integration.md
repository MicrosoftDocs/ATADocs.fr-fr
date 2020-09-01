---
title: Azure Advanced Threat Protection dans Microsoft Cloud App Security
description: Vue d’ensemble des fonctionnalités d’Azure ATP dans Microsoft Cloud App Security.
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
ms.openlocfilehash: cc76b68971ae780e90260f198d0745a29719ca45
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88955358"
---
# <a name="using-azure-atp-with-microsoft-cloud-app-security"></a>Utilisation d’Azure ATP avec Microsoft Cloud App Security

Cet article est conçu pour vous aider à comprendre et à parcourir l’expérience d’examen améliorée lorsque vous utilisez le portail Microsoft Cloud App Security avec Azure ATP.

En tirant parti des détections d’attaques locales existantes et de l’analyse du comportement, l’accès à Azure ATP à l’aide du portail Microsoft Cloud App Security permet également de détecter l’exfiltration de données sensibles dans votre entreprise, de donner l’alerte ainsi que de filtrer les activités et de créer des stratégies exploitables. Cette solution hybride analyse l’activité et les alertes sur la base de l’analyse du comportement des utilisateurs et des entités (UEBA) pour identifier des comportements à risque et fournit un indice de priorité d’examen afin de rationaliser votre réponse incidente concernant des identités compromises.

Dans cet article, vous apprendrez ce qui suit :

> [!div class="checklist"]
>
> - Présentation du service
> - Nouvelles façons d’accéder à Azure ATP
> - Conditions préalables à la gestion des licences
> - Où trouver les activités suivies par Azure ATP dans Cloud App Security

## <a name="service-overview"></a>Présentation du service

Intégré dans Azure ATP, le portail Cloud App Security émet des alertes et fournit des informations à partir de :

- Microsoft Cloud App Security, qui identifie les attaques au sein d'une session cloud, couvrant non seulement les produits Microsoft mais aussi les applications tierces
- Azure Advanced Threat Protection, qui utilise le Machine Learning et l'analyse comportementale pour identifier les attaques sur votre réseau local
- Azure Active Directory Identity Protection, qui détecte et prévient de manière proactive les risques pouvant affecter les identités dans le cloud au niveau des utilisateurs et des connexions

## <a name="access-azure-atp"></a>Accéder à Azure ATP

Vous pouvez choisir de continuer à utiliser Azure ATP dans le portail Azure ATP, ou d’accéder aux alertes Azure ATP et aux indices d’identité à l’aide du portail Microsoft Cloud App Security. Dans les deux cas, les tâches de paramétrage et de configuration d’Azure ATP continuent à être gérées dans le portail Azure ATP.

## <a name="prerequisites"></a>Configuration requise

Pour bénéficier de l’ensemble des fonctionnalités d’examen utilisateur dans l’environnement hybride, les éléments suivants sont nécessaires :

- Une licence valide pour Microsoft Cloud App Security
- Licence valide pour Azure ATP connectée à votre instance Active Directory

>[!NOTE]
>
> - Si vous n’avez pas d’abonnement à Cloud App Security, vous pourrez continuer à utiliser le portail Cloud App Security pour examiner les alertes Azure ATP et explorer les utilisateurs et leurs activités managées locales, mais vous ne recevrez pas d’informations connexes de vos applications cloud.
> - Les administrateurs Azure ATP peuvent avoir besoin de nouvelles autorisations pour accéder à Cloud App Security. Pour savoir comment attribuer des autorisations à Cloud App Security, consultez [Gérer l’accès administrateur](/cloud-app-security/manage-admins).

Consultez [Intégration d’Azure ATP](/cloud-app-security/aatp-integration) pour apprendre à activer rapidement Azure ATP dans Cloud App Security.

## <a name="azure-atp-in-cloud-app-security"></a>Azure ATP dans Cloud App Security

Consultez le [démarrage rapide de Cloud App Security](/cloud-app-security/getting-started-with-cloud-app-security) pour vous familiariser avec les principes fondamentaux de l’utilisation du portail Cloud App Security.

Accédez à vos données Azure ATP et à de nouvelles fonctionnalités hybrides au sein des alertes, des activités et des pages utilisateur de Cloud App Security.

## <a name="alerts"></a>Alerts

Les alertes Azure ATP sont affichées dans la file d'attente **Alertes** de Cloud App Security. Des options de filtrage d’alertes supplémentaires sont disponibles uniquement lorsque les alertes sont affichées avec Cloud App Security. Les alertes Azure ATP sont filtrées avec le filtre d’application pour **Active Directory**.

## <a name="alert-management"></a>Gestion des alertes

Quand vous utilisez Azure ATP avec Cloud App Security, le fait de fermer des alertes dans un service ne les ferme pas automatiquement dans l’autre service. Décidez où gérer et corriger les alertes pour éviter la duplication des efforts.

## <a name="siem-notification"></a>Notification SIEM

Si vos deux services (Azure ATP et Cloud App Security) sont actuellement configurés pour envoyer des notifications d’alerte à un SIEM, vous commencerez à recevoir des notifications SIEM en double pour la même alerte une fois l’intégration d’Azure ATP activée dans Cloud App Security. Chaque service émet une alerte avec un ID d’alerte différent. Pour éviter la duplication et la confusion, décidez où vous souhaitez gérer les alertes, puis configurez l’autre service pour ne plus envoyer de notifications SIEM.

## <a name="activities"></a>Activités

Les alertes Azure ATP sont affichées dans le **journal d'activité** de Cloud App Security. Des options et fonctionnalités de filtrage d’activité supplémentaires sont disponibles uniquement lorsque les alertes sont affichées avec Cloud App Security. Consultez [Activités Azure ATP à l’aide de Microsoft Cloud App Security](atp-activities-filtering-mcas.md) pour apprendre à filtrer et à créer des stratégies d’activité.

## <a name="user-pages"></a>Pages utilisateur

Les pages utilisateur contiennent l’[indice de priorité d’examen](/cloud-app-security/tutorial-ueba) de chaque utilisateur et un journal d’activité de toutes les actions.

Pour accéder à une page utilisateur d’un utilisateur système :
1. Ouvrez **Alertes** dans le menu principal.
1. Sélectionnez et filtrez la file d’attente des alertes pour un utilisateur spécifique à l’aide du champ **Nom d’utilisateur**.

 or

1. À partir du menu **Examiner**, sélectionnez **Journal d’activité**.
1. Filtrez la file d’attente du journal d’activité par utilisateur.

    ![Journal d’activité](media/atp-mcas-activity-filter.png)

## <a name="next-steps"></a>Étapes suivantes

Consultez [Activités Azure ATP à l’aide de Microsoft Cloud App Security](atp-activities-filtering-mcas.md) pour apprendre à filtrer et à créer des stratégies d’activité.

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) dès aujourd’hui !