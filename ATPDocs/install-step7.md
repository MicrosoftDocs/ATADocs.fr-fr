---
title: Microsoft Defender for Identity configurer les exclusions de détection et les comptes honeytoken
description: Configuration d’exclusions de détection et de comptes honeytoken
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
ms.openlocfilehash: 68ed20a243a307992b2d11c633728bf34abf6302
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93277031"
---
# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>Configurer des exclusions d’adresses IP et de comptes honeytoken

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[!INCLUDE [Product long](includes/product-long.md)] permet d’exclure des adresses IP ou des utilisateurs spécifiques d’un certain nombre de détections.

Par exemple, une **exclusion DNS Reconnaissance** peut être un analyseur de sécurité qui utilise DNS comme mécanisme d’analyse. L’exclusion permet d' [!INCLUDE [Product short](includes/product-short.md)] ignorer ces scanneurs.

[!INCLUDE [Product short](includes/product-short.md)] active également la configuration des comptes honeytoken, qui sont utilisés comme interruptions pour les acteurs malveillants. toute authentification associée à ces comptes honeytoken (normalement dormant) déclenche une alerte.

Pour la configuration, procédez comme suit :

1. À partir du [!INCLUDE [Product short](includes/product-short.md)] portail, cliquez sur l’icône des paramètres et sélectionnez **configuration**.

    ![[! INCLUDe [Product Short] (includes/Product-Short. MD)] paramètres de configuration](media/config-menu.png)

1. Sous **Détection** , cliquez sur **Étiquettes d’entité**.

1. Sous **Comptes Honeytoken** , entrez le nom du compte Honeytoken et cliquez sur le signe **+** . Le champ des comptes Honeytoken peut faire l’objet d’une recherche et affiche automatiquement les entités dans votre réseau. Cliquez sur **Save**.

    ![Honeytoken](media/honeytoken-sensitive.png)

1. Cliquez sur **Exclusions**. Pour chaque type de menace, entrez un compte d’utilisateur ou une adresse IP à exclure de la détection.
1. Cliquez sur le signe *plus*. Le champ **Ajouter une entité** (utilisateur ou ordinateur) peut faire l’objet d’une recherche et est automatiquement renseigné avec les entités de votre réseau. Pour plus d’informations, consultez [Exclusion d’entités des détections](excluding-entities-from-detections.md) et le [Guide des alertes de sécurité](suspicious-activity-guide.md).

    ![Exclusion d’entités des détections](media/exclusions.png)

1. Cliquez sur **Save**.

Félicitations, vous avez réussi à déployer [!INCLUDE [Product long](includes/product-long.md)] !

Vérifiez la chronologie des attaques pour afficher les alertes de sécurité générées par des activités détectées et rechercher des utilisateurs ou des ordinateurs et afficher leurs profils.

[!INCLUDE [Product short](includes/product-short.md)] l’analyse démarre immédiatement. Certaines détections, telles que les [ajouts suspects à des groupes sensibles](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024), nécessitent une période d’apprentissage et ne sont pas disponibles immédiatement après le [!INCLUDE [Product short](includes/product-short.md)] déploiement. La période d’apprentissage pour chaque alerte est indiquée dans le [Guide](suspicious-activity-guide.md)détaillé des alertes de sécurité.

## <a name="see-also"></a>Voir aussi

- [[!INCLUDE [Product short](includes/product-short.md)] outil de dimensionnement](https://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [[!INCLUDE [Product short](includes/product-short.md)] conditions préalables](prerequisites.md)
- [Consultez le [!INCLUDE [Product short](includes/product-short.md)] Forum !](https://aka.ms/MDIcommunity)
