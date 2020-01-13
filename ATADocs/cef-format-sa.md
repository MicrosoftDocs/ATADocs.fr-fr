---
title: Informations de référence sur le journal SIEM ATA | Microsoft Docs
description: Fournit des exemples de journaux d’alertes de sécurité envoyés depuis ATA vers votre serveur SIEM.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: f11f304c4c157980711e5859cd0c391b2b5c93bf
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75907678"
---
# <a name="ata-siem-log-reference"></a>Informations de référence sur le journal SIEM ATA


*S’applique à : Advanced Threat Analytics version 1.9*

ATA peut transférer les événements d’alerte de sécurité et d’alerte de surveillance à votre serveur SIEM. Les alertes sont transférées au format CEF. Vous trouverez ci-dessous un exemple de chaque type de journal d’alertes de sécurité à envoyer à votre serveur SIEM.

## <a name="sample-ata-security-alerts-in-cef-format"></a>Exemples d’alertes de sécurité ATA au format CEF
Les champs suivants et leurs valeurs sont transférés à votre serveur SIEM :

-   start : heure de début de l’alerte
-   suser : compte (généralement le compte d’utilisateur) impliqué dans l’alerte
-   shost : machine source de l’alerte
-   résultat : alertes dont l’activité a réussi ou échoué  
-   msg : description de l’alerte
-   cnt : les alertes indiquant le nombre de fois où l’alerte s’est produite (par exemple une attaque par force brute a une certaine quantité de mots de passe devinés)
-   app : protocole de l’alerte
-   externalId : ID d’événement écrit par ATA dans le journal des événements correspondant à l’alerte*
-   cs#label et cs# : chaînes du client dont CEF autorise l’utilisation. cs#label est le nom du nouveau champ et cs# est sa valeur. Par exemple : cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

Dans cet exemple, cs1 est un champ qui a une URL vers l’alerte.

*Si vous créez des scripts ou une automatisation basée sur des journaux, utilisez la valeur externalID permanente de chaque journal au lieu des noms des journaux, car les noms de journaux peuvent être modifiés sans préavis. 

|Noms des alertes|ID des événements d’alerte|
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



## <a name="sample-logs"></a>Exemples de journaux

Priorités : 3=Faible 5=Moyenne 10=Élevée

### <a name="abnormal-modification-of-sensitive-groups"></a>Modification anormale de groupes sensibles
1 2018-12-12T16:53:22.925757+00:00 CENTER ATA 4688 AbnormalSensitiveGroupMembership CEF:0|Microsoft|ATA|1.9.0.0|AbnormalSensitiveGroupMembershipChangeSuspiciousActivity|Modification anormale de groupes sensibles|5|start=2018-12-12T18:52:58.0000000Z app=GroupMembershipChangeEvent suser=krbtgt msg=krbtgt contient des appartenances à des groupes sensibles qui ont été modifiées de façon inhabituelle. externalId=2024 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113d028ca1ec1250ca0491

### <a name="brute-force-attack-using-ldap-simple-bind"></a>Attaque par force brute par le biais d’une liaison simple LDAP
12-12-2018  19:52:18    Auth.Warning    192.168.0.222   1 2018-12-12T17:52:18.899690+00:00 CENTER ATA 4688 LdapBruteForceSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|LdapBruteForceSuspiciousActivity|Attaque par force brute par le biais d’une liaison simple LDAP|5|start=2018-12-12T17:52:10.2350665Z app=Ldap msg=10000 tentatives pour deviner des mots de passe ont été faites sur 100 comptes à partir de W2012R2-000000-Server. Un mot de passe de compte a été deviné avec succès. externalId=2004 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114acb8ca1ec1250cacdcb

