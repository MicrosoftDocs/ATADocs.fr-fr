---
title: Utilisation des rapports Azure ATP | Microsoft Docs
description: Explique comment vous pouvez générer des rapports dans Azure ATP pour surveiller votre réseau.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/27/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8d9c7f9208ce76e6c2ca915729b9c64f769ae7bd
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
ms.locfileid: "30202287"
---
*S’applique à : Azure - Protection avancée contre les menaces*


# <a name="azure-atp-reports"></a>Rapports Azure ATP

La section Rapports Azure ATP du portail d’espace de travail vous permet de générer des rapports contenant des informations sur l’état du système, sur l’intégrité du système et sur les activités suspectes détectées dans votre environnement.


Pour accéder à la page Rapports, cliquez sur l’icône de rapport dans la barre de menus : ![icône de rapport](./media/atp-report-icon.png).
Les rapports disponibles sont : 

- **Rapport de synthèse** : ce rapport présente un tableau de bord de l’état dans le système. Vous pouvez afficher trois onglets : un pour un **résumé** de ce qui a été détecté sur votre réseau, un pour les **activités suspectes ouvertes** qui répertorie les activités suspectes nécessitant votre attention, et un pour les **problèmes d’intégrité ouverts** qui répertorie les problèmes d’intégrité Azure ATP nécessitant votre attention. Les activités suspectes répertoriées sont regroupées par type, tout comme les problèmes d’intégrité. 

- **Modification des groupes sensibles** : ce rapport répertorie toutes les modifications apportées à des groupes sensibles (comme les administrateurs, ou les comptes et groupes manuellement balisés). Si vous utilisez des capteurs autonomes Azure ATP, pour recevoir un rapport complet sur vos groupes sensibles, vous devez vous assurer que [les événements sont transférés de vos contrôleurs de domaine vers les capteurs autonomes](configure-event-forwarding.md). 

- **Mots de passe exposés en texte clair** : certains services utilisent le protocole LDAP non sécurisé pour envoyer des informations d’identification de compte en texte brut, y compris pour des comptes sensibles. Les attaquants qui surveillent le trafic réseau peuvent intercepter ces informations d’identification et les réutiliser à des fins malveillantes. Ce rapport répertorie tous les mots de passe de compte et d’ordinateur source qu’Azure ATP a détecté comme envoyés en texte clair. 

- **Chemins d'accès de mouvement latéral pour les comptes sensibles** : ce rapport répertorie les comptes sensibles qui sont exposés via les chemins d’accès de mouvement latéral. Pour plus d’informations, consultez [Chemins d’accès de mouvement latéral](use-case-lateral-movement-path.md). Ce rapport collecte les chemins qui ont été créés au cours des 60 derniers jours, plutôt que les informations affichées dans le portail d’espace de travail, qui représentent seulement deux jours.

Il existe deux façons de générer un rapport : à la demande ou en planifiant un rapport à envoyer périodiquement à votre adresse e-mail.

Pour générer un rapport à la demande :

1. Dans la barre de menus du portail d’espace de travail Azure ATP, cliquez sur l’icône de rapport : ![icône de rapport](./media/atp-report-icon.png).

2. Sous le type de rapport sélectionné, définissez les dates **De** et **À**, et cliquez sur **Télécharger**. 
 ![rapports](./media/reports.png)

Pour définir un rapport planifié :
 
1. Dans la page **Rapports**, cliquez sur **Définir les rapports planifiés** ou, dans la page de configuration du portail d’espace de travail Azure ATP, sous Notifications et rapports, cliquez sur **Rapports planifiés**.

   ![Planification de rapports](./media/atp-sched-reports.png)
 
 > [!NOTE]
 > Les rapports quotidiens sont conçus pour être envoyés quelques instants après minuit, heure UTC.

2. Cliquez sur **Planifier** en regard de votre type de rapport sélectionné pour définir la fréquence et l’adresse e-mail de remise des rapports, puis cliquez sur le signe plus en regard des adresses e-mail pour les ajouter et cliquez sur **Enregistrer**.

   ![Planifier la fréquence et l’adresse e-mail des rapports](./media/sched-report1.png)


## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)