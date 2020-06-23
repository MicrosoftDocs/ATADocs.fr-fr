---
title: Valider la mise en miroir des ports dans Azure Advanced Threat Protection
description: Explique comment vérifier que la mise en miroir des ports est configurée correctement dans Azure ATP
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 0a56cf27-9eaa-4ad0-ae6c-9d0484c69094
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2fa7214aa4da04641a4f02b9df4de0b768fbbba2
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84775775"
---
# <a name="validate-port-mirroring"></a>Valider la mise en miroir des ports

Cet article s’applique uniquement si vous déployez le capteur autonome Azure ATP à la place du capteur Azure ATP.

> [!NOTE]
> Les capteurs autonomes Azure ATP ne prennent pas en charge la collecte d’entrées de journal du Suivi d’événements pour Windows (ETW) qui fournissent les données pour de nombreuses détections. Pour une couverture complète de votre environnement, nous vous recommandons de déployer le capteur Azure ATP.

Les étapes suivantes sont conçues pour vous guider dans le processus de validation de la mise en miroir des ports. Pour qu’Azure ATP fonctionne correctement, le capteur autonome Azure ATP doit pouvoir voir le trafic entrant et sortant du contrôleur de domaine. La principale source de données utilisée par Azure ATP est l’inspection approfondie des paquets du trafic réseau entrant et sortant de vos contrôleurs de domaine. Pour qu’Azure ATP puisse voir le trafic réseau, vous devez configurer la mise en miroir des ports. La mise en miroir des ports copie le trafic d’un port (le port source) vers un autre port (le port de destination).

## <a name="validate-port-mirroring-using-net-mon"></a>Valider la mise en miroir à l’aide du Moniteur réseau

1. Installez [Moniteur réseau Microsoft 3.4](https://www.microsoft.com/download/details.aspx?id=4865) sur le capteur autonome ATP que vous souhaitez valider.

    > [!IMPORTANT]
    > Si vous choisissez d’installer Wireshark afin de valider la mise en miroir des ports, redémarrez le service du capteur autonome Azure ATP après la validation.

1. Ouvrez le Moniteur réseau et créez un nouvel onglet de capture.

    1. Sélectionnez uniquement la carte réseau **Capture** ou celle qui est connectée au port de commutateur qui est configuré comme le port de destination de la mise en miroir.

    1. Assurez-vous que le mode P est activé.

    1. Cliquez sur **Nouvelle capture**.

        ![Image de la création d’un nouvel onglet de capture](media/atp-port-mirroring-capture.png)

1. Dans la fenêtre Filtre d’affichage, entrez le filtre **KerberosV5 OR LDAP**, puis cliquez sur **Appliquer**.

    ![Image de l’application du filtre KerberosV5 or LDAP](media/atp-port-mirroring-filter-settings.png)

1. Pour démarrer la session de capture, cliquez sur **Démarrer**. Si vous ne voyez pas le trafic entrant et sortant du contrôleur de domaine, examinez la configuration de mise en miroir des ports.

    ![Image du démarrage de la session de capture](media/atp-port-mirroring-capture-traffic.png)

    > [!NOTE]
    > Il est important de vous assurer que vous voyez le trafic entrant et sortant des contrôleurs de domaine.

1. Si vous voyez uniquement le trafic dans un sens, vous devez résoudre ce problème de configuration de la mise en miroir des ports avec l’aide de l’équipe chargée du réseau ou de la virtualisation.

## <a name="see-also"></a>Voir aussi

- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Configurer la mise en miroir des ports](configure-port-mirroring.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
