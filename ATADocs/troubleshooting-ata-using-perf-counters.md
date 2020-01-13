---
title: Résolution des problèmes d’Advanced Threat Analytics avec les compteurs de performances | Microsoft Docs
description: Explique comment utiliser les compteurs de performances pour résoudre les problèmes liés à ATA
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 9/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: df162a62-f273-4465-9887-94271f5000d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 495813678b18b71af45240e18c40fdab5a5154a3
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75908217"
---
# <a name="troubleshooting-ata-using-the-performance-counters"></a>Résolution des problèmes liés à ATA à l’aide des compteurs de performances

*S’applique à : Advanced Threat Analytics version 1.9*

Les compteurs de performances ATA vous permettent de savoir si les composants ATA s’exécutent correctement. Les composants ATA traitant les données de manière séquentielle, la présence d’un problème peut entraîner le rejet partiel du trafic quelque part le long de la chaîne de composants. Pour résoudre le problème, vous devez déterminer le composant impliqué et résoudre le problème au début de la chaîne. Utilisez les données fournies par les compteurs de performance pour comprendre comment fonctionne chaque composant.
Pour comprendre le flux des composants ATA internes, voir [Architecture ATA](ata-architecture.md).

**Processus des composants ATA** :

1.  Quand un composant atteint sa taille maximale, il empêche le composant qui le précède de lui envoyer des entités supplémentaires.

2.  En conséquence, le composant précédent augmente **sa propre** taille jusqu’à empêcher le composant qui le précède d’envoyer des entités.

3.  Ce cas se produit jusqu’au composant NetworkListener qui supprime le trafic quand il ne peut plus transférer d’entités.


## <a name="retrieving-performance-monitor-files-for-troubleshooting"></a>Récupération des fichiers de surveillance des performances pour la résolution des problèmes

Pour récupérer les fichiers de surveillance des performances (BLG) à partir de divers composants ATA :
1.  Ouvrez l’Analyseur de performances.
2.  Arrêtez l’ensemble de collecteurs de données nommé : **Microsoft ATA Gateway** ou **Microsoft ATA Center**.
3.  Accédez au dossier de l’ensemble de collecteurs de données (par défaut, il s’agit de « C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs\DataCollectorSets » ou de « C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs\DataCollectorSets »).
4.  Copiez le fichier BLG qui a été modifié le plus récemment.
5.  Redémarrez l’ensemble de collecteurs de données nommé : **Microsoft ATA Gateway** ou **Microsoft ATA Center**.


## <a name="ata-gateway-performance-counters"></a>Compteurs de performances de la passerelle ATA

Dans cette section, chaque référence à la passerelle ATA fait également référence à la passerelle légère ATA.

Vous pouvez observer l’état des performances de la passerelle ATA en temps réel en ajoutant des compteurs de performances à la passerelle ATA.
Pour cela, ouvrez l’**Analyseur de performances**, puis ajoutez tous les compteurs à la passerelle ATA. Le nom de l’objet de compteur de performances est : **Microsoft ATA Gateway**.

Voici la liste des principaux compteurs de passerelle ATA :

