---
title: Guide pratique pour investiguer des utilisateurs et des ordinateurs avec Azure ATP | Microsoft Docs
description: Décrit comment investiguer les activités suspectes effectuées par des utilisateurs, des entités, des ordinateurs ou des appareils avec Azure - Protection avancée contre les menaces (ATP, Advanced Threat Protection)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/3/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d892b22e46efee6ab8315a20e39bd7b47a4c824b
ms.sourcegitcommit: 6a0ac21f59e72db8615811da2c886f54cf3727f5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/13/2019
ms.locfileid: "54249944"
---
# <a name="tutorial-investigate-an-entity"></a>Didacticiel : Examiner une entité

Dans ce tutoriel, vous allez apprendre à investiguer les entités connectées à des activités suspectes détectées par Azure Advanced Threat Protection (ATP). Après avoir consulté une alerte de sécurité dans la chronologie, vous découvrirez comment explorer l’entité impliquée dans l’alerte, puis comment utiliser les paramètres et détails suivants pour en savoir plus sur ce qui est arrivé et sur ce que vous devez faire pour réduire les risques.

> [!div class="checklist"]
> * Vérifier le profil de l’entité
> * Vérifier les étiquettes des entités
> * Vérifier les indicateurs de contrôle de compte d’utilisateur
> * Croiser les informations avec Windows Defender
> * Surveiller les utilisateurs et les groupes sensibles
> * Passer en revue les chemins de mouvement latéral potentiels
> * Vérifier l’état de honeytoken

## <a name="check-the-entity-profile"></a>Vérifier le profil de l’entité

Le profil d’entité fournit une page complète sur l’entité, qui permet une enquête approfondie sur les utilisateurs, les ordinateurs, les périphériques et les ressources auxquelles ils ont accès et leur historique. La page de profil tire parti du nouveau traducteur d’activité logique Azure ATP qui peut examiner un groupe d’activités en cours (agrégées jusqu'à une minute) et les regrouper en une seule activité logique pour vous permettre de mieux comprendre les activités réelles de vos utilisateurs.

Pour accéder à une page de profil d’entité, cliquez sur le nom de l’entité, par exemple sur son nom d’utilisateur, dans la chronologie des alertes de sécurité. Vous pouvez également voir une version abrégée du profil de l’entité dans la page de l’alerte de sécurité, en pointant sur le nom de l’entité.

Le profil de l’entité vous permet de voir les activités de l’entité, les données de l’annuaire et les [chemins de mouvement latéral](use-case-lateral-movement-path.md) pour cette entité. Pour plus d’informations sur les entités, consultez [Présentation des profils d’entité](entity-profiles.md).

## <a name="check-entity-tags"></a>Vérifier les étiquettes des entités

Azure ATP extrait des étiquettes d’Active Directory pour vous offrir une même interface permettant de surveiller vos utilisateurs et vos entités Active Directory. Ces étiquettes vous donnent des informations relatives à l’entité d’Active Directory, notamment :
- Partiel : cet utilisateur, cet ordinateur ou ce groupe n’a été pas été synchronisé à partir du domaine, et a été partiellement résolu par le biais d’un catalogue global. Certains attributs ne sont pas disponibles.
- Non résolu : cet ordinateur n’a pas été résolu en une entité valide dans la forêt Active Directory. Aucune information d’annuaire n’est disponible.
- Supprimé : l’entité a été supprimée d’Active Directory.
- Désactivé : l’entité a été désactivée dans Active Directory.
- Verrouillé : l’entité a entré un mot de passe incorrect un trop grand nombre de fois et est verrouillée.
- Expiré : l’entité a expiré dans Active Directory.
- Nouveau : l’entité a été créée il y a moins de 30 jours.

## <a name="check-user-account-control-flags"></a>Vérifier les indicateurs de contrôle de compte d’utilisateur

Les indicateurs de contrôle de compte d’utilisateur sont également importés depuis Active Directory. Les données du répertoire d’entités Azure ATP incluent 10 indicateurs qui permettent une investigation : 
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

Azure ATP vous permet de savoir si ces indicateurs sont activés ou désactivés dans Azure Active Directory. Les icônes de couleur et le bouton bascule correspondant indiquent l’état de chaque indicateur. Dans l’exemple ci-dessous, seule l’option **Le mot de passe n'expire jamais** est activée dans Active Directory.

 ![indicateurs de contrôle de compte d’utilisateur](./media/user-access-flags.png)

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

## <a name="review-lateral-movement-paths"></a>Passer en revue les chemins de mouvement latéral

Azure ATP peut vous aider à empêcher les attaques qui utilisent des chemins de mouvement latéral. Il est question de mouvement latéral quand un attaquant utilise de façon proactive des comptes non sensibles pour accéder à des comptes sensibles.

Si un chemin de mouvement latéral existe pour une entité, dans la page de profil de l’entité, vous pouvez cliquer sur l’onglet **Chemins d’accès de mouvement latéral**. Le diagramme qui s’affiche vous fournit un mappage des chemins possibles pour votre utilisateur sensible. 

Pour plus d’informations, consultez [Examen des chemins de mouvement latéral avec Azure ATP](use-case-lateral-movement-path.md).

## <a name="check-honeytoken-status"></a>Vérifier l’état de honeytoken

Avant de procéder à votre investigation, il est important de savoir si l’entité est un honeytoken. Vous pouvez marquer les comptes et les entités comme des honeytokens dans Azure ATP. Lorsque vous ouvrez le profil d’entité ou le mini-profil d’un compte ou d’une entité marquée comme un honeytoken, le badge honeytoken apparaît. Lors de l’investigation, le badge honeytoken vous avertit que l’activité en cours de validation a été effectuée par un compte que vous avez marqué comme un honeytoken.

## <a name="see-also"></a>Voir aussi

- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)