---
title: Utilisation des rapports ATA
description: Explique comment vous pouvez générer des rapports dans ATA pour surveiller votre réseau.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4565c55a754cbbd650fff0e100e727c9c2720fc7
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690395"
---
# <a name="ata-reports"></a>Rapports ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

La section Rapports ATA de la console vous permet de générer des rapports contenant des informations sur l’état du système, sur l’intégrité du système et sur les activités suspectes détectées dans votre environnement.

Pour accéder à la page Rapports, cliquez sur l’icône de rapport dans la barre de menus : ![icône de rapport](media/ata-report-icon.png).
Les rapports disponibles sont :

- **Rapport de synthèse** : ce rapport présente un tableau de bord de l’état dans le système. Vous pouvez afficher trois onglets : un pour un **Résumé** de ce qui a été détecté sur votre réseau, un pour les **Activités suspectes ouvertes** qui répertorie les activités suspectes nécessitant votre attention, et un pour les **Problèmes d’intégrité ouverts** qui répertorie les problèmes d’intégrité système ATA nécessitant votre attention. Les activités suspectes répertoriées sont regroupées par type, tout comme les problèmes d’intégrité.

- **Modification des groupes sensibles** : ce rapport liste toutes les modifications apportées aux groupes sensibles (comme les administrateurs).

- **Mots de passe exposés en texte clair** : certains services utilisent le protocole LDAP non sécurisé pour envoyer des informations d’identification de compte en texte brut, y compris pour des comptes sensibles. Les attaquants qui surveillent le trafic réseau peuvent intercepter ces informations d’identification et les réutiliser à des fins malveillantes. Ce rapport liste tous les mots de passe de compte et d’ordinateur sources qu’ATA a détectés comme envoyés en texte clair.

- **Chemins d’accès par mouvement latéral aux comptes sensibles** : ce rapport liste les comptes sensibles exposés au moyen de chemins d’accès par mouvement latéral. Pour plus d’informations, consultez [chemins de mouvement latéral](use-case-lateral-movement-path.md) .

Il existe deux façons de générer un rapport : à la demande ou en planifiant un rapport à envoyer périodiquement à votre adresse e-mail.

Pour générer un rapport à la demande :

1. Dans la barre de menus de la console ATA, cliquez sur l’icône de rapport dans la barre de menus : ![icône de rapport](media/ata-report-icon.png).

1. Sous le type de rapport sélectionné, définissez les dates **De** et **À**, et cliquez sur **Télécharger**.
 ![Capture d’écran montrant la sélection de la plage de dates du rapport](media/reports.png)

Pour définir un rapport planifié :

1. Dans la page **Rapports**, cliquez sur **Définir les rapports planifiés** ou, dans la page de configuration de la console ATA, sous Notifications et rapports, cliquez sur **Rapports planifiés**.

    ![Planification de rapports](media/ata-sched-reports.png)

   > [!NOTE]
   > Les rapports quotidiens sont conçus pour être envoyés quelques instants après minuit, heure UTC.

1. Cliquez sur **Planifier** en regard de votre type de rapport sélectionné pour définir la fréquence et l’adresse e-mail de remise des rapports, puis cliquez sur le signe plus en regard des adresses e-mail pour les ajouter et cliquez sur **Enregistrer**.

    ![Planifier la fréquence et l’adresse e-mail des rapports](media/sched-report1.png)

> [!NOTE]
> Les rapports planifiés sont remis par e-mail et peuvent être envoyés seulement si vous avez déjà configuré un serveur de messagerie sous **Configuration** en sélectionnant **Serveur de messagerie** sous **Notifications et rapports**.

## <a name="see-also"></a>Voir aussi

- [Configuration requise pour ATA](ata-prerequisites.md)
- [Planification de la capacité ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
