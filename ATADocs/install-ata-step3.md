---
title: Installer Advanced Threat Analytics - Étape 3 | Microsoft Docs
description: La troisième étape de la procédure d’installation d’ATA vous aide à télécharger le package d’installation de la passerelle ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d49770f435985027690ddfc05a9359e84841c0ff
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454035"
---
*S’applique à : Advanced Threat Analytics version 1.9*



# <a name="install-ata---step-3"></a>Installer ATA - Étape 3

> [!div class="step-by-step"]
> [« Étape 2](install-ata-step2.md)
> [Étape 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Étape 3. Télécharger le package d’installation de la passerelle ATA
Après avoir configuré les paramètres de connectivité du domaine, vous pouvez télécharger le package d’installation de la passerelle ATA. Elle peut être installée sur un serveur dédié ou sur un contrôleur de domaine. Si vous l’installez sur un contrôleur de domaine, elle est installée en tant que passerelle légère ATA. Pour plus d’informations sur la passerelle légère ATA, consultez [Architecture ATA](ata-architecture.md). 

Cliquez sur **Télécharger l’installation de la passerelle** dans la liste des étapes en haut de la page pour accéder à la page **Passerelles**.

![Paramètres de configuration de la passerelle ATA](media/ATA_1.7-welcome-download-gateway.PNG)

> [!NOTE] 
> Pour accéder ultérieurement à l’écran de configuration de la passerelle, cliquez sur **l’icône de paramètres** (en haut à droite) et sélectionnez **Configuration** puis, sous **Système**, cliquez sur **Passerelles**.  

1.  Cliquez sur **Configuration de la passerelle**.
  ![Télécharger le programme d’installation de la passerelle ATA](media/download-gateway-setup.png)
2.  Enregistrez le package localement.
3.  Copiez le package sur le serveur dédié ou sur le contrôleur de domaine sur lequel vous installez la passerelle ATA. Vous pouvez également ouvrir la console ATA à partir du serveur dédié ou du contrôleur de domaine et ignorer cette étape.

Le fichier zip comprend les fichiers suivants :

-   Programme d’installation de la passerelle ATA

-   Fichier de paramètres de configuration avec les informations requises pour se connecter au centre ATA


> [!div class="step-by-step"]
> [« Étape 2](install-ata-step2.md)
> [Étape 4 »](install-ata-step4.md)


## <a name="related-videos"></a>Vidéos connexes
- [Vue d’ensemble du déploiement ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Sélection du type de passerelle ATA approprié](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Voir aussi
- [Guide de déploiement ATA POC](http://aka.ms/atapoc)
- [Outil de dimensionnement ATA](http://aka.ms/atasizingtool)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](ata-prerequisites.md)
