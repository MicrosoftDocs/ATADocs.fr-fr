---
title: 'Azure Advanced Threat Protection : évaluation de la posture de sécurité des identités concernant les délégations Kerberos sans contrainte | Microsoft Docs'
description: Cet article propose une vue d’ensemble des rapports d’évaluation de la posture de sécurité fournis par Azure ATP concernant les délégations Kerberos sans contrainte.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 7eea354b-7a50-40d9-bfa7-dcccaef23179
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1343d0359750744890fdb3e15b5f49adfd2459d1
ms.sourcegitcommit: 475df3e87d8476ff13e48ebc7a722f46f29dab70
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2019
ms.locfileid: "71007439"
---
# <a name="security-assessment-unsecure-kerberos-delegation---preview"></a>Évaluation de la sécurité : Délégations Kerberos non sécurisées - Préversion


## <a name="what-is-kerberos-delegation"></a>Qu’est-ce que la délégation Kerberos ? 

La délégation Kerberos est un paramètre de délégation qui permet aux applications de demander les informations d’identification d’un utilisateur final pour accéder à des ressources au nom de l’utilisateur d’origine.  

## <a name="what-risk-does-unsecure-kerberos-delegation-pose-to-an-organization"></a>Quel risque présente la délégation Kerberos non sécurisée pour une organisation ? 

La délégation Kerberos non sécurisée permet à une entité d’emprunter l’identité de tout autre service choisi. Par exemple, imaginons que vous disposiez d’un site web IIS et que le compte du pool d’applications soit configuré avec une délégation sans contrainte. L’authentification Windows est activée sur le site web IIS, ce qui permet de prendre en charge l’authentification Kerberos native, et le site utilise un serveur SQL Server back-end pour les données métier. Avec votre compte d’administrateur de domaine, vous accédez au site web IIS et vous vous authentifiez auprès de celui-ci. Le site web, utilisant la délégation sans contrainte, peut obtenir un ticket de service d’un contrôleur de domaine au service SQL, et ce, en votre nom.

Le principal problème avec la délégation Kerberos est que vous vous en remettez à l’application pour faire toujours les bons choix. Des acteurs malveillants peuvent donc forcer l’application à commettre des actes inappropriés. Si vous êtes connecté en tant qu’**administrateur de domaine**, le site peut créer un ticket vers un autre service et agir en votre nom, à savoir en tant qu’**administrateur du domaine**. Par exemple, le site peut choisir un contrôleur de domaine et apporter des changements au groupe d’**administrateurs d’entreprise**. De même, le site peut acquérir le hachage du compte KRBTGT ou télécharger un fichier intéressant à partir du service des ressources humaines. Le risque est clair et les possibilités de la délégation non sécurisée sont quasiment illimitées. 

 
## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez le tableau de rapport pour découvrir les entités autres que des contrôleurs de domaine qui sont configurées pour la **délégation Kerberos non sécurisée**.    
    <br>![Évaluation de la sécurité concernant la délégation Kerberos non sécurisée](media/atp-cas-isp-kerberos-delegation-2.png)
1. Prenez les mesures appropriées pour les utilisateurs à risque, par exemple en supprimant leur attribut sans contrainte ou en le remplaçant par une délégation contrainte plus sécurisée.

## <a name="remediation"></a>Mise à jour

Pour en savoir plus sur la correction de ces types de comptes, consultez [Suppression des comptes utilisant une délégation Kerberos sans contrainte](https://blogs.technet.microsoft.com/389thoughts/2017/04/18/get-rid-of-accounts-that-use-kerberos-unconstrained-delegation/).

## <a name="next-steps"></a>Étapes suivantes
- [Filtrage des activités Azure ATP dans Cloud App Security](atp-activities-filtering-mcas.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
