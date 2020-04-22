---
title: Alertes de sécurité Azure ATP indiquant une dominance du domaine
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of domain dominance phase efforts are detected against your organization.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 03/01/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 0b3a1db5-0d43-49af-b356-7094cc85f0a5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 37e153e3b5b6c4511648c6971b07602cf5f34b6a
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80669671"
---
# <a name="tutorial-domain-dominance-alerts"></a>Tutoriel : Alertes de dominance du domaine

En général, les cyberattaques sont lancées contre des entités accessibles, par exemple un utilisateur avec des privilèges peu élevés, puis rapidement, elles se déplacent latéralement jusqu’à ce que l’attaquant parvienne à accéder à des ressources importantes, comme des comptes sensibles, des administrateurs de domaine ou des données hautement sensibles. Azure ATP identifie ces menaces avancées à la source tout au long de la chaîne d’annihilation des attaques et les classifie selon les phases suivantes :

1. [Reconnaissance](atp-reconnaissance-alerts.md)
2. [Informations d’identification compromises](atp-compromised-credentials-alerts.md)
3. [Mouvements latéraux](atp-lateral-movement-alerts.md)
4. **Dominance du domaine**
5. [Exfiltration](atp-exfiltration-alerts.md)

Pour en savoir plus sur la structure et les composants courants de toutes les alertes de sécurité Azure ATP, consultez [Présentation des alertes de sécurité](understanding-security-alerts.md).

Les alertes de sécurité suivantes vous aident à identifier et à résoudre les activités suspectes de la phase **Dominance du domaine** détectées par Azure ATP sur votre réseau. Dans ce tutoriel, vous allez apprendre à comprendre, classifier, prévenir et empêcher les attaques suivantes :

> [!div class="checklist"]
>
> * Demande malveillante de la clé principale de l’API de protection des données (ID externe 2020)
> * Tentative d’exécution de code à distance (ID externe 2019)
> * Suspicion d’attaque DCShadow (promotion du contrôleur de domaine) (ID externe 2028)
> * Suspicion d’attaque DCShadow (demande de réplication du contrôleur de domaine) (ID externe 2029)
> * Suspicion d’attaque DCSync (réplication de services d’annuaire) (ID externe 2006)
> * Suspicion d’utilisation de golden ticket (passage à une version antérieure du chiffrement) (ID externe 2009)
> * Suspicion d’utilisation de golden ticket (données d’autorisation falsifiées) (ID externe 2013)
> * Suspicion d’utilisation de golden ticket (compte inexistant) (ID externe 2027)
> * Suspicion d’utilisation de golden ticket (anomalie de ticket) (ID externe 2032)
> * Suspicion d’utilisation de golden ticket (anomalie de temps) (ID externe 2022)
> * Suspicion d’attaque Skeleton Key (passage à une version antérieure du chiffrement) (ID externe 2010)
> * Ajouts suspects à des groupes sensibles (ID externe 2024)
> * Création de service malveillant (ID externe 2026)

## <a name="malicious-request-of-data-protection-api-master-key-external-id-2020"></a>Demande malveillante de la clé principale de l’API de protection des données (ID externe 2020)

*Nom précédent :* Demande d’information privée de protection contre les données malveillantes

**Description**

L’API de protection des données (DPAPI) est utilisée par Windows pour protéger les mots de passe enregistrés par les navigateurs, les clés de chiffrement et d’autres données sensibles. Les contrôleurs de domaine détiennent une clé principale de sauvegarde qui peut être utilisée pour déchiffrer tous les secrets chiffrés avec DPAPI sur des machines Windows jointes au domaine. Des attaquants peuvent utiliser la clé principale pour déchiffrer les secrets protégés avec DPAPI sur toutes les machines jointes au domaine.
Cette détection déclenche une alerte Azure ATP quand DPAPI est utilisé pour récupérer la clé principale de sauvegarde.

**TP, B-TP ou FP ?**

Les scanners de sécurité avancés peuvent générer légitimement ce type d’activité dans Active Directory.

1. Vérifiez si l’ordinateur source exécute un scanner de sécurité approuvé par l’organisation dans Active Directory.

    * Si la réponse est **oui** alors qu’il ne devrait pas s’exécuter, corrigez la configuration de l’application. Cette alerte est une activité **B-TP** et peut être **fermée**.
    * Si la réponse est **oui** et qu’il doit toujours agir ainsi, **fermez** l’alerte et excluez cet ordinateur, il s’agit probablement d’une activité **B-TP**.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).
2. Si un [utilisateur source](investigate-a-user.md) existe, investiguez.

**Suggestions de correction et étapes préventives**

1. Réinitialisez le mot de passe de l’utilisateur source et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
2. Incluez l’ordinateur source.
    * Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    * Recherchez les utilisateurs qui étaient connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
3. La clé privée volée n’est jamais modifiée. Ce qui signifie que l’acteur peut toujours utiliser la clé volée pour déchiffrer les données protégées dans le domaine cible. Il n’existe pas de moyen méthodologique pour changer cette clé privée.
    * Pour créer une clé, utilisez la clé privée actuelle, créez une clé et rechiffrez chaque clé principale de domaine avec la nouvelle clé privée.

