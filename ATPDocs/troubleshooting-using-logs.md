---
title: Résolution des problèmes de Microsoft Defender pour l’identité à l’aide des journaux
description: Décrit comment vous pouvez utiliser Microsoft Defender pour les journaux d’identité pour résoudre les problèmes
ms.date: 10/27/2020
ms.topic: how-to
ms.openlocfilehash: 2c902576b4cf7b0acf58371bafe4bb60404890ba
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534512"
---
# <a name="troubleshooting-microsoft-defender-for-identity-sensor-using-the-defender-for-identity-logs"></a>Résolution des problèmes de Microsoft Defender pour le capteur d’identité à l’aide de Defender pour les journaux d’identité

Les [!INCLUDE [Product short](includes/product-short.md)] journaux fournissent des informations sur ce que chaque composant de [!INCLUDE [Product long](includes/product-long.md)] capteur fait à un moment donné.

Les [!INCLUDE [Product short](includes/product-short.md)] journaux se trouvent dans un sous-dossier  appelé logs [!INCLUDE [Product short](includes/product-short.md)] , où est installé. l’emplacement par défaut est : **C:\Program Files\Azure Advanced \\ Threat Protection Sensor**. Dans l’emplacement de l’installation par défaut, il se trouve ici : **C:\Program Files\Azure Advanced Threat Protection Sensor\numéro de version\Logs**.

Le [!INCLUDE [Product short](includes/product-short.md)] capteur contient les journaux suivants :

- **Microsoft. tri. Sensor. log** : ce journal contient tout ce qui se produit dans le [!INCLUDE [Product short](includes/product-short.md)] capteur (y compris la résolution et les erreurs). Son utilisation principale consiste à obtenir l’état général de toutes les opérations dans l’ordre chronologique dans lequel elles se sont produites.

- **Microsoft. tri. Sensor-Errors. log** : ce journal contient uniquement les erreurs interceptées par le [!INCLUDE [Product short](includes/product-short.md)] capteur. Son utilisation principale consiste à exécuter des vérifications d’intégrité et à examiner les problèmes qui doivent être mis en corrélation avec des heures spécifiques.

- **Microsoft. tri. Sensor. Updater. log** : ce journal est utilisé pour le processus de mise à jour du capteur, qui est chargé de mettre à jour le [!INCLUDE [Product short](includes/product-short.md)] capteur s’il est configuré pour le faire automatiquement.

> [!NOTE]
> Les trois premiers fichiers journaux ont une taille maximale de 50 Mo. Quand cette taille est atteinte, un nouveau fichier journal est ouvert et le précédent est renommé en « &lt;nom_fichier_origine&gt;-Archive-00000 » où le nombre augmente chaque fois qu’il est renommé. Par défaut, s’il existe déjà plus de 10 fichiers du même type, les plus anciens sont supprimés.

## <a name="defender-for-identity-deployment-logs"></a>Defender pour les journaux de déploiement des identités

Les [!INCLUDE [Product short](includes/product-short.md)] journaux de déploiement se trouvent dans le répertoire Temp de l’utilisateur qui a installé le produit. Dans l’emplacement d’installation par défaut, il se trouve à l’emplacement suivant : **C:\Users\Administrator\AppData\Local\Temp** (ou un répertoire au-dessus de% temp%).

[!INCLUDE [Product short](includes/product-short.md)] journaux de déploiement du capteur :

- **Azure Advanced Threat Protection Microsoft.Tri.Sensor.Deployment.Deployer_YYYYMMDDHHMMSS.log** - Ce fichier journal indique le processus complet de déploiement du capteur et se trouve dans le dossier temporaire mentionné précédemment, ou dans le dossier C:\Windows\Temp.

- **Azure-protection avancée contre les menaces Sensor_YYYYMMDDHHMMSS. log** : ce journal répertorie les étapes du processus de déploiement du [!INCLUDE [Product short](includes/product-short.md)] capteur. Son utilisation principale consiste à suivre le [!INCLUDE [Product short](includes/product-short.md)] processus de déploiement du capteur.

- **Azure-protection avancée contre les menaces Sensor_YYYYMMDDHHMMSS_001_MsiPackage. log** : ce fichier journal répertorie les étapes du processus de déploiement des [!INCLUDE [Product short](includes/product-short.md)] fichiers binaires du capteur. Son utilisation principale consiste à suivre le déploiement des [!INCLUDE [Product short](includes/product-short.md)] binaires de capteur.

> [!NOTE]
> En plus des journaux de déploiement mentionnés ici, il existe d’autres journaux qui commencent par « Azure Advanced Threat Protection » qui peuvent également fournir des informations supplémentaires sur le processus de déploiement.

## <a name="see-also"></a>Voir aussi

- [Prérequis de [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Planification de capacité [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
