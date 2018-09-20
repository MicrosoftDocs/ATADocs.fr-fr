---
title: Définir des notifications Azure - Protection avancée contre les menaces | Microsoft Docs
description: Décrit comment définir des alertes Azure ATP qui vous notifient quand des activités suspectes sont détectées.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c3fc5adbb700c4b8df66c243a655cf98aacc79af
ms.sourcegitcommit: 9f02f0f6669b25f39b616bb0885bb55b8c4f050b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/19/2018
ms.locfileid: "46362423"
---
*S’applique à : Azure - Protection avancée contre les menaces*


# <a name="set-azure-atp-notifications"></a>Définir des notifications Azure ATP

Azure ATP peut vous notifier par e-mail quand il détecte une activité suspecte ou une alerte d’intégrité. 

Pour recevoir des notifications à une adresse e-mail spécifique, définissez les paramètres suivants :


1. Dans le portail d’espace de travail Azure ATP, sélectionnez l’option de paramètres dans la barre d’outils et sélectionnez **Configuration**.

![Icône de paramètres de configuration d’Azure ATP](media/atp-config-menu.png)

2. Cliquez sur **Notifications**.
3. Sous **Notifications par e-mail**, spécifiez quelles notifications doivent être envoyées par e-mail. Elles peuvent être envoyées pour de nouvelles alertes (activités suspectes) et de nouveaux problèmes d’intégrité. 
 
 >  [!NOTE]
 >   Les alertes par e-mail pour les activités suspectes sont envoyées uniquement lors de la création de l’activité suspecte.
 
4. Cliquez sur **Save**.

 ![Notifications Azure ATP](media/atp-notifications.png)



## <a name="see-also"></a>Voir aussi

- [Configurer la collecte d’événements](configure-event-collection.md)

- [Définir les paramètres de Syslog](setting-syslog.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)
