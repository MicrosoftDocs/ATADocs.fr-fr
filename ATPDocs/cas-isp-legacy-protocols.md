---
title: 'Azure Advanced Threat Protection : évaluation de la posture de sécurité des identités concernant les protocoles hérités'
description: Cet article propose une vue d’ensemble du rapport d’évaluation de la posture de sécurité des identités fourni par Azure ATP concernant les protocoles hérités.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 6597b8c7-f83e-43c6-8149-fb4a914a845b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2eb9fb04c5f0adee2f98d73549ece6db88b0aeac
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828226"
---
# <a name="security-assessment-legacy-protocols-usage"></a>Évaluation de la sécurité : Utilisation des protocoles hérités

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

    ![Empêcher l’utilisation de protocoles hérités](media/atp-cas-isp-legacy-protocols-2.png)
1. Prenez les mesures nécessaires concernant ces entités pour découvrir les dépendances.
1. Cessez d’utiliser les protocoles hérités, puis [désactivez complètement ces protocoles](/archive/blogs/miriamxyra/stop-using-lan-manager-and-ntlmv1).
1. [Supprimez MIC 2 et cessez d’utiliser les clients LMv2](https://www.preempt.com/blog/active-directory-ntlm-attacks/).

> [!NOTE]
> Cette évaluation est mise à jour en quasi-temps réel.

## <a name="next-steps"></a>Étapes suivantes

- [Filtrage des activités Azure ATP dans Cloud App Security](activities-filtering-mcas.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)