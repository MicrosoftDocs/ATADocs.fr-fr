---
title: Stratégie de données personnelles de Microsoft Defender for Identity
description: Fournit des liens vers des informations sur la façon de supprimer des informations privées et des données personnelles de Microsoft Defender pour l’identité.
ms.date: 10/26/2020
ms.topic: conceptual
ms.openlocfilehash: b8336d4b6508fc9de462dcdbb6bc6389dd2fa0f2
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533394"
---
# <a name="microsoft-defender-for-identity-data-security-and-privacy"></a>Microsoft Defender pour la sécurité et la confidentialité des données d’identité

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Rechercher et identifier les données personnelles

Dans, [!INCLUDE [Product short](includes/product-short.md)] vous pouvez afficher les données personnelles identifiables à partir du [ [!INCLUDE [Product long](includes/product-long.md)] portail](workspace-portal.md) à l’aide de la [barre de recherche](workspace-portal.md#search-bar).

Recherchez un utilisateur ou un ordinateur spécifique et cliquez sur l’entité pour accéder à la [page de profil](entity-profiles.md) de l’utilisateur ou de l’ordinateur. Le profil vous fournit des informations détaillées sur l’entité à partir d’Active Directory, notamment l’activité réseau liée à cette entité et son historique.

[!INCLUDE [Product short](includes/product-short.md)] les données personnelles sont collectées à partir de Active Directory via le [!INCLUDE [Product short](includes/product-short.md)] capteur et stockées dans une base de données principale.

## <a name="update-personal-data"></a>Mettre à jour les données personnelles

[!INCLUDE [Product short](includes/product-short.md)]les données utilisateur personnelles de l’utilisateur sont dérivées de l’objet de l’utilisateur dans le Active Directory de l’organisation. Par conséquent, les modifications apportées au profil utilisateur dans l’annuaire Active Directory de l’organisation sont reflétées dans [!INCLUDE [Product short](includes/product-short.md)] .

## <a name="delete-personal-data"></a>Supprimer les données personnelles

- Après la suppression d’un utilisateur du Active Directory de l’organisation, [!INCLUDE [Product short](includes/product-short.md)] supprime automatiquement le profil utilisateur et toute activité réseau associée au cours d’une année. Vous pouvez également [supprimer](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) les alertes de sécurité qui contiennent des données personnelles.

- Des autorisations en **lecture seule** sur le conteneur **Objets supprimés** sont recommandées. Pour en savoir plus sur l’utilisation de l’autorisation de conteneur d’objets supprimés par le [!INCLUDE [Product short](includes/product-short.md)] service, consultez la recommandation relative au conteneur objets supprimés dans la section [ [!INCLUDE [Product short](includes/product-short.md)] conditions préalables](prerequisites.md#before-you-start).

## <a name="export-personal-data"></a>Exporter les données personnelles

Dans, [!INCLUDE [Product short](includes/product-short.md)] vous avez la possibilité d' [Exporter](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) les informations d’alerte de sécurité vers Excel. Cette fonction exporte également les données personnelles.

## <a name="audit-personal-data"></a>Effectuer un audit des données personnelles

[!INCLUDE [Product short](includes/product-short.md)] implémente l’audit des modifications de données personnelles, y compris la suppression et l’exportation d’enregistrements de données personnelles. La durée de conservation de la piste d’audit est de 90 jours. L’audit dans [!INCLUDE [Product short](includes/product-short.md)] est une fonctionnalité principale et n’est pas accessible aux clients.

## <a name="additional-resources"></a>Ressources supplémentaires

- Pour plus d’informations sur [!INCLUDE [Product short](includes/product-short.md)] l’approbation et la conformité, consultez le [portail de confiance des services](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) et le site de [conformité Microsoft 365 entreprise RGPD](/microsoft-365/compliance/gdpr?view=o365-worldwide&preserve-view=true).

## <a name="security-and-privacy-for-defender-for-identity-us-government-gcc-high-customers"></a>Sécurité et confidentialité pour Defender pour Identity US Government High Customers

Pour plus d’informations sur [!INCLUDE [Product short](includes/product-short.md)] les normes de conformité et l’emplacement des données client pour les clients des États-Unis, reportez-vous au [Enterprise Mobility + Security pour la description du service US Government](/enterprise-mobility-security/solutions/ems-govt-service-description).
