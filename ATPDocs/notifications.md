---
title: Définir des notifications Azure Advanced Threat Protection
description: Décrit comment définir des alertes de sécurité Azure ATP qui vous notifient quand des activités suspectes sont détectées.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b60044cbc2ccf05ff1802ecce6e3e11d42543f97
ms.sourcegitcommit: dd8435ba20f76a6fc4590980c040c6fc7ec6c62b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91451748"
---
# <a name="set-azure-atp-notifications"></a>Définir des notifications Azure ATP

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Azure ATP peut vous notifier par e-mail quand il détecte une activité suspecte, et qu’il émet une alerte de sécurité ou d’intégrité via un e-mail.

Pour recevoir des notifications à une adresse e-mail spécifique, définissez les paramètres suivants :

1. Dans le portail Azure ATP, sélectionnez l’option Paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône de paramètres de configuration d’Azure ATP](media/atp-config-menu.png)

1. Cliquez sur **Notifications**.
1. Sous **Notifications par e-mail**, ajoutez des adresses e-mail pour les notifications que vous voulez recevoir. Elles peuvent être envoyées pour de nouvelles alertes (activités suspectes) et de nouveaux problèmes d’intégrité.

    > [!NOTE]
    >
    > - Les e-mails sont envoyés uniquement pour les notifications avec des adresses e-mail définies.
    > - Les alertes par e-mail pour les activités suspectes sont envoyées uniquement lors de la création de l’activité suspecte.

1. Cliquez sur **Save**.

    ![Notifications Azure ATP](media/atp-notifications.png)

## <a name="see-also"></a>Voir aussi

- [Configurer la collecte d’événements](configure-event-collection.md)

- [Définir les paramètres de Syslog](setting-syslog.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
