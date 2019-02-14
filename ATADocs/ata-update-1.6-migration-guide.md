---
title: Mise à jour d’Advanced Threat Analytics vers la version 1.6 - Guide de migration | Microsoft Docs
description: Procédures pour mettre à jour ATA vers la version 1.6
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 0756ef64-3aef-4a69-8981-24fa8f285c6a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1d3e0cd545a932daae71fa4242abb43b4dc15bae
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077692"
---
# <a name="ata-update-to-16-migration-guide"></a>Mise à jour d’ATA vers la version 1.6 : guide de migration
La mise à jour vers ATA 1.6 comprend des améliorations dans les domaines suivants :

-   Nouvelles détections

-   Détections existantes plus efficaces

-   Passerelle légère ATA

-   Mises à jour automatiques

-   Performances accrues du centre ATA

-   Réduction des besoins de stockage

-   Prise en charge d’IBM QRadar

## <a name="updating-ata-to-version-16"></a>Mise à jour d’ATA vers la version 1.6
> [!NOTE] 
> Si ATA n’est pas installé dans votre environnement, téléchargez la version complète d’ATA qui inclut la version 1.6. Suivez ensuite la procédure d’installation standard décrite dans [Installer ATA](install-ata-step1.md).

Si vous avez déjà déployé la version 1.5 d’ATA, cette procédure vous guide tout au long des étapes nécessaires pour mettre à jour votre déploiement.

> [!NOTE] 
> Vous ne pouvez pas installer ATA version 1.6 directement sur ATA version 1.4. Vous devez d’abord installer ATA version 1.5. Si vous tentez par erreur d’installer ATA 1.6 sans installer ATA 1.5 au préalable, vous recevez un message d’erreur indiquant qu’**une version plus récente est déjà installée sur votre machine.** Vous devez désinstaller les éléments d’ATA 1.6 qui restent sur votre machine, même si l’installation a échoué, avant d’installer ATA version 1.5.

Suivez ces étapes pour mettre à jour ATA vers la version 1.6 :