## <a name="remote-code-execution-attempt-external-id-2019"></a>Tentative d’exécution de code à distance (ID externe 2019)

*Nom précédent :* Tentative d’exécution de code à distance

**Description**

Les attaquants qui compromettent les informations d’identification d’administration ou qui exploitent une faille de sécurité de type zero-day peuvent exécuter des commandes à distance sur votre contrôleur de domaine. Cela peut servir pour obtenir une persistance, collecter des informations, lancer des attaques par déni de service (DOS) ou toute autre raison. Azure ATP détecte les connexions PSexec, les connexions WMI à distance et les connexions PowerShell.

**TP, B-TP ou FP**

Les stations de travail d’administration, les membres des équipes informatiques et les comptes de service peuvent tous légitimement effectuer des tâches d’administration sur les contrôleurs de domaine.

1. Vérifiez si l’utilisateur ou l’ordinateur source est censé exécuter ces types de commandes sur votre contrôleur de domaine.
    * Si l’utilisateur ou l’ordinateur source est autorisé à exécuter ces types de commandes, **fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP**.
    * Si l’utilisateur ou l’ordinateur source est autorisé à exécuter ces commandes sur votre contrôleur de domaine et va continuer à le faire, il s’agit d’une activité **B-TP**. **Fermez** l’alerte de sécurité et excluez l’ordinateur.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md) et l’[utilisateur](investigate-a-user.md).
2. Examinez le [contrôleur de domaine](investigate-a-computer.md).

**Suggestions de correction et étapes préventives :**

**Correction**

1. Réinitialisez le mot de passe des utilisateurs source et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
2. Incluez les contrôleurs de domaine en procédant ainsi :
    * Empêchez la tentative d’exécution du code à distance.
    * Recherchez les utilisateurs connectés aux environs de l’heure de l’activité suspecte, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
3. Incluez l’ordinateur source.
    * Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    * Recherchez les utilisateurs connectés aux environs de l’heure de l’activité suspecte, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.

**Prévention**

1. Limitez l’accès à distance aux contrôleurs de domaine à partir d’ordinateurs qui ne sont pas de niveau 0.
2. Implémentez un [accès privilégié](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access). Autorisez uniquement les ordinateurs avec une sécurité renforcée à se connecter aux contrôleurs de domaine pour les administrateurs.
3. Implémentez un accès avec moins de privilèges sur les ordinateurs du domaine pour autoriser des utilisateurs spécifiques à créer des services.

> [!NOTE]
> Les alertes de tentative d’exécution de code à distance lors d’une tentative d’utilisation des commandes Powershell sont prises uniquement en charge par les capteurs ATP.

## <a name="suspected-dcshadow-attack-domain-controller-promotion-external-id-2028"></a>Suspicion d’attaque DCShadow (promotion du contrôleur de domaine) (ID externe 2028)

*Nom précédent :* Promotion du contrôleur de domaine suspect (attaque DcShadow potentielle)

**Description**

Une attaque DCShadow (« Domain Controller Shadow ») est une attaque conçue pour modifier des objets annuaire par réplication malveillante. Elle consiste à créer, sur n’importe quel ordinateur, un contrôleur de domaine non autorisé suivant un processus de réplication.

Dans une attaque DCShadow, RPC et LDAP servent à :

1. Enregistrer le compte d’ordinateur comme contrôleur de domaine (à l’aide de droits d’administrateur de domaine).
2. Effectuer la réplication (grâce aux droits de réplication accordés) sur DRSUAPI et envoyer les modifications aux objets annuaire.

Dans cette détection Azure ATP, une alerte de sécurité est déclenchée quand un ordinateur du réseau tente de s’enregistrer comme contrôleur de domaine non autorisé.

**TP, B-TP ou FP**

Si l’ordinateur source est un contrôleur de domaine, la résolution qui a peu ou pas de chance de réussir peut empêcher Azure ATP de confirmer l’identification.

1. Vérifiez si l’ordinateur source est un contrôleur de domaine.
    Si la réponse est **oui**, **fermez** l’alerte comme s’agissant d’une activité **B-TP**.

Les changements dans votre instance Active Directory peuvent mettre du temps à se synchroniser.

1. L’ordinateur source est-il un contrôleur de domaine qui vient d’être promu ? Si la réponse est **oui**, **fermez** l’alerte comme s’agissant d’une activité **B-TP**.

Les serveurs et les applications risquent de répliquer les données à partir d’Active Directory, tels que les appareils Azure AD Connect ou les appareils de supervision des performances réseau.

1. Vérifiez si cet ordinateur source est censé générer ce type d’activité.

    * Si la réponse est **oui** alors que l’ordinateur source ne devrait pas continuer la génération de ce type d’activité, corrigez la configuration de l’application/du serveur. **Fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP**.

    * Si la réponse est **oui** et que l’ordinateur source doit continuer à générer ce type d’activité, **fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP** et excluez l’ordinateur pour éviter d’autres alertes bénignes.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).
