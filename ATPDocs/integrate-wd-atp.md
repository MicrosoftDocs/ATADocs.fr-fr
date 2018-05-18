---
title: Intégration d’Azure - Protection avancée contre les menaces et de Windows Defender ATP | Microsoft Docs
description: Guide pratique pour intégrer Azure - Protection avancée contre les menaces et Windows Defender ATP afin de bénéficier d’une couverture complète de la détection des menaces
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/16/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 17ade33a55039eaf8abc98901cdab9ebeef850c5
ms.sourcegitcommit: 714a01edc9006b38d1163d03852dafc2a5fddb5f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2018
---
*S’applique à : Azure - Protection avancée contre les menaces*

# <a name="integrating-azure-atp-with-windows-defender-atp"></a>Intégration d’Azure ATP et de Windows Defender ATP

Azure - Protection avancée contre les menaces vous permet d’intégrer Azure ATP et Windows Defender ATP pour obtenir une solution encore plus complète de protection contre les menaces. Azure ATP surveille le trafic sur vos contrôleurs de domaine alors que Windows Defender ATP surveille vos points de terminaison, offrant ainsi ensemble une interface unique pour protéger votre environnement.

> [!NOTE]
> L’intégration est actuellement activée uniquement si vous êtes client de la préversion limitée de Windows Defender ATP.
 
En intégrant Windows Defender ATP et Azure ATP, vous pouvez tirer parti de toute la puissance des deux services et sécuriser votre environnement, notamment :

- Les capteurs Azure ATP et les capteurs autonomes : Peuvent être installés directement sur vos contrôleurs de domaine ou mettre en miroir les ports de vos contrôleurs de domaine, pour capturer et analyser le trafic réseau de plusieurs protocoles (tels que Kerberos, DNS, RPC, NTLM, etc.) à des fins d’authentification, d’autorisation et de collecte d’informations. 

-   Les capteurs comportementaux de point de terminaison : Intégrés dans Windows 10, ces capteurs collectent et traitent les signaux comportementaux du système d’exploitation (par exemple, les processus, le Registre, les fichiers et les communications réseau) et envoient ces données de capteurs à votre instance cloud, privée et isolée de Windows Defender ATP.

