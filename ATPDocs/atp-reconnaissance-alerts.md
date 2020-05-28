---
title: Alertes de sécurité de la phase de reconnaissance Azure ATP
description: Cet article décrit les alertes Azure ATP émises quand des attaques faisant généralement partie des efforts de la phase de reconnaissance sont détectées contre votre organisation.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 03/01/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 800cb9aea336c09d3e3591062faa420546822914
ms.sourcegitcommit: 3162130a85b5c6e8bf16456f8255b95e1f52b869
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2020
ms.locfileid: "83825271"
---
# <a name="tutorial-reconnaissance-alerts"></a>Tutoriel : Alertes de reconnaissance

En général, les cyberattaques sont lancées contre des entités accessibles, par exemple un utilisateur avec des privilèges peu élevés, puis rapidement, elles se déplacent latéralement jusqu’à ce que l’attaquant parvienne à accéder à des ressources importantes, comme des comptes sensibles, des administrateurs de domaine ou des données hautement sensibles. Azure ATP identifie ces menaces avancées à la source tout au long de la chaîne d’annihilation des attaques et les classifie selon les phases suivantes :

1. **Reconnaissance**
2. [Informations d’identification compromises](atp-compromised-credentials-alerts.md)
3. [Mouvements latéraux](atp-lateral-movement-alerts.md)
4. [Dominance du domaine](atp-domain-dominance-alerts.md)
5. [Exfiltration](atp-exfiltration-alerts.md)

Pour en savoir plus sur la structure et les composants courants de toutes les alertes de sécurité Azure ATP, consultez [Présentation des alertes de sécurité](understanding-security-alerts.md).

Les alertes de sécurité suivantes vous aident à identifier et à résoudre les activités suspectes de la phase **Reconnaissance** détectées par Azure ATP sur votre réseau.

Dans ce tutoriel, vous allez apprendre à comprendre, classifier, prévenir et pallier aux types d’attaques suivants :

> [!div class="checklist"]
>
> * Reconnaissance d’énumération de compte (ID externe 2003)
> * Reconnaissance de mappage de réseau (DNS) (ID externe 2007)
> * Reconnaissance de principal de sécurité (LDAP) (ID externe 2038)
> * Reconnaissance des utilisateurs et des adresses IP (SMB) (ID externe 2012)
> * Reconnaissance des utilisateurs et des membres d’un groupe (SAMR) (ID externe 2021)

## <a name="account-enumeration-reconnaissance-external-id-2003"></a>Reconnaissance d’énumération de compte (ID externe 2003)

*Nom précédent :* Reconnaissance à l’aide de l’énumération de compte

**Description**

Lors d’une reconnaissance à l’aide de l’énumération de comptes, un attaquant utilise un dictionnaire contenant des milliers de noms d’utilisateurs ou des outils comme KrbGuess afin d’essayer de deviner des noms d’utilisateur dans le domaine.

**Kerberos** : L’attaquant effectue des requêtes Kerberos avec ces noms pour tenter de trouver un nom d’utilisateur valide dans le domaine. Quand l’attaquant parvient à deviner un nom d’utilisateur, il obtient la **Pré-authentification requise** au lieu de l’erreur Kerberos **Principal de sécurité inconnu**.

**NTLM** : L’attaquant effectue des requêtes d’authentification NTLM avec l’annuaire de noms pour tenter de trouver un nom d’utilisateur valide dans le domaine. Quand l’attaquant parvient à deviner un nom d’utilisateur, il obtient **WrongPassword (0xc000006a)** au lieu de l’erreur NTLM **NoSuchUser (0xc0000064)** .

Dans le cadre de cette détection d’alerte, Azure ATP détecte d’où provient l’attaque par énumération de comptes, le nombre total de tentatives et combien ont abouti. Si le nombre d’utilisateurs inconnus est trop élevé, Azure ATP détecte cela comme une activité suspecte.

**TP, B-TP ou FP**

Certains serveurs et applications interrogent les contrôleurs de domaine pour déterminer si des comptes existent dans des scénarios d’utilisation légitime.

Pour déterminer si cette requête était un **FP**, **BTP** ou **FP**, cliquez sur l’alerte pour accéder à sa page de détails :

