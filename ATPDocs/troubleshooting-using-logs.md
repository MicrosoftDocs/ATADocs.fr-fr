---
title: Résolution des problèmes liés à Azure-protection avancée contre les menaces à l’aide des journaux
description: Décrit comment utiliser les journaux Azure ATP pour résoudre des problèmes
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/05/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: de796346-647d-48e1-970a-8f072e990f1e
ms.reviewer: ''
ms.suite: ''
ms.openlocfilehash: 5495bf07b8d8f12ba5bb1dc61f58d8e5f4475614
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828066"
---
# <a name="troubleshooting-azure-advanced-threat-protection-atp-sensor-using-the-atp-logs"></a>Résolution des problèmes du capteur Azure Advanced Threat Protection (ATP) à l’aide des journaux ATP

Les journaux ATP donnent des informations sur ce que fait chaque composant du capteur Azure ATP à n’importe quel moment.

Les journaux Azure ATP se trouvent dans le sous-dossier nommé **Logs** où ATP est installé ; l’emplacement par défaut est : **C:\Program Files\Azure Advanced Threat Protection Sensor\\**. Dans l’emplacement de l’installation par défaut, il se trouve ici : **C:\Program Files\Azure Advanced Threat Protection Sensor\numéro de version\Logs**.

Le capteur Azure ATP dispose des journaux suivants :

- **Microsoft.Tri.Sensor.log** : ce journal contient tout ce qui se produit dans le capteur Azure ATP (y compris les erreurs et la résolution). Son utilisation principale consiste à obtenir l’état général de toutes les opérations dans l’ordre chronologique dans lequel elles se sont produites.

- **Microsoft.Tri.Sensor-Errors.log** : ce journal contient uniquement les erreurs interceptées par le capteur ATP. Son utilisation principale consiste à exécuter des vérifications d’intégrité et à examiner les problèmes qui doivent être mis en corrélation avec des heures spécifiques.

- **Microsoft.Tri.Sensor.Updater.log** : ce journal est utilisé pour le processus de mise à jour de capteur, qui est responsable de la mise à jour automatique du capteur ATP s’il est configuré.

> [!NOTE]
> Les trois premiers fichiers journaux ont une taille maximale de 50 Mo. Quand cette taille est atteinte, un nouveau fichier journal est ouvert et le précédent est renommé en « &lt;nom_fichier_origine&gt;-Archive-00000 » où le nombre augmente chaque fois qu’il est renommé. Par défaut, s’il existe déjà plus de 10 fichiers du même type, les plus anciens sont supprimés.

## <a name="azure-atp-deployment-logs"></a>Journaux de déploiement Azure ATP

Les journaux de déploiement Azure ATP se trouvent dans le répertoire temp de l’utilisateur qui a installé le produit. Dans l’emplacement d’installation par défaut, il se trouve à l’emplacement suivant : **C:\Users\Administrator\AppData\Local\Temp** (ou un répertoire au-dessus de% temp%).

Journaux de déploiement du capteur Azure ATP :

- **Azure Advanced Threat Protection Microsoft.Tri.Sensor.Deployment.Deployer_YYYYMMDDHHMMSS.log** - Ce fichier journal indique le processus complet de déploiement du capteur et se trouve dans le dossier temporaire mentionné précédemment, ou dans le dossier C:\Windows\Temp.

- **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS.log** : ce journal liste les étapes du processus de déploiement du capteur Azure ATP. Son utilisation principale consiste à suivre le processus de déploiement du capteur Azure ATP.

- **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS_001_MsiPackage.log** : ce fichier journal liste les étapes du processus de déploiement des fichiers binaires du capteur Azure ATP. Son utilisation principale consiste à suivre le déploiement des fichiers binaires du capteur Azure ATP.

> [!NOTE]
> En plus des journaux de déploiement mentionnés ici, il existe d’autres journaux qui commencent par « Azure Advanced Threat Protection » qui peuvent également fournir des informations supplémentaires sur le processus de déploiement.

## <a name="see-also"></a>Voir aussi

- [Prérequis d’Azure ATP](prerequisites.md)
- [Planification de la capacité Azure ATP](capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)