2. Dans l’observateur d’événements, consultez les [événements Active Directory qu’il enregistre dans le journal des Services d’annuaire](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/). Vous pouvez utiliser le journal pour contrôler les modifications dans Active Directory. Par défaut, Active Directory n’enregistre que les événements d’erreur critique ; cependant, si cette alerte se reproduit, activez cet audit sur le contrôleur de domaine correspondant pour un examen approfondi.

**Suggestions de correction et étapes préventives :**

**Correction :**

1. Incluez l’ordinateur source.
    * Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    * Recherchez les utilisateurs qui étaient connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis.  
    Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.

**Prévention :**

Vérifiez les autorisations suivantes :

1. Répliquer les changements d’annuaire.
2. Répliquer tous les changements d’annuaire.
3. Pour plus d’informations, consultez [Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx). Vous pouvez utiliser [l’analyseur AD ACL](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou créer un script Windows PowerShell pour déterminer qui a ces autorisations dans le domaine.

> [!NOTE]
> Les alertes de promotion suspecte de contrôleur de domaine (attaque DCShadow potentielle) sont prises en charge par les capteurs ATP uniquement.

## <a name="suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029"></a>Suspicion d’attaque DCShadow (demande de réplication du contrôleur de domaine) (ID externe 2029)

*Nom précédent :* Demande de réplication suspecte (attaque DcShadow potentielle)

**Description**

La réplication Active Directory est le processus par lequel les modifications apportées à un contrôleur de domaine sont synchronisées avec d’autres contrôleurs de domaine. Disposant des autorisations nécessaires, les attaquants peuvent accorder des droits pour leur compte d’ordinateur, ce qui leur permet d’emprunter l’identité d’un contrôleur de domaine. Ils s’efforcent de lancer une demande de réplication malveillante, ce qui leur permet de changer des objets Active Directory sur un contrôleur de domaine authentique et d’obtenir éventuellement une persistance dans le domaine.
Dans cette détection, une alerte est déclenchée lorsqu’une demande de réplication suspecte est générée par rapport à un contrôleur de domaine authentique protégé par Azure ATP. Le comportement est révélateur de certaines techniques utilisées dans les attaques DCShadow.

**TP, B-TP ou FP**

Si l’ordinateur source est un contrôleur de domaine, la résolution qui a peu ou pas de chance de réussir peut empêcher Azure ATP d’effectuer l’identification.

1. Vérifiez si l’ordinateur source est un contrôleur de domaine.
    Si la réponse est **oui**, **fermez** l’alerte comme s’agissant d’une activité **B-TP**.

Les changements dans votre instance Active Directory peuvent mettre du temps à se synchroniser.

1. L’ordinateur source est-il un contrôleur de domaine qui vient d’être promu ? Si la réponse est **oui**, **fermez** l’alerte comme s’agissant d’une activité **B-TP**.

Les serveurs et les applications risquent de répliquer les données à partir d’Active Directory, tels que les appareils Azure AD Connect ou les appareils de supervision des performances réseau.

1. Cet ordinateur source était-il censé générer ce type d’activité ?

    * Si la réponse est **oui** alors que l’ordinateur source ne devrait pas continuer la génération de ce type d’activité, corrigez la configuration de l’application/du serveur. **Fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP**.

    * Si la réponse est **oui** et que l’ordinateur source doit continuer à générer ce type d’activité, **fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP** et excluez l’ordinateur pour éviter d’autres alertes **B-TP**.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur](investigate-a-computer.md) source.

**Suggestions de correction et étapes préventives**

**Correction :**

1. Incluez l’ordinateur source.
    * Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    * Recherchez les utilisateurs qui étaient connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis.
    Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
2. Corrigez les données qui ont été répliquées sur les contrôleurs de domaine.

**Prévention :**

Vérifiez les autorisations suivantes :

