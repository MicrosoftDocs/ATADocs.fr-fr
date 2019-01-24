---
title: Utilisation des journaux d’audit ATA | Microsoft Docs
description: Cet article décrit l’utilisation des journaux d’audit ATA dans le journal des événements Windows.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 630045525ce344920032ef0245692ed9ca5e5ef1
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54839520"
---
# <a name="working-with-ata-audit-logs"></a>Utilisation des journaux d’audit ATA


*S’applique à : Advanced Threat Analytics version 1.9*

Les journaux d’audit ATA sont conservés dans les journaux des événements Windows sous **Applications et services** et **Microsoft ATA** dans les ordinateurs du centre ATA et les passerelles ATA.

Le journal d’audit du centre ATA contient les éléments suivants :
-   Informations sur l’activité suspecte
-   Surveillance des alertes (page d’intégrité)
-   Connexions à de la console ATA
-   Tous les changements de configuration*

Le journal d’audit de la passerelle ATA contient les éléments suivants :
-   Les changements de configuration de la passerelle* 

(Tous les changements de configuration de la passerelle ATA sont configurés dans le centre ATA, mais ils sont toujours audités sur l’ordinateur de la passerelle.)

*Le journal d’audit des changements de configuration contient la configuration précédente et la nouvelle configuration.


## <a name="see-also"></a>Voir aussi
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
