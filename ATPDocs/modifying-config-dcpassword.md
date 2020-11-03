---
title: Modifier Microsoft Defender pour la configuration d’identité-mot de passe de connectivité de domaine
description: Décrit comment modifier le mot de passe de connectivité du domaine sur le capteur Microsoft Defender pour l’identité autonome.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b9dcd871fecd855a35a530f57c020fba5f3d1347
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275880"
---
# <a name="change-product-long-portal-configuration---domain-connectivity-password"></a>Modifier la [!INCLUDE [Product long](includes/product-long.md)] configuration du portail-mot de passe de connectivité du domaine

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="change-the-domain-connectivity-password"></a>Modifier le mot de passe de connectivité de domaine

Si vous avez besoin de modifier le mot de passe de connectivité de domaine, assurez-vous que le mot de passe que vous entrez est correct. Si ce n’est pas le cas, le [!INCLUDE [Product long](includes/product-long.md)] service de capteur s’arrête pour tous les capteurs déployés.

Si vous pensez que cela s’est produit, recherchez les erreurs suivantes dans le fichier Microsoft. tri. Sensor-Errors. log : `The supplied credential is invalid.`

Pour mettre à jour le mot de passe de connectivité du domaine sur le portail, procédez comme suit [!INCLUDE [Product short](includes/product-short.md)] :

> [!NOTE]
> Il s’agit du nom d’utilisateur et du mot de passe du déploiement local d’Active Directory et non d’Azure AD.

1. Ouvrez le [!INCLUDE [Product short](includes/product-short.md)] portail en accédant à l’URL du portail.

1. Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![[! Icône INCLUDe [Product Short] (includes/Product-Short. MD)] paramètres de configuration](media/config-menu.png)

1. Sélectionnez **Services d’annuaire**.

    ![[! INCLUDe [Product Short] (includes/Product-Short. MD)] image de modification de mot de passe de capteur autonome](media/directory-services.png)

1. Sous **Mot de passe** , modifiez le mot de passe.

    > [!NOTE]
    > Entrez un utilisateur et un mot de passe Active Directory ici, pas Azure Active Directory.

1. Cliquez sur **Enregistrer**.

1. Dans le [!INCLUDE [Product short](includes/product-short.md)] portail, sélectionnez **configuration**.
1. Sous **système** , sélectionnez la page **capteurs** et vérifiez l’état des capteurs.

## <a name="see-also"></a>Voir aussi

- [Intégration à Microsoft Defender pour le point de terminaison](integrate-mde.md)
- [Consultez le [!INCLUDE [Product short](includes/product-short.md)] Forum !](https://aka.ms/MDIcommunity)
