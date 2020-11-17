---
title: Informations de référence sur les ID d’événement ATA | Microsoft Docs
description: Fournit une liste des ID d’événement ATA et leurs descriptions.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 3d7c66c907cc237ae3458d77b25e486a90f01e2b
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690701"
---
# <a name="ata-event-id-reference"></a>Informations de référence sur les ID d’événement ATA


[!INCLUDE [Banner for top of topics](includes/banner.md)]

L’Observateur d’événements du centre ATA journalise les événements pour ATA. Cet article fournit une liste d’ID d’événement et une description de chacun d’eux.

Vous trouverez les événements ici :

![emplacement des ID d’événement](media/event-id-location.png)

## <a name="ata-health-events"></a>Événements d’intégrité ATA

|ID de l’événement|Nom de l’alerte|
|---------|---------------|
|1001|Espace disque du centre insuffisant|
|1003|Centre surchargé|
|1004|Le certificat du centre va expirer / Le certificat du centre a expiré|
|1005|MongoDB en panne|
|1006|Le mot de passe utilisateur en lecture seule va expirer / Le mot de passe utilisateur en lecture seule a expiré|
|1007|Synchronisateur de domaine non affecté|
|1008|Tout ou partie des cartes réseau de capture sur une passerelle ne sont pas disponibles|
|1009|Un adaptateur de réseau de capture sur une passerelle n’existe plus|
|1010|Certains contrôleurs de domaine ne sont pas accessibles par une passerelle / Tous les contrôleurs de domaine ne sont pas accessibles par une passerelle|
|1010|La passerelle a cessé de communiquer|
|1012|Certains événements transférés ne sont pas analysés|
|1013|Une partie du trafic réseau n’est pas analysé|
|1014|Échec de l’envoi des e-mails|
|1015|Échec de la connexion au serveur SIEM à l’aide de Syslog|
|1016|Version de la passerelle obsolète|
|1017|Aucun trafic reçu du contrôleur de domaine|
|1018|Échec du démarrage du service de passerelle|
|1019|La passerelle légère a atteint la limite des ressources mémoire|
|1020|La passerelle ne traite pas les événements Radius|
|1021|La passerelle ne traite pas les événements Syslog|
|1022|Le service de géolocalisation n'est pas disponible|
 
## <a name="ata-security-alert-events"></a>Événements d'alerte de sécurité ATA

|ID de l’événement|Nom de l’alerte|
|---------|---------------|
|2001|Suspicion d’usurpation d’identité basée sur un comportement inhabituel|
|2002|Implémentation de protocole inhabituelle|
|2003|Reconnaissance à l’aide de l’énumération de compte|
|2004|Attaque par force brute par le biais d’une liaison simple LDAP|
|2006|Réplication malveillante de services d’annuaire|
|2007|Reconnaissance à l’aide de DNS|
|2008|Passage à une version antérieure du chiffrement|
|2009|Activité de passage à une version antérieure du chiffrement (golden ticket potentielle)|
|2010|Activité de passage à une version antérieure du chiffrement (Overpass-the-Hash potentielle)|
|2011|Activité de passage à une version antérieure du chiffrement (Skeleton Key potentielle)|
|2012|Reconnaissance à l’aide de l’énumération de sessions SMB|
|2013|Réaffectation de privilèges à l’aide de données d’autorisation falsifiées|
|2014|Activité Honeytoken|
|2016|Suppression massive d’objets|
|2017|Usurpation d’identité par attaque Pass-the-Hash|
|2018|Usurpation d’identité par attaque Pass-the-Ticket|
|2019|Tentative d’exécution à distance détectée|
|2020|Demande d’information privée de protection contre les données malveillantes|
|2021|Reconnaissance à l’aide de requêtes de services d’annuaire|
|2022|Activité de Golden Ticket Kerberos|
|2023|Échecs d’authentification suspects|
|2024|Modification anormale de groupes sensibles|
|2026|Création de service malveillant|

## <a name="ata-auditing-events"></a>Événements d’audit ATA

|ID de l’événement|Nom de l’alerte|
|---------|---------------|
|3001|Changement de configuration ATA|
|3002|Passerelle ATA ajoutée|
|3003|Passerelle ATA supprimée|
|3004|Licence ATA activée|
|3005|Connexion à la console ATA|
|3006|Changement manuel de l’état d’activité d’intégrité|
|3007|Changement manuel de l’état d’activité suspect|

## <a name="see-also"></a>Voir aussi
- [Configuration requise pour ATA](ata-prerequisites.md)
- [Planification de la capacité ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
