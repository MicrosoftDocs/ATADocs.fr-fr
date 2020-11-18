---
title: Microsoft Defender pour l’intégration des identités avec Microsoft Defender pour le point de terminaison
description: Comment intégrer Microsoft Defender for Identity à Microsoft Defender for Endpoint pour la couverture complète de la détection des menaces
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 50bb601a00396aefee99d5115b1eb8825e74e39c
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848548"
---
# <a name="integrate-product-long-with-microsoft-defender-for-endpoint"></a>Intégrer [!INCLUDE [Product long](includes/product-long.md)] à Microsoft Defender for Endpoint

[!INCLUDE [Product long](includes/product-long.md)] permet une intégration à [!INCLUDE [Product long](includes/product-long.md)] Defender for Endpoint, pour une solution de protection des menaces encore plus complète. Tandis que [!INCLUDE [Product short](includes/product-short.md)] surveille le trafic sur vos contrôleurs de domaine, Defender for Endpoint surveille vos points de terminaison, en fournissant une interface unique à partir de laquelle vous pouvez protéger votre environnement.

En intégrant Defender for Endpoint dans [!INCLUDE [Product short](includes/product-short.md)] , vous pouvez tirer parti de toute la puissance des deux services et sécuriser votre environnement, notamment :

- Capteurs de comportement de point de terminaison : intégrés dans Windows 10, ces capteurs collectent et traitent les signaux comportementals du système d’exploitation (par exemple, processus, registre, fichier et communications réseau) et envoient ces données de capteur à votre instance Cloud, isolée et privée de Defender pour le point de terminaison.

