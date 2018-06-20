---
title: Exporter et importer la configuration Advanced Threat Analytics | Microsoft Docs
description: Comment exporter et importer la configuration ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: edbf553bf48d984f4864264643d197362c3d6042
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010497"
---
*S’applique à : Advanced Threat Analytics version 1.9*



# <a name="export-and-import-the-ata-configuration"></a>Exportation et importation d’une configuration ATA
La configuration d’ATA est stockée dans la collection « SystemProfile » dans la base de données.
Cette collection est sauvegardée toutes les heures par le service du centre ATA dans des fichiers nommés **SystemProfile_*timestamp*.json**. Les 10 dernières versions sont stockées.
Ce fichier se trouve dans un sous-dossier appelé **Backup**. À l’emplacement de l’installation d’ATA par défaut, il se trouve ici : *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_* horodatage *.json*. 

**Remarque** : Il est recommandé de sauvegarder ce fichier quelque part quand vous apportez des modifications importantes à ATA.

Il est possible de restaurer tous les paramètres en exécutant la commande suivante :

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Voir aussi
- [Architecture d’ATA](ata-architecture.md)
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

