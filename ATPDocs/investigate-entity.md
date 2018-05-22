---
title: Guide pratique pour investiguer des utilisateurs et des ordinateurs avec Azure ATP | Microsoft Docs
description: Décrit comment investiguer les activités suspectes effectuées par des utilisateurs, des entités, des ordinateurs ou des appareils avec Azure - Protection avancée contre les menaces (ATP, Advanced Threat Protection)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/6/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4ef4151a311dd5b076737cba9f3c7aa7454a32a7
ms.sourcegitcommit: 714a01edc9006b38d1163d03852dafc2a5fddb5f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2018
---
*S’applique à : Azure - Protection avancée contre les menaces version 1.9*



# <a name="investigate-an-entity-with-azure-atp"></a>Investiguer une entité avec Azure ATP

Cet article décrit le processus d’investigation des entités après que des activités suspectes ont été détectées avec Azure - Protection avancée contre les menaces. Quand vous voyez une activité suspecte dans la chronologie, vous pouvez explorez l’entité impliquée dans l’activité, et utiliser les paramètres et les détails suivants pour en savoir plus sur ce qui est arrivé, ainsi que ce que vous devez faire pour réduire le risque.

## <a name="look-at-the-entity-profile"></a>Examiner le profil de l’entité

Le profil d’entité fournit une page complète sur l’entité, qui permet une enquête approfondie sur les utilisateurs, les ordinateurs, les périphériques et les ressources auxquelles ils ont accès et leur historique. La page de profil tire parti du nouveau traducteur d’activité logique Azure ATP qui peut examiner un groupe d’activités en cours (agrégées jusqu'à une minute) et les regrouper en une seule activité logique pour vous permettre de mieux comprendre les activités réelles de vos utilisateurs.

Pour accéder à une page de profil d’entité, cliquez sur le nom de l’entité, par exemple sur son nom d’utilisateur, dans la chronologie des activités suspectes. Vous pouvez aussi voir une version abrégée du profil de l’entité dans la page de l’activité suspecte, en pointant sur le nom de l’entité.

Le profil de l’entité vous permet de voir les activités de l’entité, les données de l’annuaire et les chemins de mouvement latéral pour cette entité. Pour plus d’informations, consultez [Enquête sur les profils d’entité](entity-profiles.md).

## <a name="check-entity-tags"></a>Vérifier les étiquettes des entités

Azure ATP extrait des étiquettes d’Active Directory pour vous offrir une même interface permettant de surveiller vos utilisateurs et vos entités Active Directory. Ces étiquettes vous donnent des informations relatives à l’entité d’Active Directory, notamment :
- Partiel : cet utilisateur, cet ordinateur ou ce groupe n’a été pas été synchronisé à partir du domaine, et a été partiellement résolu via un catalogue global. Certains attributs ne sont pas disponibles.
- Non résolu : cet ordinateur n’a pas été résolu en une entité valide dans la forêt Active Directory. Aucune information d’annuaire n’est disponible.
- Supprimé : l’entité a été supprimée d’Active Directory.
- Désactivé : l’entité a été désactivée dans Active Directory.
- Verrouillé : l’entité a entré un mot de passe incorrect un trop grand nombre de fois et elle est verrouillée.
- Expiré : l’entité a expiré dans Active Directory.
- Nouveau : l’entité a été créée il y a moins de 30 jours.

## <a name="look-at-the-user-access-control-flags"></a>Examiner les indicateurs de contrôle d’accès utilisateur

Les indicateurs de contrôle d’accès utilisateur sont également importés depuis Active Directory. Azure ATP inclut 10 indicateurs qui permettent une investigation : 
- Le mot de passe n’expire jamais
- Approuvé pour délégation
- Carte à puce nécessaire
- Mot de passe expiré
- Absence de mot de passe autorisée
- Mot de passe en texte brut stocké
- Ne peut pas être délégué
- Chiffrement DES uniquement
- Authentification préalable Kerberos non requise
- Compte désactivé 

Azure ATP vous permet de savoir si ces indicateurs sont activés ou désactivés dans Azure Active Directory. Des icônes colorées indiquent que l’indicateur est activé dans Active Directory. Dans l’exemple ci-dessous, seul **Compte désactivé** est activé dans Active Directory.

 ![Indicateurs de contrôle d’accès d’utilisateur](./media/user-access-flags.png)

## <a name="cross-check-with-windows-defender"></a>Croiser les informations avec Windows Defender

Pour vous fournir des insights résultant du croisement entre les produits, votre profil d’entité vous indique avec un badge les entités pour lesquelles des alertes sont actives dans Windows Defender. Ce badge vous permet de savoir combien d’alertes sont ouvertes pour l’entité dans Windows Defender et quel est leur niveau de gravité. Cliquez sur le badge pour accéder directement aux alertes associées à cette entité dans Windows Defender.


## <a name="keep-an-eye-on-sensitive-users-and-groups"></a>Surveiller les utilisateurs et les groupes sensibles

Azure ATP importe des informations sur les utilisateurs et les groupes depuis Azure Active Directory, qui vous permettent d’identifier les utilisateurs automatiquement considérés comme sensibles, car membres des groupes suivants dans Active Directory :

-   Administrateurs
-   Utilisateurs avec pouvoir
-   Opérateurs de compte
-   Opérateurs de serveur
-   Opérateurs d'impression
-   Opérateurs de sauvegarde
-   Duplicateurs
-   Utilisateurs du Bureau à distance 
-   Opérateurs de configuration réseau 
-   Générateurs d’approbation de forêt entrante
-   Administrateurs du domaine
-   Contrôleurs de domaine
-   Propriétaires créateurs de la stratégie de groupe 
-   Contrôleurs de domaine en lecture seule 
-   Contrôleurs de domaine d’entreprise en lecture seule 
-   Administrateurs du schéma 
-   Administrateurs de l’entreprise

En outre, vous pouvez **étiqueter manuellement**  des entités comme sensibles dans Azure ATP. Ceci est important, car certaines détections d’Azure ATP, comme la détection des modifications des groupes sensibles et le chemin de mouvement latéral, reposent sur l’état indiquant le caractère sensible d’une entité. Si vous étiquetez manuellement d’autres utilisateurs ou groupes comme sensibles, par exemple les membres du conseil d’administration, les cadres de la société et le directeur des ventes, Azure ATP les considère comme étant sensibles. Pour plus d’informations, consultez [Utilisation de comptes sensibles](sensitive-accounts.md).

## <a name="be-aware-of-lateral-movement-paths"></a>Être informé des chemins de mouvement latéral

Azure ATP peut vous aider à empêcher les attaques qui utilisent des chemins de mouvement latéral. Il est question de mouvement latéral quand un attaquant utilise de façon proactive des comptes non sensibles pour accéder à des comptes sensibles.

Si un chemin de mouvement latéral existe pour une entité, dans la page de profil de l’entité, vous pouvez cliquer sur l’onglet **Chemins d’accès de mouvement latéral**. Le diagramme qui s’affiche vous fournit un mappage des chemins possibles pour votre utilisateur sensible. 

Pour plus d’informations, consultez [Examen des chemins de mouvement latéral avec Azure ATP](use-case-lateral-movement-path.md).


## <a name="is-it-a-honeytoken-entity"></a>Est-ce une entité honeytoken ?

Avant de procéder à votre investigation, il est important de savoir si l’entité est un honeytoken. Pour vous faciliter la tâche, Azure ATP vous permet d’étiqueter des comptes et des entités comme honeytokens. Ensuite, lors de l’investigation, quand vous ouvrez le profil d’entité ou un mini-profil, vous voyez l’étiquette « honeytoken » pour vous avertir que l’activité que vous examinez a été effectuée par un compte que vous avez étiqueté comme étant un honeytoken.


    
## <a name="see-also"></a>Voir aussi

- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)