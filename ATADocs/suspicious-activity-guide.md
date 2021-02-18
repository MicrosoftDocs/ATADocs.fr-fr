---
title: Guide des activités suspectes d’ATA
description: Cet article fournit une liste des activités suspectes qu'ATA peut détecter et décrit les étapes pour y remédier.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/03/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 9a22617587fab0aeacbc52f8b539c4a1042419d3
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097264"
---
# <a name="advanced-threat-analytics-suspicious-activity-guide"></a>Guide ATA (Advanced Threat Analytics) des activités suspectes

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Après avoir examiné une activité suspecte, vous pouvez la classer comme :

- **Vrai positif** : action malveillante détectée par ATA.

- **Vrai positif sans gravité**: action détectée par ATA qui est réelle, mais pas malveillante, comme un test de pénétration.
- **Faux positif**: fausse alerte, ce qui signifie que l’activité n’a pas eu lieu.

Pour plus d’informations sur la gestion des alertes ATA, consultez [Gestion des activités suspectes](working-with-suspicious-activities.md).

Si vous avez des questions ou des commentaires, contactez l’équipe ATA à l’adresse [ATAEval@microsoft.com](mailto:ATAEval@microsoft.com) .

## <a name="abnormal-modification-of-sensitive-groups"></a>Modification anormale de groupes sensibles

**Description**

Des attaquants ajoutent des utilisateurs à des groupes avec des privilèges élevés. Leur but est d’accéder à davantage de ressources et d’obtenir un accès persistant. Les détections s’appuient sur le profilage des activités de modification de groupes d’utilisateurs et déclenchent une alerte quand un ajout anormal à un groupe sensible est observé. ATA effectue le profilage en continu. La période minimale avant le déclenchement d’une alerte est d’un mois pour chaque contrôleur de domaine.

