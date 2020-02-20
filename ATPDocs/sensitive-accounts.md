---
title: Identifier des comptes sensibles avec Azure ATP | Microsoft Docs
description: Décrit comment identifier des comptes sensibles à l’aide d’Azure Advanced Threat Protection (ATP)
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cf29a41139973742d6a1be96643104e1cfad0703
ms.sourcegitcommit: 173b9fc26592efec2113c6ee585b04311ddfdbf1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2020
ms.locfileid: "77422011"
---
# <a name="working-with-sensitive-accounts"></a>Utilisation de comptes sensibles

## <a name="sensitive-entities"></a>Entités sensibles

Les groupes de la liste suivante sont considérés comme **Sensibles** par Azure ATP. Toute entité qui est membre d’un de ces groupes est considérée comme sensible :

- Administrateurs
- Utilisateurs avec pouvoir
- Opérateurs de compte
- Opérateurs de serveur
- Opérateurs d'impression
- Opérateurs de sauvegarde
- Duplicateurs
- Opérateurs de configuration réseau
- Générateurs d’approbation de forêt entrante
- Administrateurs du domaine
- Contrôleurs de domaine
- Propriétaires créateurs de la stratégie de groupe
- Contrôleurs de domaine en lecture seule
- Contrôleurs de domaine d’entreprise en lecture seule
- Administrateurs du schéma
- Administrateurs de l’entreprise
- Serveurs Microsoft Exchange

  > [!NOTE]
  > Jusqu’à septembre 2018, les utilisateurs du Bureau à distance étaient aussi considérés automatiquement comme sensibles par Azure ATP. Les entités ou les groupes Bureau à distance ajoutés après cette date ne sont plus automatiquement marqués comme sensibles, contrairement aux entités ou groupes Bureau à distance ajoutés avant cette date, qui peuvent rester marqués comme sensibles. Ce paramètre Sensible peut désormais être modifié manuellement.

En plus de ces groupes, Azure ATP identifie les serveurs actifs de grande valeur suivants et les marque automatiquement comme **Sensibles** :

- Serveur de l’autorité de certification
- Serveur DHCP
- Serveur DNS
- Microsoft Exchange Server

## <a name="tagging-sensitive-accounts"></a>Identification des comptes sensibles

En plus de ces groupes, vous pouvez identifier manuellement des groupes ou des comptes comme sensibles pour améliorer les détections. C’est important car certaines détections Azure ATP, telles que la détection des modifications des groupes sensibles et les chemins de mouvement latéral, s’appuient sur des groupes et des comptes considérés comme sensibles. Vous pouvez identifier manuellement d’autres utilisateurs ou groupes comme sensibles, tels que les membres du conseil d’administration, les cadres de la société, le directeur des ventes, etc., pour qu’Azure ATP les considère comme sensibles.

1. Dans le portail Azure ATP, cliquez sur l’icône d’engrenage **Configuration** dans la barre de menus.

1. Sous **Détection**, cliquez sur **Étiquettes d’entité**.

    ![Étiquettes d’entité Azure ATP](media/entity-tags.png)

1. Dans la section **Sensible**, tapez le nom des **comptes sensibles** et **groupes sensibles**, puis cliquez sur le signe **+** pour les ajouter.

    ![Exemple de compte sensible Azure ATP](media/sensitive-account-sample.png)

1. Cliquez sur **Save**.

## <a name="see-also"></a>Voir aussi

- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
