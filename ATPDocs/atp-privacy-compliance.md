---
title: Stratégie relative aux données personnelles Azure - Protection avancée contre les menaces | Microsoft Docs
description: Fournit des liens vers des informations sur la suppression des informations personnelles et des données personnelles à partir d’Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/15/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: e4aad8af65c27f351185808585aea37a8a67de42
ms.sourcegitcommit: 121c49d559e71741136db1626455b065e8624ff9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/20/2018
ms.locfileid: "41734615"
---
*S’applique à : Azure Advanced Threat Protection*

# <a name="azure-atp-data-security-and-privacy"></a>Sécurité et confidentialité des données Azure ATP

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Rechercher et identifier les données personnelles 

Dans Azure - Protection avancée contre les menaces, vous pouvez afficher les données personnelles identifiables à partir du [portail de l’espace de travail](workspace-portal.md) à l’aide de la [barre de recherche](workspace-portal.md#search-bar). 

Recherchez un utilisateur ou un ordinateur spécifique et cliquez sur l’entité pour accéder à la [page de profil](entity-profiles.md) de l’utilisateur ou de l’ordinateur. Le profil vous fournit des informations détaillées sur l’entité à partir d’Active Directory, notamment l’activité réseau liée à cette entité et son historique.

Les données personnelles Azure ATP sont recueillies à partir d’Active Directory par le biais du capteur Azure ATP et stockées dans une base de données principale.

## <a name="update-personal-data"></a>Mettre à jour les données personnelles 

Les données utilisateur personnelles d’Azure ATP sont dérivées de l’objet utilisateur dans Active Directory de l’organisation. Par conséquent, les modifications apportées au profil utilisateur dans l’AD de l’organisation sont répercutées dans Azure ATP.


## <a name="delete-personal-data"></a>Supprimer les données personnelles 

Si un utilisateur est supprimé de l’annuaire Active Directory de l’organisation, Azure ATP supprime automatiquement le profil utilisateur et toute activité réseau associée pour une période d’une année. Vous pouvez également [supprimer](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) les alertes de sécurité qui contiennent des données personnelles. 

## <a name="export-personal-data"></a>Exporter les données personnelles 

Dans Azure ATP, il est possible [d’exporter](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) les informations relatives aux alertes de sécurité dans Excel. Cette fonction exporte également les données personnelles. 
 
## <a name="audit-personal-data"></a>Effectuer un audit des données personnelles

Azure ATP implémente l’audit des modifications des données personnelles, notamment la suppression et l’exportation d’enregistrements de données personnelles. La durée de conservation de la piste d’audit est de 90 jours. L’audit dans Azure ATP est une fonctionnalité back-end non accessible aux clients.
 
## <a name="additional-resources"></a>Ressources supplémentaires

- Pour plus d’informations sur l’approbation et la conformité dans Azure ATP, consultez le [portail Service Trust](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) et le [site sur la conformité RGPD de Microsoft 365 Entreprise](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
