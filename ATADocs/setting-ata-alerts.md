---
title: Définir des notifications Advanced Threat Analytics
description: Décrit comment définir des alertes ATA afin d’être averti quand des activités suspectes sont détectées.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 38f6fd58bb924b3dec8c03be80594fe93e523770
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84775010"
---
# <a name="set-ata-notifications"></a>Définir des notifications ATA

*S’applique à : Advanced Threat Analytics version 1.9*

ATA peut vous avertir quand il détecte une activité suspecte par e-mail ou en utilisant le transfert d’événements ATA et en transférant l’événement à votre serveur SIEM/syslog. Avant de sélectionner les notifications à recevoir, vous devez [configurer votre serveur de messagerie et votre serveur Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   Les notifications par e-mail incluent un lien qui dirige l’utilisateur directement vers l’activité suspecte qui a été détectée. La partie nom d’hôte du lien provient du paramètre de l’URL de la console ATA dans la page Centre ATA. Par défaut, l’URL de la console ATA est l’adresse IP sélectionnée pendant l’installation du centre ATA. Si vous envisagez de configurer des alertes par e-mail, nous vous recommandons d’utiliser un nom de domaine complet comme URL de la console ATA.
> -   Les notifications sont envoyées à partir du centre ATA vers le serveur SMTP ou le serveur Syslog.


Pour recevoir des notifications, définissez les paramètres suivants :


1. Dans la console ATA, sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.
    
    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.png)
    
1. Sous la section **Notifications et rapports**, sélectionnez **Notifications**.
1. Sous **Notifications par e-mail**, spécifiez quelles notifications doivent être envoyées par e-mail : nouvelles activités suspectes et nouveaux problèmes d’intégrité. Vous pouvez définir une adresse e-mail distincte où envoyer les activités suspectes et pour les alertes d’intégrité, par exemple pour que les notifications d’activité suspecte soient envoyées à votre analyste de sécurité et que vos notifications d’alerte d’intégrité soient envoyées à votre administrateur informatique.
    
    > [!NOTE]
    > Les alertes par courrier électronique pour les activités suspectes sont envoyées uniquement lors de la création de l’activité suspecte.

1. Sous **notifications syslog**, spécifiez les notifications à envoyer à votre serveur Syslog : nouvelles activités suspectes, activités suspectes mises à jour et nouveaux problèmes d’intégrité.
1. Cliquez sur **Enregistrer**.
    
    ![Image des paramètres de notification par e-mail ATA](media/ata-mail-notification-settings.png)




## <a name="see-also"></a>Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
