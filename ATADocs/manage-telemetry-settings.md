---
title: Gérer les journaux générés par le système Advanced Threat Analytics | Microsoft Docs
description: Décrit les données collectées par ATA et explique comment désactiver la collecte de données.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7f1a0cb9a7e237259a9b77b96e16c6680336c2b0
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34444516"
---
*S’applique à : Advanced Threat Analytics version 1.9*



# <a name="manage-system-generated-logs-note"></a>Gérer les journaux générés par le système>[!NOTE]
> Si vous voulez afficher ou supprimer des données personnelles, veuillez consulter les conseils de Microsoft dans [Microsoft Compliance Manager](https://servicetrust.microsoft.com/ComplianceManager) et dans la [section RGPD du site Conformité de Microsoft 365 Entreprise](https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr). Si vous recherchez des informations générales sur le RGPD, consultez la [section sur le RGPD du portail Service Trust](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).


ATA (Advanced Threat Analytics) collecte des données de journaux générés par le système rendues anonymes sur ATA et les transmet via une connexion HTTPS aux serveurs Microsoft.  Ces données sont utilisées par Microsoft pour améliorer les futures versions d’ATA.

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

    -   Nombre d’utilisateurs

-   Activités suspectes : les données rendues anonymes suivantes sont collectées pour chaque activité suspecte :

    (Les noms d’ordinateurs, noms d’utilisateurs et adresses IP ne sont **pas** collectés)

    -   Type d’activité suspecte

    -   ID d’activité suspecte

    -   État

    -   Heures de début et de fin

    -   Entrée fournie

- Problèmes d’intégrité – Les données anonymes suivantes sont collectées pour chaque problème d’intégrité :

    (Les noms d’ordinateurs, les noms d’utilisateurs et les adresses IP ne sont pas collectés.)

    -   Type de problème d’intégrité

    -   ID du problème d’intégrité

    -   État

    -   Heures de début et de fin

- Adresses URL de la console ATA - Adresses URL lors de l’utilisation de la console ATA, c’est-à-dire quelles pages de la console ATA sont consultées.


### <a name="disable-data-collection"></a>Désactiver la collecte de données
Procédez comme suit pour arrêter la collecte et l’envoi de données de télémétrie à Microsoft :

1.  Connectez-vous à la console ATA, cliquez sur les trois points dans la barre d’outils, puis sélectionnez **À propos de**.

2.  Décochez la case **Envoyez-nous des informations d’utilisation pour nous aider à améliorer votre expérience utilisateur à l’avenir**.

## <a name="see-also"></a>Voir aussi
- [Résolution des problèmes liés à ATA à l’aide du journal des événements](troubleshooting-ata-using-logs.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
