---
title: Évaluations des attributs de compte non sécurisés d’Azure Advanced Threat Protection
description: Cet article offre une vue d’ensemble des entités d’Azure ATP avec le rapport d’évaluation de la posture de sécurité des identités d’attributs non sécurisés.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d0f415d58026fe0e44b365d7f8a6f995226532bc
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912757"
---
# <a name="security-assessment-unsecure-account-attributes"></a>Évaluation de la sécurité : Attributs de compte non sécurisés

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-are-unsecure-account-attributes"></a>Qu’entend-on par « attributs de compte non sécurisés » ?

Azure ATP supervise en permanence votre environnement pour identifier les comptes dont les valeurs d’attributs présentent un risque de sécurité. Vous en êtes informé à travers des rapports qui vous aident à protéger votre environnement.

## <a name="what-risk-do-unsecure-account-attributes-pose"></a>Quels sont les risques posés par les attributs de compte non sécurisés ?

Quand une organisation ne parvient pas à sécuriser ses attributs de compte, elle laisse la porte ouverte aux acteurs malveillants.

Les acteurs malveillants, à l’instar des voleurs, recherchent souvent le moyen le plus simple et le plus silencieux de s’introduire dans un environnement. Les comptes configurés avec des attributs non sécurisés sont une aubaine pour les attaquants et peuvent être exposés à des risques.

Par exemple, si l’attribut *PasswordNotRequired* est activé, un attaquant peut facilement accéder au compte. Cela est particulièrement risqué si le compte dispose d’un accès privilégié à d’autres ressources.

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez le tableau du rapport pour identifier les comptes qui présentent des attributs non sécurisés.
    ![Passer en revue les principales entités impactées et créer un plan d’action](media/atp-cas-isp-unsecure-account-attributes-1.png)
1. Prenez les mesures appropriées sur ces comptes d’utilisateurs en modifiant ou supprimant les attributs en question.

> [!NOTE]
> Cette évaluation est mise à jour en quasi-temps réel.

## <a name="remediation"></a>Correction

Utilisez les mesures correctives adaptées à l’attribut en question, comme décrit dans le tableau suivant.

| Action recommandée | Correction | Raison |
| --- | --- | --- |
| Supprimer Utiliser les types de chiffrement DES via Kerberos pour ce compte| Supprimer ce paramètre des propriétés de compte dans Active Directory (AD) | La suppression de ce paramètre nécessite une pré-authentification Kerberos pour le compte, ce qui améliore la sécurité. |
| Supprimer Stocker le mot de passe en utilisant un chiffrement réversible | Supprimer ce paramètre des propriétés de compte dans AD | La suppression de ce paramètre empêche le déchiffrement facile du mot de passe du compte. |
| Supprimer Mot de passe non nécessaire | Supprimer ce paramètre des propriétés de compte dans AD | La suppression de ce paramètre nécessite l’utilisation d’un mot de passe avec le compte et empêche l’accès non autorisé aux ressources. |
| Supprimer Mot de passe stocké avec un chiffrement faible | Réinitialiser le mot de passe du compte | Le fait de changer le mot de passe du compte permet l’utilisation d’algorithmes de chiffrement plus forts pour sa protection. |
| Activer la prise en charge du chiffrement AES via Kerberos | Activer les fonctionnalités AES dans les propriétés de compte dans AD | L’activation d’AES128_CTS_HMAC_SHA1_96 ou d’AES256_CTS_HMAC_SHA1_96 sur le compte permet d’empêcher l’utilisation de chiffrements plus faibles pour l’authentification Kerberos. |
| Supprimer Utiliser les types de chiffrement DES via Kerberos pour ce compte | Supprimer ce paramètre des propriétés de compte dans AD | La suppression de ce paramètre permet l’utilisation d’algorithmes de chiffrement plus forts pour le mot de passe du compte. |

## <a name="see-also"></a>Voir aussi

- [Filtrage des activités Azure ATP dans Cloud App Security](activities-filtering-mcas.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
