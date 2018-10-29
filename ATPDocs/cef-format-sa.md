---
title: Informations de référence sur le journal SIEM Azure ATP | Microsoft Docs
description: Fournit des exemples de journaux d’activités suspectes envoyés depuis Azure ATP vers votre serveur SIEM.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 754b0860e050cca7bd455e948bda911950012dab
ms.sourcegitcommit: c4978be196e0039c7a5d5887bec4cbc5c01d64f9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/07/2018
ms.locfileid: "48848662"
---
*S’applique à : Azure - Protection avancée contre les menaces*


# <a name="azure-atp-siem-log-reference"></a>Informations de référence sur le journal SIEM Azure ATP

Azure ATP peut transférer les événements d’activité suspecte et d’alerte de surveillance à votre serveur SIEM. Les événements d’activité suspecte sont au format CEF. Cet article de référence fournit des exemples des journaux d’activités suspectes envoyés à votre serveur SIEM.

## <a name="sample-azure-atp-suspicious-activities-in-cef-format"></a>Exemples d’activités suspectes Azure ATP au format CEF
Les champs suivants et leurs valeurs sont transférés à votre serveur SIEM :

-   start : heure de début de l’alerte
-   suser : compte (généralement le compte d’utilisateur) impliqué dans cette alerte
-   shost : machine source de cette alerte
-   outcome : pour les alertes indiquant la réussite ou l’échec de l’activité effectuée dans cette alerte  
-   msg : description de l’alerte
-   cnt : pour les alertes dont le nombre d’occurrences est compté (par exemple une attaque par force brute qui a une certaine quantité de mots de passe devinés)
-   app : protocole utilisé dans cette alerte
-   externalId : ID d’événement écrit par Azure ATP dans le journal des événements correspondant à cette alerte
-   cs#label et cs# : il s’agit des chaînes du client dont CEF autorise l’utilisation. cs#label est le nom du nouveau champ et cs# est sa valeur. Par exemple : cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

Dans cet exemple, cs1 est un champ qui a une URL vers l’alerte.

## <a name="sample-logs"></a>Exemples de journaux

Les exemples de journaux suivants sont conformes au document RFC 5242, mais Azure ATP prend également en charge le document RFC 3164.

Priorités :

- 3=Faible
- 5=Moyenne
- 10=Élevée

### <a name="bruteforce--ldap"></a>BruteForce – LDAP
21-02-2018  16:20:21    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:06.156238+00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|LdapBruteForceSecurityAlert|Attaque par force brute à l’aide d’une liaison simple LDAP|5|start=2018-02-21T14:19:41.7422810Z app=Ldap suser=Wofford Thurston shost=CLIENT1 msg=Une attaque en force brute utilisant le protocole Ldap a été tentée sur Wofford Thurston (Software Engineer) à partir de CLIENT1 (100 tentatives de deviner le mot de passe). cnt=100 externalId=2004 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a


### <a name="bruteforce"></a>BruteForce
21-02-2018  16:19:20    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:15.397995+00:00 CENTER CEF 6076 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|BruteForceSecurityAlert|Échecs d’authentification suspects|5|start=2018-02-21T14:19:03.3831122Z app=Kerberos shost=CLIENT1 msg=Nous avons détecté un échec d’authentification suspect indiquant une possible attaque par force brute à partir de CLIENT1. externalId=2023 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6
### <a name="privilege-escalation"></a>Élévation des privilèges
#### <a name="silver"></a>Silver
21-02-2018  16:19:20    Auth.Error  192.168.0.220   1 2018-02-21T14:19:15.186167+00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|ForgedPacSecurityAlert|Réaffectation de privilèges à l’aide de données d’autorisation falsifiées|10|start=2018-02-21T14:19:02.8595383Z app=Kerberos suser=user1 msg=user1 a tenté une réaffectation de privilèges dans host/domain1.test.local à partir de CLIENT1 en utilisant des données d’autorisation falsifiées. externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/029189e1-6bb4-490b-bcaf-5fac4457e9f3
#### <a name="gold"></a>Gold
21-02-2018  16:19:20    Auth.Error  192.168.0.220   1 2018-02-21T14:19:14.358037+00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|ForgedPacSecurityAlert|Réaffectation de privilèges à l’aide de données d’autorisation falsifiées|10|start=2018-02-21T14:19:02.8595383Z app=Kerberos suser=user1 msg=La tentative d’user1 de réaffecter des privilèges sur DC1 dans host/domain1.test.local à partir de CLIENT1 en utilisant des données d’autorisation falsifiées a échoué. externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f3359eff-cb59-44b9-82b6-5e82ff06e6c8
### <a name="golden-ticket"></a>Golden Ticket
21-02-2018  16:22:39    Auth.Error  192.168.0.220   1 2018-02-21T14:22:34.274054+00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|GoldenTicketSecurityAlert|Activité de Golden Ticket Kerberos|10|start=2018-02-21T14:19:03.2416152Z app=Kerberos suser=Lanell Campos msg=Nous avons détecté une utilisation suspecte du ticket Kerberos de Lanell Campos (Software Engineer), ce qui peut indiquer une attaque par Golden Ticket. externalId=2022 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0
### <a name="kerberos-golden-ticket-nonexistent-account"></a>Golden Ticket Kerberos - compte non existant
07-01-2018  14:28:49    Auth.Error  192.168.0.100   1 2018-07-01T11:28:35.546638+00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|ForgedPrincipalSecurityAlert|Golden Ticket Kerberos - compte inexistant|10|start=2018-07-01T09:48:31.2567987Z app=Kerberos suser=domain1.test.local\fake msg=domain1.test.local\faux, qui n’existe pas dans Active Directory, a utilisé un ticket Kerberos. Le ticket a été détecté sur 2 ordinateurs pour accéder à 3 ressources. Cela peut indiquer une attaque potentielle de Golden Ticket. externalId=2027 cs1Label=url cs1=https://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4


