---
title: Informations de référence sur le journal SIEM Azure ATP | Microsoft Docs
description: Fournit des exemples de journaux d’activités suspectes envoyés depuis Azure ATP vers votre serveur SIEM.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/26/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: fcad0fd1677a6e34a9d72b0e9660eb2e680ca22e
ms.sourcegitcommit: e2a89030c31376c6798697a62b484f45ed54e679
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52501141"
---
*S’applique à : Azure Advanced Threat Protection*


# <a name="azure-atp-siem-log-reference"></a>Informations de référence sur le journal SIEM Azure ATP

Azure ATP peut transférer les événements d’alerte de sécurité et d’alerte de surveillance à votre serveur SIEM. Les alertes et les événements sont au format CEF. Cet article de référence fournit des exemples des journaux envoyés à votre serveur SIEM.

## <a name="sample-azure-atp-security-alerts-in-cef-format"></a>Exemples d’alertes de sécurité Azure ATP au format CEF
Les champs suivants et leurs valeurs sont transférés à votre serveur SIEM :

|Détail|Explication|
|---------|---------------|
|start|heure de début de l’alerte|
|suser|compte (généralement le compte d’utilisateur) impliqué dans l’alerte|
|compte d'ordinateur|compte (généralement le compte d’utilisateur) impliqué dans l’alerte|
|outcome|le cas échéant, réussite ou échec de l’activité suspecte dans l’alerte|
|msg|description de l'alerte|
|cnt|pour les alertes qui ont le compte du nombre de fois où l’activité s’est produite (par exemple une attaque par force brute a une certaine quantité de mots de passe devinés)|
|app |protocole utilisé dans cette alerte|
|externalId|ID de type d’événement écrit par Azure ATP dans le journal des événements correspondant à chaque type d’alerte|
|cs#label|chaînes du client autorisées par CEF, où cs#label est le nom du nouveau champ |
|cs#|chaînes du client autorisés par CEF, où cs# est sa valeur.|
|
- Par exemple : cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
<br> Le champ cs1 est l’URL de l’alerte. 

- Exemple : cs2Label=trigger cs2=new
<br> Le champ cs2 identifie s’il s’agit d’une alerte nouvelle ou mise à jour.


> [!NOTE]
> Si vous envisagez de créer l’automatisation ou des scripts pour les journaux Azure ATP SIEM, nous vous recommandons d’utiliser le champ **externalId** afin d’identifier le type d’alerte au lieu d’utiliser le nom de l’alerte à cet effet. Les noms d’alerte peuvent parfois être modifiés alors que l’**externalId** de chaque alerte est définitif.  

## <a name="azure-atp-security-alert-unique-externalids"></a>ExternalIds uniques des alertes de sécurité Azure ATP

