---
title: Informations de référence sur le journal SIEM ATA | Microsoft Docs
description: Fournit des exemples de journaux d’activités suspectes envoyés depuis ATA vers votre serveur SIEM.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 7c6eaba8f80dcc7a8fc767f2bb8168221fbc7207
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009868"
---
*S’applique à : Advanced Threat Analytics version 1.9*


# <a name="ata-siem-log-reference"></a>Informations de référence sur le journal SIEM ATA

ATA peut transférer les événements d’activité suspecte et d’alerte de surveillance à votre serveur SIEM. Les événements d’activité suspecte sont au format CEF. Cet article de référence fournit des exemples des journaux d’activités suspectes envoyés à votre serveur SIEM.

## <a name="sample-ata-suspicious-activities-in-cef-format"></a>Exemples d’activités suspectes ATA au format CEF
Les champs suivants et leurs valeurs sont transférés à votre serveur SIEM :

-   start : heure de début de l’alerte
-   suser : compte (généralement le compte d’utilisateur) impliqué dans cette alerte
-   shost : machine source de cette alerte
-   outcome : pour les alertes indiquant la réussite ou l’échec de l’activité effectuée dans cette alerte  
-   msg : description de l’alerte
-   cnt : pour les alertes dont le nombre d’occurrences est compté (par exemple une attaque par force brute qui a une certaine quantité de mots de passe devinés)
-   app : protocole utilisé dans cette alerte
-   externalId : l’ID d’événement écrit par ATA dans le journal des événements correspondant à cette alerte
-   cs#label et cs# : il s’agit des chaînes du client dont CEF autorise l’utilisation. cs#label est le nom du nouveau champ et cs# est sa valeur. Par exemple : cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

Dans cet exemple, cs1 est un champ qui a une URL vers l’alerte.

## <a name="sample-logs"></a>Exemples de journaux

Priorités : 3=Faible 5=Moyenne 10=Élevée

### <a name="bruteforce--ldap"></a>BruteForce – LDAP
03-05-2017          13:35:01               Auth.Warning    192.168.0.220     3  mai 10:35:01 CENTER ATA:CEF:0|Microsoft|ATA|.5942.64854|BruteForceSuspiciousActivity|Attaque par force brute à l’aide d’une liaison simple LDAP|5|start=2017-05-03T10:34:57.2785534Z app=Ldap suser=Darris Woods shost=CLIENT1 msg=Une attaque en force brute utilisant le protocole LDAP a été tentée sur Darris Woods (Software Engineer) à partir de CLIENT1 (76 tentatives de deviner le mot de passe). cnt=76 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

03-05-2017          13:35:05               Auth.Warning    192.168.0.220     3  mai 10:35:01 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|Attaque par force brute à l’aide d’une liaison simple LDAP|5|start=2017-05-03T10:34:58.7004159Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=Une attaque en force brute utilisant le protocole LDAP a été tentée sur Dino Hopkins (Software Engineer) à partir de CLIENT1 (3 tentatives de deviner le mot de passe). cnt=3 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

