---
title: Utilisation des rapports ATA | Microsoft Docs
description: Explique comment vous pouvez générer des rapports dans ATA pour surveiller votre réseau.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ea63b6966cc933fcb0a4c748e5b4de511895c483
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54840333"
---
# <a name="ata-reports"></a>Rapports ATA


*S’applique à : Advanced Threat Analytics version 1.9*

La section Rapports ATA de la console vous permet de générer des rapports contenant des informations sur l’état du système, sur l’intégrité du système et sur les activités suspectes détectées dans votre environnement.

Pour accéder à la page Rapports, cliquez sur l’icône de rapport dans la barre de menus : ![icône de rapport](./media/ata-report-icon.png).
Les rapports disponibles sont : 

- **Rapport de synthèse** : ce rapport présente un tableau de bord de l’état dans le système. Vous pouvez afficher trois onglets : un pour un **Résumé** de ce qui a été détecté sur votre réseau, un pour les **Activités suspectes ouvertes** qui répertorie les activités suspectes nécessitant votre attention, et un pour les **Problèmes d’intégrité ouverts** qui répertorie les problèmes d’intégrité système ATA nécessitant votre attention. Les activités suspectes répertoriées sont regroupées par type, tout comme les problèmes d’intégrité. 

- **Modification de groupes sensibles** : ce rapport liste toutes les modifications apportées aux groupes sensibles (comme les administrateurs).

- **Mots de passe exposés en texte clair** : certains services utilisent le protocole LDAP non sécurisé pour envoyer des informations d’identification de compte en texte brut, y compris pour des comptes sensibles. Les attaquants qui surveillent le trafic réseau peuvent intercepter ces informations d’identification et les réutiliser à des fins malveillantes. Ce rapport liste tous les mots de passe de compte et d’ordinateur sources qu’ATA a détectés comme envoyés en texte clair. 

- **Chemins d’accès par mouvement latéral aux comptes sensibles** : ce rapport liste les comptes sensibles exposés au moyen de chemins d’accès par mouvement latéral. Pour plus d’informations, consultez [Chemins de mouvement latéral](use-case-lateral-movement-path.md).

Il existe deux façons de générer un rapport : à la demande ou en planifiant un rapport à envoyer périodiquement à votre adresse e-mail.

Pour générer un rapport à la demande :

1. Dans la barre de menus de la console ATA, cliquez sur l’icône de rapport dans la barre de menus : ![icône de rapport](./media/ata-report-icon.png).

2. Sous le type de rapport sélectionné, définissez les dates **De** et **À**, et cliquez sur **Télécharger**. 
 ![rapports](./media/reports.png)

Pour définir un rapport planifié :
 
1. Dans la page **Rapports**, cliquez sur **Définir les rapports planifiés** ou, dans la page de configuration de la console ATA, sous Notifications et rapports, cliquez sur **Rapports planifiés**.

   ![Planification de rapports](./media/ata-sched-reports.png)

   > [!NOTE]
   > Les rapports quotidiens sont conçus pour être envoyés quelques instants après minuit, heure UTC.

2. Cliquez sur **Planifier** en regard de votre type de rapport sélectionné pour définir la fréquence et l’adresse e-mail de remise des rapports, puis cliquez sur le signe plus en regard des adresses e-mail pour les ajouter et cliquez sur **Enregistrer**.

   ![Planifier la fréquence et l’adresse e-mail des rapports](./media/sched-report1.png)


> [!NOTE]
> Les rapports planifiés sont remis par e-mail et peuvent être envoyés seulement si vous avez déjà configuré un serveur de messagerie sous **Configuration** en sélectionnant **Serveur de messagerie** sous **Notifications et rapports**.


## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Planification de la capacité d’ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
