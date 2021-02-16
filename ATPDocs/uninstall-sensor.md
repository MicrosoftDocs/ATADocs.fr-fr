---
title: Désinstaller Microsoft Defender pour le capteur d’identité
description: Cet article explique comment désinstaller le capteur d’identité Microsoft Defender pour les contrôleurs de domaine.
ms.date: 12/22/2020
ms.topic: how-to
ms.openlocfilehash: 4d93637cabc0169efa0c3d62b4342578c4f006e1
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533339"
---
# <a name="uninstall-the-microsoft-defender-for-identity-sensor"></a>Désinstaller Microsoft Defender pour le capteur d’identité

Cet article explique comment désinstaller le [!INCLUDE [Product long](includes/product-long.md)] capteur des contrôleurs de domaine pour les scénarios suivants :

1. Désinstaller un capteur d’un contrôleur de domaine
1. Supprimer un capteur orphelin
1. Supprimer un capteur dupliqué

## <a name="uninstall-a-sensor-from-a-domain-controller"></a>Désinstaller un capteur d’un contrôleur de domaine

Les étapes suivantes décrivent comment désinstaller un capteur d’un contrôleur de domaine.

1. Connectez-vous au contrôleur de domaine avec des privilèges d’administrateur local.
1. Dans le menu **Démarrer** de Windows, cliquez sur Paramètres Panneau de **configuration**  >    >  **Ajout/suppression de programmes**.
1. Sélectionnez l’installation du capteur, cliquez sur **désinstaller**, puis suivez les instructions pour supprimer le capteur.

## <a name="remove-an-orphaned-sensor"></a>Supprimer un capteur orphelin

Ce scénario peut se produire lorsqu’un contrôleur de domaine a été supprimé sans avoir préalablement désinstallé le capteur, et le capteur apparaît toujours dans le [!INCLUDE [Product short](includes/product-short.md)] portail.

1. Dans le [!INCLUDE [Product short](includes/product-short.md)] portail, accédez à **configuration** et, sous la section **système** , sélectionnez **capteurs**.
1. Recherchez le capteur orphelin et, à la fin de la ligne, cliquez sur **supprimer** (icône Corbeille).

    ![Supprimer les [ ! INCLUDe [Product Short] (includes/Product-Short. MD)] capteur à partir de la page des capteurs](media/delete-orphaned-sensor.png)

## <a name="remove-a-duplicate-sensor"></a>Supprimer un capteur dupliqué

Ce scénario peut se produire après une mise à niveau de capteur sur place et le capteur apparaît deux fois dans le [!INCLUDE [Product short](includes/product-short.md)] portail.

1. Dans le [!INCLUDE [Product short](includes/product-short.md)] portail, accédez à **configuration** et, sous la section **système** , sélectionnez **capteurs**.
1. Recherchez le capteur orphelin et, à la fin de la ligne, cliquez sur **supprimer** (icône Corbeille).

## <a name="see-also"></a>Voir aussi

- [Désinstaller le [!INCLUDE [Product short](includes/product-short.md)] capteur en mode silencieux](silent-installation.md#silently-uninstall-sensor)
