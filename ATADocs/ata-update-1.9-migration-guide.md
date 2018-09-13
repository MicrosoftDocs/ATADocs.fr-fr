---
title: Mise à jour d’Advanced Threat Analytics vers la version 1.9 - Guide de migration | Microsoft Docs
description: Procédures de mise à jour d’ATA vers la version 1.9
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 03/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: bd96cf2b2048aa37e559649d15565c3244684e35
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44165997"
---
# <a name="updating-ata-to-version-19"></a>Mise à jour d’ATA vers la version 1.9

> [!NOTE] 
> Si ATA n’est pas installé dans votre environnement, téléchargez la version complète d’ATA qui inclut la version 1.9. Suivez ensuite la procédure d’installation standard décrite dans [Installer ATA](install-ata-step1.md).

Si vous avez déjà déployé la version 1.8 d’ATA, cette procédure vous guide tout au long des étapes nécessaires pour mettre à jour votre déploiement.

> [!NOTE] 
>  Seuls ATA version 1.8 (1.8.6645) et ATA 1.8 Update 1 (1.8.6765) peuvent être mis à jour vers ATA version 1.9, les versions précédentes d’ATA ne peuvent pas être directement mises à jour vers la version 1.9.

Suivez ces étapes pour mettre à jour ATA vers la version 1.9 :

1.  [Téléchargez la version mise à jour d’ATA 1.9 à partir du Centre de téléchargement](https://www.microsoft.com/download/details.aspx?id=56725) ou la version complète à partir du [Centre d’évaluation](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
Dans la version de migration, le fichier peut être utilisé uniquement pour la mise à jour d’ATA 1.8. Dans la version du Centre d’évaluation, le même fichier d’installation (Microsoft ATA Center Setup.exe) est utilisé pour l’installation d’un nouveau déploiement d’ATA et la mise à niveau des déploiements existants.

2.  Mettez à jour le centre ATA.

4.  Mettez à jour les passerelles ATA.

    > [!IMPORTANT]
    > Pour assurer le bon fonctionnement d’ATA, mettez à jour toutes les passerelles.

### <a name="step-1-update-the-ata-center"></a>Étape 1 : mettre à jour le centre ATA

1.  Sauvegardez votre base de données (facultatif) :

    -   Si le centre ATA s’exécute en tant que machine virtuelle et que vous souhaitez effectuer un point de contrôle, commencez par arrêter la machine virtuelle.

    -   Si le centre ATA est en cours d’exécution sur un serveur physique, consultez l’article [Récupération d’urgence](disaster-recovery.md) pour plus d’informations sur la sauvegarde de la base de données.

2.  Exécutez le fichier d’installation, **Microsoft ATA Center Setup.exe**, puis suivez les instructions à l’écran pour installer la mise à jour.

    -  Dans la page **Bienvenue**, choisissez votre langue et cliquez sur **Suivant**.

    -  Si vous n’avez pas activé les mises à jour automatiques dans la version 1.8, vous êtes invité à configurer ATA pour utiliser Microsoft Update afin de rester à jour.  Dans la page Microsoft Update, sélectionnez **Utiliser Microsoft Update lorsque je recherche des mises à jour (recommandé)**.
    ![Image montrant comment maintenir ATA à jour](media/ata_ms_update.png)
     
     Ceci ajuste les paramètres Windows pour activer les mises à jour pour ATA. 
    
    -  L’écran **Migration de données partielle** vous permet de savoir que le trafic réseau capturé précédemment, les entités, les événements et la détection liés aux données sont supprimés. Toutes les détections fonctionnent immédiatement, à l’exception de la détection de comportement anormal, la modification anormale d’un groupe, la Reconnaissance à l’aide des services d’annuaire (SAM-R) et les détections de passage à une version antérieure de chiffrement qui prennent jusqu'à trois semaines pour créer un profil complet après le temps d’apprentissage nécessaire. 
     
      ![Migration partielle d’ATA](media/partial-migration.png)

    -  Cliquez sur **Mettre à jour**. Une fois que vous avez cliqué sur Mettre à jour, ATA passe en mode hors connexion jusqu’à la fin de la mise à jour.

4.  Une fois la mise à jour du centre ATA terminée, cliquez sur **Lancer** pour afficher l’écran **Mettre à jour** dans la console ATA pour les passerelles ATA.

     ![Écran de réussite de mise à jour](media/migration-center-success.png)

5.  Dans l’écran **Mises à jour**, si vous avez déjà configuré vos passerelles ATA pour une mise à jour automatique, elles sont mises à jour à ce stade. Sinon, cliquez sur **Mettre à jour** en regard de chaque passerelle ATA.
  
     ![Image de mise à jour des passerelles](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Pour assurer le bon fonctionnement d’ATA, mettez à jour toutes les passerelles.
 
> [!NOTE] 
> Pour installer de nouvelles passerelles ATA, accédez à l’écran **Passerelles** et cliquez sur **Télécharger le programme d’installation de la passerelle** pour obtenir le package d’installation ATA 1.9 et suivre les instructions d’installation de la nouvelle passerelle, comme décrit dans [Étape 4. Installer la passerelle ATA](install-ata-step4.md).


## <a name="see-also"></a>Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
