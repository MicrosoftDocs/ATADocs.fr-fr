---
title: Guide des alertes de sécurité d’Azure ATP | Microsoft Docs
d|Description: This article provides a list of the security alerts issued by Azure ATP and steps for remediation.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a32d19e8e130f326859276dde60c794712da5a91
ms.sourcegitcommit: f4f2a1b2c674c4dba7a46ece0624f5ea10c4865e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2018
ms.locfileid: "52744810"
---
*S’applique à : Azure Advanced Threat Protection*


# <a name="azure-advanced-threat-protection-security-alert-guide"></a>Guide des alertes de sécurité d’Azure Advanced Threat Protection

Après une investigation appropriée, toutes les alertes de sécurité Azure ATP peuvent être classées comme suit :

-   **Vrai positif** : action malveillante détectée par Azure ATP.

-   **Vrai positif sans gravité** : action détectée par Azure ATP qui est réelle, mais pas malveillante, comme un test de pénétration.

-   **Faux positif** : fausse alerte. L’activité n’a pas eu lieu.

Pour plus d’informations sur l’utilisation des alertes de sécurité d’Azure ATP, consultez [Utilisation des alertes de sécurité](working-with-suspicious-activities.md).

## <a name="security-alert-name-mapping-and-unique-externalid"></a>Mappage et externalId unique des noms des alertes de sécurité

Dans la version 2.56, toutes les alertes de sécurité Azure ATP existantes ont été renommées avec des noms plus faciles à comprendre. Les mappages entre les anciens et les nouveaux noms ainsi que leur externalId unique correspondant sont listés dans le tableau suivant. Microsoft recommande d’utiliser les externalIds des alertes au lieu de leur nom pour les scripts ou pour l’automation, car seuls les externalIds des alertes sont permanents et non susceptibles d’être modifiés. 

> [!div class="mx-tableFixed"] 

|Nouveau nom de l’alerte de sécurité|Ancien nom de l’alerte de sécurité|ExternalId unique|
|---------|----------|---------|
|Reconnaissance d’énumération de compte|Reconnaissance à l’aide de l’énumération de compte|2003|
|Activité Honeytoken|Activité Honeytoken|2014|
|Demande malveillante de la clé principale de l’API de protection des données|Demande d’information privée de protection contre les données malveillantes|2020|
|Reconnaissance de mappage de réseau (DNS)|Reconnaissance à l’aide de DNS|2007|
|Tentative d’exécution de code à distance|Tentative d’exécution de code à distance|2019|
|Suspicion d’attaque par force brute (LDAP)|Attaque par force brute par le biais d’une liaison simple LDAP|2004|
|Suspicion d’attaque DCShadow (promotion du contrôleur de domaine)|Promotion du contrôleur de domaine suspect (attaque DcShadow potentielle)|2028|
|Suspicion d’attaque DCShadow (demande de réplication du contrôleur de domaine)|Demande de réplication suspecte du contrôleur de domaine (attaque DcShadow potentielle)|2029|
|Suspicion d’attaque DCSync (réplication de services d’annuaire)|Réplication malveillante de services d’annuaire|2006|
|Suspicion d’utilisation de golden ticket (passage à une version antérieure du chiffrement)|Activité de passage à une version antérieure du chiffrement (attaque golden ticket potentielle)|2009|
|Suspicion d’utilisation de golden ticket (données d’autorisation falsifiées) |Réaffectation de privilèges à l’aide de données d’autorisation falsifiées|2013|
|Suspicion d'utilisation de golden ticket (compte inexistant)|Golden ticket Kerberos - compte inexistant|2027|
|Suspicion d’utilisation de golden ticket (anomalie de ticket) |Golden ticket Kerberos - anomalie de ticket|2022|
|Suspicion d’utilisation de golden ticket (anomalie de temps) - préversion| NA|2032|
|Suspicion d'usurpation d’identité (pass-the-hash)|Usurpation d’identité par attaque Pass-the-Hash|2017|
|Suspicion d’usurpation d’identité (pass-the-ticket)|Usurpation d’identité par attaque Pass-the-Ticket|2018|
|Suspicion d’attaque over-pass-the-hash (passage à une version antérieure du chiffrement)|Activité de passage à une version antérieure du chiffrement (attaque Overpass-the-Hash potentielle)|2008|
|Suspicion d’attaque Skeleton Key (passage à une version antérieure du chiffrement)|Activité de passage à une version antérieure du chiffrement (attaque Skeleton Key potentielle)|2010|
|Communication suspecte sur DNS|Communication suspecte sur DNS|2031|
|Modification suspecte de groupes sensibles|Modification suspecte de groupes sensibles|2024|
|Création de service malveillant|Création de service malveillant|2026|
|Connexion VPN suspecte|Connexion VPN suspecte|2025|
|Suspicion d’attaque de ransomware WannaCry|Implémentation de protocole inhabituelle (attaque ransomware WannaCry potentielle) *|2002|
|Suspicion d’attaque par force brute (SMB)|Implémentation de protocole inhabituelle (utilisation potentielle d’outils malveillants comme Hydra) *|2002|
|Suspicion d’utilisation du framework de piratage Metasploit|Implémentation de protocole inhabituelle (utilisation potentielle d’outils de piratage Metasploit)*|2002|
|Suspicion d’attaque over-pass-the-hash (Kerberos)|Implémentation inhabituelle du protocole Kerberos (attaque overpass-the-hash potentielle)*|2002|
|Les alertes d’* *implémentation de protocole inhabituelle* ont toutes le même externalId. Cet externalId sera changé dans une version ultérieure pour avoir un externalId propre à chaque type d’alerte||****|
|Reconnaissance des utilisateurs et des membres d’un groupe (SAMR)|Reconnaissance à l’aide de requêtes de services d’annuaire|2021|
|Reconnaissance des utilisateurs et des adresses IP (SMB) |Reconnaissance à l’aide de l’énumération de sessions SMB|2012|


## <a name="account-enumeration-reconnaissance"></a>Reconnaissance d’énumération de compte
<a name="reconnaissance-using-account-enumeration"></a>
*Nom précédent :* Reconnaissance à l’aide de l’énumération de compte

**Description**

Lors d’une reconnaissance à l’aide de l’énumération de comptes, un attaquant utilise un dictionnaire contenant des milliers de noms d’utilisateurs ou des outils comme KrbGuess pour essayer de deviner des noms d’utilisateur de votre domaine. Il procède à des demandes Kerberos en utilisant ces noms afin de tenter de trouver un nom d’utilisateur valide dans votre domaine. Si l’attaquant parvient à deviner un nom d’utilisateur, il obtient l’erreur Kerberos **Pré-authentification requise** au lieu de **Principal de sécurité inconnu**. 

Dans le cadre de cette détection, Azure ATP peut détecter d'où provient l’attaque, le nombre total de tentatives et combien ont abouti. Si le nombre d’utilisateurs inconnus est trop élevé, Azure ATP détecte cela comme une activité suspecte. 

**Examen**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante. 

2. Cet ordinateur hôte doit-il interroger le contrôleur de domaine pour savoir si des comptes existent (par exemple, des serveurs Exchange) ? <br></br>
Est-ce qu’un script ou une application s’exécutant sur l’hôte pourrait générer ce comportement ? <br></br>
Si la réponse à l’une de ces questions est oui, **fermez** l’activité suspecte (c’est un vrai positif sans incidence) et excluez cet hôte de l’activité suspecte.

3. Téléchargez les détails de l’alerte dans une feuille de calcul Excel pour voir clairement la liste des tentatives de comptes, avec d’un côté les comptes qui existent et de l’autre ceux qui n’existent pas. Si vous examinez la feuille des comptes qui n’existent pas et que vous pensez les connaître, il s’agit peut-être de comptes désactivés ou d’employés ayant quitté l’entreprise. Dans ce cas, il est peu probable que la tentative provienne d’un dictionnaire. Il s’agit très certainement d’une application ou d’un script qui vérifie les comptes qui existent toujours dans Active Directory, c’est donc un vrai positif sans incidence.

