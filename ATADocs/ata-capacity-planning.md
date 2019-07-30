---
title: Planification de votre déploiement Advanced Threat Analytics | Microsoft Docs
description: Vous aide à planifier votre déploiement et à déterminer le nombre de serveurs ATA nécessaires pour prendre en charge votre réseau
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/28/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.assetid: 1b5b24ff-0df8-4660-b4f8-64d68cc72f65
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c77f855066f8385925dc9039c6532f1981ac0dfe
ms.sourcegitcommit: dd8c94db68e85752c20bba3446b678cd1edcd932
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2019
ms.locfileid: "68604358"
---
# <a name="ata-capacity-planning"></a>Planification de la capacité ATA

*S’applique à : Advanced Threat Analytics version 1.9*

Cet article vous aide à déterminer le nombre de serveurs ATA nécessaires pour surveiller votre réseau. Il vous aide également à déterminer le nombre de passerelles ATA et/ou passerelles légères ATA dont vous avez besoin, et la capacité du serveur pour votre centre ATA et les passerelles ATA.

> [!NOTE] 
> Vous pouvez déployer le Centre ATA sur n’importe quel fournisseur IaaS du moment que vous respectez les critères de performance décrits dans cet article.

## <a name="using-the-sizing-tool"></a>Utilisation de l’outil de dimensionnement
La manière recommandée la plus simple de déterminer la capacité pour votre déploiement ATA est d’utiliser l’[outil de dimensionnement ATA](http://aka.ms/atasizingtool). Exécutez l’outil de dimensionnement ATA, puis dans les résultats du fichier Excel, utilisez les champs suivants pour déterminer la capacité ATA dont vous avez besoin :

- Processeur et mémoire du centre ATA : faites correspondre le champ **Paquets occupés/s** du tableau du centre ATA dans le fichier de résultats avec le champ **PAQUETS PAR SECONDE** du [tableau du centre ATA](#ata-center-sizing).

- Stockage du centre ATA : faites correspondre le champ **Moyenne de paquets/s** du tableau du centre ATA dans le fichier de résultats avec le champ **PAQUETS PAR SECONDE** du [tableau du centre ATA](#ata-center-sizing).
- Passerelle ATA : faites correspondre le champ **Paquets occupés/s** du tableau de la passerelle ATA du fichier de résultats avec le champ **PAQUETS PAR SECONDE** du [tableau de la passerelle ATA](#ata-gateway-sizing) ou du [tableau de la passerelle légère ATA](#ata-lightweight-gateway-sizing) en fonction du [type de passerelle choisi](#choosing-the-right-gateway-type-for-your-deployment).


![Exemple d’outil de planification des capacités](media/capacity-tool.png)


> [!NOTE]
> Étant donné que les différents environnements varient et présentent plusieurs caractéristiques de trafic réseau particulières et imprévisibles, une fois que vous déployez initialement ATA et exécuter l’outil de dimensionnement, vous devrez peut-être ajuster et adapter votre déploiement au niveau de la capacité.


Si pour une raison ou une autre, vous ne pouvez pas utiliser l’outil de dimensionnement ATA, collectez manuellement les informations du compteur de paquets/s de tous vos contrôleurs de domaine pendant 24 heures avec un intervalle de collecte court (environ 5 secondes). Ensuite, pour chaque contrôleur de domaine, vous devez calculer la moyenne quotidienne et la moyenne des périodes les plus occupées (15 minutes).
Les sections suivantes expliquent comment collecter le compteur paquets/s dans un contrôleur de domaine.


> [!NOTE]
> Étant donné que les différents environnements varient et présentent plusieurs caractéristiques de trafic réseau particulières et imprévisibles, une fois que vous déployez initialement ATA et exécuter l’outil de dimensionnement, vous devrez peut-être ajuster et adapter votre déploiement au niveau de la capacité.


### <a name="ata-center-sizing"></a>Dimensionnement du centre ATA
Le centre ATA nécessite l’équivalent de 30 jours de données qui est le minimum recommandé pour obtenir des analyses comportementales des utilisateurs.
 

|Paquets par seconde pour tous les contrôleurs de domaine|Processeur (cores&#42;)|Mémoire (Go)|Stockage de la base de données par jour (Go)|Stockage de la base de données par mois (Go)|IOPS&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1 000|2|32|0.3|9|30 (100)
|40 000|4|48|12|360|500 (750)
|200 000|8|64|60|1 800|1 000 (1 500)
|400,000|12|96|120|3,600|2 000 (2 500)
|750,000|24|112|225|6,750|2,500 (3,000)
|1,000,000|40|128|300|9 000|4,000 (5,000)

&#42; Cela comprend des cœurs physiques et non des cœurs hyper-thread.

&#42;&#42;Nombres moyens (pic)
> [!NOTE]
> - Le centre ATA peut gérer un maximum agrégé de 1 million de paquets par seconde provenant de l’ensemble des contrôleurs de domaine surveillés. Dans certains environnements, le même centre ATA peut gérer un trafic global supérieur à 1 million. Contactez askcesec@microsoft.com pour obtenir de l’assistance sur ce type d’environnements.
> - Si l’espace libre atteint la valeur minimale de 20 % ou 200 Go, la collecte de données la plus ancienne est supprimée. S’il n’est pas possible de réduire la collecte de données à ce niveau, une alerte est consignée.  ATA continue de fonctionner jusqu’à ce que le seuil de 5 % ou de 50 Go d’espace disponible soit atteint.  S’il est atteint, ATA arrête de remplir la base de données et une nouvelle alerte est émise.
> - Il vous est possible de déployer le Centre ATA sur n’importe quel fournisseur IaaS du moment que vous respectez les critères de performance qui sont décrits dans cet article.
> - La latence de stockage pour les activités de lecture et d’écriture doit être inférieure à 10 ms.
> - Le rapport entre les activités de lecture et d’écriture est d’environ 1 pour 3 en dessous de 100 000 paquets par seconde et de 1 pour 6 au-dessus de 100 000 paquets par seconde.
> - En cas d’exécution en tant que machine virtuelle, la mémoire dynamique ou toute autre fonctionnalité d’augmentation de la mémoire n’est pas prise en charge. Pour plus d’informations sur l’exécution du centre ATA en tant que machine virtuelle, consultez [Configuration requise pour le centre ATA](https://docs.microsoft.com/advanced-threat-analytics/ata-prerequisites#ata-center-requirements)
> - Pour bénéficier de performances optimales, choisissez **Hautes performances** comme **Option d’alimentation** pour le centre ATA.<br>
> - Sur un serveur physique, la base de données ATA nécessite la **désactivation** de l’accès mémoire non uniforme (NUMA) dans le BIOS. Votre système peut utiliser l’entrelacement de nœuds pour faire référence à NUMA, auquel cas vous devez **activer** l’entrelacement de nœuds pour désactiver NUMA. Pour plus d’informations, consultez la documentation du BIOS. Notez que cela ne s’applique pas quand le centre ATA s’exécute sur un serveur virtuel.


## <a name="choosing-the-right-gateway-type-for-your-deployment"></a>Choix du type de passerelle appropriée pour votre déploiement
Dans un déploiement ATA, toutes les combinaisons de types de passerelles ATA sont prises en charge :

- Passerelles ATA uniquement
- Passerelles légères ATA uniquement
- Une combinaison des deux

Quand vous choisissez le type de déploiement de passerelle, prenez en compte les avantages suivants :

|Type de passerelle|Avantages|Coût|Topologie de déploiement|Utilisation des contrôleurs de domaine|
|----|----|----|----|-----|
|Passerelle ATA|Avec un déploiement hors bande, il est plus difficile pour les agresseurs de détecter qu’ATA est présent|Plus élevé|Installée en même temps que le contrôleur de domaine (hors bande)|Prend en charge jusqu’à 50 000 paquets par seconde|
|Passerelle légère ATA|Ne nécessite pas de configuration de la mise en miroir de port ni de serveur dédié|Plus faible|Installée sur un contrôleur de domaine|Prend en charge jusqu’à 10 000 paquets par seconde|

Voici quelques exemples de scénarios dans lesquels les contrôleurs de domaine doivent être couverts par la passerelle légère ATA :


- Sites de succursale

- Contrôleurs de domaine virtuels déployés dans le cloud (IaaS)


Voici quelques exemples de scénarios dans lesquels les contrôleurs de domaine doivent être couverts par la passerelle ATA :


- Siège social de centres de données (comptant des contrôleurs de domaine avec plus de 10 000 paquets par seconde)


### <a name="ata-lightweight-gateway-sizing"></a>Dimensionnement de passerelle légère ATA

Une passerelle légère ATA peut prendre en charge la surveillance d’un contrôleur de domaine en fonction de la quantité de trafic réseau qu’il génère. 


|Paquets par seconde&#42;|Unité centrale (cœurs&#42;&#42;)|Mémoire (Go)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1 000|2|6\.|
|5 000|6\.|16|
    |10 000|10|24|

&#42;Nombre total de paquets par seconde sur le contrôleur de domaine surveillé par une passerelle légère ATA donnée.

&#42;&#42;Nombre total de cœurs non multithreads installés sur ce contrôleur de domaine.<br>Même si le multithread est acceptable pour la passerelle légère ATA, vous devez compter les cœurs réels et non les cœurs multithreads lors de la planification de la capacité.

&#42;&#42;&#42;Quantité totale de mémoire installée sur ce contrôleur de domaine.

> [!NOTE]   
> -   Si le contrôleur de domaine n’a pas les ressources demandées par la passerelle légère ATA, les performances du contrôleur de domaine ne sont pas affectées, mais la passerelle légère ATA risque de ne pas fonctionner comme prévu.
> -   En cas d’exécution en tant que machine virtuelle, la mémoire dynamique ou toute autre fonctionnalité d’augmentation de la mémoire n’est pas prise en charge. Pour plus d’informations sur l’exécution du centre ATA en tant que machine virtuelle, consultez [Configuration requise pour le centre ATA](https://docs.microsoft.com/advanced-threat-analytics/ata-prerequisites#ata-center-requirements)
> -   Pour bénéficier de performances optimales, choisissez **Hautes performances** comme **Option d’alimentation** pour la passerelle légère ATA.
> -   Au moins 5 Go d’espace sont nécessaires, 10 Go sont recommandés, notamment pour les fichiers binaires ATA, les [journaux ATA](troubleshooting-ata-using-logs.md) et les [journaux des performances](troubleshooting-ata-using-perf-counters.md).


### <a name="ata-gateway-sizing"></a>Dimensionnement de la passerelle ATA

Prenez en compte les problèmes suivants quand vous choisissez le nombre de passerelles ATA à déployer.

-   **Forêts et domaines Active Directory**<br>
    ATA peut surveiller le trafic provenant de plusieurs domaines d’une même forêt Active Directory. La surveillance de plusieurs forêts Active Directory nécessite des déploiements ATA distincts. Ne configurez pas un déploiement ATA unique pour surveiller le trafic réseau des contrôleurs de domaine de différentes forêts.

-   **Mise en miroir des ports**<br>
Les considérations relatives à la mise en miroir des ports peuvent vous amener à déployer plusieurs passerelles ATA par site de succursale ou centre de données.

-   **Capacité**<br>
    Une passerelle ATA peut prendre en charge la surveillance de plusieurs contrôleurs de domaine, en fonction de la quantité de trafic réseau des contrôleurs de domaine surveillés. 
<br>



|Paquets par seconde&#42;|Unité centrale (cœurs&#42;&#42;)|Mémoire (Go)|
|---------------------------|-------------------------|---------------|
|1 000|1|6\.|
|5 000|2|10|
|10 000|3|12|
|20 000|6\.|24|
|50 000|16|48|

&#42;Nombre total moyen de paquets par seconde provenant de l’ensemble des contrôleurs de domaine surveillés par une passerelle ATA donnée durant leur heure de la journée la plus occupée.

&#42; La quantité totale de trafic des contrôleurs de domaine avec mise en miroir des ports ne peut pas dépasser la capacité de la carte réseau de capture de la passerelle ATA.

&#42;&#42; L’hyper-threading doit être désactivé.

> [!NOTE] 
> -   La mémoire dynamique n’est pas prise en charge.
> -   Pour bénéficier de performances optimales, choisissez **Hautes performances** comme **Option d’alimentation** pour la passerelle ATA.
> -   Au moins 5 Go d’espace sont nécessaires, 10 Go sont recommandés, notamment pour les fichiers binaires ATA, les [journaux ATA](troubleshooting-ata-using-logs.md) et les [journaux des performances](troubleshooting-ata-using-perf-counters.md).



## <a name="related-videos"></a>Vidéos connexes
- [Sélection du type de passerelle ATA approprié](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement ATA](http://aka.ms/atasizingtool)
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Architecture d’ATA](ata-architecture.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
