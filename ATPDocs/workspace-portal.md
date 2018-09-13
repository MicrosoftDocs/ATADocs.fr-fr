---
title: Présentation du portail d’espace de travail Azure - Protection avancée contre les menaces | Microsoft Docs
description: Décrit comment se connecter au portail d’espace de travail Azure ATP et aux composants de ce portail d’espace de travail
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0fa8c1e19fde1ec779699b3a2c5411dea0908451
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166289"
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="working-with-the-azure-atp-workspace-portal"></a>Utilisation du portail d’espace de travail Azure ATP

Utilisez le portail d’espace de travail Azure ATP pour surveiller les activités suspectes détectées par ATP et y répondre.

Entrez la clé `?` pour obtenir les raccourcis clavier d’accessibilité au portail d’espace de travail Azure ATP. 

Le portail d’espace de travail Azure ATP fournit un aperçu rapide de toutes les activités suspectes par ordre chronologique. Elle vous permet d’examiner les détails de toutes les activités et d’effectuer des actions en fonction de ces activités. Le portail d’espace de travail affiche également des alertes et des notifications pour signaler des problèmes détectés par Azure ATP ou de nouvelles activités considérées suspectes.

Cet article décrit comment utiliser les éléments clés du portail d’espace de travail Azure ATP.


## <a name="enabling-access-to-the-azure-atp-workspace-portal"></a>Activation de l’accès au portail d’espace de travail Azure ATP
Pour pouvoir vous connecter au portail d’espace de travail Azure ATP, vous devez vous connecter en tant qu’utilisateur auquel le groupe de sécurité Azure Active Directory approprié a été affecté pour accéder au portail d’espace de travail Azure ATP. Pour plus d’informations sur le contrôle d’accès en fonction du rôle (RBAC) dans Azure ATP, consultez [Utilisation de groupes de rôles Azure ATP](atp-role-groups.md).

## <a name="logging-into-the-azure-atp-workspace-portal"></a>Connexion au portail d’espace de travail Azure ATP

1. Vous pouvez entrer sur le portail d’espace de travail en vous connectant au portail de gestion d’espace de travail [https://portal.atp.azure.com](https://portal.atp.azure.com), puis en sélectionnant l’espace de travail approprié ou en accédant à l’URL d’espace de travail : [https://*nom_espace_de_travail*.atp.azure.com](https://*workspacename*.atp.azure.com).


2.  Azure ATP prend en charge l’authentification unique intégrée à l’authentification Windows : si vous avez déjà ouvert une session sur votre ordinateur, Azure ATP utilise ce jeton pour vous connecter au portail d’espace de travail Azure ATP. Vous pouvez aussi vous connecter à l’aide d’une carte à puce. Vos autorisations dans Azure ATP correspondent à votre [rôle d’administrateur](atp-role-groups.md).

 > [!NOTE]
 > Veillez à ouvrir une session sur l’ordinateur à partir duquel vous voulez accéder au portail d’espace de travail Azure ATP en utilisant votre nom d’utilisateur et votre mot de passe d’administrateur Azure ATP. Vous pouvez également exécuter votre navigateur en tant qu’un autre utilisateur, ou fermer votre session Windows et vous connecter avec votre utilisateur administrateur d’Azure ATP. 


### <a name="attack-time-line"></a>Chronologie des attaques

Il s’agit de la page de destination qui s’affiche par défaut quand vous vous connectez au portail d’espace de travail Azure ATP. Par défaut, toutes les activités suspectes ouvertes sont affichées dans la chronologie des attaques. Vous pouvez filtrer la chronologie des attaques de manière à tout afficher ou à afficher uniquement les activités suspectes dont l’état est Ouvert, Masqué ou Ignoré. Vous pouvez également voir le niveau de gravité attribué à chaque activité.

![Image de la chronologie des attaques Azure ATP](media/atp-sa-timeline.png)

Pour plus d’informations, consultez [Gestion des activités suspectes](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Nouveautés

Après la publication d’une nouvelle version d’Azure ATP, la fenêtre **Nouveautés** s’affiche dans le coin supérieur droit pour vous indiquer ce qui a été ajouté dans la dernière version. Elle fournit également un lien vers le téléchargement de cette version.

### <a name="filtering-panel"></a>Filtrage du panneau

Vous pouvez filtrer les activités suspectes qui s’affichent dans la chronologie des attaques ou sous l’onglet Activités suspectes du profil d’entité, selon leur l’état et leur niveau de gravité.

### Barre de recherche <a name="search-bar"></a>

Le menu supérieur comprend une barre de recherche. Vous pouvez rechercher un utilisateur spécifique, un ordinateur ou un groupe dans Azure ATP. Pour tester la fonction de recherche, commencez à taper un nom. Au bas de la barre de recherche, le nombre de résultats de recherche trouvés est indiqué. 

![Image de recherche dans le portail d’espace de travail Azure ATP](media/atp-workspace-portal-search.png)

Si vous cliquez sur ce nombre, vous pouvez accéder à la page des résultats de recherche, dans laquelle vous pouvez filtrer les résultats par type d’entité pour un examen approfondi.

![Recherche de résultats](media/search-results.png)

### <a name="health-center"></a>Centre d’intégrité

Le centre d’intégrité envoie des alertes quand un élément de votre espace de travail Azure ATP ne fonctionne pas correctement.

![Image du centre d’intégrité Azure ATP](media/atp-health-issue.png)

Quand votre système rencontre un problème, tel qu’une erreur de connectivité ou la déconnexion d’un capteur autonome Azure ATP, un point rouge apparaît sur l’icône du centre d’intégrité pour vous en informer. 

![Image du point rouge dans le centre d’intégrité Azure ATP](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>Groupes sensibles

Pour obtenir des informations sur les groupes sensibles dans ATP, consultez [Utilisation de groupes sensibles](sensitive-accounts.md).

### <a name="mini-profile"></a>Mini-profil

Si vous pointez votre souris sur une entité, n'importe où dans le portail d’espace de travail, où une entité unique est présentée, par exemple un utilisateur ou un ordinateur, un mini-profil s’ouvre automatiquement et affiche les informations suivantes si elles sont disponibles et appropriées :

![Image du mini-profil dans Azure ATP](media/atp-mini-profile.png)

- Nom
- Titre
- Service
- Balises AD
- E-mail
- Office
- Numéro de téléphone
- Domaine
- Nom SAM
- Créé le – Date et heure où l’entité a été créée dans Active Directory. Si elle a été créée avant qu’Azure ATP commence la surveillance, ces informations ne sont pas affichées.
- Première consultation – Première fois où Azure ATP a observé une activité à partir de cette entité.
- Dernière consultation – Dernière fois où Azure ATP a observé une activité à partir de cette entité.
- Badge d’association de sécurité – S’affiche si des activités suspectes sont associées à cette entité.
- Badge WD ATP – S’affiche si des activités suspectes dans Windows Defender ATP sont associées à cette entité.
- Badge de chemins de mouvement latéral – S’affiche si des chemins de mouvement latéral ont été détectés pour cette entité au cours des deux derniers jours.


## <a name="see-also"></a>Voir aussi

- [Création d’espaces de travail Azure ATP](install-atp-step1.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)