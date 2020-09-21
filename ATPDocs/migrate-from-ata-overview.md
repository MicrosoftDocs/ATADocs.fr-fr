---
title: Passer d’Advanced Threat Analytics à Azure Advanced Threat Protection
description: Découvrez comment faire passer une installation Advanced Threat Analytics existante à Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/13/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e734e382-c4b1-43ca-9a8d-96c91daf2578
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cb9a6c8e560b6e52a6385cf4e926aae8cc723ca8
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828324"
---
# <a name="advanced-threat-analytics-ata-to-azure-advanced-threat-protection-azure-atp"></a>Passer d’Advanced Threat Analytics (ATA) à Azure Advanced Threat Protection (Azure ATP)

Utilisez ce guide pour faire passer une installation ATA existante au service Azure Advanced Threat Protection (Azure ATP). Ce guide explique les prérequis et les exigences d’Azure ATP. Il décrit également comment planifier et mener à bien votre transfert. Vous trouverez également des étapes de validation et des conseils pour tirer parti des solutions de sécurité et de protection contre les menaces les plus récentes avec Azure ATP après l’installation.

Pour plus d’informations sur les différences entre ATA et Azure ATP, consultez la [Foire aux questions Azure ATP](technical-faq.md#what-is-azure-atp).

Dans ce guide, vous allez :

> [!div class="checklist"]
>
> - Passer en revue et confirmer les prérequis du service Azure ATP
> - Documenter votre configuration ATA existante
> - Planifier votre transfert
> - Installer et configurer votre service Azure ATP
> - Effectuer des vérifications post-transfert
> - Désactiver ATA une fois le transfert terminé

> [!NOTE]
> Vous pouvez passer à Azure ATP à partir de n’importe quelle version d’ATA. Toutefois, comme les données ne peuvent pas passer d’ATA à Azure ATP, nous vous recommandons de conserver les données et alertes du centre ATA nécessaires pour les examens en cours jusqu’à ce que toutes les alertes ATA soient fermées ou corrigées.

## <a name="prerequisites"></a>Prérequis

- Un locataire Azure Active Directory avec au moins un administrateur général ou de sécurité est nécessaire pour créer une instance Azure ATP. Chaque instance Azure ATP prend en charge une limite de forêt Active Directory multiple et le niveau fonctionnel de forêt (FFL) Windows 2003 et versions ultérieures.

- Azure ATP exige .NET Framework 4.7 ou version ultérieure. Si vous ne disposez pas d’une telle version, il peut exiger le redémarrage du contrôleur de domaine.

- Vérifiez que vos contrôleurs de domaine répondent à toutes les [exigences du capteur Azure ATP](prerequisites.md#azure-atp-sensor-requirements) et que votre environnement répond à toutes les [exigences d’Azure ATP](prerequisites.md).

- Vérifiez que tous les contrôleurs de domaine que vous envisagez d’utiliser disposent d’un accès Internet suffisant au service Azure ATP. Vérifiez et confirmez que vos contrôleurs de domaine répondent aux [exigences de configuration d’un proxy Azure ATP](configure-proxy.md).

> [!NOTE]
> Ce guide de migration est destién uniquement aux capteurs Azure ATP.

## <a name="plan"></a>Plan

Veillez à rassembler les informations suivantes avant de commencer le transfert :

1. Détails de votre compte [Directory Services](install-step2.md).
1. [Paramètres](setting-syslog.md) de notification Syslog.
1. [Détails des notifications](notifications.md) par e-mail.
1. Appartenance au groupe de rôle ATA
1. Intégration VPN
1. Exclusions des alertes
    - Les exclusions n’étant pas transférables d’ATA vers Azure ATP, les détails de chaque exclusion sont nécessaires pour [répliquer les exclusions dans Azure ATP](excluding-entities-from-detections.md).
1. Détails des comptes HoneyToken.
    - Si vous ne disposez pas de comptes HoneyToken dédiés, découvrez-en plus sur [HoneyTokens dans Azure ATP](install-step7.md) et créez des comptes à cet effet.
1. Liste complète de toutes les entités (ordinateurs, groupes, utilisateurs) à étiqueter manuellement comme entités sensibles.
    - Découvrez l’importance des [entités sensibles](sensitive-accounts.md) dans Azure ATP.
1. [Détails](reports.md) de la planification des rapports (liste des rapports et planifications).

> [!NOTE]
> Ne désinstallez pas le centre ATA tant que toutes les passerelles ATA n’ont pas été supprimées. Si vous désinstallez le centre ATA alors que des passerelles ATA sont en cours d’exécution, votre organisation se retrouve sans aucune protection contre les menaces.

## <a name="move"></a>Déplacer

Pour finir de passer à Azure ATP, effectuez ces deux étapes simples :

### <a name="step-1-create-and-install-azure-atp-instance-and-sensors"></a>Étape 1 : Créer et installer une instance et des capteurs Azure ATP

1. [Créer votre instance Azure ATP](install-step1.md)

1. Désinstallez la passerelle légère ATA sur tous les contrôleurs de domaine.

1. Installez le capteur Azure ATP sur tous les contrôleurs de domaine :
    - [Téléchargez les fichiers du capteur Azure ATP](install-step3.md).
    - [Récupérez votre clé d’accès Azure ATP](install-step3.md#download-the-setup-package).
    - [Installez des capteurs Azure ATP sur vos contrôleurs de domaine](install-step4.md).

### <a name="step-2-configure-and-validate-azure-atp-instance"></a>Étape 2 : Configurer et valider l’instance Azure ATP

- [Configurer le capteur](install-step5.md)

> [!NOTE]
> Certaines tâches de la liste suivante, comme la sélection d’entités pour attribuer manuellement l’étiquette **Sensible**, ne peuvent pas être effectuées avant l’installation de capteurs Azure ATP et la synchronisation initiale. Prévoyez jusqu’à 2 heures pour la synchronisation initiale.

#### <a name="configuration"></a>Configuration

Connectez-vous au portail Azure ATP et effectuez les tâches de configuration suivantes.

| Étape    | Action | État |
|--------------|------------|------------------|
| 1  | Définir des [mises à jour différées sur une sélection de contrôleurs de domaine](sensor-update.md) | - [ ] |
| 2  | Détails du compte [Services d’annuaire](install-step2.md).| - [ ] |
| 3  | Configurer des [notifications Syslog](setting-syslog.md) | - [ ] |
| 4  | Informations sur l’[intégration du VPN](install-step6-vpn.md)| - [ ] |
| 5  | Configurer [l’intégration de WDATP](integrate-msde.md)| - [ ] |
| 6  | Définir des comptes [HoneyTokens](install-step7.md)| - [ ] |
| 7  | Étiqueter les [entités sensibles](sensitive-accounts.md)| - [ ] |
| 8  | Créer des [exclusions d’alerte de sécurité](excluding-entities-from-detections.md)| - [ ] |
| 9 | [Activer/désactiver les notifications par e-mail](notifications.md) | - [ ] |
| 10  | [Paramètres de planification des rapports](reports.md) (liste des rapports et planifications).| - [ ] |
| 11  | Configurer des [autorisations en fonction du rôle](role-groups.md) | - [ ] |
| 12  | [Configuration de notifications SIEM (adresse IP)](configure-event-collection.md#siemsyslog)| - [ ] |

#### <a name="validation"></a>Validation

Dans le portail Azure ATP :

- Passez en revue les [alertes d’intégrité](health-center.md) à la recherche de problèmes de service.
- Passez en revue les [journaux des erreurs de capteur](troubleshooting-using-logs.md) Azure ATP à la recherche d’erreurs inhabituelles.

## <a name="after-the-move"></a>Après le transfert

Cette section du guide présente les actions que vous pouvez effectuer à l’issue du transfert.

> [!NOTE]
> L’importation d’alertes de sécurité existantes d’ATA vers ATP n’est pas prise en charge. Veillez à enregistrer ou à corriger toutes les alertes ATA existantes avant de désactiver le centre ATA.

- **Désactiver le centre ATA**  
  - Pour référencer les données du centre ATA après le transfert, nous vous recommandons de conserver les données du centre en ligne pendant un certain temps. Une fois le centre ATA désactivé, le nombre de ressources peut généralement être réduit, surtout si les ressources sont une machine virtuelle.

- **Sauvegarder MongoDB**  
  - Si vous souhaitez conserver les données ATA indéfiniment, [sauvegardez MongoDB](/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database).

## <a name="mission-accomplished"></a>Mission accomplie

Félicitations ! Vous venez de passer d’ATA à Azure ATP.

## <a name="next-steps"></a>Étapes suivantes

Découvrez plus en détail les fonctionnalités d’[Azure ATP](what-is.md), ses fonctions et les [alertes de sécurité](understanding-security-alerts.md).

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) dès aujourd’hui !