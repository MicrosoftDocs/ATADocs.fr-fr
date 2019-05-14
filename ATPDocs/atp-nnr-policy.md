---
title: Résolution de noms réseau Azure Advanced Threat Protection | Microsoft Docs
description: Cet article offre une vue d’ensemble de la fonctionnalité de résolution de noms réseau avancée d’Azure ATP et de ses applications.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/31/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ac873fc-b763-41d7-878e-7c08da421cb5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1489f1b24065a153734bdd46975576d469b57f24
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196940"
---
# <a name="what-is-network-name-resolution"></a>Présentation de la résolution de noms réseau

La résolution de noms réseau (NNR) est l’un des principaux composants de la fonctionnalité Azure ATP. Azure ATP capture les activités en fonction du trafic réseau, des événements Windows et d’ETW ; or, ces activités contiennent normalement des données d’adresses IP.  

Avec la résolution de noms réseau, Azure ATP peut corréler les activités brutes (contenant des adresses IP) aux ordinateurs concernés impliqués dans chaque activité. À partir des activités brutes, Azure ATP profile les entités, notamment les ordinateurs, et génère des alertes en cas d’activité suspecte.

Pour relier les adresses IP au nom des ordinateurs, les capteurs ATP envoient une requête à l’adresse IP afin de connaître le nom d’ordinateur « sous-jacent » suivant différentes méthodes :

1. NTLM sur RPC (port TCP 135)
2. NetBIOS (port UDP 137)
3. RDP (port TCP 3389), seulement le premier paquet de **Client hello**
4. Interroger le serveur DNS à l’aide de la recherche DNS inversée de l’adresse IP (UDP 53)

> [!NOTE]
>Aucune authentification n’est effectuée sur aucun des ports.

Après avoir récupéré le nom d’ordinateur, le capteur Azure ATP regarde dans Active Directory s’il existe un objet ordinateur corrélé à ce nom d’ordinateur. Si le capteur détecte la corrélation, il associe l’adresse IP à l’objet ordinateur.

Les données NNR sont cruciales pour détecter les alertes suivantes :

- Suspicion d’usurpation d’identité (pass-the-ticket)
- Suspicion d’attaque DCSync (réplication de services d’annuaire)
- Reconnaissance de mappage de réseau (DNS)

Pour améliorer votre capacité à déterminer si une alerte est un **vrai positif (TP)** ou un **faux positif (FP)**, Azure ATP inclut le degré de certitude de résolution du nom de l’ordinateur dans la preuve de chaque alerte de sécurité. 
 
Par exemple, si des noms d’ordinateurs sont résolus avec une **certitude élevée**, cela augmente la confiance que l’alerte de sécurité qui en résulte est un **vrai positif** ou **TP**. 

La preuve inclut l’heure, l’adresse IP et le nom de l’ordinateur qui ont permis la résolution de l’adresse IP. Lorsque la certitude de résolution est **faible**, utilisez ces informations pour identifier l’appareil qui était la source réelle de l’adresse IP à cet instant. Après avoir confirmé l’appareil, vous pouvez déterminer si l’alerte est un **faux positif** ou **FP**, comme dans les exemples suivants :

- Suspicion d’usurpation d’identité (pass-the-ticket) : l’alerte a été déclenchée pour le même ordinateur.
- Suspicion d’attaque DCSync (réplication de services d’annuaire) : l’alerte a été déclenchée à partir d’un contrôleur de domaine.
- Reconnaissance de mappage réseau (DNS) : l’alerte réseau a été déclenchée à partir d’un serveur DNS.

    ![Certitude de la preuve](media/nnr-high-certainty.png)


### <a name="prerequisites"></a>Prérequis
|Protocole|  Transport|  Port|   Appareil| Sens|
|--------|--------|------|-------|------|
|NTLM sur RPC| TCP |135|   Tous les appareils sur le réseau| Entrant|
|NetBIOS|   UDP|    137|    Tous les appareils sur le réseau| Entrant|
|DNS|   UDP|    53| Contrôleurs de domaine| Sortant|
|

Lorsque le port 3389 est ouvert sur les appareils de l’environnement, le capteur Azure ATP l’utilise à des fins de résolution de noms réseau.
Il **n’est pas obligatoire** d’ouvrir le port 3389 ; c’est simplement un moyen supplémentaire d’obtenir le nom d’ordinateur si le port est déjà ouvert à d’autres fins.

Pour vérifier le fonctionnement d’Azure ATP et la bonne configuration de l’environnement, Azure ATP contrôle l’état de résolution de chaque capteur et émet une alerte de monitoring par méthode ; il donne ainsi la liste des capteurs Azure ATP affichant un faible taux de réussite de résolution de noms active pour chaque méthode.

Chaque alerte de monitoring fournit les détails de la méthode, des capteurs et de la stratégie problématique, ainsi que des recommandations de configuration.

![Alerte de résolution de noms réseau (NNR) à faible taux de réussite](media/atp-nnr-success-rate.png)


### <a name="configuration-recommendations"></a>Recommandations de configuration

- RPC sur NTLM :
    - Vérifiez que le port 135 est ouvert aux communications entrantes issues des capteurs Azure ATP, sur tous les ordinateurs de l’environnement.
    - Vérifiez toute la configuration réseau, et notamment les pare-feu qui risquent d’empêcher la communication vers les ports concernés.

- NetBIOS :
    - Vérifiez que le port 137 est ouvert aux communications entrantes issues des capteurs Azure ATP, sur tous les ordinateurs de l’environnement.
    - Vérifiez toute la configuration réseau, et notamment les pare-feu qui risquent d’empêcher la communication vers les ports concernés.
- DNS inversé :
    - Vérifiez que le capteur peut atteindre le serveur DNS et que les zones de recherche inversée sont activées.


## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)