1. Vérifiez si l’ordinateur source était censé effectuer ce type de requête. Dans ce cas, un **B-TP** pourrait être dû à des systèmes de ressources humaines ou à des serveurs Microsoft Exchange.

2. Vérifiez les domaines des comptes.
    - Voyez-vous des utilisateurs supplémentaires qui appartiennent à un autre domaine ?  
     Une erreur de configuration de serveur (par exemple dans Exchange/Skype ou ADSF) peut faire apparaître des utilisateurs supplémentaires qui appartiennent à différents domaines.
    - Examinez la configuration du service à problème afin de corriger l’erreur de configuration.

    Si vous avez répondu **oui** aux questions ci-dessus, il s’agit d’une activité **B-TP**. *Fermez* l’alerte de sécurité.

En guise d’étape suivante, examinez l’ordinateur source :

1. Est-ce qu’un script ou une application s’exécutant sur l’ordinateur source pourrait générer ce comportement ?
    - S’agit-il d’un ancien script exécuté avec d’anciennes informations d’identification ?  
    Si oui, arrêtez et modifiez ou supprimez le script.
    - S’agit-il d’un script ou d’une application d’administration ou de sécurité censé(e) s’exécuter dans l’environnement ?

      Si vous avez répondu **oui** à la question précédente, *fermez* l’alerte de sécurité et excluez cet ordinateur. Il s’agit probablement d’une activité **B-TP**.

À présent, examinez les comptes :

Les attaquants utilisent généralement un dictionnaire de noms de comptes aléatoires pour rechercher des noms de comptes existants dans une organisation.

1. Les comptes inexistants vous disent-ils quelque chose ?
    - Si les comptes inexistants vous semblent familiers, il s’agit peut-être de comptes désactivés ou appartenant à des employés ayant quitté l’entreprise.
    - Recherchez une application ou un script qui vérifie quels comptes existent toujours dans Active Directory.

      Si vous avez répondu **oui** à l’une des questions précédentes, *fermez* l’alerte de sécurité. Il s’agit probablement d’une activité **B-TP**.

2. Si des tentatives correspondent à des noms de compte existants, l’attaquant connaît l’existence de comptes dans votre environnement et peut essayer d’utiliser des attaques par force brute pour accéder à votre domaine en utilisant les noms d’utilisateur découverts.
    - Vérifiez les noms de compte trouvés en recherchant d’autres activités suspectes.
    - Regardez si des comptes sensibles se trouvent parmi les comptes trouvés.

### <a name="understand-the-scope-of-the-breach"></a>Comprendre l’étendue de la violation

1. Examinez l’ordinateur source
1. Si des tentatives correspondent à des noms de comptes existants, l’attaquant connaît l’existence de comptes dans votre environnement et peut utiliser des attaques par force brute pour essayer d’accéder à votre domaine en utilisant les noms d’utilisateur découverts. Examinez les comptes existants en suivant le [guide d’investigation sur les utilisateurs](investigate-a-user.md).
    > [!NOTE]
    > Examinez les preuves pour déterminer le protocole d’authentification utilisé. Si l’authentification NTLM a été utilisée, activez l’audit NTLM de l’événement Windows 8004 sur le contrôleur de domaine pour déterminer le serveur de ressources auquel les utilisateurs ont tenté d’accéder.  
    > L’événement Windows 8004 est l’événement d’authentification NTLM qui inclut des informations sur l’ordinateur source, le compte d’utilisateur et le serveur auquel le compte d'utilisateur a essayé d’accéder.  
    > Azure ATP capture les données de l’ordinateur source suivant l’événement Windows 4776, qui contient le nom de l’ordinateur source défini par l’ordinateur. À l’aide de l’événement Windows 4776 pour capturer ces informations, le champ source des informations est parfois remplacé par l’appareil ou le logiciel et affiche uniquement Poste de travail ou MSTSC comme source d’informations. En outre, l’ordinateur source n’est peut-être pas réellement présent sur votre réseau. Cela est possible, car les malfaiteurs ciblent communément les serveurs ouverts accessibles sur Internet à partir de l’extérieur du réseau, puis l’utilisent pour énumérer vos utilisateurs. Si vous avez fréquemment des appareils qui s’affichent comme Poste de travail ou MSTSC, veillez à activer l’audit NTLM sur les contrôleurs de domaine pour obtenir le nom du serveur de ressources. Vous devez également examiner ce serveur, vérifier s’il est ouvert sur Internet et, si possible, le fermer.

