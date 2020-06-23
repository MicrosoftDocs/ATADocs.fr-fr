---
title: Architecture Azure Advanced Threat Protection
description: Décrit l’architecture Azure - Protection avancée contre les menaces (ATP)
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/23/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 14e789e307b04a25c5a095aa1496780135ac49e5
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84774483"
---
# <a name="azure-atp-architecture"></a>Architecture Azure ATP

Azure ATP supervise vos contrôleurs de domaine en capturant et en analysant le trafic réseau, ainsi qu’en utilisant les événements Windows provenant directement de vos contrôleurs de domaine. Ensuite, il analyse les données relatives aux attaques et aux menaces. Azure ATP utilise le profilage, la détection déterministe, le machine learning et les algorithmes comportementaux pour en savoir plus sur votre réseau, pour détecter les anomalies et pour vous avertir des activités suspectes.

Architecture Azure Advanced Threat Protection :

![Diagramme de la topologie de l’architecture Azure ATP](media/atp-architecture-topology.png)

Cette section explique comment fonctionne le flux de capture des événements et du réseau Azure ATP et décrit en détail les fonctionnalités des composants principaux : le portail Azure ATP, le capteur Azure ATP et le service cloud Azure ATP. 

Directement installé sur vos contrôleurs de domaine, le capteur Azure ATP accède aux journaux d’événements dont il a besoin directement sur les contrôleurs de domaine. Une fois les journaux et le trafic réseau analysés par le capteur, Azure ATP envoie uniquement les informations analysées au service cloud Azure ATP (ce qui ne présente qu’une partie des journaux envoyés). 

## <a name="azure-atp-components"></a>Composants d’Azure ATP
Azure ATP est constitué des composants suivants :

-    **Portail Azure ATP** <br>
Le portail Azure ATP vous permet de créer votre instance Azure ATP, montre les données provenant des capteurs Azure ATP, et vous permet de superviser, gérer et examiner les menaces dans votre environnement réseau.  
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

 
## <a name="azure-atp-sensor-features"></a>Fonctionnalités des capteurs Azure ATP

Le capteur Azure ATP lit les événements localement, ce qui évite les frais liés à l’achat et à la maintenance de matériel et de configurations supplémentaires. Le capteur Azure ATP prend également en charge le suivi d’événements pour Windows (ETW) qui fournit des informations de journaux pour plusieurs détections. Les détections ETW reconnaissent notamment les suspicions d’attaques DCShadow tentées via des demandes de réplication de contrôleur de domaine et la promotion de contrôleur de domaine.

### <a name="domain-synchronizer-process"></a>Processus de synchronisateur de domaine

Le processus de synchronisateur de domaine est responsable de la synchronisation proactive de toutes les entités d’un domaine Active Directory spécifique (il est similaire au mécanisme utilisé par les contrôleurs de domaine eux-mêmes pour la réplication). Un capteur est automatiquement choisi de façon aléatoire parmi tous les capteurs éligibles comme synchronisateur de domaine. 

Si le synchronisateur de domaine est hors connexion pendant plus de 30 minutes, un autre capteur est automatiquement choisi à la place. 
    
### <a name="resource-limitations"></a>Limitations des ressources

Le capteur Azure ATP inclut un composant de surveillance qui évalue la capacité de calcul et de mémoire disponible sur le contrôleur de domaine où il s’exécute. Le processus de supervision s’exécute toutes les 10 secondes, et met à jour dynamiquement le quota d’utilisation du processeur et de la mémoire dans le processus du capteur Azure ATP. Le processus de supervision permet de garantir que le contrôleur de domaine dispose toujours d’au moins 15 % de ressources de calcul et de mémoire disponibles.

Quoi qu’il se passe sur le contrôleur de domaine, le processus de supervision libère continuellement des ressources pour que les fonctionnalités principales du contrôleur de domaine ne soient pas affectées.

Si en raison du processus de supervision, le capteur Azure ATP vient à manquer de ressources, le trafic n’est que partiellement supervisé et l’alerte d’intégrité « Dropped port mirrored network traffic » (Le trafic réseau du port en miroir a été supprimé) s’affiche dans la page Intégrité du portail Azure ATP.

### <a name="windows-events"></a>Événements Windows

Pour améliorer sa détection relative aux authentifications NTLM, aux modifications de groupes sensibles et à la création de services suspects, Azure ATP doit analyser les journaux des événements Windows suivants : 4776,4732,4733,4728,4729,4756,4757,7045 et 8004. Ces événements sont lus automatiquement par les capteurs Azure ATP avec les [paramètres de stratégie d’audit avancés](atp-advanced-audit-policy.md) adaptés. Pour [vous assurer que l’événement Windows 8004 est audité](configure-windows-event-collection.md#ntlm-authentication-using-windows-event-8004) en fonction des besoins du service, vérifiez vos [paramètres d’audit NTLM](https://blogs.technet.microsoft.com/askds/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7/).

## <a name="next-steps"></a>Étapes suivantes

- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Outil de dimensionnement Azure ATP](https://aka.ms/trisizingtool)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
