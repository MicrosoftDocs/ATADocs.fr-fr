---
title: Alertes de sécurité Azure ATP indiquant un mouvement latéral | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of lateral movement phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/15/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2257eb00-8614-4577-b6a1-5c65085371f2
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7816dba02c2fea07afc080c7aed5ede073c88fac
ms.sourcegitcommit: e2daa0f93d97d552cfbf1577fbd05a547b63e95b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54314310"
---
# <a name="tutorial-lateral-movement-alerts"></a>Tutorial : Alertes de mouvement latéral  

En général, les attaques sont lancées contre des entités accessibles, par exemple un utilisateur avec des privilèges peu élevés, puis rapidement, elles se déplacent latéralement jusqu’à ce que l’attaquant parvienne à accéder à des ressources importantes, comme des comptes sensibles, des administrateurs de domaine ou des données hautement sensibles. Azure ATP identifie ces menaces avancées à la source tout au long de la chaîne d’annihilation des attaques et les classifie selon les phases suivantes :

1. [Reconnaissance](atp-reconnaissance-alerts.md)
2. [Informations d’identification compromises](atp-compromised-credentials-alerts.md)
3. **Mouvements latéraux**
4. [Dominance du domaine](atp-domain-dominance-alerts.md)
5. [Exfiltration](atp-exfiltration-alerts.md)

Pour en savoir plus sur la structure et les composants courants de toutes les alertes de sécurité Azure ATP, consultez [Présentation des alertes de sécurité](understanding-security-alerts.md).

Les alertes de sécurité suivantes vous aident à identifier et à résoudre les activités suspectes de la phase **Mouvement latéral** détectées par Azure ATP sur votre réseau. Dans ce tutoriel, vous allez apprendre à comprendre, classifier, prévenir et empêcher les types d’attaques suivants :

> [!div class="checklist"]
> * Suspicion d’usurpation d’identité (pass-the-hash) (ID externe 2017)
> * Suspicion d’usurpation d’identité (pass-the-ticket) (ID externe 2018)
> * Suspicion d’attaque over-pass-the-hash (passage à une version antérieure du chiffrement) (ID externe 2008)
> * Suspicion d’attaque over-pass-the-hash (Kerberos) (ID externe 2002)

## <a name="suspected-identity-theft-pass-the-hash-external-id-2017"></a>Suspicion d’usurpation d’identité (pass-the-hash) (ID externe 2017)

*Nom précédent :* Usurpation d’identité par attaque Pass-the-Hash

**Description**

Pass-the-Hash est une technique de mouvement latéral par laquelle les attaquants volent le code de hachage NTLM d’un utilisateur sur un ordinateur et utilisent ensuite ce code pour accéder à un autre ordinateur.

**TP, B-TP ou FP ?**
1. Déterminez si le hachage a été utilisé à partir d’ordinateurs que l’utilisateur utilise régulièrement. 
    - Si le hachage a été utilisé à partir d’ordinateurs utilisés régulièrement, **fermez** l’alerte comme s’agissant d’un **FP**.  
 
**Comprendre l’étendue de la violation**

1. Examinez les [ordinateurs sources et de destination](investigate-a-computer.md) plus en détail.  
2. Examinez l’[utilisateur compromis](investigate-a-computer.md).
 
**Suggestions de correction et étapes préventives**

1. Réinitialisez le mot de passe de l’utilisateur source et activez MFA.
2. Contenez les ordinateurs sources et de destination.
3. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
4. Recherchez les utilisateurs connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.

## <a name="suspected-identity-theft-pass-the-ticket-external-id-2018"></a>Suspicion d’usurpation d’identité (pass-the-ticket) (ID externe 2018)

*Nom précédent :* Usurpation d’identité par attaque Pass-the-Ticket

**Description**

Pass-the-Ticket est une technique de mouvement latéral par laquelle les attaquants volent un ticket Kerberos sur un ordinateur et réutilisent ensuite ce ticket pour accéder à un autre ordinateur. Cette détection vérifie si un ticket Kerberos a été utilisé sur plusieurs ordinateurs différents.

**TP, B-TP ou FP ?**

