---
title: Gérer les journaux générés par le système Advanced Threat Analytics
description: Décrit les données collectées par ATA et explique comment désactiver la collecte de données.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 8/19/2018
ms.topic: article
ms.prod: advanced-threat-analytics
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c17405cd1f3da619ad6942e082420e58c4e9c430
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84775129"
---
# <a name="manage-system-generated-logs"></a>Gérer les journaux générés par le système

*S’applique à : Advanced Threat Analytics version 1.9*

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

 > [!NOTE]
 > ATA (Advanced Threat Analytics) collecte des données de journaux générés par le système rendues anonymes sur ATA et les transmet via une connexion HTTPS aux serveurs Microsoft. Ces données sont utilisées par Microsoft pour améliorer les futures versions d’ATA.

## <a name="data-collected"></a>Données collectées

Les données rendues anonymes collectées incluent les paramètres suivants :

-   Compteurs de performances du centre ATA et de la passerelle ATA

-   ID de produit des copies sous licence d’ATA

-   Date de déploiement du centre ATA

-   Nombre de passerelles ATA déployées

-   Informations Active Directory rendues anonymes suivantes :

    -   ID du domaine dont le nom correspond au premier domaine lors d’un tri par ordre alphabétique

    -   Nombre de contrôleurs de domaine

    -   Nombre de contrôleurs de domaine surveillés par ATA via la mise en miroir des ports

    -   Nombre de sites

    -   Nombre d’ordinateurs

    -   Nombre de groupes

    -   Nombre d'utilisateurs

-   Activités suspectes : les données rendues anonymes suivantes sont collectées pour chaque activité suspecte :

    (Les noms d’ordinateur, les noms d’utilisateur et les adresses IP ne sont **pas** collectés)

    -   Type d’activité suspecte

    -   ID d’activité suspecte

    -   Statut

    -   Heures de début et de fin

    -   Entrée fournie

- Problèmes d’intégrité – Les données anonymes suivantes sont collectées pour chaque problème d’intégrité :

    (Les noms d’ordinateurs, les noms d’utilisateurs et les adresses IP ne sont pas collectés.)

    -   Type de problème d’intégrité

    -   ID du problème d’intégrité

    -   Statut

    -   Heures de début et de fin

- Adresses URL de la console ATA - Adresses URL lors de l’utilisation de la console ATA, c’est-à-dire quelles pages de la console ATA sont consultées.


### <a name="disable-data-collection"></a>Désactiver la collecte de données
Procédez comme suit pour arrêter la collecte et l’envoi de données de télémétrie à Microsoft :

1.  Connectez-vous à la console ATA, cliquez sur les trois points dans la barre d’outils, puis sélectionnez **À propos de**.

2.  Décochez la case **Envoyez-nous des informations d’utilisation pour nous aider à améliorer votre expérience utilisateur à l’avenir**.

## <a name="see-also"></a>Voir aussi
- [Résolution des problèmes liés à ATA à l’aide du journal des événements](troubleshooting-ata-using-logs.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
