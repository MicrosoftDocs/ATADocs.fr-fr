---
title: Récupération d’urgence pour Advanced Threat Analytics
description: Décrit comment vous pouvez récupérer rapidement les fonctionnalités ATA après un sinistre
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/02/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 578e8ecdd598b404c570d41e71d487cf798cb602
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690786"
---
# <a name="ata-disaster-recovery"></a>Récupération d’urgence d’ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Cet article décrit comment récupérer rapidement votre centre ATA et restaurer les fonctionnalités ATA quand le centre ATA a cessé de fonctionner, mais que les passerelles ATA fonctionnent encore. 

>[!NOTE]
> Le processus décrit ne récupère pas les activités suspectes détectées précédemment, mais rétablit le fonctionnement intégral du centre ATA. En outre, la période d’apprentissage nécessaire pour certaines détections de comportements redémarre, la majeure partie de la détection offerte par ATA étant néanmoins opérationnelle une fois le centre ATA restauré. 

## <a name="back-up-your-ata-center-configuration"></a>Sauvegarder votre configuration du centre ATA

1. La configuration du centre ATA est sauvegardée dans un fichier toutes les 4 heures. Recherchez la dernière copie de sauvegarde de la configuration du centre ATA et enregistrez-la sur un ordinateur distinct. Pour obtenir une explication complète de la localisation de ces fichiers, consultez [Exporter et importer la configuration ATA](ata-configuration-file.md). 
1. Exportez le certificat du centre ATA.
    1. Dans le gestionnaire de certificats, accédez à **certificats (ordinateur local)**  ->  **Personal**  -> **certificats** personnels, puis sélectionnez **Centre ATA**.
    2. Cliquez avec le bouton droit sur **Centre ATA** et sélectionnez **Toutes les tâches** puis **Exportation**. 
     ![Certificat du centre ATA](media/ata-center-cert.png)
    3. Suivez les instructions pour exporter le certificat, en veillant à exporter également la clé privée.
    4. Sauvegardez le fichier de certificat exporté sur un ordinateur distinct.

   > [!NOTE] 
   > Si vous ne pouvez pas exporter la clé privée, vous devez créer un nouveau certificat et le déployer sur ATA, comme décrit dans [Changer le certificat du centre ATA](modifying-ata-center-configuration.md), puis l’exporter. 

## <a name="recover-your-ata-center"></a>Récupérer votre centre ATA

1. Créez un ordinateur Windows Server en utilisant la même adresse IP et le même nom d’ordinateur que l’ordinateur du centre ATA précédent.
1. Importez le certificat que vous avez sauvegardé précédemment, sur le nouveau serveur.
1. Suivez les instructions pour [déployer le centre ATA](install-ata-step1.md) sur le serveur Windows qui vient d’être créé. Il est inutile de redéployer les passerelles ATA. Lorsque vous êtes invité à fournir un certificat, fournissez le certificat que vous avez exporté lors de la sauvegarde de la configuration du centre ATA. 
![Restauration du centre ATA](media/disaster-recovery-deploymentss.png)
1. Arrêtez le service du centre ATA.
1. Importez la configuration sauvegardée du centre ATA :
    1. Supprimez le document du profil système du centre ATA par défaut dans MongoDB : 
        1. Accédez à **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Exécutez `mongo.exe ATA` 
        3. Exécutez cette commande pour supprimer le profil système par défaut : `db.SystemProfile.remove({})`
        4. Quittez l’interpréteur de commandes Mongo et revenez à l’invite de commandes en entrant : `exit`
    2. Exécutez la commande : `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert` en utilisant le fichier de sauvegarde de l’étape 1.</br>
    Pour obtenir une explication complète de la localisation et de l’importation des fichiers de sauvegarde, consultez [Exporter et importer la configuration ATA](ata-configuration-file.md). 
    3. Démarrez le service du centre ATA.
    4. Ouvrez la console ATA. Vous devez normalement voir toutes les passerelles ATA liées sous l’onglet Configuration/Passerelles.
    5. Veillez à définir un [**utilisateur des services d’annuaire**](install-ata-step2.md) et à choisir un [**synchronisateur de contrôleur de domaine**](install-ata-step5.md). 






## <a name="see-also"></a>Voir aussi
- [Configuration requise pour ATA](ata-prerequisites.md)
- [Planification de la capacité ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](install-ata-step6.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
