---
title: Définition de notifications Microsoft Defender pour Identity
description: Explique comment définir des alertes de sécurité Microsoft Defender pour Identity pour recevoir une notification en cas de détection d’activités suspectes.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: ad02fab44b76fc9d30af59a331ec5243796224d5
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533645"
---
# <a name="set-microsoft-defender-for-identity-notifications"></a>Définition de notifications Microsoft Defender pour Identity

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
