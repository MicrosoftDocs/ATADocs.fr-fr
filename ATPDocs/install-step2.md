---
title: 'Démarrage rapide : Connecter Microsoft Defender pour Identity à Active Directory'
description: La deuxième étape de la procédure d’installation de Microsoft Defender pour Identity vous aide à configurer les paramètres de connectivité du domaine sur votre service cloud Defender pour Identity
ms.date: 10/26/2020
ms.topic: quickstart
ms.openlocfilehash: b1379570d87957fc943bf8b0727b6b0294f26695
ms.sourcegitcommit: b6da51c97e8fb70ca04c0c0d5ea694700db9de86
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/21/2021
ms.locfileid: "98634554"
---
# <a name="quickstart-connect-to-your-active-directory-forest"></a>Démarrage rapide : Se connecter à votre forêt Active Directory

Dans ce guide de démarrage rapide, vous connectez [!INCLUDE [Product long](includes/product-long.md)] à Active Directory (AD) pour récupérer les données portant sur des utilisateurs et des ordinateurs. Si vous connectez plusieurs forêts, consultez l’article [Prise en charge de plusieurs forêts](multi-forest.md).

## <a name="prerequisites"></a>Prérequis

- Une [instance [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md).
- Consultez l’article [Prérequis de [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md).
- Au moins l’un des comptes de services d’annuaire suivants, avec accès en lecture à tous les objets dans les domaines analysés :
  - Un mot de passe et un compte d’utilisateur AD **standard**. Requis pour les capteurs exécutant Windows Server 2008 R2 SP1.
  - Un **compte de service administré du groupe** (gMSA). Requiert Windows Server 2012 ou version ultérieure.  
  Tous les capteurs doivent disposer des autorisations pour récupérer le mot de passe du compte gMSA. Pour plus d’informations sur la création d’un compte gMSA, consultez [Configurer un compte gMSA](#how-to-set-up-a-gmsa-account).

    > [!NOTE]
    >
    > - Pour les ordinateurs du capteur exécutant Windows Server 2012 et versions ultérieures, nous vous recommandons d’utiliser un compte **gMSA** pour améliorer la sécurité et la gestion automatique des mots de passe.
    > - Si vous avez plusieurs capteurs, certains exécutant Windows Server 2008 et d’autres qui exécutent Windows Server 2012 ou version ultérieure, en plus de la recommandation d’utiliser un compte **gMSA**, vous devez également utiliser au moins un compte d’utilisateur AD **standard**.

### <a name="how-to-set-up-a-gmsa-account"></a>Comment configurer un compte gMSA

1. Créer un [compte gMSA](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts#BKMK_CreateGMSA).
1. Créez un nouveau [groupe de sécurité contenant tous vos contrôleurs de domaine avec des capteurs (exécutant Windows Server 2012 ou version ultérieure)](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts#BKMK_AddMemberHosts) avec les autorisations nécessaires pour récupérer le mot de passe du compte gMSA. (Recommandé)

## <a name="provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Fournir un nom d’utilisateur et un mot de passe pour vous connecter à votre forêt Active Directory

La première fois que vous ouvrez le portail [!INCLUDE [Product short](includes/product-short.md)], l’écran suivant s’affiche :

![Bienvenue, phase 1, paramètres des services d’annuaire](media/directory-services.png)

1. Entrez les informations suivantes, puis cliquez sur **Enregistrer** :

    |Champ|Commentaires|
    |---|---|
    |**Nom d’utilisateur** (obligatoire)|Saisissez le nom d'utilisateur AD en lecture seule. Par exemple : **DefenderForIdentityUser**. Vous devez utiliser un compte d’utilisateur ou gMSA AD **standard**. N’utilisez **pas** le format UPN pour votre nom d’utilisateur.<br />**REMARQUE :** Nous vous recommandons d’éviter d’utiliser des comptes attribués à des utilisateurs spécifiques.|
    |**Mot de passe** (requis pour le compte d’utilisateur AD standard)|Pour le compte d'utilisateur AD, saisissez le mot de passe de l’utilisateur en lecture seule. Par exemple : **Pencil1**.|
    |**Compte de service administré du groupe** (requis pour le compte gMSA)|Pour le compte gMSA, sélectionnez **Compte de service administré du groupe**.|
    |**Domaine** (obligatoire)|Entrez le domaine de l’utilisateur en lecture seule. Par exemple : **contoso.com**. Il est important d’entrer le nom de domaine complet où se trouve l’utilisateur. Par exemple, si le compte de l’utilisateur se trouve dans le domaine corp.contoso.com, vous devez entrer `corp.contoso.com`, et non contoso.com.|

1. Dans le portail [!INCLUDE [Product short](includes/product-short.md)], cliquez sur **Télécharger le programme d’installation du capteur et installer le premier capteur** pour continuer.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="step-by-step"]
> [« Étape 1 : Créer l’instance [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
> [Étape 3 : Télécharger le programme d’installation du capteur »](install-step3.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter de [!INCLUDE [Product short](includes/product-short.md)] et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity) !
