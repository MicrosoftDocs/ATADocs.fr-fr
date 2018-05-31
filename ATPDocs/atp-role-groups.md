---
title: Groupes de rôles Azure - Protection avancée contre les menaces pour la gestion des accès | Microsoft Docs
description: Explique comment utiliser des groupes de rôles Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 77a2464634b4286d2f6d35504e9ab7512cf7b612
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34444771"
---
*S’applique à : Azure - Protection avancée contre les menaces*




# <a name="azure-atp-role-groups"></a>Groupes de rôles Azure ATP

Azure ATP offre la sécurité basée sur les rôles pour protéger les données conformément aux besoins de sécurité et de conformité spécifiques d’une organisation. Azure ATP prend en charge trois rôles distincts : Administrateurs, Utilisateurs et Observateurs. 

> [!NOTE]
> Si vous voulez afficher ou supprimer des données personnelles, veuillez consulter les conseils de Microsoft dans [Microsoft Compliance Manager](https://servicetrust.microsoft.com/ComplianceManager) et dans la [section RGPD du site Conformité de Microsoft 365 Entreprise](https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr). Si vous recherchez des informations générales sur le RGPD, consultez la [section sur le RGPD du portail Service Trust](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

Les groupes de rôles permettent de gérer les accès pour Azure ATP. À l’aide des groupes de rôles, vous pouvez séparer les tâches au sein de votre équipe de sécurité et accorder uniquement le nombre d’accès dont les utilisateurs ont besoin pour effectuer leur travail. Cet article décrit la gestion des accès et l’autorisation de rôle Azure ATP, puis vous aide à configurer des groupes de rôles dans ATP.

> [!NOTE]
> N’importe quel administrateur général ou de la sécurité de l’annuaire Azure Active Directory du locataire est automatiquement un administrateur Azure ATP.

## <a name="accessing-the-workspace-management-portal"></a>Accès au portail de gestion de l’espace de travail

L’accès au portail de gestion de l’espace de travail (portal.atp.azure.com) est possible uniquement par un utilisateur Azure AD qui a le rôle d’annuaire de l’administrateur général ou de la sécurité. Après avoir passé le portail, vous pouvez créer les différents espaces de travail. Pour chaque espace de travail, le service Azure ATP crée trois groupes de sécurité dans votre locataire Azure Active Directory : Administrateurs, Utilisateurs, Observateurs. 

> [!NOTE]
> L’accès au portail de l’espace de travail Azure ATP est accordé uniquement aux utilisateurs au sein de groupes de sécurité Azure AD pour cet espace de travail ainsi qu’aux administrateurs généraux et de sécurité.


## <a name="types-of-azure-atp-security-groups"></a>Types de groupes de sécurité Azure ATP 

Azure ATP présente trois types de groupes de sécurité : Administrateurs *nom de l’espace de travail* Azure ATP, Utilisateurs *nom de l’espace de travail* Azure ATP et Observateurs *nom de l’espace de travail* Azure ATP. Le tableau suivant décrit le type d’accès dans le portail de l’espace de travail Azure ATP disponible par rôle. En fonction du rôle que vous attribuez, différents écrans et options de menu dans le portail de l’espace de travail Azure ATP ne sont pas disponibles, comme suit :

|Activité |Administrateurs *nom de l’espace de travail* Azure ATP|Utilisateurs *nom de l’espace de travail* Azure ATP|Observateurs *nom de l’espace de travail* Azure ATP|
|----|----|----|----|
|Se connecter|Disponible|Disponible|Disponible|
|Modifier l’état des activités suspectes|Disponible|Disponible|Non disponible|
|Partager/exporter une activité suspecte par e-mail/via un lien|Disponible|Disponible|Disponible|
|Modifier l’état de la surveillance des alertes|Disponible|Non disponible|Non disponible|
|Mettre à jour la configuration Azure ATP|Disponible|Non disponible|Non disponible|
|Capteur – Ajouter|Disponible|Non disponible|Non disponible|
|Capteur – Supprimer |Disponible|Non disponible|Non disponible|
|Contrôleur de domaine surveillé - Ajouter |Disponible|Non disponible|Non disponible|
|Contrôleur de domaine surveillé – Supprimer|Disponible|Non disponible|Non disponible|
|Afficher les alertes et les activités suspectes|Disponible|Disponible|Disponible|


Quand les utilisateurs tentent d’accéder à une page qui n’est pas disponible pour leur groupe de rôles, ils sont redirigés vers la page Azure ATP d’accès non autorisé. 

## <a name="add-and-remove-users"></a>Ajouter et supprimer des utilisateurs 

Azure ATP utilise des groupes de sécurité Azure AD comme base pour les groupes de rôles. Les groupes de rôles peuvent être gérés à partir des groupes [ https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All groups).  Seuls des utilisateurs AAD peuvent être ajoutés ou supprimés dans les groupes de sécurité. 


## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement ATA](http://aka.ms/aatpsizingtool)
- [Architecture d’ATA](atp-architecture.md)
- [Installer ATA](install-atp-step1.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)

