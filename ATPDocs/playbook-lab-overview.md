---
title: Azure ATP vue d’ensemble du didacticiel Lab d’alerte de sécurité
description: Cette vue d’ensemble du tutoriel décrit les quatre parties du labo d’alertes de sécurité Azure ATP pour la simulation de menaces à détecter par Azure ATP.
ms.service: azure-advanced-threat-protection
ms.topic: how-to
author: shsagir
ms.author: shsagir
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: 52c20174b431da000ecba922462d0c6af112b005
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828294"
---
# <a name="tutorial-overview-atp-security-alert-lab"></a>Vue d’ensemble du didacticiel : laboratoire d’alerte de sécurité ATP

L’objectif du tutoriel sur le labo d’alerte de sécurité Azure ATP est d’illustrer les capacités d’**Azure ATP** à identifier et à détecter des activités suspectes et des attaques potentielles contre votre réseau. Ce tutoriel en quatre parties explique comment installer et configurer un environnement de travail pour tester des détections *discrètes* d’Azure ATP. Ce labo se concentre sur les fonctionnalités d’Azure ATP basées sur la *signature*. Ce labo n’inclut ni le Machine Learning avancé, ni les détections de comportements basées sur utilisateur ou l’entité, car celles-ci nécessitent une période d’apprentissage avec un trafic réseau réel pouvant aller jusqu’à 30 jours.

## <a name="lab-setup"></a>Configuration du laboratoire

Le premier tutoriel de cette série en quatre parties vous explique comment créer un labo de tests de détections discrètes d’Azure ATP. Le tutoriel inclut des informations sur les ordinateurs, les utilisateurs et les outils nécessaires pour configurer le labo et terminer ses playbooks. Les instructions supposent que vous connaissez bien la configuration d’un contrôleur de domaine et les stations de travail pour une utilisation de labo, ainsi que d’autres tâches administratives. Plus votre labo sera proche de la configuration suggérée, plus les procédures de test Azure ATP seront faciles à suivre. Une fois que votre laboratoire est installé, utilisez les playbooks des alertes de sécurité Azure ATP pour le test.

> [!div class="nextstepaction"]
> [Configurer un labo d’alertes de sécurité ATP](playbook-setup-lab.md)

## <a name="reconnaissance-playbook"></a>Playbook de reconnaissance

Le deuxième tutoriel de cette série en quatre parties est un playbook de reconnaissance. Les activités de reconnaissance permettent aux attaquants d’acquérir une compréhension approfondie et d’effectuer le mappage complet de votre environnement pour une utilisation ultérieure. Le playbook présente certaines des capacités d’Azure ATP à identifier et à détecter les activités suspectes liées à des attaques potentielles à l’aide d’exemples tirés d’outils de piratage et d’attaque courants accessibles au public.

> [!div class="nextstepaction"]
> [Playbook de reconnaissance](playbook-reconnaissance.md)


## <a name="lateral-movement-playbook"></a>Playbook de mouvement latéral

Le playbook de mouvement latéral est le troisième de la série de tutoriels en quatre parties. Les mouvements latéraux sont effectués par un attaquant qui tente de prendre le contrôle du domaine. Lors de l’exécution de ce playbook, vous verrez la détection des menaces liées aux mouvements latéraux et les services d’alertes de sécurité d’Azure ATP suite aux mouvements latéraux simulés dans votre labo.  

> [!div class="nextstepaction"]
> [Playbook de mouvement latéral](playbook-lateral-movement.md)

## <a name="domain-dominance-playbook"></a>Playbook de contrôle du domaine

Le dernier tutoriel de la série en quatre parties est le playbook de contrôle du domaine. Pendant la phase de contrôle du domaine, un attaquant a déjà obtenu des informations d’identification légitimes pour accéder à votre contrôleur de domaine et tente d’obtenir le contrôle persistant du domaine. Vous allez simuler des méthodes de contrôle du domaine courantes pour voir la détection des menaces axée sur le contrôle du domaine et les services d’alertes de sécurité d’Azure ATP.

> [!div class="nextstepaction"]
> [Playbook de contrôle du domaine](playbook-domain-dominance.md)


## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) dès aujourd’hui !