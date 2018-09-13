---
title: Présentation des alertes de surveillance d’ATA | Microsoft Docs
description: Décrit comment utiliser les journaux ATA pour résoudre des problèmes
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: b04fb8a4-b366-4b55-9d4c-6f054fa58a90
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: dbe8f6d918086c028f5cd20bf60d0e5a24df0ad5
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166335"
---
*S’applique à : Advanced Threat Analytics version 1.9*


# <a name="understanding-ata-monitoring-alerts"></a>Présentation des alertes de surveillance d’ATA
Le centre d’intégrité ATA vous permet de savoir s’il existe un problème avec le déploiement d’ATA en déclenchant une alerte de surveillance.
Cet article décrit toutes les alertes de surveillance pour chaque composant, en indiquant la cause et les étapes nécessaires pour résoudre le problème.
## <a name="ata-center-issues"></a>Problèmes du centre ATA
### <a name="center-running-out-of-disk-space"></a>Espace disque du centre insuffisant
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|L’espace libre sur le lecteur de l’ordinateur du centre ATA qui est utilisé pour stocker la base de données ATA est insuffisant.|Cela signifie que le disque dur dispose de moins de 200 Go d’espace libre ou qu’il y a moins de 20 % d’espace libre, selon celui des deux qui est le plus petit. Quand ATA reconnaît que le lecteur manque d’espace, il commence à supprimer les anciennes données de la base de données. S’il ne peut pas supprimer les anciennes données parce qu’il en a encore besoin pour le moteur de détection, vous recevez cette alerte. Quand vous recevez cette alerte, ATA arrête le suivi des nouvelles activités.|Augmentez la taille du disque ou libérez de l’espace sur ce lecteur.|Importante|
### <a name="failure-sending-mail"></a>Échec de l’envoi des e-mails
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|ATA n’arrive pas à envoyer une notification par e-mail au serveur de messagerie spécifié.|Aucun e-mail n'est envoyé depuis ATA.|Vérifiez la configuration du serveur SMTP.|Faible|

### <a name="center-overloaded"></a>Centre surchargé
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le centre ATA n’est pas en mesure de gérer la quantité de données transférées depuis les passerelles ATA. |Le centre ATA cesse l’analyse du nouveau trafic réseau et des événements. Cela signifie que la précision des détections et des profils est réduite pendant que cette alerte de surveillance est active.|Vérifiez que vous avez fourni suffisamment de ressources pour le centre ATA. Pour plus de détails sur la façon de planifier correctement la capacité du centre ATA, consultez [Planification de la capacité ATA](ata-capacity-planning.md). Analysez les performances du centre ATA en utilisant [Résolution des problèmes liés à ATA à l’aide des compteurs de performances](troubleshooting-ata-using-perf-counters.md).|Importante|

### <a name="failure-connecting-to-the-siem-server-using-syslog"></a>Échec de la connexion au serveur SIEM à l’aide de Syslog
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|ATA n’arrive pas à envoyer des événements au serveur SIEM spécifié.|Cela signifie que le centre ATA ne peut pas envoyer des activités suspectes et des alertes de surveillance à votre serveur SIEM.|Vérifiez que les [paramètres de votre serveur Syslog sont configurés correctement](setting-syslog-email-server-settings.md).|Faible|
### <a name="center-certificate-is-about-to-expire"></a>Le certificat du centre est sur le point d’expirer
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le certificat du centre ATA expire dans moins de 3 semaines.|Après l’expiration du certificat : la connectivité des passerelles ATA avec le centre ATA échoue. Le processus du centre ATA se bloque et toutes les fonctionnalités d’ATA sont arrêtées.|[Remplacez le certificat du centre ATA](modifying-ata-center-configuration.md)|Moyenne|
### <a name="ata-center-certificate-expired"></a>Le certificat du centre ATA a expiré
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le certificat du centre ATA a expiré.|Après l’expiration du certificat : la connectivité des passerelles ATA avec le centre ATA échoue. Le processus du centre ATA se bloque et toutes les fonctionnalités d’ATA sont arrêtées.|[Remplacez le certificat du centre ATA](modifying-ata-center-configuration.md)|Importante|
## <a name="ata-gateway-issues"></a>Problèmes de la passerelle ATA
### <a name="read-only-user-password-to-expire-shortly"></a>Le mot de passe de l’utilisateur en lecture seule est sur le point d’expirer
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le mot de passe de l’utilisateur en lecture seule, utilisé pour effectuer la résolution des entités sur Active Directory, expire dans moins de 30 jours.|Si le mot de passe pour cet utilisateur expire, toutes les passerelles ATA cessent de fonctionner et aucune nouvelle donnée n’est collectée.|[Changez le mot de passe de connectivité du domaine](modifying-ata-config-dcpassword.md), puis mettez à jour le mot de passe dans la console ATA.|Moyenne|
### <a name="read-only-user-password-expired"></a>Le mot de passe de l’utilisateur en lecture seule a expiré
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le mot de passe de l’utilisateur en lecture seule, utilisé pour d’obtenir des données de l’annuaire, a expiré.|Toutes les passerelles ATA cessent de fonctionner (ou le feront sous peu) et aucune nouvelle donnée n’est collectée.|[Changez le mot de passe de connectivité du domaine](modifying-ata-config-dcpassword.md), puis mettez à jour le mot de passe dans la console ATA.|Importante|
### <a name="gateway-certificate-about-to-expire"></a>Le certificat de la passerelle est sur le point d’expirer
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le certificat de la passerelle ATA expire dans moins de 3 semaines.|La connectivité de la passerelle ATA concernée avec le centre ATA échoue. Aucune donnée provenant de cette passerelle ATA n'est envoyée.|Le certificat de la passerelle ATA devrait normalement avoir été renouvelé automatiquement. Lisez les journaux de la passerelle ATA et du centre ATA pour comprendre pourquoi ce certificat n’a pas été renouvelé automatiquement.|Moyenne|

