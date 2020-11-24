---
title: Alertes de sécurité Microsoft Defender pour Identity indiquant un mouvement latéral
description: Cet article décrit les alertes Microsoft Defender pour Identity qui sont émises quand des attaques faisant généralement partie des efforts de la phase de mouvement latéral sont détectées dans votre organisation.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 78d7a4d51459c5ea9099198e43097757ee2c588e
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847651"
---
# <a name="tutorial-lateral-movement-alerts"></a>Tutoriel : Alertes de mouvement latéral

En général, les cyberattaques sont lancées contre des entités accessibles, par exemple un utilisateur avec des privilèges peu élevés, puis rapidement, elles se déplacent latéralement jusqu’à ce que l’attaquant parvienne à accéder à des ressources importantes, comme des comptes sensibles, des administrateurs de domaine ou des données hautement sensibles. [!INCLUDE [Product long](includes/product-long.md)] identifie ces menaces avancées à la source tout au long de la chaîne d’annihilation des attaques et les classifie selon les phases suivantes :

1. [Reconnaissance](reconnaissance-alerts.md)
1. [Informations d’identification compromises](compromised-credentials-alerts.md)
1. **Mouvements latéraux**
1. [Dominance du domaine](domain-dominance-alerts.md)
1. [Exfiltration](exfiltration-alerts.md)

