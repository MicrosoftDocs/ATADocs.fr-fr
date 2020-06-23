---
title: Évaluation de l’utilisation de Microsoft LAPS d’Azure Advanced Threat Protection
description: Cet article fournit une vue d’ensemble du rapport d’évaluation de la posture de sécurité des identités fourni par Azure ATP concernant l’utilisation Microsoft LAPS.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/20/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a8829ed9f1cb13ba86f940ceff0c60428bea5210
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84774347"
---
# <a name="security-assessment-microsoft-laps-usage"></a>Évaluation de la sécurité : Utilisation de Microsoft LAPS

## <a name="what-is-microsoft-laps"></a>Qu’est-ce que Microsoft LAPS ?

La « solution de mot de passe d’administrateur local » (LAPS, Local Administrator Password Solution) de Microsoft fournit des capacités de gestion des mots de passe des comptes d’administrateur local pour les ordinateurs joints à un domaine. Les mots de passe sont aléatoires et stockés dans Active Directory (AD), protégés par des listes de contrôle d’accès. Par conséquent, seuls les utilisateurs éligibles peuvent les lire ou demander leur réinitialisation.

## <a name="what-risk-does-not-implementing-laps-pose-to-an-organization"></a>Quel risque prend une organisation si elle n’implémente pas LAPS ?

LAPS fournit une solution au problème lié à l’utilisation d’un compte local commun avec un mot de passe identique sur chaque ordinateur d’un domaine. LAPS résout ce problème en définissant un autre mot de passe aléatoire différent pour le compte d’administrateur local commun sur chaque ordinateur du domaine.

LAPS simplifie la gestion des mots de passe tout en permettant aux clients d’implémenter des défenses recommandées supplémentaires contre les cyberattaques. En particulier, la solution réduit le risque d’escalade latérale qui en résulte quand des clients utilisent la même combinaison et le même mot de passe de compte local administratif sur leurs ordinateurs. LAPS stocke le mot de passe du compte d’administrateur local de chaque ordinateur dans AD, sécurisé dans un attribut confidentiel de l’objet AD correspondant de l’ordinateur. L’ordinateur peut mettre à jour ses propres données de mot de passe dans AD, et les administrateurs de domaine peuvent accorder un accès en lecture à des utilisateurs ou groupes autorisés, comme les administrateurs de support technique des stations de travail.

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez la table de rapport pour découvrir lesquels de vos domaines ont certains (ou tous les) appareils Windows compatibles non protégés par LAPS, ou dont le mot de passe managé LAPS n’a pas été changé au cours des 60 derniers jours.
1. Pour les domaines partiellement protégés, sélectionnez la ligne appropriée pour voir la liste des appareils non protégés par LAPS dans ce domaine.
    ![Sélectionner un domaine avec des appareils LAPS](media/atp-cas-isp-laps-1.png)
1. Prenez la mesure appropriée sur ces appareils en téléchargeant, en installant et en configurant [Microsoft LAPS](https://go.microsoft.com/fwlink/?linkid=2104282), ou en résolvant les problèmes s’y rapportant, à l’aide de la documentation fournie dans le téléchargement.
    ![Corriger un appareil LAPS](media/atp-cas-isp-laps-2.png)

## <a name="see-also"></a>Voir aussi

- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