### <a name="gateway-certificate-expired"></a>Le certificat de la passerelle a expiré
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le certificat de la passerelle ATA a expiré.|Il n’existe pas de connectivité de cette passerelle ATA avec le centre ATA. Aucune donnée provenant de cette passerelle ATA n'est envoyée.|[Désinstallez et réinstallez la passerelle ATA](install-ata-step3.md).|Importante|
### <a name="domain-synchronizer-not-assigned"></a>Synchronisateur de domaine non affecté
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Aucun synchronisateur de domaine n’est affecté aux passerelles ATA. Ce cas peut se produire si aucune passerelle ATA n’est configurée en tant que candidat synchronisateur de domaine.|Quand le domaine n’est pas synchronisé, les modifications apportées aux entités peuvent entraîner l’obsolescence ou l’absence des informations des entités dans ATA, mais elles n’impactent pas la détection.|Vérifiez qu’au moins une passerelle ATA est définie comme [synchronisateur de domaine](install-ata-step5.md).|Faible|
### <a name="allsome-of-the-capture-network-adapters-on-a-gateway-are-not-available"></a>Tout ou partie des cartes réseau de capture sur une passerelle ne sont pas disponibles
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Tout ou partie des cartes réseau de capture sélectionnées sur la passerelle ATA sont désactivées ou déconnectées.|Le trafic réseau pour tout ou partie des contrôleurs de domaine n’est plus capturé par la passerelle ATA. Ceci a un impact sur la possibilité de détecter les activités suspectes liées à ces contrôleurs de domaine.|Vérifiez que ces cartes réseau de capture sélectionnées sur la passerelle ATA sont activées et connectées.|Moyenne|
### <a name="some-domain-controllers-are-unreachable-by-a-gateway"></a>Certains contrôleurs de domaine ne sont pas accessibles par une passerelle
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Une passerelle ATA a des fonctionnalités limitées en raison de problèmes de connectivité avec certains des contrôleurs de domaine configurés.|La détection de pass-the-hash peut être moins précise quand certains contrôleurs de domaine ne peuvent pas être interrogés par la passerelle ATA.|Vérifiez que les contrôleurs de domaine sont fonctionnels et que cette passerelle ATA peut les utiliser pour ouvrir des connexions LDAP.|Moyenne|
### <a name="all-domain-controllers-are-unreachable-by-a-gateway"></a>Tous les contrôleurs de domaine ne sont pas accessibles par une passerelle
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|La passerelle ATA est actuellement hors connexion en raison de problèmes de connectivité avec tous les contrôleurs de domaine configurés.|Ceci a un impact sur la capacité d’ATA à détecter les activités suspectes liées à des contrôleurs de domaine surveillés par cette passerelle ATA.| Vérifiez que les contrôleurs de domaine sont fonctionnels et que cette passerelle ATA peut les utiliser pour ouvrir des connexions LDAP.|Moyenne|
### <a name="gateway-stopped-communicating"></a>La passerelle a cessé de communiquer
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Aucune communication n’a été reçue de la passerelle ATA. L’intervalle de temps par défaut pour cette alerte est de 5 minutes.|Le trafic réseau n’est plus capturé par la carte réseau sur la passerelle ATA. Ceci a un impact sur la capacité d’ATA à détecter les activités suspectes, car le trafic réseau ne pourra pas atteindre le centre ATA.|Vérifiez que le port utilisé pour la communication entre la passerelle ATA et le service du centre ATA n’est pas bloqué par un routeur ou un pare-feu.|Moyenne|
### <a name="no-traffic-received-from-domain-controller"></a>Aucun trafic reçu du contrôleur de domaine
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Aucun trafic n’a été reçu du contrôleur de domaine via cette passerelle ATA.|Ceci peut indiquer que la mise en miroir de ports des contrôleurs de domaine vers la passerelle ATA n’est pas encore configurée ou ne fonctionne pas.|Vérifiez que la [mise en miroir de ports est configurée correctement sur vos appareils réseau](configure-port-mirroring.md).<br></br>Sur la carte réseau de capture de la passerelle ATA, désactivez ces fonctionnalités dans Paramètres avancés :<br></br>RSC (Receive Segment Coalescing) (IPv4)<br></br>RSC (Receive Segment Coalescing) (IPv6)|Moyenne|
### <a name="some-forwarded-events-are-not-being-analyzed"></a>Certains événements transférés ne sont pas analysés
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|La passerelle ATA reçoit plus d’événements que ce qu’elle peut traiter.|Certains événements transférés ne sont pas analysés, ce qui peut impacter la capacité à détecter les activités suspectes provenant des contrôleurs de domaine surveillés par cette passerelle ATA.|Vérifiez que seuls les événements nécessaires sont transférés vers la passerelle ATA ou essayez de transférer certains des événements vers une autre passerelle ATA.|Moyenne|
### <a name="some-network-traffic-is-not-being-analyzed"></a>Une partie du trafic réseau n’est pas analysé
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|La passerelle ATA reçoit plus de trafic réseau que ce qu’elle peut traiter.|Une partie du trafic réseau n’est pas analysée, ce qui peut impacter la capacité à détecter les activités suspectes provenant des contrôleurs de domaine surveillés par cette passerelle ATA.|Envisagez [d’ajouter des processeurs et de la mémoire](ata-capacity-planning.md) selon les besoins. S’il s’agit d’une passerelle ATA autonome, réduisez le nombre de contrôleurs de domaine analysés.<br></br>Cela peut également se produire si vous utilisez des contrôleurs de domaine sur des machines virtuelles VMware. Pour éviter ces alertes, vous pouvez vérifier que les paramètres suivants sont définis sur 0 ou sont désactivés dans la machine virtuelle :<br></br>- TsoEnable<br></br>- LargeSendOffload(IPv4)<br></br>- IPv4 TSO Offload<br></br>Pensez aussi à désactiver IPv4 Giant TSO Offload. Pour plus d’informations, voir la documentation de VMware.|Moyenne|

