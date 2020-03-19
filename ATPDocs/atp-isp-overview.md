---
title: 'Azure Advanced Threat Protection : évaluations de la posture de sécurité des identités'
description: Cet article propose une vue d’ensemble des rapports d’évaluation de la posture de sécurité des identités fournis par Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 71b15bd9-3183-4e24-b18a-705023ccc313
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 27e6a0c474b06e21942e4e07211c608f7cdfd1fd
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414078"
---
# <a name="azure-atps-identity-security-posture-assessments"></a>Évaluations de la posture de sécurité des identités Azure ATP
 
En raison d’un manque de visibilité, les organisations de toutes tailles ne savent généralement pas si leurs applications et services locaux peuvent introduire une faille de sécurité. Ce problème de visibilité limitée est particulièrement vrai en ce qui concerne l’utilisation de composants non pris en charge ou obsolètes. 

Même si votre entreprise investit beaucoup de temps et d’efforts pour renforcer de manière continue la sécurité des identités et de leur infrastructure (comme Active Directory ou Active Directory Connect), vous pouvez très bien ne pas être au courant des erreurs de configuration fréquentes et de l’utilisation de composants hérités qui présentent un risque majeur pour votre organisation. Les recherches sur la sécurité réalisées par Microsoft révèlent que la plupart des attaques d’identité exploitent les erreurs de configurations courantes dans Active Directory et l’utilisation continue de composants hérités (tels que le protocole NTLMv1) pour compromettre les identités et s’introduire dans votre organisation. Pour lutter efficacement contre cela, Azure ATP propose des évaluations proactives de la posture de sécurité des identités pour détecter et suggérer des actions d’amélioration à l’échelle de vos configurations Active Directory locales. 

## <a name="what-do-azure-atp-identity-security-posture-assessments-provide"></a>Qu’apportent les évaluations de la posture de sécurité des identités Azure ATP ?  
- Détections et données contextuelles sur les composants exploitables et les erreurs de configuration connus, ainsi que des chemins de résolution appropriés.
- Azure ATP détecte non seulement les activités suspectes, mais supervise aussi activement vos identités locales et leur infrastructure à la recherche de points faibles avec le capteur Azure ATP existant. 
- Rapports d’évaluation précis sur la posture de sécurité actuelle de votre organisation, d’où la possibilité de mettre en place des réponses rapides et la supervision des effets en continu. 

## <a name="how-do-i-get-started"></a>Comment faire pour commencer 

### <a name="access"></a>Access

Vous pouvez accéder aux évaluations de la sécurité Azure ATP dans le portail Microsoft Cloud App Security après avoir activé l’intégration d’Azure ATP. Pour apprendre à intégrer Azure ATP à Cloud App Security, consultez [Intégration d’Azure ATP](https://docs.microsoft.com/cloud-app-security/aatp-integration). 

### <a name="licensing"></a>Licences

L’accès aux rapports d’évaluation de la sécurité Azure ATP dans Cloud App Security ne nécessite pas de licence Cloud App Security. Seule une licence Azure ATP est nécessaire. 

## <a name="access-azure-atp-using-cloud-app-security"></a>Accéder à Azure ATP avec Cloud App Security 

Consultez le [guide de démarrage rapide de Cloud App Security](https://docs.microsoft.com/cloud-app-security/getting-started-with-cloud-app-security) pour vous familiariser avec les principes de base du portail Cloud App Security. 

**Évaluations de la posture de sécurité des identités**

Les évaluations de la posture de sécurité des identités d’Azure ATP sont listées ci-dessous. Chaque évaluation est un rapport téléchargeable contenant des instructions d’utilisation et des outils permettant de générer un plan d’action pour corriger ou résoudre les problèmes. 

**Rapports d’évaluation**
- Empêcher les [entités exposant les informations d’identification en texte clair](atp-cas-isp-clear-text.md)
- Empêcher l’[utilisation des protocoles hérités](atp-cas-isp-legacy-protocols.md)
- Empêcher l’[utilisation de chiffrements faibles](atp-cas-isp-weak-cipher.md)
- Empêcher les [délégations Kerberos non sécurisées](atp-cas-isp-unconstrained-kerberos.md)
- Désactiver le [service Spouleur d’impression sur les contrôleurs de domaine](atp-cas-isp-print-spooler.md)
- Supprimer les [entités dormantes des groupes sensibles](atp-cas-isp-dormant-entities.md)

Pour accéder aux évaluations de la posture de sécurité des identités :
1. Ouvrez le portail **Microsoft Cloud App Security**. 
    ![Accéder aux rapports de la posture de sécurité des identités Azure ATP dans Cloud App Security](media/atp-cas-isp-report-1.png)
1. Sélectionnez **Examiner** dans le menu de gauche, puis cliquez sur **Posture de sécurité des identités** dans le menu déroulant. 
1. Dans la liste **Rapports d’évaluation de la sécurité** qui s’ouvre, cliquez sur l’évaluation de la posture de sécurité des identités que vous souhaitez examiner.  


## <a name="next-steps"></a>Étapes suivantes
- [En savoir plus sur l’utilisation de Cloud App Security avec Azure ATP](atp-activities-filtering-mcas.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)

