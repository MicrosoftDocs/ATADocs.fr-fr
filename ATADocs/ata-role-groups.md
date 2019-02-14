---
title: Groupes de rôles Advanced Threat Analytics pour la gestion des accès | Microsoft Docs
description: Explique comment utiliser des groupes de rôles ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 99b047305ee0638123f0ef22d9752ca10a6b7a96
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076672"
---
# <a name="ata-role-groups"></a>Groupes de rôles ATA


*S’applique à : Advanced Threat Analytics version 1.9*

Les groupes de rôles permettent de gérer l’accès pour ATA. À l’aide des groupes de rôles, vous pouvez séparer les tâches au sein de votre équipe de sécurité et accorder uniquement le nombre d’accès dont les utilisateurs ont besoin pour effectuer leur travail. Cet article explique ce qu’est la gestion des accès et l’autorisation de rôle ATA, puis vous aide à configurer des groupes de rôles dans ATA.

> [!NOTE]
> Tout administrateur local du Centre ATA est automatiquement administrateur Microsoft Advanced Threat Analytics.

## <a name="types-of-ata-role-groups"></a>Types de groupes de rôles ATA 

ATA présente trois types de groupes de rôles : Administrateurs ATA, Utilisateurs ATA et Observateurs ATA. Le tableau suivant décrit le type d’accès dans ATA disponible par rôle. En fonction du rôle que vous attribuez, différents écrans et options de menu dans ATA ne sont pas disponibles, comme suit :

|Activité |Administrateurs Microsoft Advanced Threat Analytics|Utilisateurs Microsoft Advanced Threat Analytics|Observateurs Microsoft Advanced Threat Analytics|
|----|----|----|----|
|Se connecter|Disponible|Disponible|Disponible|
|Fournir des commentaires sur les activités suspectes|Disponible|Disponible|Non disponible|
|Modifier l’état des activités suspectes|Disponible|Disponible|Non disponible|
|Partager/exporter une activité suspecte par e-mail/via un lien|Disponible|Disponible|Non disponible|
|Modifier l’état de la surveillance des alertes|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration ATA|Disponible|Non disponible|Non disponible|
|Passerelle – Ajouter|Disponible|Non disponible|Non disponible|
|Passerelle – Supprimer |Disponible|Non disponible|Non disponible|
|Contrôleur de domaine surveillé - Ajouter |Disponible|Non disponible|Non disponible|
|Contrôleur de domaine surveillé – Supprimer|Disponible|Non disponible|Non disponible|
|Afficher les alertes et les activités suspectes|Disponible|Disponible|Disponible|


Quand les utilisateurs tentent d’accéder à une page qui n’est pas disponible pour leur groupe de rôles, ils sont redirigés vers la page ATA d’accès non autorisé. 

## <a name="add--remove-users---ata-role-groups"></a>Ajouter \ supprimer des utilisateurs - Groupes de rôles ATA 

ATA utilise les groupes Windows locaux comme base pour les groupes de rôles. Les groupes de rôles doivent être gérés sur le serveur du centre ATA.
Pour ajouter ou supprimer des utilisateurs, utilisez la console MMC **Utilisateurs et groupes locaux** (Lusrmgr.msc). Sur un ordinateur joint à un domaine, vous pouvez ajouter des comptes de domaine et des comptes locaux. 

