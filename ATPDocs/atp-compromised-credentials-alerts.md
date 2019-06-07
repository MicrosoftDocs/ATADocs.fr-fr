---
title: Alertes de sécurité Azure ATP indiquant des informations d’identification compromises | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typical of the compromised credentials phase are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 05/30/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6e55ebfaeac540d15a8539ee2c5b1450ee0c3f10
ms.sourcegitcommit: b021f8dfc54e59de429f93cc5fc0d733d92b00b8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403556"
---
# <a name="tutorial-compromised-credential-alerts"></a>Tutoriel : Alertes indiquant des informations d’identification compromises  

En général, les cyberattaques sont lancées contre des entités accessibles, par exemple un utilisateur avec des privilèges peu élevés, puis rapidement, elles se déplacent latéralement jusqu’à ce que l’attaquant parvienne à accéder à des ressources importantes, comme des comptes sensibles, des administrateurs de domaine et des données hautement sensibles. Azure ATP identifie ces menaces avancées à la source tout au long de la chaîne d’annihilation des attaques et les classifie selon les phases suivantes :

1. [Reconnaissance](atp-reconnaissance-alerts.md)
2. **Informations d’identification compromises**
3. [Déplacements latéraux](atp-lateral-movement-alerts.md)
4. [Dominance du domaine](atp-domain-dominance-alerts.md)
5. [Exfiltration](atp-exfiltration-alerts.md) 

Pour en savoir plus sur la structure et les composants courants de toutes les alertes de sécurité Azure ATP, consultez [Présentation des alertes de sécurité](understanding-security-alerts.md).

Les alertes de sécurité suivantes vous aident à identifier et à résoudre les activités suspectes de la phase **Informations d’identification compromises** détectées par Azure ATP sur votre réseau. Dans ce tutoriel, vous allez apprendre à comprendre, classifier, prévenir et empêcher les types d’attaques suivants :

> [!div class="checklist"]
> * Activité Honeytoken (ID externe 2014)
> * Suspicion d’attaque par force brute (Kerberos, NTLM) (ID externe 2023)
> * Suspicion d’attaque par force brute (LDAP) (ID externe 2004)
> * Suspicion d’attaque par force brute (SMB) (ID externe 2033)
> * Suspicion d’attaque de ransomware WannaCry (ID externe 2035)
> * Suspicion d’utilisation du framework de piratage Metasploit (ID externe 2034)
> * Connexion VPN suspecte (ID externe 2025)

## <a name="honeytoken-activity-external-id-2014"></a>Activité Honeytoken (ID externe 2014) 

*Nom précédent :* Activité Honeytoken

**Description**

Les comptes Honeytoken sont des comptes servant de leurre pour identifier et suivre l’activité malveillante qui implique ces comptes. Les comptes Honeytoken doivent rester inutilisés, et avoir un nom évocateur pour attirer et leurrer les attaquants (par exemple, SQL-Admin). Toute activité observée sur ces comptes peut être le signe d’un comportement malveillant.

Pour plus d’informations sur les comptes honeytoken, consultez [Configurer des exclusions de détection et des comptes honeytoken](install-atp-step7.md).

**TP, B-TP ou FP**

1. Vérifiez si le propriétaire de l’ordinateur source a utilisé le compte Honeytoken pour s’authentifier, à l’aide de la méthode décrite dans la page de l’activité suspecte (par exemple, Kerberos, LDAP, NTLM).

    Si le propriétaire de l’ordinateur source a utilisé le compte Honeytoken pour s’authentifier à l’aide de la méthode précisément décrite dans l’alerte, *fermez* l’alerte de sécurité comme s’agissant d’une activité **B-TP**.

**Comprendre l’étendue de la violation**

1. Examinez l’[utilisateur source](investigate-a-user.md).
2. Examinez l’[ordinateur source](investigate-a-computer.md).

