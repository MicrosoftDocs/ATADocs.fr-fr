---
title: Utilisation des alertes de sécurité dans Microsoft Defender pour Identity
description: Explique comment examiner les alertes de sécurité émises par Microsoft Defender pour Identity.
ms.date: 10/27/2020
ms.topic: how-to
ms.openlocfilehash: cb589442143bfd78f13360c076d9f5205c0a21af
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534427"
---
# <a name="working-with-security-alerts"></a>Utilisation des alertes de sécurité

> [!NOTE]
> Les fonctionnalités [!INCLUDE [Product long](includes/product-long.md)] décrites sur cette page sont également accessibles sur le nouveau [portail](https://portal.cloudappsecurity.com).

Cet article explique les bases de l’utilisation des alertes de sécurité [!INCLUDE [Product long](includes/product-long.md)].

<a name="review-suspicious-activities-on-the-attack-time-line"></a>

## <a name="review-security-alerts-on-the-attack-timeline"></a>Passer en revue les alertes de sécurité dans la chronologie des attaques 

Après connexion au portail [!INCLUDE [Product short](includes/product-short.md)], la **Chronologie des alertes de sécurité** s’ouvre automatiquement. Les alertes de sécurité sont listées par ordre chronologique, les plus récentes figurant en haut de la liste.

Une alerte de sécurité comprend les informations suivantes :

- Les entités impliquées, y compris les utilisateurs, les ordinateurs, les serveurs, les contrôleurs de domaine et les ressources

- L’heure et le délai d’exécution des activités suspectes ayant déclenché une alerte de sécurité.
- Gravité de l’alerte : haute, moyenne ou faible.
- État : Ouvert, fermé ou supprimé.
- Possibilité de :
  - Transmettre l’alerte de sécurité par e-mail à d’autres membres de votre entreprise.
  - Télécharger l’alerte de sécurité au format Excel.

> [!NOTE]
>
> - Lorsque vous pointez votre souris sur un utilisateur ou un ordinateur, un mini-profil d’entité s’affiche. Il fournit des informations complémentaires sur l’entité, notamment le nombre d’alertes de sécurité auxquelles est liée l’entité.
> - En cliquant sur une entité, vous êtes dirigé vers le profil d’entité de l’utilisateur ou l’ordinateur.

![Image de chronologie des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)]](media/sa-timeline.png)

## <a name="security-alert-categories"></a>Catégories des alertes de sécurité

Les alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] sont réparties en plusieurs catégories ou phases (cf. ci-dessous), comme les phases d’une chaîne cybercriminelle standard.

- [Alertes de reconnaissance](reconnaissance-alerts.md)
- [Alertes indiquant des informations d’identification compromises](compromised-credentials-alerts.md)
- [Alertes de mouvement latéral](lateral-movement-alerts.md)
- [Alertes de dominance du domaine](domain-dominance-alerts.md)
- [Alertes d’exfiltration](exfiltration-alerts.md)

## <a name="preview-detections"></a>Détections en préversion 

L’équipe de recherche [!INCLUDE [Product short](includes/product-short.md)] travaille sans relâche à l’implémentation de nouvelles détections pour les attaques récemment découvertes. Dans la mesure où [!INCLUDE [Product short](includes/product-short.md)] est un service cloud, ces nouvelles détections sont publiées rapidement pour permettre aux clients [!INCLUDE [Product short](includes/product-short.md)] d’en bénéficier aussi vite que possible.

Ces détections sont marquées d’un badge de préversion pour vous permettre d’identifier les nouvelles détections et les nouveautés du produit. Si vous désactivez les détections en préversion, elles n’apparaîtront pas dans la console [!INCLUDE [Product short](includes/product-short.md)] (ni dans la chronologie ni dans les profils d’entité). Les nouvelles alertes ne seront pas non plus ouvertes.

![Détection en préversion dans la chronologie](media/preview-detection-in-timeline.png)

Par défaut, les détections en préversion sont activées dans [!INCLUDE [Product short](includes/product-short.md)].

Pour désactiver les détections en préversion :

1. Dans la console [!INCLUDE [Product short](includes/product-short.md)] , sélectionnez **Configuration**.
1. Dans le menu de gauche, cliquez sur **Détections** sous **Préversion**.
1. Utilisez le curseur pour activer et désactiver les détections en préversion.

![détections en préversion](media/preview-detections.png)

## <a name="filter-security-alerts-list"></a>Filtrer la liste des alertes de sécurité

Pour filtrer la liste des alertes de sécurité :

1. Dans le volet **Filtrer par** sur le côté gauche de l’écran, sélectionnez l’une des options suivantes : **Tout**, **Ouvert**, **Fermé** ou **Ignoré**.

1. Pour filtrer la liste, sélectionnez **Haute**, **Moyenne** ou **Faible**.

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

![Actions [!INCLUDE [Product short](includes/product-short.md)] pour les alertes de sécurité](media/sa-actions.png)

**États des alertes de sécurité**

- **Ouvert** : toutes les nouvelles alertes de sécurité s’affichent dans la liste.

- **Fermé** : utilisé pour effectuer le suivi des activités que vous avez identifiées, examinées et résolues.

- **Ignoré** : permet d’ignorer temporairement une alerte, et de n’être averti de nouveau qu’en cas de nouvelle instance. Si une alerte similaire survient, [!INCLUDE [Product short](includes/product-short.md)] ne la rouvre pas. Cependant, si l’alerte cesse pendant sept jours avant de réapparaître, une nouvelle alerte est ouverte.

- **Supprimer** : Si vous supprimez une alerte, elle est supprimée du système et de la base de données, et vous NE pourrez PAS la restaurer. Si vous cliquez sur Supprimer, vous supprimez toutes les alertes de sécurité du même type.

- **Exclure** : Possibilité d’empêcher une entité de déclencher un certain type d’alertes. Par exemple, vous pouvez configurer [!INCLUDE [Product short](includes/product-short.md)] de façon à empêcher une entité spécifique (un utilisateur ou un ordinateur) de déclencher à nouveau une alerte pour un certain type d’activité (par exemple, un administrateur qui exécute du code à distance ou un scanner de sécurité qui effectue une reconnaissance DNS). En plus d’ajouter des exclusions directement dans l’alerte de sécurité lorsque celle-ci est détectée dans la chronologie, vous pouvez également accéder aux **Exclusions** de la page Configuration et, pour chaque alerte de sécurité, ajouter et supprimer manuellement des entités ou des sous-réseaux exclus (par exemple, pour les attaques pass-the-ticket).

> [!NOTE]
> Les pages de configuration ne sont modifiables que par les administrateurs [!INCLUDE [Product short](includes/product-short.md)].

## <a name="see-also"></a>Voir aussi

- [Utilisation du portail [!INCLUDE [Product short](includes/product-short.md)]](workspace-portal.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