3. Si les noms sont en grande partie inconnus, des tentatives ont-elle abouti à une correspondance à des noms de comptes existants dans Active Directory ? S’il n’y a aucune correspondance, la tentative n’a servi à rien, mais vous devez surveiller l’alerte pour voir si elle est mise à jour au fil du temps.

4. Si des tentatives correspondent à des noms de compte existants, l’attaquant connaît l’existence de comptes dans votre environnement et peut essayer d’utiliser des attaques par force brute pour accéder à votre domaine en utilisant les noms d’utilisateur découverts. Vérifiez les noms de compte trouvés en recherchant d’autres activités suspectes. Regardez si des comptes sensibles se trouvent parmi les comptes trouvés.


**Correction**

Les [mots de passe longs et complexes](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) assurent le niveau minimum de sécurité nécessaire contre les attaques par force brute.

## <a name="honeytoken-activity"></a>Activité Honeytoken
<a name="honeytoken-activity"></a>

*Nom précédent :* Activité Honeytoken

**Description**

Les comptes Honeytoken sont des comptes servant de leurre pour identifier et suivre l’activité malveillante qui implique ces comptes. Les comptes Honeytoken doivent rester inutilisés, et avoir un nom évocateur pour attirer et leurrer les attaquants (par exemple, SQL-Admin). Toute activité observée sur ces comptes peut être le signe d’un comportement malveillant.

Pour plus d’informations sur les comptes Honeytoken, consultez [Installer Azure ATP - Étape 7](install-atp-step7.md).

**Examen**

1.  Vérifiez si le propriétaire de l’ordinateur source a utilisé le compte Honeytoken pour s’authentifier, à l’aide de la méthode décrite dans la page de l’activité suspecte (par exemple, Kerberos, LDAP, NTLM).

2.  Accédez à la page du profil de chaque ordinateur source et vérifiez si d’autres comptes se sont authentifiés à partir de ces ordinateurs. Vérifiez auprès des propriétaires de ces comptes s’ils ont utilisé le compte Honeytoken.

3.  Il peut s’agir d’une connexion non interactive. Vous devez donc vérifier si des applications ou des scripts s’exécutent sur les ordinateurs sources.

Si, après avoir effectué les étapes 1 à 3, vous ne pouvez pas déterminer avec certitude que l’attaque est sans gravité, considérez qu’il s’agit d’une attaque malveillante.

**Correction**

Assurez-vous que les comptes Honeytoken sont utilisés uniquement pour leur rôle prévu afin d’éviter la génération de nombreuses alertes.

## <a name="malicious-request-of-data-protection-api-master-key"></a>Demande malveillante de la clé principale de l’API de protection des données
<a name="malicious-data-protection-private-information-request"></a>

*Nom précédent :* Demande d’information privée de protection contre les données malveillantes

**Description**

L’API de protection des données (DPAPI) est utilisée par Windows pour protéger les mots de passe enregistrés par les navigateurs, les clés de chiffrement et d’autres données sensibles. Les contrôleurs de domaine détiennent une clé principale de sauvegarde qui peut être utilisée pour déchiffrer tous les secrets chiffrés avec DPAPI sur des machines Windows jointes au domaine. Des attaquants peuvent utiliser cette clé principale pour déchiffrer les secrets protégés avec DPAPI sur toutes les machines jointes au domaine.
Cette détection déclenche une alerte quand DPAPI est utilisé pour récupérer la clé principale de sauvegarde.

**Examen**

1. L’ordinateur source exécute-t-il un scanner de sécurité approuvé par l’organisation dans Active Directory ?

2. Si c’est le cas et si ce comportement est normal, **fermez et excluez** l’activité suspecte.

3. Si c’est le cas, mais que ce comportement n’est pas normal, **fermez** l’activité suspecte.

**Correction**

Pour pouvoir utiliser DPAPI, un attaquant doit avoir les droits d’administrateur de domaine. Suivez les  [recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="suspected-brute-force-attack-ldap"></a>Suspicion d’attaque par force brute (LDAP) 
<a name="brute-force-attack-using-ldap-simple-bind"></a>
*Nom précédent :* Attaque par force brute à l'aide d'une liaison simple LDAP

**Description**

>[!NOTE]
> La principale différence entre les **échecs d’authentification suspects** et cette détection est que celle-ci permet à Azure ATP de déterminer si des mots de passe différents ont été utilisés.

Dans une attaque par force brute, un attaquant tente de s’authentifier en essayant plusieurs mots de passe pour différents comptes jusqu’à ce qu’il trouve le bon mot de passe de l’un des comptes. Une fois qu’il a deviné le mot de passe d’un compte, l’attaquant utilise ce compte pour se connecter au réseau.

Dans cette détection, une alerte est déclenchée quand Azure ATP détecte un nombre massif d’authentifications de liaison simple. L’attaque peut être *horizontale* avec un petit nombre de mots de passe possibles pour de nombreux utilisateurs, *verticale* avec un grand nombre de mots de passe pour seulement quelques utilisateurs, ou à la fois horizontale et verticale.

**Examen**

1. Si de nombreux comptes sont concernés, cliquez sur **Télécharger les détails** pour afficher la liste complète dans une feuille de calcul Excel.

2. Cliquez sur l’alerte pour accéder à la page associée. Déterminez si des tentatives de connexion ont donné lieu à une authentification. Les tentatives s’affichent en tant que **Comptes devinés** à droite des données graphiques. Si des comptes devinés sont affichés, font-ils partie des **comptes devinés** normalement utilisés à partir de l’ordinateur source ? Si c’est le cas, **supprimez** l’activité suspecte.

3. S’il n’y a pas de **comptes devinés** affichés, s’agit-il de **comptes attaqués** normalement utilisés à partir de l’ordinateur source ? Si c’est le cas, **supprimez** l’activité suspecte.

**Correction**

Les [mots de passe longs et complexes](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) assurent le niveau minimum de sécurité nécessaire contre les attaques par force brute.

## <a name="suspected-brute-force-attack-kerberos-ntlm"></a>Suspicion d’attaque par force brute (Kerberos, NTLM)
<a name="suspicious-authentication-failures"></a>

*Nom précédent :* Échecs d’authentification suspects

**Description**

Dans une attaque par force brute, l’attaquant tente de s’authentifier avec plusieurs mots de passe auprès de différents comptes, jusqu'à ce qu’un mot de passe correct soit trouvé, ou avec un mot de passe dans une attaque par pulvérisation de mots de passe à grande échelle qui fonctionne au moins pour un compte. Lorsqu’un mot de passe est trouvé, l’attaquant se connecte en utilisant le compte authentifié.

Dans cette détection, une alerte est déclenchée lorsque de nombre d’échecs d’authentification se produisent à l’aide de la méthode Kerberos ou NTLM, ou lorsque une pulvérisation de mots de passe est détectée. Avec Kerberos ou NTLM, cette attaque peut être généralement horizontale, avec un petit nombre de mots de passe possibles pour de nombreux utilisateurs, verticale, avec un grand nombre de mots de passe pour seulement quelques utilisateurs, ou à la fois horizontale et verticale. Dans une pulvérisation de mots de passe, après avoir correctement dressé la liste des utilisateurs valides à partir du contrôleur de domaine, les attaquants tentent d’utiliser UN mot de passe élaboré avec soin sur tous les comptes d’utilisateur connus (un mot de passe sur de nombreux comptes). Si la pulvérisation de mots de passe initiale échoue, ils réessayent en utilisant un autre mot de passe élaboré avec soin, généralement après avoir attendu 30 minutes entre les tentatives. Ce délai d’attente évite aux attaquants de déclencher la plupart des seuils de verrouillage de compte temporels. La pulvérisation de mots de passe est rapidement devenue la technique préférée des pirates et des tests d’intrusion. Les attaques par pulvérisation de mots de passe se sont révélées efficaces pour créer une brèche dans une organisation et pour effectuer des déplacements latéraux afin d’essayer d’élever des privilèges. 

**Période d’apprentissage** : le délai minimal avant le déclenchement d’une alerte est d’une semaine.

**Examen**

1.  Cliquez sur **Télécharger les détails** pour voir toutes les informations dans une feuille de calcul Excel. Les informations suivantes sont disponibles : 
   -    Liste des comptes attaqués
   -    Liste des comptes devinés dans lesquels des tentatives de connexion se sont terminées par une authentification réussie
   -    Activités des événements concernés si les tentatives d’authentification ont été effectuées à l’aide de NTLM 
   -    Activités réseau associées si les tentatives d’authentification ont été effectuées à l’aide de Kerberos
   -  Activités réseau associées si les tentatives d’authentification ont été effectuées à l’aide d’une pulvérisation de mots de passe

2.  Cliquez sur l’ordinateur source pour accéder à sa page de profil. Vérifiez ce qui s’est passé à peu près au même moment que ces tentatives, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté et a accédé à quelles ressources. Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge Windows Defender ATP](./media/wd-badge.png) pour examiner davantage l’ordinateur. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte. 