> [!div class="mx-tableFixed"] 
|Nouveau nom de l’alerte de sécurité|Ancien nom de l’alerte de sécurité|ExternalId unique|
|---------|----------|---------|
|Suspicion d’attaque par force brute (LDAP)|Attaque par force brute par le biais d’une liaison simple LDAP|2004|
|Suspicion d’attaque Skeleton Key (passage à une version antérieure du chiffrement)|Activité de passage à une version antérieure du chiffrement (Skeleton Key)|2011|
|Suspicion d’attaque over-pass-the-hash (passage à une version antérieure du chiffrement)|Activité de passage à une version antérieure du chiffrement (attaque Overpass-the-Hash potentielle)|2008|
|Suspicion d’utilisation de golden ticket (passage à une version antérieure du chiffrement)|Activité de passage à une version antérieure du chiffrement (attaque golden ticket potentielle)|2009|
|Suspicion d’attaque Skeleton Key (passage à une version antérieure du chiffrement)|Activité de passage à une version antérieure du chiffrement (attaque Skeleton Key potentielle)|2010|
|Activité Honeytoken|Activité Honeytoken|2014|
|Suspicion d'usurpation d’identité (pass-the-hash)|Usurpation d’identité par attaque Pass-the-Hash|2017|
|Suspicion d’usurpation d’identité (pass-the-ticket)|Usurpation d’identité par attaque Pass-the-Ticket|2018|
|Suspicion d’utilisation de golden ticket (anomalie de temps) |Golden ticket Kerberos - anomalie de temps|2022|
|Suspicion d’utilisation de golden ticket (compte inexistant)|Golden ticket Kerberos - compte inexistant|2027|
|Demande malveillante de la clé principale de l’API de protection des données|Demande d’information privée de protection contre les données malveillantes|2020|
|Suspicion d’attaque DCSync (réplication de services d’annuaire)|Réplication malveillante de services d’annuaire|2006|
|Suspicion d’utilisation de golden ticket (données d’autorisation falsifiées) |Réaffectation de privilèges à l’aide de données d’autorisation falsifiées|2013|
|Reconnaissance d’énumération de compte|Reconnaissance à l’aide de l’énumération de compte|2003|
|Reconnaissance de mappage de réseau (DNS)|Reconnaissance à l’aide de DNS|2007|
|Reconnaissance des utilisateurs et des adresses IP (SMB) |Reconnaissance à l’aide de l’énumération de sessions SMB|2012|
|Reconnaissance des utilisateurs et des membres d’un groupe (SAMR)|Reconnaissance à l’aide de requêtes de services d’annuaire|2021|
|Tentative d’exécution de code à distance|Tentative d’exécution de code à distance|2019|
|Suspicion d’attaque DCShadow (demande de réplication du contrôleur de domaine)|Demande de réplication suspecte du contrôleur de domaine (attaque DcShadow potentielle)|2029|
|Suspicion d’attaque DCShadow (promotion du contrôleur de domaine)|Promotion du contrôleur de domaine suspect (attaque DcShadow potentielle)|2028|
|Communication suspecte sur DNS|Communication suspecte sur DNS|2031|
|Modification suspecte de groupes sensibles|Modification suspecte de groupes sensibles|2024|
|Création de service malveillant|Création de service malveillant|2026|
|Connexion VPN suspecte|Connexion VPN suspecte|2025|
|Suspicion d’attaque de ransomware WannaCry|Implémentation de protocole inhabituelle (attaque ransomware WannaCry potentielle)*|2002|
|Suspicion d’attaque par force brute (SMB)|Implémentation de protocole inhabituelle (utilisation potentielle d’outils malveillants tels que Hydra)*|2002|
|Suspicion d’utilisation du framework de piratage Metasploit|Implémentation de protocole inhabituelle (utilisation potentielle d’outils de piratage Metasploit)*|2002|
|Suspicion d’attaque over-pass-the-hash (Kerberos)|Implémentation inhabituelle du protocole Kerberos (attaque Overpass-the-Hash potentielle)*|2002|
|Les alertes *Implémentation de protocole inhabituelle* ont toutes le même externalId. Cet externalId sera changé dans une version ultérieure pour avoir un externalId propre à chaque type d’alerte||****|

## <a name="sample-logs"></a>Exemples de journaux

Les exemples de journaux sont conformes à la RFC 5242, mais Azure ATP prend également en charge la RFC 3164.

Priorités :

- 3=Faible
- 5=Moyenne
- 10=Élevée

### <a name="brute-force-attack-using-ldap-simple-bind"></a>Attaque par force brute par le biais d’une liaison simple LDAP
21-02-2018  16:20:21    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:06.156238+00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|LdapBruteForceSecurityAlert|Attaque par force brute à l’aide d’une liaison simple LDAP|5|start=2018-02-21T14:19:41.7422810Z app=Ldap suser=Wofford Thurston shost=CLIENT1 msg=Une attaque en force brute utilisant le protocole Ldap a été tentée sur Wofford Thurston (Software Engineer) à partir de CLIENT1 (100 tentatives de deviner le mot de passe). cnt=100 externalId=2004 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a cs2Label=trigger cs2=update

