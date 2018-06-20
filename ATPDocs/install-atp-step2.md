---
title: Installer Azure - Protection avancée contre les menaces – Étape 2 | Microsoft Docs
description: La deuxième étape de la procédure d’installation d’Azure ATP vous permet de configurer les paramètres de connectivité du domaine sur votre service cloud Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 11f9d5bf69ffda0843a94c7a2bb31869dc980dce
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
ms.locfileid: "29445575"
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="install-azure-atp---step-2"></a>Installer Azure ATP – Étape 2

>[!div class="step-by-step"]
[« Étape 1](install-atp-step1.md)
[Étape 3 »](install-atp-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Étape 2. Fournir un nom d’utilisateur et un mot de passe pour vous connecter à votre forêt Active Directory

La première fois que vous ouvrez le portail d’espace de travail Azure ATP, l’écran suivant apparaît :

![Étape 1 de bienvenue Azure ATP](media/directory-services.png)

> [!IMPORTANT]
> Les présentes informations d’identification utilisateur doivent être celles d’un compte d’utilisateur dans l’instance Active Directory locale. 


1.  Entrez les informations suivantes, puis cliquez sur **Enregistrer** :

    |Champ|Commentaires|
    |---------|------------|
    |**Nom d’utilisateur** (obligatoire)|Entrez le nom d’utilisateur Active Directory en lecture seule, par exemple : **ATPuser**.|
    |**Mot de passe** (obligatoire)|Entrez le mot de passe de l’utilisateur en lecture seule, par exemple : **Pencil1**.|
    |**Domaine** (obligatoire)|Entrez le domaine de l’utilisateur en lecture seule, par exemple : **contoso.com**. **Remarque :** il est important d’entrer le nom complet du domaine où se trouve l’utilisateur. Par exemple, si le compte de l’utilisateur se trouve dans le domaine corp.contoso.com, vous devez entrer `corp.contoso.com`, et non contoso.com.|

3. Dans le portail d’espace de travail, cliquez sur **Télécharger le programme d'installation du capteur et installer le premier capteur** pour continuer.


>[!div class="step-by-step"]
[« Étape 1](install-atp-step1.md)
[Étape 3 »](install-atp-step3.md)


## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)