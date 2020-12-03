---
title: Étiquetage des comptes sensibles avec Microsoft Defender pour Identity
description: Explique comment étiqueter les comptes sensibles avec Microsoft Defender pour Identity.
ms.date: 10/27/2020
ms.topic: how-to
ms.openlocfilehash: 2e013b12a73e099d1d3292d77cc3f2ef98706a09
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96542405"
---
# <a name="working-with-sensitive-accounts"></a>Utilisation de comptes sensibles

## <a name="sensitive-entities"></a>Entités sensibles

Les groupes de la liste suivante sont considérés comme **Sensibles** par [!INCLUDE [Product long](includes/product-long.md)]. Toute entité qui est membre d’un de ces groupes est considérée comme sensible :

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
  > Jusqu’en septembre 2018, les utilisateurs du Bureau à distance étaient aussi considérés automatiquement comme Sensibles par [!INCLUDE [Product short](includes/product-short.md)]. Les entités ou les groupes Bureau à distance ajoutés après cette date ne sont plus automatiquement marqués comme sensibles, contrairement aux entités ou groupes Bureau à distance ajoutés avant cette date, qui peuvent rester marqués comme sensibles. Ce paramètre Sensible peut désormais être modifié manuellement.

En plus de ces groupes, [!INCLUDE [Product short](includes/product-short.md)] identifie les serveurs d’actifs de grande valeur suivants et les marque automatiquement comme **Sensibles** :

- Serveur de l’autorité de certification
- Serveur DHCP
- Serveur DNS
- Microsoft Exchange Server

## <a name="tagging-sensitive-accounts"></a>Identification des comptes sensibles

En plus de ces groupes, vous pouvez identifier manuellement des groupes ou des comptes comme sensibles pour améliorer les détections. Ce point est important, car certaines détections [!INCLUDE [Product short](includes/product-short.md)] (par exemple, la détection des modifications des groupes sensibles et les chemins de mouvement latéral) s’appuient sur l’identification des groupes et des comptes sensibles. Vous pouvez marquer manuellement d’autres utilisateurs et groupes comme sensibles (par exemple, les membres du conseil d’administration, les dirigeants de la société ou le directeur des ventes) pour que [!INCLUDE [Product short](includes/product-short.md)] les considère comme sensibles.

1. Sur le portail [!INCLUDE [Product short](includes/product-short.md)], cliquez sur **Configuration**.

1. Sous **Détection**, cliquez sur **Étiquettes d’entité**.

    ![Étiquettes d’entité [!INCLUDE [Product short](includes/product-short.md)]](media/entity-tags.png)

1. Dans la section **Sensible**, tapez le nom des **comptes sensibles** et **groupes sensibles**, puis cliquez sur le signe **+** pour les ajouter.

    ![Exemple de compte sensible [!INCLUDE [Product short](includes/product-short.md)]](media/sensitive-account-sample.png)

1. Cliquez sur **Save**.

## <a name="see-also"></a>Voir aussi

- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
