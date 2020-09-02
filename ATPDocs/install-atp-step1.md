---
title: 'Démarrage rapide : Créer votre instance Azure ATP'
description: Guide de démarrage rapide pour créer l’instance pour votre déploiement d’Azure ATP, qui est la première étape de l’installation d’Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 10/31/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 12765e698f750bb2be05fd4ca308c494a1ea2c87
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88955154"
---
# <a name="quickstart-create-your-azure-atp-instance"></a>Démarrage rapide : Créer votre instance Azure ATP

Dans ce guide de démarrage rapide, vous allez créer votre instance Azure ATP dans le portail Azure ATP. Dans Azure ATP, vous avez une seule instance, qui était appelée espace de travail. Une seule instance vous permet de gérer plusieurs forêts à partir d’un même volet.

> [!IMPORTANT]
> Actuellement, les centres de données Azure ATP sont déployés en Europe, au Royaume-Uni, en Amérique du Nord, en Amérique Centrale, aux Caraïbes et en Asie. Votre instance est créée automatiquement dans le centre de données géographiquement le plus proche de votre annuaire Azure Active Directory (Azure AD). Une fois créées, les instances Azure ATP ne peuvent pas être déplacées.

## <a name="prerequisites"></a>Prérequis

- Une [licence Azure ATP](atp-technical-faq.md#licensing-and-privacy).
- Pour pouvoir accéder au portail Azure ATP, vous devez être [administrateur général ou administrateur de sécurité sur le locataire](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#available-roles).
- Examinez l’article [Architecture Azure ATP](atp-architecture.md).
- Examinez l’article [Prérequis d’Azure ATP](atp-prerequisites.md).

## <a name="sign-in-to-the-azure-atp-portal"></a>Se connecter au portail Azure ATP

Après avoir vérifié que votre réseau est conforme aux exigences du capteur, commencez la création de votre instance Azure ATP.

1. Accédez au [portail Azure ATP](https://portal.atp.azure.com)*.

1. Connectez-vous avec votre compte d’utilisateur Azure Active Directory.

\* Les clients GCC High doivent utiliser le portail [Azure ATP GCC High](http://portal.atp.azure.us).

## <a name="create-your-instance"></a>Créer votre instance

1. Cliquez sur **Créer une instance**.

    ![Créer une instance Azure ATP](media/create-instance.png)

1. Votre instance Azure ATP prend automatiquement le nom de domaine initial Azure AD et est créée dans le centre de données le plus proche de votre annuaire Azure AD.

    ![Instance Azure créée](media/instance-created.png)

    > [!NOTE]
    > Pour vous connecter à Azure ATP, vous devez utiliser un compte d’utilisateur auquel a été attribué un rôle Azure ATP doté de droits d’accès au portail Azure ATP. Pour plus d’informations sur le contrôle d’accès en fonction du rôle (RBAC) dans Azure ATP, consultez [Utilisation de groupes de rôles Azure ATP](atp-role-groups.md).

1. Cliquez sur **Configuration**, sur **Gérer les groupes de rôles**, puis utilisez le lien [Centre d’administration Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) pour gérer vos groupes de rôles.

    ![Gérer les groupes de rôles](media/creation-manage-role-groups.png)

- Conservation des données : les instances Azure ATP supprimées précédemment n’apparaissent pas dans l’interface utilisateur. Pour plus d’informations sur la conservation des données Azure ATP, consultez [Sécurité et confidentialité des données Azure ATP](atp-privacy-compliance.md).

## <a name="next-steps"></a>Étapes suivantes

> [!div class="step-by-step"]
> [« Prérequis](atp-prerequisites.md)
> [Étape 2 : Se connecter à Active Directory »](install-atp-step2.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://aka.ms/azureatpcommunity) dès aujourd’hui !