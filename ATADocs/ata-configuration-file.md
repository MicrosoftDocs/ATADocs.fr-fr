---
title: Exporter et importer la configuration Advanced Threat Analytics | Microsoft Docs
description: Comment exporter et importer la configuration ATA.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b1b0c23547783b9cdb671dda35acf7cb8689f64b
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076383"
---
# <a name="export-and-import-the-ata-configuration"></a>Exportation et importation d’une configuration ATA

*S’applique à : Advanced Threat Analytics version 1.9*

La configuration d’ATA est stockée dans la collection « SystemProfile » dans la base de données.
Cette collection est sauvegardée toutes les quatre heures par le service du centre ATA dans des fichiers nommés : **SystemProfile_*timestamp*.json**. Les 300 dernières versions sont stockées.
Ce fichier se trouve dans un sous-dossier appelé **Backup**. Dans l'emplacement d'installation d’ATA par défaut, il s’agit de :  <em>C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_</em>timestamp<em>.json</em>. 

**Remarque** : Il est recommandé de sauvegarder ce fichier quelque part quand vous apportez des modifications importantes à ATA.

Il est possible de restaurer tous les paramètres en exécutant la commande suivante :

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Voir aussi
- [Architecture d’ATA](ata-architecture.md)
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

