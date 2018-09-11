---
title: Installer Azure - Protection avancée contre les menaces – Étape 1 | Microsoft Docs
description: La première étape pour installer Azure ATP implique la création de l’instance pour votre déploiement Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9ba476c579de3c468ce9c8ca09e8b8bab4fa9e1d
ms.sourcegitcommit: f9400ae27d22607e4146dc9b8a0b9ba6f61fdd38
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/05/2018
ms.locfileid: "43743312"
---
*S’applique à : Azure Advanced Threat Protection*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Création d’un espace de travail dans le portail de gestion d’espace de travail Azure ATP – Étape 1

>[!div class="step-by-step"]
[Étape 2 »](install-atp-step2.md)

Cette procédure d’installation fournit des instructions pour créer et gérer votre instance Azure ATP. Pour obtenir des informations sur l’architecture Azure ATP, consultez [Architecture Azure ATP](atp-architecture.md).

Dans Azure ATP, vous disposez d’un seul espace de travail ou d’une seule instance pour gérer plusieurs forêts dans un volet unique. 

> [!NOTE]
> Actuellement, les centres de données Azure ATP sont déployés en Europe, en Amérique du Nord/Amérique centrale/Caraïbes et en Asie.

## <a name="step-1-enter-the-management-portal"></a>Étape 1. Accéder au portail de gestion

Après avoir vérifié que votre réseau est conforme aux exigences du capteur, vous pouvez passer à la création de l’espace de travail Azure ATP.

> [!NOTE]
>Pour accéder au portail de gestion d’espace de travail, vous devez être administrateur général ou administrateur de sécurité sur ce locataire.


1.  Accédez au [portail Azure ATP](https://portal.atp.azure.com).

2.  Connectez-vous avec votre compte d’utilisateur Azure Active Directory.

## <a name="step-2-create-your-workspace"></a>Étape 2. Créer votre espace de travail

1. Cliquez sur **Créer un espace de travail**.

2. Dans la boîte de dialogue **Créer un espace de travail**, nommez votre espace de travail, puis sélectionnez une **géolocalisation** pour votre centre de données. Un seul espace de travail peut être défini comme principal. La définition d’un espace de travail comme principal affecte les intégrations - vous pouvez intégrer Azure ATP et Windows Defender ATP uniquement pour votre espace de travail principal. Vous pouvez changer ultérieurement l’espace de travail principal, mais pour cela, vous devez supprimer toutes les intégrations déjà définies pour l’espace de travail principal actuel.
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

- Conservation des données – les espaces de travail supprimés n’apparaissent pas dans l’interface utilisateur. Pour plus d’informations sur la conservation des données Azure ATP, consultez [Sécurité des données Azure ATP et confidentialité](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[« Préinstallation](configure-port-mirroring.md)
[Étape 2 »](install-atp-step2.md)


## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)
