---
title: Présentation de la console Advanced Threat Analytics | Microsoft Docs
description: Explique comment se connecter à la console ATA et à ses composants
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6bc3c0ef8860bf95718023234fd55f676a304b1b
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077539"
---
# <a name="working-with-the-ata-console"></a>Utilisation de la console ATA


*S’applique à : Advanced Threat Analytics version 1.9*

Utilisez la console ATA pour surveiller les activités suspectes et les gérer.

Entrez la clé `?` pour obtenir les raccourcis clavier d’accessibilité du portail ATA. 

## <a name="enabling-access-to-the-ata-console"></a>Activation de l’accès à la console ATA
Pour ouvrir une session dans la console ATA, vous devez utiliser le compte d’un utilisateur auquel a été attribué le rôle ATA approprié pour accéder à la console ATA. Pour plus d’informations sur le contrôle d’accès en fonction du rôle (RBAC) dans ATA, consultez [Utilisation de groupes de rôles ATA](ata-role-groups.md).

## <a name="logging-into-the-ata-console"></a>Connexion à la console ATA

>[!NOTE]
 > Depuis ATA 1.8, la procédure de connexion à la console ATA est effectuée en utilisant l’authentification unique.

1. Sur le serveur du centre ATA, cliquez sur l’icône **Console ATA Microsoft** sur le Bureau ou ouvrez un navigateur pour accéder à la console ATA.

    ![Icône du serveur ATA](media/ata-server-icon.png)

   >[!NOTE]
   > Vous pouvez également ouvrir un navigateur à partir du centre ATA ou de la passerelle ATA et accéder à l’adresse IP que vous avez configurée dans l’installation du centre ATA pour la console ATA.    

2. Si l’ordinateur où le centre ATA est installé et l’ordinateur à partir duquel vous tentez d’accéder à la console ATA sont joints à un domaine, ATA prend en charge l’authentification unique intégrée avec l’authentification Windows. Si vous avez déjà ouvert une session sur votre ordinateur, ATA utilise ce jeton pour vous connecter à la console ATA. Vous pouvez aussi vous connecter à l’aide d’une carte à puce. Vos autorisations dans ATA correspondent à votre [rôle administrateur](ata-role-groups.md).

   > [!NOTE]
   > Veillez à ouvrir une session sur l’ordinateur à partir duquel vous voulez accéder à la console ATA en utilisant votre nom d’utilisateur et votre mot de passe d’administrateur ATA. Vous pouvez également exécuter votre navigateur en tant qu’un autre utilisateur, ou vous déconnecter de Windows et ouvrir une session avec votre utilisateur administrateur ATA. Pour faire en sorte que la console ATA demande des informations d’identification, accédez à la console en utilisant une adresse IP : vous êtes alors invité à entrer des informations d’identification.

3. Pour vous connecter à l’aide de l’authentification unique, vérifiez que le site de la console ATA est défini en tant que site intranet local dans votre navigateur et que vous y accédez en utilisant un nom court ou un localhost.

> [!NOTE]
> En plus de la journalisation de chaque alerte d’activité suspecte et d’intégrité, chaque modification de configuration apportée à la console ATA est auditée dans le journal des événements Windows sur l’ordinateur du centre ATA, sous **Journal des applications et des services** puis **Microsoft ATA**. Chaque connexion à la console ATA est également auditée.<br></br>  Les configurations qui affectent la passerelle ATA sont également consignées dans le journal des événements Windows de l’ordinateur de la passerelle ATA. 



## <a name="the-ata-console"></a>Console ATA

La console ATA fournit un aperçu rapide de toutes les activités suspectes par ordre chronologique. Elle vous permet d’examiner les détails de toutes les activités et d’effectuer des actions en fonction de ces activités. La console affiche également des alertes et des notifications pour signaler des problèmes liés au réseau ATA ou aux nouvelles activités considérées comme suspectes.

Voici les principaux éléments de la console ATA.


### <a name="attack-time-line"></a>Chronologie des attaques

