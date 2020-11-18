---
title: Validation de la mise en miroir de ports dans Microsoft Defender pour Identity
description: Explique comment vérifier que la mise en miroir de ports est configurée correctement dans Microsoft Defender pour Identity.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a6b3a3ef5d16a3e92a4bcf6a8d52d96c9c4036ce
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94846729"
---
# <a name="validate-port-mirroring"></a>Valider la mise en miroir des ports

Cet article ne s’applique que dans le cadre du déploiement du capteur autonome [!INCLUDE [Product long](includes/product-long.md)] plutôt que du capteur [!INCLUDE [Product short](includes/product-short.md)].

> [!NOTE]
> Les capteurs autonomes [!INCLUDE [Product short](includes/product-short.md)] ne prennent pas en charge la collecte d’entrées de journal du Suivi d’événements pour Windows (ETW) qui fournissent les données pour de nombreuses détections. Pour une couverture complète de votre environnement, nous vous recommandons de déployer le capteur [!INCLUDE [Product short](includes/product-short.md)].

Les étapes suivantes sont conçues pour vous guider dans le processus de validation de la mise en miroir des ports. Pour que [!INCLUDE [Product short](includes/product-short.md)] fonctionne correctement, le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] doit pouvoir voir le trafic entrant et sortant du contrôleur de domaine. La principale source de données utilisée par [!INCLUDE [Product short](includes/product-short.md)] est l’inspection approfondie des paquets du trafic réseau entrant et sortant des contrôleurs de domaine. Pour que [!INCLUDE [Product short](includes/product-short.md)] puisse voir le trafic réseau, vous devez configurer la mise en miroir de ports. La mise en miroir des ports copie le trafic d’un port (le port source) vers un autre port (le port de destination).

## <a name="validate-port-mirroring-using-net-mon"></a>Valider la mise en miroir à l’aide du Moniteur réseau

1. Installez [Moniteur réseau Microsoft 3.4](https://www.microsoft.com/download/details.aspx?id=4865) sur le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] que vous souhaitez valider.

    > [!IMPORTANT]
    > Si vous choisissez d’installer Wireshark pour valider la mise en miroir de ports, redémarrez le service du capteur autonome [!INCLUDE [Product short](includes/product-short.md)] après la validation.

1. Ouvrez le Moniteur réseau et créez un nouvel onglet de capture.

    1. Sélectionnez uniquement la carte réseau **Capture** ou celle qui est connectée au port de commutateur qui est configuré comme le port de destination de la mise en miroir.

    1. Assurez-vous que le mode P est activé.

    1. Cliquez sur **Nouvelle capture**.

        ![Image de la création d’un nouvel onglet de capture](media/port-mirroring-capture.png)

1. Dans la fenêtre Filtre d’affichage, entrez le filtre **KerberosV5 OR LDAP**, puis cliquez sur **Appliquer**.

    ![Image de l’application du filtre KerberosV5 or LDAP](media/port-mirroring-filter-settings.png)

1. Pour démarrer la session de capture, cliquez sur **Démarrer**. Si vous ne voyez pas le trafic entrant et sortant du contrôleur de domaine, examinez la configuration de mise en miroir des ports.

    ![Image du démarrage de la session de capture](media/port-mirroring-capture-traffic.png)

    > [!NOTE]
    > Il est important de vous assurer que vous voyez le trafic entrant et sortant des contrôleurs de domaine.

1. Si vous voyez uniquement le trafic dans un sens, vous devez résoudre ce problème de configuration de la mise en miroir des ports avec l’aide de l’équipe chargée du réseau ou de la virtualisation.

## <a name="see-also"></a>Voir aussi

- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Configurer la mise en miroir des ports](configure-port-mirroring.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