### <a name="encryption-downgrade-activity-golden-ticket"></a>Activité de passage à une version antérieure du chiffrement (golden ticket)
12-12-2018  20:12:35    Auth.Warning    192.168.0.222   1 2018-12-12T18:12:35.105942+00:00 CENTER ATA 4688 EncryptionDowngradeSuspiciousAct ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|EncryptionDowngradeSuspiciousActivity|Activité de passage à une version antérieure du chiffrement|5|start=2018-12-12T18:10:35.0334169Z app=Kerberos msg=La méthode de chiffrement du champ TGT du message TGS_REQ de W2012R2-000000-Server a été passée à une version antérieure suivant un précédent comportement appris. Cela peut provenir d’un golden ticket utilisé sur W2012R2-000000-Server. externalId=2009 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114f938ca1ec1250cafcfa

### <a name="encryption-downgrade-activity-overpass-the-hash"></a>Activité de passage à une version antérieure du chiffrement (overpass-the-hash)
12-12-2018  19:00:31    Auth.Warning    192.168.0.222   1 2018-12-12T17:00:31.963485+00:00 CENTER ATA 4688 EncryptionDowngradeSuspiciousAct ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|EncryptionDowngradeSuspiciousActivity|Activité de passage à une version antérieure du chiffrement|5|start=2018-12-12T17:00:31.2975188Z app=Kerberos msg=La méthode de chiffrement du champ Encrypted_Timestamp du message AS_REQ de W2012R2-000000-Server a été passée à une version antérieure suivant un précédent comportement appris. Cela peut provenir d’un vol des informations d’identification de type overpass-the-hash depuis W2012R2-000000-Server. externalId=2010 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113eaf8ca1ec1250ca0883

###  <a name="encryption-downgrade-activity-skeleton-key"></a>Activité de passage à une version antérieure du chiffrement (Skeleton Key)
12-12-2018  20:07:24    Auth.Warning    192.168.0.222   1 2018-12-12T18:07:24.065140+00:00 CENTER ATA 4688 EncryptionDowngradeSuspiciousAct ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|EncryptionDowngradeSuspiciousActivity|Activité de passage à une version antérieure du chiffrement|5|start=2018-12-12T18:07:24.0222746Z app=Kerberos msg=La méthode de chiffrement du champ ETYPE_INFO2 du message KRB_ERR de W2012R2-000000-Server a été passée à une version antérieure suivant un précédent comportement appris. Cela peut provenir d’un Skeleton Key sur DC1. externalId=2011 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114e5c8ca1ec1250cafafe

### <a name="honeytoken-activity"></a>Activité Honeytoken
12-12-2018  19:51:52    Auth.Warning    192.168.0.222   1 2018-12-12T17:51:52.659618+00:00 CENTER ATA 4688 HoneytokenActivitySuspiciousActi ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|HoneytokenActivitySuspiciousActivity|Activité Honeytoken|5|start=2018-12-12T17:51:52.5855994Z app=Kerberos suser=USR78982 msg=Les activités suivantes ont été réalisées par USR78982 LAST78982:\r\nAuthentifié par CLIENT1 en utilisant NTLM pour accéder à domain1.test.local\cifs sur DC1. externalId=2014 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114ab88ca1ec1250ca7f76

### <a name="identity-theft-using-pass-the-hash-attack"></a>Usurpation d’identité par attaque Pass-the-Hash
12-12-2018  19:56:02    Auth.Error  192.168.0.222   1 2018-12-12T17:56:02.047236+00:00 CENTER ATA 4688 PassTheHashSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|PassTheHashSuspiciousActivity|Usurpation d’identité par attaque Pass-the-Hash|10|start=2018-12-12T17:54:01.9582400Z app=Ntlm suser=USR46829 LAST46829 msg=Le code de hachage USR46829 de LAST46829 a été volé de l’un des ordinateurs déjà connectés par USR46829 LAST46829 et utilisé à partir de W2012R2-000000-Server. externalId=2017 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114bb28ca1ec1250caf673

