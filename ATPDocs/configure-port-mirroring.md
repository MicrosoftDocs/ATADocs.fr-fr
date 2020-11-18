---
title: Configuration de la mise en miroir de ports lors du déploiement de Microsoft Defender pour Identity
description: Décrit les options de mise en miroir de ports et explique comment les configurer pour Microsoft Defender pour Identity.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c0dacdf37dbcc033a310fb4b0995ab8259db452f
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848089"
---
# <a name="configure-port-mirroring"></a>Configurer la mise en miroir des ports

Cet article ne s’applique que dans le cadre du déploiement de capteurs autonomes [!INCLUDE [Product long](includes/product-long.md)] plutôt que de capteurs [!INCLUDE [Product short](includes/product-short.md)].

> [!NOTE]
> Les capteurs autonomes [!INCLUDE [Product short](includes/product-short.md)] ne prennent pas en charge la collecte d’entrées de journal du Suivi d’événements pour Windows (ETW) qui fournissent les données pour de nombreuses détections. Pour une couverture complète de votre environnement, nous vous recommandons de déployer le capteur [!INCLUDE [Product short](includes/product-short.md)].

La principale source de données utilisée par [!INCLUDE [Product short](includes/product-short.md)] est l’inspection approfondie des paquets du trafic réseau entrant et sortant des contrôleurs de domaine. Pour que [!INCLUDE [Product short](includes/product-short.md)] puisse voir le trafic réseau, vous devez configurer la mise en miroir de ports ou utiliser un TAP réseau.

Pour la **mise en miroir des ports**, configurez-la pour chaque contrôleur de domaine à surveiller en tant que **source** du trafic réseau. En règle générale, vous devez collaborer avec l’équipe de virtualisation ou de mise en réseau pour configurer la mise en miroir des ports.
Pour plus d’informations, reportez-vous à la documentation de votre fournisseur.

Vos contrôleurs de domaine et votre capteur autonome [!INCLUDE [Product short](includes/product-short.md)] peuvent être physiques ou virtuels. Voici les méthodes couramment employées dans le cadre de la mise en miroir des ports et quelques considérations à prendre en compte. Pour plus d’informations, reportez-vous à la documentation produit de votre commutateur ou de votre serveur de virtualisation. Le fabricant de votre commutateur peut utiliser une terminologie différente.

**SPAN (Switched Port Analyzer)**  : copie le trafic réseau à partir d’un ou plusieurs ports de commutateur vers un autre port du même commutateur. Le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] et les contrôleurs de domaine doivent être connectés au même commutateur physique.

**RSPAN (Remote Switch Port Analyzer)**  : vous permet de surveiller le trafic réseau à partir de ports sources répartis sur plusieurs commutateurs physiques. RSPAN copie le trafic source dans un VLAN spécial configuré pour RSPAN. Ce VLAN doit être relié en mode trunk aux autres commutateurs impliqués. RSPAN fonctionne sur la couche 2.

**ERSPAN (Encapsulated Remote Switch Port Analyzer)**  : il s’agit d’une technologie propriétaire qui fonctionne sur la couche 3. ERSPAN vous permet de surveiller le trafic entre les commutateurs sans faire appel à des trunks VLAN. ERSPAN utilise le protocole GRE (Generic Routing Encapsulation) pour copier le trafic réseau surveillé. [!INCLUDE [Product short](includes/product-short.md)] ne peut pas recevoir directement de trafic ERSPAN à l’heure actuelle. Pour qu’il fonctionne avec le trafic ERSPAN, vous devez configurer un commutateur ou un routeur capable de décapsuler le trafic comme destination d’ERSPAN à l’endroit où le trafic est décapsulé. Configurez ensuite le commutateur ou le routeur de façon à transférer le trafic décapsulé vers le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] à l’aide de SPAN ou de RSPAN.

