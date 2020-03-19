---
title: Modifier le mot de passe de connectivité de domaine dans la configuration d’Azure Advanced Threat Protection
description: Décrit comment modifier le mot de passe de connectivité de domaine sur le capteur autonome Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 294d76a0455ac11866196919caa1bd830617420b
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414707"
---
# <a name="change-azure-atp-portal-configuration---domain-connectivity-password"></a>Modifier le mot de passe de connectivité de domaine dans la configuration du portail Azure ATP

## <a name="change-the-domain-connectivity-password"></a>Modifier le mot de passe de connectivité de domaine

Si vous avez besoin de modifier le mot de passe de connectivité de domaine, assurez-vous que le mot de passe que vous entrez est correct. Dans le cas contraire, le service de capteur Azure ATP s’arrête pour tous les capteurs déployés.

Si vous pensez que cela s’est produit, recherchez les erreurs suivantes dans le fichier Microsoft.Tri.sensor-Errors.log : `The supplied credential is invalid.`

Suivez la procédure ci-dessous pour mettre à jour le mot de passe de connectivité de domaine dans le portail Azure ATP :

> [!NOTE]
> Il s’agit du nom d’utilisateur et du mot de passe du déploiement local d’Active Directory et non d’Azure AD.

1. Ouvrez le portail Azure ATP en accédant à l’URL du portail.

1. Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône de paramètres de configuration d’Azure ATP](media/atp-config-menu.png)

1. Sélectionnez **Services d’annuaire**.

    ![Image du mot de passe de modification du capteur autonome Azure ATP](media/directory-services.png)

1. Sous **Mot de passe**, modifiez le mot de passe.

    > [!NOTE]
    > Entrez un utilisateur et un mot de passe Active Directory ici, pas Azure Active Directory.

1. Cliquez sur **Save**.

1. Dans le portail Azure ATP, sous **Configuration**, accédez à la page **Capteur** et vérifiez l’état des capteurs.

## <a name="see-also"></a>Voir aussi

- [Intégration à Windows Defender ATP](integrate-wd-atp.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
