---
title: Microsoft Defender pour les groupes de rôles d’identité pour la gestion des accès
description: Vous guide tout au long de l’utilisation de Microsoft Defender pour les groupes de rôles d’identité.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 269343e6cdc5ceba875d5b6de1c740415a862eca
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275314"
---
# <a name="product-long-role-groups"></a>[!INCLUDE [Product long](includes/product-long.md)] groupes de rôles

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[!INCLUDE [Product long](includes/product-long.md)] offre une sécurité basée sur les rôles pour protéger les données en fonction des besoins spécifiques d’une organisation en matière de sécurité et de conformité. [!INCLUDE [Product short](includes/product-short.md)] prise en charge de trois rôles distincts : administrateurs, utilisateurs et visionneuses.

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Les groupes de rôles permettent la gestion des accès pour [!INCLUDE [Product short](includes/product-short.md)] . À l’aide des groupes de rôles, vous pouvez séparer les tâches au sein de votre équipe de sécurité et accorder uniquement le nombre d’accès dont les utilisateurs ont besoin pour effectuer leur travail. Cet article explique la gestion des accès, l' [!INCLUDE [Product short](includes/product-short.md)] autorisation des rôles et vous permet d’être opérationnel avec les groupes de rôles dans [!INCLUDE [Product short](includes/product-short.md)] .

> [!NOTE]
> Tout administrateur général ou administrateur de la sécurité sur le Azure Active Directory du locataire est automatiquement un [!INCLUDE [Product short](includes/product-short.md)] administrateur.

## <a name="accessing-the-product-short-portal"></a>Accès au [!INCLUDE [Product short](includes/product-short.md)] portail

L’accès au [!INCLUDE [Product short](includes/product-short.md)] portail (Portal.ATP.Azure.com) ne peut être effectué que par un utilisateur Azure ad disposant du rôle d’annuaire administrateur général ou administrateur de sécurité. Après avoir entré le portail avec le rôle requis, vous pouvez créer votre [!INCLUDE [Product short](includes/product-short.md)] instance. [!INCLUDE [Product short](includes/product-short.md)] le service crée trois groupes de sécurité dans votre Azure Active Directory locataire : administrateurs, utilisateurs, observateurs.

> [!NOTE]
> L’accès au [!INCLUDE [Product short](includes/product-short.md)] portail est accordé uniquement aux utilisateurs au sein des [!INCLUDE [Product short](includes/product-short.md)] groupes de sécurité, au sein de votre Azure Active Directory, ainsi qu’aux administrateurs globaux et de sécurité du utilisateurs locataires.

## <a name="types-of-product-short-security-groups"></a>Types de [!INCLUDE [Product short](includes/product-short.md)] groupes de sécurité

[!INCLUDE [Product short](includes/product-short.md)] fournit trois types de groupes de sécurité : les administrateurs Azure ATP *(nom de l’instance)* , les utilisateurs Azure ATP *(nom de l’instance)* et les visionneuses Azure ATP *(nom* de l’instance). Le tableau suivant décrit le type d’accès dans le [!INCLUDE [Product short](includes/product-short.md)] portail disponible pour chaque rôle. Selon le rôle que vous attribuez, différents écrans et options de menu dans le [!INCLUDE [Product short](includes/product-short.md)] portail ne sont pas disponibles pour ces utilisateurs, comme suit :

|Activité |Administrateurs *de Azure ATP (nom de l’instance)*|Utilisateurs du Azure ATP *(nom de l’instance)*|Visionneuses Azure ATP *(nom de l’instance)*|
|----|----|----|----|
|Modifier l’état des alertes d’intégrité|Disponible|Non disponible|Non disponible|
|Changer l’état des alertes de sécurité (rouvrir, fermer, exclure, supprimer)|Disponible|Disponible|Non disponible|
|Supprimer l'instance|Disponible|Non disponible|Non disponible|
|Télécharger un rapport|Disponible|Disponible|Disponible|
|Connexion|Disponible|Disponible|Disponible|
|Partager/exporter les alertes de sécurité (via e-mail, obtenir un lien, télécharger les détails)|Disponible|Disponible|Disponible|
|Configuration des mises à jour [!INCLUDE [Product short](includes/product-short.md)] -mises à jour|Disponible|Non disponible|Non disponible|
|Configuration de la mise à jour [!INCLUDE [Product short](includes/product-short.md)] -balises d’entité (sensitive et honeytoken)|Disponible|Disponible|Non disponible|
|Configuration de la mise à jour [!INCLUDE [Product short](includes/product-short.md)] -exclusions|Disponible|Disponible|Non disponible|
|Configuration de la mise à jour [!INCLUDE [Product short](includes/product-short.md)] -langue|Disponible|Disponible|Non disponible|
|Configuration de la mise à jour [!INCLUDE [Product short](includes/product-short.md)] -notifications (e-mail et syslog)|Disponible|Disponible|Non disponible|
|Configuration de la mise à jour [!INCLUDE [Product short](includes/product-short.md)] -aperçu des détections|Disponible|Disponible|Non disponible|
|Configuration de la mise à jour [!INCLUDE [Product short](includes/product-short.md)] -rapports planifiés|Disponible|Disponible|Non disponible|
|Configuration de la mise à jour [!INCLUDE [Product short](includes/product-short.md)] -sources de données (services d’annuaire, Siem, VPN WD-ATP)|Disponible|Non disponible|Non disponible|
|Configuration de la mise à jour [!INCLUDE [Product short](includes/product-short.md)] -capteurs (Télécharger, régénérer la clé, configurer, supprimer)|Disponible|Non disponible|Non disponible|
|Afficher les profils d’entité et les alertes de sécurité|Disponible|Disponible|Disponible|

Lorsque les utilisateurs essaient d’accéder à une page qui n’est pas disponible pour leur groupe de rôles, ils sont redirigés vers la [!INCLUDE [Product short](includes/product-short.md)] page non autorisée.

## <a name="add-and-remove-users"></a>Ajouter et supprimer des utilisateurs

[!INCLUDE [Product short](includes/product-short.md)] utilise des groupes de sécurité Azure AD comme base pour les groupes de rôles. Les groupes de rôles peuvent être gérés à partir de la [page de gestion des groupes](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups). Seuls des utilisateurs Azure AD peuvent être ajoutés ou supprimés dans les groupes de sécurité.

## <a name="see-also"></a>Voir aussi

- [[!INCLUDE [Product short](includes/product-short.md)] outil de dimensionnement](https://aka.ms/aatpsizingtool)
- [[!INCLUDE [Product short](includes/product-short.md)] SOA](architecture.md)
- [Installer [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Consultez le [!INCLUDE [Product short](includes/product-short.md)] Forum !](https://aka.ms/MDIcommunity)
