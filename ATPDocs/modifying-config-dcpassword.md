---
title: Modifier la configuration Azure-protection avancée contre les menaces-mot de passe de connectivité du domaine
description: Décrit comment modifier le mot de passe de connectivité de domaine sur le capteur autonome Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/19/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3d35651f0741caa6189ae8ef79e14e8b0db78eff
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828321"
---
# <a name="change-azure-atp-portal-configuration---domain-connectivity-password"></a>Modifier le mot de passe de connectivité de domaine dans la configuration du portail Azure ATP

## <a name="change-the-domain-connectivity-password"></a>Modifier le mot de passe de connectivité de domaine

Si vous avez besoin de modifier le mot de passe de connectivité de domaine, assurez-vous que le mot de passe que vous entrez est correct. Dans le cas contraire, le service de capteur Azure ATP s’arrête pour tous les capteurs déployés.

Si vous pensez que cela s’est produit, recherchez les erreurs suivantes dans le fichier Microsoft. tri. Sensor-Errors. log : `The supplied credential is invalid.`

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

1. Cliquez sur **Enregistrer**.

1. Dans le portail Azure ATP, sous **Configuration**, accédez à la page **Capteur** et vérifiez l’état des capteurs.

## <a name="see-also"></a>Voir aussi

- [Intégration avec Microsoft Defender ATP](integrate-msde.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
