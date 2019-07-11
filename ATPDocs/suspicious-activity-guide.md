---
title: Guide des alertes de sécurité d’Azure ATP | Microsoft Docs
d|Description: This article provides a list of the security alerts issued by Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 05/27/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7d8550113e1ea7cce6cb7ca1c6e497a9fc8e3708
ms.sourcegitcommit: 52bc20dfa1f64ff3e8c16eb5edea2813d54ba308
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67562164"
---
# <a name="azure-atp-security-alerts"></a>Alertes de sécurité Azure ATP

Les alertes de sécurité Azure ATP expliquent les activités suspectes détectées par des capteurs Azure ATP sur votre réseau, et présentent les acteurs et les ordinateurs impliqués dans chaque menace.   Des listes de preuves d’alertes contiennent des liens directs vers les ordinateurs et les utilisateurs impliqués, afin de rendre vos recherches plus faciles et plus directes.

Les alertes de sécurité d’Azure ATP sont divisées en catégories ou phases (voir ci-dessous), comme les phases d’une chaîne de destruction de cyberattaque standard. Apprenez-en davantage sur chaque phase et sur les alertes conçues pour détecter chaque attaque, et découvrez comment utiliser les alertes pour vous aider à protéger votre réseau en suivant les liens ci-dessous :

  1. [Alertes de la phase de reconnaissance](atp-reconnaissance-alerts.md)
  2. [Alertes de la phase des informations d’identification compromises](atp-compromised-credentials-alerts.md)
  3. [Alertes de la phase de mouvement latéral](atp-lateral-movement-alerts.md)
  4. [Alertes de la phase de dominance du domaine](atp-domain-dominance-alerts.md)
  5. [Alertes de la phase d’exfiltration](atp-exfiltration-alerts.md)

Pour en savoir plus sur la structure et les composants courants de toutes les alertes de sécurité Azure ATP, consultez [Présentation des alertes de sécurité](understanding-security-alerts.md).

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>Mappage des noms d’alertes de sécurité et ID externes uniques

Dans la version 2.56, toutes les alertes de sécurité Azure ATP existantes ont été renommées avec des noms plus faciles à comprendre. Les mappages entre les anciens et les nouveaux noms ainsi que leur externalId unique correspondant sont listés dans le tableau suivant. En cas d’utilisation avec des scripts ou avec l’automation, Microsoft recommande d’utiliser les ID externes des alertes au lieu de leur nom, car seuls les ID externes des alertes de sécurité sont permanents et non susceptibles d’être modifiés.

> [!div class="mx-tableFixed"] 

