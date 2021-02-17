---
title: Advanced Threat Analytics à Microsoft Defender pour le déplacement de l’identité
description: Découvrez comment déplacer une installation Advanced Threat Analytics existante vers Microsoft Defender pour l’identité.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: f363543cca20e0dba853c58db1e1c1cc0c60ce22
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630541"
---
# <a name="advanced-threat-analytics-ata-to-microsoft-defender-for-identity"></a>ATA (Advanced Threat Analytics) à Microsoft Defender pour l’identité

> [!NOTE]
> La version finale d’ATA est mise à la [disposition générale](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9). ATA prendra fin au support standard le 12 janvier 2021. Le support étendu se poursuivra jusqu’au 2026 janvier. Pour plus d’informations, consultez [notre blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181).

Utilisez ce guide pour passer d’une installation ATA existante au service ( [!INCLUDE [Product long](includes/product-long.md)] ). Ce guide explique les conditions [!INCLUDE [Product short](includes/product-short.md)] préalables et la configuration requise, ainsi que les détails de la planification et de l’exécution de votre déplacement. Des étapes de validation et des conseils pour tirer parti des dernières solutions de sécurité et de protection contre les menaces avec [!INCLUDE [Product short](includes/product-short.md)] après l’installation sont également inclus.

Pour en savoir plus sur les différences entre ATA et [!INCLUDE [Product short](includes/product-short.md)] , consultez le [ [!INCLUDE [Product short](includes/product-short.md)] Forum aux questions](technical-faq.yml).

Dans ce guide, vous allez :

> [!div class="checklist"]
>
> - Vérifier et confirmer les [!INCLUDE [Product short](includes/product-short.md)] conditions préalables du service
> - Documenter votre configuration ATA existante
> - Planifier votre transfert
> - Configurer et configurer votre [!INCLUDE [Product short](includes/product-short.md)]  service
> - Effectuer des vérifications post-transfert
> - Désactiver ATA une fois le transfert terminé

> [!NOTE]
> Le passage à [!INCLUDE [Product short](includes/product-short.md)] d’ATA est possible à partir de n’importe quelle version d’ATA. Toutefois, comme les données ne peuvent pas être déplacées d’ATA vers [!INCLUDE [Product short](includes/product-short.md)] , il est recommandé de conserver les données et les alertes du centre ATA requises pour les investigations en cours jusqu’à ce que toutes les alertes ATA soient fermées ou corrigées.

## <a name="prerequisites"></a>Prérequis

- Un locataire Azure Active Directory avec au moins un administrateur global/de sécurité est requis pour créer une [!INCLUDE [Product short](includes/product-short.md)] instance. Chaque instance [!INCLUDE [Product short](includes/product-short.md)] prend en charge une limite de forêt Active Directory multiple et le niveau fonctionnel de forêt (FFL) Windows 2003 et versions ultérieures.

- [!INCLUDE [Product short](includes/product-short.md)] nécessite .NET Framework 4,7 ou une version ultérieure et peut nécessiter un contrôleur de domaine (redémarrage) si la version actuelle de .NET Framework n’est pas 4,7 ou version ultérieure.