### <a name="encryption-downgrade-activity---golden-ticket"></a>Activité de passage à une version antérieure du chiffrement (golden ticket)
10-29-2018  11:25:07    Auth.Warning    192.168.0.202   1 2018-10-29T09:25:01.007701+00:00 DC3 CEF 3908 GoldenTicketEncryptionDowngradeS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|GoldenTicketEncryptionDowngradeSecurityAlert|Activité de passage à une version antérieure du chiffrement (attaque golden ticket potentielle)|5|start=2018-10-29T09:37:49.0849130Z app=Kerberos msg=W10-000007-Lap a utilisé une méthode de chiffrement plus faible (RC4),Â dans la requête de service Kerberos (TGS_REQ),Â reçue de W10-000007-Lap, pour accéder à host/domain1.test.local. externalId=2009 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f01f8403-88b2-437e-b4ad-d72485fe05ac cs2Label=trigger cs2=new

### <a name="encryption-downgrade-activity----skeleton-key"></a>Activité de passage à une version antérieure du chiffrement - Skeleton Key
21-02-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Activité de passage à une version antérieure du chiffrement|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=La méthode de chiffrement du champ ETYPE_INFO2 du message KRB_ERR de CLIENT1 a été passée à une version antérieure suivant un précédent comportement appris. Cela peut provenir d’un Skeleton Key sur DC1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=new

### <a name="encryption-downgrade-activity---overpass-the-hash"></a>Activité de passage à une version antérieure du chiffrement - Overpass-the-Hash
21-02-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Activité de passage à une version antérieure du chiffrement|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg= La méthode de chiffrement du champ Encrypted_Timestamp du message AS_REQ de CLIENT1 a été passée à une version antérieure suivant un précédent comportement appris. Cela peut provenir d’un vol des informations d’identification de type overpass-the-hash depuis CLIENT1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=update

### <a name="honeytoken-activity"></a>Activité Honeytoken
02-21-2018  16:20:36    Auth.Warning  192.168.0.220 1 2018-02-21T14:20:34.106162+00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|HoneytokenActivitySecurityAlert|Honeytoken activity|5|start=2018-02-21T14:20:26.6705617Z app=Kerberos suser=honey msg=Les activités suivantes ont été exécutées par honey :\r\nConnecté à CLIENT2 par le biais de DC1. externalId=2014 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c cs2Label=trigger cs2=new

### <a name="identity-theft-using-pass-the-hash"></a>Usurpation d’identité par Pass-the-Hash
21-02-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|Usurpation d’identité par attaque de type « Pass-The-Hash »|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Le code de hachage de Eugene Jenkins (Software Engineer) a été volé à l’un des ordinateurs déjà connectés par Eugene Jenkins (Software Engineer) et utilisé à partir de CLIENT1. externalId=2017 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=update

### <a name="identity-theft-using-pass-the-ticket-attack"></a>Usurpation d’identité par attaque Pass-the-Ticket
21-02-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheTicketSecurityAlert|Usurpation d’identité par attaque pass-the-ticket|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Les tickets Kerberos d’Eugene Jenkins (Software Engineer) ont été volés d’Admin-PC vers Victim-PC et utilisés pour accéder à krbtgt/DOMAIN1.TEST.LOCAL. externalId=2018 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=new

### <a name="kerberos-golden-ticket"></a>Kerberos Golden Ticket 
21-02-2018  16:22:39    Auth.Error  192.168.0.220   1 2018-02-21T14:22:34.274054+00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|GoldenTicketSecurityAlert|Activité de Golden Ticket Kerberos|10|start=2018-02-21T14:19:03.2416152Z app=Kerberos suser=Lanell Campos msg=Nous avons détecté une utilisation suspecte du ticket Kerberos de Lanell Campos (Software Engineer), ce qui peut indiquer une attaque par Golden Ticket. externalId=2022 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0 cs2Label=trigger cs2=update