1. Une fois que vous savez quel serveur a envoyé la validation de l’authentification, examinez-le en vérifiant ses événements, par exemple l’événement Windows 4624, pour mieux comprendre le processus d’authentification.

1. Regardez si ce serveur est exposé à Internet avec des ports ouverts. Par exemple, est-il ouvert à Internet avec le protocole RDP ?

### <a name="suggested-remediation-and-steps-for-prevention"></a>Suggestions de correction et étapes préventives

1. Contenez l’[ordinateur source](investigate-a-computer.md).
    1. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    1. Recherchez les utilisateurs qui étaient connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis.
    1. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
1. Appliquez des [mots de passe complexes et longs](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) dans l’organisation. Les mots de passe longs et complexes assurent le niveau minimal de sécurité nécessaire contre les attaques par force brute. Les attaques par force brute sont généralement l’étape qui suit l’énumération dans la chaîne de destruction de cyber-attaque.

## <a name="network-mapping-reconnaissance-dns-external-id-2007"></a>Reconnaissance de mappage de réseau (DNS) (ID externe 2007)

*Nom précédent :* Reconnaissance à l’aide de DNS

**Description**

Votre serveur DNS contient une carte de l’ensemble des ordinateurs, adresses IP et services de votre réseau. Ces informations sont utilisées par les attaquants pour mapper la structure de votre réseau et cibler les ordinateurs intéressants pour les étapes suivantes de l’attaque.

Il existe plusieurs types de requêtes dans le protocole DNS. Cette alerte de sécurité Azure ATP détecte les requêtes suspectes, soit les requêtes utilisant un AXFR (transfert) provenant de serveurs non DNS, soit les requêtes utilisant un nombre excessif de requêtes.

**Période d’apprentissage**

Cette alerte a une période d’apprentissage de 8 jours à partir du début de l’analyse du contrôleur de domaine.

**TP, B-TP ou FP**

1. Vérifiez si l’ordinateur source est un serveur DNS.

    - Si l’ordinateur source **est** un serveur DNS, fermez l’alerte de sécurité comme s’agissant d’un **FP**.
    - Pour empêcher tout **FP** ultérieur, vérifiez que le port UDP 53 est **ouvert** entre le capteur Azure ATP et l’ordinateur source.

Les scanners de sécurité et les applications légitimes peuvent générer des requêtes DNS.

1. Vérifiez si cet ordinateur source est censé générer ce type d’activité.

    - Si cet ordinateur source est censé générer ce type d’activité, **fermez** l’alerte de sécurité en tant qu’activité **B-TP** et excluez l’ordinateur.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).

**Suggestions de correction et étapes préventives**

**Correction :**

- Incluez l’ordinateur source.
    - Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    - Recherchez les utilisateurs qui étaient connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.

**Prévention :**

Il est important de prévenir toute attaque ultérieure à l’aide de requêtes AXFR en sécurisant votre serveur DNS interne.

- Sécurisez votre serveur DNS interne pour éviter la reconnaissance à l’aide de DNS en désactivant les transferts de zone ou en [limitant les transferts de zone](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)) uniquement aux adresses IP spécifiées. La modification des transferts de zone est l’une des tâches de la liste de contrôle que vous devez suivre pour [sécuriser vos serveurs DNS contre les attaques internes et externes](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)).

## <a name="security-principal-reconnaissance-ldap-external-id-2038"></a>Reconnaissance de principal de sécurité (LDAP) (ID externe 2038)

**Description**

La reconnaissance de principal de sécurité est utilisée par les attaquants pour obtenir des informations critiques sur l’environnement de domaine. Informations qui aident les attaquants à mapper la structure de domaine et à identifier des comptes privilégiés pour une utilisation dans les étapes ultérieures de leur chaîne d’attaque. Le protocole LDAP est l’une des méthodes les plus populaires utilisées à des fins légitimes et malveillantes pour interroger Active Directory.  La reconnaissance de principal de sécurité basée sur LDAP est couramment utilisée en tant que première phase d’une attaque Kerberoasting. Les attaques Kerberoasting sont utilisées pour obtenir la liste cible des noms de principal de sécurité (SPN), pour lesquels les attaquants tentent ensuite d’obtenir des tickets TGS (Ticket Granting Server).

