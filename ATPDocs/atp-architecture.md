---
title: Architecture Azure - Protection avancée contre les menaces | Microsoft Docs
description: Décrit l’architecture Azure - Protection avancée contre les menaces (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/30/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f23ae083ea09150849f95b58d1ab441af061f7bf
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166593"
---
*S’applique à : Azure - Protection avancée contre les menaces*


# <a name="azure-atp-architecture"></a>Architecture Azure ATP
Architecture Azure - Protection avancée contre les menaces :

![Diagramme de la topologie de l’architecture Azure ATP](media/atp-architecture-topology.png)

Azure ATP surveille le trafic réseau de vos contrôleurs de domaine en utilisant la mise en miroir des ports sur un capteur autonome Azure ATP à l’aide de commutateurs physiques ou virtuels. Si vous déployez le capteur autonome Azure ATP directement sur vos contrôleurs de domaine, la mise en miroir des ports est inutile. De plus, Azure ATP peut tirer parti des événements Windows (transférés directement à partir de vos contrôleurs de domaine ou d’un serveur SIEM) et analyser les données à la recherche d’attaques et de menaces. Azure ATP reçoit le trafic analysé à partir du capteur autonome Azure ATP et du capteur Azure ATP. Azure ATP effectue ensuite le profilage, exécute la détection déterministe, et exécute l’apprentissage automatique et les algorithmes comportementaux pour en savoir plus sur votre réseau afin de détecter les anomalies et vous avertir des activités suspectes.

Cette section décrit le flux de capture réseau et d’événements, ainsi que les fonctionnalités des principaux composants d’ATP : le capteur Azure ATP, le capteur autonome Azure ATP (qui a les mêmes fonctionnalités de base que le capteur autonome Azure ATP mais nécessite du matériel supplémentaire, la mise en miroir des ports, une configuration, et ne prend pas en charge les détections basées sur ETW) et le service cloud Azure ATP. 

Lors de son installation directe sur les contrôleurs de domaine, le capteur ATP accède aux journaux d’événements directement à partir du contrôleur de domaine. Une fois ces journaux et le trafic analysés par le capteur, Azure ATP envoie uniquement cette information analysée au service Azure ATP (pas tous les journaux).

## <a name="azure-atp-components"></a>Composants d’Azure ATP
Azure ATP est constitué des composants suivants :

-   **Portail de gestion d’espace de travail Azure ATP** <br>
Le portail de gestion d’espace de travail Azure ATP vous permet de créer et de gérer votre espace de travail et permet l’intégration à d’autres services Microsoft.

-   **Portail d’espace de travail Azure ATP** <br>
Le portail d’espace de travail Azure ATP reçoit des données des capteurs et des capteurs autonomes ATP. Il surveille, gère et examine les menaces dans votre environnement.

-   **Capteur Azure ATP**<br>
Le capteur Azure ATP est installé directement sur vos contrôleurs de domaine et il surveille directement leur trafic, sans recourir à un serveur dédié ni à une configuration de mise en miroir des ports. 

-   **Capteur autonome Azure ATP**<br>
Le capteur autonome Azure ATP est installé sur un serveur dédié qui surveille le trafic à partir de vos contrôleurs de domaine à l’aide de la mise en miroir des ports ou d’un TAP réseau. Il s’agit d’une alternative au capteur Azure ATP qui nécessite du matériel supplémentaire, la mise en miroir des ports et une configuration. Les capteurs autonomes Azure ATP ne prennent pas en charge les détections basées sur ETW prises en charge par le capteur ATP. 

## <a name="deployment-options"></a>Options de déploiement
Vous pouvez déployer Azure ATP à l’aide de la combinaison suivante de capteurs :

-   **Utilisation de capteurs Azure ATP uniquement**<br>
Votre déploiement Azure ATP peut contenir uniquement des capteurs Azure ATP : les capteurs Azure ATP sont déployés directement sur chaque contrôleur de domaine et aucun serveur supplémentaire ni configuration de mise en miroir des ports n’est nécessaire.

-   **Utilisation de capteurs autonomes Azure ATP uniquement** <br>
Votre déploiement Azure ATP peut contenir uniquement des capteurs autonomes Azure ATP, sans aucun capteur Azure ATP : tous les contrôleurs de domaine doivent être configurés pour activer la mise en miroir des ports sur un capteur autonome Azure ATP ou des TAP réseau doivent être en place.

-   **Utilisation de capteurs autonomes Azure ATP et de capteurs Azure ATP**<br>
Votre déploiement Azure ATP inclut des capteurs autonomes Azure ATP et des capteurs Azure ATP. Les capteurs autonomes Azure ATP sont installés sur certains de vos contrôleurs de domaine (par exemple, tous les contrôleurs de domaine de vos sites de succursale). En même temps, d’autres contrôleurs de domaine sont surveillés par des capteurs autonomes Azure ATP (par exemple, les plus grands contrôleurs de domaine de vos principaux centres de données). 


### <a name="azure-atp-management-portal"></a>Portail de gestion Azure ATP

Le portail de gestion Azure ATP vous permet d’effectuer les opérations suivantes :

-   Créer et gérer votre espace de travail Azure ATP

-   Effectuer l’intégration à d’autres services de sécurité Microsoft

> [!NOTE]
> - Azure ATP prend actuellement en charge la création d’un seul espace de travail. Après avoir supprimé un espace de travail, vous pouvez contacter le support pour le réactiver. Vous pouvez avoir au maximum trois espaces de travail supprimés. Pour augmenter le nombre d’espaces de travail enregistrés et supprimés, contactez le support Azure ATP.
> - Si aucun capteur n’est installé sur votre espace de travail dans un délai de 60 jours, l’espace de travail risque d’être supprimé, et vous devrez le recréer.



### <a name="azure-atp-workspace-portal"></a>Portail d’espace de travail Azure ATP

L’espace de travail Azure ATP vous permet de gérer les fonctionnalités Azure ATP suivantes :

-   Gérer les paramètres de configuration des capteurs et des capteurs autonomes Azure ATP

-   Visualiser les données reçues des capteurs autonomes Azure ATP et des capteurs Azure ATP 

-   Surveiller les activités suspectes détectées sur la base des algorithmes d’apprentissage automatique de comportement pour détecter les comportements anormaux et des algorithmes déterministes pour détecter les attaques avancées en fonction de la chaîne de destruction d’attaque

-   Facultatif : le portail de gestion d’espace de travail peut être configuré pour envoyer des e-mails et des événements lors de la détection d’activités suspectes ou d’événements d’intégrité.


|||
|-|-|
|Portail de gestion Azure ATP|Gère votre espace de travail Azure ATP.|
|Portail d’espace de travail Azure ATP|L’espace de travail Azure ATP est utilisé pour configurer Azure ATP et surveiller les activités suspectes détectées par Azure ATP sur votre réseau. L’espace de travail Azure ATP ne dépend pas du capteur Azure ATP et s’exécute même lorsque le service de capteur Azure ATP est arrêté. |
|Détecteurs|Les détecteurs utilisent des algorithmes d’apprentissage automatique et des règles déterministes pour rechercher les activités suspectes et les comportements anormaux des utilisateurs sur votre réseau.|


## <a name="azure-atp-sensor-and-azure-atp-standalone-sensor"></a>Capteur Azure ATP et capteur autonome Azure ATP

Le **capteur Azure ATP** et le **capteur autonome Azure ATP** ont les mêmes fonctionnalités de base :

-   Capturez et inspectez le trafic réseau des contrôleurs de domaine. Il s’agit du trafic local du contrôleur de domaine dans les capteurs Azure ATP et du trafic avec mise en miroir des ports pour les capteurs autonomes Azure ATP. 

-   Recevoir des événements Windows directement à partir des contrôleurs de domaine (pour les capteurs ATP) ou à partir des serveurs SIEM ou Syslog (pour les capteurs autonomes ATP)

-   Recevoir des informations de gestion de comptes RADIUS à partir de votre fournisseur VPN

-   Récupérer les données concernant les utilisateurs et les ordinateurs à partir du domaine Active Directory

-   Effectuer la résolution des entités réseau (utilisateurs, groupes et ordinateurs)

-   Transférer les données pertinentes au service cloud Azure ATP

-   Surveillez un seul contrôleur de domaine pour un capteur Azure ATP ou surveillez plusieurs contrôleurs de domaine à partir d’un seul capteur autonome Azure ATP.

Par défaut, Azure ATP prend en charge jusqu’à 100 capteurs. Si vous voulez en installer plus, contactez le support Azure ATP.

Le capteur autonome Azure ATP reçoit le trafic réseau et les événements Windows de votre réseau, et les traite dans les composants principaux suivants :

|||
|-|-|
|Écouteur réseau|L’écouteur réseau capture le trafic réseau et analyse le trafic. Il s’agit d’une tâche qui nécessite une utilisation intensive du processeur. Il est donc important de consulter les [conditions préalables d’Azure ATP](atp-prerequisites.md) quand vous planifiez votre capteur Azure ATP ou capteur autonome Azure ATP.|
|Écouteur d’événements|L’écouteur d’événements capture et analyse les événements Windows transférés à partir d’un serveur SIEM sur votre réseau.|
|Lecteur du journal des événements Windows|Le lecteur du journal des événements Windows lit et analyse les événements Windows transférés dans le journal des événements Windows du capteur autonome Azure ATP à partir des contrôleurs de domaine.|
|Traducteur d’activité réseau | Traduit le trafic analysé en une représentation logique du trafic, utilisée par Azure ATP (NetworkActivity).
|Programme de résolution des entités|Le programme de résolution des entités reçoit les données analysées (le trafic réseau et les événements) et les résout à l’aide d’Active Directory pour trouver les informations de compte et d’identité. Ensuite, il les met en correspondance avec les adresses IP trouvées dans les données analysées. Le programme de résolution des entités inspecte les en-têtes de paquets de manière efficace, pour permettre l’analyse des noms, propriétés et identités d’ordinateurs dans les paquets d’authentification. Le programme de résolution des entités combine les paquets d’authentification analysés avec les données du paquet.|
|Expéditeur d’entité|L’expéditeur d’entité envoie au service cloud Azure ATP les données analysées et mises en correspondance.|

## <a name="azure-atp-sensor-features"></a>Fonctionnalités des capteurs Azure ATP

Les fonctionnalités suivantes fonctionnent différemment selon que vous exécutez un capteur Azure ATP ou un capteur autonome Azure ATP.

-   Le capteur Azure ATP lit les événements localement, sans devoir acheter et entretenir du matériel supplémentaire ou configurer le transfert d’événements requis avec les capteurs autonomes ATP. Le capteur Azure ATP prend également en charge ETW qui fournit les informations du journal pour plusieurs détections. Les détections ETW incluent : Demande de réplication suspecte et Promotion du contrôleur de domaine suspect, deux attaques DCShadow potentielles, et ne sont pas prises en charge par les capteurs autonomes ATP.  

-   **Candidat synchronisateur de domaine**<br>
Le candidat synchronisateur de domaine est responsable de la synchronisation proactive de toutes les entités d’un domaine Active Directory spécifique (semblable au mécanisme utilisé par les contrôleurs de domaine eux-mêmes pour la réplication). Un capteur est choisi au hasard, dans la liste des candidats, comme synchronisateur de domaine. <br><br>
Si le synchronisateur est hors connexion pendant plus de 30 minutes, un autre candidat est choisi à la place. Si aucun synchronisateur de domaine n’est disponible pour un domaine spécifique, Azure ATP ne peut pas synchroniser de manière proactive les entités et leurs modifications, mais il récupère les nouvelles entités à mesure qu’elles sont détectées dans le trafic analysé. 
<br>Si aucun synchronisateur de domaine n’est disponible et que vous recherchez une entité avec laquelle aucun trafic n’était associé, aucun résultat de recherche ne s’affiche.<br><br>
Par défaut, tous les capteurs autonomes Azure ATP sont des candidats synchronisateurs.<br><br>
Les capteurs Azure ATP ne sont pas des candidats synchronisateurs par défaut.


-   **Limitations des ressources**<br>
Le capteur Azure ATP inclut un composant d’analyse qui évalue la capacité de calcul et de mémoire disponible sur le contrôleur de domaine sur lequel il s’exécute. Le processus d’analyse s’exécute toutes les 10 secondes et met à jour de manière dynamique le quota d’utilisation du processeur et de la mémoire sur le processus du capteur Azure ATP pour s’assurer qu’à tout moment le contrôleur de domaine dispose d’au moins 15 % de ressources de calcul et de mémoire libres.<br><br>
Quoi qu’il se passe sur le contrôleur de domaine, ce processus libère toujours des ressources pour s’assurer que la fonctionnalité de base du contrôleur de domaine n’est pas affectée.<br><br>
Si à cause de cela le capteur Azure ATP vient à manquer de ressources, le trafic est seulement partiellement analysé et l’alerte de surveillance « Le trafic réseau du port en miroir a été supprimé » s’affiche dans la page Intégrité.

Le tableau suivant présente un exemple de contrôleur de domaine qui dispose de suffisamment de ressources de calcul pour autoriser un quota plus élevé que ce qui est nécessaire actuellement. Ainsi, tout le trafic est analysé :

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Capteur Azure ATP (Microsoft.Tri.sensor.exe)|Divers (autres processus) |Quota du capteur Azure ATP|Le capteur supprime-t-il une part du trafic ?|
|30 %|20 %|10 %|45 %|Non|

Si Active Directory a besoin de davantage de puissance de calcul, le quota requis par le capteur Azure ATP est réduit. Dans l’exemple suivant, le capteur Azure ATP a besoin de davantage que le quota alloué et ignore une partie du trafic (analyse partielle du trafic) :

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Capteur Azure ATP (Microsoft.Tri.sensor.exe)|Divers (autres processus) |Quota du capteur Azure ATP|Le capteur supprime-t-il une part du trafic ?|
|60 %|15 %|10 %|15 %|Oui|


## <a name="your-network-components"></a>Composants du réseau
Pour utiliser Azure ATP, vérifiez que les composants suivants sont configurés.

### <a name="port-mirroring"></a>Mise en miroir des ports
Si vous utilisez des capteurs autonomes Azure ATP, la configuration de la mise en miroir de port est requise pour les contrôleurs de domaine sont supervisés. Configurez le capteur autonome Azure ATP comme destination à l’aide des commutateurs physiques ou virtuels. Une autre option consiste à utiliser des TAP réseau. Azure ATP fonctionne si plusieurs contrôleurs de domaine sont surveillés, mais pas tous. Toutefois, la détection est moins efficace.

Même si tout le trafic réseau des contrôleurs de domaine est mis en miroir vers le capteur autonome Azure ATP, seul un faible pourcentage de ce trafic est envoyé (compressé) au service cloud Azure ATP à des fins d’analyse.

Vos contrôleurs de domaine et les capteurs autonomes Azure ATP peuvent être physiques ou virtuels. Pour plus d’informations, consultez [Configurer la mise en miroir des ports](configure-port-mirroring.md).


### <a name="events"></a>Événements
Pour améliorer la couverture de détection d’Azure ATP des types d’attaques Pass-the-Hash, échecs d’authentification suspecte, Modification des groupes sensibles, Création de services suspects et activité de jeton honeytoken, Azure ATP doit analyser les journaux des événements Windows suivants : 4776,4732,4733,4728,4729,4756,4757 et 7045. Ces événements sont lus automatiquement par les capteurs Azure ATP avec les paramètres de stratégie d’audit avancés corrects. Si des capteurs autonomes Azure ATP sont déployés, les journaux d’événements peuvent être transférés au capteur autonome de deux manières : en configurant le capteur autonome Azure ATP afin qu’il reste à l’écoute des événements SIEM ou en [configurant les transferts d’événements Windows](configure-event-forwarding.md). 

> [!NOTE]
> - Le transfert d’événements Windows pour les capteurs autonomes ne prend pas en charge ETW (Suivi d’événements pour Windows). Les détections ETW incluent : Demande de réplication suspecte et Promotion du contrôleur de domaine suspect, deux attaques DCShadow potentielles.  

-   Configuration du capteur autonome Azure ATP pour écouter les événements SIEM <br>Configurez votre serveur SIEM de manière à transférer des événements Windows spécifiques vers ATP. Azure ATP prend en charge plusieurs fournisseurs SIEM. Pour plus d’informations, consultez [Configuration du transfert d’événements Windows](configure-event-forwarding.md).

-   Configuration du transfert d’événements Windows<br>Azure ATP peut aussi obtenir vos événements en configurant vos contrôleurs de domaine pour qu’ils transfèrent les événements Windows 4776, 4732, 4733, 4728, 4729, 4756, 4757 et 7045 à votre capteur autonome Azure ATP. Cette méthode est particulièrement utile si vous n’avez pas de serveur SIEM ou si votre serveur SIEM n’est actuellement pas pris en charge par ATP. Pour plus d’informations sur le transfert d’événements Windows dans ATP, consultez [Configuration du transfert d’événements Windows](configure-event-forwarding.md). Cela s’applique uniquement aux capteurs autonomes Azure ATP physiques, et non pas au capteur Azure ATP.


## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Outil de dimensionnement Azure ATP](http://aka.ms/trisizingtool)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)
