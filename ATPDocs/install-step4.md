---
title: 'Démarrage rapide : Installer le capteur Azure ATP'
description: La quatrième étape de la procédure d’installation d’Azure ATP vous permet d’installer le capteur Azure ATP.
author: shsagir
ms.author: shsagir
ms.date: 07/29/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d82468ef075c61de9709ce251a04e9d19fb797cb
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90826776"
---
# <a name="quickstart-install-the-azure-atp-sensor"></a>Démarrage rapide : Installer le capteur Azure ATP

Dans ce guide de démarrage rapide, vous allez installer le capteur Azure ATP sur un contrôleur de domaine. Si vous préférez une installation sans assistance, consultez l’article [Installation sans assistance](silent-installation.md).

## <a name="prerequisites"></a>Prérequis

- Une [instance Azure ATP](install-step1.md) qui est [connectée à Active Directory](install-step2.md).
- Une copie téléchargée de votre [package d’installation du capteur ATP](install-step3.md) et la clé d’accès.
- Vérifiez que Microsoft .NET Framework 4.7 (ou version ultérieure) est installé sur l’ordinateur. Si Microsoft .NET Framework 4.7 (ou version ultérieure) n’est pas installé, le package d’installation du capteur Azure ATP l’installe, ce qui peut nécessiter un redémarrage du serveur.

## <a name="install-the-sensor"></a>Installer le capteur

Effectuez les opérations suivantes sur le contrôleur de domaine.

1. Vérifiez que l’ordinateur dispose d’une connectivité au(x) point(s) de terminaison approprié(s) du [service cloud Azure ATP](configure-proxy.md#enable-access-to-azure-atp-service-urls-in-the-proxy-server) :
1. Extrayez les fichiers d’installation à partir du fichier zip. L’installation directe à partir du fichier zip est vouée à l’échec.
1. Exécutez **Azure ATP sensor setup.exe**, puis suivez les instructions de l’Assistant Installation.
1. Dans la page **Bienvenue**, sélectionnez votre langue, puis cliquez sur **Suivant**.

    ![Langue d’installation du capteur autonome Azure ATP](media/sensor-install-language.png)

1. L’Assistant Installation vérifie automatiquement si le serveur est un contrôleur de domaine ou un serveur dédié. S’il s’agit d’un contrôleur de domaine, le capteur Azure ATP est installé. S’il s’agit d’un serveur dédié, le capteur autonome Azure ATP est installé.

    Par exemple, pour un capteur Azure ATP, l’écran suivant s’affiche pour vous informer qu’un capteur Azure ATP est installé sur votre serveur dédié :

    ![Installation du capteur Azure ATP](media/sensor-install-deployment-type.png)

    Cliquez sur **Suivant**.

    > [!NOTE]
    > Un avertissement s’affiche si le contrôleur de domaine ou le serveur dédié ne présente pas la configuration matérielle minimale requise pour l’installation. Cet avertissement ne vous empêche pas de cliquer sur **Suivant** et d’effectuer l’installation. Cela peut être le bon choix pour installer Azure ATP dans un petit environnement de test de laboratoire qui nécessite moins de place pour le stockage des données. Pour les environnements de production, nous vous recommandons vivement de respecter le guide de [planification de la capacité](capacity-planning.md) d’Azure ATP pour vous assurer que vos contrôleurs de domaine ou serveurs dédiés répondent aux conditions requises.

1. Sous **Configurer le capteur**, entrez le chemin d’installation et la clé d’accès que vous avez copiée à l’étape précédente, en fonction de votre environnement :

    ![Image de la configuration du capteur Azure ATP](media/sensor-install-config.png)

    - Chemin d’installation : Emplacement où le capteur Azure ATP est installé. Par défaut, le chemin est %programfiles%\Azure Advanced Threat Protection sensor. Conservez la valeur par défaut.
    - Clé d’accès : Récupérée auprès du portail Azure ATP à l’étape précédente.

1. Cliquez sur **Suivant**. Les composants suivants sont installés et configurés pendant l’installation du capteur Azure ATP :

    - KB 3047154 (pour Windows Server 2012 R2 uniquement)

        > [!IMPORTANT]
        >
        > - N’installez pas le correctif KB 3047154 sur un hôte de virtualisation (l’hôte responsable de la virtualisation, que vous pouvez exécuter sur une machine virtuelle), car cela pourrait nuire au bon fonctionnement de la mise en miroir des ports.
        > - Si Wireshark est installé sur l’ordinateur du capteur ATP, après avoir exécuté Wireshark, vous devez redémarrer le capteur ATP, car il utilise les mêmes pilotes.

    - Service de capteur Azure ATP et service de mise à jour du capteur Azure ATP
    - Microsoft Visual C++ 2013 Redistributable

## <a name="next-steps"></a>Étapes suivantes

Le capteur Azure ATP est conçu pour avoir un impact minimal sur les ressources de votre contrôleur de domaine et sur l’activité réseau. Pour créer une évaluation des performances, consultez [Planifier la capacité pour Azure ATP](capacity-planning.md).

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://aka.ms/azureatpcommunity) dès aujourd’hui !