### <a name="identity-theft-using-pass-the-ticket-attack"></a>Usurpation d’identité par attaque Pass-the-Ticket
12-12-2018  22:03:51    Auth.Error  192.168.0.222   1 2018-12-12T20:03:51.643633+00:00 CENTER ATA 4688 PassTheTicketSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|PassTheTicketSuspiciousActivity|Usurpation d’identité par attaque Pass-the-Ticket|10|start=2018-12-12T17:54:12.9960662Z app=Kerberos suser=Birdie Lamb msg=Les tickets Kerberos de Birdie Lamb (ingénieur logiciel) ont été volés du serveur W2012R2-000106 au serveur W2012R2-000051 et utilisés pour accéder à domain1.test.local\host. externalId=2018 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b458ca1ec1250caf5b7

### <a name="kerberos-golden-ticket-activity"></a>Activité de Golden Ticket Kerberos
12-12-2018  19:53:26    Auth.Error  192.168.0.222   1 2018-12-12T17:53:26.869091+00:00 CENTER ATA 4688 GoldenTicketSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|GoldenTicketSuspiciousActivity|Activité de Golden Ticket Kerberos|10|start=2018-12-13T06:51:26.7290524Z app=Kerberos suser=Sonja Chadsey msg=Une utilisation suspecte du ticket Kerberos de Sonja Chadsey (ingénieur logiciel) a été détectée, indiquant une attaque Golden ticket potentielle. externalId=2022 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b168ca1ec1250caf556

### <a name="malicious-data-protection-private-information-request"></a>Demande d’information privée de protection contre les données malveillantes
12-12-2018  20:03:49    Auth.Error  192.168.0.222   1 2018-12-12T18:03:49.814620+00:00 CENTER ATA 4688 RetrieveDataProtectionBackupKeyS ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|RetrieveDataProtectionBackupKeySuspiciousActivity|Demande d’information privée de protection contre les données malveillantes|10|start=2018-12-12T17:58:56.3537533Z app=LsaRpc shost=W2012R2-000000-Server msg=Un utilisateur inconnu a effectué 1 tentative réussie partir de W2012R2-000000-Server pour récupérer la clé de sauvegarde de domaine DPAPI de DC1. externalId=2020 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114d858ca1ec1250caf983

### <a name="malicious-replication-of-directory-services"></a>Réplication malveillante de services d’annuaire
12-12-2018  19:56:49    Auth.Error  192.168.0.222   1 2018-12-12T17:56:49.312648+00:00 CENTER ATA 4688 DirectoryServicesReplicationSusp ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|DirectoryServicesReplicationSuspiciousActivity|Réplication malveillante de services d’annuaire|10|start=2018-12-12T17:52:34.3287329Z app=Drsr shost=W2012R2-000000-Server msg=Des demandes de réplication malveillantes ont été exécutées avec succès à partir de W2012R2-000000-Server dans DC1. outcome=Success externalId=2006 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114be18ca1ec1250caf6b8

### <a name="privilege-escalation-using-forged-authorization-data"></a>Réaffectation de privilèges à l’aide de données d’autorisation falsifiées
12-12-2018  19:51:15    Auth.Error  192.168.0.222   1 2018-12-12T17:51:15.658608+00:00 CENTER ATA 4688 ForgedPacSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|ForgedPacSuspiciousActivity|Réaffectation de privilèges à l’aide de données d’autorisation falsifiées|10|start=2018-12-12T17:51:15.0261128Z app=Kerberos suser=triservice msg=triservice a tenté une réaffectation de privilèges dans DC1 à partir de W2012R2-000000-Server en utilisant des données d’autorisation falsifiées. externalId=2013 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114a938ca1ec1250ca7f48

### <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance à l’aide de requêtes de services d’annuaire
12-12-2018  20:23:52    Auth.Warning    192.168.0.222   1 2018-12-12T18:23:52.155531+00:00 CENTER ATA 4688 SamrReconnaissanceSuspiciousActi ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|SamrReconnaissanceSuspiciousActivity|Reconnaissance à l’aide de requêtes de services d’annuaire|5|start=2018-12-12T18:04:12.9868815Z app=Samr shost=W2012R2-000000-Server msg=Les requêtes de services d'annuaire suivantes utilisant le protocole SAMR ont été tentées dans DC1 à partir de W2012R2-000000-Server:\r\r\nRequête réussie pour les générateurs d’approbation de forêt entrante (les membres de ce groupe peuvent créer des approbations entrantes à sens unique vers cette forêt) dans domain1.test.local externalId=2021 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114e758ca1ec1250cafb2e

