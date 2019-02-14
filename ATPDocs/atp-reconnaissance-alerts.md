---
title: Alertes de sécurité de la phase de reconnaissance Azure ATP | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of reconnaissance phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 02/04/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2d4d7f65f0b46624acc64b25fbd0241b876be421
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077743"
---
# <a name="tutorial-reconnaissance-alerts"></a>Didacticiel : Alertes de reconnaissance  

En général, les attaques sont lancées contre des entités accessibles, par exemple un utilisateur avec des privilèges peu élevés, puis rapidement, elles se déplacent latéralement jusqu’à ce que l’attaquant parvienne à accéder à des ressources importantes, comme des comptes sensibles, des administrateurs de domaine ou des données hautement sensibles. Azure ATP identifie ces menaces avancées à la source tout au long de la chaîne d’annihilation des attaques et les classifie selon les phases suivantes :

1. **Reconnaissance**
2. [Informations d’identification compromises](atp-compromised-credentials-alerts.md)
3. [Mouvements latéraux](atp-lateral-movement-alerts.md)
4. [Dominance du domaine](atp-domain-dominance-alerts.md)
5. [Exfiltration](atp-exfiltration-alerts.md) 

Pour en savoir plus sur la structure et les composants courants de toutes les alertes de sécurité Azure ATP, consultez [Présentation des alertes de sécurité](understanding-security-alerts.md).

Les alertes de sécurité suivantes vous aident à identifier et à résoudre les activités suspectes de la phase **Reconnaissance** détectées par Azure ATP sur votre réseau.

Dans ce tutoriel, vous allez apprendre à comprendre, classifier, prévenir et pallier aux types d’attaques suivants :

> [!div class="checklist"]
> * Reconnaissance d’énumération de compte (ID externe 2003)
> * Reconnaissance de mappage de réseau (DNS) (ID externe 2007)
> * Reconnaissance des utilisateurs et des adresses IP (SMB) (ID externe 2012)
> * Reconnaissance des utilisateurs et des membres d’un groupe (SAMR) (ID externe 2021)

## <a name="account-enumeration-reconnaissance-external-id-2003"></a>Reconnaissance d’énumération de compte (ID externe 2003) 


*Nom précédent :* Reconnaissance à l’aide de l’énumération de compte

**Description**

Lors d’une reconnaissance à l’aide de l’énumération de comptes, un attaquant utilise un dictionnaire contenant des milliers de noms d’utilisateurs ou des outils comme KrbGuess afin d’essayer de deviner des noms d’utilisateur dans le domaine.

**Kerberos** : L’attaquant effectue des requêtes Kerberos avec ces noms pour tenter de trouver un nom d’utilisateur valide dans le domaine. Quand l’attaquant parvient à deviner un nom d’utilisateur, il obtient la **Pré-authentification requise** au lieu de l’erreur Kerberos **Principal de sécurité inconnu**.

**NTLM** : L’attaquant effectue des requêtes d’authentification NTLM avec l’annuaire de noms pour tenter de trouver un nom d’utilisateur valide dans le domaine. Quand l’attaquant parvient à deviner un nom d’utilisateur, il obtient **WrongPassword (0xc000006a)** au lieu de l’erreur NTLM **NoSuchUser (0xc0000064)**.

Dans le cadre de cette détection d’alerte, Azure ATP détecte d’où provient l’attaque par énumération de comptes, le nombre total de tentatives et combien ont abouti. Si le nombre d’utilisateurs inconnus est trop élevé, Azure ATP détecte cela comme une activité suspecte.

**TP, B-TP ou FP**

Certains serveurs et applications interrogent les contrôleurs de domaine pour déterminer si des comptes existent dans des scénarios d’utilisation légitime.

Pour déterminer si cette requête était un **FP**, **BTP** ou **FP**, cliquez sur l’alerte pour accéder à sa page de détails :

1. Vérifiez si l’ordinateur source était censé effectuer ce type de requête. Dans ce cas, un **B-TP** pourrait être dû à des systèmes de ressources humaines ou à des serveurs Microsoft Exchange.

2. Vérifiez les domaines des comptes.
   - Voyez-vous des utilisateurs supplémentaires qui appartiennent à un autre domaine ? 
     <br>Une erreur de configuration de serveur (par exemple dans Exchange/Skype ou ADSF) peut faire apparaître des utilisateurs supplémentaires qui appartiennent à différents domaines.
   - Examinez la configuration du service à problème afin de corriger l’erreur de configuration.

     Si vous avez répondu **oui** aux questions ci-dessus, il s’agit d’une activité **B-TP**. *Fermez* l’alerte de sécurité.<br>

