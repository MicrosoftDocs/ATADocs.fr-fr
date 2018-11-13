---
title: Guide des alertes de sécurité d’Azure ATP | Microsoft Docs
d|Description: This article provides a list of the security alerts issued by Azure ATP and steps for remediation.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/28/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: daeb998f6e97bc4ebdf290d4430fec8fcef40313
ms.sourcegitcommit: 03b1949beaf2f78a3cdf9396356a96488ea2e127
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/05/2018
ms.locfileid: "50983155"
---
*S’applique à : Azure Advanced Threat Protection*


# <a name="azure-advanced-threat-protection-security-alert-guide"></a>Guide des alertes de sécurité d’Azure Advanced Threat Protection

Après une investigation appropriée, toutes les alertes de sécurité Azure ATP peuvent être classées comme suit :

-   **Vrai positif** : action malveillante détectée par Azure ATP.

-   **Vrai positif sans gravité** : action détectée par Azure ATP qui est réelle, mais pas malveillante, comme un test de pénétration.

-   **Faux positif** : fausse alerte. L’activité n’a pas eu lieu.

Pour plus d’informations sur l’utilisation des alertes de sécurité d’Azure ATP, consultez [Utilisation des alertes de sécurité](working-with-suspicious-activities.md).




## <a name="brute-force-attack-using-ldap-simple-bind"></a>Attaque par force brute par le biais d’une liaison simple LDAP

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

## <a name="encryption-downgrade-activity"></a>Passage à une version antérieure du chiffrement

**Description**

Le passage à une version antérieure du chiffrement est une méthode visant à affaiblir Kerberos en abaissant le niveau de chiffrement de différents champs du protocole qui sont généralement chiffrés à l’aide du niveau de chiffrement le plus élevé. Un champ au chiffrement affaibli peut être plus vulnérable à des attaques de force brute en mode hors connexion. Plusieurs méthodes d’attaque exploitent les codes faibles de chiffrement Kerberos. Dans cette détection, Azure ATP examine les types de chiffrement Kerberos utilisés par les ordinateurs et les utilisateurs, et déclenche des alertes quand un chiffrement plus faible est utilisé : (1) qui est inhabituel pour l’ordinateur source et/ou l’utilisateur ; et (2) qui correspond à une technique d’attaque connue.

Il existe trois types de détection :

1.  Skeleton Key. Ce programme malveillant s’exécute sur les contrôleurs de domaine et autorise l’authentification sur le domaine de n’importe quel compte sans connaître son mot de passe. Il utilise souvent des algorithmes de chiffrement plus faibles pour hacher les mots de passe de l’utilisateur sur le contrôleur de domaine. Dans le cadre de cette détection, la méthode de chiffrement du message KRB_ERR adressé par le contrôleur de domaine au compte demandant un ticket a été passée à une version antérieure par rapport au comportement appris.