### <a name="reconnaissance-using-account-enumeration"></a>Reconnaissance à l’aide de l’énumération de compte
1 2018-12-12T16:57:09.661680+00:00 CENTER ATA 4688 AccountEnumerationSuspiciousActi CEF:0|Microsoft|ATA|1.9.0.0|AccountEnumerationSuspiciousActivity|Reconnaissance à l’aide de l’énumération de compte|5|start=2018-12-12T16:57:09.1706828Z app=Kerberos shost=W2012R2-000000-Server msg=Une activité d’énumération de compte suspecte utilisant le protocole Kerberos et provenant de W2012R2-000000-Server a été détectée. La personne malveillante a fait 100 tentatives de deviner le mot de passe pour des noms de comptes, 1 tentative de deviner le mot de passe correspondait à des noms de compte existant dans Active Directory. externalId=2003 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113de58ca1ec1250ca06d8

### <a name="reconnaissance-using-dns"></a>Reconnaissance à l’aide de DNS
1 2018-12-12T16:57:20.743634+00:00 CENTER ATA 4688 DnsReconnaissanceSuspiciousActiv CEF:0|Microsoft|ATA|1.9.0.0|DnsReconnaissanceSuspiciousActivity|Reconnaissance à l’aide de DNS|5|start=2018-12-12T16:57:20.2556472Z app=Dns shost=W2012R2-000000-Server msg=Une activité DNS suspecte provenant de W2012R2-000000-Server (qui n’est pas un serveur DNS) a été observée dans DC1. externalId=2007 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113df08ca1ec1250ca074c

### <a name="reconnaissance-using-smb-session-enumeration"></a>Reconnaissance à l’aide de l’énumération de sessions SMB
12-12-2018  19:50:51    Auth.Warning    192.168.0.222   1 2018-12-12T17:50:51.090247+00:00 CENTER ATA 4688 EnumerateSessionsSuspiciousActiv ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|EnumerateSessionsSuspiciousActivity|Reconnaissance à l’aide de l’énumération de sessions SMB|5|start=2018-12-12T17:00:42.7234229Z app=SrvSvc shost=W2012R2-000000-Server msg=Les tentatives d'énumération de session SMB ont échoué depuis W2012R2-000000-Server avec DC1. Aucun compte n’a été exposé. externalId=2012 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114a788ca1ec1250ca7735

### <a name="remote-execution-attempt-detected"></a>Tentative d’exécution à distance détectée
12-12-2018  19:58:45    Auth.Warning    192.168.0.222   1 2018-12-12T17:58:45.082799+00:00 CENTER ATA 4688 RemoteExecutionSuspiciousActivit ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|RemoteExecutionSuspiciousActivity|Tentative d’exécution à distance détectée|5|start=2018-12-12T17:54:23.9523766Z shost=W2012R2-000000-Server msg=Les tentatives d'exécution à distance suivantes ont été effectuées sur DC1 à partir de W2012R2-000000-Server:\r\nLa planification à distance d'une ou plusieurs autres tâches a échoué. externalId=2019 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114c548ca1ec1250caf783

### <a name="unusual-protocol-implementation"></a>Implémentation de protocole inhabituelle
1 2018-12-12T16:50:46.930234+00:00 CENTER ATA 4688 AbnormalProtocolSuspiciousActivi CEF:0|Microsoft|ATA|1.9.0.0|AbnormalProtocolSuspiciousActivity|Implémentation de protocole inhabituelle|5|start=2018-12-12T16:48:46.6480337Z app=Ntlm shost=W2012R2-000000-Server outcome=Success msg=triservice a été authentifié avec succès à partir de W2012R2-000000-Server avec DC1 en utilisant une implémentation de protocole inhabituelle. Il s’agit peut-être de la conséquence de l’utilisation d’outils malveillants pour l’exécution d’attaques de type « Pass-the-Hash » et par force brute. externalId=2002 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113c668ca1ec1250ca0397

