---
title: Groupes de rôles Azure - Protection avancée contre les menaces pour la gestion des accès | Microsoft Docs
description: Explique comment utiliser des groupes de rôles Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/29/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bb577283303437db1e524f1e1f5a112be2bb8bcf
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54458697"
---
# <a name="azure-atp-role-groups"></a>Groupes de rôles Azure ATP

Azure ATP offre la sécurité basée sur les rôles pour protéger les données conformément aux besoins de sécurité et de conformité spécifiques d’une organisation. Azure ATP gère trois rôles distincts : Administrateurs, Utilisateurs et Observateurs. 

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Les groupes de rôles permettent de gérer les accès pour Azure ATP. À l’aide des groupes de rôles, vous pouvez séparer les tâches au sein de votre équipe de sécurité et accorder uniquement le nombre d’accès dont les utilisateurs ont besoin pour effectuer leur travail. Cet article explique la gestion des accès et l’autorisation des rôles Azure ATP, et vous aide à configurer des groupes de rôles dans Azure ATP.

> [!NOTE]
> N’importe quel administrateur général ou de la sécurité de l’annuaire Azure Active Directory du locataire est automatiquement un administrateur Azure ATP.

## <a name="accessing-the-azure-atp-portal"></a>Accès au portail Azure ATP

L’accès au portail Azure ATP (portal.atp.azure.com) est possible seulement par un utilisateur Azure AD qui a le rôle d’annuaire d’administrateur général ou de sécurité. Après être entré dans le portail avec le rôle requis, vous pouvez créer votre instance Azure ATP. Le service Azure ATP crée trois groupes de sécurité dans le client Azure Active Directory : Administrateurs, Utilisateurs et Observateurs. 

> [!NOTE]
> L’accès au portail Azure ATP est accordé uniquement aux utilisateurs appartenant aux groupes de sécurité Azure ATP, à votre annuaire Azure Active Directory ainsi qu’aux administrateurs généraux et de sécurité du locataire.


## <a name="types-of-azure-atp-security-groups"></a>Types de groupes de sécurité Azure ATP 

Azure ATP propose trois types de groupes de sécurité : Administrateurs *(nom de l’instance)* Azure ATP, Utilisateurs *(nom de l’instance)* Azure ATP et Observateurs *(nom de l’instance)* Azure ATP. Le tableau suivant décrit le type d’accès dans le portail Azure ATP disponible pour chaque rôle. En fonction du rôle que vous affectez, différents écrans et options de menu ne sont pas disponibles dans le portail Azure ATP, comme suit :

|Activité |Administrateurs *(nom de l’instance)* Azure ATP|Utilisateurs *(nom de l’instance)* Azure ATP|Observateurs *(nom de l’instance)* Azure ATP|
|----|----|----|----|
|Se connecter|Disponible|Disponible|Disponible|
|Changer l’état des alertes de sécurité (rouvrir, fermer, exclure, supprimer)|Disponible|Disponible|Non disponible|
|Partager/exporter les alertes de sécurité (via e-mail, obtenir un lien, télécharger les détails)|Disponible|Disponible|Disponible|
|Télécharger un rapport|Disponible|Disponible|Disponible|
|Modifier l’état de la surveillance des alertes|Disponible|Non disponible|Non disponible|
|Mettre à jour la configuration d’Azure ATP - Capteurs (télécharger, regénérer la clé, configurer, supprimer)|Disponible|Non disponible|Non disponible|
|Mettre à jour la configuration d’Azure ATP - Sources de données (services d’annuaire, SIEM, VPN WD-ATP)|Disponible|Non disponible|Non disponible|
|Mettre à jour la configuration d’Azure ATP - Mises à jour|Disponible|Non disponible|Non disponible|
|Mettre à jour la configuration d’ATP - Rapports planifiés|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration d’ATP - Étiquettes d’entité (sensible et honeytoken)|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration d’Azure ATP - Exclusions|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration d’Azure ATP - Langue|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration d’ATP - Notifications (e-mail et Syslog)|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration d’Azure ATP - Aperçu des détections|Disponible|Disponible|Non disponible|
|Afficher les profils d’entité et les alertes de sécurité|Disponible|Disponible|Disponible|


Quand les utilisateurs tentent d’accéder à une page qui n’est pas disponible pour leur groupe de rôles, ils sont redirigés vers la page Azure ATP d’accès non autorisé. 

## <a name="add-and-remove-users"></a>Ajouter et supprimer des utilisateurs 


Azure ATP utilise des groupes de sécurité Azure AD comme base pour les groupes de rôles. Les groupes de rôles peuvent être gérés depuis [ https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups). Seuls des utilisateurs Azure AD peuvent être ajoutés ou supprimés dans les groupes de sécurité. 

## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement ATP](http://aka.ms/aatpsizingtool)
- [Architecture ATP](atp-architecture.md)
- [Installer Azure ATP](install-atp-step1.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)