En guise d’étape suivante, examinez l’ordinateur source : 

1. Est-ce qu’un script ou une application s’exécutant sur l’ordinateur source pourrait générer ce comportement ?  
   - S’agit-il d’un ancien script exécuté avec d’anciennes informations d’identification ? <br>Si oui, arrêtez et modifiez ou supprimez le script. 
   - S’agit-il d’un script ou d’une application d’administration ou de sécurité censé(e) s’exécuter dans l’environnement ?
 
     Si vous avez répondu **oui** à la question précédente, *fermez* l’alerte de sécurité et excluez cet ordinateur. Il s’agit probablement d’une activité **B-TP**.

À présent, examinez les comptes :<br>
<br>Les attaquants utilisent généralement un dictionnaire de noms de comptes aléatoires pour rechercher des noms de comptes existants dans une organisation.

1. Les comptes inexistants vous disent-ils quelque chose ?  
   - Si les comptes inexistants vous semblent familiers, il s’agit peut-être de comptes désactivés ou appartenant à des employés ayant quitté l’entreprise.
   - Recherchez une application ou un script qui vérifie quels comptes existent toujours dans Active Directory.

     Si vous avez répondu **oui** à l’une des questions précédentes, *fermez* l’alerte de sécurité. Il s’agit probablement d’une activité **B-TP**.

2. Si des tentatives correspondent à des noms de compte existants, l’attaquant connaît l’existence de comptes dans votre environnement et peut essayer d’utiliser des attaques par force brute pour accéder à votre domaine en utilisant les noms d’utilisateur découverts. 
    - Vérifiez les noms de compte trouvés en recherchant d’autres activités suspectes. 
    - Regardez si des comptes sensibles se trouvent parmi les comptes trouvés.

### <a name="understand-the-scope-of-the-breach"></a>Comprendre l’étendue de la violation

1. Examinez l’ordinateur source
2. Si des tentatives correspondent à des noms de comptes existants, l’attaquant connaît l’existence de comptes dans votre environnement et peut utiliser des attaques par force brute pour essayer d’accéder à votre domaine en utilisant les noms d’utilisateur découverts. Examinez les comptes existants en suivant le [guide d’investigation sur les utilisateurs](investigate-a-user.md). 

### <a name="suggested-remediation-and-steps-for-prevention"></a>Suggestions de correction et étapes préventives

1. Contenez l’[ordinateur source](investigate-a-computer.md). 
    1. Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    2. Recherchez les utilisateurs qui étaient connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. 
    3. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.
2. Appliquez des [mots de passe complexes et longs](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) dans l’organisation. Les mots de passe longs et complexes assurent le niveau minimal de sécurité nécessaire contre les attaques par force brute. Les attaques par force brute sont généralement l’étape qui suit l’énumération dans la chaîne de destruction de cyber-attaque. 

## <a name="network-mapping-reconnaissance-dns-external-id-2007"></a>Reconnaissance de mappage de réseau (DNS) (ID externe 2007) 


*Nom précédent :* Reconnaissance à l’aide de DNS

**Description**

Votre serveur DNS contient une carte de l’ensemble des ordinateurs, adresses IP et services de votre réseau. Ces informations sont utilisées par les attaquants pour mapper la structure de votre réseau et cibler les ordinateurs intéressants pour les étapes suivantes de l’attaque. 
 
Il existe plusieurs types de requêtes dans le protocole DNS. Cette alerte de sécurité Azure ATP détecte les requêtes (transferts) AXFR suspectes provenant de serveurs autres que DNS.

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
1. Incluez l’ordinateur source. 
    - Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    - Recherchez les utilisateurs qui étaient connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.

**Prévention :** Il est important de prévenir toute attaque ultérieure à l’aide de requêtes AXFR en sécurisant votre serveur DNS interne.

1. Sécurisez votre serveur DNS interne pour éviter la reconnaissance à l’aide de DNS en désactivant les transferts de zone ou en [limitant les transferts de zone](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)) uniquement aux adresses IP spécifiées. La modification des transferts de zone est l’une des tâches de la liste de contrôle que vous devez suivre pour [sécuriser vos serveurs DNS contre les attaques internes et externes](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)).

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

**Description** La reconnaissance des utilisateurs et des membres d’un groupe permet aux attaquants de mapper la structure d’annuaire et de cibler des comptes privilégiés pour les étapes suivantes de leur attaque. Le protocole SAM-R (Security Account Manager Remote) est l’une des méthodes utilisées pour interroger l’annuaire et effectuer ce type de mappage.  
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
3. Recherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.
4. Réinitialisez le mot de passe utilisateur source et activez l’authentification multifacteur.
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