|Nouveau nom de l’alerte de sécurité|Ancien nom de l’alerte de sécurité|ID externe unique|Gravité|MITRE ATT&CK Matrix™ |
|---------|----------|---------|---------|---------|
|[Reconnaissance d’énumération de compte](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|Reconnaissance à l’aide de l’énumération de compte|2003|Moyenne|Découverte|
|[Exfiltration de données sur SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)| NA| 2030|Importante|Exfiltration<br>Mouvement latéral<br>Commande et contrôle|
|[Activité Honeytoken](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|Activité Honeytoken|2014|Moyenne|Accès aux informations d’identification<br> Découverte|
|[Demande malveillante de la clé principale de l’API de protection des données](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|Demande d’information privée de protection contre les données malveillantes|2020|Importante|Accès aux informations d’identification|
|[Reconnaissance de mappage de réseau (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|Reconnaissance à l’aide de DNS|2007|Moyenne|Découverte|
|[Tentative d’exécution de code à distance](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|Tentative d’exécution de code à distance|2019|Moyenne|Exécution<br> Persistance<br> Élévation des privilèges<br> Intrusion dans la défense<br> Mouvement latéral|
|[Exécution de code à distance sur DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|NA|2036|Moyenne|Élévation des privilèges<br> Mouvement latéral|
|[Reconnaissance de principal de sécurité (LDAP)](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|NA|2038|Moyenne|Accès aux informations d’identification|
|[Suspicion d’attaque par force brute (Kerberos, NTLM)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|Échecs d’authentification suspects|2023|Moyenne|Accès aux informations d’identification|
|[Suspicion d’attaque par force brute (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|Attaque par force brute par le biais d’une liaison simple LDAP|2004|Moyenne|Accès aux informations d’identification|
|[Suspicion d’attaque par force brute (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|Implémentation de protocole inhabituelle (utilisation potentielle d’outils malveillants comme Hydra)|2033|Moyenne|Mouvement latéral|
|[Suspicion d’attaque DCShadow (promotion du contrôleur de domaine)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|Promotion du contrôleur de domaine suspect (attaque DcShadow potentielle)|2028|Importante|Intrusion dans la défense|
|[Suspicion d’attaque DCShadow (demande de réplication du contrôleur de domaine)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|Demande de réplication suspecte du contrôleur de domaine (attaque DcShadow potentielle)|2029|Importante|Intrusion dans la défense|
|[Suspicion d’attaque DCSync (réplication de services d’annuaire)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|Réplication malveillante de services d’annuaire|2006|Importante|Persistance<br> Accès aux informations d’identification|
|[Suspicion d’utilisation de golden ticket (passage à une version antérieure du chiffrement)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|Activité de passage à une version antérieure du chiffrement (attaque golden ticket potentielle)|2009|Moyenne|Élévation des privilèges<br> Mouvement latéral<br>Persistance|
|[Suspicion d’utilisation de golden ticket (données d’autorisation falsifiées)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|Réaffectation de privilèges à l’aide de données d’autorisation falsifiées|2013|Importante|Élévation des privilèges<br>Mouvement latéral<br>Persistance|
|[Suspicion d’utilisation de golden ticket (compte inexistant)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|Golden ticket Kerberos - compte inexistant|2027|Importante|Élévation des privilèges<br> Mouvement latéral<br>Persistance|
|[Suspicion d’utilisation de golden ticket (anomalie de ticket)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|NA|2032|Importante|Élévation des privilèges<br> Mouvement latéral<br>Persistance|
|[Suspicion d’utilisation de golden ticket (anomalie de temps)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|Golden ticket Kerberos - anomalie de temps|2022|Importante|Élévation des privilèges<br> Mouvement latéral<br>Persistance|
|[Suspicion d’usurpation d’identité (pass-the-hash)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|Usurpation d’identité par attaque Pass-the-Hash|2017|Importante|Mouvement latéral|
|[Suspicion d’usurpation d’identité (pass-the-ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|Usurpation d’identité par attaque Pass-the-Ticket|2018|Importante ou Moyenne|Mouvement latéral|
|[Suspicion d’attaque over-pass-the-hash (passage à une version antérieure du chiffrement)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|Activité de passage à une version antérieure du chiffrement (attaque Overpass-the-Hash potentielle)|2008|Moyenne|Mouvement latéral|
|[Suspicion d’attaque over-pass-the-hash (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|Implémentation inhabituelle du protocole Kerberos (attaque overpass-the-hash potentielle)|2002|Moyenne|Mouvement latéral|
|[Suspicion d’attaque Skeleton Key (passage à une version antérieure du chiffrement)](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|Activité de passage à une version antérieure du chiffrement (attaque Skeleton Key potentielle)|2010|Moyenne|Mouvement latéral<br> Persistance|
|[Suspicion d’utilisation du framework de piratage Metasploit](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|Implémentation de protocole inhabituelle (utilisation potentielle d’outils de piratage Metasploit)|2034|Moyenne|Mouvement latéral|
|[Suspicion d’attaque de relais NTLM (compte Exchange) - préversion](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037---preview)|NA|2037|Moyenne ou Faible si observée à l’aide du protocole NTLM v2 signé|Élévation des privilèges <br> Mouvement latéral|
|[Suspicion d’attaque de ransomware WannaCry](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|Implémentation de protocole inhabituelle (attaque ransomware WannaCry potentielle)|2035|Moyenne|Mouvement latéral|
|[Communication suspecte sur DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|Communication suspecte sur DNS|2031|Moyenne|Exfiltration|
|[Ajouts suspects à des groupes sensibles](atp-domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|Ajouts suspects à des groupes sensibles|2024|Moyenne|Accès aux informations d’identification<br>Persistance|
|[Création de service malveillant](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|Création de service malveillant|2026|Moyenne|Exécution<br> Persistance<br> Élévation des privilèges<br> Intrusion dans la défense<br>Mouvement latéral|
|[Connexion VPN suspecte](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|Connexion VPN suspecte|2025|Moyenne|Persistance<br>Intrusion dans la défense|
|[Reconnaissance des utilisateurs et des membres d’un groupe (SAMR)](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|Reconnaissance à l’aide de requêtes de services d’annuaire|2021|Moyenne|Découverte|
|[Reconnaissance des utilisateurs et des adresses IP (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|Reconnaissance à l’aide de l’énumération de sessions SMB|2012|Moyenne|Découverte|
|

> [!NOTE]
> Pour désactiver une alerte de sécurité, contactez le support technique.


## <a name="see-also"></a>Voir aussi
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Comprendre les alertes de sécurité](understanding-security-alerts.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