Afin de permettre à Azure ATP de dresser avec précision le profil et d’apprendre les utilisateurs légitimes, aucune alerte de ce type n’est déclenchée dans les 10 premiers jours suivant le déploiement d’Azure ATP. Une fois que la phase d’apprentissage initiale d’Azure ATP est terminée, les alertes sont générées sur les ordinateurs qui effectuent des requêtes d’énumération LDAP suspectes ou des requêtes ciblant des groupes sensibles à l’aide de méthodes jamais observées auparavant.

**Période d’apprentissage**

15 jours par ordinateur à partir du jour du premier événement, observé à partir de l’ordinateur.

**TP, B-TP ou FP**

1. Cliquez sur l’ordinateur source pour accéder à sa page de profil.
    1. Cet ordinateur source est-il censé générer cette activité ?
    2. Si l’ordinateur et l’activité sont tels qu’attendus, **fermez** l’alerte de sécurité et excluez cet ordinateur comme s’agissant d’une activité **B-TP**.

**Comprendre l’étendue de la violation**

1. Vérifiez les requêtes qui ont été effectuées (par exemple, Administrateurs du domaine ou tous les utilisateurs d’un domaine) et déterminez si les requêtes ont réussi. Examinez chaque groupe exposé, recherchez les activités suspectes effectuées sur le groupe, ou par des utilisateurs membres du groupe.
2. Examinez l’[ordinateur source](investigate-a-computer.md).
    - Les requêtes LDAP vous permettent de vérifier si une activité d’accès à une ressource s’est produite sur l’un des noms SPN exposés.

**Suggestions de correction et étapes préventives**

1. Incluez l’ordinateur source.
    1. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    2. L’ordinateur exécute-t-il un outil d’analyse qui effectue une variété de requêtes LDAP ?
    3. Recherchez les utilisateurs connectés à peu près au même moment que l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
2. Réinitialisez le mot de passe si l’accès à la ressource SPN a été effectuée et s’exécute sous un compte utilisateur (pas le compte machine).

**Suggestions d’étapes Kerberoasting spécifiques pour la prévention et la correction**

1. Réinitialisez les mots de passe des utilisateurs compromis et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
2. Exiger l’utilisation de [mots de passe longs et complexes pour les utilisateurs disposant d’un compte de principal du service](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/minimum-password-length).
3. [Remplacer le compte d’utilisateur par un compte de service administré de groupe (gMSA)](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).

> [!NOTE]
> Les alertes de reconnaissance du principal de sécurité (LDAP) sont prises en charge uniquement par les capteurs ATP.

## <a name="user-and-ip-address-reconnaissance-smb-external-id-2012"></a>Reconnaissance des utilisateurs et des adresses IP (SMB) (ID externe 2012)

*Nom précédent :* Reconnaissance à l’aide de l’énumération de sessions SMB

### <a name="description"></a>Description

L’énumération à l’aide du protocole SMB (Server Message Block) permet aux attaquants d’obtenir des informations sur les emplacements de connexion récents des utilisateurs. Une fois qu’ils connaissent ces informations, les attaquants peuvent se déplacer de façon latérale dans le réseau pour accéder à un compte sensible spécifique.

Dans cette détection, une alerte est déclenchée quand une énumération de sessions SMB est effectuée sur un contrôleur de domaine.

**TP, B-TP ou FP**

Les applications et les scanners de sécurité sont susceptibles d’interroger légitimement des contrôleurs de domaine pour les sessions SMB ouvertes.

1. Cet ordinateur source est-il censé générer des activités de ce type ?
2. L’ordinateur source exécute-t-il un scanner de sécurité ?
    Si la réponse est oui, il s’agit probablement d’une activité B-TP. *Fermez* l’alerte de sécurité et excluez cet ordinateur.
3. Vérifiez l’identité des utilisateurs qui ont effectué l’opération.
    Ces utilisateurs sont-ils censés effectuer ces actions ?
    Si la réponse est oui, *fermez* l’alerte de sécurité comme s’agissant d’une activité B-TP.