- Analyse de la sécurité cloud : Grâce au Big Data, au machine learning et à la vision unique de Microsoft sur l’écosystème Windows (par exemple, l’[Outil de suppression de logiciels malveillants Microsoft](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), les produits cloud d’entreprise (par exemple, Microsoft 365) et les ressources en ligne (par exemple, Bing et la réputation d’URL SmartScreen), les signaux comportementaux sont convertis en insights, détections et réponses recommandées aux menaces avancées.

- Informations sur les menaces : générées par Microsoft affluence, équipes de sécurité et complétées par les informations sur les menaces fournies par les partenaires, Threat Intelligence permet à Defender pour le point de terminaison d’identifier les outils, les techniques et les procédures des attaquants, et de générer des alertes lorsque ces activités sont observées dans les données de capteur collectées.

[!INCLUDE [Product short](includes/product-short.md)] la technologie détecte plusieurs activités suspectes, en se concentrant sur plusieurs phases de la chaîne de destruction des attaques informatiques, notamment :

- Reconnaissance, au cours de laquelle les personnes malveillantes vont recueillir des informations sur la façon dont l’environnement est construit, sur les différents assets, et sur les entités qui existent. Elles élaborent généralement leur plan pour les prochaines phases de l’attaque ici.

- Cycle de mouvement latéral, pendant lequel un attaquant investit temps et efforts dans la l'élargissement de sa surface d’attaque au sein de votre réseau.

- Dominance (persistance) de domaine, pendant laquelle un attaquant capture les informations lui permettant de reprendre sa campagne à l’aide de différents ensembles de points d’entrée, d’informations d’identification et de techniques.

En même temps, Defender for Endpoint tire parti de la technologie et de l’expertise Microsoft pour détecter les attaques informatiques sophistiquées, en fournissant :

- Détection d’attaques avancées, basée sur le cloud et les comportements  
Détecte les attaques qui ont fait face à toutes les autres défenses (détection après violations), fournit des alertes corrélées et exploitables pour les adversaires connus et inconnus tentant de masquer leurs activités sur les points de terminaison.

- Chronologie détaillée pour une enquête approfondie et l’atténuation des risques  
Recherchez facilement des comportements suspects ou la portée d’une violation sur n’importe quel ordinateur dans une riche chronologie informatique. Inventaire des fichiers, URL et connexions réseau sur le réseau. Obtenez des informations supplémentaires grâce à la collection et à l’analyse approfondies (« détonation ») pour tous les fichiers et URL.

- Base de connaissances unique intégrée à Threat Intelligence  
La perception inégalée des menaces fournit des détails sur les acteurs et le contexte intentionnel de chaque détection basée sur les renseignements sur les menaces – en associant les sources de renseignement internes et tierces.

## <a name="prerequisites"></a>Prérequis

Pour activer cette fonctionnalité, vous avez besoin d’une licence pour [!INCLUDE [Product short](includes/product-short.md)] et Defender pour le point de terminaison.

<a name="how-to-integrate-azure-atp-with-microsoft-defender-atp"></a>

## <a name="how-to-integrate-product-short-with-defender-for-endpoint"></a>Comment intégrer à [!INCLUDE [Product short](includes/product-short.md)] Defender pour le point de terminaison

1. Sur le portail [!INCLUDE [Product short](includes/product-short.md)], cliquez sur **Configuration**.

    ![[! INCLUDe [Product Short] (includes/Product-Short. MD)] menu de configuration](media/msde-configuration.png)
1. Dans la liste configurations, sélectionnez **Microsoft Defender pour point de terminaison** et définissez le basculement de l’intégration **sur activé**.

    ![Activer l’intégration de Windows Defender](media/msde-enable-integration.png)

1. Dans le [portail Defender pour les points de terminaison](https://securitycenter.windows.com/preferences/advanced), accédez à **paramètres**, **fonctionnalités avancées** et définissez **[!INCLUDE [Product long](includes/product-long.md)] intégration** sur **activé**.

    ![Defender pour le point de terminaison activer l’intégration](media/msde-enable.png)

1. Pour vérifier l’état de l’intégration, dans le [!INCLUDE [Product short](includes/product-short.md)] portail, accédez à **paramètres**  >  **Microsoft Defender pour l’intégration des points de terminaison**. Vous pouvez voir le statut de l’intégration ; en cas de problème, vous verrez une erreur.

## <a name="how-it-works"></a>Fonctionnement

Après [!INCLUDE [Product short](includes/product-short.md)] et Defender pour le point de terminaison sont entièrement intégrés, dans le [!INCLUDE [Product short](includes/product-short.md)] portail, dans la fenêtre contextuelle mini-profil et dans la page profil d’entité, chaque entité qui existe dans Defender pour le point de terminaison comprend un badge pour montrer qu’elle est intégrée à Defender pour le point de terminaison.

 ![Profil d’alertes Defender pour les points de terminaison](media/profile-alerts-msde.png)

Si l’entité contient des alertes dans Defender pour le point de terminaison, un numéro s’affiche à côté du badge pour vous permettre de savoir combien d’alertes ont été générées.

 ![[! INCLUDe [Product Short] (includes/Product-Short. MD)] alertes](media/msde-icon-alerts.png)

Si vous cliquez sur le badge, vous êtes dirigé vers le portail Defender pour les points de terminaison dans lequel vous pouvez afficher et atténuer les alertes. Si l’entité n’est pas reconnue par Defender pour le point de terminaison, le badge est grisé.

 ![Defender pour Endpoint gris](media/msde-grey.png)

À partir du portail Defender pour les points de terminaison, cliquez sur un point de terminaison pour afficher les [!INCLUDE [Product short](includes/product-short.md)] alertes. Si vous cliquez sur les alertes pour cette entité dans Defender pour point de terminaison, la page de profil de l’entité s’ouvre dans [!INCLUDE [Product short](includes/product-short.md)] .

 > [!NOTE]
 > Actuellement, [!INCLUDE [Product short](includes/product-short.md)] l’intégration à Defender pour le point de terminaison prend uniquement en charge les utilisateurs et les ordinateurs de l’annuaire Active Directory local. Les utilisateurs d’Azure AD et les machines virtuelles gérées dans Azure ne sont pas pris en compte dans le cadre de l’intégration

![Defender pour les alertes de point de terminaison](media/msde-alerts.png)

## <a name="see-also"></a>Voir aussi

- [Examen des chemins de mouvement latéral avec [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [Outil de dimensionnement [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/aatpsizingtool)
- [Architecture [!INCLUDE [Product short](includes/product-short.md)]](architecture.md)
- [Installer [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