> [!NOTE]
    > Si l’authentification a été effectuée avec NTLM, il peut arriver dans certains scénarios que les informations disponibles sur le serveur auquel l’ordinateur source a tenté d’accéder soient insuffisantes. Azure ATP capture les données de l’ordinateur source suivant l’événement Windows 4776, qui contient le nom de l’ordinateur source défini par l’ordinateur.
    > À l’aide de l’événement Windows 4776 pour capturer ces informations, le champ source de ces informations est parfois remplacé par l’appareil ou le logiciel pour afficher uniquement Poste de travail ou MSTSC. Si vous avez fréquemment des appareils qui s’affichent comme Poste de travail ou MSTSC, veillez à activer l’audit NTLM sur les contrôleurs de domaine appropriés pour obtenir le vrai nom de l’ordinateur source.    
    > Pour activer l’audit NTLM, activez l’événement Windows 8004 (l’événement d’authentification NTLM qui contient des informations sur l’ordinateur source, le compte d’utilisateur et le serveur auquel l’ordinateur source a tenté d’accéder).

**Suggestions de correction et étapes préventives**

1. Incluez l’ordinateur source.
    - Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    - Recherchez les utilisateurs qui étaient connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.

## <a name="suspected-brute-force-attack-kerberos-ntlm-external-id-2023"></a>Suspicion d’attaque par force brute (Kerberos, NTLM) (ID externe 2023)

*Nom précédent :* Échecs d’authentification suspects

**Description**

Dans une attaque par force brute, l’attaquant tente de s’authentifier en utilisant plusieurs mots de passe auprès de différents comptes jusqu'à ce qu’un mot de passe correct soit trouvé, ou en utilisant un mot de passe dans une attaque par pulvérisation de mots de passe à grande échelle qui fonctionne au moins pour un compte. Lorsqu’un mot de passe est trouvé, l’attaquant se connecte en utilisant le compte authentifié.

Dans cette détection, une alerte est déclenchée quand de nombreux échecs d’authentification se produisent avec Kerberos ou NTLM, ou quand une pulvérisation de mots de passe est détectée. Avec Kerberos ou NTLM, ce type d’attaque est généralement *horizontal*, avec un petit nombre de mots de passe possibles pour de nombreux utilisateurs, *vertical*, avec un grand nombre de mots de passe pour seulement quelques utilisateurs, ou un mélange des deux.

Dans une pulvérisation de mots de passe, après avoir correctement dressé la liste des utilisateurs valides à partir du contrôleur de domaine, les attaquants tentent d’utiliser UN mot de passe élaboré avec soin sur tous les comptes d’utilisateur connus (un mot de passe sur de nombreux comptes). Si la pulvérisation de mots de passe initiale échoue, ils réessayent en utilisant un autre mot de passe élaboré avec soin, généralement après avoir attendu 30 minutes entre les tentatives. Ce délai d’attente évite aux attaquants de déclencher la plupart des seuils de verrouillage de compte temporels. La pulvérisation de mots de passe est rapidement devenue la technique préférée des pirates et des tests d’intrusion. Les attaques par pulvérisation de mots de passe se sont révélées efficaces pour créer une brèche dans une organisation et pour effectuer des déplacements latéraux afin d’essayer d’élever des privilèges. La période minimale avant le déclenchement d’une alerte est d’une semaine.

**Période d’apprentissage**
 <br>1 semaine

**TP, B-TP ou FP**

Il est important de vérifier si des tentatives de connexion ont abouti à une authentification réussie.

1. Si des tentatives de connexion ont abouti, vérifiez si les **comptes devinés** sont normalement utilisés à partir de cet ordinateur source.
   - Est-il possible que ces comptes aient échoué à cause d’un mot de passe incorrect ?  
   - Vérifiez auprès du ou des utilisateurs s’ils ont généré l’activité (ils ne sont pas arrivés à se connecter plusieurs fois, puis ont réussi). 

     Si la réponse aux questions ci-dessus est **oui**, **fermez** l’alerte de sécurité comme s’agissant d’une activité B-TP.

2. S’il n’y a pas de **comptes devinés**, vérifiez si les **comptes attaqués** sont normalement utilisés à partir de l’ordinateur source.
    - Regardez si un script s’exécute sur l’ordinateur source avec des informations d’identification incorrectes/anciennes.
    - Si la réponse à la question précédente est **oui**, arrêtez et modifiez le script, ou supprimez-le. **Fermez** l’alerte de sécurité comme s’agissant d’une activité B-TP.

**Comprendre l’étendue de la violation**

