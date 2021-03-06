---
title: Baliser les comptes sensibles avec ATA
description: Décrit comment identifier des comptes sensibles à l’aide d’Advanced Threat Analytics (ATA)
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 40a1c5c4-b8d6-477c-8ae5-562b37661624
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e80eeda17fa458f994a9e637cd95362601ffd89a
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690123"
---
# <a name="tag-sensitive-accounts"></a>Identifier des comptes sensibles


[!INCLUDE [Banner for top of topics](includes/banner.md)]

Vous pouvez identifier manuellement des groupes ou des comptes comme sensibles pour améliorer les détections. C’est important que ces informations soient à jour, car certaines détections ATA, comme la détection des modifications des groupes sensibles et le chemin de mouvement latéral, s’appuient sur les groupes et les comptes considérés comme sensibles. Avant, ATA considérait automatiquement une entité comme *sensible* s’il s’agissait d’un membre d’une liste spécifique de groupes. À présent, vous pouvez identifier manuellement d’autres utilisateurs ou groupes comme sensibles, tels que les membres du conseil d’administration, les cadres de la société, le directeur des ventes, etc., pour qu’ATA les considère comme sensibles.

1. Dans la console ATA, cliquez sur l’icône de **configuration** (roue dentée) dans la barre de menus.

1. Sous **détection,** cliquez sur **étiquettes d’entité**.

    ![Étiquettes d’entité ATA](media/entity-tags.png)

1. Dans la section **Sensible**, tapez le nom des **comptes sensibles** et **groupes sensibles**, puis cliquez sur le signe **+** pour les ajouter.

    ![Exemple de compte sensible ATA](media/sensitive-account-sample.png)

1. Cliquez sur **Enregistrer**.

1. Accédez à la page de profil d’entité en cliquant sur le nom de l’entité. Ici, vous serez en mesure de voir pourquoi l’entité est considérée comme sensible - parce qu’elle appartient à un groupe ou qu’elle a été marquée comme sensible manuellement.


## <a name="sensitive-groups"></a>Groupes sensibles

Les groupes de la liste suivante sont considérés comme sensibles par ATA. Une entité qui est membre de ces groupes est considérée comme sensible :

- Administrateurs
- Utilisateurs avec pouvoir
- Opérateurs de compte
- Opérateurs de serveur
- Opérateurs d'impression
- Opérateurs de sauvegarde
- Duplicateurs
- Utilisateurs du Bureau à distance 
- Opérateurs de configuration réseau 
- Générateurs d’approbation de forêt entrante
- Administrateurs du domaine
- Contrôleurs de domaine
- Propriétaires créateurs de la stratégie de groupe 
- Contrôleurs de domaine en lecture seule 
- Contrôleurs de domaine d’entreprise en lecture seule 
- Administrateurs du schéma 
- Administrateurs de l’entreprise
     
## <a name="see-also"></a>Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
