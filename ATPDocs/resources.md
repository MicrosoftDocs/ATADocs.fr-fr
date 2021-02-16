---
title: Liste des ressources utiles pour Microsoft Defender pour l’identité
description: Cet article fournit une liste de ressources utiles pour Microsoft Defender pour l’identité
ms.date: 10/27/2020
ms.topic: conceptual
ms.openlocfilehash: 8a814a51fdc63f59b36288922017280e0d7f3968
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533305"
---
# <a name="microsoft-defender-for-identity-readiness-guide"></a>Guide Microsoft Defender pour Identity Readiness

Cet article vous fournit une liste de ressources qui vous aideront à vous familiariser avec [!INCLUDE [Product long](includes/product-long.md)] .

## <a name="understanding-microsoft-defender-for-identity"></a>Comprendre Microsoft Defender for Identity

[!INCLUDE [Product long](includes/product-long.md)] est un service Cloud qui permet d’identifier et de protéger votre entreprise à partir de plusieurs types d’attaques informatiques ciblées avancées et de menaces internes.

Pour en savoir plus sur [!INCLUDE [Product short](includes/product-short.md)] :

- [[!INCLUDE [Product short](includes/product-short.md)] vue](what-is.md)
- [[!INCLUDE [Product short](includes/product-short.md)] vidéo d’introduction (25 minutes)-Full](https://www.youtube.com/watch?v=EGY2m8yU_KE)
- [[!INCLUDE [Product short](includes/product-short.md)] vidéo de présentation approfondie (75 minutes)-Full](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

## <a name="deployment-decisions"></a>Décisions de déploiement

[!INCLUDE [Product short](includes/product-short.md)] est constitué d’un service Cloud résidant dans Azure et de capteurs intégrés qui peuvent être installés sur les contrôleurs de domaine. Si vous utilisez des serveurs physiques, il est essentiel de planifier la capacité. Aidez-vous de l’outil de dimensionnement pour allouer de l’espace à vos capteurs :

- [ [!INCLUDE [Product short](includes/product-short.md)] outil de dimensionnement](https://aka.ms/aatpsizingtool) : l’outil de dimensionnement automatise la collecte de la quantité de moniteurs de trafic [!INCLUDE [Product short](includes/product-short.md)] . Il fournit automatiquement des recommandations de prise en charge et de ressource pour les capteurs.
- [[!INCLUDE [Product short](includes/product-short.md)] conseils sur la planification de la capacité](capacity-planning.md)

## <a name="deploy-defender-for-identity"></a>Déployer Defender pour l’identité

Utilisez ces ressources pour vous aider à configurer [!INCLUDE [Product short](includes/product-short.md)] , à vous connecter à Active Directory, à télécharger le package de capteurs, à configurer la collecte d’événements et éventuellement à l’intégrer à votre VPN, ainsi qu’à configurer des comptes et des exclusions honeytoken.

- [Try [!INCLUDE [Product short](includes/product-short.md)] (partie de EMS E5)](https://aka.ms/aatptrial)  la version d’évaluation est valide pendant 90 jours.
- [ [!INCLUDE [Product short](includes/product-short.md)] Configurer](install-step1.md) pour déployer [!INCLUDE [Product short](includes/product-short.md)] dans votre environnement, procédez comme suit.
- [Intégrer [!INCLUDE [Product short](includes/product-short.md)] à Microsoft Defender for Endpoint](integrate-mde.md)

## <a name="defender-for-identity-settings"></a>Defender pour les paramètres d’identité

Lorsque vous créez votre [!INCLUDE [Product short](includes/product-short.md)] instance, les paramètres de base nécessaires sont configurés automatiquement. Il existe plusieurs paramètres configurables supplémentaires dans [!INCLUDE [Product short](includes/product-short.md)] pour améliorer la détection et la précision des alertes pour votre environnement, tels que l’intégration VPN, les autorisations requises Sam et les paramètres de stratégie d’audit avancés.

- [Intégration VPN](install-step6-vpn.md)
- [Autorisations SAM-R](install-step8-samr.md)
- [Paramètres de stratégie d’audit](configure-windows-event-collection.md) : auditer l’intégrité de votre contrôleur de domaine avant et après un [!INCLUDE [Product short](includes/product-short.md)] déploiement.

## <a name="work-with-defender-for-identity"></a>Utiliser Defender pour l’identité

Une fois que [!INCLUDE [Product short](includes/product-short.md)] est opérationnel, affichez les alertes de sécurité dans la chronologie de l' [!INCLUDE [Product short](includes/product-short.md)] activité du portail. La chronologie de l’activité est la page d’accueil par défaut après la connexion au [!INCLUDE [Product short](includes/product-short.md)] portail. Par défaut, toutes les alertes de sécurité ouvertes sont affichées dans la chronologie des activités. Vous pouvez également voir le niveau de gravité attribué à chaque alerte. Examinez chaque alerte en explorant les entités (ordinateurs, appareils, utilisateurs) et en ouvrant leurs pages de profil qui contiennent des informations supplémentaires. Les chemins de mouvement latéral montrent les possibles mouvements dans votre réseau ainsi que les utilisateurs sensibles à risque. Évaluez l’exposition et prenez des mesures correctives en vous aidant des graphiques de détection des chemins de mouvement latéral. Ces ressources vous aident à utiliser les [!INCLUDE [Product short](includes/product-short.md)] alertes de sécurité de :

- [ [!INCLUDE [Product short](includes/product-short.md)] Guide d’alerte de sécurité](suspicious-activity-guide.md) Apprenez à trier et suivez les étapes suivantes avec vos [!INCLUDE [Product short](includes/product-short.md)] détections.
- [[!INCLUDE [Product short](includes/product-short.md)] chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Identifier des groupes comme sensibles](sensitive-accounts.md) Gagnez en visibilité dans l’exposition des informations d’identification sur les groupes de sécurité sensibles.

## <a name="security-best-practices"></a>Meilleures pratiques en matière de sécurité

- Forum [ [!INCLUDE [Product short](includes/product-short.md)] aux questions](technical-faq.yml) (FAQ) : cet article fournit une liste de questions fréquemment posées sur [!INCLUDE [Product short](includes/product-short.md)] et fournit des conseils et des réponses.

## <a name="community-resources"></a>Ressources communautaires

Blog : [ [!INCLUDE [Product short](includes/product-short.md)] blog](https://aka.ms/aatpblog)

Communauté publique : [ [!INCLUDE [Product short](includes/product-short.md)] communauté technique](https://aka.ms/AatpCom)

Communauté privée : [ [!INCLUDE [Product short](includes/product-short.md)] groupe Yammer](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all&preserve-view=true)

Channel 9 : [Page Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="see-also"></a>Voir aussi

- [Utilisation de comptes sensibles](sensitive-accounts.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
