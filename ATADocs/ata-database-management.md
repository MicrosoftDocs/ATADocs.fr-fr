---
title: Gestion de base de données Advanced Threat Analytics
description: Procédures pour vous aider à déplacer, sauvegarder ou restaurer la base de données ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c1d26afbb9121e9c8516ded5d50ad08accea8f17
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90909216"
---
# <a name="ata-database-management"></a>Gestion de la base de données ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Si vous voulez déplacer, sauvegarder ou restaurer la base de données ATA, suivez ces procédures pour MongoDB.

## <a name="backing-up-the-ata-database"></a>Sauvegarde de la base de données ATA
Reportez-vous à la [documentation MongoDB pertinente](http://docs.mongodb.org/manual/administration/backup/).

## <a name="restoring-the-ata-database"></a>Restauration de la base de données ATA
Reportez-vous à la [documentation MongoDB pertinente](http://docs.mongodb.org/manual/administration/backup/).

## <a name="moving-the-ata-database-to-another-drive"></a>Déplacement de la base de données ATA vers un autre lecteur

1. Arrêtez le service **Microsoft Advanced Threat Analytics Center**.
   > [!Important] 
   > Assurez-vous que le service ATA Center est arrêté avant de passer à l’étape suivante.

1. Arrêtez le service **MongoDB**.

1. Ouvrez le fichier de configuration Mongo situé par défaut à l’emplacement suivant : C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

   Trouvez le paramètre `storage: dbPath`.

1. Déplacez le dossier indiqué dans le paramètre `dbPath` vers le nouvel emplacement.

1. Remplacez le paramètre `dbPath` du fichier de configuration mongo par le nouveau chemin de dossier, puis enregistrez et fermez le fichier.

    ![Modifier l’image de configuration MongoDB](media/ATA-mongoDB-moveDB.png)

1. Démarrez le service **MongoDB** .

1. Démarrez le service **Microsoft Advanced Threat Analytics Center**.

## <a name="see-also"></a>Voir aussi
- [Architecture ATA](ata-architecture.md)
- [Configuration requise pour ATA](ata-prerequisites.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

