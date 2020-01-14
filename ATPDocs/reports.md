---
title: Utilisation des rapports Azure ATP | Microsoft Docs
description: Explique comment vous pouvez générer des rapports dans Azure ATP pour surveiller votre réseau.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 11/26/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 76db7841745c7da555caa356808464d9d45b8107
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75907852"
---
# <a name="azure-atp-reports"></a>Rapports Azure ATP

La section Rapports Azure ATP du portail Azure ATP vous permet de planifier ou de générer immédiatement, puis de télécharger des rapports qui fournissent des informations sur l’état du système et des entités. La fonctionnalité de rapports vous permet de créer des rapports sur l’intégrité du système, sur les alertes de sécurité et sur les chemins de mouvement latéral potentiels détectés dans votre environnement.


Pour accéder à la page Rapports, cliquez sur l’icône de rapport dans la barre de menus : ![icône de rapport](./media/atp-report-icon.png).
Les rapports disponibles sont les suivants : 

- **Rapport de synthèse** : ce rapport présente un tableau de bord de l’état dans le système. Vous pouvez afficher trois onglets : un pour un **résumé** de ce qui a été détecté sur votre réseau, un pour les **activités suspectes ouvertes** qui répertorie les activités suspectes nécessitant votre attention, et un pour les **problèmes d’intégrité ouverts** qui répertorie les problèmes d’intégrité Azure ATP nécessitant votre attention. Les activités suspectes répertoriées sont regroupées par type, tout comme les problèmes d’intégrité. 

- **Modification de groupes sensibles** : ce rapport liste toutes les modifications apportées aux groupes sensibles (comme les administrateurs ou les comptes et groupes étiquetés manuellement). Si vous utilisez des capteurs autonomes Azure ATP pour recevoir un rapport complet sur vos groupes sensibles, vérifiez que [les événements sont transférés de vos contrôleurs de domaine vers les capteurs autonomes](configure-event-forwarding.md). 

- **Mots de passe exposés en texte clair** : certains services utilisent le protocole LDAP non sécurisé pour envoyer des informations d’identification de compte en texte brut, y compris pour des comptes sensibles. Les attaquants qui surveillent le trafic réseau peuvent intercepter ces informations d’identification et les réutiliser à des fins malveillantes. Ce rapport liste tous les mots de passe de compte et d’ordinateur source dont Azure ATP a détecté qu’ils étaient envoyés en texte clair. 

- **Chemins d’accès par mouvement latéral aux comptes sensibles** : ce rapport liste les comptes sensibles exposés au moyen de chemins d’accès par mouvement latéral. Pour plus d’informations, consultez [Chemins de mouvement latéral](use-case-lateral-movement-path.md). Ce rapport collecte les chemins de mouvement latéral potentiels qui ont été détectés dans la période de rapport que vous sélectionnez. 

Il existe deux façons de générer un rapport : à la demande ou en planifiant un rapport à envoyer périodiquement à votre adresse e-mail.

Pour générer un rapport à la demande :

1. Dans la barre de menus du portail Azure ATP, cliquez sur l’icône Rapport : ![icône de rapport](./media/atp-report-icon.png).

2. Sous le type de rapport sélectionné, définissez les dates **De** et **À**, puis cliquez sur **Télécharger**. 
 ![rapports](./media/reports.png)

Pour définir un rapport planifié :
 
1. Dans la page **Rapports**, cliquez sur **Définir les rapports planifiés** ou, dans la page de configuration du portail Azure ATP, sous Notifications et rapports, cliquez sur **Rapports planifiés**.

   ![Planification de rapports](./media/atp-sched-reports.png)
 
   > [!NOTE]
   > Par défaut, les rapports quotidiens sont conçus pour être envoyés quelques instants après minuit, heure UTC. Choisissez votre heure via l’option prévue à cet effet. 

2. Cliquez sur **Planifier** en regard de votre type de rapport sélectionné pour définir la fréquence et l’adresse e-mail pour la remise des rapports. La fréquence des rapports que vous sélectionnez détermine les informations incluses dans le rapport. Pour ajouter des adresses e-mail, cliquez sur le signe Plus en regard du champ d’adresse e-mail, entrez l’adresse et cliquez sur **Enregistrer**.

   ![Planifier la fréquence et l’adresse e-mail des rapports](./media/sched-report1.png)


## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
