---
title: Définir des notifications Azure - Protection avancée contre les menaces | Microsoft Docs
description: Décrit comment définir des alertes de sécurité Azure ATP qui vous notifient quand des activités suspectes sont détectées.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 79368731bcfef923466d566f06fe775ebf1caeac
ms.sourcegitcommit: e783df4c9d928fedf6dc3c65d58d9b530cdd2ff2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49800035"
---
*S’applique à : Azure Advanced Threat Protection*


# <a name="set-azure-atp-notifications"></a>Définir des notifications Azure ATP

Azure ATP peut vous notifier par e-mail quand il détecte une activité suspecte, et qu’il émet une alerte de sécurité ou d’intégrité via un e-mail. 

Pour recevoir des notifications à une adresse e-mail spécifique, définissez les paramètres suivants :


1. Dans le portail Azure ATP, sélectionnez l’option Paramètres dans la barre d’outils, puis **Configuration**.

 ![Icône de paramètres de configuration d’Azure ATP](media/atp-config-menu.png)

2. Cliquez sur **Notifications**.
3. Sous **Notifications par e-mail**, spécifiez quelles notifications doivent être envoyées par e-mail. Elles peuvent être envoyées pour de nouvelles alertes (activités suspectes) et de nouveaux problèmes d’intégrité. 
 
 > [!NOTE]
 > Les alertes par e-mail pour les activités suspectes sont envoyées uniquement lors de la création de l’activité suspecte.
 
4. Cliquez sur **Save**.

 ![Notifications Azure ATP](media/atp-notifications.png)



## <a name="see-also"></a>Voir aussi

- [Configurer la collecte d’événements](configure-event-collection.md)

- [Définir les paramètres de Syslog](setting-syslog.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
