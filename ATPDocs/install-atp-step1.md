---
title: Installer Azure - Protection avancée contre les menaces | Microsoft Docs
description: La première étape pour installer Azure ATP implique la création de l’instance pour votre déploiement Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4c178d4ed874ae3d826e97a154ae2e17bd52f48c
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54840367"
---
# <a name="creating-your-azure-atp-instance-in-the-azure-atp-portal---step-1"></a>Création de votre instance Azure ATP sur le portail Azure ATP - Étape 1

> [!div class="step-by-step"]
> [Étape 2 »](install-atp-step2.md)

Cette procédure d’installation fournit des instructions pour créer et gérer votre instance Azure ATP (appelée précédemment espace de travail). Pour obtenir des informations sur l’architecture Azure ATP, consultez [Architecture Azure ATP](atp-architecture.md).

Dans Azure ATP, vous disposez d’une seule instance pour gérer plusieurs forêts dans un même volet. 

> [!NOTE]
> Actuellement, les centres de données Azure ATP sont déployés en Europe, en Amérique du Nord/Amérique centrale/Les Antilles et en Asie. Votre instance est créée automatiquement dans le centre de données le plus proche géographiquement de votre annuaire AAD. Une fois créées, les instances Azure ATP ne peuvent plus être déplacées. 

## <a name="step-1-enter-the-azure-atp-portal"></a>Étape 1. Accédez au portail Azure ATP.

Après avoir vérifié que votre réseau est conforme aux exigences du capteur, passez à la création de votre instance Azure ATP.

> [!NOTE]
>Pour pouvoir accéder au portail Azure ATP, vous devez être administrateur général ou administrateur de sécurité de ce locataire.


1.  Accédez au [portail Azure ATP](https://portal.atp.azure.com).

2.  Connectez-vous avec votre compte d’utilisateur Azure Active Directory.

## <a name="step-2-create-your-instance"></a>Étape 2. Créer votre instance

1. Cliquez sur **Créer une instance**. 

    ![Créer une instance Azure ATP](media/create-instance.png)

2. Votre instance Azure ATP prend automatiquement le nom de domaine initial AAD et est allouée au centre de données situé le plus près de votre annuaire AAD avant d’être créée. 

    ![Instance Azure créée](media/instance-created.png)

    > [!NOTE]
    > Pour vous connecter à Azure ATP, vous devez utiliser un compte d’utilisateur auquel a été attribué un rôle Azure ATP doté de droits d’accès au portail Azure ATP. Pour plus d’informations sur le contrôle d’accès en fonction du rôle (RBAC) dans Azure ATP, consultez [Utilisation de groupes de rôles Azure ATP](atp-role-groups.md).
 
3. Cliquez sur **Configuration**, sur **Gérer les groupes de rôles**, puis utilisez le lien [Centre d’administration Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) pour gérer vos groupes de rôles. .

    ![Gérer les groupes de rôles](media/creation-manage-role-groups.png)

- Conservation des données : les instances Azure ATP supprimées précédemment ne figurent pas dans l’interface utilisateur. Pour plus d’informations sur la conservation des données Azure ATP, consultez [Sécurité des données Azure ATP et confidentialité](atp-privacy-compliance.md).


> [!div class="step-by-step"]
> [« Préinstallation](atp-prerequisites.md)
> [Étape 2 »](install-atp-step2.md)



## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
