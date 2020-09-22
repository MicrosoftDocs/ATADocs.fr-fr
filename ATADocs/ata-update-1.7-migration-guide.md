---
title: Mise à jour d’Advanced Threat Analytics vers le Guide de migration 1,7
description: Procédures pour mettre à jour ATA vers la version 1.7
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8eefcd45-7a4b-4074-ac5b-1ffc48e6654a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4772e9cbb1e00e4bb1a4bebd5cc6e2b7821766dc
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90909883"
---
# <a name="ata-update-to-17-migration-guide"></a>Mise à jour d’ATA vers la version 1.7 : guide de migration

[!INCLUDE [Rebranding notice](includes/rebranding.md)]
La mise à jour vers ATA 1.7 comprend des améliorations dans les domaines suivants :

- Nouvelles détections

- Détections existantes plus efficaces
  

## <a name="updating-ata-to-version-17"></a>Mise à jour d’ATA vers la version 1.7

> [!NOTE] 
> Si ATA n’est pas installé dans votre environnement, téléchargez la version complète d’ATA, qui comprend la version 1,7 et suivez la procédure d’installation standard décrite dans [installer ATA](install-ata-step1.md).

Si vous avez déjà déployé la version 1.6 d’ATA, cette procédure vous guide tout au long des étapes nécessaires pour mettre à jour votre déploiement.

> [!NOTE] 
> Vous ne pouvez pas installer ATA version 1.7 directement sur ATA version 1.4 ou 1.5. Vous devez d’abord installer ATA version 1.6. 

Suivez ces étapes pour mettre à jour ATA vers la version 1.7 :

1.  [Télécharger la mise à jour vers la version 1.7](https://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
Dans cette version, le même fichier d’installation (Microsoft ATA Center Setup.exe) est utilisé pour l’installation d’un nouveau déploiement d’ATA et la mise à niveau des déploiements existants.

1. Mettez à jour le centre ATA.

1. Mettez à jour les passerelles ATA.

    > [!IMPORTANT]
    > Pour assurer le bon fonctionnement d’ATA, mettez à jour toutes les passerelles.

### <a name="step-1-update-the-ata-center"></a>Étape 1 : mettre à jour le centre ATA

1. Sauvegardez votre base de données (facultatif) :

    - Si le centre ATA s’exécute en tant que machine virtuelle et que vous souhaitez effectuer un point de contrôle, commencez par arrêter la machine virtuelle.

    - Si le centre ATA s’exécute sur un serveur physique, suivez la procédure recommandée pour [sauvegarder MongoDB](https://docs.mongodb.org/manual/core/backups/).

1. Exécutez le fichier d’installation, **Microsoft ATA Center Setup.exe**, puis suivez les instructions à l’écran pour installer la mise à jour.

    - Dans la page **Bienvenue**, sélectionnez votre langue, puis cliquez sur **Suivant**.

    - Si vous n’avez pas activé les mises à jour automatiques dans la version 1.6, vous êtes invité à configurer ATA pour utiliser Microsoft Update afin de rester à jour.  Dans la page Microsoft Update, sélectionnez **utiliser Microsoft Update lorsque je recherche des mises à jour (recommandé)**.
    ![Image montrant comment maintenir ATA à jour](media/ata_ms_update.png) Ainsi, Windows est configuré de manière à récupérer les mises à jour des autres produits Microsoft (notamment ATA), comme illustré ci-après. 
     ![Image de mise à jour automatique de Windows](media/ata_installupdatesautomatically.png)

    - Dans l’écran **Migration des données**, indiquez si vous souhaitez migrer tout ou une partie des données. Si vous choisissez de migrer uniquement des données partielles, vos profils de comportement et de trafic réseau capturés précédemment ne seront pas migrés. Cela signifie qu’il faudra trois semaines avant que la détection d’un comportement anormal ait un profil complet pour activer la détection d’activité anormale. Pendant ces trois semaines, toutes les autres détections ATA fonctionnent correctement. L’installation de la migration des données **Partielle** prend beaucoup moins de temps. Si vous sélectionnez la migration des données **Complète**, l’installation peut prendre beaucoup plus de temps. La durée estimée et l’espace disque requis, qui sont répertoriés dans l’écran **Migration des données**, dépendent de la quantité de trafic de réseau capturée, précédemment enregistrée dans les versions précédentes d’ATA. Avant de sélectionner **Partielle** ou **Complète**, veillez à vérifier ces exigences.  
    
    ![Migration des données ATA](media/migration-data-migration17.png)

    - Cliquez sur **Update**. Une fois que vous avez cliqué sur Mettre à jour, ATA passe en mode hors connexion jusqu’à la fin de la mise à jour.

1. Une fois la mise à jour du centre ATA terminée, cliquez sur **Lancer** pour afficher l’écran **Mettre à jour** dans la console ATA pour les passerelles ATA.
    ![Écran de réussite de mise à jour](media/migration-center-success17.png)

1. Dans l’écran **Mises à jour**, si vous avez déjà configuré vos passerelles ATA pour une mise à jour automatique, elles sont mises à jour à ce stade. Sinon, cliquez sur **Mettre à jour** en regard de chaque passerelle ATA.
  ![Image de mise à jour des passerelles](media/migration-update-gw-17.png)

  
> [!IMPORTANT] 
> Pour assurer le bon fonctionnement d’ATA, mettez à jour toutes les passerelles.
> Le port d’écoute Syslog configuré sur toutes les passerelles sera modifié : il s’agira du port 514.
 
> [!NOTE] 
> Pour installer de nouvelles passerelles ATA, accédez à l’écran **passerelles** et cliquez sur **Télécharger la configuration** de la passerelle pour obtenir le package d’installation ATA 1,7 et suivez les instructions pour l’installation de la nouvelle passerelle, comme décrit à l' [étape 4. Installez la passerelle ATA](install-ata-step4.md).



## <a name="see-also"></a>Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
