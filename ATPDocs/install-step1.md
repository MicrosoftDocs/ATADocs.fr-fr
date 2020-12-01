---
title: 'Démarrage rapide : Créer votre instance Microsoft Defender pour Identity'
description: Guide de démarrage rapide afin de créer l’instance pour votre déploiement de Microsoft Defender pour Identity, qui est la première étape de l’installation de Defender pour Identity.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 10/26/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fcb99edccdd8ce98be4b9335d7703503307fd0ac
ms.sourcegitcommit: 07a855b87931875bdeca14b152b13a36db79bfa8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2020
ms.locfileid: "94848577"
---
# <a name="quickstart-create-your-product-long-instance"></a>Démarrage rapide : Créer votre instance [!INCLUDE [Product long](includes/product-long.md)]

Dans ce guide de démarrage rapide, vous allez créer votre instance [!INCLUDE [Product long](includes/product-long.md)] dans le portail [!INCLUDE [Product short](includes/product-short.md)]. Dans [!INCLUDE [Product short](includes/product-short.md)], vous avez une seule instance, qui était appelée espace de travail. Une seule instance vous permet de gérer plusieurs forêts à partir d’un même volet.

> [!IMPORTANT]
> Les centres de données [!INCLUDE [Product short](includes/product-short.md)] sont déployés en Europe, au Royaume-Uni, en Amérique du Nord, en Amérique Centrale, aux Caraïbes et en Asie. Votre instance est créée automatiquement dans le centre de données géographiquement le plus proche de votre annuaire Azure Active Directory (Azure AD). Une fois créées, les instances [!INCLUDE [Product short](includes/product-short.md)] ne peuvent pas être déplacées.

## <a name="prerequisites"></a>Prérequis

- Une [licence [!INCLUDE [Product long](includes/product-long.md)]](technical-faq.md#licensing-and-privacy).
- Pour pouvoir accéder au portail [!INCLUDE [Product short](includes/product-short.md)], vous devez être [administrateur général ou administrateur de sécurité sur le locataire](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#available-roles).
- Consultez l’article [Architecture [!INCLUDE [Product short](includes/product-short.md)]](architecture.md).
- Consultez l’article [Prérequis de [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md).

## <a name="sign-in-to-the-product-short-portal"></a>Se connecter au portail [!INCLUDE [Product short](includes/product-short.md)]

Après avoir vérifié que votre réseau est conforme à la configuration requise du capteur, commencez la création de votre instance [!INCLUDE [Product short](includes/product-short.md)].

1. Accédez au [portail [!INCLUDE [Product short](includes/product-short.md)]](https://portal.atp.azure.com)*.

1. Connectez-vous avec votre compte d’utilisateur Azure Active Directory.

\* Les clients GCC High doivent utiliser le portail [[!INCLUDE [Product short](includes/product-short.md)] GCC High](http://portal.atp.azure.us).

## <a name="create-your-instance"></a>Créer votre instance

1. Cliquez sur **Créer une instance**.

    ![Créer l’instance [!INCLUDE [Product short](includes/product-short.md)]](media/create-instance.png)

1. Votre instance [!INCLUDE [Product short](includes/product-short.md)] prend automatiquement le nom de domaine initial Azure AD et est créée dans le centre de données le plus proche de votre annuaire Azure AD.

    ![Instance Azure créée](media/instance-created.png)

    > [!NOTE]
    > Pour vous connecter à [!INCLUDE [Product short](includes/product-short.md)], vous devez utiliser un compte d’utilisateur auquel a été attribué un rôle [!INCLUDE [Product short](includes/product-short.md)] doté de droits d’accès au portail [!INCLUDE [Product short](includes/product-short.md)]. Pour plus d’informations sur le contrôle d’accès en fonction du rôle (RBAC) dans [!INCLUDE [Product short](includes/product-short.md)], consultez [Utilisation de groupes de rôles [!INCLUDE [Product short](includes/product-short.md)]](role-groups.md).

1. Sélectionnez **Configuration**, sur **Gérer les groupes de rôles**, puis utilisez le lien [Centre d’administration Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) pour gérer vos groupes de rôles.

    ![Gérer les groupes de rôles](media/creation-manage-role-groups.png)

- Conservation des données : les instances [!INCLUDE [Product short](includes/product-short.md)] supprimées n’apparaissent pas dans l’interface utilisateur. Pour plus d’informations sur la conservation des données [!INCLUDE [Product short](includes/product-short.md)], consultez [Sécurité et confidentialité des données [!INCLUDE [Product short](includes/product-short.md)]](privacy-compliance.md).

## <a name="next-steps"></a>Étapes suivantes

> [!div class="step-by-step"]
> [« Prérequis](prerequisites.md)
> [Étape 2 : Se connecter à Active Directory »](install-step2.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter de [!INCLUDE [Product short](includes/product-short.md)] et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity) !
