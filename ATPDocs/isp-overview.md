---
title: 'Azure Advanced Threat Protection : évaluations de la posture de sécurité des identités'
description: Cet article propose une vue d’ensemble des rapports d’évaluation de la posture de sécurité des identités fournis par Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/16/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 71b15bd9-3183-4e24-b18a-705023ccc313
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: eaef6571a11852e66634e9043daa25ec8fdbe2ef
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910201"
---
# <a name="azure-atps-identity-security-posture-assessments"></a>Évaluations de la posture de sécurité des identités Azure ATP

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

En raison d’un manque de visibilité, les organisations de toutes tailles ne savent généralement pas si leurs applications et services locaux peuvent introduire une faille de sécurité. Ce problème de visibilité limitée est particulièrement vrai en ce qui concerne l’utilisation de composants non pris en charge ou obsolètes.

Même si votre entreprise investit beaucoup de temps et d’efforts pour renforcer de manière continue la sécurité des identités et de leur infrastructure (comme Active Directory ou Active Directory Connect), vous pouvez très bien ne pas être au courant des erreurs de configuration fréquentes et de l’utilisation de composants hérités qui présentent un risque majeur pour votre organisation. Les recherches sur la sécurité réalisées par Microsoft révèlent que la plupart des attaques d’identité exploitent les erreurs de configurations courantes dans Active Directory et l’utilisation continue de composants hérités (tels que le protocole NTLMv1) pour compromettre les identités et s’introduire dans votre organisation. Pour lutter efficacement contre cela, Azure ATP propose des évaluations proactives de la posture de sécurité des identités pour détecter et suggérer des actions d’amélioration à l’échelle de vos configurations Active Directory locales.

## <a name="what-do-azure-atp-identity-security-posture-assessments-provide"></a>Qu’apportent les évaluations de la posture de sécurité des identités Azure ATP ?

- Détections et données contextuelles sur les composants exploitables et les erreurs de configuration connus, ainsi que des chemins de résolution appropriés.
- Azure ATP détecte non seulement les activités suspectes, mais supervise aussi activement vos identités locales et leur infrastructure à la recherche de points faibles avec le capteur Azure ATP existant.
- Rapports d’évaluation précis sur la posture de sécurité actuelle de votre organisation, d’où la possibilité de mettre en place des réponses rapides et la supervision des effets en continu.

## <a name="how-do-i-get-started"></a>Comment faire pour commencer

### <a name="access"></a>Access

Vous pouvez accéder aux évaluations de la sécurité Azure ATP dans le portail Microsoft Cloud App Security après avoir activé l’intégration d’Azure ATP. Pour apprendre à intégrer Azure ATP à Cloud App Security, consultez [Intégration d’Azure ATP](/cloud-app-security/aatp-integration).

### <a name="licensing"></a>Licences

L’accès aux rapports d’évaluation de la sécurité Azure ATP dans Cloud App Security ne nécessite pas de licence Cloud App Security. Seule une licence Azure ATP est nécessaire.

## <a name="access-azure-atp-using-cloud-app-security"></a>Accéder à Azure ATP avec Cloud App Security

Consultez le [guide de démarrage rapide de Cloud App Security](/cloud-app-security/getting-started-with-cloud-app-security) pour vous familiariser avec les principes de base du portail Cloud App Security.

**Évaluations de la posture de sécurité des identités**

Les évaluations de la posture de sécurité des identités d’Azure ATP sont listées ci-dessous. Chaque évaluation est un rapport téléchargeable contenant des instructions d’utilisation et des outils permettant de générer un plan d’action pour corriger ou résoudre les problèmes.

**Rapports d’évaluation**

- [Contrôleurs de domaine avec le service Spouleur d’impression disponible](cas-isp-print-spooler.md)
- [Entités dormantes dans les groupes sensibles](cas-isp-dormant-entities.md)
- [Entités exposant les informations d’identification en texte clair](cas-isp-clear-text.md)
- [Utilisation de Microsoft LAPS](cas-isp-laps.md)
- [Utilisation des protocoles hérités](cas-isp-legacy-protocols.md)
- [Chemins de mouvement latéral les plus risqués](cas-isp-riskiest-lmp.md)
- [Contrôleurs de domaine non supervisés](cas-isp-unmonitored-domain-controller.md)
- [Attributs de compte non sécurisé](cas-isp-unsecure-account-attributes.md)
- [Délégation Kerberos non sécurisée](cas-isp-unconstrained-kerberos.md)
- [Attributs d’historique SID non sécurisés](cas-isp-unsecure-sid-history-attribute.md)
- [Utilisation d’un chiffrement faible](cas-isp-weak-cipher.md)

Pour accéder aux évaluations de la posture de sécurité des identités :

1. Ouvrez le portail **Microsoft Cloud App Security**.
    ![Accéder aux rapports de la posture de sécurité des identités Azure ATP dans Cloud App Security](media/atp-cas-isp-report-1.png)
1. Sélectionnez **Examiner** dans le menu de gauche, puis cliquez sur **Posture de sécurité des identités** dans le menu déroulant.
1. Dans la liste **Rapports d’évaluation de la sécurité** qui s’ouvre, cliquez sur l’évaluation de la posture de sécurité des identités que vous souhaitez examiner.

## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus sur l’utilisation de Cloud App Security avec Azure ATP](activities-filtering-mcas.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)