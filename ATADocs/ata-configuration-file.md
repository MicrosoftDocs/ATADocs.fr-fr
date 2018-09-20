---
title: Exporter et importer la configuration Advanced Threat Analytics | Microsoft Docs
description: Comment exporter et importer la configuration ATA.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3abe18d7da00e5af0373d74db2dc2dc1f91a6fc9
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133308"
---
*S’applique à : Advanced Threat Analytics version 1.9*



# <a name="export-and-import-the-ata-configuration"></a>Exportation et importation d’une configuration ATA
La configuration d’ATA est stockée dans la collection « SystemProfile » dans la base de données.
Cette collection est sauvegardée toutes les 4 heures par le service du centre ATA dans des fichiers nommés **SystemProfile_*timestamp*.json**. Les 300 dernières versions sont stockées.
Ce fichier se trouve dans un sous-dossier appelé **Backup**. À l’emplacement de l’installation d’ATA par défaut, il se trouve ici : *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_* horodatage *.json*. 

**Remarque** : Il est recommandé de sauvegarder ce fichier quelque part quand vous apportez des modifications importantes à ATA.

Il est possible de restaurer tous les paramètres en exécutant la commande suivante :

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Voir aussi
- [Architecture d’ATA](ata-architecture.md)
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

