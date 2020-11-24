---
title: Architecture de Microsoft Defender pour Identity
description: Décrit l’architecture de Microsoft Defender pour Identity
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cb67a36402c0b6b193fbd5ee11b63113714cd885
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848803"
---
# <a name="microsoft-defender-for-identity-architecture"></a>Architecture de Microsoft Defender pour Identity

[!INCLUDE [Product long](includes/product-long.md)] supervise vos contrôleurs de domaine en capturant et en analysant le trafic réseau, ainsi qu’en utilisant les événements Windows provenant directement de vos contrôleurs de domaine. Ensuite, il analyse les données relatives aux attaques et aux menaces. [!INCLUDE [Product short](includes/product-short.md)] utilise le profilage, la détection déterministe, le machine learning et les algorithmes comportementaux pour en savoir plus sur votre réseau, pour détecter les anomalies et pour vous avertir des activités suspectes.

Architecture [!INCLUDE [Product short](includes/product-short.md)] :

![Diagramme de topologie de l’architecture [!INCLUDE [Product short](includes/product-short.md)]](media/architecture-topology.png)

Cette section explique comment fonctionne le flux de capture des événements et du réseau [!INCLUDE [Product short](includes/product-short.md)] et décrit en détail les fonctionnalités des composants principaux : le portail [!INCLUDE [Product short](includes/product-short.md)], le capteur [!INCLUDE [Product short](includes/product-short.md)] et le service cloud [!INCLUDE [Product short](includes/product-short.md)].

Directement installé sur vos contrôleurs de domaine, le capteur [!INCLUDE [Product short](includes/product-short.md)] accède aux journaux d’événements dont il a besoin directement sur les contrôleurs de domaine. Une fois les journaux et le trafic réseau analysés par le capteur, [!INCLUDE [Product short](includes/product-short.md)] envoie uniquement les informations analysées au service cloud [!INCLUDE [Product short](includes/product-short.md)] (ce qui ne présente qu’une partie des journaux envoyés).

## <a name="product-short-components"></a>Composants [!INCLUDE [Product short](includes/product-short.md)]

[!INCLUDE [Product short](includes/product-short.md)] est constitué des composants suivants :

- **Portail [!INCLUDE [Product short](includes/product-short.md)]**  
Le portail [!INCLUDE [Product short](includes/product-short.md)] vous permet de créer votre instance [!INCLUDE [Product short](includes/product-short.md)], montre les données provenant des capteurs [!INCLUDE [Product short](includes/product-short.md)], et vous permet de superviser, gérer et examiner les menaces dans votre environnement réseau.

- **Capteur [!INCLUDE [Product short](includes/product-short.md)]**  
Les capteurs [!INCLUDE [Product short](includes/product-short.md)] sont installés directement sur vos contrôleurs de domaine. Le capteur supervise directement le trafic des contrôleurs de domaine, sans recourir à un serveur dédié, ou à une configuration de mise en miroir de ports.
- **Service cloud [!INCLUDE [Product short](includes/product-short.md)]**  
Le service cloud [!INCLUDE [Product short](includes/product-short.md)] s’exécute dans l’infrastructure Azure et est actuellement disponible aux États-Unis, en Europe et en Asie. Le service cloud [!INCLUDE [Product short](includes/product-short.md)] est connecté à Microsoft Intelligent Security Graph.

## <a name="product-short-portal"></a>Portail [!INCLUDE [Product short](includes/product-short.md)]

Utilisez le portail [!INCLUDE [Product short](includes/product-short.md)] pour :

- Créer votre instance [!INCLUDE [Product short](includes/product-short.md)]
- Effectuer l’intégration à d’autres services de sécurité Microsoft
- Gérer les paramètres de configuration de capteur [!INCLUDE [Product short](includes/product-short.md)]
- Afficher les données provenant des capteurs [!INCLUDE [Product short](includes/product-short.md)]
- Superviser les activités suspectes et les attaques détectées en suivant le modèle Kill Chain
- **Facultatif** : Le portail peut également être configuré pour envoyer des e-mails et des événements lorsque des alertes de sécurité ou des problèmes d’intégrité sont détectés.

> [!NOTE]
> Si aucun capteur n’est installé dans votre instance [!INCLUDE [Product short](includes/product-short.md)] dans un délai de 60 jours, il se peut qu’elle soit supprimée et que vous deviez la recréer.