1. Pour éviter les problèmes de mise à niveau, veillez à suivre les étapes 8 à 10 de **Échec de la migration en cas de mise à jour à partir d’ATA 1.6** dans [Nouveautés ATA version 1.6](whats-new-version-1.6.md).
2. Assurez-vous d’avoir assez d’espace libre pour terminer la mise à niveau. Vous pouvez effectuer l’installation jusqu’à la vérification de la disponibilité pour avoir une estimation de la quantité d’espace libre dont vous avez besoin, puis redémarrer la mise à niveau après avoir alloué l’espace disque nécessaire.
1.  [Télécharger la mise à jour vers la version 1.6](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
Dans cette version, le même fichier d’installation (Microsoft ATA Center Setup.exe) est utilisé pour l’installation d’un nouveau déploiement d’ATA et la mise à niveau des déploiements existants.

2.  Mettez à jour le centre ATA.

3.  Téléchargez le package mis à jour de la passerelle ATA.

4.  Mettez à jour les passerelles ATA.

    > [!IMPORTANT]
    > Pour assurer le bon fonctionnement d’ATA, mettez à jour toutes les passerelles.

### <a name="step-1-update-the-ata-center"></a>Étape 1 : Mettez à jour le centre ATA.

1.  Sauvegardez votre base de données (facultatif) :

    -   Si le centre ATA s’exécute en tant que machine virtuelle et que vous souhaitez effectuer un point de contrôle, commencez par arrêter la machine virtuelle.

    -   Si le centre ATA s’exécute sur un serveur physique, suivez la procédure recommandée pour [sauvegarder MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Exécutez le fichier d’installation, Microsoft ATA Center Setup.exe, puis suivez les instructions à l’écran pour installer la mise à jour.

    1.  ATA 1.6 requiert l’installation du .NET Framework 4.6.1. Si ce n’est déjà fait, la procédure d’installation d’ATA installe .Net Framework 4.6.1 dans le cadre de l’installation.
    
        > [!NOTE] 
        > L’installation de .Net Framework 4.6.1 peut nécessiter le redémarrage du serveur. L’installation d’ATA se poursuit une fois le serveur redémarré.
    
    2.  Dans la page **Bienvenue**, sélectionnez votre langue, puis cliquez sur **Suivant**.

    3.  Lisez le Contrat de Licence Utilisateur Final et, si vous en acceptez les termes, cliquez sur **Suivant**.

    4.  Vous pouvez désormais utiliser Microsoft Update pour qu’ATA reste à jour.  Dans la page Microsoft Update, sélectionnez **Utiliser Microsoft Update lorsque je recherche des mises à jour (recommandé)**.
    ![Image montrant comment maintenir ATA à jour](media/ata_ms_update.png) Ainsi, Windows est configuré de manière à récupérer les mises à jour des autres produits Microsoft (notamment ATA), comme illustré ci-après. 
     ![Image de mise à jour automatique de Windows](media/ata_installupdatesautomatically.png)

    5.  Avant le début de l’installation, ATA effectue une vérification de la disponibilité. Examinez les résultats de la vérification pour vérifier que les composants requis sont correctement configurés et que vous disposez de l’espace disque minimal. 
    ![Image de vérification de la disponibilité d’ATA](media/ata_install_readinesschecks.png)

    6.  Cliquez sur **Mettre à jour**. Une fois que vous avez cliqué sur Mettre à jour, ATA passe en mode hors connexion jusqu’à la fin de la mise à jour.

3.  Une fois le centre ATA mis à jour, les passerelles ATA indiquent qu’elles sont obsolètes.

    ![Image des passerelles obsolètes](media/ATA-center-outdated.png)

> [!IMPORTANT] 
> Pour assurer le bon fonctionnement d’ATA, mettez à jour toutes les passerelles.

### <a name="step-2-download-the-ata-gateway-setup-package"></a>Étape 2. Télécharger le package d’installation de la passerelle ATA
Après avoir configuré les paramètres de connectivité du domaine, vous pouvez télécharger le package d’installation de la passerelle ATA.

Pour télécharger le package d’installation de la passerelle ATA :

1.  Supprimez les versions précédemment téléchargées du package de la passerelle ATA.

2.  Sur la machine de la passerelle ATA, ouvrez un navigateur et entrez l’adresse IP de la console ATA que vous avez configurée dans le centre ATA. Une fois la console ATA ouverte, cliquez sur l’icône des paramètres et sélectionnez **Configuration**.

    ![Icône des paramètres de configuration](media/ATA-config-icon.png)

3.  Sous l’onglet **Passerelles ATA**, cliquez sur **Télécharger l’installation de la passerelle ATA**.

4.  Enregistrez le package localement.

Le fichier zip comprend les fichiers suivants :

-   Programme d’installation de la passerelle ATA

-   Fichier de paramètres de configuration avec les informations requises pour se connecter au centre ATA

### <a name="step-3-update-the-ata-gateways"></a>Étape 3 : Mettez à jour les passerelles ATA.

1.  Sur chaque passerelle ATA, extrayez les fichiers du package de passerelle ATA et exécutez le fichier **Microsoft ATA Gateway Setup.exe**.

    > [!NOTE] 
    > Vous pouvez également utiliser ce package pour installer de nouvelles passerelles ATA.

2.  Vos paramètres précédents sont conservés, mais le redémarrage du service peut prendre quelques minutes.

3.  Répétez cette étape pour toutes les autres passerelles ATA déployées.

> [!NOTE] 
> Une fois la passerelle ATA mise à jour avec succès, la notification d’obsolescence de cette passerelle ATA est résolue.

Si toutes les passerelles ATA indiquent qu’elles ont été synchronisées avec succès et que le message signalant l’existence d’un package de passerelle ATA mis à jour ne s’affiche plus, vous savez que toutes les passerelles ATA ont été correctement mises à jour.

![Image des passerelles mises à jour](media/ATA-gw-updated.png)


## <a name="see-also"></a>Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
