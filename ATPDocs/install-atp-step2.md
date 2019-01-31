---
title: Installer Azure - Protection avancée contre les menaces | Microsoft Docs
description: La deuxième étape de la procédure d’installation d’Azure ATP vous permet de configurer les paramètres de connectivité du domaine sur votre service cloud Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/30/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ada659d86088cb9f93eba4aca54dd2553e8fb69a
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085450"
---
# <a name="install-azure-atp---step-2"></a>Installer Azure ATP – Étape 2

> [!div class="step-by-step"]
> [« Étape 1](install-atp-step1.md)
> [Étape 3 »](install-atp-step3.md)

## <a name="provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Fournir un nom d’utilisateur et un mot de passe pour vous connecter à votre forêt Active Directory

La première fois que vous ouvrez le portail Azure ATP, l’écran suivant s’affiche :

![Étape 1 de bienvenue Azure ATP](media/directory-services.png)

> [!IMPORTANT]
> Les présentes informations d’identification utilisateur doivent être celles d’un compte d’utilisateur dans l’instance Active Directory locale. 


1.  Entrez les informations suivantes, puis cliquez sur **Enregistrer** :

    |Champ|Commentaires|
    |---------|------------|
    |**Nom d’utilisateur** (obligatoire)|Entrez le nom d’utilisateur Active Directory en lecture seule, par exemple : **ATPuser**. **Remarque :** N’utilisez **pas** le format UPN pour votre nom d’utilisateur.|
    |**Mot de passe** (obligatoire)|Entrez le mot de passe de l’utilisateur en lecture seule, par exemple : **Pencil1**.|
    |**Domaine** (obligatoire)|Entrez le domaine de l’utilisateur en lecture seule, par exemple : **contoso.com**. **Remarque :** Il est important d’entrer le nom complet du domaine où se trouve l’utilisateur. Par exemple, si le compte de l’utilisateur se trouve dans le domaine corp.contoso.com, vous devez entrer `corp.contoso.com`, et non contoso.com.|

2. Dans le portail Azure ATP, cliquez sur **Télécharger le programme d’installation du capteur et installer le premier capteur** pour continuer.


> [!div class="step-by-step"]
> [« Étape 1](install-atp-step1.md)
> [Étape 3 »](install-atp-step3.md)


## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)