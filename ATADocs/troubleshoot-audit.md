---
title: Utilisation des journaux d’audit ATA
description: Cet article décrit l’utilisation des journaux d’audit ATA dans le journal des événements Windows.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 14f818e8149e239f8c7b88487b4fb388ad557458
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910819"
---
# <a name="working-with-ata-audit-logs"></a>Utilisation des journaux d’audit ATA


[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Les journaux d’audit ATA sont conservés dans les journaux des événements Windows sous **Applications et services** et **Microsoft ATA** dans les ordinateurs du centre ATA et les passerelles ATA.

Le journal d’audit du centre ATA contient les éléments suivants :
- Informations sur l’activité suspecte
- Alertes d’intégrité (page d’intégrité)
- Connexions à de la console ATA
- Tous les changements de configuration*

Le journal d’audit de la passerelle ATA contient les éléments suivants :
- Les changements de configuration de la passerelle* 

(Tous les changements de configuration de la passerelle ATA sont configurés dans le centre ATA, mais ils sont toujours audités sur l’ordinateur de la passerelle.)

*Le journal d’audit des changements de configuration contient la configuration précédente et la nouvelle configuration.


## <a name="see-also"></a>Voir aussi
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
