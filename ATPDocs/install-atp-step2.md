---
title: 'Démarrage rapide : Connecter Azure ATP à Active Directory | Microsoft Docs'
description: La deuxième étape de la procédure d’installation d’Azure ATP vous permet de configurer les paramètres de connectivité du domaine sur votre service cloud Azure ATP
author: mlottner
ms.author: mlottner
ms.date: 02/05/2019
ms.topic: conceptual
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 404252e7fb9d71a067def9b28870d68736a493dd
ms.sourcegitcommit: 96752da28f43896e7b8e5945947b32c4810bdff6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/07/2019
ms.locfileid: "55831410"
---
# <a name="quickstart-connect-to-your-active-directory-forest"></a>Démarrage rapide : Se connecter à votre forêt Active Directory

Dans ce guide de démarrage rapide, vous connectez Azure ATP à Active Directory (AD) pour récupérer les données portant sur des utilisateurs et des ordinateurs. Si vous connectez plusieurs forêts, consultez l’article [Prise en charge de plusieurs forêts](atp-multi-forest.md).

## <a name="prerequisites"></a>Prérequis

- Une [instance Azure ATP](install-atp-step1.md).
- Examinez l’article [Prérequis d’Azure ATP](atp-prerequisites.md).
- Compte d’utilisateur AD **local** et mot de passe avec accès en lecture à tous les objets dans les domaines surveillés.

## <a name="provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Fournir un nom d’utilisateur et un mot de passe pour vous connecter à votre forêt Active Directory

La première fois que vous ouvrez le portail Azure ATP, l’écran suivant s’affiche :

![Étape 1 de bienvenue Azure ATP](media/directory-services.png)


1. Entrez les informations suivantes, puis cliquez sur **Enregistrer** :

    |Champ|Commentaires|
    |---------|------------|
    |**Nom d’utilisateur** (obligatoire)|Entrez le nom d’utilisateur Active Directory en lecture seule. Par exemple : **ATPuser**.  Vous devez utiliser un compte d’utilisateur AD **local**. N’utilisez **pas** le format UPN pour votre nom d’utilisateur.|
    |**Mot de passe** (obligatoire)|Entrez le mot de passe de l’utilisateur en lecture seule. Par exemple : **Pencil1**.|
    |**Domaine** (obligatoire)|Entrez le domaine de l’utilisateur en lecture seule. Par exemple : **contoso.com**. Il est important d’entrer le nom de domaine complet où se trouve l’utilisateur. Par exemple, si le compte de l’utilisateur se trouve dans le domaine corp.contoso.com, vous devez entrer `corp.contoso.com`, et non contoso.com.|

2. Dans le portail Azure ATP, cliquez sur **Télécharger le programme d’installation du capteur et installer le premier capteur** pour continuer.


## <a name="next-steps"></a>Étapes suivantes

> [!div class="step-by-step"]
> [« Étape 1 : Créer l’instance Azure ATP](install-atp-step1.md)
> [Étape 3 : Télécharger le programme d’installation du capteur »](install-atp-step3.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://aka.ms/azureatpcommunity) dès aujourd’hui !
