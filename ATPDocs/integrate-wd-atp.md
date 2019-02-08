---
title: Intégration d’Azure Advanced Threat Protection et de Windows Defender ATP | Microsoft Docs
description: Guide pratique pour intégrer Azure Advanced Threat Protection Windows Defender ATP afin de bénéficier d’une couverture complète de la détection des menaces
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/18/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2ff18759e23462a2b01a10f45729b5a282495347
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54458816"
---
# <a name="integrate-azure-atp-with-windows-defender-atp"></a>Intégrer Azure ATP à Windows Defender ATP

Azure Advanced Threat Protection vous permet d’intégrer Azure ATP et Windows Defender ATP pour obtenir une solution encore plus complète de protection contre les menaces. Azure ATP surveille le trafic sur vos contrôleurs de domaine alors que Windows Defender ATP surveille vos points de terminaison, offrant ainsi ensemble une interface unique pour protéger votre environnement.

En intégrant Windows Defender ATP et Azure ATP, vous pouvez tirer parti de toute la puissance des deux services et sécuriser votre environnement, notamment :

- Capteurs et capteurs autonomes Azure ATP : ils peuvent être installés directement sur vos contrôleurs de domaine ou mettre en miroir les ports de vos contrôleurs de domaine sur ATP, pour capturer et analyser le trafic réseau de plusieurs protocoles (par exemple, Kerberos, DNS, RPC ou NTLM) à des fins d’authentification, d’autorisation et de collecte d’informations. 

-   Capteurs comportementaux de point de terminaison : intégrés à Windows 10, ils collectent et traitent les signaux comportementaux du système d’exploitation (par exemple, les processus, le Registre, les fichiers et les communications réseau) et envoient ces données de capteurs à votre instance cloud, isolée et privée de Windows Defender ATP.

- Analyse de la sécurité cloud : grâce au Big Data, au Machine Learning et à la vision unique de Microsoft sur l’écosystème Windows (par exemple, [l’Outil de suppression de logiciels malveillants Microsoft](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), les produits cloud d’entreprise (par exemple, Office 365) et les ressources en ligne (par exemple, Bing et la réputation d’URL SmartScreen), les signaux comportementaux sont convertis en insights, détections et réponses recommandées aux menaces avancées.

- Veille des menaces : générée par les chasseurs et les équipes de sécurité de Microsoft, et complétée par les renseignements fournis par les partenaires, la veille des menaces permet à Windows Defender ATP d’identifier les procédures, les techniques et les outils utilisés par les attaquants, et de générer des alertes quand ces activités sont observées dans les données collectées par les capteurs.

La technologie Azure ATP détecte des activités suspectes multiples en se focalisant sur plusieurs phases de la chaîne de cyberattaque, notamment :

- Reconnaissance, au cours de laquelle les personnes malveillantes vont recueillir des informations sur la façon dont l’environnement est construit, sur les différents assets, et sur les entités qui existent. Elles élaborent généralement leur plan pour les prochaines phases de l’attaque ici.

- Cycle de mouvement latéral, pendant lequel un attaquant investit temps et efforts dans la l'élargissement de sa surface d’attaque au sein de votre réseau.

- Dominance (persistance) de domaine, pendant laquelle un attaquant capture les informations lui permettant de reprendre sa campagne à l’aide de différents ensembles de points d’entrée, d’informations d’identification et de techniques.

Au même moment, Windows Defender ATP tire parti de la technologie et de l’expertise de Microsoft pour détecter les cyber-attaques sophistiquées, en fournissant :

- Détection d’attaques avancées, basée sur le cloud et les comportements<br></br>Détecte des attaques ayant traversé toutes les autres défenses (détection après violation), fournit des alertes corrélées activables pour des adversaires connus et inconnus qui tentent de dissimuler leurs activités sur les points de terminaison.

- Chronologie détaillée pour une enquête approfondie et l’atténuation des risques<br></br>Recherchez facilement des comportements suspects ou la portée d’une violation sur n’importe quel ordinateur dans une riche chronologie informatique. Inventaire des fichiers, URL et connexions réseau sur le réseau. Obtenez des informations supplémentaires grâce à la collection et à l’analyse approfondies (« détonation ») pour tous les fichiers et URL.

- Base de connaissances de renseignements sur les menaces, unique et intégrée<br></br>La perception inégalée des menaces fournit des détails sur les acteurs et le contexte intentionnel de chaque détection basée sur les renseignements sur les menaces – en associant les sources de renseignement internes et tierces.

## <a name="prerequisites"></a>Prérequis

Pour activer cette fonctionnalité, vous avez besoin d’une licence pour Azure ATP et Windows Defender ATP. 


## <a name="how-to-integrate-azure-atp-with-windows-defender-atp"></a>Comment intégrer Azure ATP et Windows Defender ATP

1. Dans le portail Azure ATP, ouvrez **Configuration**. 

    ![Menu Configuration Azure ATP](./media/atp-configuration-wd.png)
2. Dans la liste des Configurations, sélectionnez **Windows Defender ATP** et définissez l’activation/la désactivation de l’intégration sur **Activé**. 

    ![Activer l’intégration de Windows Defender](./media/enable-integration.png)


3. Dans le [portail Windows Defender ATP](https://securitycenter.windows.com/preferences/advanced), accédez à **Paramètres** et à **Fonctionnalités avancées**, puis définissez **Intégration Azure ATP** sur **ON**. 

    ![Activer l’intégration Windows Defender ATP](./media/wd-atp-enable.png)

4. Pour vérifier l’état de l’intégration, dans le portail Azure ATP, accédez à **Paramètres** > **Intégration avec Windows Defender ATP**. Vous pouvez voir le statut de l’intégration ; en cas de problème, vous verrez une erreur. 

## <a name="how-it-works"></a>Fonctionnement

Une fois Azure ATP et Windows Defender ATP complètement intégrés, dans le portail Azure ATP, dans la fenêtre contextuelle de mini-profil et dans la page de profil d’entité, chaque entité figurant dans Windows Defender ATP inclut un badge pour montrer qu’elle est intégrée à Windows Defender ATP. 

 ![Alertes Windows Defender ATP](./media/profile-alerts-wd.png)

Si l’entité contient des alertes dans Windows Defender ATP, un nombre à côté du badge indique combien d’alertes ont été générées.

 ![Alertes Azure ATP](./media/atp-integrated-wd-icon-alerts.png)

Si vous cliquez sur le badge, vous êtes dirigé vers le portail Windows Defender ATP où vous pouvez afficher et solutionner les alertes. Si l’entité n’est pas reconnue par Windows Defender ATP, le badge est grisé. 

 ![Windows Defender ATP grisé](./media/wd-grey.png)

Dans le portail Windows Defender ATP, cliquez sur un point de terminaison pour voir les alertes Azure ATP. Si vous cliquez sur les alertes pour cette entité dans Windows Defender ATP, la page de profil de l’entité s’ouvre dans Azure ATP. 
 
 > [!NOTE]
 > Actuellement, l’intégration d’Azure ATP à Windows Defender ATP prend en charge seulement les utilisateurs et les machines qui font partie de l’annuaire AD local. Les utilisateurs d’Azure AD et les machines virtuelles gérées dans Azure ne sont pas pris en compte dans le cadre de l’intégration 

![Alertes Windows Defender ATP](./media/wd-atp-alerts.png)


## <a name="see-also"></a>Voir aussi

- [Examen des chemins de mouvement latéral avec Azure ATP](use-case-lateral-movement-path.md)
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Architecture Azure ATP](atp-architecture.md)
- [Installer ATP](install-atp-step1.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)