1. Répliquer les changements d’annuaire.
2. Répliquer tous les changements d’annuaire.
3. Pour plus d’informations, consultez [Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx). Vous pouvez utiliser [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou créer un script Windows PowerShell pour déterminer qui a ces autorisations dans le domaine.

> [!NOTE]
> Les alertes de demande de réplication suspecte (attaque DCShadow potentielle) sont prises en charge par les capteurs ATP uniquement.

## <a name="suspected-dcsync-attack-replication-of-directory-services-external-id-2006"></a>Suspicion d’attaque DCSync (réplication de services d’annuaire) (ID externe 2006)

*Nom précédent :* Réplication malveillante de services d’annuaire

**Description**

La réplication Active Directory est le processus par lequel les modifications apportées à un contrôleur de domaine sont synchronisées avec tous les autres contrôleurs de domaine. Quand les attaquants ont les autorisations nécessaires, ils peuvent lancer une demande de réplication dans le but de récupérer ensuite les données stockées dans Active Directory, y compris les hachages de mot de passe.

Dans cette détection, une alerte est déclenchée quand une demande de réplication est lancée à partir d’un ordinateur qui n’est pas un contrôleur de domaine.

> [!NOTE]
> Si vous avez des contrôleurs de domaine sur lesquels les capteurs Azure ATP ne sont pas installés, ces contrôleurs de domaine ne sont pas couverts par Azure ATP. Si vous déployez un nouveau contrôleur de domaine sur un contrôleur de domaine non inscrit ou non protégé, il peut ne pas être identifié par Azure ATP comme contrôleur de domaine tout de suite. Il est vivement recommandé d’installer le capteur Azure ATP sur chaque contrôleur de domaine pour obtenir une couverture complète.

**TP, B-TP ou FP**

Si l’ordinateur source est un contrôleur de domaine, la résolution qui a peu ou pas de chance de réussir peut empêcher Azure ATP d’effectuer l’identification.

1. Vérifiez si l’ordinateur source est un contrôleur de domaine.
    Si la réponse est **oui**, **fermez** l’alerte comme s’agissant d’une activité **B-TP**.

Les changements dans votre instance Active Directory peuvent mettre du temps à se synchroniser.

1. L’ordinateur source est-il un contrôleur de domaine qui vient d’être promu ? Si la réponse est **oui**, **fermez** l’alerte comme s’agissant d’une activité **B-TP**.

Les serveurs et les applications risquent de répliquer les données à partir d’Active Directory, tels que les appareils Azure AD Connect ou les appareils de supervision des performances réseau.

1. Cet ordinateur source était-il censé générer ce type d’activité ?

    * Si la réponse est **oui** alors que l’ordinateur source ne devrait pas continuer la génération de ce type d’activité, corrigez la configuration de l’application/du serveur. **Fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP**.

    * Si la réponse est **oui** et que l’ordinateur source doit continuer à générer ce type d’activité, **fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP** et excluez l’ordinateur pour éviter d’autres alertes bénignes.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md) et l’[utilisateur](investigate-a-user.md).

**Suggestions de correction et étapes préventives :**

**Correction :**

1. Réinitialisez le mot de passe des utilisateurs source et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
2. Incluez l’ordinateur source.
    * Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    * Recherchez les utilisateurs qui étaient connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.

**Prévention :**

Vérifiez les autorisations suivantes :

1. Répliquer les changements d’annuaire.
2. Répliquer tous les changements d’annuaire.
3. Pour plus d’informations, consultez [Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx). Vous pouvez utiliser [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou créer un script Windows PowerShell pour déterminer qui a ces autorisations dans le domaine.

## <a name="suspected-golden-ticket-usage-encryption-downgrade-external-id-2009"></a>Suspicion d’utilisation de golden ticket (passage à une version antérieure du chiffrement) (ID externe 2009)

*Nom précédent :* Passage à une version antérieure du chiffrement

**Description**

Le passage à une version inférieure du chiffrement est une méthode visant à affaiblir Kerberos en abaissant le niveau de chiffrement de différents champs du protocole qui ont normalement le niveau de chiffrement le plus élevé. Un champ au chiffrement affaibli peut être plus vulnérable à des attaques de force brute en mode hors connexion. Plusieurs méthodes d’attaque exploitent les codes faibles de chiffrement Kerberos. Dans le cadre de cette détection, Azure ATP examine les types de chiffrement Kerberos utilisés par les ordinateurs et les utilisateurs, et déclenche des alertes quand un chiffrement plus faible et inhabituel est utilisé pour l’ordinateur source et/ou l’utilisateur et correspond à une technique d’attaque connue.

Dans une alerte Golden Ticket, la méthode de chiffrement du champ TGT du message TGS_REQ (demande de service) reçu de l’ordinateur source a été détectée comme inférieure par rapport au comportement appris. Cette détection n’est pas basée sur une anomalie de temps (contrairement à l’autre détection Golden Ticket). De plus, dans le cas de cette alerte, Azure ATP n’a pas détecté de demande d’authentification Kerberos associée à la demande de service précédente.

**TP, B-TP ou FP**

Certaines ressources légitimes, qui ne prennent pas en charge le chiffrement renforcé, sont susceptibles de déclencher cette alerte.

1. Les utilisateurs sources partagent-ils tous quelque chose en commun ?
   1. Par exemple, les membres du personnel marketing accèdent-ils tous à une ressource spécifique susceptible de provoquer le déclenchement de l’alerte ?
   2. Vérifiez les ressources auxquelles ces tickets ont accédé.
      * Vérifiez cela dans Active Directory en consultant l’attribut *msDS-SupportedEncryptionTypes* du compte de service de la ressource.
   3. Si une seule ressource fait actuellement l’objet d’un accès, vérifiez qu’il s’agit d’une ressource valide à laquelle ces utilisateurs sont censés accéder.

      Si la réponse à l’une des questions précédentes est **oui**, il s’agit probablement d’une activité **T-BP**. Vérifiez si la ressource peut prendre en charge un code de chiffrement fort, implémentez un code de chiffrement plus fort dans la mesure du possible et **fermez** l’alerte de sécurité.

Les applications peuvent s’authentifier avec un code de chiffrement plus faible. Certaines s’authentifient pour le compte d’utilisateurs, comme les serveurs IIS et SQL.

1. Vérifiez si les utilisateurs sources partagent quelque chose en commun.
    * Par exemple, les membres du personnel de vente utilisent-ils tous une application spécifique qui risque déclencher l’alerte ?
    * Vérifiez s’il existe des applications de ce type sur l’ordinateur source.
    * Vérifiez les rôles de l’ordinateur.  
    Des serveurs fonctionnent-ils avec ces types d’applications ?

     Si la réponse à l’une des questions précédentes est **oui**, il s’agit probablement d’une activité **T-BP**. Vérifiez si la ressource peut prendre en charge un code de chiffrement fort, implémentez un code de chiffrement plus fort dans la mesure du possible et **fermez** l’alerte de sécurité.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source et les ressources](investigate-a-computer.md) qui ont fait l’objet d’un accès.
