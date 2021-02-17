---
title: Gérer les comptes sensibles ou honeytoken avec Microsoft Defender pour l’identité
description: Décrit comment gérer les comptes sensibles ou honeytoken à l’aide de Microsoft Defender pour l’identité
ms.date: 02/17/2021
ms.topic: how-to
ms.openlocfilehash: 7078e93ad384d81d59a13ff4b527ca59bc678ad2
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630764"
---
# <a name="manage-sensitive-or-honeytoken-accounts"></a>Gérer les comptes sensibles ou honeytoken

Cet article explique comment appliquer des balises d’entité aux comptes sensibles. Cela est important, car certaines [!INCLUDE [Short long](includes/product-short.md)] détections, telles que la détection des modifications de groupes sensibles et le chemin de mouvement latéral, s’appuient sur l’état de sensibilité d’une entité.

[!INCLUDE [Product short](includes/product-short.md)] active également la configuration des comptes honeytoken, qui sont utilisés comme interruptions pour les acteurs malveillants. toute authentification associée à ces comptes honeytoken (normalement dormant) déclenche une alerte.

## <a name="sensitive-entities"></a>Entités sensibles

Les groupes de la liste suivante sont considérés comme **Sensibles** par [!INCLUDE [Short long](includes/product-short.md)]. Toute entité qui est membre de l’un de ces groupes de Azure Active Directory est considérée comme sensible :

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

## <a name="manually-tagging-entities"></a>Balisage manuel des entités

Vous pouvez également étiqueter manuellement les entités en tant que comptes sensibles ou honeytoken. Si vous étiquetez manuellement des utilisateurs ou des groupes supplémentaires, tels que les membres du tableau, les cadres de l’entreprise et les directeurs des ventes, [!INCLUDE [Product short](includes/product-short.md)] les considéreront comme sensibles.

### <a name="to-manually-tag-entities"></a>Pour baliser manuellement des entités

Pour baliser des entités, procédez comme suit :

1. Sur le portail [!INCLUDE [Product short](includes/product-short.md)], cliquez sur **Configuration**.

    ![[! INCLUDe [Product Short] (includes/Product-Short. MD)] paramètres de configuration](media/config-menu.png)

1. Sous **détection**, sélectionnez **étiquettes d’entité**.

    ![Étiquettes d’entité [!INCLUDE [Product short](includes/product-short.md)]](media/entity-tags.png)

1. Pour chaque compte que vous souhaitez configurer, procédez comme suit :
    1. Sous **comptes Honeytoken** ou **sensibles**, entrez le nom du compte.
    1. Cliquez sur l’icône plus **(+)**.

    > [!TIP]
    > Le champ compte sensible ou honeytoken peut faire l’objet d’une recherche et sera automatiquement renseigné avec les entités de votre réseau.

    ![Exemple de compte sensible [!INCLUDE [Product short](includes/product-short.md)]](media/sensitive-account-sample.png)

1. Cliquez sur **Save**.

## <a name="see-also"></a>Voir aussi

- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
