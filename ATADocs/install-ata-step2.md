---
title: Installer Advanced Threat Analytics-étape 2
description: La deuxième étape de la procédure d’installation d’ATA vous aide à configurer les paramètres de connectivité du domaine sur le serveur de votre centre ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/30/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e7f88831d10cfb1ba15d2fe650a056e7a3004d2f
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097510"
---
# <a name="install-ata---step-2"></a>Installer ATA - Étape 2

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!div class="step-by-step"]
> [«Étape 1](install-ata-step1.md) 
>  [Étape 3»](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Étape 2. Fournir un nom d’utilisateur et un mot de passe pour se connecter à votre forêt Active Directory

La première fois que vous ouvrez la console ATA, l’écran suivant apparaît :

![ATA welcome stage 1 (Accueil ATA - phase 1)](media/ATA_1.7-welcome-provide-username.png)

1. Entrez les informations suivantes, puis cliquez sur **Enregistrer** :

    |Champ|Commentaires|
    |---------|------------|
    |**Nom d’utilisateur** (obligatoire)|Entrez le nom de l’utilisateur en lecture seule, par exemple : **ATAuser**. **Remarque :** N’utilisez **pas** le format UPN pour votre nom d’utilisateur.|
    |**Mot de passe** (obligatoire)|Entrez le mot de passe de l’utilisateur en lecture seule, par exemple : **Pencil1**.|
    |**Domaine** (obligatoire)|Entrez le domaine de l’utilisateur en lecture seule, par exemple : **contoso.com**. **Remarque :** il est important d’entrer le nom complet du domaine où se trouve l’utilisateur. Par exemple, si le compte de l’utilisateur se trouve dans le domaine corp.contoso.com, vous devez entrer `corp.contoso.com`, et non contoso.com.|

1. Vous pouvez cliquer sur **Tester la connexion** pour tester la connectivité au domaine et vérifier que les informations d’identification fournies y donnent accès. Cela ne fonctionne que si le centre ATA dispose d’une connectivité au domaine.

    Après l’enregistrement, le message d’accueil dans la console devient : ![Étape de bienvenue ATA 1 terminée](media/ATA_1.7-welcome-provide-username-finished.png)

1. Dans la console, cliquez sur **Download Gateway setup and install the first Gateway** (Télécharger le programme d’installation de passerelle et installer la première passerelle) pour continuer.

> [!div class="step-by-step"]
> [«Étape 1](install-ata-step1.md) 
>  [Étape 3»](install-ata-step3.md)

## <a name="related-videos"></a>Vidéos connexes

- [Vue d’ensemble du déploiement ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Sélection du type de passerelle ATA approprié](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Voir aussi

- [Guide de déploiement ATA POC](/samples/browse/?redirectedfrom=TechNet-Gallery)
- [Outil de dimensionnement ATA](https://aka.ms/atasizingtool)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](ata-prerequisites.md)