---
title: Présentation du portail Microsoft Defender pour Identity
description: Explique comment se connecter au portail Microsoft Defender pour Identity et à ses composants.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e695bd20717bbb26cffcd5a6cb069eb2c520c876
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847596"
---
# <a name="working-with-the-product-long-portal"></a>Utilisation du portail [!INCLUDE [Product long](includes/product-long.md)]

> [!NOTE]
> Toutes les fonctionnalités [!INCLUDE [Product long](includes/product-long.md)] décrites sur cette page sont également accessibles sur le nouveau [portail Cloud App Security](https://portal.cloudappsecurity.com).

Utilisez le portail [!INCLUDE [Product long](includes/product-long.md)] pour superviser les activités suspectes détectées par [!INCLUDE [Product short](includes/product-short.md)] et y répondre.

Entrez la clé `?` pour obtenir les raccourcis clavier d’accessibilité du portail [!INCLUDE [Product short](includes/product-short.md)].

Le portail [!INCLUDE [Product short](includes/product-short.md)] offre un aperçu de toutes les activités suspectes par ordre chronologique. Elle vous permet d’examiner les détails de toutes les activités et d’effectuer des actions en fonction de ces activités. Le portail [!INCLUDE [Product short](includes/product-short.md)] affiche également des alertes et des notifications relatives à des problèmes détectés par [!INCLUDE [Product short](includes/product-short.md)] ou à de nouvelles activités considérées comme suspectes.

Cet article explique comment utiliser les éléments clés du portail [!INCLUDE [Product short](includes/product-short.md)].

## <a name="enabling-access-to-the-product-short-portal"></a>Activation de l’accès au portail [!INCLUDE [Product short](includes/product-short.md)]

Vous devez vous connecter au portail [!INCLUDE [Product short](includes/product-short.md)] en tant qu’utilisateur affecté à un groupe de sécurité Azure Active Directory y ayant accès.
Pour plus d’informations sur le contrôle d’accès en fonction du rôle (RBAC) dans [!INCLUDE [Product short](includes/product-short.md)], consultez [Utilisation de groupes de rôles [!INCLUDE [Product short](includes/product-short.md)]](role-groups.md).

## <a name="logging-into-the-product-short-portal"></a>Connexion au portail [!INCLUDE [Product short](includes/product-short.md)]

1. Vous avez deux possibilités pour accéder au portail [!INCLUDE [Product short](includes/product-short.md)] : connectez-vous au portail [https://portal.atp.azure.com](https://portal.atp.azure.com) et sélectionnez votre instance, ou bien accédez à l’URL de l’instance (`https://*instancename*.atp.azure.com` ).

1. [!INCLUDE [Product short](includes/product-short.md)] prend en charge l’authentification unique intégrée à l’authentification Windows : si vous avez déjà ouvert une session sur votre ordinateur, il utilise ce jeton pour vous connecter au portail [!INCLUDE [Product short](includes/product-short.md)]. Vous pouvez aussi vous connecter à l’aide d’une carte à puce. Vos autorisations dans [!INCLUDE [Product short](includes/product-short.md)] correspondent à votre [rôle Administrateur](role-groups.md).

   > [!NOTE]
   > Veillez à ouvrir une session sur l’ordinateur à partir duquel vous voulez accéder au portail [!INCLUDE [Product short](includes/product-short.md)] avec votre nom d’utilisateur et votre mot de passe d’administrateur [!INCLUDE [Product short](includes/product-short.md)]. Vous pouvez également exécuter votre navigateur sous l’identité d’un autre utilisateur ou fermer votre session Windows, puis en ouvrir une autre avec votre utilisateur administrateur [!INCLUDE [Product short](includes/product-short.md)]. Contrairement au portail [!INCLUDE [Product short](includes/product-short.md)], le nouveau [portail Cloud App Security](https://portal.cloudappsecurity.com) offre une connexion multi-utilisateur. Par ailleurs, aucune licence supplémentaire n’est nécessaire pour une utilisation avec [!INCLUDE [Product short](includes/product-short.md)].

### <a name="attack-time-line"></a>Chronologie des attaques

La page de destination qui s’affiche par défaut en cas de connexion au portail [!INCLUDE [Product short](includes/product-short.md)] est la chronologie des attaques. Par défaut, toutes les activités suspectes ouvertes sont affichées dans la chronologie des attaques. Vous pouvez filtrer la chronologie des attaques de manière à tout afficher ou à afficher uniquement les activités suspectes dont l’état est Ouvert, Masqué ou Ignoré. Vous pouvez également voir le niveau de gravité attribué à chaque activité.

![Image de chronologie des attaques [!INCLUDE [Product short](includes/product-short.md)]](media/sa-timeline.png)

Pour plus d’informations, consultez [Utilisation des alertes de sécurité](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Nouveautés

Après la publication d’une nouvelle version de [!INCLUDE [Product short](includes/product-short.md)], la fenêtre **Nouveautés** s’affiche en haut à droite pour vous indiquer ce qui a été ajouté dans la dernière version. Elle fournit également un lien vers le téléchargement de cette version.

### <a name="filtering-panel"></a>Filtrage du panneau

Vous pouvez filtrer les activités suspectes qui s’affichent dans la chronologie des attaques ou sous l’onglet Activités suspectes du profil d’entité, selon leur l’état et leur niveau de gravité.

<a name="search-bar"></a>

### <a name="search-bar"></a>Barre de recherche

Le menu supérieur comprend une barre de recherche. Vous pouvez rechercher un utilisateur spécifique, un ordinateur ou un groupe dans [!INCLUDE [Product short](includes/product-short.md)]. Pour tester la fonction de recherche, commencez à taper un nom. Au bas de la barre de recherche, le nombre de résultats de recherche trouvés est indiqué.

![Image de recherche sur le portail [!INCLUDE [Product short](includes/product-short.md)]](media/workspace-portal-search.png)

Si vous cliquez sur ce nombre, vous pouvez accéder à la page des résultats de recherche, dans laquelle vous pouvez filtrer les résultats par type d’entité pour un examen approfondi.

![Recherche de résultats](media/search-results.png)

### <a name="health-center"></a>Centre d’intégrité

Le centre d’intégrité envoie des alertes quand un élément de l’instance [!INCLUDE [Product short](includes/product-short.md)] ne fonctionne pas correctement.

![Image du centre d’intégrité [!INCLUDE [Product short](includes/product-short.md)]](media/health-issue.png)

Quand votre système rencontre un problème (par exemple, une erreur de connectivité ou un capteur autonome [!INCLUDE [Product short](includes/product-short.md)] déconnecté), un point rouge apparaît sur l’icône du centre d’intégrité pour vous en informer.

![Image de point rouge du centre d’intégrité [!INCLUDE [Product short](includes/product-short.md)]](media/health-bar.png)

### <a name="sensitive-groups"></a>Groupes sensibles

Pour plus d’informations sur les groupes sensibles dans [!INCLUDE [Product short](includes/product-short.md)], consultez [Utilisation des groupes sensibles](sensitive-accounts.md).

### <a name="mini-profile"></a>Mini-profil

Si vous pointez votre souris sur une entité, sur un endroit du portail [!INCLUDE [Product short](includes/product-short.md)] où apparaît une entité unique (par exemple, un utilisateur ou un ordinateur), un mini-profil s’ouvre automatiquement. Il affiche les informations suivantes si elles sont disponibles et pertinentes :

![Image du mini-profil [!INCLUDE [Product short](includes/product-short.md)]](media/mini-profile.png)

- Nom
- Titre
- Service
- Balises AD
- E-mail
- Office
- Numéro de téléphone
- Domaine
- Nom SAM
- Créé le – Date et heure où l’entité a été créée dans Active Directory. Si elle a été créée avant que [!INCLUDE [Product short](includes/product-short.md)] ne commence la supervision, ces informations ne sont pas affichées.
- Première consultation – Première fois où [!INCLUDE [Product short](includes/product-short.md)] a observé une activité provenant de cette entité.
- Dernière consultation – Dernière fois où [!INCLUDE [Product short](includes/product-short.md)] a observé une activité provenant de cette entité.
- Badge d’association de sécurité – S’affiche si des activités suspectes sont associées à cette entité.
- Badge WD ATP – S’affiche s’il existe des activités suspectes associées à cette entité dans Microsoft Defender pour point de terminaison.
- Badge de chemins de mouvement latéral – S’affiche si des chemins de mouvement latéral ont été détectés pour cette entité au cours des deux derniers jours.

## <a name="see-also"></a>Voir aussi

- [Création d’instances [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
