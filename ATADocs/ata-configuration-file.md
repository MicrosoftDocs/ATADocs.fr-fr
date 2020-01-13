---
title: Exporter et importer la configuration Advanced Threat Analytics | Microsoft Docs
description: Comment exporter et importer la configuration ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 522c4e197a52c6ccbd40d7ab1e8dea1764bce275
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75905418"
---
# <a name="export-and-import-the-ata-configuration"></a>Exportation et importation d’une configuration ATA

*S’applique à : Advanced Threat Analytics version 1.9*

La configuration d’ATA est stockée dans la collection « SystemProfile » dans la base de données.
Cette collection est sauvegardée toutes les 4 heures par le service du centre ATA dans des fichiers nommés **SystemProfile_*timestamp*.json**. Les 300 dernières versions sont stockées.
Ce fichier se trouve dans un sous-dossier nommé **Backup**. À l’emplacement de l’installation d’ATA par défaut, il se trouve ici : <em>C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_</em>horodatage<em>.json</em>. 

**Remarque** : Il est recommandé de sauvegarder ce fichier quelque part quand vous apportez des modifications importantes à ATA.

Il est possible de restaurer tous les paramètres en exécutant la commande suivante :

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Voir aussi
- [Architecture d’ATA](ata-architecture.md)
- [Configuration requise pour ATA](ata-prerequisites.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