### <a name="gateway-version-outdated"></a>Version de la passerelle obsolète
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le centre ATA est plus récent que la version installée sur la passerelle ATA. Conséquence : la passerelle ATA cesse de fonctionner comme prévu.|Ceci peut impacter la capacité à détecter les activités suspectes provenant des contrôleurs de domaine surveillés par cette passerelle ATA.|Mettez à jour automatiquement la passerelle ATA avec la dernière version en activant la [mise à jour automatique](install-ata-step1.md) dans la console ATA ou en téléchargeant le dernier package de la passerelle ATA disponible dans la console ATA.|Importante|
### <a name="gateway-service-failed-to-start"></a>Échec du démarrage du service de passerelle
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le démarrage du service de passerelle ATA échoue pendant au moins 30 minutes.|Ceci peut impacter la capacité à détecter les activités suspectes provenant des contrôleurs de domaine surveillés par cette passerelle ATA.|Surveillez les journaux de la passerelle ATA pour [comprendre la cause principale de l’échec du service de passerelle ATA](troubleshooting-ata-using-logs.md).|Importante|
## <a name="lightweight-gateway"></a>Passerelle légère
### <a name="lightweight--gateway-reached-a-memory-resource-limit"></a>La passerelle légère a atteint la limite des ressources mémoire
|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|La passerelle légère ATA s’est arrêtée elle-même et redémarrera automatiquement pour éviter que le contrôleur de domaine soit face à une mémoire insuffisante.|La passerelle légère ATA s’applique à elle-même des limitations de mémoire pour éviter que le contrôleur de domaine connaisse des limitations de ressources. Ce cas de figure se produit quand l’utilisation de la mémoire sur le contrôleur de domaine est élevée. Les données provenant de ce contrôleur de domaine ne sont que partiellement suivies.|Augmentez la quantité de mémoire (RAM) sur le contrôleur de domaine ou ajoutez des contrôleurs de domaine dans ce site afin de mieux répartir la charge de ce contrôleur de domaine.|Moyenne|


## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Planification de la capacité d’ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