> [!div class="mx-tableFixed"]
> 
> |Compteur|Description|Seuil|Résolution des problèmes|
> |-----------|---------------|-------------|-------------------|
> |Passerelle Microsoft ATA\Messages analysés PEF NetworkListener\s|Quantité de trafic traitée par la passerelle ATA chaque seconde.|Aucun seuil|Aide à comprendre la quantité de trafic qui est analysée par la passerelle ATA.|
> |Événements supprimés PEF NetworkListener\s|Quantité de trafic supprimée par la passerelle ATA chaque seconde.|Ce nombre doit toujours être égal à zéro (de rares suppressions en rafales sont acceptables).|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
> |Passerelle Microsoft ATA\Événements supprimés NetworkListener ETW\s|Quantité de trafic supprimée par la passerelle ATA chaque seconde.|Ce nombre doit toujours être égal à zéro (de rares suppressions en rafales sont acceptables).|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
> |Passerelle Microsoft ATA\Données de messages NetworkActivityTranslator # Taille de blocs|Quantité de trafic mise en file d’attente pour la traduction en activités réseau.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 100 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
> |Passerelle Microsoft ATA\Taille de blocs d’activité EntityResolver|Nombre d’activités réseau en attente de résolution.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 10 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
> |Passerelle Microsoft ATA\Taille de blocs de lots d’entités EntitySender|Quantité d’activités réseau en attente d’envoi vers le centre ATA.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 1 000 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
> |Passerelle Microsoft ATA\Temps d’envoi des lots EntitySender|Durée nécessaire pour envoyer le dernier lot.|Doit être inférieur à 1 000 millisecondes dans la plupart des cas|Vérifiez la présence de problèmes réseau entre la passerelle ATA et le centre ATA.|
> 
> [!NOTE]
> -   Les valeurs temporelles des compteurs sont exprimées en millisecondes.
> -   Il est parfois plus pratique de surveiller tous les compteurs en même temps à l’aide du type de graphe **Rapport** (par exemple : monitoring en temps réel de l’ensemble des compteurs)

## <a name="ata-lightweight-gateway-performance-counters"></a>Compteurs de performance de la passerelle légère ATA
Vous pouvez utiliser les compteurs de performances pour la gestion de quota dans la passerelle légère, pour vous assurer qu’ATA n’épuise pas trop les ressources des contrôleurs de domaine sur lesquels il est installé.
Pour mesurer les limitations de ressources appliquées par ATA sur la passerelle légère, ajoutez ces compteurs.

Pour cela, ouvrez l’**Analyseur de performances** et ajoutez tous les compteurs à la passerelle légère ATA. Les noms des objets de compteurs de performance sont : **Microsoft ATA Gateway** et **Microsoft ATA Gateway Updater**.

> [!div class="mx-tableFixed"]
> 
> |Compteur|Description|Seuil|Résolution des problèmes|
> |-----------|---------------|-------------|-------------------|
> |Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager CPU Time Max %|Quantité maximale de temps processeur (en pourcentage) que le processus de passerelle légère peut consommer. |Aucun seuil. | Il s’agit de la limitation qui empêche que toutes les ressources du contrôleur de domaine soient utilisées par la passerelle légère ATA. Si vous voyez que le processus atteint souvent la limite maximale sur une période donnée (le processus atteint la limite, puis commence à ignorer le trafic), cela signifie que vous devez ajouter des ressources au serveur qui exécute le contrôleur de domaine.|
> |Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Commit Memory Max Size|Quantité maximale de mémoire allouée (en octets) que le processus de passerelle légère peut consommer.|Aucun seuil. | Il s’agit de la limitation qui empêche que toutes les ressources du contrôleur de domaine soient utilisées par la passerelle légère ATA. Si vous voyez que le processus atteint souvent la limite maximale sur une période donnée (le processus atteint la limite, puis commence à ignorer le trafic), cela signifie que vous devez ajouter des ressources au serveur qui exécute le contrôleur de domaine.| 
> |Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Working Set Limit Size|Quantité maximale de mémoire physique (en octets) que le processus de passerelle légère peut consommer.|Aucun seuil. | Il s’agit de la limitation qui empêche que toutes les ressources du contrôleur de domaine soient utilisées par la passerelle légère ATA. Si vous voyez que le processus atteint souvent la limite maximale sur une période donnée (le processus atteint la limite, puis commence à ignorer le trafic), cela signifie que vous devez ajouter des ressources au serveur qui exécute le contrôleur de domaine.|



Pour connaître la consommation réelle, consultez les compteurs suivants :


