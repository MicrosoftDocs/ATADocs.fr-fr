---
title: Microsoft Defender for Identity Microsoft couvre l’utilisation des évaluations
description: Cet article fournit une vue d’ensemble du rapport d’évaluation de l’évaluation de l’utilisation des identités Microsoft de Microsoft Defender pour les identités.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 170385cfb1bd3fc82a77d67cd6f82d2197c458bf
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848769"
---
# <a name="security-assessment-microsoft-laps-usage"></a>Évaluation de la sécurité : Utilisation de Microsoft LAPS

## <a name="what-is-microsoft-laps"></a>Qu’est-ce que Microsoft LAPS ?

La « solution de mot de passe d’administrateur local » (LAPS, Local Administrator Password Solution) de Microsoft fournit des capacités de gestion des mots de passe des comptes d’administrateur local pour les ordinateurs joints à un domaine. Les mots de passe sont aléatoires et stockés dans Active Directory (AD), protégés par des listes de contrôle d’accès. Par conséquent, seuls les utilisateurs éligibles peuvent les lire ou demander leur réinitialisation.

## <a name="what-risk-does-not-implementing-laps-pose-to-an-organization"></a>Quel risque prend une organisation si elle n’implémente pas LAPS ?

LAPS fournit une solution au problème lié à l’utilisation d’un compte local commun avec un mot de passe identique sur chaque ordinateur d’un domaine. LAPS résout ce problème en définissant un autre mot de passe aléatoire différent pour le compte d’administrateur local commun sur chaque ordinateur du domaine.

LAPS simplifie la gestion des mots de passe tout en permettant aux clients d’implémenter des défenses recommandées supplémentaires contre les cyberattaques. En particulier, la solution réduit le risque d’escalade latérale qui en résulte quand des clients utilisent la même combinaison et le même mot de passe de compte local administratif sur leurs ordinateurs. LAPS stocke le mot de passe du compte d’administrateur local de chaque ordinateur dans AD, et le sécurise dans un attribut confidentiel de l’objet AD correspondant de l’ordinateur. L’ordinateur peut mettre à jour ses propres données de mot de passe dans AD, et les administrateurs de domaine peuvent accorder un accès en lecture à des utilisateurs ou groupes autorisés, comme les administrateurs de support technique des stations de travail.

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez la table de rapport pour découvrir lesquels de vos domaines ont certains (ou tous les) appareils Windows compatibles non protégés par LAPS, ou dont le mot de passe managé LAPS n’a pas été changé au cours des 60 derniers jours.
1. Pour les domaines partiellement protégés, sélectionnez la ligne appropriée pour voir la liste des appareils non protégés par LAPS dans ce domaine.
    ![Sélectionner un domaine avec des appareils LAPS](media/cas-isp-laps-1.png)
1. Prenez la mesure appropriée sur ces appareils en téléchargeant, en installant et en configurant [Microsoft LAPS](https://go.microsoft.com/fwlink/?linkid=2104282), ou en résolvant les problèmes s’y rapportant, à l’aide de la documentation fournie dans le téléchargement.
    ![Corriger un appareil LAPS](media/cas-isp-laps-2.png)

> [!NOTE]
> Cette évaluation est mise à jour toutes les 24 heures.

## <a name="see-also"></a>Voir aussi

- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
