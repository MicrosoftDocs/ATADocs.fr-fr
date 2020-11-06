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
ms.openlocfilehash: 1cb2ea1c5f853f6f3a56d4bcccd84b5958078329
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275575"
---
# <a name="set-product-long-notifications"></a>Définition de notifications [!INCLUDE [Product long](includes/product-long.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[!INCLUDE [Product long](includes/product-long.md)] peut envoyer une notification en cas de détection d’une activité suspecte en émettant une alerte de sécurité ou d’intégrité par e-mail.

Pour recevoir des notifications à une adresse e-mail spécifique, définissez les paramètres suivants :

1. Sur le portail [!INCLUDE [Product short](includes/product-short.md)], sélectionnez l’option Paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône Paramètres de configuration [!INCLUDE [Product short](includes/product-short.md)]](media/config-menu.png)

1. Cliquez sur **Notifications**.
1. Sous **Notifications par e-mail** , ajoutez des adresses e-mail pour les notifications que vous voulez recevoir. Elles peuvent être envoyées pour de nouvelles alertes (activités suspectes) et de nouveaux problèmes d’intégrité.

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