1. Examinez l’ordinateur source.  
1. Dans la page de l’alerte, vérifiez si des utilisateurs ont été devinés, le cas échéant.
    - Pour chaque utilisateur qui a été deviné, [consultez leur profil](investigate-a-user.md) afin d’en savoir plus.

    > [!NOTE]
    > Si l’authentification a été effectuée avec NTLM, il peut arriver dans certains scénarios que les informations disponibles sur le serveur auquel l’ordinateur source a tenté d’accéder soient insuffisantes. Azure ATP capture les données de l’ordinateur source suivant l’événement Windows 4776, qui contient le nom de l’ordinateur source défini par l’ordinateur.
    > À l’aide de l’événement Windows 4776 pour capturer ces informations, le champ source de ces informations est parfois remplacé par l’appareil ou le logiciel pour afficher uniquement Poste de travail ou MSTSC. Si vous avez fréquemment des appareils qui s’affichent comme Poste de travail ou MSTSC, veillez à activer l’audit NTLM sur les contrôleurs de domaine appropriés pour obtenir le vrai nom de l’ordinateur source.    
    > Pour activer l’audit NTLM, activez l’événement Windows 8004 (l’événement d’authentification NTLM qui contient des informations sur l’ordinateur source, le compte d’utilisateur et le serveur auquel l’ordinateur source a tenté d’accéder).
    
1. Une fois que vous savez quel serveur a envoyé la validation de l’authentification, examinez-le en vérifiant ses événements, par exemple l’événement Windows 4624, pour mieux comprendre le processus d’authentification. 
1. Regardez si ce serveur est exposé à Internet avec des ports ouverts. 
    Par exemple, est-il ouvert à Internet avec le protocole RDP ?

**Suggestions de correction et étapes préventives**

1. Réinitialisez les mots de passe des utilisateurs devinés et activez MFA.
2. Incluez l’ordinateur source.
    - Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    - Recherchez les utilisateurs qui étaient connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.
3. Réinitialisez les mots de passe de l’utilisateur source et activez MFA.
4. Appliquez des [mots de passe complexes et longs](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) dans l’organisation afin d’assurer le niveau minimum de sécurité nécessaire contre les futures attaques par force brute.

## <a name="suspected-brute-force-attack-ldap-external-id-2004"></a>Suspicion d’attaque par force brute (LDAP) (ID externe 2004) 

*Nom précédent :* Attaque par force brute par le biais d’une liaison simple LDAP

**Description**

Dans une attaque par force brute, l’attaquant tente de s’authentifier en essayant plusieurs mots de passe pour différents comptes jusqu’à ce qu’il trouve le bon mot de passe de l’un des comptes. Une fois qu’il a deviné le mot de passe d’un compte, l’attaquant utilise ce compte pour se connecter au réseau.  

Dans cette détection, une alerte est déclenchée quand Azure ATP détecte un nombre massif d’authentifications de liaison simple. Cette alerte détecte les attaques par force brute *horizontales* avec un petit nombre de mots de passe pour de nombreux utilisateurs, *verticales* avec un grand nombre de mots de passe pour seulement quelques utilisateurs, ou un mélange des deux options.

**TP, B-TP ou FP**

Il est important de vérifier si des tentatives de connexion ont abouti à une authentification réussie.

1. Si des tentatives de connexion ont abouti, les **comptes devinés** sont-ils normalement utilisés à partir de cet ordinateur source ?
   - Est-il possible que ces comptes aient échoué à cause d’un mot de passe incorrect ?  
   - Vérifiez auprès du ou des utilisateurs s’ils ont généré l’activité (ils ne sont pas arrivés à se connecter plusieurs fois, puis ont réussi).

     Si la réponse aux questions précédentes est **oui**, **fermez** l’alerte de sécurité comme s’agissant d’une activité B-TP.

2. S’il n’y a pas de **comptes devinés**, vérifiez si les **comptes attaqués** sont normalement utilisés à partir de l’ordinateur source.
   - Regardez si un script s’exécute sur l’ordinateur source avec des informations d’identification incorrectes/anciennes.

     Si la réponse à la question précédente est **oui**, arrêtez et modifiez le script, ou supprimez-le. **Fermez** l’alerte de sécurité comme s’agissant d’une activité B-TP.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).  
2. Dans la page de l’alerte, vérifiez si des utilisateurs ont été devinés, le cas échéant. Pour chaque utilisateur qui a été deviné, [consultez leur profil](investigate-a-user.md) afin d’en savoir plus.

**Suggestions de correction et étapes préventives**