2. Examinez les [utilisateurs](investigate-a-computer.md).

**Suggestions de correction et étapes préventives**

**Correction**

1. Réinitialisez le mot de passe de l’utilisateur source et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
2. Incluez l’ordinateur source.
    * Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    * Recherchez les utilisateurs connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
    * Si vous avez installé Microsoft Defender ATP, utilisez **klist.exe purger** pour supprimer tous les tickets de la session spécifiée et empêcher toute utilisation ultérieure des tickets.
2. Incluez les ressources auxquelles a accédé ce ticket.
3. Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    * Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. L’invalidation de tous les tickets Kerberos dans le domaine signifie que **tous** les services seront interrompus et ne refonctionneront qu’une fois qu’ils auront été renouvelés ou, dans certains cas, redémarrés.
    * **Planifiez soigneusement avant d’effectuer la double réinitialisation KRBTGT. Celle-ci impacte tous les ordinateurs, serveurs et utilisateurs de l’environnement.**

4. Vérifiez que tous les contrôleurs de domaine avec une version de système d’exploitation antérieure ou égale à Windows Server 2012 R2 sont installés avec [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) et que tous les serveurs et contrôleurs de domaine membres avec une version antérieure ou égale à 2012 R2 sont à jour avec [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg). Pour plus d’informations, consultez  [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx)  et  [Faux PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="suspected-golden-ticket-usage-forged-authorization-data-external-id-2013"></a>Suspicion d’utilisation de golden ticket (données d’autorisation falsifiées) (ID externe 2013)

Nom précédent : Réaffectation de privilèges à l’aide de données d’autorisation falsifiées

**Description**

Des vulnérabilités connues dans les versions antérieures de Windows Server permettent aux attaquants d’obtenir des privilèges supplémentaires par le biais du certificat PAC (Privileged Attribute Certificate), un champ dans le ticket Kerberos qui contient les données d’autorisation de l’utilisateur (dans Active Directory, il s’agit de l’appartenance au groupe).

**TP, B-TP ou FP**

Pour les ordinateurs qui sont corrigés avec MS14-068 (contrôleur de domaine) ou MS11-013 (serveur), les tentatives d’attaque ne réussissent pas et génèrent une erreur Kerberos.

1. Vérifiez si les ressources ont fait l’objet d’un accès dans la liste des preuves d’alerte de sécurité, et si les tentatives ont réussi ou échoué.
2. Vérifiez si les ordinateurs qui ont fait l’objet d’un accès ont été corrigés, comme décrit ci-dessus.
    * Si les ordinateurs ont été corrigés, **fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP**.

Certains systèmes d’exploitation ou applications sont connus pour modifier les données d’autorisation. Par exemple, les services Linux et Unix ont leur propre mécanisme d’autorisation qui peut déclencher l’alerte.

1. L’ordinateur source exécute-t-il un système d’exploitation ou une application qui a son propre mécanisme d’autorisation ?
    * Si l’ordinateur source exécute ce type de mécanisme d’autorisation, mettez à niveau le système d’exploitation ou corrigez la configuration de l’application. **Fermez** l’alerte comme s’agissant d’une activité **B-TP**.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source](investigate-a-computer.md).
2. S’il y a un [utilisateur source](investigate-a-user.md), investiguez.
3. Vérifiez les ressources qui ont fait l’objet d’un accès réussi et [investiguez](investigate-a-computer.md).

**Suggestions de correction et étapes préventives**

1. Réinitialisez le mot de passe de l’utilisateur source et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
2. Incluez l’ordinateur source.
    * Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    * Recherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
3. Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    * Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. L’invalidation de tous les tickets Kerberos dans le domaine signifie que **tous** les services seront interrompus et ne refonctionneront qu’une fois qu’ils auront été renouvelés ou, dans certains cas, redémarrés. Planifiez avec soin avec d’effectuer une double réinitialisation de KRBTGT, car celle-ci impacte tous les ordinateurs, serveurs et utilisateurs de l’environnement.
4. Vérifiez que tous les contrôleurs de domaine avec une version de système d’exploitation antérieure ou égale à Windows Server 2012 R2 sont installés avec [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) et que tous les serveurs et contrôleurs de domaine membres avec une version antérieure ou égale à 2012 R2 sont à jour avec [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg). Pour plus d’informations, consultez  [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx)  et  [Faux PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="suspected-golden-ticket-usage-nonexistent-account-external-id-2027"></a>Suspicion d’utilisation de golden ticket (compte inexistant) (ID externe 2027)

Nom précédent : golden ticket Kerberos

**Description**

Les attaquants ayant des droits d’administrateur de domaine peuvent compromettre le compte KRBTGT. Ils utilisent ensuite ce compte KRBTGT pour créer un ticket TGT (Ticket Granting Ticket) Kerberos qui fournit une autorisation d’accès à toutes les ressources du réseau, et définir l’heure d’expiration du ticket à la valeur de leur choix. Ce faux ticket TGT appelé « Golden Ticket » permet aux attaquants d’obtenir une persistance réseau. Dans cette détection, une alerte est déclenchée par un compte qui n’existe pas.

**TP, B-TP ou FP**

La synchronisation des changements dans Active Directory peut prendre du temps.
1. L’utilisateur est-il un utilisateur de domaine connu et valide ?
2. L’utilisateur a-t-il été récemment ajouté ?
3. L’utilisateur a-t-il été récemment supprimé d’Active Directory  ?

Si la réponse à toutes les questions précédentes est **oui**, **fermez** l’alerte comme s’agissant d’une activité **B-TP**.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source et les ressources qui ont fait l’objet d’un accès](investigate-a-computer.md).

**Suggestions de correction et étapes préventives**

1. Inclure les ordinateurs sources
    * Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    * Recherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
    * Si vous avez installé Microsoft Defender ATP, utilisez **klist.exe purger** pour supprimer tous les tickets de la session spécifiée et empêcher toute utilisation ultérieure des tickets.
2. Incluez les ressources auxquelles a accédé ce ticket.
3. Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    * Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. L’invalidation de tous les tickets Kerberos dans le domaine signifie que **tous** les services seront interrompus et ne refonctionneront qu’une fois qu’ils auront été renouvelés ou, dans certains cas, redémarrés. Planifiez avec soin avec d’effectuer une double réinitialisation de KRBTGT, car celle-ci impacte tous les ordinateurs, serveurs et utilisateurs de l’environnement.

## <a name="suspected-golden-ticket-usage-ticket-anomaly-external-id-2032"></a>Suspicion d’utilisation de golden ticket (anomalie de ticket) (ID externe 2032)

**Description**

Les attaquants ayant des droits d’administrateur de domaine peuvent compromettre le compte KRBTGT. Ils utilisent ensuite ce compte KRBTGT pour créer un ticket TGT (Ticket Granting Ticket) Kerberos qui fournit une autorisation d’accès à toutes les ressources du réseau, et définir l’heure d’expiration du ticket à la valeur de leur choix. Ce faux ticket TGT appelé « Golden Ticket » permet aux attaquants d’obtenir une persistance réseau. Les golden tickets falsifiés de ce type ont des caractéristiques uniques et cette détection est spécialement conçue pour les identifier. 

**TP, B-TP ou FP**

Les services de fédération peuvent générer des tickets qui déclencheront cette alerte.
1. L’ordinateur source héberge-t-il les services de fédération qui génèrent ces types de tickets ?
    * Si l’ordinateur source héberge des services qui génèrent ces types de tickets, fermez l’alerte de sécurité comme s’agissant d’une activité **B-TP**.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source et les ressources qui ont fait l’objet d’un accès](investigate-a-computer.md).
2. Examinez l’[utilisateur source](investigate-a-user.md).

**Suggestions de correction et étapes préventives**

1. Inclure les ordinateurs sources
    * Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    * Recherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
    * Si vous avez installé Microsoft Defender ATP, utilisez **klist.exe purger** pour supprimer tous les tickets de la session spécifiée et empêcher toute utilisation ultérieure des tickets.
2. Incluez les ressources auxquelles a accédé ce ticket.
3. Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    * Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. L’invalidation de tous les tickets Kerberos dans le domaine signifie que **tous** les services sont interrompus et ne refonctionnent qu’après avoir été renouvelés ou, dans certains cas, redémarrés.

    **Planifiez soigneusement avant d’effectuer une double réinitialisation KRBTGT. La réinitialisation impacte tous les ordinateurs, serveurs et utilisateurs de l’environnement.**

## <a name="suspected-golden-ticket-usage-time-anomaly-external-id-2022"></a>Suspicion d’utilisation de golden ticket (anomalie de temps) (ID externe 2022)

Nom précédent : golden ticket Kerberos

**Description**

Les attaquants ayant des droits d’administrateur de domaine peuvent compromettre le compte KRBTGT. Ils utilisent ensuite ce compte KRBTGT pour créer un ticket TGT (Ticket Granting Ticket) Kerberos qui fournit une autorisation d’accès à toutes les ressources du réseau, et définir l’heure d’expiration du ticket à la valeur de leur choix. Ce faux ticket TGT appelé « Golden Ticket » permet aux attaquants d’obtenir une persistance réseau. Cette alerte est déclenchée quand un ticket TGT Kerberos est utilisé depuis plus longtemps que la durée autorisée telle qu’elle est spécifiée dans Durée de vie maximale du ticket utilisateur.

