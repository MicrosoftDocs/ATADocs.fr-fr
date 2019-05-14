---
title: Gestion de la base de données Advanced Threat Analytics | Microsoft Docs
description: Procédures pour vous aider à déplacer, sauvegarder ou restaurer la base de données ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e2e57f5816ff1f250ba04cddb65848b31673a71e
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196335"
---
# <a name="ata-database-management"></a>Gestion de la base de données ATA

*S’applique à : Advanced Threat Analytics version 1.9*

Si vous voulez déplacer, sauvegarder ou restaurer la base de données ATA, suivez ces procédures pour MongoDB.

## <a name="backing-up-the-ata-database"></a>Sauvegarde de la base de données ATA
Reportez-vous à la [documentation MongoDB correspondante](http://docs.mongodb.org/manual/administration/backup/).

## <a name="restoring-the-ata-database"></a>Restauration de la base de données ATA
Reportez-vous à la [documentation MongoDB correspondante](http://docs.mongodb.org/manual/administration/backup/).

## <a name="moving-the-ata-database-to-another-drive"></a>Déplacement de la base de données ATA vers un autre lecteur

1. Arrêtez le service **Microsoft Advanced Threat Analytics Center**.
   > [!Important] 
   > Assurez-vous que le service ATA Center est arrêté avant de passer à l’étape suivante.

2. Arrêtez le service **MongoDB**.

3. Ouvrez le fichier de configuration Mongo situé par défaut à l’emplacement suivant : C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

   Trouvez le paramètre `storage: dbPath`.

4. Déplacez le dossier indiqué dans le paramètre `dbPath` vers le nouvel emplacement.

5. Remplacez le paramètre `dbPath` du fichier de configuration mongo par le nouveau chemin de dossier, puis enregistrez et fermez le fichier.

   ![Modifier l’image de configuration MongoDB](media/ATA-mongoDB-moveDB.png)

6. Démarrez le service **MongoDB**.

7. Démarrez le service **Microsoft Advanced Threat Analytics Center**.

## <a name="see-also"></a>Voir aussi
- [Architecture d’ATA](ata-architecture.md)
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