1. Réinitialisez les mots de passe des utilisateurs devinés et activez MFA.
2. Incluez l’ordinateur source.
    - Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    - Recherchez les utilisateurs qui étaient connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.
3. Réinitialisez les mots de passe de l’utilisateur source et activez MFA.
4. Appliquez des [mots de passe complexes et longs](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) dans l’organisation afin d’assurer le niveau minimum de sécurité nécessaire contre les futures attaques par force brute.
5. Empêchez l’utilisation du protocole de texte clair LDAP dans votre organisation.

## <a name="suspected-brute-force-attack-smb-external-id-2033"></a>Suspicion d’attaque par force brute (SMB) (ID externe 2033) 

*Nom précédent :* Implémentation de protocole inhabituelle (utilisation potentielle d’outils malveillants comme Hydra)

**Description**

Les attaquants utilisent des outils qui implémentent différents protocoles, tels que SMB, Kerberos, NTLM, de façon inhabituelle. Ce type de trafic réseau est admis par Windows sans avertissement, mais Azure ATP est capable de reconnaître une intention potentiellement malveillante. Le comportement est révélateur de techniques de force brute.

**TP, B-TP ou FP**

1. Vérifiez si l’ordinateur source exécute un outil d’attaque tel qu’Hydra.
   1. Si l’ordinateur source exécute un outil d’attaque, cette alerte est un **TP**. Suivez les instructions de la rubrique **Comprendre l’étendue de la violation** ci-dessus.

Parfois, les applications implémentent leur propre pile NTLM ou SMB.

1. Vérifiez si l’ordinateur source exécute son propre type de pile NTLM ou SMB d’application.
    1. Si l’ordinateur source exécute ce type d’application alors qu’il ne devrait pas continuer à le faire, corrigez la configuration de l’application si nécessaire. **Fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP**.
    2. Si l’ordinateur source exécute ce type d’application et qu’il doit continuer à le faire, **fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP** et excluez cet ordinateur.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).
2. Examinez l’[utilisateur source](investigate-a-user.md) (le cas échéant).

**Suggestions de correction et étapes préventives**

1. Réinitialisez les mots de passe des utilisateurs devinés et activez l’authentification multifacteur.
2. Incluez l’ordinateur source.
   1. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
   2. Cherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis.
   3. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.
3. Appliquez des [mots de passe complexes et longs](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/password-policy) dans l’organisation. Les mots de passe complexes et longs assurent le niveau minimum de sécurité nécessaire contre les futures attaques par force brute.
4. [Désactivez SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/).

## <a name="suspected-wannacry-ransomware-attack-external-id-2035"></a>Suspicion d’attaque de ransomware WannaCry (ID externe 2035)

*Nom précédent :* Implémentation de protocole inhabituelle (attaque ransomware WannaCry potentielle)

**Description**

Les attaquants utilisent des outils qui implémentent différents protocoles de façon inhabituelle. Ce type de trafic réseau est admis par Windows sans avertissement, mais Azure ATP est capable de reconnaître une intention potentiellement malveillante. Le comportement est révélateur de certaines techniques utilisées par des ransomwares avancés tels que WannaCry.

**TP, B-TP ou FP**

1. Vérifiez si WannaCry est en cours d’exécution sur l’ordinateur source. 

    - Si WannaCry est en cours d’exécution, cette alerte est une **TP**. Suivez les instructions de la rubrique **Comprendre l’étendue de la violation** ci-dessus.

Parfois, les applications implémentent leur propre pile NTLM ou SMB.

1. Vérifiez si l’ordinateur source exécute son propre type de pile NTLM ou SMB d’application. 
    1. Si l’ordinateur source exécute ce type d’application alors qu’il ne devrait pas continuer à le faire, corrigez la configuration de l’application si nécessaire. **Fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP**.
    2. Si l’ordinateur source exécute ce type d’application et qu’il doit continuer à le faire, **fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP** et excluez cet ordinateur.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).
2. Examinez l’[utilisateur compromis](investigate-a-user.md).

**Suggestions de correction et étapes préventives**

1. Incluez l’ordinateur source.
      - [Supprimez WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo).
      - WanaKiwi peut déchiffrer les données interceptées par certains ransomwares, mais uniquement si l’utilisateur n’a pas redémarré ou éteint l’ordinateur. Pour plus d’informations, consultez [Ransomware WannaCry](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)
      - Recherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.