**TP, B-TP ou FP**

1. Au cours des dernières heures, le paramètre **Durée de vie maximale du ticket utilisateur** de la stratégie de sécurité a-t-il fait l’objet de modifications susceptibles d’affecter l’alerte ?
2. Le capteur autonome Azure ATP impliqué dans cette alerte est-il une machine virtuelle ?
    * Si le capteur autonome Azure ATP est impliqué, a-t-il été récemment repris à partir d’un état enregistré ?
3. Le réseau présente-t-il un problème de synchronisation d’heure, où les ordinateurs ne sont pas tous synchronisés ?
    * Cliquez sur le bouton **Télécharger les détails** pour voir le fichier Excel du rapport de l’alerte de sécurité, voir les activités réseau associées et vérifier s’il existe une différence entre « StartTime » et « DomainControllerStartTime ».

Si la réponse aux questions précédentes est **oui**, **fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP**.

**Comprendre l’étendue de la violation**

1. Examinez l’[ordinateur source et les ressources qui ont fait l’objet d’un accès](investigate-a-computer.md).
2. Examinez l’[utilisateur compromis](investigate-a-user.md).

**Suggestions de correction et étapes préventives**

1. Incluez l’ordinateur source.
    * Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    * Recherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
    * Si vous avez installé Microsoft Defender ATP, utilisez **klist.exe purger** pour supprimer tous les tickets de la session spécifiée et empêcher toute utilisation ultérieure des tickets.
2. Incluez les ressources auxquelles a accédé ce ticket.
3. Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    * Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. L’invalidation de tous les tickets Kerberos dans le domaine signifie que **tous** les services sont interrompus et ne refonctionnent qu’après avoir été renouvelés ou, dans certains cas, redémarrés.

    **Planifiez soigneusement avant d’effectuer une double réinitialisation KRBTGT. La réinitialisation impacte tous les ordinateurs, serveurs et utilisateurs de l’environnement.**

## <a name="suspected-skeleton-key-attack-encryption-downgrade-external-id-2010"></a>Suspicion d’attaque Skeleton Key (passage à une version antérieure du chiffrement) (ID externe 2010)

*Nom précédent :* Passage à une version antérieure du chiffrement

**Description**

Le passage à une version inférieure du chiffrement est une méthode visant à affaiblir Kerberos en abaissant le niveau de chiffrement de différents champs du protocole qui ont normalement le niveau de chiffrement le plus élevé. Un champ au chiffrement affaibli peut être plus vulnérable à des attaques de force brute en mode hors connexion. Plusieurs méthodes d’attaque exploitent les codes faibles de chiffrement Kerberos. Dans cette détection, Azure ATP apprend les types de chiffrement Kerberos utilisés par les ordinateurs et les utilisateurs. L’alerte est émise quand un chiffrement plus faible inhabituel est utilisé pour l’ordinateur source et/ou l’utilisateur et correspond à des techniques d’attaque connus.

Skeleton Key est un programme malveillant qui s’exécute sur les contrôleurs de domaine et qui autorise l’authentification auprès du domaine de n’importe quel compte sans connaître son mot de passe. Il utilise souvent des algorithmes de chiffrement plus faibles pour hacher les mots de passe de l’utilisateur sur le contrôleur de domaine. Dans cette alerte, le comportement appris du chiffrement de message KRB_ERR précédent du contrôleur de domaine pour le compte demandant un ticket, a été rétrogradé.

**Comprendre l’étendue de la violation**

1. Examinez le [contrôleur de domaine](investigate-a-computer.md).
2. Vérifiez si Skeleton Key a affecté vos contrôleurs de domaine avec le [scanner écrit par l’équipe Azure ATP](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73).
3. Examinez les [utilisateurs](investigate-a-user.md) et les [ordinateurs](investigate-a-computer.md) impliqués.

**Suggestions de correction et étapes préventives**

1. Réinitialisez les mots de passe des utilisateurs compromis et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
2. Incluez le contrôleur de domaine.
    * Supprimez les programmes malveillants. Pour plus d’informations, voir [Analyse des programmes malveillants Skeleton Key](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).
    * Recherchez les utilisateurs connectés au environs de l’heure où l’activité suspecte s’est produite, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.

## <a name="suspicious-additions-to-sensitive-groups-external-id-2024"></a>Ajouts suspects à des groupes sensibles (ID externe 2024)

**Description**

Des attaquants ajoutent des utilisateurs à des groupes avec des privilèges élevés. Le but d’ajouter des utilisateurs est d’accéder à davantage de ressources et d’obtenir un accès persistant. Cette détection s’appuie sur le profilage des activités de modification des utilisateurs d’un groupe et déclenche une alerte quand un ajout anormal à un groupe sensible est observé. Azure ATP effectue un profilage en continu.

Pour obtenir la définition des groupes sensibles dans Azure ATP, consultez [Gestion des comptes sensibles](sensitive-accounts.md).

