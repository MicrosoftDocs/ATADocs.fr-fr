---
title: Informations de référence sur les ID d’événement ATA | Microsoft Docs
description: Fournit une liste des ID d’événement ATA et leurs descriptions.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 0c37024719a9037cb0522ba40115714a35a399b2
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166434"
---
*S’applique à : Advanced Threat Analytics version 1.9*


# <a name="ata-event-id-reference"></a>Informations de référence sur les ID d’événement ATA

L’Observateur d’événements du centre ATA journalise les événements pour ATA. Cet article fournit une liste d’ID d’événement et une description de chacun d’eux.

Vous trouverez les événements ici :

![emplacement des ID d’événement](./media/event-id-location.png)

## <a name="ata-health-events"></a>Événements d’intégrité ATA

1001 – Alerte d’intégrité sur l’espace disponible du lecteur de données de base de données du centre ATA 

1003 – Alerte d’intégrité sur la surcharge du centre ATA 

1004 – Alerte d’intégrité sur l’expiration des certificats 

1005 – Alerte d’intégrité sur la déconnexion de base de données du centre 

1006 – Alerte d’intégrité sur l’expiration de mots de passe de comptes client des services d’annuaire dans la passerelle ATA 

1007 – Alerte d’intégrité sur la non-affectation du synchronisateur de domaine dans la passerelle ATA 

1008 – Alerte d’intégrité sur l’échec de l’adaptateur de réseau de capture dans la passerelle ATA 

1009 – Alerte d’intégrité sur l’absence de l’adaptateur de réseau de capture dans la passerelle ATA 

1010 – Alerte d’intégrité sur la connectivité des clients des services d’annuaire dans la passerelle ATA 

1011 – Alerte d’intégrité sur la déconnexion de la passerelle ATA 

1012 – Alerte d’intégrité sur la surcharge des activités d’événement dans la passerelle ATA 

1013 – Alerte d’intégrité sur la surcharge des activités réseau dans la passerelle ATA 

1014 – Alerte d’intégrité sur la messagerie du centre 

1015 – Alerte d’intégrité sur le fichier Syslog du centre 

1016 – Alerte d’intégrité sur les passerelles ATA obsolètes 

1017 – Alerte d’intégrité sur la non-réception du trafic du centre 

1018 – Alerte d’intégrité sur l’échec de démarrage de la passerelle ATA 

1019 – Alerte d’intégrité sur la mémoire insuffisante de la passerelle ATA 

1020 – Alerte d’intégrité sur l’écouteur des événements RADIUS dans la passerelle ATA 

1021 – Alerte d’intégrité sur l’écouteur des événements Syslog dans la passerelle ATA 

1022 – Alerte d’intégrité sur l’échec de la résolution des adresses IP externes du centre ATA 
 
## <a name="ata-suspicious-activity-events"></a>Événements d’activités suspectes ATA

2001 – Activité suspecte de comportement anormal 

2002 – Activité suspecte de protocole anormal 

2003 – Activité suspecte d’énumération de comptes 

2004 – Activité suspecte d’attaque par force brute LDAP 

2006 – Activité suspecte de réplication des services d’annuaire 

2007 – Activité suspecte de reconnaissance DNS 

2008 – Activité suspecte de déclassement du chiffrement 

2012 – Activité suspecte d’énumération de sessions 

2013 – Activité suspecte de faux PAC 

2014 – Activité suspecte des activités Honeytoken 

2016 – Activité suspecte de suppression massive d’objets 

2017 – Activité suspecte de Pass the hash 

2018 – Activité suspecte de Pass the ticket 

2019 – Activité suspecte d’exécution à distance 

2020 – Activité suspecte de récupération de clé de sauvegarde de protection des données 

2021 – Activité suspecte de reconnaissance SAMR 

2022 – Activité suspecte de Golden ticket 

2023 – Activité suspecte d’attaque par force brute 

2024 – Activité suspecte de changement d’appartenance à un groupe sensible anormal  

## <a name="ata-auditing-events"></a>Événements d’audit ATA

3001 – Changement de configuration ATA 

3002 – Passerelle ATA ajoutée

3003 – Passerelle ATA supprimée

3004 - Licence ATA activée

3005 – Connexion à la console ATA

3006 – Changement manuel de l’état d’activité d’intégrité 

3007 – Changement manuel de l’état d’activité suspect 


## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Planification de la capacité d’ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
