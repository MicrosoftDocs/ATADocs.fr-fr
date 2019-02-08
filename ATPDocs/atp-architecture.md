---
title: Architecture Azure Advanced Threat Protection | Microsoft Docs
description: Décrit l’architecture Azure - Protection avancée contre les menaces (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/27/2019
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6988b41b64dc3d8afef5f7af614f78b41501e2af
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085314"
---
# <a name="azure-atp-architecture"></a>Architecture Azure ATP

Azure ATP supervise vos contrôleurs de domaine en capturant et en analysant le trafic réseau, ainsi qu’en utilisant les événements Windows provenant directement de vos contrôleurs de domaine. Ensuite, il analyse les données relatives aux attaques et aux menaces. Azure ATP utilise le profilage, la détection déterministe, le machine learning et les algorithmes comportementaux pour en savoir plus sur votre réseau, pour détecter les anomalies et pour vous avertir des activités suspectes.

Architecture Azure Advanced Threat Protection :

![Diagramme de la topologie de l’architecture Azure ATP](media/atp-architecture-topology.png)

Cette section explique comment fonctionne le flux de capture des événements et du réseau Azure ATP et décrit en détail les fonctionnalités des composants principaux : le portail Azure ATP, le capteur Azure ATP et le service cloud Azure ATP. 

Directement installé sur vos contrôleurs de domaine, le capteur Azure ATP accède aux journaux d’événements dont il a besoin directement sur les contrôleurs de domaine. Une fois les journaux et le trafic réseau analysés par le capteur, Azure ATP envoie uniquement les informations analysées au service cloud Azure ATP (ce qui ne présente qu’une partie des journaux envoyés). 

## <a name="azure-atp-components"></a>Composants d’Azure ATP
Azure ATP est constitué des composants suivants :

-   **Portail Azure ATP** <br>
Le portail Azure ATP vous permet de créer votre instance Azure ATP, présente les données provenant des capteurs Azure ATP et vous permet de superviser, gérer et examiner les menaces dans votre environnement réseau.  
-   **Capteur Azure ATP**<br>
Les capteurs Azure ATP sont installés directement sur vos contrôleurs de domaine. Le capteur supervise directement le trafic des contrôleurs de domaine, sans recourir à un serveur dédié, ou à une configuration de mise en miroir de ports.

-   **Service cloud Azure ATP**<br>
Le service cloud Azure ATP s’exécute dans l’infrastructure Azure et est actuellement disponible aux États-Unis, en Europe et en Asie. Le service cloud Azure ATP est connecté à Microsoft Intelligent Security Graph. 

## <a name="azure-atp-portal"></a>Portail Azure ATP 
Utilisez le portail Azure ATP pour :
- Créer votre instance Azure ATP
- Effectuer l’intégration à d’autres services de sécurité Microsoft 
- Gérer les paramètres de configuration du capteur Azure ATP 
- Afficher les données provenant des capteurs Azure ATP
- Superviser les activités suspectes et les attaques détectées en suivant le modèle Kill Chain
- **Facultatif** : Le portail peut également être configuré pour envoyer des e-mails et des événements lorsque des alertes de sécurité ou des problèmes d’intégrité sont détectés.

> [!NOTE]
> - Si aucun capteur n’est installé dans votre instance Azure ATP dans un délai de 60 jours, il se peut qu’elle soit supprimée et que vous deviez la recréer.

## <a name="azure-atp-sensor"></a>Capteur Azure ATP
Les fonctionnalités principales du capteur Azure ATP sont les suivantes :
- Capturer et inspecter le trafic réseau des contrôleurs de domaine (trafic local du contrôleur de domaine)
- Recevoir des événements Windows directement à partir des contrôleurs de domaine 
- Recevoir des informations de gestion de comptes RADIUS à partir de votre fournisseur VPN
- Récupérer les données concernant les utilisateurs et les ordinateurs à partir du domaine Active Directory
- Effectuer la résolution des entités réseau (utilisateurs, groupes et ordinateurs)
- Transférer les données pertinentes au service cloud Azure ATP

 
## <a name="azure-atp-sensor-features"></a>Fonctionnalités du capteur Azure ATP
Le capteur Azure ATP lit les événements localement, ce qui évite les frais liés à l’achat et à la maintenance de matériel et de configurations supplémentaires. Le capteur Azure ATP prend également en charge le suivi d’événements pour Windows (ETW) qui fournit des informations de journaux pour plusieurs détections. Les détections ETW reconnaissent notamment les suspicions d’attaques DCShadow tentées via des demandes de réplication de contrôleur de domaine et la promotion de contrôleur de domaine.

### <a name="domain-synchronizer-candidate"></a>Candidat synchronisateur de domaine

    The domain synchronizer candidate is responsible for synchronizing all entities from a specific Active Directory domain proactively (similar to the mechanism used by the domain controllers themselves for replication). One sensor is chosen randomly, from the list of candidates, to serve as the domain synchronizer. 

    If the synchronizer is offline for more than 30 minutes, another candidate is chosen instead. If there is no domain synchronizer available for a specific domain, Azure ATP proactively synchronizes entities and their changes, however Azure ATP retrieves new entities as they are detected in the monitored traffic. 
    
    If there is no domain synchronizer available, and you search for an entity that did not have any traffic related to it, no search results are displayed.

    By default, Azure ATP sensors are not synchronizer candidates. To manually set an Azure ATP sensor as a domain synchronizer candidate, follow the steps in the [Azure ATP installation workflow](install-atp-step5.md#configure-azure-atp-sensor-settings).

### <a name="resource-limitations"></a>Limitations des ressources

    The Azure ATP sensor includes a monitoring component that evaluates the available compute and memory capacity on the domain controller on which it is running. The monitoring process runs every 10 seconds and dynamically updates the CPU and memory utilization quota on the Azure ATP sensor process. The monitoring process makes sure the domain controller always has at least 15% of free compute and memory resources available.

    No matter what occurs on the domain controller, the monitoring process continually frees up resources to make sure the domain controller's core functionality is never affected.

    If the monitoring process causes the Azure ATP sensor to run out of resources, only partial traffic is monitored and the monitoring alert "Dropped port mirrored network traffic" appears in the Azure ATP portal Health page.

### <a name="windows-events"></a>Événements Windows

    To enhance Azure ATP detection coverage of suspected identity theft (pass-the-hash), suspicious authentication failures,modifications to sensitive groups, creation of suspicious services, and Honeytoken activity types of attack, Azure ATP needs to analyze the logs of the following Windows events: 4776,4732,4733,4728,4729,4756,4757, and 7045. These events are read automatically by Azure ATP sensors with correct [advanced audit policy settings](atp-advanced-audit-policy.md). 

## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Outil de dimensionnement Azure ATP](http://aka.ms/trisizingtool)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