2.  Golden Ticket. Dans une alerte [Golden Ticket](#golden-ticket), la méthode de chiffrement du champ TGT du message TGS_REQ (demande de service) reçu de l’ordinateur source a été passée à une version antérieure par rapport au comportement appris. Cette détection n’est pas basée sur une anomalie de temps (contrairement à l’autre détection Golden Ticket). De plus, ATP n’a pas détecté de demande d’authentification Kerberos associée à la demande de service précédente.

3.  Overpass-the-Hash. Un intrus peut utiliser un code de hachage faible dérobé pour créer un ticket fort via une demande Kerberos AS. Dans le cadre de cette détection, le type de chiffrement du message AS_REQ reçu de l’ordinateur source a été passé à une version antérieure par rapport au comportement appris (l’ordinateur utilisait l’algorithme AES).

**Examen**

Lisez d’abord la description de l’alerte pour déterminer de quel type de détection il s’agit entre les trois types de détection répertoriés ci-dessus. Pour plus d’informations, téléchargez la feuille de calcul Excel.

1.  Skeleton Key : déterminez si Skeleton Key a affecté vos contrôleurs de domaine à l’aide du [scanneur écrit par l’équipe Azure ATP](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73). Si l’analyseur détecte la présence d’un logiciel malveillant sur un ou plusieurs de vos contrôleurs de domaine, l’alerte est un vrai positif.

2.  Golden Ticket : dans la feuille de calcul Excel, ouvrez l’onglet Activité réseau. Le champ qui a changé de version concerne la **demande du type de chiffrement du ticket** et le champ des **types de chiffrement pris en charge par les ordinateurs sources** affiche des méthodes de chiffrement plus poussé.

  1. Vérifiez la ressource accessible par ces tickets, s’il existe une seule ressource à laquelle ils accèdent tous, validez-la, vérifiez qu’il s’agit d’une ressource valide, à laquelle ils sont censés accéder. De plus, vérifiez si la ressource cible prend en charge des méthodes de chiffrement renforcé. Vous pouvez le vérifier dans Active Directory en consultant l’attribut msDS-SupportedEncryptionTypes du compte de service de la ressource.
  
  2. Vérifiez le compte et l’ordinateur source ; s’il y en a plusieurs, regardez s’ils ont un point commun. Il se peut par exemple que tout le personnel marketing utilise une même application, qui serait à l’origine du déclenchement de l’alerte. Il peut arriver qu’une application personnalisée rarement utilisée s’authentifie à l’aide d’un code de chiffrement plus faible. Déterminez si de telles applications personnalisées sont installées sur l’ordinateur source. Si c’est le cas, l’alerte est probablement un vrai positif sans gravité et peut être supprimée.
  


3.  Overpass-the-Hash – Dans la feuille de calcul Excel, accédez à l’onglet relatif à l’activité réseau. Vous voyez que le champ qui a changé de version concerne le **type de chiffrement d’horodateur chiffré** et que le champ des **types de chiffrement pris en charge par les ordinateurs sources** contient des méthodes de chiffrement renforcé.

  1. Dans certains cas, cette alerte peut se déclencher quand des utilisateurs se connectent à l’aide de cartes à puce dont la configuration a récemment été modifiée. Vérifiez si des changements de ce type ont été apportés pour les comptes concernés. Si c’est le cas, l’alerte est probablement un vrai positif sans gravité et peut être supprimée.
  2. Vérifiez la ressource accessible par ces tickets, s’il existe une seule ressource à laquelle ils accèdent tous, validez-la, vérifiez qu’il s’agit d’une ressource valide, à laquelle ils sont censés accéder. De plus, vérifiez si la ressource cible prend en charge des méthodes de chiffrement renforcé. Vous pouvez le vérifier dans Active Directory en consultant l’attribut msDS-SupportedEncryptionTypes du compte de service de la ressource.

**Correction**

1.  Skeleton Key : supprimez le logiciel malveillant. Pour plus d’informations, voir [Analyse des programmes malveillants Skeleton Key](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).

2.  Golden Ticket : suivez les instructions pour les activités suspectes [Golden Ticket](#golden-ticket).   
    De plus, comme la création d’un Golden Ticket nécessite des droits d’administrateur de domaine, suivez les  [recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

3.  Overpass-the-Hash : si le compte concerné n’est pas un compte sensible, réinitialisez son mot de passe. Cela empêche l’attaquant de créer d’autres tickets Kerberos à partir du hachage de mot de passe. Toutefois, les tickets existants resteront utilisables jusqu’à leur expiration. S’il s’agit d’un compte sensible, réinitialisez deux fois le compte KRBTGT comme dans l’activité suspecte Golden Ticket. Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. Consultez les conseils fournis dans l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients). Utilisez également  [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Dans la mesure où il s’agit d’une technique de mouvement latéral, suivez les bonnes pratiques indiquées dans [Recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="honeytoken-activity"></a>Activité Honeytoken


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

## <a name="identity-theft-using-pass-the-hash-attack"></a>Usurpation d’identité par attaque Pass-the-Hash

**Description**

Pass-the-Hash est une technique de mouvement latéral par laquelle les attaquants volent le code de hachage NTLM d’un utilisateur sur un ordinateur et utilisent ensuite ce code pour accéder à un autre ordinateur. 

**Examen**

Vérifiez si le hachage provient d’un ordinateur que l’utilisateur ciblé possède ou utilise régulièrement. Si oui, l’alerte est un faux positif ; sinon, il s’agit probablement d’un vrai positif.

**Correction**

1. Si le compte concerné n’est pas un compte sensible, réinitialisez le mot de passe de ce compte. Cela empêche l’attaquant de créer d’autres tickets Kerberos à partir du hachage de mot de passe. Toutefois, les tickets existants resteront utilisables jusqu’à leur expiration. 

2. S’il s’agit d’un compte sensible, réinitialisez deux fois le compte KRBTGT comme dans l’activité suspecte Golden Ticket. Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. Consultez les conseils fournis dans l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et utilisez  [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Dans la mesure où il s’agit d’une technique de mouvement latéral, suivez les bonnes pratiques indiquées dans [Recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Usurpation d’identité par attaque Pass-the-Ticket

**Description**

Pass-the-Ticket est une technique de mouvement latéral par laquelle les attaquants volent un ticket Kerberos sur un ordinateur et réutilisent ensuite ce ticket pour accéder à un autre ordinateur. Cette détection vérifie si un ticket Kerberos a été utilisé sur plusieurs ordinateurs différents.

**Examen**

1. Cliquez sur le bouton **Télécharger les détails** pour afficher la liste complète des adresses IP impliquées. L’adresse IP de l’un ou des deux ordinateurs appartient-elle à un sous-réseau alloué à partir d’un pool DHCP de taille insuffisante, par exemple, VPN ou WiFi ? L’adresse IP est-elle partagée ? Par exemple, par un appareil NAT ? Une ou plusieurs des adresses IP sources sont-elles non résolues par le capteur ? (Cela peut indiquer que les ports appropriés du capteur vers les périphériques ne sont pas correctement ouverts.) Si vous répondez par l’affirmative à l’une de ces questions, il s’agit d’un faux positif.

2. Y a-t-il une application personnalisée qui transfère les tickets pour le compte d’utilisateurs ? Si c’est le cas, il s’agit d’un vrai positif.

**Correction**

1. Si le compte concerné n’est pas un compte sensible, réinitialisez le mot de passe de ce compte. Cela empêche l’attaquant de créer d’autres tickets Kerberos à partir du hachage de mot de passe. Toutefois, les tickets existants resteront utilisables jusqu’à leur expiration.  

2. S’il s’agit d’un compte sensible, réinitialisez deux fois le compte KRBTGT comme dans l’activité suspecte Golden Ticket. Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. Consultez les conseils fournis dans l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et utilisez  [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Dans la mesure où il s’agit d’une technique de mouvement latéral, suivez les bonnes pratiques indiquées dans [Recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## Golden Ticket Kerberos<a name="golden-ticket"></a>

**Description**

Les attaquants ayant des droits d’administrateur de domaine peuvent compromettre le [compte KRBTGT](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). Ils utilisent ensuite ce compte KRBTGT pour créer un ticket TGT (Ticket Granting Ticket) Kerberos qui fournit une autorisation d’accès à toutes les ressources du réseau, et définir l’heure d’expiration du ticket à la valeur de leur choix. Ce faux ticket TGT appelé « Golden Ticket » permet aux attaquants d’obtenir un accès persistant dans le réseau.

Cette détection déclenche une alerte quand un ticket TGT Kerberos est utilisé depuis plus longtemps que la durée autorisée définie dans la [Durée de vie maximale du ticket utilisateur](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx), c’est une attaque Golden Ticket de type **anomalie de temps**, ou par un compte inexistant, c’est une attaque Golden Ticket de type **compte inexistant**.


**Examen**

- **Anomalie de temps**
   1.   Le paramètre Durée de vie maximale du ticket utilisateur défini dans la stratégie de sécurité a-t-il été modifié récemment (au cours des dernières heures) ? Vérifiez la valeur spécifique pour voir si elle est inférieure à la durée pendant laquelle le ticket a été utilisé. Si c’est le cas, fermez l’alerte, car il s’agit d’un faux positif.
   2.   Le capteur Azure ATP impliqué dans cette alerte est-il une machine virtuelle ? Si c’est le cas, son exécution a-t-elle repris à partir d’un état de mise en mémoire ? Si c’est le cas, fermez l’alerte.
   3.   Si vous avez répondu non aux deux questions ci-dessus, considérez l’alerte comme une attaque malveillante.

- **Compte inexistant – Nouveau** 
   1.   Posez les questions suivantes :
         - L’utilisateur est-il un utilisateur de domaine connu et valide ? Si c’est le cas, fermez l’alerte, car il s’agit d’un faux positif.
         - L’utilisateur a-t-il été récemment ajouté ? Si c’est le cas, fermez l’alerte, car le changement n’a peut-être pas été encore été synchronisé.
         - L’utilisateur a-t-il été récemment supprimé d’AD ? Si c’est le cas, fermez l’alerte.
   2.   Si vous avez répondu non aux deux questions ci-dessus, considérez l’alerte comme une attaque malveillante.

1. Pour les deux types d’attaques par Golden Ticket, cliquez sur l’ordinateur source pour accéder à sa page **Profil**. Vérifiez ce qui s’est passé à peu près au même moment que l’activité, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté et a accédé à quelles ressources ? 

2.  Tous les utilisateurs connectés à l’ordinateur sont-ils censés l’être ? Quels sont leurs privilèges ? 

3.  Les utilisateurs connectés sont-ils censés avoir accès à ces ressources ?<br>
Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP.
 
 4. Pour un examen approfondi de l’ordinateur, vérifiez quels processus et quelles alertes se sont produits au moment de l’alerte dans Windows Defender ATP.

**Correction**


Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. De plus, du fait que la création d’un Golden Ticket nécessite des droits d’administrateur de domaine, suivez les [recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).




## <a name="malicious-data-protection-private-information-request"></a>Demande d’information privée de protection contre les données malveillantes

**Description**

L’API de protection des données (DPAPI) est utilisée par Windows pour protéger les mots de passe enregistrés par les navigateurs, les clés de chiffrement et d’autres données sensibles. Les contrôleurs de domaine détiennent une clé principale de sauvegarde qui peut être utilisée pour déchiffrer tous les secrets chiffrés avec DPAPI sur des machines Windows jointes au domaine. Des attaquants peuvent utiliser cette clé principale pour déchiffrer les secrets protégés avec DPAPI sur toutes les machines jointes au domaine.
Cette détection déclenche une alerte quand DPAPI est utilisé pour récupérer la clé principale de sauvegarde.

**Examen**

1. L’ordinateur source exécute-t-il un scanner de sécurité approuvé par l’organisation dans Active Directory ?

2. Si c’est le cas et si ce comportement est normal, **fermez et excluez** l’activité suspecte.

3. Si c’est le cas, mais que ce comportement n’est pas normal, **fermez** l’activité suspecte.

**Correction**

Pour pouvoir utiliser DPAPI, un attaquant doit avoir les droits d’administrateur de domaine. Suivez les  [recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="malicious-replication-of-directory-services"></a>Réplication malveillante de services d’annuaire


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


## <a name="privilege-escalation-using-forged-authorization-data"></a>Réaffectation de privilèges à l’aide de données d’autorisation falsifiées

**Description**

Des vulnérabilités connues dans les versions antérieures de Windows Server permettent aux attaquants de manipuler le certificat PAC (Privileged Attribute Certificate). PAC est un champ du ticket Kerberos qui contient des données d’autorisation utilisateur (dans Active Directory, il s’agit de l’appartenance au groupe) et accorde des privilèges supplémentaires aux attaquants.

**Examen**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante.

2. Le correctif MS14-068 (contrôleur de domaine) ou MS11-013 (serveur) a-t-il été installé sur l’ordinateur de destination (sous la colonne **ACCESSED**) ? Si c’est le cas, **fermez** l’activité suspecte (c’est un faux positif).

3. Sinon, l’ordinateur source s’exécute (sous la colonne **FROM**) exécute-t-il un système d’exploitation ou une application connu pour modifier le certificat PAC ? Si c’est le cas, **supprimez** l’activité suspecte (c’est un vrai positif sans gravité).

4. Si vous avez répondu non aux deux questions ci-dessus, considérez l’alerte comme une attaque malveillante.

**Correction**

Vérifiez que tous les contrôleurs de domaine dotés du système d’exploitation Windows Server 2012 R2 ou version antérieure sont installés avec  [withKB3011780and](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege)  et que tous les serveurs et contrôleurs de domaine membres avec 2012 R2 ou version antérieure sont à jour avec KB2496930. Pour plus d’informations, consultez  [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx)  et  [Faux PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="reconnaissance-using-account-enumeration"></a>Reconnaissance à l’aide de l’énumération de compte

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


## <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance à l’aide de requêtes de services d’annuaire

**Description**

La reconnaissance des services d’annuaire permet aux attaquants de mapper la structure d’annuaire et de cibler des comptes privilégiés pour les étapes suivantes d’une attaque. Le protocole SAM-R (Security Account Manager Remote) est l’une des méthodes utilisées pour interroger l’annuaire et effectuer ce type de mappage.

Dans le cadre de cette détection, aucune alerte n’est déclenchée durant le premier mois après le déploiement d’Azure ATP. Pendant cette période d’apprentissage, Azure ATP effectue un profilage des requêtes SAM-R effectuées à partir des ordinateurs, qu’il s’agisse de requêtes d’énumération ou de requêtes individuelles sur des comptes sensibles.

**Examen**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante. Examinez quels types de requêtes ont été effectuées (par exemple, des requêtes Administrateur entreprise ou Administrateur) et si elles ont réussi ou échoué.

2. Des requêtes de ce type sont-elles censées être effectuées à partir de l’ordinateur source en question ?

3. Si c’est le cas et que l’alerte a été mise à jour, **supprimez** l’activité suspecte.

4. Si c’est le cas, mais que cela ne devrait plus se produire, **fermez** l’activité suspecte.

5. Si vous avez des informations sur le compte impliqué : de telles requêtes sont-elles censées être effectuées par ce compte ou ce compte se connecte-t-il normalement à l’ordinateur source ?

 - Si c’est le cas et que l’alerte a été mise à jour, **supprimez** l’activité suspecte.

 - Si c’est le cas, mais que cela ne devrait plus se produire, **fermez** l’activité suspecte.

 - Si vous avez répondu non à toutes les questions ci-dessus, considérez l’alerte comme une attaque malveillante.

6. En l’absence d’informations sur le compte impliqué, vous pouvez accéder au point de terminaison et vérifier quel compte était connecté au moment de l’alerte.

**Correction**

Protégez mieux votre environnement contre cette technique à l’aide du processus suivant :
1. L’ordinateur exécute-t-il un outil d’analyse des vulnérabilités ?  
2. Vérifiez si les utilisateurs et groupes spécifiques interrogés dans l’attaque sont des comptes avec privilèges ou sensibles (par ex., PDG, directeur financier, direction informatique, etc.).  Si c’est le cas, examinez aussi les autres activités sur le point de terminaison et surveillez les ordinateurs auxquels les comptes interrogés sont connectés, car ils sont probablement la cible d’un mouvement latéral.

## <a name="reconnaissance-using-dns"></a>Reconnaissance à l’aide de DNS

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

## <a name="reconnaissance-using-smb-session-enumeration"></a>Reconnaissance à l’aide de l’énumération de sessions SMB


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

## <a name="remote-code-execution-attempt---enhanced"></a>Tentative d’exécution de code à distance - amélioré

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

## <a name="suspicious-authentication-failures--enhanced"></a>Échecs d’authentification suspects - amélioré

**Description**

Dans une attaque par force brute, l’attaquant tente de s’authentifier avec plusieurs mots de passe auprès de différents comptes jusqu'à ce qu’un mot de passe correct soit trouvé, ou à l’aide d’un mot de passe dans une attaque par pulvérisation de mots de passe à grande échelle qui fonctionne au moins pour un compte. Lorsqu’un mot de passe est trouvé, l’attaquant se connecte en utilisant le compte authentifié.

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

3.  Si l’authentification a été effectuée à l’aide de NTLM, que vous voyez que l’alerte se produit de nombreuses fois et il n’y a pas suffisamment d’informations disponibles sur le serveur auquel l’ordinateur source a tenté d’accéder, activez l’**audit NTLM** sur les contrôleurs de domaine concernés. Pour cela, activez l’événement 8004. Il s’agit de l’événement d’authentification NTLM qui inclut des informations sur l’ordinateur source, le compte d’utilisateur et le **serveur** auquel l’ordinateur source a essayé d’accéder. Une fois que vous savez quel serveur a envoyé la validation de l’authentification, examinez le serveur en vérifiant ses événements tels que 4624 pour mieux comprendre le processus d’authentification. 

**Correction**

Les [mots de passe longs et complexes](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) assurent le niveau minimum de sécurité nécessaire contre les attaques par force brute.

## <a name="suspicious-communication-over-dns---preview"></a>Communication suspecte sur DNS - préversion

**Description**

Dans la plupart des organisations, le protocole DNS n’est généralement pas surveillé et les activités malveillantes sont rarement bloquées. Ceci permet à un attaquant sur une machine compromise d’abuser le protocole DNS. Des communications malveillantes via DNS peuvent être utilisées pour l’exfiltration, des commandes et le contrôle des données, et/ou l’affranchissement des limitations du réseau d’entreprise.

**Examen**
> [!NOTE]
> Les alertes de sécurité *Communications suspectes via DNS* indiquent le domaine suspecté. Les nouveaux domaines, ou les domaines récemment ajoutés qui ne sont pas encore connus ou reconnus par Azure ATP, mais qui sont connus de votre organisation ou en font partie, peuvent être fermés. 


1.  Certaines entreprises légitimes utilisent DNS pour les communications régulières. Vérifiez si le domaine de requête inscrit appartient à une source approuvée, comme votre fournisseur d’antivirus. Si le domaine est connu et approuvé, et que les requêtes DNS sont autorisées, l’alerte peut être fermée et le domaine peut être [exclu](excluding-entities-from-detections.md) des alertes futures. 
2.   Si le domaine de requête inscrit n’est pas approuvé, identifiez le processus qui crée la demande sur la machine source. Utilisez le [Moniteur de processus](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon) pour vous aider dans cette tâche.
3.  À quel moment l’activité suspecte a-t-elle commencé ? De nouveaux programmes ont-ils été déployés ou installés dans l’organisation ? Y a-t-il d’autres alertes au même moment ?
4.  Cliquez sur l’ordinateur source pour accéder à la page de son profil. Vérifiez ce qui s’est passé à peu près au même moment que la requête DNS, en recherchant d’éventuelles activités inhabituelles, notamment qui s’est connecté et quelles ressources ont été utilisées. Si vous avez déjà activé l’intégration de Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge Windows Defender ATP](./media/wd-badge.png) pour examiner davantage l’ordinateur. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte.

**Correction** Si le domaine de requête inscrit n’est pas approuvé après votre investigation, nous vous recommandons de bloquer le domaine de destination afin d’éviter toute communication future. 

## <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Promotion du contrôleur de domaine suspect (attaque DcShadow potentielle)

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

## <a name="suspicious-modification-of-sensitive-groups"></a>Modification suspecte de groupes sensibles

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



## <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Demande de réplication suspecte (attaque DcShadow potentielle) 

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


## <a name="suspicious-service-creation"></a>Création de service malveillant

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


## Connexion VPN suspecte <a name="suspicious-vpn-detection"></a>

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


**Description**

Les attaquants utilisent des outils qui implémentent différents protocoles (SMB, Kerberos, NTLM) de façon inhabituelle. Ce type de trafic réseau est admis par Windows sans avertissement, mais Azure ATP est capable de reconnaître une intention potentiellement malveillante. Le comportement est révélateur de certaines techniques comme l’attaque par force brute ou Over-Pass-the-Hash, ou de l’exploitation des failles de sécurité par de puissants ransomware tels que WannaCry.

**Examen**

Identifiez le protocole inhabituel, à partir de la chronologie des activités suspectes, et cliquez sur l’activité suspecte pour accéder à la page de détails correspondante. Le protocole s’affiche au-dessus de la flèche : Kerberos ou NTLM.

- **Kerberos** : une alerte est souvent déclenchée si un outil de piratage comme Mimikatz a été utilisé dans le cadre d’une attaque potentielle de type Overpass-the-Hash. Vérifiez si l’ordinateur source exécute une application qui implémente sa propre pile Kerberos, de manière non conforme à la RFC Kerberos. Si c’est le cas, il s’agit d’un vrai positif sans gravité. Vous pouvez **fermer** l’alerte. Si l’alerte continue d’être déclenchée et que c’est toujours le cas, **supprimez** l’alerte.

- **NTLM** : une alerte peut être déclenchée si WannaCry ou un outil comme Metasploit, Medusa ou Hydra est utilisé.  

Pour déterminer s’il s’agit d’une attaque WannaCry, effectuez les étapes suivantes :

1. Vérifiez si l’ordinateur source exécute un outil d’attaque tel que Metasploit, Medusa ou Hydra.

2. Si vous ne trouvez aucun outil d’attaque, vérifiez si l’ordinateur source exécute une application qui implémente sa propre pile NTLM ou SMB.

3. Cliquez sur l’ordinateur source pour accéder à sa page de profil. Vérifiez ce qui s’est passé à peu près au même moment que l’alerte, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté et a accédé à quelles ressources. Si vous avez activé l’intégration Windows Defender ATP, cliquez sur le badge Windows Defender ATP ![badge wd](./media/wd-badge.png) pour examiner davantage l’ordinateur. Dans Windows Defender ATP, vous pouvez voir quels processus et quelles alertes se sont produits au moment de l’alerte.



**Correction**

Installez tous les correctifs logiciels nécessaires sur les machines, notamment les mises à jour de sécurité.

1. [Désactivez SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/).

2. [Supprimez WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo).

3. WanaKiwi peut déchiffrer les données interceptées par certains ransomwares, mais uniquement si l’utilisateur n’a pas redémarré ou éteint l’ordinateur. Pour plus d’informations, consultez [Ransomware WannaCry](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1).


> [!NOTE]
> Pour désactiver une alerte de sécurité, contactez le support technique.


## <a name="see-also"></a>Voir aussi
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
