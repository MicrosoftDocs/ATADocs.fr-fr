---
title: Identifier des comptes sensibles avec Azure ATP | Microsoft Docs
description: Décrit comment identifier des comptes sensibles à l’aide d’Azure - Protection avancée contre les menaces (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b8b48b8090e109c9fc23c52b05f986b34e2549eb
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44165879"
---
*S’applique à : Azure Advanced Threat Protection*



# <a name="working-with-sensitive-accounts"></a>Utilisation de comptes sensibles

## <a name="sensitive-groups"></a>Groupes sensibles

Les groupes de la liste suivante sont considérés comme sensibles par Azure ATP. Une entité qui est membre de ces groupes est considérée comme sensible :

-   Administrateurs
-   Utilisateurs avec pouvoir
-   Opérateurs de compte
-   Opérateurs de serveur
-   Opérateurs d'impression
-   Opérateurs de sauvegarde
-   Duplicateurs
-   Utilisateurs du Bureau à distance 
-   Opérateurs de configuration réseau 
-   Générateurs d’approbation de forêt entrante
-   Administrateurs du domaine
-   Contrôleurs de domaine
-   Propriétaires créateurs de la stratégie de groupe 
-   Contrôleurs de domaine en lecture seule 
-   Contrôleurs de domaine d’entreprise en lecture seule 
-   Administrateurs du schéma 
-   Administrateurs de l’entreprise


## <a name="tagging-sensitive-accounts"></a>Identification des comptes sensibles

En plus de ces groupes, vous pouvez identifier manuellement des groupes ou des comptes comme sensibles pour améliorer les détections. C’est important car certaines détections Azure ATP, telles que la détection des modifications des groupes sensibles et le chemin de mouvement latéral, s’appuient sur les groupes et les comptes considérés comme sensibles. Vous pouvez identifier manuellement d’autres utilisateurs ou groupes comme sensibles, tels que les membres du conseil d’administration, les cadres de la société, le directeur des ventes, etc., pour qu’Azure ATP les considère comme sensibles.

1.  Dans le portail d’espace de travail Azure ATP, cliquez sur l’icône de **configuration** (roue dentée) dans la barre de menus.

2.  Sous **Détection**, cliquez sur **Étiquettes d’entité**.

    ![Étiquettes d’entité Azure ATP](media/entity-tags.png)

3.  Dans la section **Sensible**, tapez le nom des **comptes sensibles** et **groupes sensibles**, puis cliquez sur le signe **+** pour les ajouter.

    ![Exemple de compte sensible Azure ATP](media/sensitive-account-sample.png)

4. Cliquez sur **Save**.

    
## <a name="see-also"></a>Voir aussi

- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)