### <a name="kerberos-golden-ticket-non-existent-account"></a>Compte inexistant Kerberos Golden Ticket
07-01-2018  14:28:49    Auth.Error  192.168.0.100   1 2018-07-01T11:28:35.546638+00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|ForgedPrincipalSecurityAlert|Golden Ticket Kerberos - compte inexistant|10|start=2018-07-01T09:48:31.2567987Z app=Kerberos suser=domain1.test.local\fake msg=domain1.test.local\faux, qui n’existe pas dans Active Directory, a utilisé un ticket Kerberos. Le ticket a été détecté sur 2 ordinateurs pour accéder à 3 ressources. Cela peut indiquer une attaque potentielle de Golden Ticket. externalId=2027 cs1Label=url cs1=https://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4 cs2Label=trigger cs2=update

### <a name="malicious-data-protection-private-information-request"></a>Demande d’information privée de protection contre les données malveillantes
10-29-2018  11:22:04    Auth.Error  192.168.0.202   1 2018-10-29T09:22:00.350864+00:00 DC3 CEF 3908 RetrieveDataProtectionBackupKeyS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|RetrieveDataProtectionBackupKeySecurityAlert|Demande d’information privée de protection contre les données malveillantes|10|start=2018-10-29T09:19:45.6307993Z app=LsaRpc shost=CLIENT1 msg=user1 a effectué 1 tentative réussie à partir de CLIENT1 pour récupérer la clé de sauvegarde du domaine DPAPI de DC1. externalId=2020 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/2f5717cb-2434-4d54-8af4-b2c6d14bc15c cs2Label=trigger cs2=new

### <a name="malicious-replication-of-directory-services"></a>Réplication malveillante de services d’annuaire 
21-02-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.254930+00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|MaliciousServiceCreationSecurityAlert|Création de service suspect|5|start=2018-02-21T14:19:41.7897808Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 a créé MaliciousService pour exécuter des commandes potentiellement dangereuses sur CLIENT1. externalId=2026 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c cs2Label=trigger cs2=update

### <a name="privilege-escalation-using-forged-authorization-data"></a>Réaffectation de privilèges à l’aide de données d’autorisation falsifiées
10-29-2018  11:22:04    Auth.Error  192.168.0.202   1 2018-10-29T09:21:59.288337+00:00 DC3 CEF 3908 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|ForgedPacSecurityAlert|Réaffectation de privilèges à l’aide de données d’autorisation falsifiées|10|start=2018-10-29T09:19:43.6403358Z app=Kerberos suser=user1 msg=Échec de la tentative d’user1 de réaffecter des privilèges sur DC1 dans host/domain1.test.local à partir de CLIENT1 en utilisant des données d’autorisation falsifiées. externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/b698d438-5013-4bca-be0b-f219f8b69108 cs2Label=trigger cs2=new

### <a name="reconnaissance-using-account-enumeration"></a>Reconnaissance à l’aide de l’énumération de compte
21-02-2018  16:19:35    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:27.540731+00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AccountEnumerationSecurityAlert|Reconnaissance à l’aide de l’énumération de compte|5|start=2018-02-21T14:19:02.6045416Z app=Kerberos shost=CLIENT1 suser=LMaldonado msg=Une activité d’énumération de compte suspecte utilisant le protocole Kerberos, provenant de CLIENT1, a été observée et a deviné avec succès Lamon Maldonado (Software Engineer). externalId=2003 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d cs2Label=trigger cs2=new

### <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance à l’aide de requêtes de services d’annuaire 
21-02-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|SamrReconnaissanceSecurityAlert| Reconnaissance à l’aide de l’énumération des services d’annuaires|5|start=2018-02-21T14:19:41.9912772Z app= Samr shost=CLIENT1 suser=user1 outcome=Success msg= Les énumérations des services d’annuaires suivantes à l’aide du protocole SAMR ont été tentées auprès de DC1 à partir de CLIENT1 :\r\nÉnumération correcte de tous les groupes dans domain1.test.local par user1. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label=trigger cs2=new

