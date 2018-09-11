---
title: Examen des attaques par chemins de mouvement latéral avec Azure ATP | Microsoft Docs
description: Cet article décrit comment détecter des attaques par chemins de mouvement latéral avec Azure - Protection avancée contre les menaces (ATP).
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/05/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 270b84c24ef8b52565ee97c2c15374645eb54a2c
ms.sourcegitcommit: 93a133430ac85d6db7afad5f6f2583b3a39c423a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/02/2018
ms.locfileid: "43469649"
---
*S’applique à : Azure Advanced Threat Protection*

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>Examen des chemins de mouvement latéral avec Azure ATP


Il est question de mouvement latéral quand un attaquant utilise des comptes non sensibles pour accéder à des comptes sensibles. Les méthodes utilisées sont décrites dans le [Guide des activités suspectes](suspicious-activity-guide.md). Les attaquants se servent du mouvement latéral pour identifier et obtenir l’accès à des ordinateurs et des comptes sensibles sur un réseau à l’aide de comptes non sensibles qui partagent des informations d’identification stockées dans des comptes, des groupes et des ordinateurs. Ils peuvent alors exploiter également les données sur les contrôleurs de domaine.


## <a name="discover-your-at-risk-sensitive-accounts"></a>Découvrir vos comptes sensibles à risque

Pour détecter les comptes sensibles du réseau qui sont vulnérables en raison de leur connexion à des comptes, des groupes ou des ordinateurs non sensibles, suivez ces étapes. 

1. Dans le menu du portail de l’espace de travail Azure ATP, cliquez sur l’icône Rapports ![Icône Rapports](./media/atp-report-icon.png).

2. Sous **Chemins d’accès par mouvement latéral à des comptes sensibles**, le rapport est grisé en l’absence de chemins potentiels de mouvement latéral. S’il en existe, il présélectionne automatiquement la première date présentant des données pertinentes. Il contient des données couvrant au maximum les 60 derniers jours.

 ![rapports](./media/reports.png)

3. Cliquez sur **Télécharger**.

4. Un fichier Excel est créé. Il donne des détails sur les chemins potentiels de mouvement latéral et sur l’exposition des comptes sensibles aux dates sélectionnées. L’onglet **Résumé** présente des graphiques qui décrivent en détail le nombre d’ordinateurs et de comptes sensibles, ainsi que les moyennes pour l’accès à risque. L’onglet **Détails** indique la liste des comptes sensibles à examiner. Il faut savoir que les chemins d’accès détaillés dans le rapport téléchargeable ne seront pas forcément disponibles, car ils ont été détectés au cours des 60 derniers jours et ont pu faire l’objet d’une modification.


## <a name="investigate"></a>Étudier



1. Sur le portail de l’espace de travail Azure ATP, recherchez le badge de mouvement latéral ajouté au profil de l’entité quand celle-ci se trouve sur un chemin de mouvement latéral ![icône de mouvement latéral](./media/lateral-movement-icon.png) ou ![icône de chemin d’accès](./media/paths-icon.png). Remarque : Les badges ne s’affichent que s’il s’est produit un mouvement latéral au cours des dernières 48 heures. 

2. Dans la page de profil utilisateur qui s’ouvre, cliquez sur l’onglet **Chemins d’accès de mouvement latéral**. 

3. Le graphique qui s’affiche établit la carte des chemins possibles vers l’utilisateur sensible. Il indique les connexions possibles observées au cours des dernières 48 heures. Si aucune activité n’a été détectée sur cette période, il n’apparaîtra pas. 

4. Examinez le graphe pour voir si vous pouvez en savoir plus sur l’exposition aux risques des informations d’identification de l’utilisateur sensible. Par exemple, sur cette carte, vous pouvez suivre les flèches grises **Connecté par** pour voir où Samira s’est connectée avec ses informations d’identification privilégiées. Dans ce cas, ses identifiants ont été enregistrés sur l’ordinateur REDMOND-WA-DEV. Identifiez maintenant, parmi les autres utilisateurs connectés à des ordinateurs, lesquels ont généré le plus de risques et de vulnérabilité. Pour ce faire, examinez les flèches noires **Administrateur de** afin de savoir qui possède des privilèges d’administrateur sur la ressource. Dans cet exemple, chaque membre du groupe Contoso All a la possibilité d’accéder aux informations d’identification d’utilisateur à partir de cette ressource.  

 ![chemins de mouvement latéral du profil utilisateur](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Bonnes pratiques de prévention

- La meilleure façon d’empêcher un mouvement latéral consiste à vérifier que les utilisateurs sensibles utilisent leurs informations d’identification d’administrateur uniquement lors de la connexion aux ordinateurs sécurisés de manière renforcée. Dans l’exemple, faites en sorte que, si l’administratrice Samira souhaite accéder à REDMOND-WA-DEV, elle se connecte avec un nom d’utilisateur et un mot de passe différents de ses informations d’identification d’administration.

- Il est également recommandé de vérifier que personne ne dispose d’autorisations d’administration inutiles. Dans l’exemple, vérifiez que tous les membres du groupe Contoso All ont réellement besoin des droits d’administrateur sur REDMOND-WA-DEV.

- Veillez à ce que les utilisateurs n’aient accès qu’aux ressources nécessaires. Dans l’exemple, Oscar Posada augmente considérablement les risques de Samira. Est-il nécessaire que cet utilisateur fasse partie du groupe **Contoso All** ? Serait-il possible de créer des sous-groupes pour minimiser l’exposition ?

**Conseil** : Lorsque aucune activité n’est détectée au cours des dernières 48 heures et que le graphique n’est pas disponible, le rapport de chemin d’accès par mouvement latéral reste accessible ; il fournit des informations sur les chemins potentiels de mouvement latéral détectés au cours des 60 derniers jours. 

**Conseil** : Pour obtenir des instructions sur la configuration des clients et des serveurs à appliquer pour permettre à Azure ATP d’effectuer les opérations SAM-R nécessaires à la détection des chemins de mouvement latéral, voir [Configurer SAM-R](install-atp-step8-samr.md).


## <a name="see-also"></a>Voir aussi

- [Configurer les autorisations requises SAM-R](install-atp-step8-samr.md)
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)