> [!div class="mx-tableFixed"]
> 
> |Compteur|Description|Seuil|Résolution des problèmes|
> |-----------|---------------|-------------|-------------------|
> |Process(Microsoft.Tri.Gateway)\%Processor Time|Temps processeur (en pourcentage) réellement consommé par le processus de passerelle légère. |Aucun seuil. | Comparez les résultats de ce compteur à la limite indiquée dans GatewayUpdaterResourceManager CPU Time Max %. Si vous voyez que le processus atteint souvent la limite maximale sur une période donnée (le processus atteint la limite, puis commence à ignorer le trafic), cela signifie que vous devez allouer davantage de ressources à la passerelle légère.|
> |Process(Microsoft.Tri.Gateway)\Private Bytes|Quantité de mémoire allouée (en octets) réellement consommée par le processus de passerelle légère.|Aucun seuil. | Comparez les résultats de ce compteur à la limite indiquée dans GatewayUpdaterResourceManager Commit Memory Max Size. Si vous voyez que le processus atteint souvent la limite maximale sur une période donnée (le processus atteint la limite, puis commence à ignorer le trafic), cela signifie que vous devez allouer davantage de ressources à la passerelle légère.| 
> |Process(Microsoft.Tri.Gateway)\Working Set|Quantité de mémoire physique (en octets) réellement consommée par le processus de passerelle légère.|Aucun seuil. |Comparez les résultats de ce compteur à la limite indiquée dans GatewayUpdaterResourceManager Working Set Limit Size. Si vous voyez que le processus atteint souvent la limite maximale sur une période donnée (le processus atteint la limite, puis commence à ignorer le trafic), cela signifie que vous devez allouer davantage de ressources à la passerelle légère.|

## <a name="ata-center-performance-counters"></a>Compteurs de performances du centre ATA
Vous pouvez observer l’état des performances du centre ATA en temps réel en ajoutant des compteurs de performances au centre ATA.

Pour cela, ouvrez l’**Analyseur de performances** et ajoutez tous les compteurs au centre ATA. Le nom de l’objet de compteur de performances est **Microsoft ATA Center**.

Voici la liste des principaux compteurs du centre ATA :

> [!div class="mx-tableFixed"]
> 
> |Compteur|Description|Seuil|Résolution des problèmes|
> |-----------|---------------|-------------|-------------------|
> |Microsoft ATA Center\EntityReceiver Entity Batch Block Size|Nombre de lots d’entités mis en file d’attente par le centre ATA.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 10 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener.  Reportez-vous à la section **Processus des composants ATA** précédente.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
> |Microsoft ATA Center\NetworkActivityProcessor Network Activity Block Size|Nombre d’activités réseau en attente de traitement.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 50 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à la section **Processus des composants ATA** précédente.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
> |Microsoft ATA Center\EntityProfiler Network Activity Block Size|Nombre d’activités réseau en attente de profilage.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 100 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à la section **Processus des composants ATA** précédente.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
> |Centre Microsoft ATA\Base de données &#42; Taille de bloc|Nombre d’activités réseau d’un type spécifique en attente d’écriture dans la base de données.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 50 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à la section **Processus des composants ATA** précédente.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
> 
> 
> [!NOTE]
> -   Les valeurs temporelles des compteurs sont exprimées en millisecondes.
> -   Il est parfois plus pratique de surveiller tous les compteurs en même temps à l’aide du graphique « Rapport » (par exemple : surveillance en temps réel de l’ensemble des compteurs).

## <a name="operating-system-counters"></a>Compteurs de système d’exploitation
Voici le tableau des principaux compteurs de système d’exploitation à prendre en compte :

