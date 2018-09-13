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
ms.openlocfilehash: 080b3469c862d4063db5a4832f63dd3614905fac
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166055"
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

5. Cliquez sur **Save**.

 ![Notifications Azure ATP](media/atp-notifications.png)



## <a name="see-also"></a>Voir aussi

- [Configurer la collecte d’événements](configure-event-collection.md)

- [Définir les paramètres de Syslog](setting-syslog.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)