---
title: Évaluation de l’exposition Clear Text pour l’identité de Microsoft Defender
description: Cet article fournit une vue d’ensemble du rapport d’évaluation de la sécurité de l’évaluation de l’exposition du texte en clair de Microsoft Defender pour l’identité.
ms.date: 08/25/2020
ms.topic: how-to
ms.openlocfilehash: ce95dd461716d72e97787f797c8326da81a43118
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543788"
---
# <a name="security-assessment-entities-exposing-credentials-in-clear-text"></a>Évaluation de la sécurité : Entités exposant les informations d’identification en texte clair

![Empêcher l’exposition d’informations d’identification en texte clair dans Cloud App Security](media/cas-isp-clear-text-1.png)

## <a name="what-information-does-the-prevent-clear-text-security-assessment-provide"></a>Quelles sont les informations fournies par l’évaluation de la sécurité concernant le texte clair?

Cette évaluation de la sécurité supervise votre trafic à la recherche d’entités exposant des informations d’identification en texte clair et vous alerte sur les risques d’exposition actuels (entités les plus impactées) dans votre organisation. Des suggestions de correction sont également proposées.

## <a name="why-is-clear-text-credential-exposure-risky"></a>Pourquoi l’exposition d’informations d’identification en texte clair présente-t-elle un risque ?

Les entités qui exposent des informations d’identification en texte clair posent non seulement un risque pour l’entité exposée en question, mais aussi pour toute l’organisation.

Ce risque accru est dû au fait que le trafic non sécurisé, comme une liaison simple LDAP, est très sensible aux attaques de l’intercepteur (« man in the middle »). Ces types d’attaques entraînent des activités malveillantes, notamment l’exploitation par un attaquant des informations d’identification exposées à des fins malveillantes.

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Comment faire pour utiliser cette évaluation de la sécurité afin d’améliorer la sécurité de mon organisation ?

1. Passez en revue l’évaluation de la sécurité pour identifier les entités impactées.
    ![Passer en revue les principales entités impactées et créer un plan d’action](media/cas-isp-clear-text-2.png)
1. Recherchez la raison pour laquelle ces entités utilisent LDAP en texte clair.
1. Corrigez les problèmes et arrêtez l’exposition.
1. Une fois la correction confirmée, nous vous recommandons d’exiger la signature LDAP au niveau du contrôleur de domaine. Pour en savoir plus sur la signature des serveurs LDAP, consultez [Contrôleur de domaine : conditions requises pour la signature de serveur LDAP](/windows/security/threat-protection/security-policy-settings/domain-controller-ldap-server-signing-requirements).

> [!NOTE]
> Cette évaluation est mise à jour en quasi-temps réel.

## <a name="next-steps"></a>Étapes suivantes

- [[!INCLUDE [Product short](includes/product-short.md)] filtrage des activités dans Cloud App Security](activities-filtering-mcas.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)