### <a name="reconnaissance-using-dns"></a>Reconnaissance à l’aide de DNS
21-02-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.063994+00:00 CENTER CEF 6076 DnsReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DnsReconnaissanceSecurityAlert|Reconnaissance DNS|5|start=2018-02-21T14:19:41.9417776Z app=Dns shost=CLIENT1 request=demo query requestMethod=Axfr reason=NoError outcome=Success msg=Une activité DNS suspecte provenant de CLIENT1 (qui n’est pas un serveur DNS) a été observée. La requête était pour la requête de démonstration (type Axfr). La réponse était NoError. externalId=2007 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c cs2Label=trigger cs2=update

### <a name="reconnaissance-using-smb-session-enumeration"></a>Reconnaissance à l’aide de l’énumération de sessions SMB
21-02-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.962930+00:00 CENTER CEF 6076 EnumerateSessionsSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EnumerateSessionsSecurityAlert|Reconnaissance à l’aide de l’énumération de sessions SMB|5|start=2018-02-21T14:19:03.2071170Z app=SrvSvc shost=CLIENT1 msg=Tentatives d’énumération de sessions SMB exécutées avec succès par user1, depuis CLIENT1 sur DC1, exposition de Eugene Jenkins (user2-computer). externalId=2012 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440 cs2Label=trigger cs2=new

### <a name="remote-code-execution-attempt"></a>Tentative d’exécution de code à distance
21-02-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 RemoteExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|RemoteExecutionSecurityAlert|Tentative d’exécution à distance détectée|5|start=2018-02-21T14:19:41.9912772Z app=Wmi shost=CLIENT1 suser=user1 outcome=Success msg=Les tentatives d’exécution à distance suivantes ont été exécutées sur DC1 depuis CLIENT1 :\r\nL’exécution à distance d’une ou de plusieurs méthodes WMI par user1 est réussie. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label=trigger cs2=new

### <a name="suspicious-authentication-failures"></a>Échecs d’authentification suspects
21-02-2018  16:19:20    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:15.397995+00:00 CENTER CEF 6076 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|BruteForceSecurityAlert|Échecs d’authentification suspects|5|start=2018-02-21T14:19:03.3831122Z app=Kerberos shost=CLIENT1 msg=Nous avons détecté un échec d’authentification suspect indiquant une possible attaque par force brute à partir de CLIENT1. externalId=2023 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6 cs2Label=trigger cs2=new

### <a name="suspicious-communication-over-dns"></a>Communication suspecte sur DNS
10-04-2018  14:49:38    Auth.Warning    192.168.0.202   1 2018-10-04T11:49:25.954059+00:00 DC3 CEF 3604 DnsSuspiciousCommunicationSecuri ï»¿0|Microsoft|Azure ATP|2.49.5589.58606|DnsSuspiciousCommunicationSecurityAlert|Communication suspecte sur DNS|5|start=2018-10-04T11:49:11.0822077Z app=DnsEvent dhost= suspiciousdomainname msg=CLIENT1 a envoyé des requêtes DNS suspectes résolvant suspiciousdomainname externalId=2031 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/0fc77777-49ca-40b3-a7ba-7644f355539e cs2Label=trigger cs2=new

### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Promotion du contrôleur de domaine suspect (attaque potentielle DcShadow)
07-12-2018  11:18:07    Auth.Error  192.168.0.200    1 2018-07-12T08:18:06.883880+00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRoguePromotionSecurityAlert| **Promotion du contrôleur de domaine suspect (attaque DCShadow potentielle)**|10|start=2018-07-12T08:17:55.4067092Z app=Ldap shost=CLIENT1 msg=CLIENT1, qui n’est pas un ordinateur dans domain1.test.local, a été enregistré comme contrôleur de domaine sur DC1. externalId=2028 cs1Label=url cs1=https://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53 cs2Label=trigger cs2=update

### <a name="suspicious-modification-of-sensitive-groups"></a>Modification suspecte de groupes sensibles
10-29-2018  11:21:03    Auth.Warning    192.168.0.202   1 2018-10-29T09:20:49.667014+00:00 DC3 CEF 3908 AbnormalSensitiveGroupMembership ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|AbnormalSensitiveGroupMembershipChangeSecurityAlert|Modification suspecte de groupes sensibles|5|start=2018-10-29T09:19:43.3013729Z app=GroupMembershipChangeEvent suser=user1 msg=user1 a anormalement modifié des appartenances à des groupes sensibles. externalId=2024 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6f7e677e-f068-41e5-bada-708cd5a322b9 cs2Label=trigger cs2=new