3.  Si l’authentification a été effectuée avec NTLM, que vous voyez que l’alerte se produit de nombreuses fois et qu’il n’y a pas suffisamment d’informations disponibles sur le serveur auquel l’ordinateur source a tenté d’accéder, activez l’**audit NTLM** sur les contrôleurs de domaine concernés. Pour cela, activez l’événement 8004. Il s’agit de l’événement d’authentification NTLM qui inclut des informations sur l’ordinateur source, le compte d’utilisateur et le **serveur auquel l’ordinateur source a tenté d’accéder. Une fois que vous savez quel serveur a envoyé la validation de l’authentification, examinez le serveur en vérifiant ses événements tels que 4624 pour mieux comprendre le processus d’authentification. 

**Correction**

Les [mots de passe longs et complexes](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) assurent le niveau minimum de sécurité nécessaire contre les attaques par force brute.

## <a name="suspected-dcshadow-attack-dc-promotion"></a>Suspicion d'attaque DCShadow (promotion du contrôleur de domaine)
<a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>

*Nom précédent :* Promotion du contrôleur de domaine suspect (attaque DcShadow potentielle)

**Description**

Une attaque DCShadow (« Domain Controller Shadow ») est une attaque conçue pour modifier des objets annuaire par réplication malveillante. Elle consiste à créer, sur n’importe quel ordinateur, un contrôleur de domaine non autorisé suivant un processus de réplication.
 
DCShadow utilise les protocoles RPC et LDAP pour :
1. Enregistrer le compte d’ordinateur comme contrôleur de domaine (à l’aide de droits d’administrateur de domaine).
2. Effectuer la réplication (grâce aux droits de réplication accordés) sur DRSUAPI et envoyer les modifications aux objets annuaire.
 
Dans cette détection, une alerte est déclenchée lorsqu’un ordinateur du réseau tente de s’enregistrer comme contrôleur de domaine non autorisé. 

**Examen**
 
1. L’ordinateur en question est-il un contrôleur de domaine ? Par exemple, un contrôleur de domaine récemment promu ayant rencontré des problèmes de réplication. Si c’est le cas, **fermez** l’activité suspecte.
2. L’ordinateur en question est-il supposé répliquer des données à partir d’Active Directory ? Par exemple, Azure AD Connect. Si c’est le cas, **fermez et excluez** l’activité suspecte.
3. Cliquez sur l’ordinateur source ou le compte pour accéder à sa page de profil. Regardez ce qui s’est passé à peu près au même moment que la réplication, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté, à quelles ressources et avec quel système d’exploitation.
   1. Tous les utilisateurs connectés à l’ordinateur sont-ils censés l’être ? Quels sont leurs privilèges ? Ont-ils l’autorisation de promouvoir un serveur comme contrôleur de domaine (sont-ils administrateurs de domaine) ?
   2. Ces utilisateurs sont-ils censés avoir accès à ces ressources ?
   3. L’ordinateur fonctionne-t-il sous le système d’exploitation Windows Server (ou Windows/Linux) ? Un ordinateur qui n’est pas un serveur n’est pas censé répliquer des données.
Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge Windows Defender ATP](./media/wd-badge.png) pour explorer la machine plus en détail. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte.

4. Dans l’observateur d’événements, consultez les [événements Active Directory qu’il enregistre dans le journal des Services d’annuaire](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/). Vous pouvez utiliser le journal pour contrôler les modifications dans Active Directory. Par défaut, Active Directory n’enregistre que les événements d’erreur critique ; cependant, si cette alerte se reproduit, activez cet audit sur le contrôleur de domaine correspondant pour un examen approfondi.

**Corriger**

Renseignez-vous pour savoir quels utilisateurs de votre organisation disposent des autorisations suivantes : 
- Répliquer les changements d’annuaire 
- Répliquer tous les changements d’annuaire 
 
 
Pour plus d’informations, consultez [Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx). 

Vous pouvez utiliser [l’analyseur AD ACL](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou créer un script Windows PowerShell pour déterminer qui a ces autorisations dans le domaine.
 
> [!NOTE]
> Les alertes de promotion suspecte de contrôleur de domaine (attaque DCShadow potentielle) sont prises en charge par les capteurs ATP uniquement. 

## <a name="suspected-dcshadow-attack-dc-replication-request"></a>Suspicion d’attaque DCShadow (demande de réplication du contrôleur de domaine)
<a name="suspicious-replication-request-potential-dcshadow-attack"></a>

*Nom précédent :* Demande de réplication suspecte (attaque DcShadow potentielle) 

**Description** 

La réplication Active Directory est le processus par lequel les modifications apportées à un contrôleur de domaine sont synchronisées avec d’autres contrôleurs de domaine. Disposant des autorisations nécessaires, les attaquants peuvent accorder des droits pour leur compte d’ordinateur, ce qui leur permet d’emprunter l’identité d’un contrôleur de domaine. Ils s’efforcent de lancer une demande de réplication malveillante, ce qui leur permet de modifier des objets Active Directory sur un contrôleur de domaine authentique et d’obtenir une persistance dans le domaine.
Dans cette détection, une alerte est déclenchée lorsqu’une demande de réplication suspecte est générée par rapport à un contrôleur de domaine authentique protégé par Azure ATP. Le comportement est révélateur de certaines techniques utilisées dans les attaques DCShadow.

**Examen** 
 
1. L’ordinateur en question est-il un contrôleur de domaine ? Par exemple, un contrôleur de domaine récemment promu ayant rencontré des problèmes de réplication. Si c’est le cas, **fermez** l’activité suspecte.
2. L’ordinateur en question est-il supposé répliquer des données à partir d’Active Directory ? Par exemple, Azure AD Connect. Si c’est le cas, **fermez et excluez** l’activité suspecte.
3. Cliquez sur l’ordinateur source pour accéder à sa page de profil. Regardez ce qui s’est passé **à peu près au même moment** que la réplication, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté, quelles ressources ont été utilisées et quel système d’exploitation possède l’ordinateur.

   1.  Tous les utilisateurs connectés à l’ordinateur sont-ils censés l’être ? Quels sont leurs privilèges ? Ont-ils l’autorisation d’effectuer des réplications (sont-ils administrateurs de domaine) ?
   2.  Ces utilisateurs sont-ils censés avoir accès à ces ressources ?
   3. L’ordinateur fonctionne-t-il sous le système d’exploitation Windows Server (ou Windows/Linux) ? Un ordinateur qui n’est pas un serveur n’est pas censé répliquer des données.
Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge Windows Defender ATP](./media/wd-badge.png) pour explorer la machine plus en détail. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte.
1. Dans l’observateur d’événements, consultez les [événements Active Directory qu’il enregistre dans le journal des Services d’annuaire](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/). Vous pouvez utiliser le journal pour contrôler les modifications dans Active Directory. Par défaut, Active Directory n’enregistre que les événements d’erreur critique ; cependant, si cette alerte se reproduit, activez cet audit sur le contrôleur de domaine correspondant pour un examen approfondi.