Il s’agit de la page de destination qui s’affiche par défaut quand vous vous connectez à la console ATA. Par défaut, toutes les activités suspectes ouvertes sont affichées dans la chronologie des attaques. Vous pouvez filtrer la chronologie des attaques de manière à tout afficher ou à afficher uniquement les activités suspectes dont l’état est Ouvert, Masqué ou Ignoré. Vous pouvez également voir le niveau de gravité attribué à chaque activité.

![Image de la chronologie des attaques ATA](media/ATA-Suspicious-Activity-Timeline.jpg)

Pour plus d’informations, consultez [Gestion des activités suspectes](working-with-suspicious-activities.md).

### <a name="notification-bar"></a>Barre de notification

Quand une activité suspecte est détectée, la barre de notification s’ouvre automatiquement sur la droite. Si de nouvelles activités suspectes ont été détectées depuis la dernière ouverture de session, la barre de notification s’ouvrira après votre connexion. Pour accéder à la barre de notification, vous pouvez cliquer sur la flèche de droite à tout moment.

![Image de la barre de notification ATA](media/notification-bar-1.7.png)

### <a name="whats-new"></a>Nouveautés

Après la publication d’une nouvelle version d’ATA, la fenêtre **Nouveautés** s’affiche en haut à droite pour vous indiquer ce qui a été ajouté dans la dernière version. Elle fournit également un lien vers le téléchargement de cette version.

### <a name="filtering-panel"></a>Filtrage du panneau

Vous pouvez filtrer les activités suspectes qui s’affichent dans la chronologie des attaques ou sous l’onglet Activités suspectes du profil d’entité, selon leur l’état et leur niveau de gravité.

### <a name="search-bar"></a>Barre de recherche

Le menu supérieur comprend une barre de recherche. Vous pouvez rechercher un utilisateur spécifique, un ordinateur ou un groupe dans ATA. Pour tester la fonction de recherche, commencez à taper un nom.

![Image de la recherche dans la console ATA](media/ATA-console-search.png)

### <a name="health-center"></a>Centre d’intégrité

Le centre d’intégrité envoie des alertes quand un élément du déploiement ATA ne fonctionne pas correctement.

![Image du centre d’intégrité ATA](media/ATA-Health-Issue.jpg)

Quand votre système rencontre un problème, par exemple une erreur de connectivité ou une passerelle ATA déconnectée, l’icône du centre d’intégrité vous en informe à l’aide d’un point rouge. ![Image du point rouge du centre d’intégrité ATA](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="sensitive-groups"></a>Groupes sensibles

Les groupes de la liste suivante sont considérés comme **sensibles** par ATA. Une entité qui est membre de ces groupes est considérée comme sensible :

- Contrôleurs de domaine d’entreprise en lecture seule 
- Administrateurs du domaine 
- Contrôleurs de domaine 
- Administrateurs de schéma
- Administrateurs de l’entreprise 
- Propriétaires créateurs de la stratégie de groupe 
- Contrôleurs de domaine en lecture seule 
- Administrateurs  
- Utilisateurs avec pouvoir  
- Opérateurs de compte  
- Opérateurs de serveur   
- Opérateurs d’impression
- Opérateurs de sauvegarde
- Duplicateurs 
- Utilisateurs du Bureau à distance 
- Opérateurs de configuration réseau 
- Générateurs d’approbation de forêt entrante 
- Administrateurs DNS 


### <a name="mini-profile"></a>Mini-profil

Si vous pointez votre souris sur une entité, n'importe où dans la console, où une entité unique et présentée, par exemple un utilisateur ou un ordinateur, un mini-profil s’ouvre automatiquement et affiche les informations suivantes si elles sont disponibles :

![Image du mini-profil dans ATA](media/ATA-mini-profile.jpg)

-   Nom

-   Image

-   E-mail

-   Téléphone

-   Nombre d’activités suspectes par niveau de gravité



## <a name="see-also"></a>Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