2. Appliquez des correctifs à toutes vos machines, sans oublier les mises à jour de sécurité. 
      - [Désactivez SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/).

## <a name="suspected-use-of-metasploit-hacking-framework-external-id-2034"></a>Suspicion d’utilisation du framework de piratage Metasploit (ID externe 2034)

*Nom précédent :* Implémentation de protocole inhabituelle (utilisation potentielle d’outils de piratage Metasploit)

**Description**

Les attaquants utilisent des outils qui implémentent différents protocoles (SMB, Kerberos, NTLM) de façon inhabituelle. Ce type de trafic réseau est admis par Windows sans avertissement, mais Azure ATP est capable de reconnaître une intention potentiellement malveillante. Le comportement est révélateur de certaines techniques comme l’utilisation du framework de piratage Metasploit. 

**TP, B-TP ou FP**

1. Vérifiez si l’ordinateur source exécute un outil d’attaque tel que Metasploit ou Medusa.

2. Si oui, c’est un vrai positif. Suivez les instructions de la rubrique **Comprendre l’étendue de la violation** ci-dessus.

Parfois, les applications implémentent leur propre pile NTLM ou SMB.

 1. Vérifiez si l’ordinateur source exécute son propre type de pile NTLM ou SMB d’application. 
    1. Si l’ordinateur source exécute ce type d’application alors qu’il ne devrait pas continuer à le faire, corrigez la configuration de l’application si nécessaire. **Fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP**.
    2. Si l’ordinateur source exécute ce type d’application et qu’il doit continuer à le faire, **fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP** et excluez cet ordinateur.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).
2. S’il y a un utilisateur source, [examinez l’utilisateur](investigate-a-user.md).

**Suggestions de correction et étapes préventives**

1. Réinitialisez les mots de passe des utilisateurs devinés et activez MFA.
2. Incluez l’ordinateur source.
   1. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
   2. Cherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.
3. Réinitialisez les mots de passe de l’utilisateur source et activez MFA. 
4. [Désactivez SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/). 

## <a name="suspicious-vpn-connection-external-id-2025"></a>Connexion VPN suspecte (ID externe 2025) 

*Nom précédent :* Connexion VPN suspecte 

**Description**

Azure ATP apprend le comportement de l’entité pour les utilisateurs de connexions VPN sur une période mobile d’un mois. 

Le modèle de comportement VPN est basé sur les ordinateurs auxquels les utilisateurs se connectent et les emplacements à partir desquels ils se connectent. 

Une alerte est ouverte quand il y a un écart de comportement de l’utilisateur par rapport à l’algorithme de machine learning.

**Période d’apprentissage**

30 jours après la première connexion VPN et au moins 5 connexions VPN au cours des 30 derniers jours, par utilisateur.

**TP, B-TP ou FP**

1. L’utilisateur suspect est-il supposé effectuer ces opérations ?
    1. L’utilisateur a-t-il changé récemment d’endroit ?
    2. L’utilisateur voyage-t-il et se connecte-t-il à partir d’un nouvel appareil ?

Si la réponse aux questions ci-dessus est oui, **fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP**.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).
2. S’il y a un utilisateur source, [examinez l’utilisateur](investigate-a-user.md).

**Suggestions de correction et étapes préventives**

1. Réinitialisez le mot de passe de l’utilisateur et activez MFA.
2. Empêchez cet utilisateur de se connecter par VPN.
3. Empêchez cet ordinateur de se connecter par VPN.
4. Vérifiez si d’autres utilisateurs sont connectés via VPN à partir de ces emplacements, puis vérifiez s’ils sont compromis.

> [!div class="nextstepaction"]
> [Tutoriel sur les alertes de mouvement latéral](atp-lateral-movement-alerts.md)

## <a name="see-also"></a>Voir aussi

- [Examiner un ordinateur](investigate-a-computer.md)
- [Examiner un utilisateur](investigate-a-user.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Utilisation des chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Alertes de reconnaissance](atp-reconnaissance-alerts.md)
- [Alertes de mouvement latéral](atp-lateral-movement-alerts.md)
- [Alertes de dominance du domaine](atp-domain-dominance-alerts.md)
- [Alertes d’exfiltration](atp-exfiltration-alerts.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