### <a name="honey-token-activity"></a>Activité de jeton honeytoken
02-21-2018  16:20:36    Auth.Warning  192.168.0.220 1 2018-02-21T14:20:34.106162+00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|HoneytokenActivitySecurityAlert|Honeytoken activity|5|start=2018-02-21T14:20:26.6705617Z app=Kerberos suser=honey msg=Les activités suivantes ont été exécutées par honey :\r\nConnecté à CLIENT2 par le biais de DC1. externalId=2014 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c
### <a name="suspicious-replication-of-directory-services"></a>Réplication suspecte de services d’annuaire
21-02-2018  16:21:22    Auth.Error  192.168.0.220   1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|Réplication malveillante de services d’annuaires|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=Des demandes de réplication malveillante ont été réalisées avec succès par user1 depuis CLIENT1 sur DC1. outcome=Success externalId=2006 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7
### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Demande de réplication suspecte (attaque potentielle DcShadow)
07-12-2018  11:18:37    Auth.Error  192.168.0.200    1 2018-07-12T08:18:32.265989+00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRogueReplicationSecurityAlert| **Demande de réplication suspecte (attaque DCShadow potentielle)**|10|start=2018-07-12T08:17:55.3816102Z **app=Replication Activity** shost=CLIENT1 msg=CLIENT1, qui n'est pas un contrôleur de domaine valide dans domain1.test.local, a envoyé des changements aux objets annuaire sur DC1. externalId=2029 cs1Label=url cs1=https://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515
### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Promotion du contrôleur de domaine suspect (attaque potentielle DcShadow)
07-12-2018  11:18:07    Auth.Error  192.168.0.200    1 2018-07-12T08:18:06.883880+00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRoguePromotionSecurityAlert| **Promotion du contrôleur de domaine suspect (attaque DCShadow potentielle)**|10|start=2018-07-12T08:17:55.4067092Z app=Ldap shost=CLIENT1 msg=CLIENT1, qui n’est pas un ordinateur dans domain1.test.local, a été enregistré comme contrôleur de domaine sur DC1. externalId=2028 cs1Label=url cs1=https://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53

### <a name="malicious-data-protection-private-information-request"></a>Demande d’information privée de protection contre les données malveillantes
21-02-2018  16:22:08    Auth.Error  192.168.0.220   1 2018-02-21T14:21:54.080266+00:00 CENTER CEF 6076 RetrieveDataProtectionBackupKeyS ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|RetrieveDataProtectionBackupKeySecurityAlert|Demande d’information privée de protection contre les données malveillantes|10|start=2018-02-21T14:19:41.8382786Z app=LsaRpc shost=CLIENT1 msg=user1 a effectué 1 tentatives réussies depuis CLIENT1 de récupérer la clé de sauvegarde du domaine DPAPI dans DC1. externalId=2020 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/b22221d1-764a-4fae-a5ce-e6a0c69dc55a

### <a name="over-pass-the-hash"></a>Over-pass-the-hash
21-02-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Activité de passage à une version antérieure du chiffrement|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg= La méthode de chiffrement du champ Encrypted_Timestamp du message AS_REQ de CLIENT1 a été passée à une version antérieure suivant un précédent comportement appris. Cela peut provenir d’un vol des informations d’identification de type overpass-the-hash depuis CLIENT1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2
### <a name="pass-the-hash"></a>Pass-the-hash
21-02-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|Usurpation d’identité par attaque de type « Pass-The-Hash »|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Le code de hachage de Eugene Jenkins (Software Engineer) a été volé à l’un des ordinateurs déjà connectés par Eugene Jenkins (Software Engineer) et utilisé à partir de CLIENT1. externalId=2017 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd
### <a name="account-enumeration"></a>Énumération de comptes
21-02-2018  16:19:35    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:27.540731+00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AccountEnumerationSecurityAlert|Reconnaissance à l’aide de l’énumération de compte|5|start=2018-02-21T14:19:02.6045416Z app=Kerberos shost=CLIENT1 suser=LMaldonado msg=Une activité d’énumération de compte suspecte utilisant le protocole Kerberos, provenant de CLIENT1, a été observée et a deviné avec succès Lamon Maldonado (Software Engineer). externalId=2003 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d
### <a name="dns-recon"></a>Reconnaissance DNS
21-02-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.063994+00:00 CENTER CEF 6076 DnsReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DnsReconnaissanceSecurityAlert|Reconnaissance DNS|5|start=2018-02-21T14:19:41.9417776Z app=Dns shost=CLIENT1 request=demo query requestMethod=Axfr reason=NoError outcome=Success msg=Une activité DNS suspecte provenant de CLIENT1 (qui n’est pas un serveur DNS) a été observée. La requête était pour la requête de démonstration (type Axfr). La réponse était NoError. externalId=2007 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c