La résolution correcte des adresses IP aux ordinateurs de l’organisation est essentielle pour identifier les attaques pass-the-ticket d’un ordinateur à un autre. 

1. Vérifiez si l’adresse IP de l’un ou des deux ordinateurs appartient à un sous-réseau alloué à partir d’un pool DHCP de taille insuffisante, par exemple, VPN, VDI ou WiFi. 
2. L’adresse IP est-elle partagée (par exemple, par un appareil NAT) ?  
3. Le capteur ne résout-il pas une ou plusieurs des adresses IP de destination ? Si une adresse IP de destination n’est pas résolue, cela peut indiquer que les ports appropriés entre le capteur et les appareils ne sont pas ouverts correctement. 

    Si la réponse à l’une des questions précédentes est **oui**, vérifiez si les ordinateurs sources et de destination sont identiques. S’ils sont identiques, il s’agit d’un **FP** et il n’y a eu aucune tentative réelle d’attaque **pass-the-ticket**. 

Il existe des applications personnalisées qui transfèrent des tickets pour le compte d’utilisateurs. Ces applications ont des droits de délégation pour les tickets de l’utilisateur.

1. Un type d’application personnalisée telle que celle décrite plus haut est-il actuellement présent sur les ordinateurs de destination ? Quels services l’application exécute-t-elle ? Les services agissent-ils au nom des utilisateurs, par exemple pour accéder à des bases de données ?
    - Si la réponse est oui, **fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP**.
2. L’ordinateur de destination est-il un serveur de délégation ?
    - Si la réponse est oui, **fermez** l’alerte de sécurité et excluez cet ordinateur comme s’agissant d’une activité **T-BP**.
 
**Comprendre l’étendue de la violation**

1. Examinez les [ordinateurs sources et de destination](investigate-a-computer.md).  
2. Examinez l’[utilisateur compromis](investigate-a-computer.md). 

**Suggestions de correction et étapes préventives**

1. Réinitialisez le mot de passe de l’utilisateur source et activez MFA.
2. Contenez les ordinateurs sources et de destination.
3. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
4. Recherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.
5. Si vous avez installé Windows Defender ATP, utilisez **klist.exe purger** pour supprimer tous les tickets de la session spécifiée et empêcher toute utilisation ultérieure des tickets.

## <a name="suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008"></a>Suspicion d’attaque over-pass-the-hash (passage à une version antérieure du chiffrement) (ID externe 2008) 

*Nom précédent :* Passage à une version antérieure du chiffrement

**Description**

Le passage à une version antérieure du chiffrement est une méthode visant à affaiblir Kerberos en abaissant le niveau de chiffrement de différents champs du protocole qui sont normalement chiffrés à l’aide du niveau de chiffrement le plus élevé. Un champ au chiffrement affaibli peut être plus vulnérable à des attaques de force brute en mode hors connexion. Plusieurs méthodes d’attaque exploitent les codes faibles de chiffrement Kerberos. Dans le cadre de cette détection, Azure ATP examine les types de chiffrement Kerberos utilisés par les ordinateurs et les utilisateurs, et déclenche des alertes quand un chiffrement plus faible et inhabituel est utilisé pour l’ordinateur source et/ou l’utilisateur, et que cela correspond à une technique d’attaque connue. 

Dans une attaque over-pass-the-hash, un attaquant peut utiliser un code de hachage faible dérobé pour créer un ticket fort avec une requête Kerberos AS. Dans le cadre de cette détection, on identifie les instances où le type de chiffrement du message AS_REQ reçu de l’ordinateur source a été abaissé par rapport au comportement appris (l’ordinateur utilisait l’algorithme AES).

**TP, B-TP ou FP ?**
1. Déterminez si la configuration de carte à puce a changé récemment. 
    - Les comptes impliqués ont-ils récemment subi des changements de configuration de carte à puce ?  
    
    Si la réponse est oui, **fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP**. 

Certaines ressources légitimes ne prennent pas en charge les codes de chiffrement fort et peuvent déclencher cette alerte. 

