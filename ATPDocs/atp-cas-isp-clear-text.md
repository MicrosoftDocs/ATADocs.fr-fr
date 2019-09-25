---
title: 'Azure Advanced Threat Protection : évaluation de l’exposition de texte clair | Microsoft Docs'
description: Cet article propose une vue d’ensemble du rapport d’évaluation de la posture de sécurité des identités fourni par Azure ATP concernant l’exposition de texte clair.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 124957bb-5882-4fcf-bab2-b74b0c69571d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8e99ab22e65538aba6f645d6bb7929330244cafc
ms.sourcegitcommit: 475df3e87d8476ff13e48ebc7a722f46f29dab70
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2019
ms.locfileid: "71007545"
---
# <a name="security-assessment-entities-exposing-credentials-in-clear-text-----preview"></a>Évaluation de la sécurité : Entités exposant les informations d’identification en texte clair - Préversion

![Empêcher l’exposition d’informations d’identification en texte clair dans Cloud App Security](media/atp-cas-isp-clear-text-1.png)

## <a name="what-information-does-the-prevent-clear-text-security-assessment-provide"></a>Quelles sont les informations fournies par l’évaluation de la sécurité concernant le texte clair? 

Cette évaluation de la sécurité supervise votre trafic à la recherche d’entités exposant des informations d’identification en texte clair et vous alerte sur les risques d’exposition actuels (entités les plus impactées) dans votre organisation. Des suggestions de correction sont également proposées. 

## <a name="why-is-clear-text-credential-exposure-risky"></a>Pourquoi l’exposition d’informations d’identification en texte clair présente-t-elle un risque ?  
Les entités qui exposent des informations d’identification en texte clair posent non seulement un risque pour l’entité exposée en question, mais aussi pour toute l’organisation.  

Ce risque accru est dû au fait que le trafic non sécurisé, comme une liaison simple LDAP, est très sensible aux attaques de l’intercepteur (« man in the middle »). Ces types d’attaques entraînent des activités malveillantes, notamment l’exploitation par un attaquant des informations d’identification exposées à des fins malveillantes. 

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Comment faire pour utiliser cette évaluation de la sécurité afin d’améliorer la sécurité de mon organisation ? 

1. Passez en revue l’évaluation de la sécurité pour identifier les entités impactées. 
    ![Passer en revue les principales entités impactées et créer un plan d’action](media/atp-cas-isp-clear-text-2.png)
1. Recherchez la raison pour laquelle ces entités utilisent LDAP en texte clair. 
1. Corrigez les problèmes et arrêtez l’exposition. 
1. Une fois la correction confirmée, nous vous recommandons d’exiger la signature LDAP au niveau du contrôleur de domaine. Pour en savoir plus sur la signature des serveurs LDAP, consultez [Contrôleur de domaine : conditions requises pour la signature de serveur LDAP](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/domain-controller-ldap-server-signing-requirements). 
 

## <a name="next-steps"></a>Étapes suivantes
- [Filtrage des activités Azure ATP dans Cloud App Security](atp-activities-filtering-mcas.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)