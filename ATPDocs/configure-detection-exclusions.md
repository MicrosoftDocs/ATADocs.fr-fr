---
title: Exclusions de détection de la configuration de Microsoft Defender pour l’identité
description: Configuration des exclusions de détection.
ms.date: 02/17/2021
ms.topic: how-to
ms.openlocfilehash: 802b54f3185a50468fe4227d4099b9edbfc8f469
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097366"
---
# <a name="configure-detection-exclusions"></a>Configurer les exclusions de détection

[!INCLUDE [Product long](includes/product-long.md)] permet d’exclure des adresses IP, des ordinateurs ou des utilisateurs spécifiques d’un certain nombre de détections.

Par exemple, une **exclusion DNS Reconnaissance** peut être un analyseur de sécurité qui utilise DNS comme mécanisme d’analyse. L’exclusion permet d' [!INCLUDE [Product short](includes/product-short.md)] ignorer ces scanneurs.

## <a name="how-to-add-detection-exclusions"></a>Comment ajouter des exclusions de détection

Il existe deux façons d’exclure manuellement des utilisateurs, des ordinateurs ou des adresses IP pour une détection. Vous pouvez le faire dans la page **configuration** sous **exclusions**, ou directement à partir de l’alerte de sécurité.

### <a name="from-the-configuration-page"></a>À partir de la page de configuration

Pour configurer des exclusions à partir de la page Configuration, procédez comme suit :

1. Sur le portail [!INCLUDE [Product short](includes/product-short.md)], cliquez sur **Configuration**.

    ![[! INCLUDe [Product Short] (includes/Product-Short. MD)] paramètres de configuration](media/config-menu.png)

1. Sous **détection**, sélectionnez **exclusions**.
1. Pour chaque détection que vous souhaitez configurer, procédez comme suit :
    1. Entrer une adresse IP, un ordinateur ou un compte d’utilisateur à exclure de la détection
    1. Cliquez sur l’icône plus **(+)**.

    > [!TIP]
    > Le champ utilisateur ou ordinateur peut faire l’objet d’une recherche et sera automatiquement rempli avec les entités de votre réseau. Pour plus d’informations, consultez le [Guide des alertes de sécurité](suspicious-activity-guide.md).

    ![Exclusion d’entités des détections](media/exclusions.png)

1. Cliquez sur **Save**.

### <a name="from-a-security-alert"></a>À partir d’une alerte de sécurité

Pour configurer des exclusions à partir d’une alerte de sécurité, procédez comme suit :

1. Dans le [!INCLUDE [Product short](includes/product-short.md)] portail, sélectionnez **chronologie**.
1. Identifiez une alerte sur une activité pour un utilisateur, un ordinateur ou une adresse IP qui **est** autorisé à effectuer l’activité en question.

1. À droite de l’alerte, sélectionnez **plus [...]**  >  **Fermer et exclure**. L’action ferme l’alerte et n’est plus répertoriée dans la liste événements **ouverts** dans la **chronologie** de l’alerte. L’action ajoute également l’utilisateur, l’ordinateur ou l’adresse IP à la liste des exclusions pour cette alerte.

    ![Exclure une entité](media/exclude-in-sa.png)

[!INCLUDE [Product short](includes/product-short.md)] l’analyse démarre immédiatement. Certaines détections, telles que les [ajouts suspects à des groupes sensibles](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024), nécessitent une période d’apprentissage et ne sont pas disponibles immédiatement après le [!INCLUDE [Product short](includes/product-short.md)] déploiement. La période d’apprentissage pour chaque alerte est indiquée dans le [Guide](suspicious-activity-guide.md)détaillé des alertes de sécurité.

## <a name="see-also"></a>Voir aussi

- [Configurer la collecte d’événements](configure-event-collection.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
