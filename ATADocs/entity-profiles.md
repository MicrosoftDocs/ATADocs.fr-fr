---
title: Utilisation des profils d’entité dans la console Advanced Threat Analytics
description: Décrit comment investiguer des entités à partir de l’écran des profils utilisateur dans la console ATA
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 581a3257-32dc-453f-b84e-b9f99186f5d3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3b2e2d5a9eee8d18b6d182afb15453a8809db605
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84775401"
---
# <a name="investigating-entity-profiles"></a>Enquête sur les profils d’entité


*S’applique à : Advanced Threat Analytics version 1.9*

Le profil d’entité vous fournit un tableau de bord conçu pour des investigations approfondies sur les utilisateurs, les ordinateurs, les appareils et les ressources auxquelles ils ont accès et leur historique. La page de profil tire parti du nouveau traducteur d’activité logique ATA qui peut examiner un groupe d’activités en cours (agrégées jusqu'à une minute) et les regrouper en une seule activité logique pour vous permettre de mieux comprendre les activités réelles de vos utilisateurs.

Pour accéder à une page de profil d’entité, cliquez sur le nom de l’entité, par exemple sur son nom d’utilisateur, dans la chronologie des activités suspectes.

Le menu de gauche vous fournit toutes les informations Active Directory disponibles sur l’entité – adresse e-mail, domaine, date à laquelle elle a été vue pour la première fois. Si l’entité est sensible, il vous indique pourquoi. Par exemple, l’utilisateur est-il marqué comme sensible ou membre d’un groupe sensible ?
Si l’utilisateur est sensible, vous voyez l’icône sous le nom de l’utilisateur.

## <a name="view-entity-activities"></a>Afficher les activités de l’entité

Pour afficher toutes les activités effectuées par l’utilisateur ou effectuées sur une entité, cliquez sur l’onglet **Activités**. 

 ![activités du profil utilisateur](media/user-profile-activities.png)

Par défaut, le volet principal du profil d’entité affiche une chronologie des activités de l’entité avec un historique pouvant couvrir jusqu’aux 6 derniers mois. Ce dernier vous permet d’explorer les entités auxquelles l’utilisateur a accédé ou, pour une entité, les utilisateurs ayant accédé à l’entité.

En haut, vous pouvez voir les vignettes de résumé qui vous donnent un petit aperçu de ce que vous devez rapidement comprendre sur votre entité. Ces vignettes varient selon le type d’entité. Pour un utilisateur, vous verrez :
- Le nombre d’activités suspectes ouvertes pour l’utilisateur
- Le nombre d’ordinateurs auxquels l’utilisateur s’est connecté
- Le nombre de ressources auxquelles l’utilisateur a accédé
- À partir de quels emplacements l’utilisateur s’est connecté au VPN

  ![menu des entités](media/entity-menu.png)

Pour les ordinateurs, vous verrez :
- Le nombre d’activités suspectes ouvertes pour l’ordinateur
-  Le nombre d’utilisateurs connectés à l’ordinateur
- Le nombre de ressources auxquelles l’ordinateur a accédé
-  Le nombre d’emplacements sur l’ordinateur à partir desquels un accès au VPN a été effectué
- La liste des adresses IP que l’ordinateur a utilisées
  
  ![ordinateur de menu des entités](media/entity-computer.png)

À l’aide du bouton **Filtrer par**, situé au-dessus de la chronologie des activités, vous pouvez filtrer les activités par type d’activité. Vous pouvez également éliminer par filtrage un type spécifique (bruyant) d’activité. C’est vraiment utile pour votre investigation lorsque vous voulez comprendre les bases de ce que fait une entité sur le réseau. Vous pouvez également accéder à une date spécifique et exporter vers Excel les activités filtrées. Le fichier exporté fournit une page pour les modifications des services d’annuaire (éléments ayant changé dans Active Directory pour ce compte) et une page distincte pour les activités. 

## <a name="view-directory-data"></a>Consulter les données d'annuaire

L’onglet **Données de l'annuaire** fournit les informations statiques disponibles à partir d’Active Directory, y compris les indicateurs de sécurité de contrôle d’accès utilisateur. ATA affiche également les appartenances aux groupes de l’utilisateur pour vous permettre de dire si l’utilisateur a une appartenance directe ou une appartenance récursive. Pour les groupes, ATA liste les membres du groupe.

 ![données d’annuaire du profil utilisateur](media/user-profile-dir-data.png)

Dans la section **Contrôle d’accès d’utilisateur**, ATA expose les paramètres de sécurité pouvant demander votre attention. Vous pouvez voir des indicateurs importants sur l’utilisateur, indiquant par exemple si l’utilisateur peut appuyer sur Entrée pour contourner le mot de passe, si l’utilisateur a un mot de passe qui n’expire jamais, etc. 

## <a name="view-lateral-movement-paths"></a>Visualiser les chemins de mouvement latéral

En cliquant sur l’onglet **Chemins d'accès de mouvement latéral**, vous pouvez afficher une image entièrement interactive et dynamique offrant une représentation visuelle des chemins de mouvement latéral en direction et en provenance de cet utilisateur qui peuvent être utilisés pour infiltrer votre réseau.

Cette image vous fournit le nombre de tronçons entre ordinateurs ou utilisateurs qu’un attaquant aurait en direction et en provenance de cet utilisateur pour compromettre un compte sensible. De plus, si l’utilisateur lui-même a un compte sensible, vous pouvez voir combien de ressources et de comptes sont directement connectés. Pour plus d’informations, consultez [chemins de mouvement latéral](use-case-lateral-movement-path.md). 

 ![chemins de mouvement latéral du profil utilisateur](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
      