> [!div class="mx-tableFixed"]
> 
> |Compteur|Description|Seuil|Résolution des problèmes|
> |-----------|---------------|-------------|-------------------|
> |Processeur(_Total)\% de temps processeur|Durée (en pourcentage) que le processeur met pour exécuter des threads actifs.|Inférieur à 80 % en moyenne|Vérifiez si l’un des processus prend beaucoup plus de temps processeur qu’il ne devrait.<br /><br />Ajoutez des processeurs.<br /><br />Réduisez la quantité de trafic sur chaque serveur.<br /><br />Le compteur « Processeur(_Total)\% de temps processeur » peut être moins précis sur les serveurs virtuels. Dans ce cas, le moyen le plus précis de mesurer le manque de puissance du processeur est d’utiliser le compteur « System\Longueur de la file du processeur ».|
> |Système\Commutateurs de contexte\s|Taux combiné auquel tous les processeurs commutent d’un thread à l’autre.|Inférieur à 5 000 cœurs&#42; (cœurs physiques)|Vérifiez si l’un des processus prend beaucoup plus de temps processeur qu’il ne devrait.<br /><br />Ajoutez des processeurs.<br /><br />Réduisez la quantité de trafic sur chaque serveur.<br /><br />Le compteur « Processeur(_Total)\% de temps processeur » peut être moins précis sur les serveurs virtuels. Dans ce cas, le moyen le plus précis de mesurer le manque de puissance du processeur est d’utiliser le compteur « System\Longueur de la file du processeur ».|
> |Système\Longueur de la file du processeur|Nombre de threads prêts à être exécutés et en attente de planification.|Inférieur à cinq&#42;cœurs (cœurs physiques)|Vérifiez si l’un des processus prend beaucoup plus de temps processeur qu’il ne devrait.<br /><br />Ajoutez des processeurs.<br /><br />Réduisez la quantité de trafic sur chaque serveur.<br /><br />Le compteur « Processeur(_Total)\% de temps processeur » peut être moins précis sur les serveurs virtuels. Dans ce cas, le moyen le plus précis de mesurer le manque de puissance du processeur est d’utiliser le compteur « System\Longueur de la file du processeur ».|
> |Mémoire\Mo disponibles|Quantité de mémoire physique (RAM) disponible pour l’allocation.|Doit être supérieur à 512|Vérifiez si l’un des processus prend beaucoup plus de mémoire physique qu’il ne devrait.<br /><br />Augmentez la quantité de mémoire physique.<br /><br />Réduisez la quantité de trafic sur chaque serveur.|
> |Disque logique&#42;() \Moy. sec\Read|Latence moyenne de lecture des données à partir du disque (vous devez choisir le lecteur de base de données comme instance).|Doit être inférieur à 10 millisecondes|Vérifiez si l’un des processus utilise le lecteur de la base de données plus qu’il ne devrait.<br /><br />Consultez l’équipe ou le fournisseur en charge du stockage pour savoir si ce lecteur peut fournir la charge de travail actuelle avec une latence inférieure à 10 ms. La charge de travail actuelle peut être déterminée à l’aide des compteurs d’utilisation du disque.|
> |Disque logique&#42;() \Moy. sec\Write|Latence moyenne d’écriture des données sur le disque (vous devez choisir le lecteur de base de données comme instance).|Doit être inférieur à 10 millisecondes|Vérifiez si l’un des processus utilise le lecteur de la base de données plus qu’il ne devrait.<br /><br />Consultez l’équipe ou le fournisseur en charge du stockage pour savoir si ce lecteur peut fournir la charge de travail actuelle avec une latence inférieure à 10 ms. La charge de travail actuelle peut être déterminée à l’aide des compteurs d’utilisation du disque.|
> |\LogicalDisk(&#42;)\Lectures disque\s|Taux d’opérations de lecture sur le disque.|Aucun seuil|Les compteurs d’utilisation du disque peuvent apporter des informations utiles à la résolution des problèmes de latence de stockage.|
> |\LogicalDisk(&#42;)\Octets de lecture disque\s|Nombre d’octets lus par seconde sur le disque.|Aucun seuil|Les compteurs d’utilisation du disque peuvent apporter des informations utiles à la résolution des problèmes de latence de stockage.|
> |\LogicalDisk&#42;\Écritures disque\s|Taux d’opérations d’écriture sur le disque.|Aucun seuil|Compteurs d’utilisation du disque (peuvent apporter des informations utiles à la résolution des problèmes de latence de stockage).|
> |\LogicalDisk(&#42;)\Octets d’écriture disque\s|Nombre d’octets écrits par seconde sur le disque.|Aucun seuil|Les compteurs d’utilisation du disque peuvent apporter des informations utiles à la résolution des problèmes de latence de stockage.|

## <a name="see-also"></a>Voir aussi
- [Configuration requise pour ATA](ata-prerequisites.md)
- [Planification de la capacité d’ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
