---
title: Groupes de rôles Azure-protection avancée contre les menaces pour la gestion des accès
description: Explique comment utiliser des groupes de rôles Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bd5a9cf3ffe32bb522d1096e089fdad263b3fcb4
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828399"
---
# <a name="azure-atp-role-groups"></a>Groupes de rôles Azure ATP

Azure ATP offre la sécurité basée sur les rôles pour protéger les données conformément aux besoins de sécurité et de conformité spécifiques d’une organisation. Azure ATP prend en charge trois rôles distincts : Administrateurs, Utilisateurs et Observateurs.

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Les groupes de rôles permettent de gérer les accès pour Azure ATP. À l’aide des groupes de rôles, vous pouvez séparer les tâches au sein de votre équipe de sécurité et accorder uniquement le nombre d’accès dont les utilisateurs ont besoin pour effectuer leur travail. Cet article explique la gestion des accès et l’autorisation des rôles Azure ATP, et vous aide à configurer des groupes de rôles dans Azure ATP.

> [!NOTE]
> N’importe quel administrateur général ou de la sécurité de l’annuaire Azure Active Directory du locataire est automatiquement un administrateur Azure ATP.

## <a name="accessing-the-azure-atp-portal"></a>Accès au portail Azure ATP

L’accès au portail Azure ATP (portal.atp.azure.com) est possible seulement par un utilisateur Azure AD qui a le rôle d’annuaire d’administrateur général ou de sécurité. Après être entré dans le portail avec le rôle requis, vous pouvez créer votre instance Azure ATP. Le service Azure ATP crée trois groupes de sécurité dans votre locataire Azure Active Directory : Administrateurs, Utilisateurs, Observateurs.

> [!NOTE]
> L’accès au portail Azure ATP est accordé uniquement aux utilisateurs appartenant aux groupes de sécurité Azure ATP, à votre annuaire Azure Active Directory ainsi qu’aux administrateurs généraux et de sécurité du locataire.

## <a name="types-of-azure-atp-security-groups"></a>Types de groupes de sécurité Azure ATP

Azure ATP propose trois types de groupe de sécurité : Administrateurs *(nom de l’instance)* Azure ATP, Utilisateurs *(nom de l’instance)* Azure ATP et Observateurs *(nom de l’instance)* Azure ATP. Le tableau suivant décrit le type d’accès dans le portail Azure ATP disponible pour chaque rôle. En fonction du rôle que vous affectez, différents écrans et options de menu ne sont pas disponibles dans le portail Azure ATP, comme suit :

|Activité |Administrateurs *de Azure ATP (nom de l’instance)*|Utilisateurs du Azure ATP *(nom de l’instance)*|Visionneuses Azure ATP *(nom de l’instance)*|
|----|----|----|----|
|Modifier l’état des alertes d’intégrité|Disponible|Non disponible|Non disponible|
|Changer l’état des alertes de sécurité (rouvrir, fermer, exclure, supprimer)|Disponible|Disponible|Non disponible|
|Supprimer l'instance|Disponible|Non disponible|Non disponible|
|Télécharger un rapport|Disponible|Disponible|Disponible|
|Connexion|Disponible|Disponible|Disponible|
|Partager/exporter les alertes de sécurité (via e-mail, obtenir un lien, télécharger les détails)|Disponible|Disponible|Disponible|
|Mettre à jour la configuration d’Azure ATP - Mises à jour|Disponible|Non disponible|Non disponible|
|Mettre à jour la configuration d’ATP - Étiquettes d’entité (sensible et honeytoken)|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration d’Azure ATP - Exclusions|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration d’Azure ATP - Langue|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration d’ATP - Notifications (e-mail et Syslog)|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration d’Azure ATP - Aperçu des détections|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration d’ATP - Rapports planifiés|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration d’Azure ATP - Sources de données (services d’annuaire, SIEM, VPN WD-ATP)|Disponible|Non disponible|Non disponible|
|Mettre à jour la configuration d’Azure ATP - Capteurs (télécharger, regénérer la clé, configurer, supprimer)|Disponible|Non disponible|Non disponible|
|Afficher les profils d’entité et les alertes de sécurité|Disponible|Disponible|Disponible|

Quand les utilisateurs tentent d’accéder à une page qui n’est pas disponible pour leur groupe de rôles, ils sont redirigés vers la page Azure ATP d’accès non autorisé.

## <a name="add-and-remove-users"></a>Ajouter et supprimer des utilisateurs

Azure ATP utilise des groupes de sécurité Azure AD comme base pour les groupes de rôles. Les groupes de rôles peuvent être gérés à partir de [https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups) . Seuls des utilisateurs Azure AD peuvent être ajoutés ou supprimés dans les groupes de sécurité.

## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement ATP](https://aka.ms/aatpsizingtool)
- [Architecture ATP](architecture.md)
- [Installer Azure ATP](install-step1.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)