Pour en savoir plus sur la structure et les composants courants de toutes les alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)], consultez [Présentation des alertes de sécurité](understanding-security-alerts.md). Pour plus d’informations sur les **vrais positifs (TP)** , les **vrais positifs bénins (B-TP)** et les **faux positifs (FP)** , consultez [Classifications des alertes de sécurité](understanding-security-alerts.md#security-alert-classifications).

Les alertes de sécurité suivantes vous aident à identifier et à résoudre les activités suspectes de la phase **Mouvement latéral** détectées par [!INCLUDE [Product short](includes/product-short.md)] sur votre réseau. Dans ce tutoriel, vous allez apprendre à comprendre, classifier, prévenir et empêcher les types d’attaques suivants :

> [!div class="checklist"]
>
> - Exécution de code à distance sur DNS (ID externe 2036)
> - Suspicion d’usurpation d’identité (pass-the-hash) (ID externe 2017)
> - Suspicion d’usurpation d’identité (pass-the-ticket) (ID externe 2018)
> - Falsification de l’authentification NTLM suspectée (ID externe 2039)
> - Suspicion d’attaque de relais NTLM (compte Exchange) (ID externe 2037)
> - Suspicion d’attaque over-pass-the-hash (Kerberos) (ID externe 2002)
> - Utilisation présumée d’un certificat Kerberos non autorisé (ID externe 2047)
> - Manipulation présumée de paquet SMB (exploitation CVE-2020-0796) - (préversion) (ID externe 2406)

<!-- * Suspected overpass-the-hash attack (encryption downgrade) (external ID 2008)-->

## <a name="remote-code-execution-over-dns-external-id-2036"></a>Exécution de code à distance sur DNS (ID externe 2036)

**Description**

Le 11 décembre 2018, Microsoft a publié [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626), qui annonce qu’une vulnérabilité de l’exécution de code à distance a été découverte dans les serveurs DNS (Domain Name System) Windows. À cause d’elle, les serveurs ne parviennent pas à gérer correctement les demandes. Un attaquant qui parviendrait à exploiter cette faille pourrait exécuter du code dans le contexte du compte système Local. Les serveurs Windows actuellement configurés comme serveurs DNS y sont exposés.

Avec ce système de détection, une alerte de sécurité [!INCLUDE [Product short](includes/product-short.md)] est déclenchée quand des requêtes DNS suspectées d’exploiter la faille de sécurité CVE-2018-8626 sont effectuées sur un contrôleur de domaine dans le réseau.

**Période d’apprentissage**

Non applicable

**TP, B-TP ou FP**

1. Les ordinateurs de destination sont-ils à jour et possèdent-ils les correctifs nécessaires contre CVE-2018-8626 ?
    - Si c’est le cas, **fermez** l’alerte de sécurité comme **FP**.
1. Un service a-t-il été créé ou un processus inconnu exécuté au moment de l’attaque ?
    - Si vous ne trouvez aucun nouveau service ou processus inconnu, **fermez** l’alerte de sécurité comme **FP**.
1. Ce type d’attaque peut bloquer le service DNS avant de provoquer l’exécution de code.
    - Regardez si le service DNS a été redémarré plusieurs fois au moment de l’attaque.
    - Si c’est le cas, il s’agit probablement d’une tentative d’attaque CVE-2018-8626. Considérez cette alerte comme **TP** et suivez les instructions présentées dans **Comprendre l’étendue de la violation**.

**Comprendre l’étendue de la violation**

- Examinez les [ordinateurs sources et de destination](investigate-a-computer.md).

**Suggestions de correction et étapes préventives**

**Correction**

1. Incluez les contrôleurs de domaine.
    1. Empêchez la tentative d’exécution du code à distance.
    1. Recherchez les utilisateurs connectés au moment de l’activité suspecte, car ils risquent d’être également compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
1. Incluez l’ordinateur source.
    1. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    1. Recherchez les utilisateurs connectés au moment de l’activité suspecte, car ils risquent d’être également compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.

**Prévention**

- Vérifiez que tous les serveurs DNS de l’environnement sont à jour et possèdent les correctifs nécessaires contre [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626).

## <a name="suspected-identity-theft-pass-the-hash-external-id-2017"></a>Suspicion d’usurpation d’identité (pass-the-hash) (ID externe 2017)

*Nom précédent :* Usurpation d’identité par attaque Pass-the-Hash

**Description**

Pass-the-Hash est une technique de mouvement latéral par laquelle les attaquants volent le code de hachage NTLM d’un utilisateur sur un ordinateur et utilisent ensuite ce code pour accéder à un autre ordinateur.

**Période d’apprentissage**

Non applicable

**TP, B-TP ou FP ?**
1. Déterminez si le hachage a été utilisé à partir d’ordinateurs que l’utilisateur utilise régulièrement.
    - Si le hachage a été utilisé à partir d’ordinateurs utilisés régulièrement, **fermez** l’alerte comme s’agissant d’un **FP**.

**Comprendre l’étendue de la violation**

1. Examinez les [ordinateurs sources et de destination](investigate-a-computer.md) plus en détail.
1. Examinez l’[utilisateur compromis](investigate-a-computer.md).

**Suggestions de correction et étapes préventives**

1. Réinitialisez le mot de passe de l’utilisateur source et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
1. Contenez les ordinateurs sources et de destination.
1. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
1. Recherchez les utilisateurs connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.

## <a name="suspected-identity-theft-pass-the-ticket-external-id-2018"></a>Suspicion d’usurpation d’identité (pass-the-ticket) (ID externe 2018)

*Nom précédent :* Usurpation d’identité par attaque Pass-the-Ticket

**Description**

Pass-the-Ticket est une technique de mouvement latéral par laquelle les attaquants volent un ticket Kerberos sur un ordinateur et réutilisent ensuite ce ticket pour accéder à un autre ordinateur. Cette détection vérifie si un ticket Kerberos a été utilisé sur plusieurs ordinateurs différents.

**Période d’apprentissage**

Non applicable

**TP, B-TP ou FP ?**

La résolution correcte des adresses IP aux ordinateurs de l’organisation est essentielle pour identifier les attaques pass-the-ticket d’un ordinateur à un autre.

1. Vérifiez si l’adresse IP de l’un ou des deux ordinateurs appartient à un sous-réseau alloué à partir d’un pool DHCP de taille insuffisante, par exemple, VPN, VDI ou WiFi.
1. L’adresse IP est-elle partagée (par exemple, par un appareil NAT) ?
1. Le capteur ne résout-il pas une ou plusieurs des adresses IP de destination ? Si une adresse IP de destination n’est pas résolue, cela peut indiquer que les ports appropriés entre le capteur et les appareils ne sont pas ouverts correctement.

    Si la réponse à l’une des questions précédentes est **oui**, vérifiez si les ordinateurs sources et de destination sont identiques. S’ils sont identiques, il s’agit d’un **FP** et il n’y a eu aucune tentative réelle d’attaque **pass-the-ticket**.

La fonctionnalité [Credential Guard à distance](/windows/security/identity-protection/remote-credential-guard) des connexions RDP, quand elle est utilisée avec Windows 10 sur Windows Server 2016 et ultérieur, peut déclencher des alertes **B-TP**.
Utilisez la preuve d’alerte pour vérifier si l’utilisateur a établi une connexion Bureau à distance de l’ordinateur source à l’ordinateur de destination.

1. Recherchez la preuve de corrélation.
1. Si une preuve de corrélation existe, vérifiez si la connexion RDP a été établie avec Credential Guard à distance.
1. Si la réponse est oui, **fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP**.

Il existe des applications personnalisées qui transfèrent des tickets pour le compte d’utilisateurs. Ces applications ont des droits de délégation pour les tickets de l’utilisateur.

1. Un type d’application personnalisée telle que celle décrite plus haut est-il actuellement présent sur les ordinateurs de destination ? Quels services l’application exécute-t-elle ? Les services agissent-ils au nom des utilisateurs, par exemple pour accéder à des bases de données ?
    - Si la réponse est oui, **fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP**.
1. L’ordinateur de destination est-il un serveur de délégation ?
    - Si la réponse est oui, **fermez** l’alerte de sécurité et excluez cet ordinateur comme s’agissant d’une activité **T-BP**.

**Comprendre l’étendue de la violation**

1. Examinez les [ordinateurs sources et de destination](investigate-a-computer.md).
1. Examinez l’[utilisateur compromis](investigate-a-computer.md).

**Suggestions de correction et étapes préventives**

1. Réinitialisez le mot de passe de l’utilisateur source et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
1. Contenez les ordinateurs sources et de destination.
1. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
1. Recherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
1. Si vous avez installé Microsoft Defender pour point de terminaison, utilisez **klist.exe purge** pour supprimer tous les tickets de la session spécifiée et empêcher toute utilisation ultérieure des tickets.

## <a name="suspected-ntlm-authentication-tampering-external-id-2039"></a>Falsification de l’authentification NTLM suspectée (ID externe 2039)

En juin 2019, Microsoft a publié la [vulnérabilité de sécurité CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040), annonçant la découverte d’une nouvelle vulnérabilité de falsification dans Microsoft Windows, quand une attaque de l’intercepteur (« man in the middle ») est en mesure de contourner la protection de la vérification de l’intégrité des messages (MIC) NTLM.

Les acteurs malveillants qui exploitent correctement cette vulnérabilité ont la possibilité de rétrograder les fonctionnalités de sécurité NTLM et peuvent parvenir à créer des sessions authentifiées pour le compte d’autres comptes. Les serveurs Windows auxquels ce correctif n’est pas appliqué sont exposés à cette vulnérabilité.

Dans cette détection, une alerte de sécurité [!INCLUDE [Product short](includes/product-short.md)] est déclenchée quand des demandes d’authentification NTLM suspectées d’exploiter la vulnérabilité de sécurité identifiée dans [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) sont effectuées sur un contrôleur de domaine dans le réseau.

**Période d’apprentissage**

Non applicable

**TP, B-TP ou FP ?**

1. Les ordinateurs concernés, notamment les contrôleurs de domaine, sont-ils à jour et corrigés par rapport à [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) ?
    - Si les ordinateurs sont à jour et corrigés, l’authentification devrait selon nous échouer. Si l’authentification a échoué, **fermez** l’alerte de sécurité en tant que tentative ayant échoué.

**Comprendre l’étendue de la violation**

1. Examinez les [ordinateurs sources](investigate-a-computer.md).
1. Examinez le [compte source](investigate-a-user.md).

**Suggestions de correction et étapes préventives**

**Correction**

1. Inclure les ordinateurs sources
1. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
1. Recherchez les utilisateurs connectés à peu près au même moment que l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
1. Forcez l’utilisation de NTLMv2 « sealed » dans le domaine, en utilisant la stratégie de groupe **Sécurité réseau : niveau d’authentification LAN Manager**. Pour plus d’informations, consultez [Instructions pour le niveau d’authentification LAN Manager](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) afin de définir la stratégie de groupe pour les contrôleurs de domaine.

**Prévention**

- Vérifiez que tous les appareils de l’environnement sont à jour et ont les correctifs nécessaires contre [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040).

## <a name="suspected-ntlm-relay-attack-exchange-account-external-id-2037"></a>Suspicion d’attaque de relais NTLM (compte Exchange) (ID externe 2037)

**Description**

Un serveur Exchange peut être configuré pour déclencher l’authentification NTLM avec le compte Exchange Server auprès d’un serveur HTTP distant exécuté par un attaquant. Le serveur attend que la communication du serveur Exchange relaie sa propre authentification sensible auprès de n’importe quel autre serveur ou, plus intéressant encore, auprès de l’annuaire Active Directory via LDAP, et s’empare des informations d’authentification.

Une fois que le serveur relais reçoit l’authentification NTLM, il fournit une demande qui a été créée à l’origine par le serveur cible. Le client répond à la demande, empêchant un attaquant de prendre la réponse et de l’utiliser pour continuer la demande NTLM avec le contrôleur de domaine cible.

Dans cette détection, une alerte est déclenchée quand [!INCLUDE [Product short](includes/product-short.md)] identifie une utilisation des informations d’identification du compte Exchange à partir d’une source suspecte.

**Période d’apprentissage**

Non applicable

**TP, B-TP ou FP ?**

1. Vérifiez les ordinateurs sources derrière les adresses IP.
    1. Si l’ordinateur source est un serveur Exchange, **fermez** l’alerte de sécurité en tant qu’activité **FP** (Faux positif).
    1. Déterminer si le compte source doit s’authentifier avec NTLM à partir de ces ordinateurs ? S’ils doivent s’authentifier, **fermez** l’alerte de sécurité et excluez ces ordinateurs en tant qu’activité **B-TP** (Vrai positif bénin).

**Comprendre l’étendue de la violation**

1. Continuez [l’examen des ordinateurs sources](investigate-a-computer.md) derrière les adresses IP impliquées.
1. Examinez le [compte source](investigate-a-user.md).

**Suggestions de correction et étapes préventives**

1. Inclure les ordinateurs sources
    1. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    1. Recherchez les utilisateurs connectés à peu près au même moment que l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
1. Forcez l’utilisation de NTLMv2 « sealed » dans le domaine, en utilisant la stratégie de groupe **Sécurité réseau : niveau d’authentification LAN Manager**. Pour plus d’informations, consultez [Instructions pour le niveau d’authentification LAN Manager](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) afin de définir la stratégie de groupe pour les contrôleurs de domaine.

<!--
## Suspected overpass-the-hash attack (encryption downgrade) (external ID 2008)

*Previous name:* Encryption downgrade activity

**Description**

Encryption downgrade is a method of weakening Kerberos using encryption downgrade of different fields of the protocol, normally encrypted using the highest levels of encryption. A weakened encrypted field can be an easier target to offline brute force attempts. Various attack methods utilize weak Kerberos encryption cyphers. In this detection, [!INCLUDE [Product short](includes/product-short.md)] learns the Kerberos encryption types used by computers and users, and alerts you when a weaker cypher is used that is unusual for the source computer, and/or user, and matches known attack techniques.

In an over-pass-the-hash attack, an attacker can use a weak stolen hash to create a strong ticket, with a Kerberos AS request. In this detection,  instances are detected where the AS_REQ message encryption type from the source computer is downgraded, when compared to the previously learned behavior (the computer used AES).

**Learning period**

Not applicable

**TP, B-TP, or FP?**

1. Determine if the smartcard configuration recently changed.
    - Did the accounts involved recently have smartcard configurations changes?

      If the answer is yes, **Close** the security alert as a **T-BP** activity.

Some legitimate resources don't support strong encryption ciphers and may trigger this alert.

1. Do all source users share something?
    1. For example, are all of your marketing personnel accessing a specific resource that could cause the alert to be triggered?
    1. Check the resources accessed by those tickets.
       - Check this in Active Directory by checking the attribute *msDS-SupportedEncryptionTypes*, of the resource service account.
    1. If there is only one accessed resource, check if it is a valid resource for these users to access.

      If the answer to one of the previous questions is **yes**, it is likely to be a **T-BP** activity. Check if the resource can support a strong encryption cipher, implement a stronger encryption cipher where possible, and **Close** the security alert.

**Understand the scope of the breach**

1. Investigate the [source computer](investigate-a-computer.md).
1. Investigate the [compromised user](investigate-a-computer.md).

**Suggested remediation and steps for prevention**

**Remediation**

1. Reset the password of the source user and enable MFA or, if you have configured the relevant high-risk user policies in Azure Active Directory Identity Protection, you can use the [**Confirm user compromised**](/cloud-app-security/accounts#governance-actions) action in the Cloud App Security portal.
1. Contain the source computer.
1. Find the tool that performed the attack and remove it.
1. Look for users logged on around the time of the activity, as they may also be compromised. Reset their passwords and enable MFA or, if you have configured the relevant high-risk user policies in Azure Active Directory Identity Protection, you can use the [**Confirm user compromised**](/cloud-app-security/accounts#governance-actions) action in the Cloud App Security portal.

**Prevention**

1. Configure your domain to support strong encryption cyphers, and remove *Use Kerberos DES encryption types*. Learn more about [encryption types and Kerberos](/archive/blogs/openspecification/windows-configurations-for-kerberos-supported-encryption-type).
1. Make sure the domain functional level is set to support strong encryption cyphers.
1. Give preference to using applications that support strong encryption cyphers.
-->

## <a name="suspected-overpass-the-hash-attack-kerberos-external-id-2002"></a>Suspicion d’attaque over-pass-the-hash (Kerberos) (ID externe 2002)

*Nom précédent :* Implémentation inhabituelle du protocole Kerberos (attaque overpass-the-hash potentielle)

**Description**

Les attaquants utilisent des outils qui implémentent différents protocoles, tels que Kerberos et SMB, de façon inhabituelle. Bien que Microsoft Windows accepte ce type de trafic réseau sans avertissement, [!INCLUDE [Product short](includes/product-short.md)] est capable de reconnaître une intention potentiellement malveillante. Le comportement est révélateur de certaines techniques comme Over-Pass-the-Hash, la Force Brute, ainsi que l’exploitation des failles de sécurité par de puissants ransomwares tels que WannaCry.

**Période d’apprentissage**

Non applicable

**TP, B-TP ou FP ?**

Parfois, les applications implémentent leur propre pile Kerberos, mais pas conformément à la RFC Kerberos.

1. Vérifiez si l’ordinateur source exécute une application avec sa propre pile Kerberos, de manière non conforme à la RFC Kerberos.
1. Si l’ordinateur source exécute une telle application alors qu’il ne doit **pas** le faire, corrigez la configuration de l’application. **Fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP**.
1. Si l’ordinateur source exécute une telle application et qu’il doit continuer à le faire, **fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP** et excluez l’ordinateur.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).
1. S’il y a un [utilisateur source](investigate-a-user.md), procédez à une investigation.

**Suggestions de correction et étapes préventives**

1. Réinitialisez les mots de passe des utilisateurs compromis et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
1. Incluez l’ordinateur source.
1. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
1. Recherchez les utilisateurs connectés aux environs de l’heure de l’activité suspecte, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
1. Réinitialisez les mots de passe de l’utilisateur source et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.

<!-- REMOVE BOOKMARK FROM TITLE WHEN PREVIEW REMOVED -->

<a name="suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406"></a>

## <a name="suspected-rogue-kerberos-certificate-usage-external-id-2047"></a>Utilisation présumée d’un certificat Kerberos non autorisé (ID externe 2047)

**Description**

L’attaque par certificat non autorisé est une technique de persistance utilisée par les attaquants une fois qu’ils ont pris le contrôle de l’organisation. Les attaquants compromettent le serveur de l’autorité de certification et génèrent des certificats qui pourront être utilisés comme des comptes de porte dérobée lors d’attaques ultérieures.

**Période d’apprentissage**

Non applicable

**TP, B-TP ou FP**

- Déterminer si le compte se connecte régulièrement à l’ordinateur
  - Si le certificat est régulièrement utilisé sur des ordinateurs, **fermez** l’alerte comme en la signalant comme un faux positif (**FP**).

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).
2. Examinez l’[utilisateur source](investigate-a-user.md).
3. Vérifiez les ressources qui ont fait l’objet d’un accès réussi et [investiguez](investigate-a-computer.md).

**Suggestions de correction et étapes préventives**

1. Réinitialisez le mot de passe de l’utilisateur source et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
1. Incluez l’ordinateur source.
    - Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    - Recherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
1. Recherchez le certificat utilisé sur le serveur de l’autorité de certification et révoquez le certificat en invalidant le protocole TLS/SSL avant sa date d’expiration planifiée.

## <a name="suspected-smb-packet-manipulation-cve-2020-0796-exploitation---preview-external-id-2406"></a>Manipulation présumée de paquet SMB (exploitation CVE-2020-0796) - (préversion) (ID externe 2406)

**Description**

12/03/2020 Microsoft a publié [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796) pour annoncer qu’une nouvelle vulnérabilité d’exécution de code à distance existe dans la façon dont le protocole Microsoft SMBv3 (Server Message Block 3.1.1) gère certaines requêtes. Un attaquant qui parviendrait à exploiter la vulnérabilité pourrait être en mesure d’exécuter du code sur le client ou le serveur cible. Les serveurs Windows auxquels ce correctif n’est pas appliqué sont exposés à cette vulnérabilité.

Avec ce système de détection, une alerte de sécurité [!INCLUDE [Product short](includes/product-short.md)] est déclenchée quand des paquets SMBv3 suspectées d’exploiter la faille de sécurité CVE-2020-0796 sont effectuées sur un contrôleur de domaine dans le réseau.

**Période d’apprentissage**

Non applicable

**TP, B-TP ou FP ?**

1. Les contrôleurs de domaine concernés sont-ils à jour et corrigés par rapport à CVE-2020-0796 ?
    - Si les ordinateurs sont à jour et corrigés, l’attaque devrait selon nous échouer, **fermez** l’alerte de sécurité en la marquant comme tentative en échec.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).
1. Investiguez le contrôleur de domaine de destination.

**Suggestions de correction et étapes préventives**

**Correction**

1. Incluez l’ordinateur source.
1. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
1. Recherchez les utilisateurs connectés aux environs de l’heure de l’activité suspecte, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
1. Si vous avez des ordinateurs équipés de systèmes d’exploitation qui ne prennent pas en charge [KB4551762](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4551762), nous vous recommandons de désactiver la fonctionnalité de compression SMBv3 dans l’environnement, comme décrit dans la section [Solutions de contournement](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796).

**Prévention**

1. Vérifiez que tous les appareils de l’environnement sont à jour et corrigés par rapport à [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796).

> [!div class="nextstepaction"]
> [Tutoriel sur les alertes de dominance du domaine](domain-dominance-alerts.md)

## <a name="see-also"></a>Voir aussi

- [Examiner un ordinateur](investigate-a-computer.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Utilisation des chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Alertes de reconnaissance](reconnaissance-alerts.md)
- [Alertes indiquant des informations d’identification compromises](compromised-credentials-alerts.md)
- [Alertes de dominance du domaine](domain-dominance-alerts.md)
- [Alertes d’exfiltration](exfiltration-alerts.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