### <a name="suspicious-replication-of-directory-services"></a>Réplication suspecte de services d’annuaire
21-02-2018  16:21:22    Auth.Error  192.168.0.220   1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|Réplication malveillante de services d’annuaires|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=Des demandes de réplication malveillante ont été réalisées avec succès par user1 depuis CLIENT1 sur DC1. outcome=Success externalId=2006 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7 cs2Label=trigger cs2=new

### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Demande de réplication suspecte (attaque potentielle DcShadow)
07-12-2018  11:18:37    Auth.Error  192.168.0.200    1 2018-07-12T08:18:32.265989+00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRogueReplicationSecurityAlert| **Demande de réplication suspecte (attaque DCShadow potentielle)**|10|start=2018-07-12T08:17:55.3816102Z **app=Replication Activity** shost=CLIENT1 msg=CLIENT1, qui n'est pas un contrôleur de domaine valide dans domain1.test.local, a envoyé des changements aux objets annuaire sur DC1. externalId=2029 cs1Label=url cs1=https://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515 cs2Label=trigger cs2=new

### <a name="suspicious-service-creation"></a>Création de service malveillant 
10-29-2018  11:20:02    Auth.Warning    192.168.0.202   1 2018-10-29T09:19:59.164874+00:00 DC3 CEF 3908 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|MaliciousServiceCreationSecurityAlert|Création de service suspect|5|start=2018-10-29T09:19:44.9471965Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 a créé MaliciousService pour exécuter des commandes potentiellement dangereuses sur CLIENT1. externalId=2026 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/118bbe3d-fe72-40de-80d0-2678b68aa027 cs2Label=trigger cs2=new

### <a name="suspicious-vpn-connection"></a>Connexion VPN suspecte
07-03-2018  13:13:12    Auth.Warning  192.168.0.200   1 2018-07-03T10:13:06.187834+00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|AbnormalVpnSecurityAlert|Connexion VPN suspecte|5|start=2018-06-30T15:34:05.3887333Z app=VpnConnection suser=user1 msg=user1 connecté à un VPN avec trois ordinateurs à trois endroits.     externalId=2025 cs1Label=url cs1=https://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68 cs2Label=trigger cs2=new

### <a name="unusual-protocol-implementation---potential-use-of-malicious-tools-such-a-hydra"></a>Implémentation de protocole inhabituelle (utilisation potentielle d’outils malveillants tels que Hydra)
21-02-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|Implémentation de protocole inhabituelle|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=Des tentatives d’authentification ont été effectuées depuis CLIENT2 sur DC1 à l’aide d’une implémentation de protocole inhabituelle. Peut être la conséquence de l’utilisation d’outils malveillants pour l’exécution d’attaques de type « Pass-the-Hash » et par force brute. externalId=2002 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="unusual-protocol-implementation---potential-use-of-malicious-tools-such-a-metasploit"></a>Implémentation de protocole inhabituelle - (utilisation potentielle d’outils malveillants, comme Metasploit)
10-29-2018  11:22:04    Auth.Warning    192.168.0.202   1 2018-10-29T09:22:00.460233+00:00 DC3 CEF 3908 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|AbnormalProtocolSecurityAlert|Implémentation de protocole inhabituelle (utilisation potentielle d’outils malveillants tels que Metasploit)|5|start=2018-10-29T09:19:46.6092465Z app=Ntlm shost=CLIENT2 outcome=Success msg=Des tentatives d’authentification ont été effectuées par CLIENT2 sur DC1 à l’aide d’une implémentation de protocole inhabituelle. externalId=2002 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/573f10a1-6f8a-44b1-a5b1-212d40996363 cs2Label=trigger cs2=new

## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)