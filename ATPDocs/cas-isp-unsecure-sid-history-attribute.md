---
title: Évaluations des attributs d’historique SID non sécurisés d’Azure Advanced Threat Protection
description: Cet article fournit une vue d’ensemble du rapport d’évaluation de la posture de sécurité des identités fourni par Azure ATP concernant les entités ayant des attributs d’historique SID non sécurisés.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7819bf79ca70068be21f0aae0b08ff920d7a1605
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912741"
---
# <a name="security-assessment-unsecure-sid-history-attributes"></a>Évaluation de la sécurité : Attributs d’historique SID non sécurisés

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-is-an-unsecure-sid-history-attribute"></a>Qu’est-ce qu’un attribut d’historique SID non sécurisé ?

L’historique SID est un attribut qui prend en charge les [scénarios de migration](/previous-versions/windows/it-pro/windows-server-2003/cc779590(v=ws.10)). Chaque compte d’utilisateur est associé à un [identificateur de sécurité (SID)](/windows/win32/secauthz/security-identifiers) qui est utilisé pour suivre le principal de sécurité et l’accès du compte lors de la connexion à des ressources. L’historique SID permet que l’accès d’un autre compte soit efficacement cloné à un autre et est extrêmement utile pour garantir que les utilisateurs conservent l’accès quand ils sont déplacés (migrés) d’un domaine vers un autre.

L’évaluation recherche les comptes disposant d’attributs d’historique SID qu’Azure ATP a profilés comme étant risqués.

## <a name="what-risk-does-unsecure-sid-history-attribute-pose"></a>Quel risque l’attribut d’historique SID non sécurisé présente-t-il ?

Quand une organisation ne parvient pas à sécuriser ses attributs de compte, elle laisse la porte ouverte aux acteurs malveillants.

Les acteurs malveillants, à l’instar des voleurs, recherchent souvent le moyen le plus simple et le plus silencieux de s’introduire dans un environnement. Les comptes configurés avec un attribut d’historique SID non sécurisé sont des fenêtres d’opportunités pour les attaquants et peuvent présenter des risques.

Par exemple, un compte non sensible dans un domaine peut contenir le SID d’administrateur d’entreprise dans son historique SID d’un autre domaine de la forêt Active Directory, ce qui « élève » l’accès du compte d’utilisateur à un administrateur de domaine effectif dans tous les domaines de la forêt. De plus, si vous disposez d’une approbation de forêt pour laquelle le filtrage des SID (également appelé « mise en quarantaine ») n’est pas activé, il est possible d’injecter un SID à partir d’une autre forêt. Il est alors ajouté au jeton utilisateur au moment de son authentification et utilisé pour les évaluations d’accès.

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez la table de rapport pour découvrir les comptes qui ont un attribut d’historique SID non sécurisé.
    ![Passer en revue les principales entités impactées et créer un plan d’action](media/atp-cas-isp-unsecure-sid-history-attribute-1.png)
1. Prenez la mesure appropriée pour supprimer l’attribut d’historique SID des comptes à l’aide de PowerShell en effectuant les étapes suivantes :

    1. Identifiez le SID dans l’attribut SIDHistory défini sur le compte.

        ```powershell
        Get-ADUser -Identity <account> -Properties SidHistory | Select-Object -ExpandProperty SIDHistory
        ```

    2. Supprimez l’attribut SIDHistory à l’aide du SID identifié précédemment.

        ```powershell
        Set-ADUser -Identity <account> -Remove @{SIDHistory='S-1-5-21-...'}
        ```

> [!NOTE]
> Cette évaluation est mise à jour en quasi-temps réel.

## <a name="see-also"></a>Voir aussi

- [Filtrage des activités Azure ATP dans Cloud App Security](activities-filtering-mcas.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
