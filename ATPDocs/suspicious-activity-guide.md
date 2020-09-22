---
title: Guide des alertes de sécurité d’Azure ATP
description: Cet article fournit la liste des alertes de sécurité émises par Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/23/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f0c39f6ec4d47136324ba25c5c9bd29e0409854c
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90909977"
---
# <a name="azure-atp-security-alerts"></a>Alertes de sécurité Azure ATP

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE]
> Les fonctionnalités Azure ATP expliquées dans cette page sont également accessibles dans le nouveau [portail](https://portal.cloudappsecurity.com).

Les alertes de sécurité Azure ATP expliquent les activités suspectes détectées par des capteurs Azure ATP sur votre réseau, et présentent les acteurs et les ordinateurs impliqués dans chaque menace. Des listes de preuves d’alertes contiennent des liens directs vers les ordinateurs et les utilisateurs impliqués, afin de rendre vos recherches plus faciles et plus directes.

Les alertes de sécurité d’Azure ATP sont divisées en catégories ou phases (voir ci-dessous), comme les phases d’une chaîne de destruction de cyberattaque standard. Apprenez-en davantage sur chaque phase et sur les alertes conçues pour détecter chaque attaque, et découvrez comment utiliser les alertes pour vous aider à protéger votre réseau en suivant les liens ci-dessous :

  1. [Alertes de la phase de reconnaissance](reconnaissance-alerts.md)
  2. [Alertes de la phase des informations d’identification compromises](compromised-credentials-alerts.md)
  3. [Alertes de la phase de mouvement latéral](lateral-movement-alerts.md)
  4. [Alertes de la phase de dominance du domaine](domain-dominance-alerts.md)
  5. [Alertes de la phase d’exfiltration](exfiltration-alerts.md)

Pour en savoir plus sur la structure et les composants courants de toutes les alertes de sécurité Azure ATP, consultez [Présentation des alertes de sécurité](understanding-security-alerts.md).

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>Mappage des noms d’alertes de sécurité et ID externes uniques

Le tableau suivant répertorie le mappage entre les noms d’alerte, leurs ID externes uniques correspondants et leurs ID d’alerte Microsoft Cloud App Security. En cas d’utilisation avec des scripts ou avec l’automation, Microsoft recommande d’utiliser les ID externes des alertes au lieu de leur nom, car seuls les ID externes des alertes de sécurité sont permanents et non susceptibles d’être modifiés.

# <a name="external-ids"></a>[ID externes](#tab/external)

> [!div class="mx-tdBreakAll"]
> |Nom de l’alerte de sécurité|ID externe unique|Gravité|MITRE ATT&CK Matrix&trade;|
> |---|---|---|---|
> |[Reconnaissance d’énumération de compte](reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|2003|Moyenne|Découverte|
> |[Exfiltration de données sur SMB](exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)|2030|Importante|Exfiltration<br>Mouvement latéral<br>Commande et contrôle|
> |[Activité Honeytoken](compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|2014|Moyenne|Accès aux informations d’identification<br>Découverte|
> |[Demande malveillante de la clé principale de l’API de protection des données](domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|2020|Importante|Accès aux informations d’identification|
> |[Reconnaissance de mappage de réseau (DNS)](reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|2007|Moyenne|Découverte|
> |[Tentative d’exécution de code à distance](domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|2019|Moyenne|Exécution<br>Persistance<br>Élévation des privilèges<br>Intrusion dans la défense<br>Mouvement latéral|
> |[Exécution de code à distance sur DNS](lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|2036|Moyenne|Élévation des privilèges<br>Mouvement latéral|
> |[Reconnaissance de principal de sécurité (LDAP)](reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|2038|Moyenne|Accès aux informations d’identification|
> |[Suspicion d’attaque par force brute (Kerberos, NTLM)](compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|2023|Moyenne|Accès aux informations d’identification|
> |[Suspicion d’attaque par force brute (LDAP)](compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|2004|Moyenne|Accès aux informations d’identification|
> |[Suspicion d’attaque par force brute (SMB)](compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|2033|Moyenne|Mouvement latéral|
> |[Suspicion d’attaque DCShadow (promotion du contrôleur de domaine)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|2028|Importante|Intrusion dans la défense|
> |[Suspicion d’attaque DCShadow (demande de réplication du contrôleur de domaine)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|2029|Importante|Intrusion dans la défense|
> |[Suspicion d’attaque DCSync (réplication de services d’annuaire)](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|2006|Importante|Persistance<br>Accès aux informations d’identification|
> |[Suspicion d’utilisation de golden ticket (passage à une version antérieure du chiffrement)](domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|2009|Moyenne|Élévation des privilèges<br>Mouvement latéral<br>Persistance|
> |[Suspicion d’utilisation de golden ticket (données d’autorisation falsifiées)](domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|2013|Importante|Élévation des privilèges<br>Mouvement latéral<br>Persistance|
> |[Suspicion d’utilisation de golden ticket (compte inexistant)](domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|2027|Importante|Élévation des privilèges<br>Mouvement latéral<br>Persistance|
> |[Suspicion d’utilisation de golden ticket (anomalie de ticket)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|2032|Importante|Élévation des privilèges<br>Mouvement latéral<br>Persistance|
> |[Suspicion d’utilisation de golden ticket (anomalie de temps)](domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|2022|Importante|Élévation des privilèges<br>Mouvement latéral<br>Persistance|
> |[Suspicion d’usurpation d’identité (pass-the-hash)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|2017|Importante|Mouvement latéral|
> |[Suspicion d’usurpation d’identité (pass-the-ticket)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|2018|Importante ou Moyenne|Mouvement latéral|
> |[Falsification de l’authentification NTLM suspectée](lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|2039|Moyenne|Élévation des privilèges <br>Mouvement latéral|
> |[Suspicion d’attaque par relais NTLM](lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|2037|Moyenne ou Faible si observée à l’aide du protocole NTLM v2 signé|Élévation des privilèges <br>Mouvement latéral|
> |[Suspicion d’attaque over-pass-the-hash (Kerberos)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|2002|Moyenne|Mouvement latéral|
> |[Suspicion d’attaque Skeleton Key (passage à une version antérieure du chiffrement)](domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|2010|Moyenne|Mouvement latéral<br>Persistance|
> |[Manipulation présumée de paquet SMB (exploitation CVE-2020-0796) - (préversion)](lateral-movement-alerts.md#suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406)|2406|Importante|Mouvement latéral|
> |[Suspicion d’utilisation du framework de piratage Metasploit](compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|2034|Moyenne|Mouvement latéral|
> |[Suspicion d’attaque de ransomware WannaCry](compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|2035|Moyenne|Mouvement latéral|
> |[Ajouts suspects à des groupes sensibles](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|2024|Moyenne|Accès aux informations d’identification<br>Persistance|
> |[Communication suspecte sur DNS](exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|2031|Moyenne|Exfiltration|
> |[Création de service malveillant](domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|2026|Moyenne|Exécution<br>Persistance<br>Élévation des privilèges<br>Intrusion dans la défense<br>Mouvement latéral|
> |[Connexion VPN suspecte](compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|2025|Moyenne|Persistance<br>Intrusion dans la défense|
> |[Reconnaissance des utilisateurs et des membres d’un groupe (SAMR)](reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|2021|Moyenne|Découverte|
> |[Reconnaissance des utilisateurs et des adresses IP (SMB)](reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|2012|Moyenne|Découverte|


# <a name="cloud-app-security-ids"></a>[ID Cloud App Security](#tab/cloud-app-security)

> [!div class="mx-tdBreakAll"]
> |Nom de l’alerte de sécurité|ID d’alerte Cloud App Security|
> |---|---|
> |[Reconnaissance d’énumération de compte](reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|ALERT_EXTERNAL_AATP_ACCOUNT_ENUMERATION_SECURITY_ALERT|
> |[Exfiltration de données sur SMB](exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)|ALERT_EXTERNAL_AATP_SMB_DATA_EXFILTRATION_SECURITY_ALERT|
> |[Activité Honeytoken](compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|ALERT_EXTERNAL_AATP_HONEYTOKEN_ACTIVITY_SECURITY_ALERT|
> |[Demande malveillante de la clé principale de l’API de protection des données](domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|ALERT_EXTERNAL_AATP_RETRIEVE_DATA_PROTECTION_BACKUP_KEY_SECURITY_ALERT|
> |[Reconnaissance de mappage de réseau (DNS)](reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|ALERT_EXTERNAL_AATP_DNS_RECONNAISSANCE_SECURITY_ALERT|
> |[Tentative d’exécution de code à distance](domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|ALERT_EXTERNAL_AATP_REMOTE_EXECUTION_SECURITY_ALERT|
> |[Exécution de code à distance sur DNS](lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|ALERT_EXTERNAL_AATP_DNS_REMOTE_CODE_EXECUTION_SECURITY_ALERT|
> |[Reconnaissance de principal de sécurité (LDAP)](reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|ALERT_EXTERNAL_AATP_LDAP_SEARCH_RECONNAISSANCE_SECURITY_ALERT|
> |[Suspicion d’attaque par force brute (Kerberos, NTLM)](compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|ALERT_EXTERNAL_AATP_BRUTE_FORCE_SECURITY_ALERT|
> |[Suspicion d’attaque par force brute (LDAP)](compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|ALERT_EXTERNAL_AATP_LDAP_BRUTE_FORCE_SECURITY_ALERT|
> |[Suspicion d’attaque par force brute (SMB)](compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_BRUTE_FORCE_SECURITY_ALERT|
> |[Suspicion d’attaque DCShadow (promotion du contrôleur de domaine)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_ROGUE_PROMOTION_SECURITY_ALERT|
> |[Suspicion d’attaque DCShadow (demande de réplication du contrôleur de domaine)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_ROGUE_REPLICATION_SECURITY_ALERT|
> |[Suspicion d’attaque DCSync (réplication de services d’annuaire)](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_REPLICATION_SECURITY_ALERT|
> |[Suspicion d’utilisation de golden ticket (passage à une version antérieure du chiffrement)](domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[Suspicion d’utilisation de golden ticket (données d’autorisation falsifiées)](domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|ALERT_EXTERNAL_AATP_FORGED_PAC_SECURITY_ALERT|
> |[Suspicion d’utilisation de golden ticket (compte inexistant)](domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|ALERT_EXTERNAL_AATP_FORGED_PRINCIPAL_SECURITY_ALERT|
> |[Suspicion d’utilisation de golden ticket (anomalie de ticket)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_SIZE_ANOMALY_SECURITY_ALERT|
> |[Suspicion d’utilisation de golden ticket (anomalie de temps)](domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_SECURITY_ALERT|
> |[Suspicion d’usurpation d’identité (pass-the-hash)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|ALERT_EXTERNAL_AATP_PASS_THE_HASH_SECURITY_ALERT|
> |[Suspicion d’usurpation d’identité (pass-the-ticket)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|ALERT_EXTERNAL_AATP_PASS_THE_TICKET_SECURITY_ALERT|
> |[Falsification de l’authentification NTLM suspectée](lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|ALERT_EXTERNAL_AATP_ABNORMAL_NTLM_SIGNING_SECURITY_ALERT|
> |[Suspicion d’attaque par relais NTLM](lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|ALERT_EXTERNAL_AATP_NTLM_RELAY_SECURITY_ALERT|
> |[Suspicion d’attaque over-pass-the-hash (Kerberos)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|ALERT_EXTERNAL_AATP_ABNORMAL_KERBEROS_OVERPASS_THE_HASH_SECURITY_ALERT|
> |[Suspicion d’attaque Skeleton Key (passage à une version antérieure du chiffrement)](domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|ALERT_EXTERNAL_AATP_SKELETON_KEY_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[Manipulation présumée de paquet SMB (exploitation CVE-2020-0796) - (préversion)](lateral-movement-alerts.md#suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406)|ALERT_EXTERNAL_AATP_SMB_GHOST_SECURITY_ALERT|
> |[Suspicion d’utilisation du framework de piratage Metasploit](compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_METASPLOIT_SECURITY_ALERT|
> |[Suspicion d’attaque de ransomware WannaCry](compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_WANNA_CRY_SECURITY_ALERT|
> |[Ajouts suspects à des groupes sensibles](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|ALERT_EXTERNAL_AATP_ABNORMAL_SENSITIVE_GROUP_MEMBERSHIP_CHANGE_SECURITY_ALERT|
> |[Communication suspecte sur DNS](exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|ALERT_EXTERNAL_AATP_DNS_SUSPICIOUS_COMMUNICATION_SECURITY_ALERT|
> |[Création de service malveillant](domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|ALERT_EXTERNAL_AATP_MALICIOUS_SERVICE_CREATION_SECURITY_ALERT|
> |[Connexion VPN suspecte](compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|ALERT_EXTERNAL_AATP_ABNORMAL_VPN_SECURITY_ALERT|
> |[Reconnaissance des utilisateurs et des membres d’un groupe (SAMR)](reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|ALERT_EXTERNAL_AATP_SAMR_RECONNAISSANCE_SECURITY_ALERT|
> |[Reconnaissance des utilisateurs et des adresses IP (SMB)](reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|ALERT_EXTERNAL_AATP_ENUMERATE_SESSIONS_SECURITY_ALERT|

<!-- FROM TOP TABLE |[Suspected over-pass-the-hash attack (encryption downgrade)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|2008|Medium|Lateral movement|-->
<!-- FROM BOTTOM TABLE |[Suspected over-pass-the-hash attack (encryption downgrade)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|ALERT_EXTERNAL_AATP_OVERPASS_THE_HASH_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|-->

> [!NOTE]
> Pour désactiver une alerte de sécurité, contactez le support technique.

## <a name="see-also"></a>Voir aussi

- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Comprendre les alertes de sécurité](understanding-security-alerts.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