**Correction**

Renseignez-vous pour savoir quels utilisateurs de votre organisation disposent des autorisations suivantes : 
- Répliquer les changements d’annuaire 
- Répliquer tous les changements d’annuaire 

Vous pouvez utiliser [l’analyseur AD ACL](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou créer un script Windows PowerShell pour déterminer qui a ces autorisations dans le domaine.

> [!NOTE]
> Les alertes de demande de réplication suspecte (attaque DCShadow potentielle) sont prises en charge par les capteurs ATP uniquement. 

## <a name="suspected-dcsync-attack-replication-of-directory-services"></a>Suspicion d’attaque DCSync (réplication de services d’annuaire)
<a name="malicious-replication-of-directory-services"></a>

*Nom précédent :* Réplication malveillante de services d’annuaire

**Description**

La réplication Active Directory est le processus par lequel les modifications apportées à un contrôleur de domaine sont synchronisées avec tous les autres contrôleurs de domaine. Quand les attaquants ont les autorisations nécessaires, ils peuvent lancer une demande de réplication dans le but de récupérer ensuite les données stockées dans Active Directory, y compris les hachages de mot de passe.

Dans cette détection, une alerte est déclenchée quand une demande de réplication est lancée à partir d’un ordinateur qui n’est pas un contrôleur de domaine.

**Examen**

> [!NOTE]
> Si vous avez des contrôleurs de domaine sur lesquels les capteurs Azure ATP ne sont pas installés, ces contrôleurs de domaine ne sont pas couverts par Azure ATP. Dans ce cas, si vous déployez un nouveau contrôleur de domaine sur un contrôleur de domaine non inscrit ou non protégé, il peut ne pas être identifié par Azure ATP comme contrôleur de domaine dans un premier temps. Il est vivement recommandé d’installer le capteur Azure ATP sur chaque contrôleur de domaine pour obtenir une couverture complète.

1. L’ordinateur en question est-il un contrôleur de domaine ? Par exemple, un contrôleur de domaine récemment promu ayant rencontré des problèmes de réplication. Si c’est le cas, **fermez** l’activité suspecte. 
2.  L’ordinateur en question est-il supposé répliquer des données à partir d’Active Directory ? Par exemple, Azure AD Connect ou des appareils de monitoring des performances réseau. Si c’est le cas, **fermez et excluez** l’activité suspecte.
3. L’adresse IP à partir de laquelle la demande de réplication a été envoyée est-elle un NAT ou un proxy ? Si c’est le cas, vérifiez s’il existe un nouveau contrôleur de domaine derrière l’appareil ou si d’autres activités suspectes se sont produites à partir de celui-ci. 

4. Cliquez sur l’ordinateur source ou le compte pour accéder à sa page de profil. Vérifiez ce qui s’est passé à peu près au même moment que la réplication, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté et a accédé à quelles ressources. Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge Windows Defender ATP](./media/wd-badge.png) pour examiner davantage l’ordinateur. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte. 


**Correction**

Vérifiez les autorisations suivantes : 

- Répliquer les changements d’annuaire   

- Répliquer tous les changements d’annuaire  

Pour plus d’informations, consultez  [Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).
Vous pouvez utiliser l’ [analyseur AD ACL](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/)  ou créer un script Windows PowerShell pour savoir qui possède ces autorisations dans le domaine.

## <a name="suspected-golden-ticket-usage-encryption-downgrade"></a>Suspicion d’utilisation de golden ticket (passage à une version antérieure du chiffrement)
<a name="Encryption-downgrade-activity-potential-golden-ticket-attack"></a>

*Nom précédent :* Activité de chiffrement du passage à une version antérieure

**Description** : Le passage à une version inférieure du chiffrement est une méthode visant à affaiblir Kerberos en abaissant le niveau de chiffrement de différents champs du protocole qui sont chiffrés avec le niveau de chiffrement le plus élevé. Un champ au chiffrement affaibli peut être plus vulnérable à des attaques de force brute en mode hors connexion. Plusieurs méthodes d’attaque exploitent les codes faibles de chiffrement Kerberos. Dans cette détection, Azure ATP examine les types de chiffrement Kerberos utilisés par les ordinateurs et les utilisateurs, et déclenche des alertes quand un chiffrement plus faible est utilisé : (1) qui est inhabituel pour l’ordinateur source et/ou l’utilisateur ; et (2) qui correspond à une technique d’attaque connue. 

Dans une alerte Golden Ticket, la méthode de chiffrement du champ TGT du message TGS_REQ (demande de service) reçu de l’ordinateur source a été passée à une version inférieure par rapport au comportement appris. Cette détection n’est pas basée sur une anomalie de temps (contrairement à l’autre détection Golden Ticket). De plus, ATP n’a pas détecté de demande d’authentification Kerberos associée à la demande de service précédente.

**Examen**
1. Certaines ressources ne prennent pas en charge les méthodes de chiffrement fort et peuvent déclencher cette alerte.
   1. Vérifiez les ressources auxquelles ces tickets ont accédé. Vérifiez cela dans Active Directory en consultant l’attribut *msDS-SupportedEncryptionTypes* du compte de service de la ressource.
   2. S’il existe une ressource ayant fait l’objet d’un accès, vérifiez-la. Vérifiez que c’est une ressource valide à laquelle ils sont censés accéder. 
2. Les applications personnalisées peuvent s’authentifier avec un cipher de chiffrement plus faible.
   1. Vérifiez s’il existe des applications personnalisées qu s’authentifient avec un cipher de chiffrement plus faible sur l’ordinateur source.
   2. S’il existe plusieurs utilisateurs, vérifiez s’ils ont quelque chose en commun. <br>Par exemple, il se peut que tout le personnel du marketing utilise une application spécifique qui déclencherait l’alerte.
3. Cliquez sur l’ordinateur source ou le compte pour accéder à sa page de profil. Vérifiez ce qui s’est passé au moment de la réplication. Recherchez d’éventuelles activités inhabituelles, comme qui s’est connecté et quelles ressources ont fait l’objet d’un accès. 

4. Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge Windows Defender ATP](./media/wd-badge.png) pour examiner davantage l’ordinateur. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte.

**Correction**

1. Redéfinissez le mot de passe pour les utilisateurs compromis.
2. Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine : planifiez donc cette opération avec soin.

## <a name="suspected-golden-ticket-usage-forged-authorization-data"></a>Suspicion d’utilisation de golden ticket (données d’autorisation falsifiées)
<a name="privilege-escalation-using-forged-authorization-data"></a>

*Nom précédent :* Réaffectation de privilèges à l’aide de données d’autorisation falsifiées

**Description**

Des vulnérabilités connues dans les versions antérieures de Windows Server permettent aux attaquants de manipuler le certificat PAC (Privileged Attribute Certificate). PAC est un champ du ticket Kerberos qui contient des données d’autorisation utilisateur (dans Active Directory, il s’agit de l’appartenance au groupe) et qui accorde des privilèges supplémentaires aux attaquants.

**Examen**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante.

2. Le correctif MS14-068 (contrôleur de domaine) ou MS11-013 (serveur) a-t-il été installé sur l’ordinateur de destination (sous la colonne **ACCESSED**) ? Si c’est le cas, **fermez** l’activité suspecte (c’est un faux positif).

