---
title: Installer Advanced Threat Analytics - Étape 4 | Microsoft Docs
description: La quatrième étape de la procédure d’installation d’ATA vous aide à installer la passerelle ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b36275bfec9d34c0d4af9a3a935bd032e886d57d
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674858"
---
# <a name="install-ata---step-4"></a>Installer ATA - Étape 4

*S’applique à : Advanced Threat Analytics version 1.9*

> [!div class="step-by-step"]
> [« Étape 3](install-ata-step3.md)
> [Étape 5 »](install-ata-step5.md)

## <a name="step-4-install-the-ata-gateway"></a>Étape 4. Installer la passerelle ATA

Avant d’installer la passerelle ATA sur un serveur dédié, vérifiez que la mise en miroir des ports est correctement configurée et que la passerelle ATA peut voir le trafic à destination et en provenance des contrôleurs de domaine. Pour plus d’informations, consultez [Valider la mise en miroir des ports](validate-port-mirroring.md).


> [!IMPORTANT]
> Vérifiez que le correctif [KB2919355](http://support.microsoft.com/kb/2919355/) a été installé.  Exécutez l’applet de commande PowerShell suivante pour vérifier si le correctif est installé :
>
> `Get-HotFix -Id kb2919355`

Effectuez les opérations suivantes sur le serveur de la passerelle ATA.

1. Extrayez les fichiers à partir du fichier zip. 
   > [!NOTE] 
   > L’installation directe à partir du fichier zip est vouée à l’échec.
    
2. Exécutez **Microsoft ATA Gateway Setup.exe**, puis suivez les instructions de l’Assistant Installation.
    
3. Dans la page **Bienvenue**, sélectionnez votre langue, puis cliquez sur **Suivant**.
    
4. L’Assistant Installation vérifie automatiquement si le serveur est un contrôleur de domaine ou un serveur dédié. S’il s’agit d’un contrôleur de domaine, la passerelle légère ATA est installée. S’il s’agit d’un serveur dédié, la passerelle ATA est installée. 
    
   Par exemple, pour une passerelle ATA, l’écran suivant s’affiche pour vous informer qu’une passerelle ATA sera installée sur votre serveur dédié :
    
   ![Installation d’une passerelle ATA](media/ata-gw-install.png) Cliquez sur **Suivant**.
    
   > [!NOTE] 
   > Si le contrôleur de domaine ou le serveur dédié ne dispose pas de la configuration matérielle minimale requise pour l’installation, un avertissement s’affiche. Il ne vous empêche pas de cliquer sur **Suivant** et de procéder à l’installation. Cela peut être le bon choix pour l’installation d’ATA dans un petit environnement de test de laboratoire dans lequel vous n’avez pas besoin d’autant de place pour le stockage des données. Pour les environnements de production, nous vous recommandons fortement de respecter le guide de [planification de la capacité](ata-capacity-planning.md) ATA pour vous assurer que vos contrôleurs de domaine ou serveurs dédiés répondent aux conditions requises.
    
5. Sous **Configurer la passerelle**, entrez les informations suivantes en fonction de votre environnement :
    
   ![Image de la configuration de la passerelle ATA](media/ata-gw-configure.png)
    
   > [!NOTE]
   > Quand vous déployez la passerelle ATA, vous ne devez pas fournir les informations d’identification. Si l’installation de la passerelle ATA ne parvient pas à récupérer vos informations d’identification à l’aide de l’authentification unique (par exemple, cela peut se produire si le centre ATA n’est pas dans le domaine, si la passerelle ATA n’est pas dans le domaine ou si vous n’avez pas les informations d’identification de l’administrateur d’ATA), vous devez fournir les informations d’identification, comme dans l’écran suivant : 
   
    ![Fournir les informations d’identification de la passerelle ATA](media/ata-install-credentials.png)
   
    - Chemin d’installation : il s’agit de l’emplacement où est installée la passerelle ATA. L’emplacement par défaut est %programfiles%\Microsoft Advanced Threat Analytics\Gateway. Conservez la valeur par défaut.
   
6. Cliquez sur **Installer**. Les composants suivants sont installés et configurés pendant l’installation de la passerelle ATA :
    
    -   KB 3047154 (pour Windows Server 2012 R2 uniquement)
    
        > [!IMPORTANT]
        > -   N’installez pas le correctif KB 3047154 sur un hôte de virtualisation (l’hôte responsable de la virtualisation, que vous pouvez exécuter sur une machine virtuelle), car cela pourrait nuire au bon fonctionnement de la mise en miroir des ports. 
        > -   N’installez pas l’Analyseur de message, Wireshark ou tout autre logiciel de capture réseau sur la passerelle ATA. Si vous souhaitez capturer le trafic réseau, installez et utilisez le Moniteur réseau Microsoft version 3.4.
    
    -   Service de passerelle ATA
    -   Microsoft Visual C++ 2013 Redistributable
    -   Jeu d’éléments de collecte de données de l’Analyseur de performances personnalisé
    
7. Une fois l’installation terminée : pour la passerelle ATA, cliquez sur **Lancer** pour ouvrir votre navigateur et vous connecter à la console ATA ; pour la passerelle légère ATA, cliquez sur **Terminer**.


> [!div class="step-by-step"]
> [« Étape 3](install-ata-step3.md)
> [Étape 5 »](install-ata-step5.md)


## <a name="related-videos"></a>Vidéos connexes
- [Vue d’ensemble du déploiement ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Sélection du type de passerelle ATA approprié](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Voir aussi
- [Guide de déploiement ATA POC](http://aka.ms/atapoc)
- [Outil de dimensionnement ATA](http://aka.ms/atasizingtool)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](ata-prerequisites.md)