La détection s’appuie sur les événements audités sur les contrôleurs de domaine. Assurez-vous que vos contrôleurs de domaine [auditent les événements nécessaires](atp-advanced-audit-policy.md).

**Période d’apprentissage**

Quatre semaines par contrôleur de domaine, à partir du premier événement.

**TP, B-TP ou FP**

Les modifications de groupe légitimes qui se produisent rarement et le système qui n’a pas appris « normalement » peuvent déclencher une alerte. Ces alertes sont considérées comme **B-TP**.
1. La modification du groupe est-elle légitime ?
    * Si la modification du groupe est légitime, **fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP**.

**Comprendre l’étendue de la violation**

1. Examinez les utilisateurs ajoutés aux groupes.
    * Concentrez-vous sur leurs activités une fois qu’ils ont été ajoutés aux groupes sensibles.
2. Examinez l’utilisateur source.
    * Téléchargez le rapport **Modifications des groupes sensibles** pour voir toutes les autres modifications effectuées au cours de la même période et en déterminer les auteurs.
3. Recherchez les ordinateurs auxquels l’utilisateur source s’est connecté aux environs de l’heure de l’activité.

**Suggestions de correction et étapes préventives**

**Correction :**

1. Réinitialisez le mot de passe de l’utilisateur source et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
    * Recherchez l’ordinateur sur lequel l’utilisateur source était actif.
    * Vérifiez les ordinateurs auxquels l’utilisateur s’est connecté aux environs de l’heure de l’activité. Vérifiez si ces ordinateurs sont compromis.
    * Si les utilisateurs sont compromis, réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.

**Prévention :**

1. Pour empêcher de futures attaques, réduisez au minimum le nombre d’utilisateurs autorisés à modifier les groupes sensibles.
2. Installez Privileged Access Management pour Active Directory, si c’est possible.

## <a name="suspicious-service-creation-external-id-2026"></a>Création de service malveillant (ID externe 2026)

*Nom précédent :* Création de service malveillant

**Description**

Un service suspect a été créé sur un contrôleur de domaine dans votre organisation. Cette alerte s’appuie sur l’événement 7045 pour identifier cette activité suspecte.

**TP, B-TP ou FP**

Certaines tâches d’administration sont légitimement effectuées sur les contrôleur de domaine par les stations de travail d’administration, les membres des équipes informatiques et les comptes de service.

1. L’utilisateur/ordinateur source est-il censé exécuter ces types de services sur le contrôleur de domaine ?
    * Si l’utilisateur ou l’ordinateur source est censé exécuter ces types de services, mais ne doit pas continuer, **fermez** l’alerte comme s’agissant d’une activité **B-TP**.
    * Si l’utilisateur ou l’ordinateur source est censé exécuter ces types de services et doit continuer, **fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP** et excluez cet ordinateur.

**Comprendre l’étendue de la violation**

1. Examinez l’[utilisateur source](investigate-a-user.md).
2. Examinez les [ordinateurs de destination](investigate-a-computer.md) sur lesquels ont été créés les services.

**Suggestions de correction et étapes préventives**

**Correction**

1. Réinitialisez le mot de passe de l’utilisateur source et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
2. Incluez les contrôleurs de domaine.
    * Corrigez le service suspect.
    * Recherchez les utilisateurs connectés aux environs de l’heure de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur (MFA) ou, si vous avez configuré les stratégies utilisateur à haut risque pertinentes dans Azure Active Directory Identity Protection, vous pouvez utiliser l'action [**Confirmer que l'utilisateur est compromis**](/cloud-app-security/accounts#governance-actions) dans le portail Cloud App Security.
3. Localisez l’ordinateur sur lequel l’utilisateur source était actif.
    * Vérifiez les ordinateurs auxquels l’utilisateur s’est connecté aux environs de l’heure de l’activité et vérifiez si ces ordinateurs sont également compromis.

**Prévention :**

1. Limitez l’accès à distance aux contrôleurs de domaine à partir d’ordinateurs qui ne sont pas de niveau 0.
2. Implémentez un [accès privilégié](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access) pour autoriser uniquement les machines avec une sécurité renforcée à se connecter aux contrôleurs de domaine pour les administrateurs.
3. Implémentez un accès avec moins de privilèges sur les ordinateurs du domaine pour donner uniquement à des utilisateurs spécifiques le droit de créer des services.

> [!div class="nextstepaction"]
> [Tutoriel sur les alertes d’exfiltration](atp-exfiltration-alerts.md)

## <a name="see-also"></a>Voir aussi

* [Examiner un ordinateur](investigate-a-computer.md)
* [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
* [Utilisation des chemins de mouvement latéral](use-case-lateral-movement-path.md)
* [Alertes de reconnaissance](atp-reconnaissance-alerts.md)
* [Alertes indiquant des informations d’identification compromises](atp-compromised-credentials-alerts.md)
* [Alertes de mouvement latéral](atp-lateral-movement-alerts.md)
* [Alertes d’exfiltration](atp-exfiltration-alerts.md)
* [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
