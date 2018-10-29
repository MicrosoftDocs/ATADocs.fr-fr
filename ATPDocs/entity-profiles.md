---
title: Utilisation des profils utilisateur dans le portail d’espace de travail Azure - Protection avancée contre les menaces | Microsoft Docs
description: Décrit comment enquêter sur les utilisateurs à partir de l’écran des profils utilisateur dans le portail d’espace de travail Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 17458706-79fb-4c23-aa42-66979164a45f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 357973698d9d53936c3fa308bc0021ae1cd98f60
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783506"
---
*S’applique à : Azure Advanced Threat Protection*



# <a name="understanding-entity-profiles"></a>Présentation des profils d’entité

Le profil d’entité fournit une page complète sur l’entité, qui permet une enquête approfondie sur les utilisateurs, les ordinateurs, les périphériques et les ressources auxquelles ils ont accès et leur historique. La page de profil tire parti du nouveau traducteur d’activité logique Azure ATP qui peut examiner un groupe d’activités en cours (agrégées jusqu'à une minute) et les regrouper en une seule activité logique pour vous permettre de mieux comprendre les activités réelles de vos utilisateurs.

Pour accéder à une page de profil d’entité, cliquez sur le nom de l’entité, par exemple sur son nom d’utilisateur, dans la chronologie des activités suspectes.

Le menu de gauche vous fournit toutes les informations Active Directory disponibles sur l’entité – adresse e-mail, domaine, date à laquelle elle a été vue pour la première fois. Si l’entité est sensible, il vous indique pourquoi. Par exemple, l’utilisateur est-il marqué comme sensible ou membre d’un groupe sensible ?
Si l’utilisateur est sensible, vous voyez l’icône sous le nom de l’utilisateur.

## <a name="view-entity-activities"></a>Afficher les activités de l’entité

Pour afficher toutes les activités effectuées par l’utilisateur ou effectuées sur une entité, cliquez sur l’onglet **Activités**. 

 ![activités du profil utilisateur](media/user-profile-activities.png)

Par défaut, le volet principal du profil d’entité affiche une chronologie des activités de l’entité avec un historique pouvant couvrir jusqu’aux six derniers mois. Ce dernier vous permet d’explorer les entités auxquelles l’utilisateur a accédé ou, pour une entité, les utilisateurs ayant accédé à l’entité.

En haut, vous pouvez afficher les vignettes de résumé qui vous donnent une vue d’ensemble rapide de ce que vous devez comprendre en un coup d’œil sur votre entité – le nombre de machines auxquelles l’utilisateur s’est connecté, le nombre de ressources auxquelles il a accédé et les emplacements à partir desquels un utilisateur s’est connecté au VPN (si configuré). 

À l’aide du bouton **Filtrer par**, situé au-dessus de la chronologie des activités, vous pouvez filtrer les activités par type d’activité. Vous pouvez également éliminer par filtrage un type spécifique (bruyant) d’activité. Cela est utile pour enquêter lorsque vous voulez comprendre les bases de ce que fait une entité sur le réseau. Vous pouvez également accéder à une date spécifique et exporter vers Excel les activités filtrées. Le fichier exporté fournit une page pour les modifications des services d’annuaire (éléments ayant changé dans Active Directory pour ce compte) et une page distincte pour les activités. 

## <a name="view-directory-data"></a>Consulter les données d'annuaire

L’onglet **Données de l'annuaire** fournit les informations statiques disponibles à partir d’Active Directory, y compris les indicateurs de sécurité de contrôle d’accès utilisateur. Azure ATP affiche également les appartenances aux groupes de l’utilisateur pour vous permettre de dire si l’utilisateur a une appartenance directe ou une appartenance récursive. Pour les groupes, Azure ATP répertorie les membres du groupe.

 ![données d’annuaire du profil utilisateur](media/user-profile-dir-data.png)

Dans la section **Contrôle d’accès d’utilisateur**, Azure ATP expose les paramètres de sécurité pouvant requérir votre attention. Vous pouvez voir des indicateurs importants sur l’utilisateur, indiquant par exemple si l’utilisateur peut appuyer sur Entrée pour contourner le mot de passe, si l’utilisateur a un mot de passe qui n’expire jamais, etc. 

## <a name="view-lateral-movement-paths"></a>Visualiser les chemins de mouvement latéral

En cliquant sur l’onglet Chemins d'accès de mouvement latéral, vous pouvez afficher une image entièrement interactive et dynamique offrant une représentation visuelle des chemins de mouvement latéral en direction et en provenance de cet utilisateur qui peuvent être utilisés pour infiltrer votre réseau.

Cette image vous fournit le nombre de tronçons entre ordinateurs ou utilisateurs qu’un attaquant aurait en direction et en provenance de cet utilisateur pour compromettre un compte sensible. De plus, si l’utilisateur a un compte sensible, vous pouvez voir combien de ressources et de comptes sont directement connectés.

Si l’activité n’est pas détectée au cours des deux derniers jours, le graphe n’apparaît plus. Toutefois, le [rapport des chemins de mouvement latéral](reports.md) vous fournit des informations sur les chemins de mouvement latéral qui ont été détectés au cours des 60 derniers jours. 

Pour plus d’informations, consultez [Chemins de mouvement latéral](use-case-lateral-movement-path.md). 

 ![chemins de mouvement latéral du profil utilisateur](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Voir aussi

- [Examiner les chemins de mouvement latéral avec Azure ATP](use-case-lateral-movement-path.md)
- [Consulter le forum Azure ATP](https://aka.ms/azureatpcommunity)