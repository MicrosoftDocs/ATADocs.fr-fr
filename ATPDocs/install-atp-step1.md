---
title: Installer Azure Advanced Threat Protection | Microsoft Docs
description: La première étape pour installer Azure ATP implique la création de l’instance pour votre déploiement Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/4/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 97cce3de3a1cbe049523c54901ecbc9228aaee53
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783010"
---
*S’applique à : Azure Advanced Threat Protection*


# <a name="creating-your-azure-atp-instance-in-the-portal---step-1"></a>Création de votre instance Azure ATP dans le portail - Étape 1

> [!div class="step-by-step"]
> [Étape 2 »](install-atp-step2.md)

Cette procédure d’installation fournit des instructions pour créer et gérer votre instance ou votre espace de travail Azure ATP. Pour obtenir des informations sur l’architecture Azure ATP, consultez [Architecture Azure ATP](atp-architecture.md).

Dans Azure ATP, vous disposez d’un seul espace de travail ou d’une seule instance pour gérer plusieurs forêts dans un même volet. 

> [!NOTE]
> Actuellement, les centres de données Azure ATP sont déployés en Europe, en Amérique du Nord/Amérique centrale/Caraïbes et en Asie.

## <a name="step-1-enter-the-azure-atp-portal"></a>Étape 1. Accédez au portail Azure ATP.

Après avoir vérifié que votre réseau est conforme aux exigences du capteur, vous pouvez passer à la création de l’espace de travail Azure ATP.

> [!NOTE]
>Pour accéder au portail de gestion d’espace de travail, vous devez être administrateur général ou administrateur de sécurité sur ce locataire.


1.  Accédez au [portail Azure ATP](https://portal.atp.azure.com).

2.  Connectez-vous avec votre compte d’utilisateur Azure Active Directory.

## <a name="step-2-create-your-workspace"></a>Étape 2. Créer votre espace de travail

1. Cliquez sur **Créer un espace de travail**.

2. Dans la boîte de dialogue **Créer un espace de travail**, nommez votre espace de travail, puis sélectionnez une **géolocalisation** pour votre centre de données. Votre espace de travail est par défaut **Principal**. 
 > [!NOTE]
 > Après avoir sélectionné une géolocalisation, vous ne pouvez plus la modifier.
    ![Espace de travail Azure ATP](media/create-workspace.png)

3. Vous pouvez cliquer sur le lien **Gérer les rôles utilisateur Azure ATP** pour accéder directement au [Centre d’administration Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) et gérer vos groupes de rôles.

 > [!NOTE]
 > Pour vous connecter correctement à Azure ATP, vous devez vous connecter comme utilisateur auquel le rôle Azure ATP approprié pour accéder au portail Azure ATP a été affecté. Pour plus d’informations sur le contrôle d’accès en fonction du rôle (RBAC) dans Azure ATP, consultez [Utilisation de groupes de rôles Azure ATP](atp-role-groups.md).

4. Cliquez sur le nom de votre espace de travail pour accéder au portail Azure ATP.

    ![Espaces de travail Azure ATP](media/atp-workspaces.png)

- Seul l’espace de travail principal peut être modifié. Si vous voulez supprimer votre espace de travail principal, vous devez d’abord désactiver les intégrations.

- Conservation des données : les espaces de travail qui ont été supprimés auparavant n’apparaissent pas dans l’interface utilisateur. Pour plus d’informations sur la conservation des données Azure ATP, consultez [Sécurité des données Azure ATP et confidentialité](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[« Préinstallation](atp-prerequisites.md)
[Étape 2 »](install-atp-step2.md)



## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
