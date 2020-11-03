---
title: Microsoft Defender pour identifier les anciens protocoles Identity Security position Assessment
description: Cet article fournit une vue d’ensemble du rapport d’évaluation de l’évaluation de l’état de la sécurité des identités du protocole hérité de Microsoft Defender.
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
ms.openlocfilehash: 223ae21d15ecc15523c3670062aa6a2502281738
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93276720"
---
# <a name="security-assessment-legacy-protocols-usage"></a>Évaluation de la sécurité : Utilisation des protocoles hérités

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-are-legacy-protocols"></a>Que sont les protocoles hérités ?

Compte tenu de toutes les opérations standard effectuées par les entreprises pour protéger leur infrastructure, notamment l’application de correctifs et la sécurisation des serveurs, il arrive souvent que la mise hors service des protocoles hérités soit négligée. Sans réduire l’exposition des protocoles hérités, le vol d’informations d’identification reste relativement facile à accomplir.

La plupart des protocoles hérités ont été élaborés et créés avant l’établissement des besoins de sécurité actuels et avant la mise en place par les entreprises modernes d’exigences claires en matière de sécurité. Toutefois, les protocoles hérités restant inchangés, ils peuvent facilement être transformés en points d’accès vulnérables dans toute organisation moderne.

## <a name="what-risks-do-retained-legacy-protocols-introduce"></a>Quels sont les risques introduits par les protocoles hérités ?

Les cyberattaques modernes utilisent souvent des protocoles hérités de manière spécifique, le plus souvent pour cibler des organisations qui n’ont pas encore implémenté de mesures d’atténuation appropriées.

Il est possible de réduire la surface d’attaque en désactivant la prise en charge des protocoles hérités non sécurisés, notamment :

- TLS 1.0 et 1.1 (ainsi que toutes les versions de SSL)
- SMBv1 (Server Message Block v1)
- LanMan (LM) / NTLMv1
- Authentification Digest

Pour mettre hors service les protocoles hérités, votre organisation doit d’abord découvrir les entités et les applications internes qui en dépendent. Le tableau du rapport d’évaluation **Utilisation des protocoles hérités** liste les principales entités qui utilisent des protocoles hérités (pour l’instant, NTLMv1). À l’aide du rapport, vous pouvez immédiatement passer en revue les entités les plus impactées et prendre des mesures appropriées, arrêter d’utiliser ces protocoles et éventuellement les désactiver complètement. Pour plus d’informations sur les dangers liés à l’utilisation de protocoles hérités, consultez [Arrêter d’utiliser LAN Manager et NTLMv1!](/archive/blogs/miriamxyra/stop-using-lan-manager-and-ntlmv1) et [Drop The MIC 2 & Exploiting LMv2 Clients](https://www.preempt.com/blog/active-directory-ntlm-attacks/).

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez le tableau de rapport pour découvrir les principales entités qui utilisent des protocoles hérités.

    ![Empêcher l’utilisation de protocoles hérités](media/cas-isp-legacy-protocols-2.png)
1. Prenez les mesures nécessaires concernant ces entités pour découvrir les dépendances.
1. Cessez d’utiliser les protocoles hérités, puis [désactivez complètement ces protocoles](/archive/blogs/miriamxyra/stop-using-lan-manager-and-ntlmv1).
1. [Supprimez MIC 2 et cessez d’utiliser les clients LMv2](https://www.preempt.com/blog/active-directory-ntlm-attacks/).

> [!NOTE]
> Cette évaluation est mise à jour en quasi-temps réel.

## <a name="next-steps"></a>Étapes suivantes

- [[!INCLUDE [Product short](includes/product-short.md)] filtrage des activités dans Cloud App Security](activities-filtering-mcas.md)
- [Consultez le [!INCLUDE [Product short](includes/product-short.md)] Forum !](https://aka.ms/MDIcommunity)