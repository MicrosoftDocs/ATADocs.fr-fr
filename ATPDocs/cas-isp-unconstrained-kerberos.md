---
title: 'Azure Advanced Threat Protection : évaluation de la posture de sécurité des identités concernant les délégations Kerberos sans contrainte'
description: Cet article propose une vue d’ensemble des rapports d’évaluation de la posture de sécurité fournis par Azure ATP concernant les délégations Kerberos sans contrainte.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 7eea354b-7a50-40d9-bfa7-dcccaef23179
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a4676837537869f6984ffe27f20b5cbeae971bde
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912793"
---
# <a name="security-assessment-unsecure-kerberos-delegation"></a>Évaluation de la sécurité : Délégations Kerberos non sécurisées

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-is-kerberos-delegation"></a>Qu’est-ce que la délégation Kerberos ?

La délégation Kerberos est un paramètre de délégation qui permet aux applications de demander les informations d’identification d’un utilisateur final pour accéder à des ressources au nom de l’utilisateur d’origine.

## <a name="what-risk-does-unsecure-kerberos-delegation-pose-to-an-organization"></a>Quel risque présente la délégation Kerberos non sécurisée pour une organisation ?

La délégation Kerberos non sécurisée permet à une entité d’emprunter l’identité de tout autre service choisi. Par exemple, imaginons que vous disposiez d’un site web IIS et que le compte du pool d’applications soit configuré avec une délégation sans contrainte. L’authentification Windows est activée sur le site web IIS, ce qui permet de prendre en charge l’authentification Kerberos native, et le site utilise un serveur SQL Server back-end pour les données métier. Avec votre compte d’administrateur de domaine, vous accédez au site web IIS et vous vous authentifiez auprès de celui-ci. Le site web, utilisant la délégation sans contrainte, peut obtenir un ticket de service d’un contrôleur de domaine au service SQL, et ce, en votre nom.

Le principal problème avec la délégation Kerberos est que vous vous en remettez à l’application pour faire toujours les bons choix. Des acteurs malveillants peuvent donc forcer l’application à commettre des actes inappropriés. Si vous êtes connecté en tant qu’**administrateur de domaine**, le site peut créer un ticket vers un autre service et agir en votre nom, à savoir en tant qu’**administrateur du domaine**. Par exemple, le site peut choisir un contrôleur de domaine et apporter des changements au groupe d’**administrateurs d’entreprise**. De même, le site peut acquérir le hachage du compte KRBTGT ou télécharger un fichier intéressant à partir du service des ressources humaines. Le risque est clair et les possibilités de la délégation non sécurisée sont quasiment illimitées.

Vous trouverez ci-dessous une description du risque encouru par différents types de délégation :

- **Délégation sans contrainte** : Tout service peut être mal utilisé si l’une de ses entrées de délégation est sensible.
- **Délégation contrainte** : Les entités contraintes peuvent être mal utilisées si l’une de leurs entrées de délégation est sensible.
- **Délégation contrainte basée sur les ressources** : Les entités contraintes basées sur les ressources peuvent être mal utilisées si l’entité elle-même est sensible.

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez le tableau de rapport pour découvrir les entités autres que des contrôleurs de domaine qui sont configurées pour la **délégation Kerberos non sécurisée**.

    ![Évaluation de la sécurité concernant la délégation Kerberos non sécurisée](media/atp-cas-isp-kerberos-delegation-2.png)
1. Prenez les mesures appropriées pour les utilisateurs à risque, par exemple en supprimant leur attribut sans contrainte ou en le remplaçant par une délégation contrainte plus sécurisée.

> [!NOTE]
> Cette évaluation est mise à jour toutes les 24 heures.

## <a name="remediation"></a>Mise à jour

Utilisez la correction appropriée à votre type de délégation.

### <a name="unconstrained-delegation"></a>Délégation sans contrainte

Désactivez la délégation ou utilisez l’un des types de délégation Kerberos contrainte suivants :

- **Délégation contrainte :** Restreint les services que ce compte peut emprunter.

    1. Sélectionnez **N’approuver cet ordinateur que pour la délégation aux services spécifiés**.

        ![Correction de la délégation Kerberos sans contrainte](media/atp-cas-isp-unconstrained-kerberos-1.png)

    2. Spécifiez les **services auxquels ce compte peut présenter des informations d’identification déléguées**.

- **Délégation contrainte basée sur les ressources :** Restreint les entités pouvant emprunter ce compte.  
La KCD basée sur la ressource est configurée à l’aide de PowerShell. Vous devez utiliser les applets de commande [Set-ADComputer](/powershell/module/addsadministration/set-adcomputer?view=win10-ps&preserve-view=true) ou [Set-ADUser](/powershell/module/addsadministration/set-aduser?view=win10-ps&preserve-view=true), selon que le compte d’emprunt est un compte d’ordinateur ou un compte de service/compte d’utilisateur.

### <a name="constrained-delegation"></a>Délégation contrainte

Passez en revue les utilisateurs sensibles listés dans les recommandations et supprimez-les des services auxquels le compte affecté peut présenter des informations d’identification déléguées.

![Correction de la délégation Kerberos contrainte](media/atp-cas-isp-unconstrained-kerberos-2.png)

### <a name="resource-based-constrained-delegation-rbcd"></a>Délégation contrainte basée sur les ressources (RBCD)

Passez en revue les utilisateurs sensibles listés dans les recommandations et supprimez-les de la ressource. Pour plus d’informations sur la configuration de la délégation RBCD, consultez [Configurer la délégation Kerberos contrainte (KCD) dans Azure Active Directory Domain Services](/azure/active-directory-domain-services/deploy-kcd).

## <a name="next-steps"></a>Étapes suivantes

- [Filtrage des activités Azure ATP dans Cloud App Security](activities-filtering-mcas.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
