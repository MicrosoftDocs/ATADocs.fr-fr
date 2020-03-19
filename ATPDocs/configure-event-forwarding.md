---
title: Configurer les transferts d’événements Windows dans Azure Advanced Threat Protection
description: Décrit les options de configuration des transferts d’événements Windows avec Azure ATP
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 3547519f-8d9c-40a9-8f0e-c7ba21081203
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: be65a11aa6ace79ec4f2e3cffdc8a196c87fa764
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414027"
---
# <a name="configuring-windows-event-forwarding"></a>Configuration du transfert d’événements Windows

> [!NOTE]
> Le capteur Azure ATP lit automatiquement les événements localement, sans qu’il ne soit nécessaire de configurer les transferts d’événements.

Pour améliorer les capacités de détection, Azure ATP a besoin des événements Windows suivants : 4776, 4732, 4733, 4728, 4729, 4756, 4757 et 7041. Ils peuvent être lus automatiquement par le capteur Azure ATP ou, si le capteur Azure ATP n’est pas déployé, ils peuvent être transférés au capteur autonome Azure ATP de deux manières : en configurant le capteur autonome Azure ATP afin qu’il reste à l’écoute des événements SIEM ou en configurant les transferts d’événements Windows.

> [!NOTE]
>
> - Les capteurs autonomes Azure ATP ne prennent pas en charge tous les types de sources de données, ce qui entraîne des détections manquées. Pour une couverture complète de votre environnement, nous vous recommandons de déployer le capteur Azure ATP.
> - Vérifiez que le contrôleur de domaine est correctement configuré pour capturer les événements requis.

## <a name="wef-configuration-for-azure-atp-standalone-sensors-with-port-mirroring"></a>Configuration WEF pour le capteur autonome Azure ATP avec mise en miroir de ports

Une fois que vous avez configuré la mise en miroir des ports des contrôleurs de domaine sur le capteur autonome Azure ATP, suivez les instructions ci-dessous pour configurer les transferts d’événements Windows à l’aide de la configuration Initialisation par la source. Il s’agit de l’une des façons de configurer Windows Event Forwarding.

**Étape 1 : Ajouter le compte de service réseau au groupe Lecteurs du journal des événements de domaine**

Dans ce scénario, nous partons du principe que le capteur autonome Azure ATP est un membre du domaine.

1. Ouvrez Utilisateurs et ordinateurs Active Directory, accédez au dossier **BuiltIn** et double-cliquez sur **Lecteurs des journaux d’événements**.
1. Sélectionnez **Membres**.
1. Si **Service réseau** ne figure pas dans la liste, cliquez sur **Ajouter** et tapez **Service réseau** dans le champ **Entrez les noms d’objets à sélectionner**. Ensuite, cliquez sur **Vérifier les noms** et cliquez deux fois sur **OK**.

Après avoir ajouté le **Service réseau** au groupe **Lecteurs des journaux d’événements**, redémarrez les contrôleurs de domaine pour que la modification prenne effet.

**Étape 2 : Créer une stratégie sur les contrôleurs de domaine pour définir le paramètre Configurer le gestionnaire d’abonnements cible**

> [!Note]
> Vous pouvez créer une stratégie de groupe pour ces paramètres et appliquer la stratégie de groupe à chaque contrôleur de domaine surveillé par le capteur autonome Azure ATP. Les étapes suivantes modifient la stratégie locale du contrôleur de domaine.

1. Exécutez la commande suivante sur chaque contrôleur de domaine : *winrm quickconfig*
1. Sur la ligne de commande, tapez *gpedit.msc*.
1. Développez **Configuration ordinateur > Modèles d’administration > Composants Windows > Transfert d’événements**.

   ![Image de l’éditeur de groupe de stratégie locale](media/wef%201%20local%20group%20policy%20editor.png)

1. Double-cliquez sur **Configurer le Gestionnaire d’abonnements cible**.

    1. Sélectionnez **Activé**.
    1. Sous **Options**, cliquez sur **Afficher**.
    1. Sous **SubscriptionManagers**, entrez la valeur suivante et cliquez sur **OK** :  Server= http\://\<fqdnATPSensor>:5985/wsman/SubscriptionManager/WEC,Refresh=10` (par exemple : Server=http\://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)

    ![Configurer l’image d’abonnement cible](media/wef%202%20config%20target%20sub%20manager.png)

1. Cliquez sur **OK**.
1. À partir d’une invite de commandes avec élévation de privilèges, tapez *gpupdate /force*.

**Étape 3 : Effectuer les opérations suivantes sur le capteur autonome Azure ATP**

1. Ouvrez une invite de commandes avec élévation de privilèges et tapez *wecutil qc*.
1. Ouvrez l’**Observateur d’événements**.
1. Cliquez avec le bouton droit sur **Abonnements** et sélectionnez **Créer un abonnement**.

    1. Entrez un nom et une description pour l’abonnement.
    1. Pour **Journal de destination**, vérifiez que **Événements transférés** est sélectionné. Pour qu’Azure ATP lise les événements, le journal de destination doit être **Événements transférés**.
    1. Sélectionnez **Initialisation par l’ordinateur source** et cliquez sur **Sélectionner les groupes d’ordinateurs**.
        1. Cliquez sur **Ajouter un ordinateur de domaine**.
        1. Entrez le nom du contrôleur de domaine dans le champ **Entrer le nom de l’objet à sélectionner**. Ensuite, cliquez sur **Vérifier les noms**, puis sur **OK**.
        1. Cliquez sur **OK**.
        ![Image de l’Observateur d’événements](media/wef3%20event%20viewer.png)
    1. Cliquez sur **Sélectionner des événements**.
        1. Cliquez sur **Par journal** et sélectionnez **Sécurité**.
        1. Dans le champ **Inclut/exclut l’ID d’événement**, tapez le numéro d’événement puis cliquez sur **OK**. Par exemple, tapez 4776, comme dans l’exemple suivant :<br/>
        ![Image de filtre de requête](media/wef-4-query-filter.png)
    1. Cliquez avec le bouton droit sur l’abonnement créé et sélectionnez **État d’exécution** pour voir s’il existe des problèmes avec l’état.
    1. Après quelques minutes, vérifiez que les événements que vous avez configurés pour être transférés apparaissent dans les événements transférés sur le capteur autonome Azure ATP.

Pour plus d'informations, voir : [Configurer les ordinateurs de façon à transférer et à recueillir les événements](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Voir aussi

- [Installer Azure ATP](install-atp-step1.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