### <a name="smb-session-enumeration"></a>Énumération des sessions SMB
21-02-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.962930+00:00 CENTER CEF 6076 EnumerateSessionsSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EnumerateSessionsSecurityAlert|Reconnaissance à l’aide de l’énumération de sessions SMB|5|start=2018-02-21T14:19:03.2071170Z app=SrvSvc shost=CLIENT1 msg=Tentatives d’énumération de sessions SMB exécutées avec succès par user1, depuis CLIENT1 sur DC1, exposition de Eugene Jenkins (user2-computer). externalId=2012 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440
### <a name="sam-r-enumeration"></a>Énumération SAM-R
21-02-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|SamrReconnaissanceSecurityAlert| Reconnaissance à l’aide de l’énumération des services d’annuaires|5|start=2018-02-21T14:19:41.9912772Z app= Samr shost=CLIENT1 suser=user1 outcome=Success msg= Les énumérations des services d’annuaires suivantes à l’aide du protocole SAMR ont été tentées auprès de DC1 à partir de CLIENT1 :\r\nÉnumération correcte de tous les groupes dans domain1.test.local par user1. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="remote-execution"></a>Exécution à distance
21-02-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 RemoteExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|RemoteExecutionSecurityAlert|Tentative d’exécution à distance détectée|5|start=2018-02-21T14:19:41.9912772Z app=Wmi shost=CLIENT1 suser=user1 outcome=Success msg=Les tentatives d’exécution à distance suivantes ont été exécutées sur DC1 depuis CLIENT1 :\r\nL’exécution à distance d’une ou de plusieurs méthodes WMI par user1 est réussie. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="skeleton-key"></a>Skeleton Key
21-02-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Activité de passage à une version antérieure du chiffrement|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=La méthode de chiffrement du champ ETYPE_INFO2 du message KRB_ERR de CLIENT1 a été passée à une version antérieure suivant un précédent comportement appris. Cela peut provenir d’un Skeleton Key sur DC1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2

### <a name="unusual-protocol-implementation"></a>Implémentation de protocole inhabituelle
21-02-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|Implémentation de protocole inhabituelle|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=Des tentatives d’authentification ont été effectuées depuis CLIENT2 sur DC1 à l’aide d’une implémentation de protocole inhabituelle. Il s’agit peut-être de la conséquence de l’utilisation d’outils malveillants pour l’exécution d’attaques de type « Pass-the-Hash » et par force brute. externalId=2002 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4

### <a name="malicious-service-creation"></a>Création de service malveillant
21-02-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.254930+00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|MaliciousServiceCreationSecurityAlert|Création de service suspect|5|start=2018-02-21T14:19:41.7897808Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 a créé MaliciousService pour exécuter des commandes potentiellement dangereuses sur CLIENT1. externalId=2026 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c

### <a name="pass-the-ticket"></a>Pass-the-Ticket
21-02-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheTicketSecurityAlert|Usurpation d’identité par attaque pass-the-ticket|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Les tickets Kerberos d’Eugene Jenkins (Software Engineer) ont été volés d’Admin-PC vers Victim-PC et utilisés pour accéder à krbtgt/DOMAIN1.TEST.LOCAL. externalId=2017 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd

### <a name="suspicious-communication-over-dns--preview"></a>Communication suspecte sur DNS - préversion
10-04-2018  14:49:38    Auth.Warning    192.168.0.202   1 2018-10-04T11:49:25.954059+00:00 DC3 CEF 3604 DnsSuspiciousCommunicationSecuri ï»¿0|Microsoft|Azure ATP|2.49.5589.58606|DnsSuspiciousCommunicationSecurityAlert|[PRÉVERSION] Communication suspecte sur DNS|5|start=2018-10-04T11:49:11.0822077Z app=DnsEvent dhost= suspiciousdomainname msg=CLIENT1 a envoyé des requêtes DNS suspectes résolvant suspiciousdomainname externalId=2031 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/0fc77777-49ca-40b3-a7ba-7644f355539e 

### <a name="suspicious-vpn-connection"></a>Connexion VPN suspecte
07-03-2018  13:13:12    Auth.Warning  192.168.0.200   1 2018-07-03T10:13:06.187834+00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|AbnormalVpnSecurityAlert|Connexion VPN suspecte|5|start=2018-06-30T15:34:05.3887333Z app=VpnConnection suser=user1 msg=user1 connecté à un VPN avec trois ordinateurs à trois endroits.     externalId=2025 cs1Label=url cs1=https://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68


## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)