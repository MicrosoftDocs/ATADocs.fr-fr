---
title: 'Démarrage rapide : Connecter Azure ATP à Active Directory'
description: La deuxième étape de la procédure d’installation d’Azure ATP vous permet de configurer les paramètres de connectivité du domaine sur votre service cloud Azure ATP
author: shsagir
ms.author: shsagir
ms.date: 01/15/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 29d6fc0a1a79b5861bad447f160ba7f5fe6a0131
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88954338"
---
# <a name="quickstart-connect-to-your-active-directory-forest"></a>Démarrage rapide : Se connecter à votre forêt Active Directory

Dans ce guide de démarrage rapide, vous connectez Azure ATP à Active Directory (AD) pour récupérer les données portant sur des utilisateurs et des ordinateurs. Si vous connectez plusieurs forêts, consultez l’article [Prise en charge de plusieurs forêts](atp-multi-forest.md).

## <a name="prerequisites"></a>Prérequis

- Une [instance Azure ATP](install-atp-step1.md).
- Examinez l’article [Prérequis d’Azure ATP](atp-prerequisites.md).
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

La première fois que vous ouvrez le portail Azure ATP, l’écran suivant s’affiche :

![Étape 1 de bienvenue Azure ATP](media/directory-services.png)

1. Entrez les informations suivantes, puis cliquez sur **Enregistrer** :

    |Champ|Commentaires|
    |---|---|
    |**Nom d’utilisateur** (obligatoire)|Saisissez le nom d'utilisateur AD en lecture seule. Par exemple : **ATPuser**. Vous devez utiliser un compte d’utilisateur ou gMSA AD **standard**. N’utilisez **pas** le format UPN pour votre nom d’utilisateur.|
    |**Mot de passe** (requis pour le compte d’utilisateur AD standard)|Pour le compte d'utilisateur AD, saisissez le mot de passe de l’utilisateur en lecture seule. Par exemple : **Pencil1**.|
    |**Compte de service administré du groupe** (requis pour le compte gMSA)|Pour le compte gMSA, sélectionnez **Compte de service administré du groupe**.|
    |**Domaine** (obligatoire)|Entrez le domaine de l’utilisateur en lecture seule. Par exemple : **contoso.com**. Il est important d’entrer le nom de domaine complet où se trouve l’utilisateur. Par exemple, si le compte de l’utilisateur se trouve dans le domaine corp.contoso.com, vous devez entrer `corp.contoso.com`, et non contoso.com.|

1. Dans le portail Azure ATP, cliquez sur **Télécharger le programme d’installation du capteur et installer le premier capteur** pour continuer.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="step-by-step"]
> [« Étape 1 : Créer l’instance Azure ATP](install-atp-step1.md)
> [Étape 3 : Télécharger le programme d’installation du capteur »](install-atp-step3.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://aka.ms/azureatpcommunity) dès aujourd’hui !
