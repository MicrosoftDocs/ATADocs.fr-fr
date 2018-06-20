---
title: Modifier le mot de passe de connectivité de domaine dans la configuration d’Azure - Protection avancée contre les menaces | Microsoft Docs
description: Décrit comment modifier le mot de passe de connectivité de domaine sur le capteur autonome Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 369f00b1b33fe509850bc331b0d5b45ae161f91c
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
ms.locfileid: "29444825"
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="change-azure-atp-workspace-portal-configuration---domain-connectivity-password"></a>Modifier le mot de passe de connectivité de domaine dans la configuration du portail d’espace de travail Azure ATP



## <a name="change-the-domain-connectivity-password"></a>Modifier le mot de passe de connectivité de domaine
Si vous avez besoin de modifier le mot de passe de connectivité de domaine, assurez-vous que le mot de passe que vous entrez est correct. Dans le cas contraire, le service de capteur Azure ATP s’arrête pour tous les capteurs déployés.

Si vous pensez que cela s’est produit, recherchez les erreurs suivantes dans le fichier Microsoft.Tri.sensor-Errors.log sur le capteur autonome Azure ATP : `The supplied credential is invalid.`

Procédez comme suit pour mettre à jour le mot de passe de connectivité de domaine dans le portail d’espace de travail Azure ATP :

> [!NOTE]
> Il s’agit du nom d’utilisateur et du mot de passe du déploiement local d’Active Directory et non d’Azure AD.

1.  Ouvrez le portail d’espace de travail Azure ATP en accédant à l’URL de l’espace de travail.

2.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône de paramètres de configuration d’Azure ATP](media/atp-config-menu.png)

3.  Sélectionnez **Services d’annuaire**.

    ![Image du mot de passe de modification du capteur autonome Azure ATP](media/directory-services.png)

4.  Sous **Mot de passe**, modifiez le mot de passe.

 > [!NOTE]
 > Entrez un utilisateur et un mot de passe Active Directory ici, pas Azure Active Directory.

5.  Cliquez sur **Enregistrer**.

6.  Après avoir changé le mot de passe, vérifiez manuellement que le service de capteur autonome Azure ATP est en cours d’exécution sur les serveurs de capteur autonome Azure ATP.

7. Dans le portail d’espace de travail, sous **Configuration**, accédez à la page **Capteur** et vérifiez le statut des capteurs.

## <a name="see-also"></a>Voir aussi

- [Intégration à Windows Defender ATP](integrate-wd-atp.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)