---
title: Examen des chemins de mouvement latéral avec Azure ATP | Microsoft Docs
description: Cet article décrit comment détecter et examiner les attaques par chemins de mouvement latéral avec Azure Advanced Threat Protection.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/3/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9295dc09-ecdb-44c0-906b-cba4c5c8f17c
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e11362c25d0d61925101db2f3f7f896f233931ca
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196749"
---
# <a name="tutorial-use-lateral-movement-paths-lmps"></a>Tutoriel : Utiliser des chemins de mouvement latéral

Les attaques par mouvements latéraux sont généralement effectuées selon différentes techniques. Certaines des méthodes les plus répandues utilisées par les attaquants sont les attaques par [vol d’informations d’identification](suspicious-activity-guide.md#) et par [Pass-the-Ticket](suspicious-activity-guide.md). Dans les deux méthodes, des comptes non sensibles sont utilisés pour des mouvements latéraux par les attaquants, qui exploitent des ordinateurs non sensibles partageant avec des comptes sensibles des informations d’identification stockées dans des comptes, des groupes et des ordinateurs.

Dans ce tutoriel, vous allez apprendre à utiliser les chemins de mouvement latéral d’Azure ATP pour [examiner](#investigate) les chemins de mouvement latéral potentiels et, en combinaison avec les alertes de sécurité d’Azure ATP, pour obtenir une meilleure compréhension de ce qui s’est passé dans votre réseau et de quelle manière. Vous allez également apprendre à utiliser le [rapport des chemins de mouvement latéral pour les comptes sensibles](#discover-your-at-risk-sensitive-accounts) pour découvrir tous les comptes sensibles avec des chemins de mouvement latéral potentiels détectés dans votre réseau sur une période de temps donnée.

> [!div class="checklist"]
> * Examiner les chemins de mouvement latéral
> * Découvrir vos comptes sensibles à risque
> * Accéder au rapport **Chemins d’accès de mouvement latéral pour les comptes sensibles**


## <a name="investigate"></a>Étudier

Il existe plusieurs façons d’utiliser et d’investiguer les chemins de mouvement latéral. Dans le portail Azure ATP, effectuez une recherche par entité, puis explorez par chemin ou par activité.

1. Dans le portail, recherchez un utilisateur ou un ordinateur. Regardez si un badge de mouvement latéral a été ajouté à un profil d’entité. Les badges apparaissent seulement quand une entité est détectée dans un chemin de mouvement latéral potentiel au cours des dernières 48 heures.  

   ![icône de mouvement latéral](./media/lateral-movement-icon.png) ou ![icône de chemin d’accès](./media/paths-icon.png).

2. Dans la page de profil utilisateur qui s’ouvre, cliquez sur l’onglet **Chemins d’accès de mouvement latéral**.

   ![Onglet Chemin de mouvement latéral d’Azure ATP](./media/lateral-movement-path-tab.png)

3. Le graphe qui s’affiche montre une carte des chemins possibles vers l’utilisateur sensible au cours des dernières 48 heures. Si aucune activité n’a été détectée sur cette période, il n’apparaîtra pas. Utilisez l’option **Afficher une autre date** pour afficher le graphe avec les détections antérieures de chemin de mouvement latéral pour l’entité.

   ![Chemin de mouvement latéral - Afficher une autre date](./media/atp-view-different-date.png)

4. Examinez le graphe pour voir si vous pouvez en savoir plus sur l’exposition aux risques des informations d’identification de l’utilisateur sensible. Par exemple, dans le chemin, suivez les flèches grises **Connecté par** pour voir où Nick s’est connecté avec ses informations d’identification privilégiées. Dans ce cas, ses informations d'identification ont été enregistrées sur l’ordinateur SHAREPOINT-SRV. Identifiez maintenant, parmi les autres utilisateurs connectés à des ordinateurs, lesquels ont généré le plus de risques et de vulnérabilité. Pour ce faire, examinez les flèches noires **Administrateur de** afin de savoir qui possède des privilèges d’administrateur sur la ressource. Dans cet exemple, chaque membre du groupe HelpDesk a la possibilité d’accéder aux informations d’identification des utilisateurs à partir de cette ressource.  

   ![Chemin de mouvement latéral d’Azure ATP](./media/atp-lmp.png)

## <a name="discover-your-at-risk-sensitive-accounts"></a>Découvrir vos comptes sensibles à risque

Pour détecter tous les comptes sensibles de votre réseau qui sont exposés en raison de leur connexion à des comptes, des groupes ou des ordinateurs non sensibles dans des chemins de mouvement latéral, suivez ces étapes. 

1. Dans le menu du portail Azure ATP, cliquez sur l’icône Rapports. ![Icône Rapports](./media/atp-report-icon.png).

2. Sous **Chemins d’accès par mouvement latéral à des comptes sensibles**, le rapport est grisé en l’absence de chemins potentiels de mouvement latéral. S’il en existe, il présélectionne automatiquement la première date présentant des données pertinentes. Il contient des données couvrant au maximum les 60 derniers jours.

   ![rapports](./media/reports.png)

3. Cliquez sur **Télécharger**.

4. Un fichier Excel est créé. Il donne des détails sur les chemins potentiels de mouvement latéral et sur l’exposition des comptes sensibles aux dates sélectionnées. L’onglet **Résumé** présente des graphiques qui décrivent en détail le nombre d’ordinateurs et de comptes sensibles, ainsi que les moyennes pour l’accès à risque. L’onglet **Détails** indique la liste des comptes sensibles à examiner.

## <a name="schedule-report"></a>Planifier un rapport

Le rapport des mouvements latéraux vers les comptes sensibles peut également être planifié avec la fonctionnalité de définition de rapports planifiés.

Notez que les chemins de mouvement latéral détaillés dans le rapport téléchargeable peuvent ne plus être disponibles, car ils ont été détectés antérieurement et avoir été changés, modifiés ou corrigés depuis leur détection.

Pour passer en revue l’historique des chemins de mouvement latéral, sélectionnez d’autres dates disponibles dans la sélection du calendrier lors de la création d’un rapport.

## <a name="next-steps"></a>Étapes suivantes

Dans ce tutoriel, vous avez appris à utiliser des chemins de mouvement latéral pour examiner des activités suspectes. Pour en savoir plus sur les entités impliquées dans les chemins de mouvement latéral, passez au tutoriel sur l’examen des entités.
> [!div class="nextstepaction"]
> [Examiner les entités](investigate-entity.md)

## <a name="see-also"></a>Voir aussi

- [Présentation des chemins de mouvement latéral d’Azure ATP](use-case-lateral-movement-path.md)
- [Configurer Azure ATP pour effectuer des appels distants vers SAM](install-atp-step8-samr.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