Pour avoir une définition des groupes sensibles dans ATA, consultez [Utilisation de la console ATA](working-with-ata-console.md#sensitive-groups).

La détection s’appuie sur les [événements audités sur les contrôleurs de domaine](configure-event-collection.md).
Pour vérifier que vos contrôleurs de domaine auditent les événements souhaités, utilisez l’outil indiqué dans le blog [ATA Auditing (AuditPol, Advanced Audit Settings Enforcement, Lightweight Gateway Service discovery)](https://aka.ms/ataauditingblog).

**Investigation**

1. La modification du groupe est-elle légitime ? </br>Les modifications de groupe légitimes qui se produisent rarement et qui n’ont pas été apprises comme « normales » peuvent entraîner une alerte, qui serait considérée comme un vrai positif sans gravité.

1. Si l’objet ajouté est un compte d’utilisateur, déterminez les actions que ce compte a effectuées après son ajout au groupe d’administration. Accédez à la page de l’utilisateur dans ATA pour obtenir plus de contexte. D’autres activités suspectes associées au compte ont-elles été effectuées avant ou après l’ajout ? Téléchargez le rapport **Modifications des groupes sensibles** pour examiner toutes les autres modifications effectuées au cours de la même période et déterminer les auteurs de ces modifications.

**Correction**

Réduisez le nombre d’utilisateurs autorisés à modifier les groupes sensibles.

Configurez [Privileged Access Management pour Active Directory](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) le cas échéant.

## <a name="broken-trust-between-computers-and-domain"></a>Relation de confiance rompue entre les ordinateurs et le domaine

> [!NOTE]
> La relation de confiance rompue entre les ordinateurs et l’alerte du domaine a été dépréciée et apparaît uniquement dans les versions ATA antérieures à 1.9.

**Description**

Une relation de confiance rompue signifie que les exigences de sécurité des services de domaine Active Directory ne sont pas respectées pour ces ordinateurs. Considéré comme une défaillance de sécurité et de conformité élémentaire, c’est une cible facile pour les attaquants. Cette détection déclenche une alerte si plus de cinq échecs d’authentification Kerberos ont été observés pour le même compte d’ordinateur dans un délai de 24 heures.

**Investigation**

L’ordinateur en cours d’examen permet-il aux utilisateurs du domaine de se connecter ?
- Si c’est le cas, vous pouvez ignorer cet ordinateur dans la procédure de correction.

**Correction**

Rejoignez la machine au domaine, si nécessaire, ou réinitialisez le mot de passe de la machine.

## <a name="brute-force-attack-using-ldap-simple-bind"></a>Attaque par force brute par le biais d’une liaison simple LDAP

**Description**

>[!NOTE]
> La principale différence entre les **échecs d’authentification suspects** et cette détection est que celle-ci permet à ATA de déterminer si des mots de passe différents ont été utilisés.

Dans une attaque par force brute, un attaquant tente de s’authentifier en essayant plusieurs mots de passe pour différents comptes jusqu’à ce qu’il trouve le bon mot de passe de l’un des comptes. Une fois qu’il a deviné le mot de passe d’un compte, l’attaquant utilise ce compte pour se connecter au réseau.

Dans cette détection, une alerte est déclenchée quand ATA détecte un nombre massif d’authentifications de liaison simple. Il peut s’agir *d’un* petit ensemble de mots de passe entre plusieurs utilisateurs. ou *verticalement»* avec un grand ensemble de mots de passe sur quelques utilisateurs seulement. ou une combinaison de ces deux options.

**Investigation**

1. Si de nombreux comptes sont concernés, cliquez sur **Télécharger les détails** pour afficher la liste complète dans une feuille de calcul Excel.

1. Cliquez sur l’alerte pour accéder à la page associée. Déterminez si des tentatives de connexion ont donné lieu à une authentification. Les tentatives s’affichent en tant que **Comptes devinés** à droite des données graphiques. Si des comptes devinés sont affichés, font-ils partie des **comptes devinés** normalement utilisés à partir de l’ordinateur source ? Si c’est le cas, **supprimez** l’activité suspecte.

1. S’il n’y a pas de **comptes devinés** affichés, s’agit-il de **comptes attaqués** normalement utilisés à partir de l’ordinateur source ? Si c’est le cas, **supprimez** l’activité suspecte.

**Correction**

Les [mots de passe longs et complexes](/windows/device-security/security-policy-settings/password-policy) fournissent le premier niveau de sécurité nécessaire contre les attaques en force brute.

## <a name="encryption-downgrade-activity"></a>Passage à une version antérieure du chiffrement

**Description**

Le passage à une version antérieure du chiffrement est une méthode visant à affaiblir Kerberos en abaissant le niveau de chiffrement de différents champs du protocole qui sont normalement chiffrés à l’aide du niveau de chiffrement le plus élevé. Un champ au chiffrement affaibli peut être plus vulnérable à des attaques de force brute en mode hors connexion. Plusieurs méthodes d’attaque exploitent les codes faibles de chiffrement Kerberos. Dans cette détection, ATA apprend les types de chiffrement Kerberos utilisés par les ordinateurs et les utilisateurs, et déclenche des alertes quand un code de chiffrement plus faible utilisé : (1) est inhabituel pour l’ordinateur source et/ou l’utilisateur ; et (2) correspond à une technique d’attaque connue.

Il existe trois types de détection :

1. Skeleton Key. Ce programme malveillant s’exécute sur les contrôleurs de domaine et autorise l’authentification sur le domaine de n’importe quel compte sans connaître son mot de passe. Il utilise souvent des algorithmes de chiffrement plus faibles pour hacher les mots de passe de l’utilisateur sur le contrôleur de domaine. Dans le cadre de cette détection, la méthode de chiffrement du message KRB_ERR adressé par le contrôleur de domaine au compte demandant un ticket a été abaissée par rapport au comportement appris.

1. Golden Ticket. Dans une alerte [Golden Ticket](#golden-ticket), la méthode de chiffrement du champ TGT du message TGS_REQ (demande de service) reçu de l’ordinateur source a été passée à une version antérieure par rapport au comportement appris. Cette détection n’est pas basée sur une anomalie de temps (contrairement à l’autre détection Golden Ticket). De plus, ATA n’a pas détecté de demande d’authentification Kerberos associée à la demande de service précédente.

1. Overpass-the-Hash. Un intrus peut utiliser un code de hachage faible dérobé pour créer un ticket fort via une demande Kerberos AS. Dans le cadre de cette détection, le type de chiffrement du message AS_REQ reçu de l’ordinateur source a été abaissé par rapport au comportement appris (l’ordinateur utilisait l’algorithme AES).

**Investigation**

Vérifiez tout d’abord la description de l’alerte pour voir lequel des trois types de détection ci-dessus sont à traiter. Pour plus d’informations, téléchargez la feuille de calcul Excel.

1. Skeleton Key : Déterminez si Skeleton Key a affecté vos contrôleurs de domaine à l’aide de [l’analyseur écrit par l’équipe ATA](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73). Si l’analyseur détecte la présence d’un logiciel malveillant sur un ou plusieurs de vos contrôleurs de domaine, l’alerte est un vrai positif.
1. Golden Ticket : dans la feuille de calcul Excel, accédez à l’onglet **activité réseau** . Vous verrez que le champ mis à niveau en question est le **type de chiffrement ticket de demande** et que **types de chiffrement pris en charge par l’ordinateur source** répertorie les méthodes de chiffrement plus fortes.
    1. Vérifiez l’ordinateur source et le compte, ou s’il existe plusieurs ordinateurs sources et si les comptes sont en commun (par exemple, tout le personnel marketing utilise une application spécifique qui peut être à l’origine du déclenchement de l’alerte). Il peut arriver qu’une application personnalisée rarement utilisée s’authentifie à l’aide d’un code de chiffrement plus faible. Déterminez si de telles applications personnalisées sont installées sur l’ordinateur source. Si c’est le cas, l’alerte est probablement un vrai positif sans gravité que vous pouvez **supprimer**.
    1. Vérifiez la ressource accessible par ces tickets, s’il y a une ressource à laquelle elles accèdent, validez-la, assurez-vous qu’il s’agit d’une ressource valide à laquelle ils sont censés accéder. De plus, vérifiez si la ressource cible prend en charge des méthodes de chiffrement renforcé. Vous pouvez le vérifier dans Active Directory en consultant l’attribut `msDS-SupportedEncryptionTypes` du compte de service de la ressource.
1. Overpass-The-hash : dans la feuille de calcul Excel, accédez à l’onglet **activité réseau** . Vous verrez que le champ de déclassement approprié est **chiffré** et que les types de chiffrement **pris en charge par l’ordinateur source** contiennent des méthodes de chiffrement plus fortes.
    1. dans certains cas, cette alerte peut être déclenchée lorsque des utilisateurs se connectent à l’aide de cartes à puce si la configuration de la carte à puce a été modifiée récemment. Vérifiez si des changements de ce type ont été apportés pour les comptes concernés. Si c’est le cas, l’alerte est probablement un vrai positif sans gravité que vous pouvez **supprimer**.
    1. Vérifiez la ressource accessible par ces tickets, s’il y a une ressource à laquelle elles accèdent, validez-la, assurez-vous qu’il s’agit d’une ressource valide à laquelle ils sont censés accéder. De plus, vérifiez si la ressource cible prend en charge des méthodes de chiffrement renforcé. Vous pouvez le vérifier dans Active Directory en consultant l’attribut `msDS-SupportedEncryptionTypes` du compte de service de la ressource.

**Correction**

1. Skeleton Key : supprimez le logiciel malveillant. Pour plus d’informations, voir [Analyse des programmes malveillants Skeleton Key](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).

1. Golden Ticket : suivez les instructions pour les activités suspectes [Golden Ticket](#golden-ticket).
    En outre, étant donné que la création d’un Golden Ticket nécessite des droits d’administrateur de domaine, implémentez [les recommandations de hachage](https://www.microsoft.com/download/details.aspx?id=36036).

1. Overpass-the-Hash : si le compte concerné n’est pas un compte sensible, réinitialisez son mot de passe. Cela empêche l’attaquant de créer d’autres tickets Kerberos à partir du hachage de mot de passe. Toutefois, les tickets existants resteront utilisables jusqu’à leur expiration. S’il s’agit d’un compte sensible, vous devez envisager de réinitialiser le compte KRBTGT à deux reprises comme dans l’activité suspecte de Golden Ticket. Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. Consultez les conseils fournis dans l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients). Consultez également utilisation du [Réinitialiser le mot de passe/les clés du compte KRBTGT

    Tool] ( https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) . Dans la mesure où il s’agit d’une technique de mouvement latéral, suivez les bonnes pratiques indiquées dans [Recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="honeytoken-activity"></a>Activité Honeytoken

**Description**

Les comptes Honeytoken sont des comptes servant de leurre pour identifier et suivre l’activité malveillante qui implique ces comptes. Les comptes Honeytoken doivent rester inutilisés, et avoir un nom évocateur pour attirer et leurrer les attaquants (par exemple, SQL-Admin). Toute activité observée sur ces comptes peut être le signe d’un comportement malveillant.

Pour plus d’informations sur les comptes Honeytoken, consultez [Installer ATA - Étape 7](install-ata-step7.md).

**Investigation**

1. Vérifiez si le propriétaire de l’ordinateur source a utilisé le compte Honeytoken pour s’authentifier, à l’aide de la méthode décrite dans la page de l’activité suspecte (par exemple, Kerberos, LDAP, NTLM).

1. Accédez à la page du profil de chaque ordinateur source et vérifiez si d’autres comptes se sont authentifiés à partir de ces ordinateurs. Vérifiez auprès des propriétaires de ces comptes s’ils ont utilisé le compte Honeytoken.

1. Il peut s’agir d’une connexion non interactive. Vous devez donc vérifier si des applications ou des scripts s’exécutent sur les ordinateurs sources.

Si, après avoir effectué les étapes 1 à 3, s’il n’y a aucune preuve d’une utilisation sans gravité, supposez que cela est malveillant.

**Correction**

Assurez-vous que les comptes Honeytoken sont utilisés uniquement pour leur rôle prévu afin d’éviter la génération de nombreuses alertes.

## <a name="identity-theft-using-pass-the-hash-attack"></a>Usurpation d’identité par attaque Pass-the-Hash

**Description**

Pass-the-Hash est une technique de mouvement latéral par laquelle les attaquants volent le code de hachage NTLM d’un utilisateur sur un ordinateur et utilisent ensuite ce code pour accéder à un autre ordinateur.

**Investigation**

Le code de hachage volé d’un ordinateur est-il détenu ou régulièrement utilisé par l’utilisateur ciblé ? Si oui, l’alerte est un faux positif, si non, c’est probablement un vrai positif.

**Correction**

1. Si le compte concerné n’est pas un compte sensible, réinitialisez le mot de passe de ce compte. La réinitialisation du mot de passe empêche les attaquants de créer de nouveaux tickets Kerberos à partir du hachage de mot de passe. Les tickets existants restent utilisables jusqu’à leur expiration.

1. Si le compte impliqué est sensible, réinitialisez deux fois le compte KRBTGT comme dans l’activité suspecte Golden Ticket. Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos de domaine, donc prévoyez son impact avant de procéder à cette opération. Consultez les conseils fournis dans l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) et utilisez [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Comme il s’agit typiquement d’une technique de mouvement latéral, suivez les bonnes pratiques indiquées dans [Recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Usurpation d’identité par attaque Pass-the-Ticket

**Description**

Pass-the-Ticket est une technique de mouvement latéral par laquelle les attaquants volent un ticket Kerberos sur un ordinateur et réutilisent ensuite ce ticket pour accéder à un autre ordinateur. Cette détection vérifie si un ticket Kerberos a été utilisé sur plusieurs ordinateurs différents.

**Investigation**

1. Cliquez sur le bouton **Télécharger les détails** pour afficher la liste complète des adresses IP impliquées. L’adresse IP de l’un ou des deux ordinateurs fait-elle partie d’un sous-réseau alloué à partir d’un pool DHCP de taille insuffisante, par exemple, VPN ou WiFi ? L’adresse IP est-elle partagée ? Par exemple, par un appareil NAT ? Si vous répondez par l’affirmative à l’une de ces questions, l’alerte est un faux positif.

1. Y a-t-il une application personnalisée qui transfère les tickets pour le compte d’utilisateurs ? Si c’est le cas, il s’agit d’un vrai positif.

**Correction**

1. Si le compte concerné n’est pas un compte sensible, réinitialisez le mot de passe de ce compte. La réinitialisation du mot de passe empêche les attaquants de créer de nouveaux tickets Kerberos à partir du hachage de mot de passe. Les tickets existants restent utilisables jusqu’à leur expiration.

1. S’il s’agit d’un compte sensible, vous devez envisager de réinitialiser le compte KRBTGT à deux reprises comme dans l’activité suspecte de Golden Ticket. Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. Consultez les conseils fournis dans l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et utilisez [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Dans la mesure où il s’agit d’une technique de mouvement latéral, suivez les bonnes pratiques indiquées dans [Recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="kerberos-golden-ticket-activity"></a>Activité de Golden Ticket Kerberos<a name="golden-ticket"></a>

**Description**

Les attaquants ayant des droits d’administrateur de domaine peuvent compromettre votre [compte KRBTGT](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn745899(v=ws.11)#Sec_KRBTGT). Les attaquants peuvent utiliser le compte KRBTGT pour créer un ticket TGT Kerberos qui leur fournit une autorisation sur n’importe quelle ressource. L’expiration du ticket peut être définie à tout moment. Ce faux ticket TGT appelé « Golden Ticket » permet aux attaquants d’obtenir et de garder un accès persistant sur votre réseau.

Cette détection déclenche une alerte quand un ticket TGT Kerberos est utilisé depuis plus longtemps que la durée autorisée définie dans la stratégie de sécurité [Durée de vie maximale du ticket utilisateur](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj852169(v=ws.11)).

**Investigation**

1. Le paramètre **Durée de vie maximale du ticket utilisateur** défini dans la stratégie de sécurité a-t-il été modifié récemment (au cours des dernières heures) ? Si c’est le cas, **Fermez** l’alerte (il s’agit d’un faux positif).

1. La passerelle ATA impliquée dans cette alerte est-elle une machine virtuelle ? Si c’est le cas, son exécution a-t-elle repris à partir d’un état de mise en mémoire ? Si c’est le cas, **fermez** l’alerte.

1. Si vous avez répondu non aux deux questions ci-dessus, considérez l’alerte comme une attaque malveillante.

**Correction**

Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération.
En outre, étant donné que la création d’un Golden Ticket nécessite des droits d’administrateur de domaine, implémentez [les recommandations de hachage](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="malicious-data-protection-private-information-request"></a>Demande d’information privée de protection contre les données malveillantes

**Description**

L’API de protection des données (DPAPI) est utilisée par Windows pour protéger les mots de passe enregistrés par les navigateurs, les clés de chiffrement et d’autres données sensibles. Les contrôleurs de domaine détiennent une clé principale de sauvegarde qui peut être utilisée pour déchiffrer tous les secrets chiffrés avec DPAPI sur des machines Windows jointes au domaine. Des attaquants peuvent utiliser cette clé principale pour déchiffrer les secrets protégés avec DPAPI sur toutes les machines jointes au domaine.
Cette détection déclenche une alerte quand DPAPI est utilisé pour récupérer la clé principale de sauvegarde.

**Investigation**

1. L’ordinateur source exécute-t-il un scanner de sécurité approuvé par l’organisation dans Active Directory ?

1. Si c’est le cas et si ce comportement est normal, **fermez et excluez** l’activité suspecte.

1. Si c’est le cas, mais que ce comportement n’est pas normal, **fermez l’activité suspecte.

**Correction**

Pour pouvoir utiliser DPAPI, un attaquant doit avoir les droits d’administrateur de domaine. Suivez les [recommandations pour Pass-the-Hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="malicious-replication-of-directory-services"></a>Réplication malveillante de services d’annuaire

**Description**

La réplication Active Directory est le processus par lequel les modifications apportées à un contrôleur de domaine sont synchronisées avec tous les autres contrôleurs de domaine. Quand les attaquants ont les autorisations nécessaires, ils peuvent lancer une demande de réplication dans le but de récupérer ensuite les données stockées dans Active Directory, y compris les hachages de mot de passe.

Dans cette détection, une alerte est déclenchée quand une demande de réplication est lancée à partir d’un ordinateur qui n’est pas un contrôleur de domaine.

**Investigation**

1. L’ordinateur en question est-il un contrôleur de domaine ? Par exemple, un contrôleur de domaine récemment promu ayant rencontré des problèmes de réplication. Si c’est le cas, **fermez** l’activité suspecte.
1. L’ordinateur en question est-il supposé répliquer des données à partir d’Active Directory ? Par exemple, Azure AD Connect. Si c’est le cas, **fermez et excluez** l’activité suspecte.
1. Cliquez sur l’ordinateur source ou le compte pour accéder à sa page de profil. Vérifiez ce qui s’est passé à peu près au même moment que la réplication, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté et a accédé à quelles ressources.

**Correction**

Vérifiez les autorisations suivantes :

- Répliquer les changements d’annuaire

- Répliquer tous les changements d’annuaire

Pour plus d’informations, consultez [Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013](/SharePoint/administration/user-profile-service-administration).
Vous pouvez utiliser [l’analyseur AD ACL](/archive/blogs/pfesweplat/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool) ou créer un script Windows PowerShell pour déterminer qui a ces autorisations dans le domaine.

## <a name="massive-object-deletion"></a>Suppression massive d’objets

**Description**

Dans certains scénarios, les attaquants effectuent des attaque par déni de service (DoS) au lieu de seulement voler des informations. La suppression d’un grand nombre de comptes est une méthode de tentative d’une attaque DoS.

Dans cette détection, une alerte est déclenchée quand plus de 5 % de l’ensemble des comptes sont supprimés. La détection nécessite un accès en lecture sur le conteneur d’objets supprimés.
Pour plus d’informations sur la configuration des autorisations en lecture seule sur le conteneur d’objets supprimés, consultez la section **Changing permissions on a deleted object container** (Modifier les autorisations sur un conteneur d’objets supprimés) dans [View or Set Permissions on a Directory Object](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824(v=ws.10)) (Afficher ou définir des autorisations sur un objet répertoire).

**Investigation**

Passez en revue la liste des comptes supprimés et déterminez si un modèle ou un motif particulier justifie cette suppression à grande échelle.

**Correction**

Supprimez les autorisations des utilisateurs qui peuvent supprimer des comptes dans Active Directory. Pour plus d’informations, consultez [View or Set Permissions on a Directory Object](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824(v=ws.10)) (Afficher ou définir des autorisations sur un objet répertoire).

## <a name="privilege-escalation-using-forged-authorization-data"></a>Réaffectation de privilèges à l’aide de données d’autorisation falsifiées

**Description**

Des vulnérabilités connues dans les versions antérieures de Windows Server permettent aux attaquants de manipuler le certificat PAC (Privileged Attribute Certificate). PAC est un champ du ticket Kerberos qui contient des données d’autorisation utilisateur (dans Active Directory, il s’agit de l’appartenance au groupe) et accorde des privilèges supplémentaires aux attaquants.

**Investigation**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante.

1. Le correctif MS14-068 (contrôleur de domaine) ou MS11-013 (serveur) a-t-il été installé sur l’ordinateur de destination (sous la colonne **ACCESSED**) ? Si c’est le cas, **fermez** l’activité suspecte (c’est un faux positif).

1. Si l’ordinateur de destination n’est pas corrigé, l’ordinateur source s’exécute (sous la colonne **FROM**) exécute-t-il un système d’exploitation ou une application connu pour modifier le certificat PAC ? Si c’est le cas, **supprimez** l’activité suspecte (c’est un vrai positif sans gravité).

1. Si la réponse à ces deux questions est non, considérez que cette activité est malveillante.

**Correction**

Vérifiez que tous les contrôleurs de domaine dotés de systèmes d’exploitation jusqu’à Windows Server 2012 R2 sont installés avec [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) et que tous les serveurs membres et contrôleurs de domaine jusqu’à 2012 R2 sont à jour avec KB2496930. Pour plus d’informations, consultez [Silver PAC](/security-updates/SecurityBulletins/2011/ms11-013) et [faux PAC](/security-updates/SecurityBulletins/2014/ms14-068).

## <a name="reconnaissance-using-account-enumeration"></a>Reconnaissance à l’aide de l’énumération de compte

**Description**

Lors d’une reconnaissance à l’aide de l’énumération de comptes, un attaquant utilise un dictionnaire contenant des milliers de noms d’utilisateurs ou des outils comme KrbGuess pour essayer de deviner des noms d’utilisateur de votre domaine. Il procède à des demandes Kerberos en utilisant ces noms afin de tenter de trouver un nom d’utilisateur valide dans votre domaine. Si l’attaquant arrive à trouver un nom d’utilisateur, il reçoit l’erreur Kerberos **Pré-authentification requise** au lieu de **Principal de sécurité inconnu**.

Dans cette détection, ATA peut détecter d'où vient l’attaque, le nombre total de tentatives et combien ont abouti. Si le nombre d’utilisateurs inconnus est trop élevé, ATA le détecte comme une activité suspecte.

**Investigation**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante.

    1. Cet ordinateur hôte doit-il interroger le contrôleur de domaine pour savoir si des comptes existent (par exemple, des serveurs Exchange) ?

1. Est-ce qu’un script ou une application s’exécutant sur l’hôte pourrait générer ce comportement ?

    Si la réponse à l’une de ces questions est oui, **fermez** l’activité suspecte (c’est un vrai positif sans incidence) et excluez cet hôte de l’activité suspecte.

1. Téléchargez les détails de l’alerte dans une feuille de calcul Excel pour voir clairement la liste des tentatives de comptes, avec d’un côté les comptes qui existent et de l’autre ceux qui n’existent pas. Si vous examinez la feuille des comptes qui n’existent pas et que vous pensez les connaître, il s’agit peut-être de comptes désactivés ou d’employés ayant quitté l’entreprise. Dans ce cas, il est peu probable que la tentative provienne d’un dictionnaire. Il s’agit très certainement d’une application ou d’un script qui vérifie les comptes qui existent toujours dans Active Directory, c’est donc un vrai positif sans incidence.

1. Si les noms sont en grande partie inconnus, des tentatives ont-elle abouti à une correspondance à des noms de comptes existants dans Active Directory ? S’il n’y a aucune correspondance, la tentative n’a servi à rien, mais vous devez surveiller l’alerte pour voir si elle est mise à jour au fil du temps.

1. Si des tentatives correspondent à des noms de compte existants, l’attaquant connaît l’existence de comptes dans votre environnement et peut essayer d’utiliser des attaques par force brute pour accéder à votre domaine en utilisant les noms d’utilisateur découverts. Vérifiez les noms de compte trouvés en recherchant d’autres activités suspectes. Regardez si des comptes sensibles se trouvent parmi les comptes trouvés.

**Correction**

Les [mots de passe longs et complexes](/windows/device-security/security-policy-settings/password-policy) fournissent le premier niveau de sécurité nécessaire contre les attaques en force brute.

## <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance à l’aide de requêtes de services d’annuaire

**Description**

La reconnaissance des services d’annuaire permet aux attaquants de mapper la structure d’annuaire et de cibler des comptes privilégiés pour les étapes suivantes d’une attaque. Le protocole SAM-R (Security Account Manager Remote) est l’une des méthodes utilisées pour interroger l’annuaire et effectuer ce type de mappage.

Dans cette détection, aucune alerte n’est déclenchée durant le premier mois après le déploiement d’ATA. Pendant cette période d’apprentissage, ATA effectue un profilage des requêtes SAM-R effectuées à partir des ordinateurs, qu’il s’agisse de requêtes d’énumération ou de requêtes individuelles sur des comptes sensibles.

**Investigation**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante. Examinez quels types de requêtes ont été effectuées (par exemple, des requêtes Administrateur entreprise ou Administrateur) et si elles ont réussi ou échoué.

1. Des requêtes de ce type sont-elles censées être effectuées à partir de l’ordinateur source en question ?

1. Si c’est le cas et que l’alerte a été mise à jour, **supprimez** l’activité suspecte.

1. Si c’est le cas, mais que cela ne devrait plus se produire, **fermez** l’activité suspecte.

1. S’il existe des informations sur le compte impliqué : ces requêtes sont-elles censées être effectuées par ce compte ou ce compte se connecte-t-il normalement à l’ordinateur source ?

   - Si c’est le cas et que l’alerte a été mise à jour, **supprimez** l’activité suspecte.

   - Si c’est le cas, mais que cela ne devrait plus se produire, **fermez** l’activité suspecte.

   - Si vous avez répondu non à toutes les questions ci-dessus, considérez l’alerte comme une attaque malveillante.

1. En l’absence d’informations sur le compte impliqué, vous pouvez accéder au point de terminaison et vérifier quel compte était connecté au moment de l’alerte.

**Correction**

Utilisez [l’outil SAMRi10](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b) pour mieux protéger votre environnement contre cette technique d’attaque.
Si l’outil n’est pas applicable à votre contrôleur de domaine :
1. L’ordinateur exécute-t-il un outil d’analyse des vulnérabilités ?
1. Vérifiez si les utilisateurs et groupes spécifiques interrogés dans l’attaque sont des comptes avec privilèges ou sensibles (par ex., PDG, directeur financier, direction informatique, etc.).  Si c’est le cas, examinez aussi les autres activités sur le point de terminaison et surveillez les ordinateurs auxquels les comptes interrogés sont connectés, car ils sont probablement la cible d’un mouvement latéral.

## <a name="reconnaissance-using-dns"></a>Reconnaissance à l’aide de DNS

**Description**

Votre serveur DNS contient une carte de l’ensemble des ordinateurs, adresses IP et services de votre réseau. Ces informations sont utilisées par les attaquants pour mapper la structure de votre réseau et cibler les ordinateurs intéressants pour les étapes suivantes de l’attaque.

Il existe plusieurs types de requêtes dans le protocole DNS. ATA détecte les demandes de transfert AXFR qui ne proviennent pas de serveurs DNS.

**Investigation**

1. La machine source (**En provenance de…**) est-elle un serveur DNS ? Si c’est le cas, il s’agit probablement d’un faux positif. Pour le vérifier, cliquez sur l’alerte pour accéder à la page de détails correspondante. Dans le tableau, sous **Requête**, vérifiez quels domaines ont été interrogés. S’agit-il de domaines existants ? Si c’est le cas, **fermez** l’activité suspecte (c’est un faux positif). De plus, vérifiez que le port UDP 53 est ouvert entre la passerelle ATA et l’ordinateur source pour éviter les futurs faux positifs.
1. L’ordinateur source exécute-t-il un scanner de sécurité ? Si c’est le cas, **excluez les entités** dans ATA, soit directement en choisissant **Fermer et exclure**, soit via la page **Exclusion**, sous **Configuration** (disponible pour les administrateurs d’ATA).
1. Si la réponse à toutes les questions précédentes est non, continuez à chercher en vous concentrant sur l’ordinateur source. Cliquez sur l’ordinateur source pour accéder à sa page de profil. Vérifiez ce qui s’est passé à peu près au même moment que la requête, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté et a accédé à quelles ressources.

**Correction**

La sécurisation d’un serveur DNS interne pour éviter la reconnaissance à l’aide de DNS est possible en désactivant les transferts de zone ou en les limitant uniquement aux adresses IP spécifiées. Pour plus d’informations sur la limitation des transferts de zone, consultez [Restrict Zone Transfers](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)) (Limiter les transferts de zone).
La modification des transferts de zone est l’une des tâches de la liste de contrôle que vous devez suivre pour [sécuriser vos serveurs DNS contre les attaques internes et externes](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770432(v=ws.11)).

## <a name="reconnaissance-using-smb-session-enumeration"></a>Reconnaissance à l’aide de l’énumération de sessions SMB

**Description**

L’énumération SMB (Server Message Block) permet aux attaquants d’obtenir des informations sur les emplacements de connexion récents des utilisateurs. Une fois qu’ils connaissent ces informations, les attaquants peuvent se déplacer de façon latérale dans le réseau pour accéder à un compte sensible spécifique.

Dans cette détection, une alerte est déclenchée quand une énumération de sessions SMB est effectuée sur un contrôleur de domaine.

**Investigation**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante. Déterminez le ou les comptes qui ont effectué l’opération et ceux qui ont été exposés, le cas échéant.

   - L’ordinateur source exécute-t-il un scanner de sécurité ? Si c’est le cas, **fermez et excluez** l’activité suspecte.

1. Déterminez quels utilisateurs ont effectué l’opération. Sont-ils des utilisateurs qui se connectent normalement à l’ordinateur source ou des administrateurs autorisés à effectuer des actions de ce type ?

1. Si c’est le cas et que l’alerte a été mise à jour, **supprimez** l’activité suspecte.

1. Si c’est le cas et qu’elle ne devrait pas être mise à jour, **fermez** l’activité suspecte.

1. Si vous avez répondu non à toutes les questions ci-dessus, considérez l’activité comme une attaque malveillante.

**Correction**

Utilisez [l’outil Net Cease](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) pour renforcer votre environnement contre ce type d’attaque.

## <a name="remote-execution-attempt-detected"></a>Tentative d’exécution à distance détectée

**Description**

Les attaquants qui compromettent les informations d’identification d’administration ou qui exploitent une faille de sécurité de type zero-day peuvent exécuter des commandes à distance sur votre contrôleur de domaine. Ils peuvent ainsi obtenir une persistance, collecter des informations, lancer des attaques par déni de service (DOS), etc. ATA détecte les connexions PSexec et les connexions WMI à distance.

**Investigation**

1. Cette situation est fréquente pour les stations de travail d’administration, ainsi que pour les membres des équipes informatiques et les comptes de service qui effectuent des tâches d’administration sur des contrôleurs de domaine. Si c’est le cas et que l’alerte a été mise à jour parce que le même administrateur ou ordinateur effectue la tâche, **supprimez** l’alerte.
1. L’ordinateur en question est-il autorisé à effectuer cette exécution à distance sur votre contrôleur de domaine ?
   - Le compte en question est-il autorisé à effectuer cette exécution à distance sur votre contrôleur de domaine ?
   - Si la réponse à ces deux questions est oui, **fermez** l’alerte.
1. Si la réponse à l’une de ces questions est non, considérez cette activité comme un vrai positif. Essayez de rechercher la source de la tentative en vérifiant les profils d’ordinateur et de compte. Cliquez sur l’ordinateur source ou le compte pour accéder à sa page de profil. Vérifiez ce qui s’est passé à peu près au même moment que ces tentatives, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté et a accédé à quelles ressources.

**Correction**

1. Limitez l’accès à distance aux contrôleurs de domaine à partir d’ordinateurs qui ne sont pas de niveau 0.

1. Implémentez un [accès privilégié](/windows-server/identity/securing-privileged-access/securing-privileged-access) pour autoriser uniquement les machines avec une sécurité renforcée à se connecter aux contrôleurs de domaine pour les administrateurs.

## <a name="sensitive-account-credentials-exposed--services-exposing-account-credentials"></a>Informations d’identification de compte sensible exposées et services qui exposent des informations d’identification de compte

> [!NOTE]
> Cette activité suspecte a été dépréciée et apparaît uniquement dans les versions d’ATA antérieures à la version 1.9. Pour ATA 1.9 et ultérieur, consultez [Rapports](reports.md).

**Description**

Certains services envoient des informations d’identification de compte au format texte brut, y compris pour des comptes sensibles. Les attaquants qui surveillent le trafic réseau peuvent intercepter ces informations d’identification et les réutiliser à des fins malveillantes. L’alerte est déclenchée dès qu’un mot de passe en texte clair est envoyé pour un compte sensible. Pour les comptes non sensibles, elle est déclenchée si les mots de passe en texte clair pour au moins cinq comptes différents sont envoyés à partir de l’ordinateur source.

**Investigation**

Cliquez sur l’alerte pour accéder à la page de détails correspondante. Déterminez quels comptes ont été exposés. Si de nombreux comptes sont concernés, cliquez sur **Télécharger les détails** pour afficher la liste complète dans une feuille de calcul Excel.

En général, il existe un script ou une application héritée sur les ordinateurs source qui utilise la liaison simple LDAP.

**Correction**

Vérifiez la configuration des ordinateurs sources et que vous n’utilisez pas de liaison simple LDAP. À la place des liaisons simples LDAP, utilisez des liaisons SALS LDAP ou LDAPS.

## <a name="suspicious-authentication-failures"></a>Échecs d’authentification suspects

**Description**

Dans une attaque par force brute, un attaquant tente de s’authentifier en essayant plusieurs mots de passe pour différents comptes jusqu’à ce qu’il trouve le bon mot de passe de l’un des comptes. Une fois qu’il a deviné le mot de passe d’un compte, l’attaquant utilise ce compte pour se connecter au réseau.

Dans cette détection, une alerte est déclenchée après l’échec de nombreuses tentatives d’authentification utilisant Kerberos ou NTLM. L’attaque peut être horizontale avec un petit nombre de mots de passe possibles pour de nombreux utilisateurs, verticale avec un grand nombre de mots de passe pour seulement quelques utilisateurs, ou à la fois horizontale et verticale. La période minimale avant le déclenchement d’une alerte est d’une semaine.

**Investigation**

1. Cliquez sur **Télécharger les détails** pour consulter toutes les informations dans une feuille de calcul Excel. Vous pouvez obtenir les informations suivantes :
   - Liste des comptes attaqués
   - Liste des comptes devinés dans lesquels des tentatives de connexion se sont terminées par une authentification réussie
   - Activités des événements concernés si les tentatives d’authentification ont été effectuées à l’aide de NTLM
   - Activités réseau associées si les tentatives d’authentification ont été effectuées à l’aide de Kerberos
1. Cliquez sur l’ordinateur source pour accéder à sa page de profil. Vérifiez ce qui s’est passé à peu près au même moment que ces tentatives, en recherchant d’éventuelles activités inhabituelles, notamment : qui s’est connecté et a accédé à quelles ressources.
1. Si l’authentification a été effectuée à l’aide de NTLM, que vous voyez que l’alerte se produit de nombreuses fois et qu’il n’y a pas suffisamment d’informations disponibles sur le serveur auquel l’ordinateur source a tenté d’accéder, vous devez activer l’**audit NTLM** sur les contrôleurs de domaine concernés. Pour cela, activez l’événement 8004. Il s’agit de l’événement d’authentification NTLM qui inclut des informations sur l’ordinateur source, le compte d’utilisateur et le **serveur** auquel l’ordinateur source a essayé d’accéder. Une fois que vous savez quel serveur a envoyé la validation de l’authentification, vous devez examiner le serveur en vérifiant ses événements tels que 4624 pour mieux comprendre le processus d’authentification.

**Correction**

Les [mots de passe longs et complexes](/windows/device-security/security-policy-settings/password-policy) fournissent le premier niveau de sécurité nécessaire contre les attaques en force brute.

## <a name="suspicious-service-creation"></a>Création de service suspect <a name="suspicious-service-creation"></a>

**Description**

Les attaquants tentent d’exécuter des services suspects sur votre réseau. ATA déclenche une alerte lorsqu’un nouveau service qui semble suspect est créé sur un contrôleur de domaine. Cette alerte s’appuie sur l’événement 7045 et est détectée sur chaque contrôleur de domaine couvert par une passerelle ATA ou la passerelle légère.

**Investigation**

1. Si l’ordinateur en question est une station de travail d’administration ou un ordinateur sur lequel les membres de l’équipe informatique et les comptes de service effectuent des tâches d’administration, il peut s’agir d’un faux positif et vous pouvez être amené à **supprimer** l’alerte et à l’ajouter à la liste des exclusions, si nécessaire.

1. Reconnaissez-vous ce service sur cet ordinateur ?

   - Le **compte** en question est-il autorisé à installer ce service ?

   - Si la réponse à ces deux questions est *oui*, **fermez** l’alerte ou ajoutez-la à la liste des exclusions.

1. Si la réponse à l’une de ces questions est *non*, cela doit être considéré comme un vrai positif.

**Correction**

- Implémentez un accès doté de moins de privilèges sur les ordinateurs du domaine pour autoriser uniquement des utilisateurs spécifiques à créer de nouveaux services.

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Suspicion d’usurpation d’identité basée sur un comportement inhabituel

**Description**

ATA apprend le comportement de l’entité pour les utilisateurs, les ordinateurs et les ressources sur une période glissante de trois semaines. Le modèle de comportement est basé sur les activités suivantes : les machines auxquelles les entités se sont connectées, les ressources pour lesquelles l’entité a demandé l’accès et la durée de ces opérations. ATA envoie une alerte en cas d’écart par rapport au comportement de l’entité en fonction des algorithmes de Machine Learning.

**Investigation**

1. L’utilisateur en question est-il supposé effectuer ces opérations normalement ?

1. Considérez les cas suivants comme des faux positifs potentiels : un utilisateur qui rentre de vacances, un membre du service informatique qui a besoin d’accéder à plus de ressources qu’habituellement (par exemple, pour répondre à toutes les demandes de support technique durant un jour ou une semaine donné) et les applications de bureau à distance. Si vous **fermez et excluez** l’alerte, l’utilisateur ne sera plus inclus dans la détection.

**Correction**

 Différentes actions doivent être entreprises en fonction de la cause de ce comportement anormal. Par exemple, si le réseau a été analysé, la machine source doit être bloquée à partir du réseau (sauf si elle est approuvée).

## <a name="unusual-protocol-implementation"></a>Implémentation de protocole inhabituelle

**Description**

Les attaquants utilisent des outils qui implémentent différents protocoles (SMB, Kerberos, NTLM) de façon inhabituelle. Ce type de trafic réseau est admis par Windows sans avertissement, mais ATA est capable de reconnaître une activité malveillante potentielle. Le comportement est révélateur de certaines techniques comme l’attaque Over-Pass-the-Hash, ou de l’exploitation des failles de sécurité par de puissants ransomwares tels que WannaCry.

**Investigation**

Identifiez le protocole inhabituel, à partir de la chronologie des activités suspectes, et cliquez sur l’activité suspecte pour accéder à la page de détails correspondante. Le protocole s’affiche au-dessus de la flèche : Kerberos ou NTLM.

- **Kerberos** : souvent déclenché si un outil de piratage comme Mimikatz a été éventuellement utilisé dans une attaque de type Overpass-the-Hash. Vérifiez si l’ordinateur source exécute une application qui implémente sa propre pile Kerberos, qui n’est pas conforme à la RFC Kerberos. Si c’est le cas, il s’agit d’un vrai positif sans gravité et l’alerte peut être **fermée**. Si l’alerte continue d’être déclenchée et que c’est toujours le cas, **supprimez** l’alerte.

- **NTLM** : une alerte peut être déclenchée si WannaCry ou un outil comme Metasploit, Medusa ou Hydra est utilisé.

Pour déterminer si l’activité est une attaque WannaCry, effectuez les étapes suivantes :

1. Vérifiez si l’ordinateur source exécute un outil d’attaque tel que Metasploit, Medusa ou Hydra.

1. Si vous ne trouvez aucun outil d’attaque, vérifiez si l’ordinateur source exécute une application qui implémente sa propre pile NTLM ou SMB.

1. Si ce n’est pas le cas, vérifiez si l’alerte est causée par WannaCry, en exécutant un script de scanner WannaCry, par exemple [this scanner](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner) sur l’ordinateur source impliqué dans l’activité suspecte. Si le scanner identifie la machine comme infectée ou vulnérable, installez les correctifs appropriés sur la machine et supprimez/bloquez le programme malveillant sur le réseau.

1. Si le script ne détecte pas que la machine est infectée ou vulnérable, cela ne signifie pas qu’elle ne l’est pas. En effet, SMBv1 peut avoir été désactivé ou un correctif peut avoir été installé sur la machine, ce qui fausse l’analyse de l’outil.

**Correction**

Appliquez les derniers correctifs à tous vos ordinateurs et vérifiez que toutes les mises à jour de sécurité sont appliquées.

1. [Désactivez SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/).

1. [Supprimez WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo).

1. Les données dans le contrôle de certains logiciels ransom peuvent parfois être déchiffrées. Le déchiffrement est possible seulement si l’utilisateur n’a pas redémarré ou éteint l’ordinateur. Pour plus d’informations, consultez [Ransomware WannaCry](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1).

>[!NOTE]
> Pour désactiver une alerte d’activité suspecte, contactez le support.

## <a name="related-videos"></a>Vidéos connexes

- [Rejoindre la communauté sur la sécurité](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)

## <a name="see-also"></a>Voir aussi

- [Scénario d’activité suspecte ATA](/samples/browse/?redirectedfrom=TechNet-Gallery)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Gestion des activités suspectes](working-with-suspicious-activities.md)