## <a name="product-short-sensor"></a>Capteur [!INCLUDE [Product short](includes/product-short.md)]

Les fonctionnalités principales du capteur [!INCLUDE [Product short](includes/product-short.md)] sont les suivantes :

- Capturer et inspecter le trafic réseau des contrôleurs de domaine (trafic local du contrôleur de domaine)
- Recevoir des événements Windows directement à partir des contrôleurs de domaine
- Recevoir des informations de gestion de comptes RADIUS à partir de votre fournisseur VPN
- Récupérer les données concernant les utilisateurs et les ordinateurs à partir du domaine Active Directory
- Effectuer la résolution des entités réseau (utilisateurs, groupes et ordinateurs)
- Transférer les données pertinentes au service cloud [!INCLUDE [Product short](includes/product-short.md)]

## <a name="product-short-sensor-features"></a>Fonctionnalités du capteur [!INCLUDE [Product short](includes/product-short.md)]

Le capteur [!INCLUDE [Product short](includes/product-short.md)] lit les événements localement, ce qui évite les frais liés à l’achat et à la maintenance de matériel et de configurations supplémentaires. Le capteur [!INCLUDE [Product short](includes/product-short.md)] prend également en charge le suivi d’événements pour Windows (ETW) qui fournit des informations de journaux pour plusieurs détections. Les détections ETW reconnaissent notamment les suspicions d’attaques DCShadow tentées via des demandes de réplication de contrôleur de domaine et la promotion de contrôleur de domaine.

### <a name="domain-synchronizer-process"></a>Processus de synchronisateur de domaine

Le processus de synchronisateur de domaine est responsable de la synchronisation proactive de toutes les entités d’un domaine Active Directory spécifique (il est similaire au mécanisme utilisé par les contrôleurs de domaine eux-mêmes pour la réplication). Un capteur est automatiquement choisi de façon aléatoire parmi tous les capteurs éligibles comme synchronisateur de domaine.

Si le synchronisateur de domaine est hors connexion pendant plus de 30 minutes, un autre capteur est automatiquement choisi à la place.

### <a name="resource-limitations"></a>Limitations des ressources

Le capteur [!INCLUDE [Product short](includes/product-short.md)] inclut un composant de surveillance qui évalue la capacité de calcul et de mémoire disponible sur le contrôleur de domaine où il s’exécute. Le processus de supervision s’exécute toutes les 10 secondes, et met à jour dynamiquement le quota d’utilisation du processeur et de la mémoire dans le processus du capteur [!INCLUDE [Product short](includes/product-short.md)]. Le processus de supervision permet de garantir que le contrôleur de domaine dispose toujours d’au moins 15 % de ressources de calcul et de mémoire disponibles.

Quoi qu’il se passe sur le contrôleur de domaine, le processus de supervision libère continuellement des ressources pour que les fonctionnalités principales du contrôleur de domaine ne soient pas affectées.

Si en raison du processus de supervision, le capteur [!INCLUDE [Product short](includes/product-short.md)] vient à manquer de ressources, le trafic n’est que partiellement supervisé et l’alerte d’intégrité « Dropped port mirrored network traffic » (Le trafic réseau du port en miroir a été supprimé) s’affiche dans la page Intégrité du portail [!INCLUDE [Product short](includes/product-short.md)].

### <a name="windows-events"></a>Événements Windows

Pour améliorer sa détection relative aux authentifications NTLM, aux modifications de groupes sensibles et à la création de services suspects, [!INCLUDE [Product short](includes/product-short.md)] doit analyser les journaux des événements Windows suivants : 4776,4732,4733,4728,4729,4756,4757,7045 et 8004. Ces événements sont lus automatiquement par les capteurs [!INCLUDE [Product short](includes/product-short.md)] avec les [paramètres de stratégie d’audit avancés adaptés](configure-windows-event-collection.md). Pour [vous assurer que l’événement Windows 8004 est audité](configure-windows-event-collection.md#ntlm-authentication-using-windows-event-8004) en fonction des besoins du service, vérifiez vos [paramètres d’audit NTLM](/archive/blogs/askds/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7).

## <a name="next-steps"></a>Étapes suivantes

- [Prérequis de [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Outil de dimensionnement [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/trisizingtool)
- [Planification de capacité [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