### <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Suspicion d’usurpation d’identité basée sur un comportement inhabituel
1 2018-12-12T16:50:35.746877+00:00 CENTER ATA 4688 AbnormalBehaviorSuspiciousActivi CEF:0|Microsoft|ATA|1.9.0.0|AbnormalBehaviorSuspiciousActivity|Suspicion d’usurpation d’identité basée sur un comportement inhabituel|5|start=2018-12-12T16:48:35.5501183Z app=Kerberos suser=USR45964 msg=USR45964 LAST45964 a affiché un comportement anormal lors de l'exécution d'activités qui n'ont pas été vues au cours du dernier mois et qui ne sont pas non plus conformes aux activités d’autres comptes dans l'organisation. Le comportement anormal est basé sur les activités suivantes :\r\nConnexion interactive effectuée à partir de 30 postes de travail anormaux.\r\nAccès demandé à 30 ressources anormales. externalId=2001 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113c5b8ca1ec1250ca0355

### <a name="suspicious-authentication-failures"></a>Échecs d’authentification suspects
12-12-2018  19:50:34    Auth.Warning    192.168.0.222   1 2018-12-12T17:04:25.214067+00:00 CENTER ATA 4688 BruteForceSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|BruteForceSuspiciousActivity|Échecs d’authentification suspects|5|start=2018-12-12T17:03:58.5892462Z app=Kerberos shost=W2012R2-000106-Server msg=Des échecs d'authentification suspects indiquant une attaque potentielle par force brute ont été détectés à partir de W2012R2-000106-Server. externalId=2023 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113f988ca1ec1250ca5810

### <a name="suspicious-service-creation"></a>Création de service malveillant
12-12-2018  19:53:49    Auth.Warning    192.168.0.222   1 2018-12-12T17:53:49.913034+00:00 CENTER ATA 4688 MaliciousServiceCreationSuspicio ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|MaliciousServiceCreationSuspiciousActivity|Création de service malveillant|5|start=2018-12-12T19:53:49.0000000Z app=ServiceInstalledEvent shost=W2012R2-000000-Server msg=triservice a créé FakeService afin d'exécuter des commandes potentiellement malveillantes sur W2012R2-000000-Server. externalId=2026 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b2d8ca1ec1250caf577

## <a name="monitoring-alerts"></a>Analyse des alertes

### <a name="gatewaydisconnectedmonitoringalert"></a>GatewayDisconnectedMonitoringAlert
1 2018-12-12T16:52:41.520759+00:00 CENTER ATA 4688 GatewayDisconnectedMonitoringAle CEF:0|Microsoft|ATA|1.9.0.0|GatewayDisconnectedMonitoringAlert|GatewayDisconnectedMonitoringAlert|5|externalId=1011 cs1Label=url cs1=https\://192.168.0.220/monitoring msg=Aucune communication depuis la passerelle CENTER depuis 5 minutes. Dernière communication établie le 12/12/2018 à 4:47:03 PM UTC.

### <a name="gatewaystartfailuremonitoringalert"></a>GatewayStartFailureMonitoringAlert
1 2018-12-12T15:36:59.701097+00:00 CENTER ATA 1372 GatewayStartFailureMonitoringAle CEF:0|Microsoft|ATA|1.9.0.0|GatewayStartFailureMonitoringAlert|GatewayStartFailureMonitoringAlert|5|externalId=1018 cs1Label=url cs1=https\://192.168.0.220/monitoring msg=Le service Gateway sur DC1 n’a pas démarré. Sa dernière exécution date du 12/12/2018 à 3:04:12 PM UTC.

> [!NOTE]
> Toutes les alertes de monitoring sont envoyées avec le même modèle que ci-dessus.


## <a name="see-also"></a>Voir aussi
- [Configuration requise pour ATA](ata-prerequisites.md)
- [Planification de la capacité d’ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
