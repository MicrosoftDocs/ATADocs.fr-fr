---
title: Rapports Microsoft Defender pour Identity
description: Explique comment générer des rapports dans Microsoft Defender pour Identity afin de superviser le réseau.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 68c129e0c92c369bb666483dc17013c54a84e282
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94849041"
---
# <a name="product-long-reports"></a>Rapports [!INCLUDE [Product long](includes/product-long.md)]

La section Rapports [!INCLUDE [Product long](includes/product-long.md)] du portail [!INCLUDE [Product short](includes/product-short.md)] vous permet de planifier ou de générer et de télécharger immédiatement des rapports qui donnent des informations sur l’état du système et des entités. La fonctionnalité de rapports vous permet de créer des rapports sur l’intégrité du système, sur les alertes de sécurité et sur les chemins de mouvement latéral potentiels détectés dans votre environnement.

Pour accéder à la page Rapports, cliquez sur l’icône de rapport dans la barre de menus : ![icône de rapport](media/report-icon.png).
Les rapports disponibles sont les suivants :

- **Rapport de synthèse** : ce rapport présente un tableau de bord de l’état dans le système. Il comporte trois onglets : **Résumé** qui synthétise les événements détectés sur votre réseau, **Activités suspectes ouvertes** qui liste les activités suspectes à traiter et **Problèmes d’intégrité ouverts** qui répertorie les problèmes d’intégrité [!INCLUDE [Product short](includes/product-short.md)] à traiter. Les activités suspectes répertoriées sont regroupées par type, tout comme les problèmes d’intégrité.

- **Modification de groupes sensibles** : ce rapport liste toutes les modifications apportées aux groupes sensibles (comme les administrateurs ou les comptes et groupes étiquetés manuellement). Si vous utilisez des capteurs autonomes [!INCLUDE [Product short](includes/product-short.md)], vérifiez que [les événements sont transférés de vos contrôleurs de domaine aux capteurs autonomes](configure-event-forwarding.md) pour recevoir un rapport complet sur vos groupes sensibles.

- **Mots de passe exposés en texte clair** : certains services utilisent le protocole LDAP non sécurisé pour envoyer des informations d’identification de compte en texte brut, y compris pour des comptes sensibles. Les attaquants qui surveillent le trafic réseau peuvent intercepter ces informations d’identification et les réutiliser à des fins malveillantes. Ce rapport liste tous les mots de passe de compte et d’ordinateur source dont [!INCLUDE [Product short](includes/product-short.md)] a détecté qu’ils étaient envoyés en texte clair.

- **Chemins d’accès par mouvement latéral aux comptes sensibles** : ce rapport liste les comptes sensibles exposés au moyen de chemins d’accès par mouvement latéral. Pour plus d’informations, consultez [Chemins de mouvement latéral](use-case-lateral-movement-path.md). Ce rapport collecte les chemins de mouvement latéral potentiels qui ont été détectés dans la période de rapport que vous sélectionnez.

Il existe deux façons de générer un rapport : à la demande ou en planifiant un rapport à envoyer périodiquement à votre adresse e-mail.

Pour générer un rapport à la demande :

1. Dans la barre de menus du portail [!INCLUDE [Product short](includes/product-short.md)], cliquez sur l’icône Rapport ![icône Rapport](media/report-icon.png).

1. Sous le type de rapport sélectionné, définissez les dates **De** et **À**, puis cliquez sur **Télécharger**.
 ![Capture d’écran montrant le téléchargement du rapport](media/reports.png)

Pour définir un rapport planifié :

1. Cliquez sur **Définir les rapports planifiés** sur la page **Rapports**, ou sur **Rapports planifiés** sous Notifications et rapports sur la page de configuration du portail [!INCLUDE [Product short](includes/product-short.md)].

    ![Planification de rapports](media/sched-reports.png)

    > [!NOTE]
    > Par défaut, les rapports quotidiens sont conçus pour être envoyés quelques instants après minuit, heure UTC. Choisissez votre heure via l’option prévue à cet effet.

1. Cliquez sur **Planifier** en regard de votre type de rapport sélectionné pour définir la fréquence et l’adresse e-mail pour la remise des rapports. La fréquence des rapports que vous sélectionnez détermine les informations incluses dans le rapport. Pour ajouter des adresses e-mail, cliquez sur le signe Plus en regard du champ d’adresse e-mail, entrez l’adresse et cliquez sur **Enregistrer**.

    ![Planifier la fréquence et l’adresse e-mail des rapports](media/sched-report1.png)

## <a name="see-also"></a>Voir aussi

- [Prérequis de [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Planification de capacité [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