**Comprendre l’étendue de la violation**

1. Examinez l’ordinateur source.
2. Dans la page d’alerte, vérifiez si des utilisateurs sont exposés. Pour examiner plus en détail chaque utilisateur exposé, vérifiez son profil. Nous vous recommandons de commencer votre investigation par les utilisateurs sensibles et de priorité élevée.

**Suggestions de correction et étapes préventives**

Utilisez [l’outil Net Cease](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) pour renforcer la protection de votre environnement contre cette attaque.

## <a name="user-and-group-membership-reconnaissance-samr-external-id-2021"></a>Reconnaissance des utilisateurs et des membres d’un groupe (SAMR) (ID externe 2021)

*Nom précédent :* Reconnaissance à l’aide de requêtes de services d’annuaire

**Description**

La reconnaissance des utilisateurs et des membres d’un groupe permet aux attaquants de mapper la structure d’annuaire et de cibler des comptes privilégiés pour les étapes suivantes de leur attaque. Le protocole SAM-R (Security Account Manager Remote) est l’une des méthodes utilisées pour interroger l’annuaire et effectuer ce type de mappage.
Dans le cadre de cette détection, aucune alerte n’est déclenchée durant le premier mois après le déploiement d’Azure ATP (période d’apprentissage). Pendant cette période d’apprentissage, Azure ATP effectue un profilage des requêtes SAM-R effectuées à partir des ordinateurs, qu’il s’agisse de requêtes d’énumération ou de requêtes individuelles sur des comptes sensibles.

**Période d’apprentissage**

Quatre semaines par contrôleur de domaine à partir de la première activité réseau SAMR sur le contrôleur de domaine en question.

**TP, B-TP ou FP**

1. Cliquez sur l’ordinateur source pour accéder à sa page de profil.
    - L’ordinateur source est-il censé générer des activités de ce type ?
      - Si oui, *fermez* l’alerte de sécurité et excluez cet ordinateur comme s’agissant d’une activité **B-TP**.
    - Vérifiez l’identité des utilisateurs qui ont effectué l’opération.
      - Ces utilisateurs se connectent-ils normalement à cet ordinateur source, ou s’agit-il d’administrateurs autorisés à effectuer ces actions spécifiques ?
    - Vérifiez le profil des utilisateurs et leurs activités. Identifiez leur comportement d’utilisateur normal et recherchez d’autres activités suspectes à l’aide du [guide d’investigation sur les utilisateurs](investigate-a-user.md).

      Si vous avez répondu **oui** à la question ci-dessus, *fermez* l’alerte comme s’agissant d’une activité **B-TP**.

**Comprendre l’étendue de la violation**

1. Examinez les requêtes qui ont été effectuées, par exemple les requêtes Administrateur entreprise ou Administrateur, et déterminez si elles ont réussi.
2. Examinez chaque utilisateur exposé à l’aide du guide d’investigation de l’utilisateur.
3. Examinez l’ordinateur source.

**Suggestions de correction et étapes préventives**

1. Incluez l’ordinateur source.
2. Trouvez et supprimez l’outil qui a effectué l’attaque.
3. Recherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
4. Réinitialisez le mot de passe de l’utilisateur source et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
5. Appliquez l’accès réseau et limitez les clients autorisés à effectuer des appels distants à l’aide de la stratégie de groupe SAM.

> [!NOTE]
> Pour désactiver une alerte de sécurité Azure ATP, contactez le support technique.

> [!div class="nextstepaction"]
> [Tutoriel sur les alertes indiquant des informations d’identification compromises](atp-compromised-credentials-alerts.md)

## <a name="see-also"></a>Voir aussi

- [Examiner un ordinateur](investigate-a-computer.md)
- [Examiner un utilisateur](investigate-a-user.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Alertes indiquant des informations d’identification compromises](atp-compromised-credentials-alerts.md)
- [Alertes de mouvement latéral](atp-lateral-movement-alerts.md)
- [Alertes de dominance du domaine](atp-domain-dominance-alerts.md)
- [Alertes d’exfiltration](atp-exfiltration-alerts.md)
- [Informations de référence sur le journal SIEM Azure ATP](cef-format-sa.md)
- [Utilisation des chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