03-05-2017          13:35:05               Auth.Warning    192.168.0.220     3  mai 10:35:01 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|Attaque par force brute à l’aide d’une liaison simple LDAP|5|start=22017-05-03T10:34:59.7269332Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=Une attaque en force brute réussie utilisant le protocole LDAP a été tentée sur Dino Hopkins (Software Engineer) à partir de CLIENT1 (77 tentatives de deviner le mot de passe). cnt=77 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70
### <a name="bruteforce"></a>BruteForce
14-05-2017          13:27:05               Auth.Warning    192.168.0.220     1 2017-05- ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|BruteForceSuspiciousActivity|Échecs d’authentification suspects|5|start=2017-05-14T10:27:04.3904739Z app=Kerberos shost=CLIENT1 msg=Nous avons détecté un échec d’authentification suspect indiquant une possible attaque par force brute à partir de CLIENT1. externalId=2023 cs1Label=url cs1=https://center/suspiciousActivity/591830f98ca1ec11d0c0d7f5
### <a name="privilege-escalation"></a>Élévation des privilèges
#### <a name="silver"></a>Silver
10-05-2017          17:14:15               Auth.Error           192.168.0.220     1 2017-05-10T14:14:15.589415+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Réaffectation de privilèges à l’aide de données d’autorisation falsifiées|10|start=2017-05-10T14:11:51.8053059Z app=Kerberos suser=user1 msg=user1 a tenté une réaffectation de privilèges dans HOST/client1 à partir de CLIENT2 en utilisant des données d’autorisation falsifiées. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/591320378ca1ec02543e4747
#### <a name="gold"></a>Gold
10-05-2017          17:13:30               Auth.Error           192.168.0.220     1 2017-05-10T14:13:30.244377+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Réaffectation de privilèges à l’aide de données d’autorisation falsifiées|10|start=2017-05-10T14:11:27.6455273Z app=Kerberos suser=user1 msg=user1 a tenté une réaffectation de privilèges sur DC4 à partir de CLIENT1 en utilisant des données d’autorisation falsifiées. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/5913200a8ca1ec02543e3ea8
### <a name="golden-ticket"></a>Golden Ticket
14-05-2017          15:57:10               Auth.Warning    192.168.0.220     1 2017-05-14T12:57:10.392730+00:00 CENTER ATA 4732 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Activité de chiffrement du passage à une version antérieure|5|start=2017-05-14T12:55:08.6913033Z app=Kerberos msg=La méthode de chiffrement du champ TGT du message TGS_REQ de CLIENT1 a été passée à une version antérieure suivant un précédent comportement appris. Cela peut provenir d’un golden ticket utilisé sur CLIENT1. externalId=2009 cs1Label=url cs1=https://center/suspiciousActivity/591854268ca1ec127ceec396
### <a name="honey-token-activity"></a>Activité de jeton honeytoken
11-05-2017          16:49:10               Auth.Warning    192.168.0.220     1 2017-05-11T13:49:10.725605+00:00 CENTER ATA 876 HoneytokenActivitySuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|HoneytokenActivitySuspiciousActivity|Honeytoken activity|5|start=2017-05-11T13:49:09.6455794Z app=Kerberos suser=privtriservice msg=Les activités suivantes ont été exécutées par privtriservice :\r\nAuthentifié depuis DC1 à l’aide de NTLM sur des ressources d’entreprise par le biais de DC1. externalId=2014 cs1Label=url cs1=https://center/suspiciousActivity/59146bd68ca1ec036ce57d29
### <a name="suspicious-replication-of-directory-services"></a>Réplication suspecte de services d’annuaire
3  mai 11:02:28 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DirectoryServicesReplicationSuspiciousActivity|Réplication malveillante de services d’annuaire|10|start=2017-05-03T11:00:13.6560919Z suser=user1 shost=CLIENT1 outcome=Échec msg=Une tentative d’envoi de demandes de réplication malveillantes a été réalisée par user1 depuis CLIENT1 sur DC1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b8c48ca1ec04d05ed28d
### <a name="malicious-data-protection-private-information-request"></a>Demande d’information privée de protection contre les données malveillantes
3  mai 13:39:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RetrieveDataProtectionBackupKeySuspiciousActivity|Demande d’information privée de protection contre les données malveillantes|10|start=2017-05-03T13:37:06.4039886Z app=LsaRpc shost=CLIENT1 suser= outcome=Réussite msg=Un utilisateur inconnu a effectué 4 tentatives réussies depuis CLIENT1 de récupérer la clé de sauvegarde du domaine DPAPI dans DC1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dd868ca1ec04d05fb01d
### <a name="massive-object-deletion"></a>Suppression massive d’objets
14-05-2017          14:38:34               Auth.Warning    192.168.0.220     1 2017-05-14T11:38:34.898810+00:00 CENTER ATA 3748 MassiveObjectDeletionSuspiciousA ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|MassiveObjectDeletionSuspiciousActivity|Suppression massive d’objets|5|start=2017-05-14T11:33:32.0000000Z msg=496 objets (9,75 % du total des objets AD) ont été supprimés dans un intervalle de [période de temps] à partir du domaine domain1.test.local. cnt=496 externalId=2016 cs1Label=url cs1=https://center/suspiciousActivity/591841ba8ca1ec0ea4ad587a
### <a name="over-pass-the-hash"></a>Over-pass-the-hash
14-05-2017          12:07:46               Auth.Warning    192.168.0.220     1 2017-05-14T09:07:46.652319+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Activité de chiffrement du passage à une version antérieure|5|start=2017-05-14T09:07:44.9933773Z app=Kerberos msg=La méthode de chiffrement du champ Encrypted_Timestamp du message TGS_REQ de AS_REQ a été passée à une version antérieure suivant un précédent comportement appris. Cela peut provenir d’un vol des informations d’identification de type overpass-the-hash depuis CLIENT1. externalId=2010 cs1Label=url cs1=https://center/suspiciousActivity/59181e628ca1ec045cdfa929
### <a name="pass-the-hash"></a>Pass-the-hash
10-05-2017          17:48:51               Auth.Error           192.168.0.220     1 2017-05-10T14:48:51.998620+00:00 CENTER ATA 596 PassTheHashSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|PassTheHashSuspiciousActivity|Usurpation d’identité par attaque de type « Pass-The-Hash »|10|start=2017-05-10T14:46:50.9463800Z app=Ntlm suser=user2 msg=Le code de hachage de user2 a été volé à l’un des ordinateurs déjà connectés par user2 et utilisé à partir de CLIENT1. externalId=2017 cs1Label=url cs1=https://center/suspiciousActivity/591328538ca1ec02543f9a1a
### <a name="account-enumeration"></a>Énumération de comptes
10-05-2017          16:44:22               Auth.Warning    192.168.0.220     1 2017-05-10T13:44:22.706381+00:00 CENTER ATA 596 AccountEnumerationSuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|AccountEnumerationSuspiciousActivity|Reconnaissance à l’aide de l’énumération de compte|5|start=2017-05-10T13:44:20.9930644Z app=Kerberos shost=CLIENT3 msg=Une activité d’énumération de compte suspecte utilisant le protocole Kerberos, provenant de CLIENT3 a été détectée. La personne malveillante a fait 72 tentatives de deviner le mot de passe pour des noms de comptes, 2 tentatives de deviner le mot de passe correspondaient à des noms de compte existant dans Active Directory. externalId=2003 cs1Label=url cs1=https://center/suspiciousActivity/591319368ca1ec02543c56ee
### <a name="dns-recon"></a>Reconnaissance DNS
03-05-2017          13:16:57               Auth.Warning    192.168.0.220     3  mai 10:16:57 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Reconnaissance DNS|5|start=2017-05-03T10:16:41.8297467Z app=Dns shost=CLIENT1 msg=Une activité DNS suspecte provenant de CLIENT1 (qui n’est pas un serveur DNS) a été observée contre DC1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa 03-05-2017          13:24:21               Auth.Warning    192.168.0.220     3  mai 10:24:21 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Reconnaissance DNS|5|start=2017-05-03T10:24:08.0950753Z app=Dns shost=CLIENT1 request=contoso.com requestMethod=Axfr reason=NameError outcome=Échec msg=Une activité DNS suspecte provenant de CLIENT1 (qui n’est pas un serveur DNS) a été observée. La requête était pour contoso.com (type Axfr). La réponse était NameError. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
### <a name="smb-session-enumeration"></a>Énumération des sessions SMB
3  mai 11:55:43 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|EnumerateSessionsSuspiciousActivity|Reconnaissance à l’aide de l’énumération de sessions SMB|5|start=2017-05-03T11:52:02.4360718Z app=SrvSvc shost=CLIENT1 msg=Tentatives d’énumération de sessions SMB exécutées avec succès depuis CLIENT1 sur DC1, exposition de user1 (daf::1). cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c53f8ca1ec04d05f1cf1
### <a name="samr-enumeration"></a>Énumération SAMR
3  mai 11:44:48 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|SamrReconnaissanceSuspiciousActivity|Reconnaissance à l’aide de requêtes de services d’annuaire|5|start=2017-05-03T11:42:46.5911225Z app=Samr shost=CLIENT1 suser=user1 outcome=Réussite msg=Les requêtes de services d’annuaires suivantes utilisant le protocole SAMR ont été tentées auprès de DC1 à partir de CLIENT1 :\r\nÉnumération correcte de tous les groupes dans domain1.test.local par user1 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c2b08ca1ec04d05f0e19
### <a name="remote-execution"></a>Exécution à distance
3  mai 12:36:47 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RemoteExecutionSuspiciousActivity|Tentative d’exécution à distance détectée|3|start=2017-05-03T12:34:32.3714348Z app=ServiceControl shost=CLIENT1 suser=Administrator outcome=Réussite msg=Les tentatives d’exécution distantes suivantes ont été exécutées sur DC1 depuis CLIENT1 :\r\nCréation distante de PSEXESVC par Administrator réalisée avec succès. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cedf8ca1ec04d05f5692
### <a name="skeleton-key"></a>Skeleton Key
14-05-2017          12:13:12               Auth.Warning    192.168.0.220     1 2017-05-14T09:13:12.102468+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Activité de chiffrement du passage à une version antérieure|5|start=2017-05-14T09:13:03.3509467Z app=Kerberos msg=La méthode de chiffrement du champ ETYPE_INFO2 du message KRB_ERR de CLIENT2 a été passée à une version antérieure suivant un précédent comportement appris. Cela peut provenir d’un Skeleton Key sur DC3. externalId=2011 cs1Label=url cs1=https://center/suspiciousActivity/59181fa88ca1ec045cdfe630
### <a name="unusual-protocol-implementation"></a>Implémentation de protocole inhabituelle
3  mai 12:28:19 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|AbnormalProtocolSuspiciousActivity|Mise en œuvre de protocole inhabituelle|5|start=2017-05-03T12:28:05.3561302Z app=Ntlm shost=CLIENT1 suser=Administrator outcome=Réussite msg=Tentative d’authentification de Administrator depuis CLIENT1 sur DC1 à l’aide d’une mise en œuvre de protocole inhabituelle réussie. Il s’agit peut-être de la conséquence de l’utilisation d’outils malveillants pour l’exécution d’attaques de type « Pass-the-Hash » et par force brute. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4
### <a name="pass-the-ticket"></a>Pass-the-Ticket
4  mai 13:15:41 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|PassTheTicketSuspiciousActivity|Usurpation d’identité par attaque pass-the-ticket|10|start=2017-05-04T13:13:44.5160000Z app=Kerberos shost=CLIENT1 suser=Administrator request=krbtgt/DOMAIN1.TEST.LOCAL msg=Les tickets Kerberos de Administrator ont été volés de CLIENT2 vers CLIENT1 et utilisés pour accéder à krbtgt/DOMAIN1.TEST.LOCAL. cs2Label=ticketSourceComputer cs2=CLIENT2 cs3Label=ticketSourceComputerIpAddress cs3= cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/590b29168ca1ec0ba438acf6

### <a name="monitoring-alert"></a>Alerte de monitoring
30-01-2018T10:42:09.102595+00:00 CENTER ATA 4932 CenterDatabaseDisconnectedMonito ï»¿CEF:0|Microsoft|ATA|1.8.6765.50002|CenterDatabaseDisconnectedMonitoringAlert|CenterDatabaseDisconnectedMonitoringAlert|10|externalId=1005 cs1Label=url cs1=https://center/monitoring msg=La base de données qui est utilisée par le Centre, CENTER, est en panne. La dernière fois qu’elle a été vue fonctionner remonte au 30/01/2018 10:39:39 : 00 UTC.

> [!NOTE]
> Toutes les alertes de monitoring sont envoyées avec le même modèle que ci-dessus.



## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Planification de la capacité d’ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
