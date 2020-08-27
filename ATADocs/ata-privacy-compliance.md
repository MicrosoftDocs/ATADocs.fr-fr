---
title: Stratégie de données personnelles d’Advanced Threat Analytics
description: Fournit des liens vers des informations sur la suppression des informations personnelles et des données personnelles à partir d’ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 9/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1b2d185c-62cd-45f0-b0dd-687b51317f32
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: 1ae7d9277de591f54cdb1918ee72174a806b1c96
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88954032"
---
# <a name="ata-data-security-and-privacy"></a>Sécurité et confidentialité des données ATA

*S’applique à : Advanced Threat Analytics version 1.9*

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="searching-for-and-identifying-personal-data"></a>Recherche et identification des données personnelles 

Toutes les données dans ATA qui se rapportent à des entités sont dérivées d’AD (Active Directory) et répliquées sur ATA. Quand vous recherchez des données personnelles, vous devez donc d’abord les rechercher sur AD. 

À partir du centre ATA, utilisez la barre de recherche pour afficher les données personnelles identifiables qui sont stockées dans la base de données. Les utilisateurs peuvent rechercher un utilisateur ou un appareil spécifique. Cliquez sur l’entité pour ouvrir la page de profil de l’utilisateur ou de l’appareil. Le profil fournit les détails complets de l’entité, son historique et l’activité réseau associée dérivée d’AD. 

## <a name="updating-personal-data"></a>Mise à jour des données personnelles 

Les données personnelles des utilisateurs et des entités dans ATA sont dérivées de l’objet utilisateur figurant dans l’AD de votre organisation. Pour cette raison, toutes les modifications apportées au profil utilisateur dans AD sont répercutées dans ATA. 

## <a name="deleting-personal-data"></a>Suppression des données personnelles 

Bien que les données d’ATA soient répliquées et toujours mises à jour à partir d’Active Directory, lorsqu’une entité est supprimée dans Active Directory, les données de l’entité dans ATA sont conservées à des fins d’investigation de sécurité. 

Pour supprimer définitivement les données relatives à un utilisateur dans la base de données ATA, effectuez les étapes suivantes : 

1. [Téléchargez](https://aka.ms/ata-gdpr-script) le script MongoDB (gdpr.js).  

1. Copiez le script dans le dossier ATA (qui se trouve dans `"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB`) et exécutez la commande suivante à partir la machine du centre ATA : 

Utilisez le script de base de données RGPD d’ATA pour supprimer les entités et les données d’activité qui s’y rapportent, comme décrit dans les sections suivantes.

### <a name="delete-entities"></a>Supprimer des entités

Cette action supprime définitivement une entité dans la base de données ATA. Pour exécuter cette commande, indiquez le nom de commande `deleteAccount` et le paramètre `SamName`, `UpnName` ou `GUID` pour l’ordinateur ou le nom d’utilisateur que vous souhaitez supprimer. Par exemple : 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteAccount,admin1@contoso.com';" GDPR.js`

L’exécution de cette commande supprime l’entité avec l’UPN admin1@contoso.com dans la base de données, ainsi que toutes les activités et alertes de sécurité associées à cette entité. 

### <a name="delete-entity-activity-data"></a>Supprimer les données d’activité des entités

Cette action supprime définitivement les données d’activité des entités dans la base de données ATA. Les entités proprement dites restent inchangées, mais les activités et les alertes de sécurité qui s’y rapportent pour la période spécifiée sont supprimées. 

Pour exécuter cette commande, indiquez le nom de commande `deleteOldData` et le nombre de jours de données que vous souhaitez conserver dans la base de données. 

Par exemple : 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteOldData,30';" GDPR.js`

Ce script supprime entièrement les données de toutes les activités et alertes de sécurité des entités dans la base de données qui datent de plus de 30 jours. Seuls les 30 derniers jours de données sont conservés.

## <a name="exporting-personal-data"></a>Exportation des données personnelles 

Du fait que les données relatives aux entités dans ATA sont dérivées d’AD, seul un sous-ensemble de ces données est stocké dans la base de données ATA. Pour cette raison, vous devez exporter les données relatives aux entités à partir d’AD. 

ATA vous permet d’exporter dans Excel toutes les informations de sécurité, qui sont susceptibles d’inclure des données personnelles. 

 
## <a name="opt-out-of-system-generated-logs"></a>Désactivation des journaux générés par le système 

ATA collecte des journaux générés par le système rendus anonymes sur chaque déploiement et les transmet via une connexion HTTPS aux serveurs Microsoft. Ces données sont utilisées par Microsoft pour améliorer les futures versions d’ATA. 

Pour plus d’informations, consultez [Gérer les journaux générés par le système](manage-telemetry-settings.md).

Pour désactiver la collecte de données :

1. Connectez-vous à la console ATA, cliquez sur les trois points dans la barre d’outils, puis sélectionnez **À propos de**. 
1. Décochez la case **Envoyez-nous des informations d’utilisation pour nous aider à améliorer votre expérience utilisateur à l’avenir**. 

## <a name="additional-resources"></a>Ressources supplémentaires

- Pour plus d’informations sur l’approbation et la conformité dans ATA, consultez le [portail d’approbation de services](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) et le [site sur la conformité RGPD de Microsoft 365 Enterprise](/microsoft-365/compliance/gdpr).