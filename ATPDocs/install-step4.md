---
title: Guide de démarrage rapide pour l’installation du capteur Microsoft Defender pour Identity
description: L’étape 4 de l’installation de Microsoft Defender pour Identity vous aide à installer le capteur Defender pour Identity.
author: shsagir
ms.author: shsagir
ms.date: 10/26/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f03f2722f86cec0ca019828b21e4851d0b1305f8
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847885"
---
# <a name="quickstart-install-the-product-long-sensor"></a>Démarrage rapide : Installer le capteur [!INCLUDE [Product long](includes/product-long.md)]

Dans ce guide de démarrage rapide, vous allez installer le capteur [!INCLUDE [Product long](includes/product-long.md)] sur un contrôleur de domaine. Si vous préférez une installation sans assistance, consultez l’article [Installation sans assistance](silent-installation.md).

## <a name="prerequisites"></a>Prérequis

- Une [instance [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md) qui est [connectée à Active Directory](install-step2.md).
- Une copie téléchargée de votre [package d’installation du capteur [!INCLUDE [Product short](includes/product-short.md)]](install-step3.md) et la clé d’accès.
- Vérifiez que Microsoft .NET Framework 4.7 (ou version ultérieure) est installé sur l’ordinateur. Si Microsoft .NET Framework 4.7 (ou version ultérieure) n’est pas installé, le package d’installation du capteur [!INCLUDE [Product short](includes/product-short.md)] l’installe, ce qui peut nécessiter un redémarrage du serveur.

## <a name="install-the-sensor"></a>Installer le capteur

Effectuez les opérations suivantes sur le contrôleur de domaine.

1. Vérifiez que l’ordinateur dispose d’une connectivité au(x) point(s) de terminaison approprié(s) du [service cloud [!INCLUDE [Product short](includes/product-short.md)]](configure-proxy.md#enable-access-to-azure-atp-service-urls-in-the-proxy-server) :
1. Extrayez les fichiers d’installation à partir du fichier zip. L’installation directe à partir du fichier zip est vouée à l’échec.
1. Exécutez **Azure ATP sensor setup.exe**, puis suivez les instructions de l’Assistant Installation.
1. Dans la page **Bienvenue**, sélectionnez votre langue, puis cliquez sur **Suivant**.

    ![Langage d’installation du capteur autonome [!INCLUDE [Product short](includes/product-short.md)]](media/sensor-install-language.png)

1. L’Assistant Installation vérifie automatiquement si le serveur est un contrôleur de domaine ou un serveur dédié. S’il s’agit d’un contrôleur de domaine, le capteur [!INCLUDE [Product short](includes/product-short.md)] est installé. S’il s’agit d’un serveur dédié, le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] est installé.

    Par exemple, pour un capteur [!INCLUDE [Product short](includes/product-short.md)], l’écran suivant s’affiche pour vous informer qu’un capteur [!INCLUDE [Product short](includes/product-short.md)] est installé sur votre serveur dédié :

    ![Installation du capteur [!INCLUDE [Product short](includes/product-short.md)]](media/sensor-install-deployment-type.png)

    Cliquez sur **Suivant**.

    > [!NOTE]
    > Un avertissement s’affiche si le contrôleur de domaine ou le serveur dédié ne présente pas la configuration matérielle minimale requise pour l’installation. Cet avertissement ne vous empêche pas de cliquer sur **Suivant** et d’effectuer l’installation. Cela peut être le bon choix pour installer [!INCLUDE [Product short](includes/product-short.md)] dans un petit environnement de test de laboratoire qui nécessite moins de place pour le stockage des données. Pour les environnements de production, nous vous recommandons fortement de respecter le guide de [planification de la capacité](capacity-planning.md) [!INCLUDE [Product short](includes/product-short.md)] pour vous assurer que vos contrôleurs de domaine ou serveurs dédiés répondent aux conditions requises.

1. Sous **Configurer le capteur**, entrez le chemin d’installation et la clé d’accès que vous avez copiée à l’étape précédente, en fonction de votre environnement :

    ![Image de configuration du capteur [!INCLUDE [Product short](includes/product-short.md)]](media/sensor-install-config.png)

    - Chemin d’installation : Emplacement où le capteur [!INCLUDE [Product short](includes/product-short.md)] est installé. Par défaut, le chemin est %programfiles%\Azure Advanced Threat Protection sensor. Conservez la valeur par défaut.
    - Clé d’accès : Récupérée auprès du portail [!INCLUDE [Product short](includes/product-short.md)] à l’étape précédente.

1. Cliquez sur **Installer**. Les composants suivants sont installés et configurés pendant l’installation du capteur [!INCLUDE [Product short](includes/product-short.md)] :

    - KB 3047154 (pour Windows Server 2012 R2 uniquement)

        > [!IMPORTANT]
        >
        > - N’installez pas le correctif KB 3047154 sur un hôte de virtualisation (l’hôte responsable de la virtualisation, que vous pouvez exécuter sur une machine virtuelle), car cela pourrait nuire au bon fonctionnement de la mise en miroir des ports.
        > - Si Wireshark est installé sur l’ordinateur du capteur [!INCLUDE [Product short](includes/product-short.md)], après avoir exécuté Wireshark, vous devez redémarrer le capteur [!INCLUDE [Product short](includes/product-short.md)], car il utilise les mêmes pilotes.

    - Service de capteur [!INCLUDE [Product short](includes/product-short.md)] et service de mise à jour du capteur [!INCLUDE [Product short](includes/product-short.md)]
    - Microsoft Visual C++ 2013 Redistributable

## <a name="next-steps"></a>Étapes suivantes

Le capteur [!INCLUDE [Product short](includes/product-short.md)] est conçu pour avoir un impact minimal sur les ressources de votre contrôleur de domaine et sur l’activité réseau. Pour créer une évaluation des performances, consultez [Planifier la capacité pour [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md).

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter de [!INCLUDE [Product short](includes/product-short.md)] et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity) !
