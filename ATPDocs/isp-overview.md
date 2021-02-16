---
title: Évaluation de l’état de la sécurité des identités Microsoft Defender
description: Cet article fournit une vue d’ensemble des rapports d’évaluation de l’évaluation de la sécurité des identités de Microsoft Defender.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 3b3f20ac50e3b5b687dd6ece8b421c84288a3126
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533849"
---
# <a name="microsoft-defender-for-identitys-identity-security-posture-assessments"></a>Évaluation de l’état de la sécurité des identités Microsoft Defender

En raison d’un manque de visibilité, les organisations de toutes tailles ne savent généralement pas si leurs applications et services locaux peuvent introduire une faille de sécurité. Ce problème de visibilité limitée est particulièrement vrai en ce qui concerne l’utilisation de composants non pris en charge ou obsolètes.

Même si votre entreprise investit beaucoup de temps et d’efforts pour renforcer de manière continue la sécurité des identités et de leur infrastructure (comme Active Directory ou Active Directory Connect), vous pouvez très bien ne pas être au courant des erreurs de configuration fréquentes et de l’utilisation de composants hérités qui présentent un risque majeur pour votre organisation. Les recherches sur la sécurité réalisées par Microsoft révèlent que la plupart des attaques d’identité exploitent les erreurs de configurations courantes dans Active Directory et l’utilisation continue de composants hérités (tels que le protocole NTLMv1) pour compromettre les identités et s’introduire dans votre organisation. Pour le combattre efficacement, [!INCLUDE [Product long](includes/product-long.md)] propose désormais des évaluations de la sécurité des identités proactives pour détecter et suggérer des actions d’amélioration dans vos configurations de Active Directory sur site.

## <a name="what-do-defender-for-identity-identity-security-posture-assessments-provide"></a>Qu’est-ce que l’évaluation de la sécurité des identités de l’identité de l’identité ?

- Détections et données contextuelles sur les composants exploitables et les erreurs de configuration connus, ainsi que des chemins de résolution appropriés.
- [!INCLUDE [Product short](includes/product-short.md)] détecte non seulement les activités suspectes, mais surveille activement vos identités locales et votre infrastructure d’identité pour les points faibles, en utilisant le [!INCLUDE [Product short](includes/product-short.md)] capteur existant.
- Rapports d’évaluation précis sur la posture de sécurité actuelle de votre organisation, d’où la possibilité de mettre en place des réponses rapides et la supervision des effets en continu.

## <a name="how-do-i-get-started"></a>Comment faire pour commencer

### <a name="access"></a>Access

[!INCLUDE [Product short](includes/product-short.md)] les évaluations de sécurité sont disponibles à l’aide du portail Microsoft Cloud App Security après l’activation de l' [!INCLUDE [Product short](includes/product-short.md)] intégration. Pour savoir comment intégrer [!INCLUDE [Product short](includes/product-short.md)] dans Cloud App Security, consultez [ [!INCLUDE [Product short](includes/product-short.md)] intégration](/cloud-app-security/aatp-integration).

### <a name="licensing"></a>Licences

L’accès aux [!INCLUDE [Product short](includes/product-short.md)] rapports d’évaluation de la sécurité dans Cloud App Security ne nécessite pas de licence Cloud App Security, seule une [!INCLUDE [Product short](includes/product-short.md)] licence est requise.

## <a name="access-defender-for-identity-using-cloud-app-security"></a>Access Defender pour l’identité à l’aide de Cloud App Security

Consultez le [guide de démarrage rapide de Cloud App Security](/cloud-app-security/getting-started-with-cloud-app-security) pour vous familiariser avec les principes de base du portail Cloud App Security.

**Évaluations de la posture de sécurité des identités**

[!INCLUDE [Product short](includes/product-short.md)] offre les évaluations de position de sécurité d’identité suivantes. Chaque évaluation est un rapport téléchargeable contenant des instructions d’utilisation et des outils permettant de générer un plan d’action pour corriger ou résoudre les problèmes.

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
    ![Accès à [ ! INCLUDe [Product Short] (includes/Product-Short. MD)] rapports de l’état de la sécurité des identités dans Cloud App Security](media/cas-isp-report-1.png)
1. Sélectionnez **Examiner** dans le menu de gauche, puis cliquez sur **Posture de sécurité des identités** dans le menu déroulant.
1. Dans la liste **Rapports d’évaluation de la sécurité** qui s’ouvre, cliquez sur l’évaluation de la posture de sécurité des identités que vous souhaitez examiner.

## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus sur l’utilisation de Cloud App Security avec [!INCLUDE [Product short](includes/product-short.md)]](activities-filtering-mcas.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
