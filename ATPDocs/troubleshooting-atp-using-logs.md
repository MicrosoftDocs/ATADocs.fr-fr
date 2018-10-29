---
title: Résolution des problèmes Azure Advanced Threat Protection à l’aide des journaux | Microsoft Docs
description: Décrit comment utiliser les journaux Azure ATP pour résoudre des problèmes
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de796346-647d-48e1-970a-8f072e990f1e
ms.reviewer: ''
ms.suite: ''
ms.openlocfilehash: 2cd1d7b070818044e74838178b0fab5838ab46ef
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783251"
---
*S’applique à : Advanced Threat Protection*



# <a name="troubleshooting-azure-advanced-threat-protection-atp-sensor-using-the-atp-logs"></a>Résolution des problèmes du capteur Azure Advanced Threat Protection (ATP) à l’aide des journaux ATP
Les journaux ATP donnent des informations sur ce que fait chaque composant du capteur Azure ATP à n’importe quel moment.


Les journaux Azure ATP se trouvent dans le sous-dossier nommé **Logs** où ATP est installé ; l’emplacement par défaut est : **C:\Program Files\Azure Advanced Threat Protection Sensor\\**. Dans l’emplacement de l’installation par défaut, il se trouve ici : **C:\Program Files\Azure Advanced Threat Protection Sensor\numéro de version\Logs**.

Le capteur Azure ATP dispose des journaux suivants :

-   **Microsoft.Tri.Sensor.log** : ce journal contient tout ce qui se produit dans le capteur Azure ATP (y compris les erreurs et la résolution). Son utilisation principale consiste à obtenir l’état général de toutes les opérations dans l’ordre chronologique dans lequel elles se sont produites.

-   **Microsoft.Tri.Sensor-Resolution.log** : ce journal contient les détails de la résolution des entités visibles dans le trafic par le capteur ATP. Son utilisation principale consiste à examiner les problèmes de résolution des entités.

-   **Microsoft.Tri.Sensor-Errors.log** : ce journal contient uniquement les erreurs interceptées par le capteur ATP. Son utilisation principale consiste à exécuter des vérifications d’intégrité et à examiner les problèmes qui doivent être mis en corrélation avec des heures spécifiques.

-   **Microsoft.Tri.Sensor.Updater.log** : ce journal est utilisé pour le processus de mise à jour de capteur, qui est responsable de la mise à jour automatique du capteur ATP s’il est configuré. 


> [!NOTE]
> Les trois premiers fichiers journaux ont une taille maximale de 50 Mo. Quand cette taille est atteinte, un nouveau fichier journal est ouvert et le précédent est renommé en « &lt;nom_fichier_origine&gt;-Archive-00000 » où le nombre augmente chaque fois qu’il est renommé. Par défaut, s’il existe déjà plus de 10 fichiers du même type, les plus anciens sont supprimés.

## <a name="azure-atp-deployment-logs"></a>Journaux de déploiement Azure ATP
Les journaux de déploiement Azure ATP se trouvent dans le répertoire temp de l’utilisateur qui a installé le produit. Dans l’emplacement de l’installation par défaut, il se trouve ici : **C:\Users\Administrator\AppData\Local\Temp** (ou un répertoire au-dessus de %temp%).

Journaux de déploiement du capteur Azure ATP :

-   **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS.log** : ce journal liste les étapes du processus de déploiement du capteur Azure ATP. Son utilisation principale consiste à suivre le processus de déploiement du capteur Azure ATP.

-   **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS_001_MsiPackage.log** : ce fichier journal liste les étapes du processus de déploiement des fichiers binaires du capteur Azure ATP. Son utilisation principale consiste à suivre le déploiement des fichiers binaires du capteur Azure ATP.


> [!NOTE] 
> En plus des journaux de déploiement mentionnés ici, il existe d’autres journaux qui commencent par « Azure Advanced Threat Protection » qui peuvent également fournir des informations supplémentaires sur le processus de déploiement.


## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)