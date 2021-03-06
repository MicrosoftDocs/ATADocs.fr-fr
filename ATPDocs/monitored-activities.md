---
title: Activités de domaine supervisées par Microsoft Defender pour Identity
description: Décrit chacun des types d’activité supervisés par Microsoft Defender pour Identity.
ms.date: 12/24/2020
ms.topic: conceptual
ms.openlocfilehash: 28115bc246f6128aeb2bc408a1107e34796c039a
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533747"
---
# <a name="microsoft-defender-for-identity-monitored-activities"></a>Activités supervisées par Microsoft Defender pour Identity

> [!NOTE]
> Les fonctionnalités [!INCLUDE [Product long](includes/product-long.md)] décrites sur cette page sont également accessibles sur le nouveau [portail](https://portal.cloudappsecurity.com).

[!INCLUDE [Product long](includes/product-long.md)] analyse les informations générées par l’annuaire Active Directory de votre organisation, ainsi que les activités réseau et les activités d’événement. L’objectif est de détecter les activités suspectes. Les informations relatives aux activités supervisées permettent à [!INCLUDE [Product short](includes/product-short.md)] de déterminer la validité de toutes les menaces potentielles, de les trier correctement et d’y répondre.

En cas de menace réelle ou de **vrai positif**, [!INCLUDE [Product short](includes/product-short.md)] vous permet de découvrir l’étendue de la violation pour chaque incident, d’examiner les entités impliquées et de déterminer comment y remédier.

Les informations supervisées par [!INCLUDE [Product short](includes/product-short.md)] sont présentées sous la forme d’activités. [!INCLUDE [Product short](includes/product-short.md)] prend actuellement en charge la supervision des types d’activités suivants :

> [!NOTE]
>
> - Cet article s’applique pour tous les types de capteurs [!INCLUDE [Product short](includes/product-short.md)].
> - Les activités supervisées par [!INCLUDE [Product short](includes/product-short.md)] s’affichent à la fois sur la page de profil de l’utilisateur et sur celle de la machine.
> - [!INCLUDE [Product short](includes/product-short.md)] activités contrôlées sont également disponibles dans la page [Chasse avancée](https://portal.cloudappsecurity.com/) de [Cloud App Security](https://security.microsoft.com/advanced-hunting) et Microsoft 365 Defender.

## <a name="monitored-user-activities-user-account-ad-attribute-changes"></a>Activités surveillées des utilisateurs : Changements d’attributs AD du compte d’utilisateur

|Activité supervisée|Description|
|---------------------|------------------|
|Changement de l’état de délégation contrainte du compte|La délégation a été activée ou désactivée pour le compte.|
|Changement des SPN de délégation contrainte du compte|La délégation contrainte restreint les services sur lesquels le serveur spécifié peut agir pour le compte d’un utilisateur.|
|Changement de l’état d’activation du compte|Indique si un compte est activé ou désactivé.|
|Expiration du compte|Date à laquelle le compte expire.|
|Changement de la date d’expiration du compte|La date à laquelle le compte expire a été changée.|
|Changement de l’état de verrouillage du compte|La date à laquelle le compte expire a été changée.|
|Changement du mot de passe du compte|L’utilisateur a modifié son mot de passe.|
|Expiration du mot de passe du compte|Le mot de passe de l’utilisateur a expiré.|
|Activation de l’option Le mot de passe n’expire jamais pour le compte|Le mot de passe de l’utilisateur a été configuré pour ne jamais expirer.|
|Activation de l’option Mot de passe non nécessaire pour le compte|Le compte d’utilisateur a été configuré pour permettre la connexion avec un mot de passe vide.|
|Changement du compte pour exiger une carte à puce|Le compte a été configuré pour exiger que les utilisateurs se connectent à un appareil à l’aide d’une carte à puce.|
|Changement des types de chiffrement pris en charge dans le compte|Les types de chiffrement pris en charge par Kerberos ont été modifiés (types : Des, AES 129, AES 256)|
|Changement du nom UPN du compte|Le nom de principal de l’utilisateur a été changé.|
|Changement de l’appartenance au groupe|L’utilisateur a été ajouté à un groupe ou supprimé d’un groupe par un autre utilisateur ou par lui-même.|
|Changement de la messagerie de l’utilisateur|L’attribut Messagerie de l’utilisateur a été changé.|
|Changement du responsable de l’utilisateur|L’attribut Responsable de l’utilisateur a été changé.|
|Changement du numéro de téléphone de l’utilisateur|L’attribut Numéro de téléphone de l’utilisateur a été changé.|
|Changement du poste de l’utilisateur|L’attribut Poste de l’utilisateur a été changé.|

<!-- Rollback
|SID-History Changed|Account's SID-History attribute was changed.|
-->

## <a name="monitored-user-activities-ad-security-principal-operations"></a>Activités surveillées des utilisateurs : Opérations de principal de sécurité AD

|Activité supervisée|Description|
|---------------------|------------------|
|Création du principal du service|Le compte a été créé (utilisateur et ordinateur).|
|Changement de l’état de suppression du principal de sécurité|Le compte a été supprimé ou restauré (utilisateur et ordinateur).|
|Changement du nom d’affichage du principal de sécurité|Le nom d’affichage X du compte a été remplacé par Y.|
|Changement du nom du principal de sécurité|L’attribut Nom du compte a été changé.|
|Changement du chemin du principal de sécurité|Le nom unique X du compte a été remplacé par Y.|
|Changement du nom SAM du principal de sécurité|Le nom SAM a été changé (SAM est le nom d’ouverture de session utilisé pour les clients et les serveurs exécutant des versions antérieures du système d’exploitation).|

## <a name="monitored-user-activities-domain-controller-based-user-operations"></a>Activités surveillées des utilisateurs : Opérations de l’utilisateur basées sur le contrôleur de domaine

|Activité supervisée|Description|
|---------------------|------------------|
|Réplication du service d’annuaire|L’utilisateur a tenté de répliquer le service d’annuaire.|
|Requête DNS|Type de requête effectuée par l’utilisateur sur le contrôleur de domaine (**AXFR**,**TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**).|
|Extraction de données privées|L’utilisateur a tenté ou a réussi à interroger des données privées à l’aide du protocole LSARPC.|
|Création de service|L’utilisateur a tenté de créer un service sur un ordinateur distant.|
|Énumération des sessions SMB|L’utilisateur a tenté d’énumérer tous les utilisateurs ayant une session SMB ouverte sur les contrôleurs de domaine.|
|Copie de fichiers SMB|Fichiers copiés par l’utilisateur à l’aide de SMB|
|Requête SAMR|L’utilisateur a exécuté une requête SAMR.|
|Planification des tâches|L’utilisateur a tenté de planifier la tâche X sur un ordinateur distant.|
|Exécution WMI|L’utilisateur a tenté d’exécuter à distance une méthode WMI.|

## <a name="monitored-user-activities-login-operations"></a>Activités surveillées des utilisateurs : Opérations de connexion

|Type d’ouverture de session|Activité supervisée|Description|
|---------------------|---------------------|------------------|
|Type d’ouverture de session 2|Validation des informations d’identification|Événement d’authentification de compte de domaine utilisant les méthodes d’authentification NTLM et Kerberos.|
|Type d’ouverture de session 2|Ouverture de session interactive|L’utilisateur a obtenu un accès réseau en entrant un nom d’utilisateur et un mot de passe (méthode d’authentification Kerberos ou NTLM).|
|Type d’ouverture de session 2|Ouverture de session interactive avec un certificat|L’utilisateur a obtenu un accès réseau à l’aide d’un certificat.|
|Type d’ouverture de session 2|Connexion VPN|L’utilisateur s’est connecté via l’authentification VPN à l’aide du protocole RADIUS.|
|Type d’ouverture de session 3|Accès aux ressources|L’utilisateur a accédé à une ressource à l’aide de l’authentification Kerberos ou NTLM.|
|Type d’ouverture de session 3|Accès délégué aux ressources|L’utilisateur a accédé à une ressource à l’aide de la délégation Kerberos.|
|Type d’ouverture de session 8|Texte en clair LDAP|L’utilisateur s’est authentifié à l’aide du protocole LDAP avec un mot de passe en texte clair (authentification simple).|
|Type d’ouverture de session 10|Bureau à distance|L’utilisateur a ouvert une session RDP sur un ordinateur distant à l’aide de l’authentification Kerberos.|
|---|Échec de l’ouverture de session|La tentative d’authentification du compte de domaine (via NTLM et Kerberos) a échoué pour l’une des raisons suivantes : le compte a été désactivé ou verrouillé, il a expiré ou il a utilisé un certificat non approuvé, ou une tentative d’ouverture de session non valide a été effectuée (heure d’ouverture de session non valide, utilisation d’un ancien mot de passe, expiration du mot de passe ou mot de passe incorrect).|
|---|Échec de l’ouverture de session avec un certificat|La tentative d’authentification du compte de domaine (par Kerberos) a échoué pour l’une des raisons suivantes : compte désactivé, expiré ou verrouillé, certificat non approuvé, heure d’ouverture de session non valide, ancien mot de passe, mot de passe expiré ou mot de passe incorrect.|

## <a name="monitored-machine-activities-machine-account"></a>Activités surveillées des machines : Compte d’ordinateur

|Activité supervisée|Description|
|---------------------|------------------|
|Modification du système d’exploitation de l’ordinateur|Le système d’exploitation de l’ordinateur a été modifié.

## <a name="see-also"></a>Voir aussi

- [Gestion des alertes de sécurité](working-with-suspicious-activities.md)
- [Guide sur les alertes de sécurité](suspicious-activity-guide.md)
- [Examiner les entités](investigate-entity.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
