---
title: Examiner les attaques par chemin de mouvement latéral avec ATA
description: Cet article décrit comment détecter des attaques par chemins de mouvement latéral avec Advanced Threat Analytics (ATA).
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 06/14/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4c937a99da6bd26d58fc112eb1c154b59d8d53a1
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79412038"
---
# <a name="investigate-lateral-movement-paths-with-ata"></a>Examiner les chemins de mouvement latéral avec ATA


*S’applique à : Advanced Threat Analytics version 1.9*

Même si vous faites de votre mieux pour protéger vos utilisateurs sensibles, que les administrateurs ont des mots de passe complexes qu’ils changent fréquemment, que leurs ordinateurs sont renforcés et que le stockage de leurs données est sécurisé, des attaquants peuvent malgré tout utiliser des chemins de mouvement latéral pour accéder aux comptes sensibles. Dans les attaques de mouvement latéral, l’attaquant tire parti des instances lorsque des utilisateurs sensibles se connectent à un ordinateur où un utilisateur non sensible a des droits locaux. Les attaquants peuvent ensuite se déplacer latéralement, accéder à l’utilisateur moins sensible, puis se déplacer au sein de l’ordinateur pour se procurer les informations d’identification de l’utilisateur sensible. 

## <a name="what-is-a-lateral-movement-path"></a>Qu’est-ce qu’un chemin de mouvement latéral ?

Il est question de mouvement latéral quand un attaquant utilise des comptes non sensibles pour accéder à des comptes sensibles. Les méthodes utilisées sont décrites dans le [Guide des activités suspectes](suspicious-activity-guide.md). Les attaquants utilisent un mouvement latéral pour identifier les administrateurs de votre réseau et découvrir les ordinateurs auxquels ils peuvent accéder. Avec ces informations et se déplace encore plus loin, l’attaquant peut tirer parti des données de vos contrôleurs de domaine. 

ATA vous permet de prendre des mesures préventives sur votre réseau pour empêcher les attaquants de réussir un mouvement latéral.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Détection de vos comptes sensibles à risque

Pour découvrir les comptes sensibles de votre réseau qui sont vulnérables en raison de leur connexion à des comptes ou des ressources non sensibles, dans un laps de temps spécifique, procédez comme suit : 

1. Dans le menu de la console ATA, cliquez sur l’icône Rapports ![Icône Rapports](./media/ata-report-icon.png).

2. Sous les **chemins de mouvements latéraux vers les comptes sensibles**, si aucun chemin de mouvement latéral n’est trouvé, le rapport est grisé. S’il y a des chemins de mouvement latéral, les dates du rapport sélectionnent automatiquement la première date quand il y a des données pertinentes. 

   ![rapports](./media/reports.png)

3. Cliquez sur **Télécharger**.

4. Le fichier Excel créé vous fournit des détails sur vos comptes sensibles menacés. L’onglet **Résumé** propose des graphes qui décrivent en détail le nombre de comptes sensibles, les ordinateurs et les moyennes pour les ressources à risque. L’onglet **Détails** présente une liste des comptes sensibles dont vous devez vous soucier. Notez que les chemins sont des chemins qui existaient auparavant et qui peuvent ne pas être disponibles aujourd’hui.


## <a name="investigate"></a>Étudier

Maintenant que vous avez identifié les comptes sensibles qui présentent des risques, vous pouvez vous plonger dans ATA pour en savoir plus et prendre des mesures préventives.

1. Dans la console ATA, recherchez le badge Mouvement latéral qui est ajouté au profil de l’entité quand celle-ci se trouve sur un chemin de mouvement latéral. ![icône de mouvement latéral](./media/lateral-movement-icon.png) or ![icône de chemin d’accès](./media/paths-icon.png). Cette opération est possible si un chemin de mouvement latéral a existé au cours des deux derniers jours.

2. Dans la page de profil utilisateur qui s’ouvre, cliquez sur l’onglet **Chemins d’accès de mouvement latéral**.

3. Le graphique qui s’affiche établit la carte des chemins possibles vers l’utilisateur sensible. Le graphe montre les connexions qui ont été établies au cours des deux derniers jours.

4. Examinez le graphe pour voir si vous pouvez en savoir plus sur l’exposition aux risques des informations d’identification de l’utilisateur sensible. Par exemple, dans ce mappage, vous pouvez suivre les flèches de **connexion à par** des flèches grises pour voir où samira s’est connecté à l’aide de leurs informations d’identification privilégiées. Dans ce cas, les informations d’identification sensibles de Samira ont été enregistrées sur l’ordinateur REDMOND-WA-DEV. Vérifiez ensuite quels sont les autres utilisateurs connectés à quels ordinateurs ayant créé le plus d’exposition et de vulnérabilité. Pour ce faire, examinez les flèches noires **Administrateur de** afin de savoir qui possède des privilèges d’administrateur sur la ressource. Dans cet exemple, chaque membre du groupe **Contoso All** a la possibilité d’accéder aux informations d’identification des utilisateurs à partir de cette ressource.  

   ![Chemins de mouvement latéral du profil utilisateur](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Bonnes pratiques de prévention

- La meilleure façon d’empêcher un mouvement latéral consiste à s’assurer que les utilisateurs sensibles utilisent leurs informations d’identification d’administrateur uniquement lorsqu’ils se connectent à des ordinateurs sécurisés où aucun utilisateur non sensible ne dispose de droits d’administrateur sur le même ordinateur. Dans l’exemple, assurez-vous que si samira a besoin d’accéder à REDMOND-WA-DEV, il se connecte avec un nom d’utilisateur et un mot de passe autres que leurs informations d’identification d’administrateur, ou il supprime le groupe contoso All du groupe Administrateurs local sur REDMOND-WA-DEV.

- Il est également recommandé de vérifier que personne ne dispose d’autorisations d’administration locales inutiles. Dans l’exemple, vérifiez si tous les membres de contoso ont vraiment besoin de droits d’administrateur sur REDMOND-WA-DEV.

- Veillez à ce que les utilisateurs n’aient accès qu’aux ressources nécessaires. Dans l’exemple, Oscar Posada augmente considérablement les risques de Samira. Est-il nécessaire qu’elles soient incluses dans le groupe **contoso All**? Avez-vous la possibilité de créer des sous-groupes pour minimiser les risques ?

> [!TIP]
> Si l’activité n’est pas détectée au cours des deux derniers jours, le graphique n’apparaît pas, mais le rapport chemin de mouvement latéral est toujours disponible pour fournir des informations sur les chemins de mouvement latéral au cours des 60 derniers jours.

> [!TIP]
> Pour obtenir des instructions sur la façon de configurer vos serveurs de façon à autoriser ATA à exécuter les opérations SAM-R nécessaires à la détection de chemin de mouvement latéral, [configurez Sam-r](install-ata-step9-samr.md).




## <a name="see-also"></a>Voir aussi
- [Travailler avec des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
