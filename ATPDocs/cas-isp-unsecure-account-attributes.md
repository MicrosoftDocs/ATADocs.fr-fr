---
title: Évaluation des attributs de compte non sécurisé Microsoft Defender pour l’identité
description: Cet article fournit une vue d’ensemble de Microsoft Defender pour les entités de l’identité avec des attributs non sécurisés rapport d’évaluation de la sécurité de l’identité.
ms.date: 01/18/2021
ms.topic: how-to
ms.openlocfilehash: 64aa95a423d0c8fc0bb210c2c10bc63f8c33bca4
ms.sourcegitcommit: 14f7228dbe6af353e81f20d2047dad24043840b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/31/2021
ms.locfileid: "99217700"
---
# <a name="security-assessment-unsecure-account-attributes"></a>Évaluation de la sécurité : Attributs de compte non sécurisés

## <a name="what-are-unsecure-account-attributes"></a>Qu’entend-on par « attributs de compte non sécurisés » ?

[!INCLUDE [Product long](includes/product-long.md)] surveille en permanence votre environnement afin d’identifier les comptes avec des valeurs d’attribut qui présentent un risque de sécurité et des rapports sur ces comptes pour vous aider à protéger votre environnement.

## <a name="what-risk-do-unsecure-account-attributes-pose"></a>Quels sont les risques posés par les attributs de compte non sécurisés ?

Quand une organisation ne parvient pas à sécuriser ses attributs de compte, elle laisse la porte ouverte aux acteurs malveillants.

Les acteurs malveillants, à l’instar des voleurs, recherchent souvent le moyen le plus simple et le plus silencieux de s’introduire dans un environnement. Les comptes configurés avec des attributs non sécurisés sont des fenêtres d’opportunités pour les attaquants et peuvent exposer des risques.

Par exemple, si l’attribut *PasswordNotRequired* est activé, un attaquant peut facilement accéder au compte. Cela est particulièrement risqué si le compte dispose d’un accès privilégié à d’autres ressources.

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez le tableau du rapport pour identifier les comptes qui présentent des attributs non sécurisés.
    ![Passer en revue les principales entités impactées et créer un plan d’action](media/cas-isp-unsecure-account-attributes-1.png)
1. Prenez les mesures appropriées sur ces comptes d’utilisateurs en modifiant ou supprimant les attributs en question.

> [!NOTE]
>
> - Cette évaluation est mise à jour en quasi-temps réel.
> - Cette évaluation peut contenir des entités supprimées précédemment si les [conditions préalables](prerequisites.md#before-you-start) pour [!INCLUDE [Product long](includes/product-long.md)] ne sont pas remplies.

## <a name="remediation"></a>Correction

Utilisez les mesures correctives adaptées à l’attribut en question, comme décrit dans le tableau suivant.

| Action recommandée | Correction | Raison |
| --- | --- | --- |
| Supprimer ne pas exiger la pré-authentification Kerberos| Supprimer ce paramètre des propriétés de compte dans Active Directory (AD) | La suppression de ce paramètre nécessite une pré-authentification Kerberos pour le compte, ce qui améliore la sécurité. |
| Supprimer Stocker le mot de passe en utilisant un chiffrement réversible | Supprimer ce paramètre des propriétés de compte dans AD | La suppression de ce paramètre empêche le déchiffrement facile du mot de passe du compte. |
| Supprimer Mot de passe non nécessaire | Supprimer ce paramètre des propriétés de compte dans AD | La suppression de ce paramètre nécessite l’utilisation d’un mot de passe avec le compte et empêche l’accès non autorisé aux ressources. |
| Supprimer Mot de passe stocké avec un chiffrement faible | Réinitialiser le mot de passe du compte | Le fait de changer le mot de passe du compte permet l’utilisation d’algorithmes de chiffrement plus forts pour sa protection. |
| Activer la prise en charge du chiffrement AES via Kerberos | Activer les fonctionnalités AES dans les propriétés de compte dans AD | L’activation d’AES128_CTS_HMAC_SHA1_96 ou d’AES256_CTS_HMAC_SHA1_96 sur le compte permet d’empêcher l’utilisation de chiffrements plus faibles pour l’authentification Kerberos. |
| Supprimer Utiliser les types de chiffrement DES via Kerberos pour ce compte | Supprimer ce paramètre des propriétés de compte dans AD | La suppression de ce paramètre permet l’utilisation d’algorithmes de chiffrement plus forts pour le mot de passe du compte. |

## <a name="see-also"></a>Voir aussi

- [[!INCLUDE [Product short](includes/product-short.md)] filtrage des activités dans Cloud App Security](activities-filtering-mcas.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
