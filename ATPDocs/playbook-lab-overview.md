---
title: Vue d’ensemble des tutoriels du labo des alertes de sécurité Microsoft Defender pour Identity
description: Cette vue d’ensemble des tutoriels décrit les quatre parties du labo des alertes de sécurité Microsoft Defender pour Identity visant à simuler des menaces à des fins de détection par Defender pour Identity.
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: 61602a6bb7d3037d2278c2f492395ed058e8910b
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533560"
---
# <a name="tutorial-overview-microsoft-defender-for-identity-security-alert-lab"></a>Présentation du tutoriel : Labo des alertes de sécurité Microsoft Defender pour Identity

L’objectif des tutoriels du labo des alertes de sécurité [!INCLUDE [Product long](includes/product-long.md)] est d’illustrer les fonctionnalités de **[!INCLUDE [Product short](includes/product-short.md)]** concernant l’identification et la détection des activités suspectes et des attaques potentielles du réseau. Ces quatre tutoriels expliquent comment installer et configurer un environnement fonctionnel pour tester certaines détections *discrètes* de [!INCLUDE [Product short](includes/product-short.md)]. Ce labo se concentre sur les fonctionnalités liées à la *signature* de [!INCLUDE [Product short](includes/product-short.md)]. Ce labo n’inclut ni le Machine Learning avancé, ni les détections de comportements basées sur utilisateur ou l’entité, car celles-ci nécessitent une période d’apprentissage avec un trafic réseau réel pouvant aller jusqu’à 30 jours.

## <a name="lab-setup"></a>Configuration du laboratoire

Le premier tutoriel de cette série en quatre parties explique comment créer un labo permettant de tester les détections discrètes de [!INCLUDE [Product short](includes/product-short.md)]. Le tutoriel inclut des informations sur les ordinateurs, les utilisateurs et les outils nécessaires pour configurer le labo et terminer ses playbooks. Les instructions supposent que vous connaissez bien la configuration d’un contrôleur de domaine et les stations de travail pour une utilisation de labo, ainsi que d’autres tâches administratives. Plus votre labo sera proche de la configuration suggérée, plus les procédures de test [!INCLUDE [Product short](includes/product-short.md)] seront faciles à suivre. Une fois que vous l’aurez configuré, utilisez les playbooks des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] pour les tests.

> [!div class="nextstepaction"]
> [Configurer un labo d’alertes de sécurité ATP](playbook-setup-lab.md)

## <a name="reconnaissance-playbook"></a>Playbook de reconnaissance

Le deuxième tutoriel de cette série en quatre parties est un playbook de reconnaissance. Les activités de reconnaissance permettent aux attaquants d’acquérir une compréhension approfondie et d’effectuer le mappage complet de votre environnement pour une utilisation ultérieure. Le playbook présente certaines des fonctionnalités de [!INCLUDE [Product short](includes/product-short.md)] concernant l’identification et la détection des activités suspectes liées à des attaques potentielles à l’aide d’exemples tirés d’outils de piratage et d’attaque courants et accessibles au public.

> [!div class="nextstepaction"]
> [Playbook de reconnaissance](playbook-reconnaissance.md)

## <a name="lateral-movement-playbook"></a>Playbook de mouvement latéral

Le playbook de mouvement latéral est le troisième de la série de tutoriels en quatre parties. Les mouvements latéraux sont effectués par un attaquant qui tente de prendre le contrôle du domaine. Lors de l’exécution de ce playbook, vous verrez les services de détection de menaces de type chemin de mouvement latéral et d’alertes de sécurité de [!INCLUDE [Product short](includes/product-short.md)] en simulant des mouvements latéraux dans votre labo.  

> [!div class="nextstepaction"]
> [Playbook de mouvement latéral](playbook-lateral-movement.md)

## <a name="domain-dominance-playbook"></a>Playbook de contrôle du domaine

Le dernier tutoriel de la série en quatre parties est le playbook de contrôle du domaine. Pendant la phase de contrôle du domaine, un attaquant a déjà obtenu des informations d’identification légitimes pour accéder à votre contrôleur de domaine et tente d’obtenir le contrôle persistant du domaine. Vous allez simuler des techniques courantes de contrôle de domaine pour voir les services de détection des menaces de ce type et d’alertes de sécurité de [!INCLUDE [Product short](includes/product-short.md)].

> [!div class="nextstepaction"]
> [Playbook de contrôle du domaine](playbook-domain-dominance.md)


## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter de [!INCLUDE [Product short](includes/product-short.md)] et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté [!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) !
