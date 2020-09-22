---
title: Nouveautés d’ATA version 1.9
description: Liste les nouveautés de la version 1.9 d’ATA ainsi que les problèmes connus
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 51de491c-49ba-4aff-aded-cc133a8ccf0b
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 01c8d55654ed4e1b425f8a043628e425496da4cb
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912814"
---
# <a name="whats-new-in-ata-version-19"></a>Nouveautés d’ATA version 1.9

[!INCLUDE [Rebranding notice](includes/rebranding.md)]
La dernière version de la mise à jour d’ATA peut être [téléchargée à partir du Centre de téléchargement](https://www.microsoft.com/download/details.aspx?id=56725) ou la version complète peut être téléchargée à partir du [centre d’évaluation](https://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Ces notes de publication fournissent des informations sur les mises à jour, les nouvelles fonctionnalités, les correctifs de bogue et les problèmes connus de cette version d’Advanced Threat Analytics.

## <a name="new--updated-detections"></a>Détections nouvelles et mises à jour

-  **Création de service suspect** : les attaquants tentent d’exécuter un service suspect sur votre réseau. ATA génère désormais une alerte quand il voit qu’une personne exécute un nouveau service qui semble suspect sur un contrôleur de domaine. Cette détection est basée sur des événements (pas le trafic réseau). Pour plus d’informations, consultez le [guide des activités suspectes](suspicious-activity-guide.md#suspicious-service-creation).


## <a name="new-reports-to-help-you-investigate"></a>Nouveaux rapports pour vous aider dans votre analyse 

- L’option [**Mots de passe exposés en texte clair**](reports.md) vous permet de détecter quand des comptes, sensibles ou pas, envoient des informations d’identification de compte en texte clair. Vous pouvez ainsi investiguer et limiter l’utilisation d’une liaison simple LDAP dans votre environnement pour améliorer le niveau de sécurité de votre réseau. Ce rapport remplace les alertes d’activité suspecte en texte clair de compte sensible et de service.

- L’option [**Chemins de mouvement latéral vers des comptes sensibles**](reports.md) liste les comptes sensibles qui sont exposés via des chemins de mouvement latéral. Il vous permet de limiter ces chemins et de renforcer votre réseau pour réduire le risque de surface d’attaque. Vous pouvez ainsi empêcher le mouvement latéral pour ne pas que les attaquants se déplacent sur votre réseau entre les utilisateurs et les ordinateurs et finissent par toucher le jackpot en termes de sécurité virtuel : vos informations d’identification de compte administrateur sensibles.

## <a name="improved-investigation"></a>Investigation avancée

- ATA 1.9 inclut un nouveau [profil d’entité](entity-profiles.md) amélioré. Le profil d’entité vous fournit un tableau de bord conçu pour des investigations approfondies complètes sur les utilisateurs, les ressources auxquelles ils accèdent et leur historique. Le profil d’entité vous permet également d’identifier les utilisateurs sensibles qui sont accessibles via les chemins de mouvement latéral. 

- Avec ATA 1.9, vous pouvez [identifier manuellement des groupes](tag-sensitive-accounts.md) ou des comptes comme sensibles pour améliorer les détections. Cette identification impacte de nombreuses détections ATA, telles que la détection des modifications des groupes sensibles et le chemin de mouvement latéral, qui s’appuient sur les groupes et les comptes considérés comme sensibles.

## <a name="performance-improvements"></a>Optimisation des performances

- L’infrastructure du Centre ATA a été améliorée au niveau des performances : la vue de synthèse du trafic permet l’optimisation du pipeline des paquets et du processeur, et réutilise les sockets sur les contrôleurs de domaine pour minimiser les sessions SSL sur ces derniers.



## <a name="additional-changes"></a>Modifications supplémentaires

- Après l’installation d’une nouvelle version d’ATA, l’icône [**Nouveautés**](working-with-ata-console.md) apparaît dans la barre d’outils pour vous indiquer ce qui a été changé dans la dernière version. Elle fournit également un lien vers le journal des modifications détaillé de la version.


## <a name="removed-and-deprecated-features"></a>Fonctionnalités supprimées et déconseillées

- L’alerte de l’**activité suspecte Relation de confiance rompue** a été supprimée.
- L’activité suspecte Mots de passe exposés en texte clair a été supprimée. Elle a été remplacée par le [**rapport Mots de passe exposés en texte clair**](reports.md).



## <a name="see-also"></a>Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Mise à jour d’ATA vers la version 1.9 : guide de migration](ata-update-1.9-migration-guide.md)

