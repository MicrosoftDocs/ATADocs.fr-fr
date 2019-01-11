---
title: Utilisation des alertes de sécurité dans Azure Advanced Threat Protection | Microsoft Docs
description: Explique comment examiner les alertes de sécurité émises par Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/1/2019
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8ff32e742dc1ff1ce48077206b78d4badd10f74e
ms.sourcegitcommit: 1ba4e327784c6267db5a708592c4d81ca23376ba
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53996823"
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="working-with-security-alerts"></a>Utilisation des alertes de sécurité

Cet article explique les bases de l’utilisation des alertes de sécurité d’Azure ATP.

## Passer en revue les alertes de sécurité dans la chronologie des attaques <a name="review-suspicious-activities-on-the-attack-time-line"></a>

Une fois connecté au portail Azure ATP, vous êtes automatiquement dirigé vers la **chronologie des alertes de sécurité** ouverte. Les alertes de sécurité sont listées par ordre chronologique, les plus récentes figurant en haut de la liste.

Une alerte de sécurité comprend les informations suivantes :

- Les entités impliquées, y compris les utilisateurs, les ordinateurs, les serveurs, les contrôleurs de domaine et les ressources

- L’heure et le délai d’exécution des activités suspectes ayant déclenché une alerte de sécurité.

- Gravité de l’alerte : Haute, Moyenne ou Faible.

- État : Ouvert, fermé ou supprimé.

- Possibilité de :

    - Transmettre l’alerte de sécurité par e-mail à d’autres membres de votre entreprise.

    - Télécharger l’alerte de sécurité au format Excel.

> [!NOTE]
> - Quand vous pointez votre souris sur un utilisateur ou un ordinateur, un mini-profil d’entité s’affiche avec des informations complémentaires sur l’entité, notamment le nombre d’alertes de sécurité auxquelles est liée l’entité.
> - Quand vous cliquez sur une entité, vous êtes dirigé vers le profil d’entité de l’utilisateur ou l’ordinateur.

![Image de la chronologie des alertes de sécurité Azure ATP](media/atp-sa-timeline.png)

## <a name="security-alert-categories"></a>Catégories des alertes de sécurité

Les alertes de sécurité d’Azure ATP sont divisées en catégories ou phases (voir ci-dessous), comme les phases d’une chaîne de destruction de cyberattaque standard. 

- Alertes de reconnaissance
- Alertes indiquant des informations d’identification compromises
- Alertes de mouvement latéral
- Alertes de dominance du domaine
- Alertes d’exfiltration

## Détections en préversion <a name="preview-detections"></a>

L’équipe de recherche Azure ATP travaille sans relâche à l’implémentation de nouvelles détections pour les attaques récemment découvertes. Dans la mesure où Azure ATP est un service cloud, de nouvelles détections sont publiées rapidement pour permettre aux clients Azure ATP d’en bénéficier dès que possible.

Ces détections sont marquées d’un badge de préversion pour vous permettre d’identifier les nouvelles détections et les nouveautés du produit. Si vous désactivez les détections en préversion, vous ne les verrez pas dans la console Azure ATP (ni dans la chronologie ni dans les profils d’entité). Les nouvelles alertes ne seront pas non plus ouvertes.

![détection vpn en préversion](./media/preview-detection-vpn.png)

Par défaut, les détections en préversion sont activées dans Azure ATP. 

Pour désactiver les détections en préversion :

1. Dans la console Azure ATP, cliquez sur la roue dentée des paramètres.
2. Dans le menu de gauche, sous Préversion, cliquez sur **Détections**.
3. Utilisez le curseur pour activer et désactiver les détections en préversion.
 
![détections en préversion](./media/preview-detections.png) 


## <a name="filter-security-alerts-list"></a>Filtrer la liste des alertes de sécurité
Pour filtrer la liste des alertes de sécurité :

1. Dans le volet **Filtrer par** sur le côté gauche de l’écran, sélectionnez l’une des options suivantes : **Tout**, **Ouvert**, **Fermé** ou **Ignoré**.

2. Pour filtrer la liste, sélectionnez **Haute**, **Moyenne** ou **Faible**.

**Gravité des activités suspectes**

- **Faible**

    Correspond aux activités pouvant conduire à des attaques durant lesquelles des utilisateurs ou des logiciels malveillants accèdent aux données d’une entreprise.

- **Moyenne**

    Correspond aux activités qui peuvent faire courir un risque à certaines identités en permettant des attaques plus graves qui pourraient entraîner une usurpation d’identité ou une élévation des privilèges.

- **Importante**

    Correspond aux activités pouvant conduire à une usurpation d’identité, une élévation des privilèges ou d’autres attaques à impact élevé.


## <a name="managing-security-alerts"></a>Gestion des alertes de sécurité

Vous pouvez changer l’état d’une alerte de sécurité en cliquant sur son état actuel, puis en sélectionnant l’une des options suivantes : **Ouvertes**, **Ignorées**, **Fermées** ou **Supprimées**.
Pour cela, cliquez sur les trois points en haut à droite d’une alerte pour afficher la liste des actions disponibles.

![Actions Azure ATP pour les alertes de sécurité](./media/atp-sa-actions.png)

**États des alertes de sécurité**

- **Ouvert** : toutes les nouvelles alertes de sécurité s’affichent dans la liste.

- **Fermé** : utilisé pour effectuer le suivi des activités que vous avez identifiées, examinées et résolues.

    > [!NOTE]
    > Si une activité est détectée à nouveau après une courte période, Azure ATP peut rouvrir une alerte ayant été fermée.

- **Ignoré** : permet d’ignorer temporairement une alerte, et de n’être averti de nouveau qu’en cas de nouvelle instance. Cela signifie que si une alerte similaire survient, Azure ATP ne la rouvre pas. Cependant, si l’alerte cesse pendant sept jours puis réapparaît, vous êtes averti à nouveau.

- **Supprimer** : Si vous supprimez une alerte, elle est supprimée du système et de la base de données, et vous NE pourrez PAS la restaurer. Si vous cliquez sur Supprimer, vous supprimez toutes les alertes de sécurité du même type.

- **Exclure** : Possibilité d’empêcher une entité de déclencher un certain type d’alertes. Par exemple, vous pouvez configurer Azure ATP pour empêcher une entité (un utilisateur ou un ordinateur) de déclencher à nouveau une alerte pour un certain type d’activité, par exemple un administrateur qui exécute du code à distance ou un scanner de sécurité qui effectue une reconnaissance DNS. En plus d’ajouter des exclusions directement dans l’alerte de sécurité lorsque celle-ci est détectée dans la chronologie, vous pouvez également accéder aux **Exclusions** de la page Configuration et, pour chaque alerte de sécurité, ajouter et supprimer manuellement des entités ou des sous-réseaux exclus (par exemple, pour les attaques pass-the-ticket).

> [!NOTE]
> Les pages de configuration peuvent être modifiées seulement par des administrateurs Azure ATP.


## <a name="see-also"></a>Voir aussi

- [Utilisation du portail Azure ATP](workspace-portal.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)