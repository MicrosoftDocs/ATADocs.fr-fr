---
title: Définition des paramètres Syslog dans Microsoft Defender pour Identity
description: Explique comment indiquer à Microsoft Defender pour Identity d’envoyer une notification (par e-mail ou par transfert d’événements Defender pour Identity) en cas de détection d’activités suspectes.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 55487b6638fc8278ae94b3444f74f2abe2b2dc56
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275247"
---
# <a name="integrate-with-syslog"></a>Intégrer à Syslog

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE]
> Les fonctionnalités [!INCLUDE [Product long](includes/product-long.md)] décrites sur cette page sont également accessibles sur le nouveau [portail](https://portal.cloudappsecurity.com).

[!INCLUDE [Product long](includes/product-long.md)] peut vous informer en cas de détection d’activités suspectes en envoyant des alertes de sécurité et d’intégrité à votre serveur Syslog par le biais d’un capteur désigné.

Une fois que vous avez activé les notifications Syslog, vous pouvez définir les éléments suivants :

|Champ|Description|
|---------|---------------|
|capteur|Sélectionnez un capteur désigné comme responsable de l’agrégation de tous les événements Syslog et de leur transfert vers votre serveur SIEM.|
|Point de terminaison de service|Nom de domaine complet du serveur Syslog et modifiez éventuellement le numéro de port (par défaut, 514)|
|Transport|Peut être UDP, TCP ou TLS (Syslog sécurisé)|
|Format|Format utilisé par [!INCLUDE [Product short](includes/product-short.md)] pour envoyer des événements au serveur SIEM : RFC 5424 ou RFC 3164.|

1. Avant de configurer les notifications Syslog, collaborez avec votre administrateur SIEM pour connaître les informations suivantes :

    - Nom de domaine complet ou adresse IP du serveur SIEM
    - Port sur lequel écoute le serveur SIEM
    - Mode de transport à utiliser : UDP, TCP ou TLS (Syslog sécurisé)
    - Format sous lequel envoyer les données, RFC 3164 ou 5424

1. Ouvrez le portail [!INCLUDE [Product short](includes/product-short.md)].
1. Cliquez sur **Paramètres**.
1. Dans le sous-menu **Notifications et rapports** , sélectionnez **Notifications**.
1. Dans l’option **Service Syslog** , cliquez sur **Configurer**.
1. Sélectionnez le **Capteur**.
1. Entrez l’URL du **Point de terminaison de service**.
1. Sélectionnez le protocole de **Transport** (TCP ou UDP).
1. Sélectionnez le format (RFC 3164 ou RFC 5424).
1. Sélectionnez **Envoyer un message de test à syslog** , puis vérifiez que le message est reçu dans votre solution d’infrastructure Syslog.
1. Cliquez sur **Save**.

Pour passer en revue ou modifier vos paramètres Syslog.

1. Cliquez sur **Notifications** , puis, sous **Notifications Syslog** , cliquez sur **Configurer** et entrez les informations suivantes :

    ![Image Paramètres du serveur Syslog [!INCLUDE [Product short](includes/product-short.md)]](media/syslog.png)

1. Vous pouvez sélectionner les événements à envoyer à votre serveur Syslog. Sous **Notifications Syslog** , spécifiez quelles notifications doivent être envoyées à votre serveur Syslog : nouvelles alertes de sécurité, alertes de sécurité mises à jour et nouveaux problèmes d’intégrité.

> [!NOTE]
> Si vous envisagez de créer une automatisation ou des scripts pour les journaux SIEM [!INCLUDE [Product short](includes/product-short.md)], nous vous recommandons d’utiliser le champ **externalId** pour identifier le type d’alerte au lieu d’utiliser le nom d’alerte à cet effet. Les noms d’alerte peuvent parfois être modifiés alors que l’ **externalId** de chaque alerte est définitif. Pour plus d’informations, consultez [Informations de référence sur les journaux SIEM [!INCLUDE [Product short](includes/product-short.md)]](cef-format-sa.md).

## <a name="see-also"></a>Voir aussi

- [Utilisation de comptes sensibles](sensitive-accounts.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
