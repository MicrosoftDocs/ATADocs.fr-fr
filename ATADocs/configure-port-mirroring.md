---
title: Configurer la mise en miroir des ports lors du déploiement d’Advanced Threat Analytics | Microsoft Docs
description: Décrit les options de mise en miroir des ports et comment les configurer pour ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 37ce0480015e3b241b0253a80692beca3e12c0a7
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077556"
---
# <a name="configure-port-mirroring"></a>Configurer la mise en miroir des ports

*S’applique à : Advanced Threat Analytics version 1.9*

> [!NOTE] 
> Cet article ne vous concerne que si vous déployez des passerelles ATA au lieu de passerelles légères ATA. Pour déterminer si vous devez utiliser des passerelles ATA, consultez [Choix des passerelles appropriées pour votre déploiement](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment).

La principale source de données utilisée par ATA est l’inspection approfondie des paquets du trafic réseau entrant et sortant de vos contrôleurs de domaine. Pour qu’ATA puisse voir le trafic réseau, vous devez configurer la mise en miroir des ports ou utiliser un TAP réseau.

Pour la **mise en miroir des ports**, configurez-la pour chaque contrôleur de domaine à surveiller en tant que **source** du trafic réseau. En règle générale, vous devez collaborer avec l’équipe de virtualisation ou de mise en réseau pour configurer la mise en miroir des ports.
Pour plus d’informations, reportez-vous à la documentation de votre fournisseur.

Vos contrôleurs de domaine et vos passerelles ATA peuvent être physiques ou virtuels. Voici les méthodes couramment employées dans le cadre de la mise en miroir des ports et quelques considérations à prendre en compte. Pour plus d’informations, reportez-vous à la documentation produit de votre commutateur ou de votre serveur de virtualisation. Le fabricant de votre commutateur peut utiliser une terminologie différente.

**SPAN (Switched Port Analyzer)**  : copie le trafic réseau à partir d’un ou plusieurs ports de commutateur vers un autre port du même commutateur. La passerelle ATA et les contrôleurs de domaine doivent être connectés au même commutateur physique.

**RSPAN (Remote Switch Port Analyzer)**  : vous permet de surveiller le trafic réseau à partir de ports sources répartis sur plusieurs commutateurs physiques. RSPAN copie le trafic source dans un VLAN spécial configuré pour RSPAN. Ce VLAN doit être relié en mode trunk aux autres commutateurs impliqués. RSPAN fonctionne sur la couche 2.

**ERSPAN (Encapsulated Remote Switch Port Analyzer)**  : il s’agit d’une technologie propriétaire qui fonctionne sur la couche 3. ERSPAN vous permet de surveiller le trafic entre les commutateurs sans faire appel à des trunks VLAN. ERSPAN utilise le protocole GRE (Generic Routing Encapsulation) pour copier le trafic réseau surveillé. ATA ne peut pas recevoir directement le trafic ERSPAN pour l’instant. Pour qu’ATA fonctionne avec le trafic ERSPAN, un commutateur ou un routeur capable de décapsuler le trafic doit être configuré comme destination d’ERSPAN à l’endroit où le trafic est décapsulé. Configurez ensuite le commutateur ou le routeur pour transférer le trafic décapsulé vers la passerelle ATA à l’aide de SPAN ou de RSPAN.

> [!NOTE]
> Si le contrôleur de domaine faisant l’objet d’une mise en miroir des ports est connecté via une liaison WAN, vérifiez que celle-ci peut gérer la charge supplémentaire du trafic ERSPAN.
> ATA prend uniquement en charge la surveillance du trafic quand le trafic atteint la carte réseau et le contrôleur de domaine de la même manière. ATA ne prend pas en charge la surveillance du trafic quand celui-ci est réparti sur différents ports.

## <a name="supported-port-mirroring-options"></a>Options de mise en miroir des ports prises en charge

|Passerelle ATA|Contrôleur de domaine|Considérations|
|---------------|---------------------|------------------|
|Virtuelle|Virtuel sur le même hôte|Le commutateur virtuel doit prendre en charge la mise en miroir des ports.<br /><br />Le fait de déplacer l’une des machines virtuelles vers un autre hôte où elle sera toute seule risque de briser la mise en miroir des ports.|
|Virtuel|Virtuel sur des hôtes différents|Vérifiez que votre commutateur virtuel prend en charge ce scénario.|
|Virtuelle|Physique|Nécessite une carte réseau dédiée ; sinon, ATA détecte tout le trafic entrant et sortant de l’hôte, même le trafic qu’il envoie au centre ATA.|
|Physique|Virtuelle|Vérifiez que votre commutateur virtuel prend en charge ce scénario et configurez la mise en miroir des ports sur vos commutateurs physiques selon le cas :<br /><br />Si l’hôte virtuel se trouve sur le même commutateur physique, vous devez configurer SPAN au niveau du commutateur.<br /><br />Si l’hôte virtuel se trouve sur un autre commutateur, vous devez configurer RSPAN ou ERSPAN&#42;.|
|Physique|Physique sur le même commutateur|Le commutateur physique doit prendre en charge SPAN/la mise en miroir des ports.|
|Physique|Physique sur un autre commutateur|Exige que les commutateurs physiques prennent en charge RSPAN ou ERSPAN&#42;.|

&#42; ERSPAN est uniquement pris en charge quand la décapsulation est effectuée avant l’analyse du trafic par ATA.

> [!NOTE]
> Vérifiez que l’heure des contrôleurs de domaine et des passerelles ATA auxquelles ils se connectent est synchronisée de manière à ce que tout écart entre eux ne dépasse pas cinq minutes.

**Si vous travaillez avec des clusters de virtualisation :**

-   Pour chaque contrôleur de domaine en cours d’exécution sur le cluster de virtualisation dans une machine virtuelle avec la passerelle ATA, configurez l’affinité entre le contrôleur de domaine et la passerelle ATA. Ainsi, quand le contrôleur de domaine passe à un autre hôte dans le cluster, la passerelle ATA le suit. Cela fonctionne bien quand il y a quelques contrôleurs de domaine.

> [!NOTE]
> Si votre environnement prend en charge la configuration « virtuel à virtuel » sur différents hôtes (RSPAN), vous n’avez pas à vous soucier de l’affinité.

-   Pour faire en sorte que les passerelles ATA soient correctement dimensionnées pour gérer par elles-mêmes le monitoring de tous les contrôleurs de domaine, essayez cette option : installez une machine virtuelle sur chaque hôte de virtualisation et une passerelle ATA sur chaque hôte. Configurez chaque passerelle ATA de façon à surveiller tous les contrôleurs de domaine qui s’exécutent sur le cluster. Ainsi, n’importe quel hôte sur lequel les contrôleurs de domaine s’exécutent est surveillé.

Après avoir configuré la mise en miroir des ports, validez son fonctionnement avant d’installer la passerelle ATA.

## <a name="see-also"></a>Voir aussi
- [Valider la mise en miroir des ports](validate-port-mirroring.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
