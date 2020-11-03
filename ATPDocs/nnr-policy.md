---
title: Microsoft Defender for Identity Network Name Resolution
description: Cet article fournit une vue d’ensemble de la fonctionnalité avancée de résolution de noms de réseau de Microsoft Defender et utilise.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 228d583fde3e08c497721e0aa5a8aa1b61318937
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93274788"
---
# <a name="what-is-network-name-resolution"></a>Présentation de la résolution de noms réseau

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

La résolution de noms de réseau (NNR) est un composant principal des  [!INCLUDE [Product long](includes/product-long.md)] fonctionnalités. [!INCLUDE [Product short](includes/product-short.md)] capture les activités basées sur le trafic réseau, les événements Windows et ETW. ces activités contiennent normalement des données IP.

À l’aide de NNR, [!INCLUDE [Product short](includes/product-short.md)] peut corréler entre des activités brutes (contenant des adresses IP) et les ordinateurs concernés impliqués dans chaque activité. En fonction des activités brutes, [!INCLUDE [Product short](includes/product-short.md)] profils entités, y compris les ordinateurs, et génère des alertes de sécurité pour les activités suspectes.

Pour résoudre les adresses IP en noms d’ordinateur, [!INCLUDE [Product short](includes/product-short.md)] les capteurs recherchent les adresses IP à l’aide des méthodes suivantes :

- NTLM sur RPC (port TCP 135)
- NetBIOS (port UDP 137)
- RDP (port TCP 3389), seulement le premier paquet de **Client hello**
- Interroge le serveur DNS par recherche DNS inversée de l’adresse IP (UDP 53)

Pour obtenir les meilleurs résultats, nous vous recommandons d’utiliser toutes les méthodes. Si ce n’est pas possible, vous devez utiliser la méthode de recherche DNS et au moins l’une des autres méthodes.

> [!NOTE]
> Aucune authentification n’est effectuée sur aucun des ports.

[!INCLUDE [Product short](includes/product-short.md)] évalue et détermine le système d’exploitation de l’appareil en fonction du trafic réseau. Après avoir récupéré le nom de l’ordinateur, le [!INCLUDE [Product short](includes/product-short.md)] capteur vérifie Active Directory et utilise les empreintes digitales TCP pour voir s’il existe un objet ordinateur corrélé portant le même nom d’ordinateur. L’utilisation d’empreintes TCP permet d’identifier les appareils non inscrits et non-Windows, facilitant ainsi vos processus d’investigation.
Lorsque le [!INCLUDE [Product short](includes/product-short.md)] capteur trouve la corrélation, le capteur associe l’adresse IP à l’objet ordinateur.

Dans les cas où aucun nom n’est récupéré, un **profil d’ordinateur non résolu par adresse IP** est créé, contenant l’adresse IP et l’activité détectée correspondante.

![Profil d’ordinateur non résolu](media/unresolved-computer-profile.png)

Les données NNR sont cruciales pour détecter les alertes suivantes :

- Suspicion d’usurpation d’identité (pass-the-ticket)
- Suspicion d’attaque DCSync (réplication de services d’annuaire)
- Reconnaissance de mappage de réseau (DNS)

Pour améliorer votre capacité à déterminer si une alerte est un **vrai positif (TP)** ou un **faux positif (FP)** , [!INCLUDE [Product short](includes/product-short.md)] comprend le degré de certitude de la résolution des noms d’ordinateur dans la preuve de chaque alerte de sécurité.

Par exemple, si des noms d’ordinateurs sont résolus avec une **certitude élevée** , cela augmente la confiance que l’alerte de sécurité qui en résulte est un **vrai positif** ou **TP**.

La preuve inclut l’heure, l’adresse IP et le nom de l’ordinateur qui ont permis la résolution de l’adresse IP. Lorsque la certitude de résolution est **faible** , utilisez ces informations pour identifier l’appareil qui était la source réelle de l’adresse IP à cet instant.
Après avoir confirmé l’appareil, vous pouvez déterminer si l’alerte est un **faux positif** ou **FP** , comme dans les exemples suivants :

- Suspicion d’usurpation d’identité (pass-the-ticket) : l’alerte a été déclenchée pour le même ordinateur.
- Suspicion d’attaque DCSync (réplication de services d’annuaire) : l’alerte a été déclenchée à partir d’un contrôleur de domaine.
- Reconnaissance de mappage réseau (DNS) : l’alerte réseau a été déclenchée à partir d’un serveur DNS.

    ![Certitude de la preuve](media/nnr-high-certainty.png)

### <a name="prerequisites"></a>Prérequis

|Protocole|Transport|Port|Appareil|Sens|
|--------|--------|------|-------|------|
|NTLM sur RPC *|TCP|135|Tous les appareils sur le réseau|Trafic entrant|
|NetBIOS|UDP|137|Tous les appareils sur le réseau|Trafic entrant|
|RDP|TCP|3389|Tous les appareils sur le réseau|Trafic entrant|
|DNS|UDP|53|Contrôleurs de domaine|Sortant|

\* L’une de ces méthodes est obligatoire, mais nous vous recommandons de les utiliser toutes.

Pour vous assurer que [!INCLUDE [Product short](includes/product-short.md)] fonctionne idéalement et que l’environnement est correctement configuré, [!INCLUDE [Product short](includes/product-short.md)] vérifie l’état de résolution de chaque capteur et émet une alerte d’intégrité par méthode, en fournissant une liste des [!INCLUDE [Product short](includes/product-short.md)] capteurs avec un faible taux de réussite de la résolution de noms active à l’aide de chaque méthode.

> [!NOTE]
> Pour désactiver une méthode NNR facultative dans en [!INCLUDE [Product short](includes/product-short.md)] fonction des besoins de votre environnement, ouvrez un appel de support.

Chaque alerte d’intégrité fournit des détails spécifiques sur la méthode, les capteurs, la stratégie problématique et les recommandations de configuration.

![Alerte de résolution de noms réseau (NNR) à faible taux de réussite](media/nnr-success-rate.png)

### <a name="configuration-recommendations"></a>Recommandations relatives à la configuration

- NTLM sur RPC :
  - Vérifiez que le port TCP 135 est ouvert pour les communications entrantes à partir de [!INCLUDE [Product short](includes/product-short.md)] capteurs, sur tous les ordinateurs de l’environnement.
  - Vérifiez toute la configuration réseau, et notamment les pare-feu qui risquent d’empêcher la communication vers les ports concernés.

- NetBIOS :
  - Vérifiez que le port UDP 137 est ouvert pour les communications entrantes à partir de [!INCLUDE [Product short](includes/product-short.md)] capteurs, sur tous les ordinateurs de l’environnement.
  - Vérifiez toute la configuration réseau, et notamment les pare-feu qui risquent d’empêcher la communication vers les ports concernés.
- RDP
  - Vérifiez que le port TCP 3389 est ouvert pour les communications entrantes à partir de [!INCLUDE [Product short](includes/product-short.md)] capteurs, sur tous les ordinateurs de l’environnement.
  - Vérifiez toute la configuration réseau, et notamment les pare-feu qui risquent d’empêcher la communication vers les ports concernés.
- DNS inversé :
  - Vérifiez que le capteur peut atteindre le serveur DNS et que les zones de recherche inversée sont activées.

## <a name="see-also"></a>Voir aussi

- [[!INCLUDE [Product short](includes/product-short.md)] conditions préalables](prerequisites.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Consultez le [!INCLUDE [Product short](includes/product-short.md)] Forum !](https://aka.ms/MDIcommunity)
