---
title: Définition de notifications Microsoft Defender pour Identity
description: Explique comment définir des alertes de sécurité Microsoft Defender pour Identity pour recevoir une notification en cas de détection d’activités suspectes.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3eb687b716ce69bb4be0aabc2b128b1cf46242ff
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847137"
---
# <a name="set-product-long-notifications"></a>Définition de notifications [!INCLUDE [Product long](includes/product-long.md)]

[!INCLUDE [Product long](includes/product-long.md)] peut envoyer une notification en cas de détection d’une activité suspecte en émettant une alerte de sécurité ou d’intégrité par e-mail.

Pour recevoir des notifications à une adresse e-mail spécifique, définissez les paramètres suivants :

1. Sur le portail [!INCLUDE [Product short](includes/product-short.md)], sélectionnez l’option Paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône Paramètres de configuration [!INCLUDE [Product short](includes/product-short.md)]](media/config-menu.png)

1. Cliquez sur **Notifications**.
1. Sous **Notifications par e-mail**, ajoutez des adresses e-mail pour les notifications que vous voulez recevoir. Elles peuvent être envoyées pour de nouvelles alertes (activités suspectes) et de nouveaux problèmes d’intégrité.

    > [!NOTE]
    >
    > - Les e-mails sont envoyés uniquement pour les notifications avec des adresses e-mail définies.
    > - Les alertes par e-mail pour les activités suspectes sont envoyées uniquement lors de la création de l’activité suspecte.

1. Cliquez sur **Save**.

    ![Notifications [!INCLUDE [Product short](includes/product-short.md)]](media/notifications.png)

## <a name="see-also"></a>Voir aussi

- [Configurer la collecte d’événements](configure-event-collection.md)

- [Définir les paramètres de Syslog](setting-syslog.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