- Assurez-vous que vos contrôleurs de domaine répondent à toutes les [ [!INCLUDE [Product short](includes/product-short.md)] conditions requises](prerequisites.md#azure-atp-sensor-requirements) par le capteur et que votre environnement est conforme à toutes les [ [!INCLUDE [Product short](includes/product-short.md)] exigences](prerequisites.md).

- Vérifiez que tous les contrôleurs de domaine que vous envisagez d’utiliser disposent d’un accès Internet suffisant au [!INCLUDE [Product short](includes/product-short.md)] service. Vérifiez et confirmez que vos contrôleurs de domaine satisfont à la [ [!INCLUDE [Product short](includes/product-short.md)] Configuration requise du proxy](configure-proxy.md).

> [!NOTE]
> Ce guide de migration est conçu [!INCLUDE [Product short](includes/product-short.md)] uniquement pour les capteurs.

## <a name="plan"></a>Plan

Veillez à rassembler les informations suivantes avant de commencer le transfert :

1. Détails de votre compte [Directory Services](install-step2.md).
1. [Paramètres](setting-syslog.md) de notification Syslog.
1. [Détails des notifications](notifications.md) par e-mail.
1. Appartenance au groupe de rôle ATA
1. Intégration VPN
1. Exclusions des alertes
    - Les exclusions ne peuvent pas être transférées d’ATA vers [!INCLUDE [Product short](includes/product-short.md)] . par conséquent, les détails de chaque exclusion sont requis pour [répliquer les exclusions dans [!INCLUDE [Product short](includes/product-short.md)] ](excluding-entities-from-detections.md).
1. Détails des comptes HoneyToken.
    - Si vous ne disposez pas déjà de comptes HoneyToken dédiés, en savoir plus sur les [HoneyTokens dans [!INCLUDE [Product short](includes/product-short.md)] ](configure-detection-exclusions.md) et créer des comptes à utiliser à cet effet.
1. Liste complète de toutes les entités (ordinateurs, groupes, utilisateurs) à étiqueter manuellement comme entités sensibles.
    - En savoir plus sur l’importance des [entités sensibles](manage-sensitive-honeytoken-accounts.md) dans [!INCLUDE [Product short](includes/product-short.md)] .
1. [Détails](reports.md) de la planification des rapports (liste des rapports et planifications).

> [!NOTE]
> Ne désinstallez pas le centre ATA tant que toutes les passerelles ATA n’ont pas été supprimées. Si vous désinstallez le centre ATA alors que des passerelles ATA sont en cours d’exécution, votre organisation se retrouve sans aucune protection contre les menaces.

## <a name="move"></a>Déplacer

Procédez à la migration [!INCLUDE [Product short](includes/product-short.md)] en deux étapes simples :

### <a name="step-1-create-and-install-defender-for-identity-instance-and-sensors"></a>Étape 1 : créer et installer Defender pour l’instance d’identité et les capteurs

1. [Créer votre nouvelle [!INCLUDE [Product short](includes/product-short.md)] instance](install-step1.md)

1. Désinstallez la passerelle légère ATA sur tous les contrôleurs de domaine.

1. Installez le [!INCLUDE [Product short](includes/product-short.md)] capteur sur tous les contrôleurs de domaine :
    - [Téléchargez les [!INCLUDE [Product short](includes/product-short.md)] fichiers de capteur](install-step3.md).
    - [Récupérer votre [!INCLUDE [Product short](includes/product-short.md)] Clé d’accès](install-step3.md#download-the-setup-package).
    - [Installez [!INCLUDE [Product short](includes/product-short.md)] les capteurs sur vos contrôleurs de domaine](install-step4.md).

### <a name="step-2-configure-and-validate-defender-for-identity-instance"></a>Étape 2 : configurer et valider Defender pour l’instance d’identité

- [Configurer le capteur](install-step5.md)

> [!NOTE]
> Certaines tâches de la liste suivante ne peuvent pas être effectuées avant d’installer des [!INCLUDE [Product short](includes/product-short.md)] capteurs, puis d’effectuer une synchronisation initiale, comme la sélection d’entités pour le balisage **sensible** manuelle. Prévoyez jusqu’à 2 heures pour la synchronisation initiale.

#### <a name="configuration"></a>Configuration

Connectez-vous au [!INCLUDE [Product short](includes/product-short.md)] portail et effectuez les tâches de configuration suivantes.

| Étape    | Action | État |
|--------------|------------|------------------|
| 1  | Définir des [mises à jour différées sur une sélection de contrôleurs de domaine](sensor-update.md) | - [ ] |
| 2  | Détails du compte [Services d’annuaire](install-step2.md).| - [ ] |
| 3  | Configurer des [notifications Syslog](setting-syslog.md) | - [ ] |
| 4  | Informations sur l’[intégration du VPN](install-step6-vpn.md)| - [ ] |
| 5  | Configurer [l’intégration de WDATP](integrate-mde.md)| - [ ] |
| 6  | Définir des comptes [HoneyTokens](configure-detection-exclusions.md)| - [ ] |
| 7  | Étiqueter les [entités sensibles](manage-sensitive-honeytoken-accounts.md)| - [ ] |
| 8  | Créer des [exclusions d’alerte de sécurité](excluding-entities-from-detections.md)| - [ ] |
| 9 | [Activer/désactiver les notifications par e-mail](notifications.md) | - [ ] |
| 10  | [Paramètres de planification des rapports](reports.md) (liste des rapports et planifications).| - [ ] |
| 11  | Configurer des [autorisations en fonction du rôle](role-groups.md) | - [ ] |
| 12  | [Configuration de notifications SIEM (adresse IP)](configure-event-collection.md#siemsyslog)| - [ ] |

#### <a name="validation"></a>Validation

Dans le [!INCLUDE [Product short](includes/product-short.md)] portail :

- Passez en revue les [alertes d’intégrité](health-center.md) à la recherche de problèmes de service.
- Consultez [!INCLUDE [Product short](includes/product-short.md)] les [journaux d’erreurs de capteur](troubleshooting-using-logs.md) pour connaître les erreurs inhabituelles.

## <a name="after-the-move"></a>Après le transfert

Cette section du guide présente les actions que vous pouvez effectuer à l’issue du transfert.

> [!NOTE]
> L’importation d’alertes de sécurité existantes à partir d’ATA vers [!INCLUDE [Product short](includes/product-short.md)] n’est pas prise en charge. Veillez à enregistrer ou à corriger toutes les alertes ATA existantes avant de désactiver le centre ATA.

- **Désactiver le centre ATA**  
  - Pour référencer les données du centre ATA après le transfert, nous vous recommandons de conserver les données du centre en ligne pendant un certain temps. Une fois le centre ATA désactivé, le nombre de ressources peut généralement être réduit, surtout si les ressources sont une machine virtuelle.

- **Sauvegarder MongoDB**  
  - Si vous souhaitez conserver les données ATA indéfiniment, [sauvegardez MongoDB](/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database).

## <a name="mission-accomplished"></a>Mission accomplie

Félicitations ! Votre passage d’ATA à [!INCLUDE [Product short](includes/product-short.md)] est terminé.

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur [[!INCLUDE [Product short](includes/product-short.md)]](what-is.md) les fonctionnalités, les fonctionnalités et les [alertes de sécurité](understanding-security-alerts.md).

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter de [!INCLUDE [Product short](includes/product-short.md)] et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté [!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) !