3. Sinon, l’ordinateur source s’exécute (sous la colonne **FROM**) exécute-t-il un système d’exploitation ou une application connu pour modifier le certificat PAC ? Si c’est le cas, **supprimez** l’activité suspecte (c’est un vrai positif sans gravité).

4. Si vous avez répondu non aux deux questions ci-dessus, considérez l’alerte comme une attaque malveillante.

**Correction**

Vérifiez que tous les contrôleurs de domaine dotés du système d’exploitation Windows Server 2012 R2 ou version antérieure sont installés avec  [withKB3011780and](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege)  et que tous les serveurs et contrôleurs de domaine membres avec 2012 R2 ou version antérieure sont à jour avec KB2496930. Pour plus d’informations, consultez  [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx)  et  [Faux PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="suspected-golden-ticket-usage-nonexistant-account"></a>Suspicion d’utilisation de golden ticket (compte inexistant)
<a name="golden-ticket"></a>

Nom précédent : Golden Ticket Kerberos

**Description**

Les attaquants obtenant des droits d’administrateur de domaine peuvent compromettre le compte KRBTGT. Avec le compte KRBTGT, les attaquants peuvent créer un ticket TGT Kerberos qui fournit une autorisation sur n’importe quelle ressource. Un ticket TGT falsifié de ce type est appelé « Golden Ticket », car il permet aux attaquants d’obtenir une persistance réseau durable. Dans cette détection, une alerte est déclenchée par l’utilisation d’un compte qui n’existe pas.

**Examen**

1. Posez les questions suivantes :
      - L’utilisateur est-il un utilisateur de domaine connu et valide ? Si c’est le cas, fermez l’alerte, car il s’agit d’un faux positif.
      - L’utilisateur a-t-il été récemment ajouté ? Si c’est le cas, fermez l’alerte, car le changement n’a peut-être pas été encore été synchronisé.
      - L’utilisateur a-t-il été récemment supprimé d’AD ? Si c’est le cas, fermez l’alerte.
2. Si vous avez répondu non aux deux questions ci-dessus, considérez l’alerte comme une attaque malveillante.

3. Cliquez sur l’ordinateur source pour accéder à sa page **Profil**. Vérifiez ce qui s’est passé à peu près au même moment que l’activité, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté et a accédé à quelles ressources ? 

4. Tous les utilisateurs connectés à l’ordinateur sont-ils censés l’être ? Quels sont leurs privilèges ? 

5. Les utilisateurs connectés sont-ils censés avoir accès à ces ressources ?<br>
Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP.
 
 1. Pour un examen approfondi de l’ordinateur, vérifiez quels processus et quelles alertes se sont produits au moment de l’alerte dans Windows Defender ATP.

**Correction**


Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. De plus, du fait que la création d’un Golden Ticket nécessite des droits d’administrateur de domaine, suivez les [recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="suspected-golden-ticket-usage-time-anomaly"></a>Suspicion d’utilisation de golden ticket (anomalie de temps)

Nom précédent : Golden Ticket Kerberos

**Description**

Les attaquants obtenant des droits d’administrateur de domaine peuvent compromettre le compte [KRBTGT](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). Avec le compte KRBTGT, les attaquants peuvent créer un ticket TGT (Ticket Granting Ticket) Kerberos qui fournit une autorisation d’accès à toutes les ressources, et définir l’heure d’expiration du ticket à une valeur de leur choix. Un ticket TGT falsifié de ce type est appelé « Golden Ticket », car il permet aux attaquants d’obtenir une persistance réseau durable. Cette détection déclenche une alerte quand un ticket TGT Kerberos est utilisé depuis plus longtemps que la durée autorisée telle qu’elle est spécifiée dans [Durée de vie maximale du ticket utilisateur](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx).


**Examen**

1. Le paramètre Durée de vie maximale du ticket utilisateur défini dans la stratégie de sécurité a-t-il été modifié récemment (au cours des dernières heures) ? Vérifiez la valeur spécifique pour voir si elle est inférieure à la durée pendant laquelle le ticket a été utilisé. Si c’est le cas, fermez l’alerte, car il s’agit d’un faux positif.

2. Le capteur Azure ATP impliqué dans cette alerte est-il une machine virtuelle ? Si c’est le cas, son exécution a-t-elle repris à partir d’un état de mise en mémoire ? Si c’est le cas, fermez l’alerte.

3. Si vous avez répondu non aux deux questions ci-dessus, considérez l’alerte comme une attaque malveillante.

**Correction**


Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. De plus, du fait que la création d’un Golden Ticket nécessite des droits d’administrateur de domaine, suivez les [recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="suspected-golden-ticket-usage-ticket-anomaly---preview"></a>Suspicion d’utilisation de golden ticket (anomalie de ticket) - préversion
<a name="golden-ticket-usage-ticket-anomaly
"></a>

**Description**

Les attaquants ayant des droits d’administrateur de domaine peuvent compromettre le compte KRBTGT. Avec le compte KRBTGT, ils peuvent créer un ticket TGT Kerberos qui fournit une autorisation sur n’importe quelle ressource. Un ticket TGT falsifié de ce type est appelé « Golden Ticket », car il permet aux attaquants d’obtenir une persistance réseau durable. Les golden tickets falsifiées de ce type ont des caractéristiques uniques qui peuvent être identifiées par cette détection. 

**Examen**
1. Les services de fédération peuvent générer des tickets qui déclencheront cette alerte. L’ordinateur source héberge-t-il des services de ce type ? Si oui, fermez l’alerte de sécurité.
2. Cliquez sur l’utilisateur source pour accéder à sa page de profil. Vérifiez ce qui s’est passé au moment de l’activité.
      1. L’utilisateur est-il supposé avoir accès (autorisation) à cette ressource ? 
      2.  Le principal est-il censé accéder à ce service ? 
3. Cliquez sur l’ordinateur source pour accéder à sa page de profil. Vérifiez ce qui s’est passé au moment de l’activité et recherchez des activités inhabituelles, notamment les personnes qui se sont connectées et les ressources auxquelles elles ont accédé. 
4. Tous les utilisateurs qui se sont connectés à l’ordinateur sont-ils censés l’être ? Quels sont leurs privilèges ? 
5. Les utilisateurs qui se sont connectés sont-ils censés avoir accès aux ressources auxquelles ils se sont connectés ?
<br>Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP.
6. Pour un examen approfondi de l’ordinateur, vérifiez quels processus et quelles alertes se sont produits au moment de l’alerte dans Windows Defender ATP.


**Correction**

Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier soigneusement cette opération. De plus, du fait que la création d’un Golden Ticket nécessite des droits d’administrateur de domaine, suivez les [recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="suspected-identity-theft-pass-the-hash"></a>Suspicion d'usurpation d’identité (pass-the-hash) 
<a name="identity-theft-using-pass-the-hash-attack"></a>

*Nom précédent :* Usurpation d’identité par attaque pass-the-hash

**Description**

Pass-the-Hash est une technique de mouvement latéral par laquelle les attaquants volent le code de hachage NTLM d’un utilisateur sur un ordinateur et utilisent ensuite ce code pour accéder à un autre ordinateur. 

**Examen**

Vérifiez si le hachage provient d’un ordinateur que l’utilisateur ciblé possède ou utilise régulièrement. Si oui, l’alerte est un faux positif ; sinon, il s’agit probablement d’un vrai positif.

**Correction**

1. Si le compte concerné n’est pas un compte sensible, réinitialisez le mot de passe de ce compte. Cela empêche l’attaquant de créer d’autres tickets Kerberos à partir du hachage de mot de passe. Toutefois, les tickets existants resteront utilisables jusqu’à leur expiration. 

2. S’il s’agit d’un compte sensible, envisagez de réinitialiser deux fois le compte KRBTGT. Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. Consultez les conseils fournis dans l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et utilisez  [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Dans la mesure où il s’agit d’une technique de mouvement latéral, suivez les bonnes pratiques indiquées dans [Recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="suspected-identity-theft-pass-the-ticket"></a>Suspicion d’usurpation d’identité (pass-the-ticket) 
<a name="identity-theft-using-pass-the-ticket-attack"></a>

*Nom précédent :* Usurpation d’identité par attaque pass-the-ticket

**Description**

Pass-the-Ticket est une technique de mouvement latéral par laquelle les attaquants volent un ticket Kerberos sur un ordinateur et réutilisent ensuite ce ticket pour accéder à un autre ordinateur. Cette détection vérifie si un ticket Kerberos a été utilisé sur plusieurs ordinateurs différents.

**Examen**

1. Cliquez sur le bouton **Télécharger les détails** pour afficher la liste complète des adresses IP impliquées. L’adresse IP de l’un ou des deux ordinateurs appartient-elle à un sous-réseau alloué à partir d’un pool DHCP de taille insuffisante, par exemple, VPN ou WiFi ? L’adresse IP est-elle partagée ? Par exemple, par un appareil NAT ? Une ou plusieurs des adresses IP sources sont-elles non résolues par le capteur ? (Cela peut indiquer que les ports appropriés du capteur vers les périphériques ne sont pas correctement ouverts.) Si vous répondez par l’affirmative à l’une de ces questions, il s’agit d’un faux positif.

2. Y a-t-il une application personnalisée qui transfère les tickets pour le compte d’utilisateurs ? Si c’est le cas, il s’agit d’un vrai positif.

**Correction**

1. Si le compte concerné n’est pas un compte sensible, réinitialisez le mot de passe de ce compte. Cela empêche l’attaquant de créer d’autres tickets Kerberos à partir du hachage de mot de passe. Toutefois, les tickets existants resteront utilisables jusqu’à leur expiration.  

2. S’il s’agit d’un compte sensible, envisagez de réinitialiser deux fois le compte KRBTGT. Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. Consultez les conseils fournis dans l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et utilisez  [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Dans la mesure où il s’agit d’une technique de mouvement latéral, suivez les bonnes pratiques indiquées dans [Recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="suspected-over-pass-the-hash-attack-encryption-downgrade"></a>Suspicion d'attaque over-pass-the-hash (passage à une version antérieure du chiffrement) 
<a name="Encryption-downgrade-activity-potential-over-pass-the-hash"></a>

*Nom précédent :* Activité de chiffrement du passage à une version antérieure

**Description**

Le passage à une version inférieure du chiffrement est une méthode visant à affaiblir Kerberos en abaissant le niveau de chiffrement de différents champs du protocole qui sont chiffrés avec le niveau de chiffrement le plus élevé. Un champ au chiffrement affaibli peut être plus vulnérable à des attaques de force brute en mode hors connexion. Plusieurs méthodes d’attaque exploitent les codes faibles de chiffrement Kerberos. Dans cette détection, Azure ATP examine les types de chiffrement Kerberos utilisés par les ordinateurs et les utilisateurs, et déclenche des alertes quand un chiffrement plus faible est utilisé : (1) qui est inhabituel pour l’ordinateur source et/ou l’utilisateur ; et (2) qui correspond à une technique d’attaque connue. 

Dans une attaque over-pass-the-hash, un attaquant peut utiliser un code de hachage faible dérobé pour créer un ticket fort avec une demande Kerberos AS. Dans le cadre de cette détection, le type de chiffrement du message AS_REQ reçu de l’ordinateur source a été abaissé par rapport au comportement appris (l’ordinateur utilisait l’algorithme AES).

**Examen**

1. La configuration de la carte à puce a-t-elle été changée récemment ? <br>Vérifiez si des changements de ce type ont été apportés pour les comptes concernés. Si c’est le cas, l’alerte est probablement un vrai positif sans gravité et peut être supprimée.
2. Certaines ressources ne prennent pas en charge les méthodes de chiffrement fort. Des méthodes de chiffrement faible peuvent déclencher cette alerte.<br>Vérifiez les ressources auxquelles ces tickets ont accédé. Vérifiez cela dans Active Directory en consultant l’attribut *msDS-SupportedEncryptionTypes* du compte de service de la ressource.<br>S’il existe une ressource ayant fait l’objet d’un accès, vérifiez-la. Vérifiez que c’est une ressource valide à laquelle ils sont censés accéder. 
3. Cliquez sur l’ordinateur source ou le compte pour accéder à sa page de profil. Vérifiez ce qui s’est passé à peu près au même moment que la réplication, en recherchant d’éventuelles activités inhabituelles, notamment qui s’est connecté et quelles ressources ont fait l’objet d’un accès. <br> Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge Windows Defender ATP](./media/wd-badge.png) pour examiner davantage l’ordinateur. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte.


**Correction**
1. Si l’utilisateur compromis *n’est pas un utilisateur sensible*, réinitialisez le mot de passe de ce compte. Cela empêche l’attaquant de créer d’autres tickets Kerberos à partir du hachage de mot de passe. Toutefois, les tickets existants resteront utilisables jusqu’à leur expiration. 
2. Si l’utilisateur compromis est *un utilisateur sensible*, envisagez de réinitialiser le compte KRBTGT à deux reprises. Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine : planifiez donc cette opération avec soin. Consultez les conseils fournis dans l’article [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients). Utilisez également [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).

## <a name="suspected-skeleton-key-attack-encryption-downgrade"></a>Suspicion d’attaque Skeleton Key (passage à une version antérieure du chiffrement) 
<a name="encryption-downgrade-activity-potential-skeleton-key-attack"></a>

*Nom précédent :* Activité de chiffrement du passage à une version antérieure

**Description** : Le passage à une version inférieure du chiffrement est une méthode visant à affaiblir Kerberos en abaissant le niveau de chiffrement de différents champs du protocole qui sont chiffrés avec le niveau de chiffrement le plus élevé. Un champ au chiffrement affaibli peut être plus vulnérable à des attaques de force brute en mode hors connexion. Plusieurs méthodes d’attaque exploitent les codes faibles de chiffrement Kerberos. Dans cette détection, Azure ATP examine les types de chiffrement Kerberos utilisés par les ordinateurs et les utilisateurs, et déclenche des alertes quand un chiffrement plus faible est utilisé : (1) qui est inhabituel pour l’ordinateur source et/ou l’utilisateur ; et (2) qui correspond à une technique d’attaque connue. 

Skeleton Key est un programme malveillant qui s’exécute sur les contrôleurs de domaine et qui autorise l’authentification auprès du domaine de n’importe quel compte sans connaître son mot de passe. Il utilise souvent des algorithmes de chiffrement plus faibles pour hacher les mots de passe de l’utilisateur sur le contrôleur de domaine. Dans le cadre de cette détection, la méthode de chiffrement du message KRB_ERR adressé par le contrôleur de domaine au compte demandant un ticket a été abaissée par rapport au comportement appris.

**Examen**
1. Cliquez sur l’ordinateur source ou le compte pour accéder à sa page de profil. <br>Vérifiez ce qui s’est passé à peu près au même moment que la réplication, en recherchant d’éventuelles activités inhabituelles, notamment qui s’est connecté et quelles ressources ont fait l’objet d’un accès. <br>Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge Windows Defender ATP](./media/wd-badge.png) pour examiner davantage l’ordinateur. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte. 
2. Vérifiez si Skeleton Key a affecté vos contrôleurs de domaine avec l’[analyseur écrit par l’équipe Azure ATP](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73).


**Correction**
1. Supprimez les programmes malveillants. Pour plus d’informations sur la suppression des programmes malveillants, consultez [Analyse des programmes malveillants Skeleton Key](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).


## <a name="network-mapping-reconnaissance-dns"></a>Reconnaissance de mappage de réseau (DNS)
<a name="reconnaissance-using-dns"></a>

Reconnaissance à l’aide de DNS

**Description**

Votre serveur DNS contient une carte de l’ensemble des ordinateurs, adresses IP et services de votre réseau. Ces informations sont utilisées par les attaquants pour mapper la structure de votre réseau et cibler les ordinateurs intéressants pour les étapes suivantes de l’attaque.

Il existe plusieurs types de requêtes dans le protocole DNS. Azure ATP détecte les demandes de transfert AXFR provenant de serveurs autres que DNS.

**Examen**

1. La machine source (**En provenance de…**) est-elle un serveur DNS ? Si c’est le cas, il s’agit probablement d’un faux positif. Pour le vérifier, cliquez sur l’alerte pour accéder à la page de détails correspondante. Dans le tableau, sous **Requête**, vérifiez quels domaines ont été interrogés. S’agit-il de domaines existants ? Si c’est le cas, **fermez** l’activité suspecte (c’est un faux positif). De plus, assurez-vous que le port UDP 53 est ouvert entre le capteur autonome Azure ATP et l’ordinateur source pour éviter de futurs faux positifs.

2. L’ordinateur source exécute-t-il un scanner de sécurité ? Si c’est le cas, **excluez les entités** dans ATP, soit directement en choisissant **Fermer et exclure**, soit via la page **Exclusion** (sous **Configuration**, disponible pour les administrateurs d’Azure ATP).

3. Si la réponse à toutes les questions précédentes est non, continuez à chercher en vous concentrant sur l’ordinateur source. Cliquez sur l’ordinateur source pour accéder à sa page de profil. Vérifiez ce qui s’est passé à peu près au même moment que la requête, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté et a accédé à quelles ressources. Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge Windows Defender ATP](./media/wd-badge.png) pour examiner davantage l’ordinateur. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte. 

**Correction**

La sécurisation d’un serveur DNS interne pour éviter la reconnaissance à l’aide de DNS est possible en désactivant les transferts de zone ou en les limitant uniquement aux adresses IP spécifiées. Pour plus d’informations sur la limitation des transferts de zone, consultez [Restrict Zone Transfers](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx) (Limiter les transferts de zone).
La modification des transferts de zone est l’une des tâches de la liste de contrôle que vous devez suivre pour  [sécuriser vos serveurs DNS contre les attaques internes et externes](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).

## <a name="remote-code-execution-attempt"></a>Tentative d’exécution de code à distance
<a name="remote-code-execution-attempt"></a>
*Nom précédent :* Tentative d’exécution de code à distance

**Description**

Les attaquants qui compromettent les informations d’identification d’administration ou qui exploitent une faille de sécurité de type zero-day peuvent exécuter des commandes à distance sur votre contrôleur de domaine. Cela peut servir pour obtenir une persistance, collecter des informations, lancer des attaques par déni de service (DOS) ou toute autre raison. Azure ATP détecte les connexions PSexec, les connexions WMI à distance et les connexions PowerShell.

**Examen**

1. Cette situation est fréquente pour les stations de travail d’administration, les membres des équipes informatiques et les comptes de service qui effectuent des tâches d’administration sur les contrôleurs de domaine. Si c’est le cas et que l’alerte a été mise à jour du fait qu’elle est effectuée par le même administrateur et/ou ordinateur, **supprimez** l’alerte.

2. **L’ordinateur** en question est-il autorisé à effectuer cette exécution à distance sur votre contrôleur de domaine ?

 - **Le compte** en question est-il autorisé à effectuer cette exécution à distance sur votre contrôleur de domaine ?

 - Si la réponse à ces deux questions est *oui*, **fermez** l’alerte.

3. Si la réponse à l’une de ces questions est non, considérez l’attaque comme un vrai positif. Essayez de rechercher la source de la tentative en vérifiant les profils d’ordinateur et de compte. Cliquez sur l’ordinateur source ou le compte pour accéder à sa page de profil. Vérifiez ce qui s’est passé à peu près au même moment que ces tentatives, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté et a accédé à quelles ressources. Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge Windows Defender ATP](./media/wd-badge.png) pour examiner davantage l’ordinateur. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte. 

**Correction**

1. Limitez l’accès à distance aux contrôleurs de domaine à partir d’ordinateurs qui ne sont pas de niveau 0.

2. Implémentez un  [accès privilégié](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access)  pour autoriser uniquement les machines avec une sécurité renforcée à se connecter aux contrôleurs de domaine pour les administrateurs.

> [!NOTE]
> Les alertes de tentative d’exécution de code à distance sont prises en charge par les capteurs ATP uniquement. 

## <a name="suspicious-communication-over-dns"></a>Communication suspecte sur DNS
<a name="suspicious-communication-over-dns"></a>

*Nom précédent :* Communication suspecte sur DNS 

**Description**

Dans la plupart des organisations, le protocole DNS n’est généralement pas surveillé et les activités malveillantes sont rarement bloquées. Ceci permet à un attaquant sur une machine compromise d’abuser le protocole DNS. Des communications malveillantes via DNS peuvent être utilisées pour l’exfiltration, des commandes et le contrôle des données, et/ou l’affranchissement des limitations du réseau d’entreprise.

**Examen**
> [!NOTE]
> Les alertes de sécurité *Communications suspectes via DNS* indiquent le domaine suspecté. Les nouveaux domaines, ou les domaines récemment ajoutés qui ne sont pas encore connus ou reconnus par Azure ATP, mais qui sont connus de votre organisation ou en font partie, peuvent être fermés. 


1.  Certaines entreprises légitimes utilisent DNS pour les communications régulières. Vérifiez si le domaine de requête inscrit appartient à une source approuvée, comme votre fournisseur d’antivirus. Si le domaine est connu et approuvé, et que les requêtes DNS sont autorisées, l’alerte peut être fermée et le domaine peut être [exclu](excluding-entities-from-detections.md) des alertes futures. 
2.   Si le domaine de requête inscrit n’est pas approuvé, identifiez le processus qui crée la demande sur la machine source. Utilisez le [Moniteur de processus](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon) pour vous aider dans cette tâche.
3.  À quel moment l’activité suspecte a-t-elle commencé ? De nouveaux programmes ont-ils été déployés ou installés dans l’organisation ? Y a-t-il d’autres alertes au même moment ?
4.  Cliquez sur l’ordinateur source pour accéder à la page de son profil. Vérifiez ce qui s’est passé à peu près au même moment que la requête DNS, en recherchant d’éventuelles activités inhabituelles, notamment qui s’est connecté et quelles ressources ont été utilisées. Si vous avez déjà activé l’intégration de Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge Windows Defender ATP](./media/wd-badge.png) pour examiner davantage l’ordinateur. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte.

**Correction**

Si le domaine de requête inscrit n’est pas approuvé après votre investigation, nous vous recommandons de bloquer le domaine de destination afin d’éviter toute communication future. 

## <a name="suspicious-modification-of-sensitive-groups"></a>Modification suspecte de groupes sensibles
<a name="suspicious-midification-of-sensitive-groups"></a>

*Nom précédent :* Modification suspecte de groupes sensibles

**Description**

Des attaquants ajoutent des utilisateurs à des groupes avec des privilèges élevés. Leur but est d’accéder à davantage de ressources et d’obtenir un accès persistant. La détection s’appuie sur le profilage des activités de modification des utilisateurs d’un groupe et déclenche une alerte quand un ajout anormal à un groupe sensible est observé. Azure ATP effectue un profilage en continu. La période minimale avant le déclenchement d’une alerte est d’un mois pour chaque contrôleur de domaine.

Pour obtenir la définition des groupes sensibles dans Azure ATP, consultez [Gestion des comptes sensibles](sensitive-accounts.md).


La détection s’appuie sur les [événements audités sur les contrôleurs de domaine](configure-event-collection.md).
Pour vous assurer que vos contrôleurs de domaine effectuent l’audit des événements requis.

**Examen**

1. La modification du groupe est-elle légitime ? </br>Une modification de groupe légitime qui est peu fréquente ou qui n’a pas été classée comme « normale » pendant l’apprentissage peut déclencher une alerte. Considérez cette alerte comme un vrai positif sans gravité.

2. Si l’objet ajouté est un compte d’utilisateur, déterminez les actions que ce compte a effectuées après son ajout au groupe d’administration. Consultez la page de l’utilisateur dans Azure ATP pour obtenir plus de contexte. D’autres activités suspectes associées au compte ont-elles été effectuées avant ou après l’ajout ? Téléchargez le rapport **Modifications des groupes sensibles** pour examiner toutes les autres modifications effectuées au cours de la même période et déterminer les auteurs de ces modifications.

**Correction**

Réduisez le nombre d’utilisateurs autorisés à modifier les groupes sensibles.

Installez [Privileged Access Management pour les services de domaine Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services), si cela est approprié.

## <a name="suspicious-service-creation"></a>Création de service malveillant
<a name="suspicious-service-creation"></a>

*Nom précédent :* Création de service suspect

**Description**

Un service suspect a été créé sur un contrôleur de domaine dans votre organisation. Cette alerte s’appuie sur l’événement 7045 afin d’identifier cette activité suspecte. 

**Examen**

1. Si l’ordinateur en question est une station de travail d’administration ou un ordinateur sur lequel les membres de l’équipe informatique et les comptes de service effectuent des tâches d’administration, il peut s’agir d’un faux positif et vous pouvez être amené à **supprimer** l’alerte et à l’ajouter à la liste des exclusions, si nécessaire.

2. Reconnaissez-vous ce service sur cet ordinateur ?

 - Le **compte** en question est-il autorisé à installer ce service ?

 - Si la réponse à ces deux questions est *oui*, **fermez** l’alerte ou ajoutez-la à la liste des exclusions.

3. Si la réponse à l’une de ces questions est *non*, considérez l’attaque comme un vrai positif.

**Correction**

- Implémentez un accès doté de moins de privilèges sur les ordinateurs du domaine pour autoriser uniquement des utilisateurs spécifiques à créer de nouveaux services.


## <a name="suspicious-vpn-connection"></a>Connexion VPN suspecte
<a name="suspicious-vpn-detection"></a>

*Nom précédent :* Connexion VPN suspecte 

**Description**

Azure ATP apprend le comportement de l’entité pour les utilisateurs de connexions VPN sur une période mobile d’un mois. 

Le modèle de comportement VPN est basé sur les activités suivantes : les ordinateurs auxquels les utilisateurs se connectent et les emplacements à partir desquels les utilisateurs se connectent. 

Une alerte est ouverte quand il y a un écart entre le comportement de l’utilisateur et l’algorithme d’apprentissage automatique.

**Examen**

1.  L’utilisateur en question est-il supposé effectuer ces opérations normalement ?
2.  Considérez les cas suivants comme faux positifs potentiels : un utilisateur qui a changé d’emplacement, un utilisateur qui est en déplacement et qui se connecte depuis un nouvel appareil.

**Correction**

1.  Réinitialisez le mot de passe de cet utilisateur. Cette opération empêche l’attaquant de créer des connexions VPN avec les anciennes informations d’identification.
2.  Empêchez cet utilisateur de se connecter par VPN.


## <a name="unusual-protocol-implementation"></a>Implémentation de protocole inhabituelle
<a name="unusual-protocol-implementation"></a>

*Nom précédent :* Mise en œuvre de protocole inhabituelle *Ce groupe d’alertes de sécurité sera renommé et de nouveaux externalIds leur seront affectés dans une version future d’Azure ATP*

**Description**

Les attaquants utilisent des outils qui implémentent différents protocoles (SMB, Kerberos, NTLM) de façon inhabituelle. Ce type de trafic réseau est admis par Windows sans avertissement, mais Azure ATP est capable de reconnaître une intention potentiellement malveillante. Le comportement est révélateur de certaines techniques comme l’attaque par force brute ou Over-Pass-the-Hash, ou de l’exploitation des failles de sécurité par de puissants ransomware tels que WannaCry.

**Examen**

Identifiez le protocole inhabituel : à partir de la chronologie des activités suspectes, cliquez sur l’alerte de sécurité pour accéder à la page de détails correspondante. Le protocole s’affiche au-dessus de la flèche : Kerberos ou NTLM.

- **Kerberos** : une alerte est souvent déclenchée si un outil de piratage comme Mimikatz a été utilisé dans le cadre d’une attaque potentielle de type Overpass-the-Hash. Vérifiez si l’ordinateur source exécute une application qui implémente sa propre pile Kerberos, de manière non conforme à la RFC Kerberos. Si c’est le cas, il s’agit d’un vrai positif sans gravité. Vous pouvez **fermer** l’alerte. Si l’alerte continue de se déclencher et que votre vérification précédente reste vraie, vous pouvez **supprimer** l’alerte.

- **NTLM** : possiblement WannaCry ou des outils comme Metasploit, Medusa ou Hydra.  

Pour déterminer s’il s’agit d’une attaque WannaCry, effectuez les étapes suivantes :

1. Vérifiez si l’ordinateur source exécute un outil d’attaque tel que Metasploit, Medusa ou Hydra.

2. Si vous ne trouvez aucun outil d’attaque, vérifiez si l’ordinateur source exécute une application qui implémente sa propre pile NTLM ou SMB.

3. Cliquez sur l’ordinateur source pour accéder à sa page de profil. Vérifiez ce qui s’est passé à peu près au même moment que l’alerte, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté et a accédé à quelles ressources. Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge wd](./media/wd-badge.png) pour examiner davantage l’ordinateur. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte.


**Correction**

Installez tous les correctifs logiciels nécessaires sur les machines, notamment les mises à jour de sécurité.

1. [Désactivez SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/).

2. [Supprimez WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo).

3. WanaKiwi peut déchiffrer les données interceptées par certains ransomwares, mais uniquement si l’utilisateur n’a pas redémarré ou éteint l’ordinateur. Pour plus d’informations, consultez [Ransomware WannaCry](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1).

## <a name="user-and-ip-address-reconnaissance-smb"></a>Reconnaissance des utilisateurs et des adresses IP (SMB)
<a name="reconnaissance-using-smb-session-enumeration"></a> Reconnaissance à l’aide de l’énumération de sessions SMB


**Description**

L’énumération SMB (Server Message Block) permet aux attaquants d’obtenir des informations sur les emplacements de connexion récents des utilisateurs. Une fois qu’ils connaissent ces informations, les attaquants peuvent se déplacer de façon latérale dans le réseau pour accéder à un compte sensible spécifique.

Dans cette détection, une alerte est déclenchée quand une énumération de sessions SMB est effectuée sur un contrôleur de domaine, ce qui ne doit pas se produire normalement.

**Examen**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante. Déterminez quels comptes ont effectué l’opération et quels comptes ont été exposés, le cas échéant.

 - L’ordinateur source exécute-t-il un scanner de sécurité ? Si c’est le cas, **fermez et excluez** l’activité suspecte.

2. Déterminez quels utilisateurs ont effectué l’opération. Sont-ils des utilisateurs qui se connectent normalement à l’ordinateur source ou des administrateurs autorisés à effectuer des actions de ce type ?  

3. Si c’est le cas et que l’alerte a été mise à jour, **supprimez** l’activité suspecte.  

4. Si c’est le cas, mais que cela ne devrait plus se produire, **fermez** l’activité suspecte.

5. Si vous avez répondu non à toutes les questions ci-dessus, considérez l’alerte comme une attaque malveillante.

**Correction**

Utilisez [l’outil Net Cease](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) pour renforcer la protection de votre environnement contre cette attaque.



> [!NOTE]
> Pour désactiver une alerte de sécurité, contactez le support technique.


## <a name="see-also"></a>Voir aussi
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