- L’analytique de la sécurité cloud : Tirant parti du Big Data, de l’apprentissage automatique, de la vision unique de Microsoft sur l’écosystème Windows (tel que l’[outil de suppression de logiciels malveillants Microsoft](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), des produits cloud d’entreprise (tels qu’Office 365) et des ressources en ligne (telles que la réputation des URL SmartScreen et Bing), les signaux comportementaux sont convertis en insights, détections et réponses recommandées aux menaces avancées.

- Les renseignements sur les menaces : Générés par les chasseurs et les équipes de sécurité de Microsoft, et complétés par les renseignements fournis par les partenaires, les renseignements sur les menaces permettent à Windows Defender ATP d’identifier les procédures, les techniques et les outils utilisés par les attaquants, ainsi que de générer des alertes quand ces éléments sont observés dans les données collectées par les capteurs.

La technologie Azure ATP détecte des activités suspectes multiples en se focalisant sur plusieurs phases de la chaîne de cyberattaque, notamment :

- Reconnaissance, au cours de laquelle les personnes malveillantes vont recueillir des informations sur la façon dont l’environnement est construit, sur les différents assets, et sur les entités qui existent. Elles élaborent généralement leur plan pour les prochaines phases de l’attaque.

- Cycle de mouvement latéral, pendant lequel un attaquant investit temps et efforts dans la l'élargissement de sa surface d’attaque au sein de votre réseau.

- Dominance (persistance) de domaine, pendant laquelle un attaquant capture les informations lui permettant de reprendre sa campagne à l’aide de différents ensembles de points d’entrée, d’informations d’identification et de techniques.

Au même moment, Windows Defender ATP tire parti de la technologie et de l’expertise de Microsoft pour détecter les cyber-attaques sophistiquées, en fournissant :

- Détection d’attaques avancées, basée sur le cloud et les comportements<br></br>Détecte des attaques ayant traversé toutes les autres défenses (détection après violation), fournit des alertes corrélées activables pour des adversaires connus et inconnus qui tentent de dissimuler leurs activités sur les points de terminaison.

- Chronologie détaillée pour une enquête approfondie et l’atténuation des risques<br></br>Recherchez facilement des comportements suspects ou la portée d’une violation sur n’importe quel ordinateur dans une riche chronologie informatique. Inventaire des fichiers, URL et connexions réseau sur le réseau. Obtenez des informations supplémentaires grâce à la collection et à l’analyse approfondies (« détonation ») pour tous les fichiers et URL.

- Base de connaissances de renseignements sur les menaces, unique et intégrée<br></br>La perception inégalée des menaces fournit des détails sur les acteurs et le contexte intentionnel pour chaque détection basée sur les renseignements sur les menaces – en associant les sources de renseignement internes et tierces.

## <a name="prerequisites"></a>Prérequis

Pour activer cette fonctionnalité, vous avez besoin d’une licence pour Azure ATP et Windows Defender ATP. 


## <a name="how-to-integrate-azure-atp-with-windows-defender-atp"></a>Comment intégrer Azure ATP et Windows Defender ATP

1. Définissez l’espace de travail que vous souhaitez intégrer en tant que **principal**. Un seul espace de travail peut être l’espace de travail principal, et seul un espace de travail principal peut être intégré à d’autres services. Si, à l’avenir, vous souhaitez que cet espace de travail ne soit plus l’espace de travail principal, vous devez supprimer l’intégration avant de le définir comme secondaire.

 ![espace de travail principal](./media/primary-workspace.png)

2. Cliquez sur **Configuration** et, sous **Sources de données**, sélectionnez **Windows Defender ATP**. Ensuite, cliquez sur le lien vers **Gestion d’espace de travail**. Ce lien est disponible seulement si vous avez une licence Windows Defender ATP et que vous avez déjà effectué le processus d’intégration pour Windows Defender ATP. 

3. Dans votre espace de travail principal, cliquez sur l’icône des paramètres.

 ![intégration de l’espace de travail](./media/edit-workspace.png)
 
3. Définissez l’intégration sur **On**. 

 ![activer l’intégration](./media/enable-integration.png)

4. Dans le [portail Windows Defender ATP](https://beta.securitycenter.windows.com/preferences/advanced), accédez à **Paramètres** et à **Fonctionnalités avancées**, puis définissez **Intégration Azure ATP** sur **ON**. 

 ![Activer l’intégration Windows Defender ATP](./media/wd-atp-enable.png)

5. Pour vérifier le statut de l’intégration, dans le portail d’espace de travail Azure ATP, accédez à **Paramètres** puis à **Intégration Windows Defender ATP**. Vous pouvez voir le statut de l’intégration ; en cas de problème, vous voyez une erreur. Vous pouvez également voir quel espace de travail est intégré à Windows Defender ATP.

## <a name="how-it-works"></a>Fonctionnement

Une fois Azure ATP et Windows Defender ATP pleinement intégrés, dans le portail d’espace de travail Azure ATP, dans la fenêtre contextuelle de mini-profil et dans la page de profil d’entité, chaque entité figurant dans Windows Defender ATP inclut un badge pour montrer qu’elle est intégrée à Windows Defender ATP. 

 ![Alertes Windows Defender ATP](./media/profile-alerts-wd.png)

Si l’entité contient des alertes dans Windows Defender ATP, un nombre à côté du badge indique combien d’alertes ont été générées.

 ![Alertes Azure ATP](./media/atp-integrated-wd-icon-alerts.png)

Si vous cliquez sur le badge, vous êtes dirigé vers le portail Windows Defender ATP où vous pouvez afficher et solutionner les alertes. Si l’entité n’est pas reconnue par Windows Defender ATP, le badge est grisé. 

 ![Windows Defender ATP grisé](./media/wd-grey.png)

Dans le portail Windows Defender ATP, lorsque vous cliquez sur un point de terminaison, vous pouvez visualiser les alertes Azure ATP. Si vous cliquez sur les alertes pour cette entité dans Windows Defender ATP, la page de profil de l’entité s’ouvre dans Azure ATP. 
 
 > ![REMARQUE] Actuellement, l’intégration d’Azure ATP avec Windows Defender ATP prend en charge uniquement les utilisateurs et les machines qui font partie de l’AD local. Les utilisateurs d’Azure AD et les machines virtuelles gérées dans Azure ne sont pas pris en compte dans le cadre de l’intégration 

![Alertes Windows Defender ATP](./media/wd-atp-alerts.png)


## <a name="see-also"></a>Voir aussi

- [Examen des chemins de mouvement latéral avec Azure ATP](use-case-lateral-movement-path.md)
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Architecture Azure ATP](atp-architecture.md)
- [Installer ATP](install-atp-step1.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)

