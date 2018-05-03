---
title: Installer Azure - Protection avancée contre les menaces – Étape 1 | Microsoft Docs
description: La première étape pour installer Azure ATP implique la création d’un espace de travail pour votre déploiement Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/10/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a4c2f03955eddb4615b347fa8a211501546e6f4a
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/16/2018
---
*S’applique à : Azure - Protection avancée contre les menaces*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Création d’un espace de travail dans le portail de gestion d’espace de travail Azure ATP – Étape 1

>[!div class="step-by-step"]
[Étape 2 »](install-atp-step2.md)

Cette procédure d’installation fournit des instructions pour créer et gérer un espace de travail dans le portail de gestion d’espace de travail Azure ATP. Pour obtenir des informations sur l’architecture Azure ATP, consultez [Architecture Azure ATP](atp-architecture.md).

Dans Azure ATP, vous avez la possibilité de gérer et de surveiller plusieurs espaces de travail. Ceci est particulièrement utile si vous souhaitez créer un espace de travail de démonstration et un espace de travail de test dans lequel vous pouvez démontrer la preuve de concept Azure ATP avant de le déployer dans toute l’organisation. Cela est également nécessaire pour prendre en charge des déploiements avec plusieurs forêts. Un espace de travail individuel peut uniquement surveiller plusieurs domaines d’une même forêt. 

> [!NOTE]
> - Vous pouvez avoir un maximum de deux espaces de travail actifs. Après avoir supprimé un espace de travail, vous pouvez contacter le support pour le réactiver. Vous pouvez avoir au maximum trois espaces de travail supprimés. Pour augmenter le nombre d’espaces de travail enregistrés et supprimés, contactez le support Azure ATP.
> - Actuellement, les centres de données Azure ATP sont déployés en Europe, en Amérique du Nord/Amérique centrale/Caraïbes et en Asie.

## <a name="step-1-enter-the-workspace-management-portal"></a>Étape 1. Accéder au portail de gestion d’espace de travail

Après avoir vérifié que votre réseau est conforme aux exigences du capteur, vous pouvez passer à la création de l’espace de travail Azure ATP.

> [!NOTE]
>Pour accéder au portail de gestion d’espace de travail, vous devez être un administrateur général ou un administrateur de sécurité sur ce client.


1.  Accédez au [portail d’espace de travail Azure ATP](https://portal.atp.azure.com).

2.  Connectez-vous avec votre compte d’utilisateur Azure Active Directory.

## <a name="step-2-create-a-workspace"></a>Étape 2. Créer un espace de travail

1. Cliquez sur **Créer un espace de travail**.

2. Dans la boîte de dialogue **Créer un espace de travail**, nommez votre espace de travail, décidez s’il s’agit de votre espace de travail principal ou non, puis sélectionnez une **géolocalisation** pour votre centre de données. Un seul espace de travail peut être défini comme principal. La définition d’un espace de travail comme principal affecte les intégrations - vous pouvez intégrer Azure ATP et Windows Defender ATP uniquement pour votre espace de travail principal. Vous pouvez changer ultérieurement l’espace de travail principal, mais pour cela, vous devez supprimer toutes les intégrations déjà définies pour l’espace de travail principal actuel.
 > [!NOTE]
 > Après avoir sélectionné une géolocalisation, vous ne pouvez plus la modifier.
    ![Espace de travail Azure ATP](media/create-workspace.png)

3. Vous pouvez cliquer sur le lien **Gérer les rôles utilisateur Azure ATP** pour accéder directement au [Centre d’administration Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) et gérer vos groupes de rôles.

 > [!NOTE]
 > Pour vous connecter correctement à Azure ATP, vous devez vous connecter en tant qu’utilisateur doté du rôle Azure ATP approprié afin d’accéder au portail d’espace de travail Azure ATP. Pour plus d’informations sur le contrôle d’accès en fonction du rôle (RBAC) dans Azure ATP, consultez [Utilisation de groupes de rôles Azure ATP](atp-role-groups.md).

4. Cliquez sur le nom du nouvel espace de travail pour accéder au portail d’espace de travail Azure ATP pour cet espace de travail.

    ![Espaces de travail Azure ATP](media/atp-workspaces.png)

- Seul l’espace de travail principal peut être modifié. Pour apporter des modifications à d’autres espaces de travail, vous pouvez les supprimer et les ajouter à nouveau. Si vous souhaitez supprimer l’espace de travail principal, vous devez commencer par désactiver les intégrations et définir l’espace de travail comme non **principal** afin de pouvoir le supprimer.
- Pour modifier un espace de travail principal, vous devez commencer par désactiver les intégrations existantes dans cet espace de travail.

- Rétention des données – les espaces de travail supprimés n’apparaissent pas dans l’interface utilisateur, mais leurs données sont conservées conformément à la [stratégie de rétention des données de Microsoft](https://www.microsoft.com/trustcenter/privacy/you-own-your-data).


>[!div class="step-by-step"]
[« Préinstallation](configure-port-mirroring.md)
[Étape 2 »](install-atp-step2.md)


## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)