> [!NOTE]
> Si le contrôleur de domaine faisant l’objet d’une mise en miroir des ports est connecté via une liaison WAN, vérifiez que celle-ci peut gérer la charge supplémentaire du trafic ERSPAN.
> [!INCLUDE [Product short](includes/product-short.md)] ne gère la supervision du trafic que si ce dernier atteint l’adaptateur réseau et le contrôleur de domaine de la même manière, et non s’il est réparti sur différents ports.

## <a name="supported-port-mirroring-options"></a>Options de mise en miroir des ports prises en charge

|Capteur autonome [!INCLUDE [Product short](includes/product-short.md)]|Contrôleur de domaine|Considérations|
|---------------|---------------------|------------------|
|Virtuelle|Virtuel sur le même hôte|Le commutateur virtuel doit prendre en charge la mise en miroir des ports.<br /><br />Le fait de déplacer l’une des machines virtuelles vers un autre hôte où elle sera toute seule risque de briser la mise en miroir des ports.|
|Virtuel|Virtuel sur des hôtes différents|Vérifiez que votre commutateur virtuel prend en charge ce scénario.|
|Les machines|Physique|Exige un adaptateur réseau dédié ; sinon, [!INCLUDE [Product short](includes/product-short.md)] détecte tout le trafic entrant et sortant de l’hôte, même celui qu’il envoie au service cloud [!INCLUDE [Product short](includes/product-short.md)].|
|Physique|Les machines|Vérifiez que votre commutateur virtuel prend en charge ce scénario et configurez la mise en miroir des ports sur vos commutateurs physiques selon le cas :<br /><br />Si l’hôte virtuel se trouve sur le même commutateur physique, vous devez configurer SPAN au niveau du commutateur.<br /><br />Si l’hôte virtuel se trouve sur un autre commutateur, vous devez configurer RSPAN ou ERSPAN&#42;.|
|Physique|Physique sur le même commutateur|Le commutateur physique doit prendre en charge SPAN/la mise en miroir des ports.|
|Physique|Physique sur un autre commutateur|Exige que les commutateurs physiques prennent en charge RSPAN ou ERSPAN&#42;.|

\* ERSPAN n’est pris en charge que si la décapsulation est effectuée avant l’analyse du trafic par [!INCLUDE [Product short](includes/product-short.md)].

> [!NOTE]
> Veillez à ce que les horloges des contrôleurs de domaine et du capteur autonome [!INCLUDE [Product short](includes/product-short.md)] auquel ils se connectent soient synchronisées de façon à ne pas différer de plus de cinq minutes.

**Si vous travaillez avec des clusters de virtualisation :**

- Pour chaque contrôleur de domaine qui s’exécute dans le cluster de virtualisation sur une machine virtuelle disposant du capteur autonome [!INCLUDE [Product short](includes/product-short.md)], configurez l’affinité entre le contrôleur de domaine et le capteur autonome. De cette manière, quand le contrôleur de domaine passe à un autre hôte dans le cluster, le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] le suit. Cela fonctionne bien quand il y a quelques contrôleurs de domaine.

  > [!NOTE]
  > Si votre environnement prend en charge la configuration « virtuel à virtuel » sur différents hôtes (RSPAN), vous n’avez pas à vous soucier de l’affinité.

- Pour que le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] soit correctement dimensionné pour gérer par lui-même la supervision de tous les contrôleurs de domaine, essayez cette option : installez une machine virtuelle sur chaque hôte de virtualisation et un capteur autonome [!INCLUDE [Product short](includes/product-short.md)] sur chaque hôte. Configurez chaque capteur autonome [!INCLUDE [Product short](includes/product-short.md)] de façon qu’il supervise tous les contrôleurs de domaine qui s’exécutent dans le cluster. Ainsi, n’importe quel hôte sur lequel les contrôleurs de domaine s’exécutent est surveillé.

Après avoir configuré la mise en miroir de ports, vérifiez qu’elle fonctionne avant d’installer le capteur autonome [!INCLUDE [Product short](includes/product-short.md)].

## <a name="see-also"></a>Voir aussi

- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
