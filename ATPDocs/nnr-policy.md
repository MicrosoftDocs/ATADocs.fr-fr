---
title: Résolution de noms réseau Azure-protection avancée contre les menaces
description: Cet article offre une vue d’ensemble de la fonctionnalité de résolution de noms réseau avancée d’Azure ATP et de ses applications.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/22/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ac873fc-b763-41d7-878e-7c08da421cb5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ea2ca8c0c30c9819c8e6fd72bc159d2b65927e00
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828309"
---
# <a name="what-is-network-name-resolution"></a>Présentation de la résolution de noms réseau

La résolution de noms de réseau (NNR) est un composant principal des fonctionnalités de Azure ATP. Azure ATP capture les activités en fonction du trafic réseau, des événements Windows et d’ETW ; or, ces activités contiennent normalement des données d’adresses IP.

À l’aide de NNR, les Azure ATP peuvent corréler entre les activités brutes (contenant des adresses IP) et les ordinateurs concernés impliqués dans chaque activité. À partir des activités brutes, Azure ATP profile les entités, notamment les ordinateurs, et génère des alertes en cas d’activité suspecte.

Pour résoudre les adresses IP en noms d’ordinateur, les capteurs Azure ATP recherchent les adresses IP à l’aide des méthodes suivantes :

- NTLM sur RPC (port TCP 135)
- NetBIOS (port UDP 137)
- RDP (port TCP 3389), seulement le premier paquet de **Client hello**
- Interroge le serveur DNS par recherche DNS inversée de l’adresse IP (UDP 53)

Pour obtenir les meilleurs résultats, nous vous recommandons d’utiliser toutes les méthodes. Si ce n’est pas possible, vous devez utiliser la méthode de recherche DNS et au moins l’une des autres méthodes.

> [!NOTE]
> Aucune authentification n’est effectuée sur aucun des ports.

Azure ATP évalue et détermine le système d’exploitation de l’appareil en fonction du trafic réseau. Après avoir récupéré le nom d’ordinateur, le capteur Azure ATP regarde dans Active Directory et utilise les empreintes TCP pour rechercher s’il existe un objet ordinateur corrélé à ce nom d’ordinateur. L’utilisation d’empreintes TCP permet d’identifier les appareils non inscrits et non-Windows, facilitant ainsi vos processus d’investigation.
Quand le capteur ATP trouve la corrélation, il associe l’adresse IP à l’objet ordinateur.

Dans les cas où aucun nom n’est récupéré, un **profil d’ordinateur non résolu par adresse IP** est créé, contenant l’adresse IP et l’activité détectée correspondante.

![Profil d’ordinateur non résolu](media/unresolved-computer-profile.png)

Les données NNR sont cruciales pour détecter les alertes suivantes :

- Suspicion d’usurpation d’identité (pass-the-ticket)
- Suspicion d’attaque DCSync (réplication de services d’annuaire)
- Reconnaissance de mappage de réseau (DNS)

Pour améliorer votre capacité à déterminer si une alerte est un **vrai positif (TP)** ou un **faux positif (FP)**, Azure ATP inclut le degré de certitude de résolution du nom de l’ordinateur dans la preuve de chaque alerte de sécurité.

Par exemple, si des noms d’ordinateurs sont résolus avec une **certitude élevée**, cela augmente la confiance que l’alerte de sécurité qui en résulte est un **vrai positif** ou **TP**.

La preuve inclut l’heure, l’adresse IP et le nom de l’ordinateur qui ont permis la résolution de l’adresse IP. Lorsque la certitude de résolution est **faible**, utilisez ces informations pour identifier l’appareil qui était la source réelle de l’adresse IP à cet instant.
Après avoir confirmé l’appareil, vous pouvez déterminer si l’alerte est un **faux positif** ou **FP**, comme dans les exemples suivants :

- Suspicion d’usurpation d’identité (pass-the-ticket) : l’alerte a été déclenchée pour le même ordinateur.
- Suspicion d’attaque DCSync (réplication de services d’annuaire) : l’alerte a été déclenchée à partir d’un contrôleur de domaine.
- Reconnaissance de mappage réseau (DNS) : l’alerte réseau a été déclenchée à partir d’un serveur DNS.

    ![Certitude de la preuve](media/nnr-high-certainty.png)

### <a name="prerequisites"></a>Prérequis

|Protocole|Transport|Port|Appareil|Direction|
|--------|--------|------|-------|------|
|NTLM sur RPC *|TCP|135|Tous les appareils sur le réseau|Entrant|
|NetBIOS|UDP|137|Tous les appareils sur le réseau|Entrant|
|RDP|TCP|3389|Tous les appareils sur le réseau|Entrant|
|DNS|UDP|53|Contrôleurs de domaine|Sortant|

\* L’une de ces méthodes est obligatoire, mais nous vous recommandons de les utiliser toutes.

Pour vous assurer que Azure ATP fonctionne idéalement et que l’environnement est configuré correctement, Azure ATP vérifie l’état de résolution de chaque capteur et émet une alerte d’intégrité par méthode, en fournissant une liste des capteurs de Azure ATP avec un faible taux de réussite de la résolution de noms active à l’aide de chaque méthode.

> [!NOTE]
> Pour désactiver une méthode NNR facultative dans Azure ATP pour qu’elle répondre aux besoins de votre environnement, ouvrez un appel de support.

Chaque alerte d’intégrité fournit des détails spécifiques sur la méthode, les capteurs, la stratégie problématique et les recommandations de configuration.

![Alerte de résolution de noms réseau (NNR) à faible taux de réussite](media/atp-nnr-success-rate.png)

### <a name="configuration-recommendations"></a>Recommandations relatives à la configuration

- NTLM sur RPC :
  - Vérifie que le port TCP 135 est ouvert aux communications entrantes issues des capteurs Azure ATP, sur tous les ordinateurs de l’environnement.
  - Vérifiez toute la configuration réseau, et notamment les pare-feu qui risquent d’empêcher la communication vers les ports concernés.

- NetBIOS :
  - Vérifie que le port UDP 137 est ouvert aux communications entrantes issues des capteurs Azure ATP, sur tous les ordinateurs de l’environnement.
  - Vérifiez toute la configuration réseau, et notamment les pare-feu qui risquent d’empêcher la communication vers les ports concernés.
- RDP
  - Vérifiez que le port TCP 3389 est ouvert pour les communications entrantes à partir de Azure ATP capteurs sur tous les ordinateurs de l’environnement.
  - Vérifiez toute la configuration réseau, et notamment les pare-feu qui risquent d’empêcher la communication vers les ports concernés.
- DNS inversé :
  - Vérifiez que le capteur peut atteindre le serveur DNS et que les zones de recherche inversée sont activées.

## <a name="see-also"></a>Voir aussi

- [Prérequis d’Azure ATP](prerequisites.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)