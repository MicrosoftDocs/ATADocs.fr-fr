---
title: Informations de référence sur le journal SIEM Azure ATP | Microsoft Docs
description: Fournit des exemples de journaux d’activités suspectes envoyés depuis Azure ATP vers votre serveur SIEM.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 176ef6a45ba262e0242a1cd31f3aa1268f4ce28e
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2019
ms.locfileid: "58675147"
---
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
- Par exemple : cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
<br> Le champ cs1 est l’URL de l’alerte. 

- Exemple : cs2Label=trigger cs2=new
<br> Le champ cs2 identifie s’il s’agit d’une alerte nouvelle ou mise à jour.


> [!NOTE]
> Si vous envisagez de créer l’automatisation ou des scripts pour les journaux Azure ATP SIEM, nous vous recommandons d’utiliser le champ **externalId** afin d’identifier le type d’alerte au lieu d’utiliser le nom de l’alerte à cet effet. Les noms d’alerte peuvent parfois être modifiés alors que l’**externalId** de chaque alerte est définitif.  

## <a name="azure-atp-security-alert-unique-external-ids"></a>ID externes uniques des alertes de sécurité Azure ATP

> [!div class="mx-tableFixed"] 

|Nouveau nom de l’alerte de sécurité|Ancien nom de l’alerte de sécurité|ID externe unique|MITRE ATT&CK Matrix™ |
|---------|----------|---------|---------|
|[Reconnaissance d’énumération de compte](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|Reconnaissance à l’aide de l’énumération de compte|2003|Découverte|
|[Exfiltration de données sur SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)| NA| 2030|Exfiltration<br>Mouvement latéral<br>Commande et contrôle|
|[Activité Honeytoken](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|Activité Honeytoken|2014|Accès aux informations d’identification<br> Découverte|
|[Demande malveillante de la clé principale de l’API de protection des données](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|Demande d’information privée de protection contre les données malveillantes|2020|Accès aux informations d’identification|
|[Reconnaissance de mappage de réseau (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|Reconnaissance à l’aide de DNS|2007|Découverte|
|[Tentative d’exécution de code à distance](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|Tentative d’exécution de code à distance|2019|Exécution<br> Persistance<br> Élévation des privilèges<br> Intrusion dans la défense<br> Mouvement latéral|
|[Exécution de code à distance sur DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|NA|2036|Élévation des privilèges<br> Mouvement latéral|
|[Reconnaissance de principal de sécurité (LDAP) – préversion](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038---preview)|NA|2038|Accès aux informations d’identification|
|[Suspicion d’attaque par force brute (Kerberos, NTLM)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|Échecs d’authentification suspects|2023|Accès aux informations d’identification|
|[Suspicion d’attaque par force brute (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|Attaque par force brute par le biais d’une liaison simple LDAP|2004|Accès aux informations d’identification|
|[Suspicion d’attaque par force brute (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|Implémentation de protocole inhabituelle (utilisation potentielle d’outils malveillants comme Hydra)|2033|Mouvement latéral|
|[Suspicion d’attaque DCShadow (promotion du contrôleur de domaine)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|Promotion du contrôleur de domaine suspect (attaque DcShadow potentielle)|2028|Intrusion dans la défense|
|[Suspicion d’attaque DCShadow (demande de réplication du contrôleur de domaine)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|Demande de réplication suspecte du contrôleur de domaine (attaque DcShadow potentielle)|2029|Intrusion dans la défense|
|[Suspicion d’attaque DCSync (réplication de services d’annuaire)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|Réplication malveillante de services d’annuaire|2006|Persistance<br> Accès aux informations d’identification|
|[Suspicion d’utilisation de golden ticket (passage à une version antérieure du chiffrement)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|Activité de passage à une version antérieure du chiffrement (attaque golden ticket potentielle)|2009|Élévation des privilèges<br> Mouvement latéral<br>Persistance|
|[Suspicion d’utilisation de golden ticket (données d’autorisation falsifiées)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|Réaffectation de privilèges à l’aide de données d’autorisation falsifiées|2013|Élévation des privilèges<br>Mouvement latéral<br>Persistance|
|[Suspicion d’utilisation de golden ticket (compte inexistant)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|Golden ticket Kerberos - compte inexistant|2027|Élévation des privilèges<br> Mouvement latéral<br>Persistance|
|[Suspicion d’utilisation de golden ticket (anomalie de ticket)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|NA|2032|Élévation des privilèges<br> Mouvement latéral<br>Persistance|
|[Suspicion d’utilisation de golden ticket (anomalie de temps)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|Golden ticket Kerberos - anomalie de temps|2022|Élévation des privilèges<br> Mouvement latéral<br>Persistance|
|[Suspicion d’usurpation d’identité (pass-the-hash)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|Usurpation d’identité par attaque Pass-the-Hash|2017|Mouvement latéral|
|[Suspicion d’usurpation d’identité (pass-the-ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|Usurpation d’identité par attaque Pass-the-Ticket|2018|Mouvement latéral|
|[Suspicion d’attaque over-pass-the-hash (passage à une version antérieure du chiffrement)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|Activité de passage à une version antérieure du chiffrement (attaque Overpass-the-Hash potentielle)|2008|Mouvement latéral|
|[Suspicion d’attaque over-pass-the-hash (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|Implémentation inhabituelle du protocole Kerberos (attaque overpass-the-hash potentielle)|2002|Mouvement latéral|
|[Suspicion d’attaque Skeleton Key (passage à une version antérieure du chiffrement)](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|Activité de passage à une version antérieure du chiffrement (attaque Skeleton Key potentielle)|2010|Mouvement latéral<br> Persistance|
|[Suspicion d’utilisation du framework de piratage Metasploit](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|Implémentation de protocole inhabituelle (utilisation potentielle d’outils de piratage Metasploit)|2034|Mouvement latéral|
|[Suspicion d’attaque de relais NTLM (compte Exchange) - préversion](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037---preview)|NA|2037|Élévation des privilèges <br> Mouvement latéral|
|[Suspicion d’attaque de ransomware WannaCry](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|Implémentation de protocole inhabituelle (attaque ransomware WannaCry potentielle)|2035|Mouvement latéral|
|[Communication suspecte sur DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|Communication suspecte sur DNS|2031|Exfiltration|
|[Modification suspecte de groupes sensibles](atp-domain-dominance-alerts.md#suspicious-modification-of-sensitive-groups-external-id-2024)|Modification suspecte de groupes sensibles|2024|Accès aux informations d’identification<br>Persistance|
|[Création de service malveillant](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|Création de service malveillant|2026|Exécution<br> Persistance<br> Élévation des privilèges<br> Intrusion dans la défense<br>Mouvement latéral|
|[Connexion VPN suspecte](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|Connexion VPN suspecte|2025|Persistance<br>Intrusion dans la défense|
|[Reconnaissance des utilisateurs et des membres d’un groupe (SAMR)](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|Reconnaissance à l’aide de requêtes de services d’annuaire|2021|Découverte|
|[Reconnaissance des utilisateurs et des adresses IP (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|Reconnaissance à l’aide de l’énumération de sessions SMB|2012|Découverte|

## <a name="sample-logs"></a>Exemples de journaux

Les exemples de journaux sont conformes à la RFC 5242, mais Azure ATP prend également en charge la RFC 3164.

Priorités :

- 3=Faible
- 5=Moyenne
- 10=Élevée

### <a name="account-enumeration-reconnaissance"></a>Reconnaissance d’énumération de compte 
21-02-2018  16:19:35    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:27.540731+00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AccountEnumerationSecurityAlert|Reconnaissance à l’aide de l’énumération de compte|5|start=2018-02-21T14:19:02.6045416Z app=Kerberos shost=CLIENT1 suser=LMaldonado msg=Une activité d’énumération de compte suspecte utilisant le protocole Kerberos, provenant de CLIENT1, a été observée et a deviné avec succès Lamon Maldonado (Software Engineer). externalId=2003 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d cs2Label=trigger cs2=new

### <a name="data-exfiltration-over-smb"></a>Exfiltration de données sur SMB
12-19-2018  14:17:46    Auth.Error     127.0.0.1      1 2018-12-19T12:17:34.645993+00:00 DC1 CEF 3288 SmbDataExfiltrationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.60.0.0|SmbDataExfiltrationSecurityAlert|[PRÉVERSION] Exfiltration de données sur SMB|10|start=2018-12-19T12:14:12.4932821Z app=Smb shost=CLIENT1 msg=Eugene Jenkins (Software Engineer) sur DC2 a copié des fichiers suspects sur CLIENT1. externalId=2030 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/3ca2ec9d-2c67-44cc-a2d6-391716611bb6 cs2Label=trigger cs2=new

### <a name="honeytoken-activity"></a>Activité Honeytoken
02-21-2018  16:20:36    Auth.Warning  192.168.0.220 1 2018-02-21T14:20:34.106162+00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|HoneytokenActivitySecurityAlert|Honeytoken activity|5|start=2018-02-21T14:20:26.6705617Z app=Kerberos suser=honey msg=Les activités suivantes ont été exécutées par honey :\r\nConnecté à CLIENT2 par le biais de DC1. externalId=2014 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c cs2Label=trigger cs2=new

### <a name="malicious-request-of-data-protection-api-master-key"></a>Demande malveillante de la clé principale de l’API de protection des données 
10-29-2018  11:22:04    Auth.Error  192.168.0.202   1 2018-10-29T09:22:00.350864+00:00 DC3 CEF 3908 RetrieveDataProtectionBackupKeyS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|RetrieveDataProtectionBackupKeySecurityAlert|Demande d’information privée de protection contre les données malveillantes|10|start=2018-10-29T09:19:45.6307993Z app=LsaRpc shost=CLIENT1 msg=user1 a effectué 1 tentative réussie à partir de CLIENT1 pour récupérer la clé de sauvegarde du domaine DPAPI de DC1. externalId=2020 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/2f5717cb-2434-4d54-8af4-b2c6d14bc15c cs2Label=trigger cs2=new

### <a name="network-mapping-reconnaissance-dns"></a>Reconnaissance de mappage de réseau (DNS)
10-29-2018  11:20:02    Auth.Warning    192.168.0.202   1 2018-10-29T09:19:59.056894+00:00 DC3 CEF 3908 DnsReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|DnsReconnaissanceSecurityAlert|Reconnaissance à l’aide de DNS|5|start=2018-10-29T09:19:43.5033765Z app=Dns shost=CLIENT1 msg=Une activité DNS suspecte a été observée, provenant de CLIENT1 (qui n’est pas un serveur DNS) sur DC1. externalId=2007 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/23937d33-ff71-484d-be0a-3c417fe573ce cs2Label=trigger cs2=new

### <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance à l’aide de requêtes de services d’annuaire 
21-02-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|SamrReconnaissanceSecurityAlert| Reconnaissance à l’aide de l’énumération des services d’annuaires|5|start=2018-02-21T14:19:41.9912772Z app= Samr shost=CLIENT1 suser=user1 outcome=Success msg= Les énumérations des services d’annuaires suivantes à l’aide du protocole SAMR ont été tentées auprès de DC1 à partir de CLIENT1 :\r\nÉnumération correcte de tous les groupes dans domain1.test.local par user1. externalId=2019 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label=trigger cs2=new

### <a name="remote-code-execution-attempt"></a>Tentative d’exécution de code à distance
10-29-2018  11:22:04    Auth.Warning    192.168.0.202   1 2018-10-29T09:22:00.100856+00:00 DC3 CEF 3908 RemoteExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|RemoteExecutionSecurityAlert|Tentative d’exécution de code à distance|5|start=2018-10-29T09:19:45.0552367Z shost=CLIENT1 msg=Les tentatives d’exécution de code à distance suivantes ont été effectuées sur DC1 à partir de CLIENT1 :\r\nPlanification à distance réussie d’une ou plusieurs tâches par user1.\r\nÉchec de la planification à distance d’une ou plusieurs tâches par user1.\r\nExécution à distance réussie d’une ou plusieurs méthodes WMI par user1. externalId=2019 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/f063c778-830c-4e9f-98d1-bc6c11c94e11 cs2Label=trigger cs2=new

### <a name="remote-code-execution-over-dns"></a>Exécution de code à distance sur DNS
1-17-2019   08:24:54    Auth.Warning    192.168.0.202   1 2019-01-17T08:24:54.100856+00:00 DC3 CEF 3908 DnsRemoteCodeExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.63.0.0|DnsRemoteCodeExecutionSecurityAlert|[PREVIEW] Remote code execution over DNS|5|start=2019-01-17T08:24:54.5293800Z app=Dns shost=CLIENT1 msg=An actor attempted to run commands remotely on CLIENT1 from DC1, over DNS protocol. externalId=2036 cs1Label=url cs1=https\:////contoso-corp.atp.azure.com:13000/securityAlert/591f9769-d904-40b1-89fa-c307c2ca814f cs2Label=trigger cs2=new

### <a name="security-principal-reconnaissance-ldap---preview"></a>Reconnaissance de principal de sécurité (LDAP) – préversion 
02-18-2019  16:48:08 Auth.Warning  127.0.0.1  1 2019-02-18T14:48:02.912264+00:00 DC1 CEF 4656 LdapSearchReconnaissanceSecurity ï»¿0|Microsoft|Azure ATP|2.66.0.0|LdapSearchReconnaissanceSecurityAlert|[PREVIEW] Reconnaissance à l’aide de requêtes LDAP|5|start=2019-02-18T14:46:29.4644276Z app=LdapSearch shost=CLIENT1 msg=Un acteur sur CLIENT1 a envoyé des requêtes LDAP suspectes à DC1, recherche de 4 types d’énumération et Opérateurs de serveur (les membres peuvent administrer les serveurs de domaine) dans 2 domaines externalId=2038 cs1Label=url cs1=https\://contoso-corp.atp.azure..com:13000/securityAlert/81ea99c4-ce1f-4581-ac8f-7440fbed7cd0 cs2Label=trigger cs2=new

### <a name="suspected-brute-force-attack-ldap"></a>Suspicion d’attaque par force brute (LDAP)
21-02-2018  16:20:21    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:06.156238+00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|LdapBruteForceSecurityAlert|Attaque par force brute à l’aide d’une liaison simple LDAP|5|start=2018-02-21T14:19:41.7422810Z app=Ldap suser=Wofford Thurston shost=CLIENT1 msg=Une attaque en force brute utilisant le protocole Ldap a été tentée sur Wofford Thurston (Software Engineer) à partir de CLIENT1 (100 tentatives de deviner le mot de passe). cnt=100 externalId=2004 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a cs2Label=trigger cs2=update

### <a name="suspected-brute-force-attack-kerberos-ntlm"></a>Suspicion d’attaque par force brute (Kerberos, NTLM)
10-29-2018  11:20:47    Auth.Warning    192.168.0.202   1 2018-10-29T09:20:44.478827+00:00 DC3 CEF 3908 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|BruteForceSecurityAlert|Échecs d’authentification suspects|5|start=2018-10-29T09:19:44.9512286Z app=Kerberos shost=CLIENT1 msg=Des échecs d'authentification suspects indiquant une attaque potentielle par force brute ont été détectés par CLIENT1. externalId=2023 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/85042c8e-27fa-49b3-8667-dabc1aa31580 cs2Label=trigger cs2=new

### <a name="suspected-golden-ticket-usage-encryption-downgrade"></a>Suspicion d’utilisation de golden ticket (passage à une version antérieure du chiffrement)
10-29-2018  11:25:07    Auth.Warning    192.168.0.202   1 2018-10-29T09:25:01.007701+00:00 DC3 CEF 3908 GoldenTicketEncryptionDowngradeS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|GoldenTicketEncryptionDowngradeSecurityAlert|Activité de passage à une version antérieure du chiffrement (attaque golden ticket potentielle)|5|start=2018-10-29T09:37:49.0849130Z app=Kerberos msg=W10-000007-Lap a utilisé une méthode de chiffrement plus faible (RC4),Â dans la requête de service Kerberos (TGS_REQ),Â reçue de W10-000007-Lap, pour accéder à host/domain1.test.local. externalId=2009 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/f01f8403-88b2-437e-b4ad-d72485fe05ac cs2Label=trigger cs2=new

### <a name="suspected-golden-ticket-usage-non-existent-account"></a>Suspicion d’utilisation de golden ticket (compte inexistant)
07-01-2018  14:28:49    Auth.Error  192.168.0.100   1 2018-07-01T11:28:35.546638+00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|ForgedPrincipalSecurityAlert|Golden Ticket Kerberos - compte inexistant|10|start=2018-07-01T09:48:31.2567987Z app=Kerberos suser=domain1.test.local\fake msg=domain1.test.local\faux, qui n’existe pas dans Active Directory, a utilisé un ticket Kerberos. Le ticket a été détecté sur 2 ordinateurs pour accéder à 3 ressources. Cela peut indiquer une attaque potentielle de Golden Ticket. externalId=2027 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4 cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-ticket-anomaly"></a>Suspicion d’utilisation de golden ticket (anomalie de ticket) 
1 2018-11-18T10:46:23.346946+00:00 MAXIMG-7050 CEF 24284 GoldenTicketSizeAnomalySecurityA 0|Microsoft|Azure ATP|2.56.0.0|GoldenTicketSizeAnomalySecurityAlert|[PREVIEW] Suspicion d’utilisation de golden ticket (anomalie de ticket)|10|start=2018-11-18T10:44:12.9317797Z app=Kerberos shost=CLIENT2 suser=RFosdyke msg=Renzo Fosdyke (ingénieur logiciel) a utilisé un ticket Kerberos suspect à partir de CLIENT2 pour accéder à ldap/domain1.test.local. externalId=2032 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/63600e03-f423-49bf-a92d-4010e1d52b9f cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-time-anomaly"></a>Suspicion d’utilisation de golden ticket (anomalie de temps) 
21-02-2018  16:22:39    Auth.Error  192.168.0.220   1 2018-02-21T14:22:34.274054+00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|GoldenTicketSecurityAlert|Activité de Golden Ticket Kerberos|10|start=2018-02-21T14:19:03.2416152Z app=Kerberos suser=Lanell Campos msg=Nous avons détecté une utilisation suspecte du ticket Kerberos de Lanell Campos (Software Engineer), ce qui peut indiquer une attaque par Golden Ticket. externalId=2022 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0 cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-forged-authorization-data"></a>Suspicion d’utilisation de golden ticket (données d’autorisation falsifiées) 
10-29-2018  11:22:04    Auth.Error  192.168.0.202   1 2018-10-29T09:21:59.288337+00:00 DC3 CEF 3908 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|ForgedPacSecurityAlert|Réaffectation de privilèges à l’aide de données d’autorisation falsifiées|10|start=2018-10-29T09:19:43.6403358Z app=Kerberos suser=user1 msg=Échec de la tentative d’user1 de réaffecter des privilèges sur DC1 dans host/domain1.test.local à partir de CLIENT1 en utilisant des données d’autorisation falsifiées. externalId=2013 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/b698d438-5013-4bca-be0b-f219f8b69108 cs2Label=trigger cs2=new

### <a name="suspected-identity-theft-pass-the-hash"></a>Suspicion d’usurpation d’identité (pass-the-hash)
21-02-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|Usurpation d’identité par attaque de type « Pass-The-Hash »|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Le code de hachage de Eugene Jenkins (Software Engineer) a été volé à l’un des ordinateurs déjà connectés par Eugene Jenkins (Software Engineer) et utilisé à partir de CLIENT1. externalId=2017 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=update

### <a name="suspected-identity-theft-pass-the-ticket"></a>Suspicion d’usurpation d’identité (pass-the-ticket) 
21-02-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheTicketSecurityAlert|Usurpation d’identité par attaque pass-the-ticket|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Les tickets Kerberos d’Eugene Jenkins (Software Engineer) ont été volés d’Admin-PC vers Victim-PC et utilisés pour accéder à krbtgt/DOMAIN1.TEST.LOCAL. externalId=2018 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=new

### <a name="suspected-over-pass-the-hash-attack-encryption-downgrade"></a>Suspicion d'attaque over-pass-the-hash (passage à une version antérieure du chiffrement) 
21-02-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Activité de passage à une version antérieure du chiffrement|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg= La méthode de chiffrement du champ Encrypted_Timestamp du message AS_REQ de CLIENT1 a été passée à une version antérieure suivant un précédent comportement appris. Cela peut provenir d’un vol des informations d’identification de type overpass-the-hash depuis CLIENT1. externalId=2008 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=update

### <a name="suspected-skeleton-key-attack-encryption-downgrade"></a>Suspicion d’attaque Skeleton Key (passage à une version antérieure du chiffrement) 
21-02-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Activité de passage à une version antérieure du chiffrement|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=La méthode de chiffrement du champ ETYPE_INFO2 du message KRB_ERR de CLIENT1 a été passée à une version antérieure suivant un précédent comportement appris. Cela peut provenir d’un Skeleton Key sur DC1. externalId=2010 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=new

### <a name="suspected-dcsync-attack-replication-of-directory-services"></a>Suspicion d’attaque DCSync (réplication de services d’annuaire)
21-02-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.254930+00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|MaliciousServiceCreationSecurityAlert|Création de service suspect|5|start=2018-02-21T14:19:41.7897808Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 a créé MaliciousService pour exécuter des commandes potentiellement dangereuses sur CLIENT1. externalId=2026 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c cs2Label=trigger cs2=update

### <a name="suspicious-authentication-failures"></a>Échecs d’authentification suspects
21-02-2018  16:19:20    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:15.397995+00:00 CENTER CEF 6076 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|BruteForceSecurityAlert|Échecs d’authentification suspects|5|start=2018-02-21T14:19:03.3831122Z app=Kerberos shost=CLIENT1 msg=Nous avons détecté un échec d’authentification suspect indiquant une possible attaque par force brute à partir de CLIENT1. externalId=2023 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6 cs2Label=trigger cs2=new

### <a name="suspicious-communication-over-dns"></a>Communication suspecte sur DNS
10-04-2018  14:49:38    Auth.Warning    192.168.0.202   1 2018-10-04T11:49:25.954059+00:00 DC3 CEF 3604 DnsSuspiciousCommunicationSecuri ï»¿0|Microsoft|Azure ATP|2.49.5589.58606|DnsSuspiciousCommunicationSecurityAlert|Communication suspecte sur DNS|5|start=2018-10-04T11:49:11.0822077Z app=DnsEvent dhost= suspiciousdomainname msg=CLIENT1 a envoyé des requêtes DNS suspectes résolvant suspiciousdomainname externalId=2031 cs1Label=url cs1=\://contoso-corp.atp.azure.com/securityAlert/0fc77777-49ca-40b3-a7ba-7644f355539e cs2Label=trigger cs2=new

### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Promotion du contrôleur de domaine suspect (attaque potentielle DcShadow)
07-12-2018  11:18:07    Auth.Error  192.168.0.200    1 2018-07-12T08:18:06.883880+00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRoguePromotionSecurityAlert| **Promotion du contrôleur de domaine suspect (attaque DCShadow potentielle)**|10|start=2018-07-12T08:17:55.4067092Z app=Ldap shost=CLIENT1 msg=CLIENT1, qui n’est pas un ordinateur dans domain1.test.local, a été enregistré comme contrôleur de domaine sur DC1. externalId=2028 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53 cs2Label=trigger cs2=update

### <a name="suspicious-modification-of-sensitive-groups"></a>Modification suspecte de groupes sensibles
10-29-2018  11:21:03    Auth.Warning    192.168.0.202   1 2018-10-29T09:20:49.667014+00:00 DC3 CEF 3908 AbnormalSensitiveGroupMembership ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|AbnormalSensitiveGroupMembershipChangeSecurityAlert|Modification suspecte de groupes sensibles|5|start=2018-10-29T09:19:43.3013729Z app=GroupMembershipChangeEvent suser=user1 msg=user1 a anormalement modifié des appartenances à des groupes sensibles. externalId=2024 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6f7e677e-f068-41e5-bada-708cd5a322b9 cs2Label=trigger cs2=new

### <a name="suspicious-replication-of-directory-services"></a>Réplication suspecte de services d’annuaire
21-02-2018  16:21:22    Auth.Error  192.168.0.220   1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|Réplication malveillante de services d’annuaires|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=Des demandes de réplication malveillante ont été réalisées avec succès par user1 depuis CLIENT1 sur DC1. outcome=Success externalId=2006 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7 cs2Label=trigger cs2=new

### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Demande de réplication suspecte (attaque potentielle DcShadow)
07-12-2018  11:18:37    Auth.Error  192.168.0.200    1 2018-07-12T08:18:32.265989+00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRogueReplicationSecurityAlert| **Demande de réplication suspecte (attaque DCShadow potentielle)**|10|start=2018-07-12T08:17:55.3816102Z **app=Replication Activity** shost=CLIENT1 msg=CLIENT1, qui n'est pas un contrôleur de domaine valide dans domain1.test.local, a envoyé des changements aux objets annuaire sur DC1. externalId=2029 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515 cs2Label=trigger cs2=new

### <a name="suspicious-service-creation"></a>Création de service malveillant 
10-29-2018  11:20:02    Auth.Warning    192.168.0.202   1 2018-10-29T09:19:59.164874+00:00 DC3 CEF 3908 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|MaliciousServiceCreationSecurityAlert|Création de service suspect|5|start=2018-10-29T09:19:44.9471965Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 a créé MaliciousService pour exécuter des commandes potentiellement dangereuses sur CLIENT1. externalId=2026 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/118bbe3d-fe72-40de-80d0-2678b68aa027 cs2Label=trigger cs2=new

### <a name="suspicious-vpn-connection"></a>Connexion VPN suspecte
07-03-2018  13:13:12    Auth.Warning  192.168.0.200   1 2018-07-03T10:13:06.187834+00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|AbnormalVpnSecurityAlert|Connexion VPN suspecte|5|start=2018-06-30T15:34:05.3887333Z app=VpnConnection suser=user1 msg=user1 connecté à un VPN avec trois ordinateurs à trois endroits.     externalId=2025 cs1Label=url cs1=https\://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68 cs2Label=trigger cs2=new

### <a name="suspected-wannacry-ransomware-attack"></a>Suspicion d’attaque de ransomware WannaCry
02-21-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedWannaCryRansomwareAttack|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=Des tentatives d’authentification ont été effectuées depuis CLIENT2 sur DC1 à l’aide d’une implémentation de protocole inhabituelle. Peut être la conséquence de l’utilisation d’outils malveillants pour l’exécution d’attaques telles que WannaCry. externalId=2035 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="suspected-brute-force-attack-smb"></a>Suspicion d’attaque par force brute (SMB)
002-21-2018 16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedBrutForceAttack|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=Des tentatives d’authentification ont été effectuées depuis CLIENT2 sur DC1 à l’aide d’une implémentation de protocole inhabituelle. Peut être la conséquence de l’utilisation d’outils malveillants pour l’exécution d’attaques telles que Hydra. externalId=2033 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="suspected-use-of-metasploit-hacking-framework"></a>Suspicion d’utilisation du framework de piratage Metasploit
002-21-2018 16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedAttackUsingMetasploit|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=Des tentatives d’authentification ont été effectuées depuis CLIENT2 sur DC1 à l’aide d’une implémentation de protocole inhabituelle. Peut être la conséquence de l’utilisation d’outils malveillants pour l’exécution d’attaques telles que Metasploit. externalId=2034 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="suspected-overpass-the-hash-attack-kerberos"></a>Suspicion d’attaque over-pass-the-hash (Kerberos)
002-21-2018 16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedOverPassTheHashAttack|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=Des tentatives d’authentification ont été effectuées depuis CLIENT2 sur DC1 à l’aide d’une implémentation de protocole inhabituelle. Peut être la conséquence d’un acte malveillant à l’aide du protocole Kerberos. externalId=2002 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="user-and-ip-address-reconnaissance-smb"></a>Reconnaissance des utilisateurs et des adresses IP (SMB) 
002-21-2018 16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|ReconnaissanceusingSMBSessionEnumeration|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=Des tentatives d’authentification ont été effectuées depuis CLIENT2 sur DC1 à l’aide d’une implémentation de protocole inhabituelle. Peut être la conséquence de l’utilisation d’outils malveillants pour l’exécution d’attaques telles que Metasploit. externalId=2034 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