2. Tous les utilisateurs sources partagent-ils quelque chose ? 
    1. Par exemple, les membres du personnel marketing accèdent-ils tous à une ressource spécifique susceptible de provoquer le déclenchement de l’alerte ?
    2. Vérifiez les ressources auxquelles ces tickets ont accédé. 
        - Vérifiez cela dans Active Directory en consultant l’attribut *msDS-SupportedEncryptionTypes* du compte de service de la ressource.
    3. Si une seule ressource est sollicitée, vérifiez s’il s’agit d’une ressource à laquelle ces utilisateurs sont autorisés à accéder.   

    Si la réponse à l’une des questions précédentes est **oui**, il s’agit probablement d’une activité **T-BP**. Vérifiez si la ressource peut prendre en charge un code de chiffrement fort, implémentez un code de chiffrement plus fort dans la mesure du possible et **fermez** l’alerte de sécurité.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).  
2. Examinez l’[utilisateur compromis](investigate-a-computer.md). 

**Suggestions de correction et étapes préventives** 

**Correction**
1. Réinitialisez le mot de passe de l’utilisateur source et activez MFA. 
2. Incluez l’ordinateur source. 
3. Trouvez l’outil qui a effectué l’attaque et supprimez-le. 
4. Recherchez les utilisateurs connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur  

**Prévention**
 
1. Configurez votre domaine pour qu’il prenne en charge des codes de chiffrement renforcés et désactivez *Utiliser les types de chiffrement DES Kerberos*. Apprenez-en davantage sur [les types de chiffrement et Kerberos](https://blogs.msdn.microsoft.com/openspecification/2011/05/30/windows-configurations-for-kerberos-supported-encryption-type/). 
2. Vérifiez que le niveau fonctionnel du domaine est configuré pour prendre en charge les codes de chiffrement fort.  
3. Utilisez de préférence des applications qui prennent en charge les codes de chiffrement fort.

## <a name="suspected-overpass-the-hash-attack-kerberos-external-id-2002"></a>Suspicion d’attaque over-pass-the-hash (Kerberos) (ID externe 2002) 

*Nom précédent :* Implémentation inhabituelle du protocole Kerberos (attaque overpass-the-hash potentielle)

**Description**

Les attaquants utilisent des outils qui implémentent différents protocoles, tels que Kerberos et SMB, de façon inhabituelle. Bien que Microsoft Windows accepte ce type de trafic réseau sans avertissement, Azure ATP est capable de reconnaître une intention potentiellement malveillante. Le comportement est révélateur de certaines techniques comme Over-Pass-the-Hash, la Force Brute, ainsi que l’exploitation des failles de sécurité par de puissants ransomwares tels que WannaCry.

**TP, B-TP ou FP ?**

Parfois, les applications implémentent leur propre pile Kerberos, mais pas conformément à la RFC Kerberos. 

1. Vérifiez si l’ordinateur source exécute une application avec sa propre pile Kerberos, de manière non conforme à la RFC Kerberos.  
2. Si l’ordinateur source exécute une telle application alors qu’il ne doit **pas** le faire, corrigez la configuration de l’application. **Fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP**.  
3. Si l’ordinateur source exécute une telle application et qu’il doit continuer à le faire, **fermez** l’alerte de sécurité comme s’agissant d’une activité **T-BP** et excluez l’ordinateur. 

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).  
2. S’il y a un [utilisateur source](investigate-a-user.md), procédez à une investigation. 

**Suggestions de correction et étapes préventives** 

1. Réinitialisez les mots de passe des utilisateurs compromis et activez MFA.
2. Incluez l’ordinateur source.
3. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
4. Recherchez les utilisateurs connectés aux environs de l’heure de l’activité suspecte, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.  
5. Réinitialisez les mots de passe des utilisateurs sources et activez MFA.

> [!div class="nextstepaction"]
> [Tutoriel sur les alertes de dominance du domaine](atp-domain-dominance-alerts.md)

## <a name="see-also"></a>Voir aussi

- [Examiner un ordinateur](investigate-a-computer.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Utilisation des chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Alertes de reconnaissance](atp-reconnaissance-alerts.md)
- [Alertes indiquant des informations d’identification compromises](atp-compromised-credentials-alerts.md)
- [Alertes de dominance du domaine](atp-domain-dominance-alerts.md)
- [Alertes d’exfiltration](atp-exfiltration-alerts.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
