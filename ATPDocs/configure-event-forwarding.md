---
title: Configurer les transferts d’événements Windows dans Azure - Protection avancée contre les menaces | Microsoft Docs
description: Décrit les options de configuration des transferts d’événements Windows avec Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/07/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3547519f-8d9c-40a9-8f0e-c7ba21081203
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d8b1730da0f5ab74dff39b8331fb78c293d57db3
ms.sourcegitcommit: 1a5880de35422d050fc1bc7a918dedc4180c45ad
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51265711"
---
*S’applique à : Azure Advanced Threat Protection*



# <a name="configuring-windows-event-forwarding"></a>Configuration du transfert d’événements Windows

> [!NOTE]
> Le capteur Azure ATP lit automatiquement les événements localement, sans qu’il ne soit nécessaire de configurer les transferts d’événements.


Pour améliorer les capacités de détection, Azure ATP a besoin des événements Windows suivants : 4776, 4732, 4733, 4728, 4729, 4756, 4757 et 7045. Ils peuvent être lus automatiquement par le capteur Azure ATP ou, si le capteur Azure ATP n’est pas déployé, ils peuvent être transférés au capteur autonome Azure ATP de deux manières : en configurant le capteur autonome Azure ATP afin qu’il reste à l’écoute des événements SIEM ou en configurant les transferts d’événements Windows.

> [!NOTE]
> Vérifiez que le contrôleur de domaine est correctement configuré pour capturer les événements requis.

### <a name="wef-configuration-for-azure-atp-standalone-sensors-with-port-mirroring"></a>Configuration WEF pour le capteur autonome Azure ATP avec mise en miroir de ports

Une fois que vous avez configuré la mise en miroir des ports des contrôleurs de domaine sur le capteur autonome Azure ATP, suivez les instructions ci-dessous pour configurer les transferts d’événements Windows à l’aide de la configuration Initialisation par la source. Il s’agit de l’une des façons de configurer Windows Event Forwarding. 

**Étape 1 : ajouter le compte service réseau au groupe Lecteurs des journaux d’événements du domaine** 

Dans ce scénario, nous partons du principe que le capteur autonome Azure ATP est un membre du domaine.

1.  Ouvrez Utilisateurs et ordinateurs Active Directory, accédez au dossier **BuiltIn** et double-cliquez sur **Lecteurs des journaux d’événements**. 
2.  Sélectionnez **Membres**.
3.  Si **Service réseau** ne figure pas dans la liste, cliquez sur **Ajouter** et tapez **Service réseau** dans le champ **Entrez les noms d’objets à sélectionner**. Ensuite, cliquez sur **Vérifier les noms** et cliquez deux fois sur **OK**. 

Après avoir ajouté le **Service réseau** au groupe **Lecteurs des journaux d’événements**, redémarrez les contrôleurs de domaine pour que la modification prenne effet.

**Étape 2 : créer une stratégie sur les contrôleurs de domaine pour définir le paramètre Configurer le Gestionnaire d’abonnements cible.** 
> [!Note] 
> Vous pouvez créer une stratégie de groupe pour ces paramètres et appliquer la stratégie de groupe à chaque contrôleur de domaine surveillé par le capteur autonome Azure ATP. Les étapes suivantes modifient la stratégie locale du contrôleur de domaine.     

1.  Exécutez la commande suivante sur chaque contrôleur de domaine : *winrm quickconfig*
2.  Sur la ligne de commande, tapez *gpedit.msc*.
3.  Développez **Configuration ordinateur > Modèles d’administration > Composants Windows > Transfert d’événements**.

 ![Image de l’éditeur de groupe de stratégie locale](media/wef%201%20local%20group%20policy%20editor.png)

4.  Double-cliquez sur **Configurer le Gestionnaire d’abonnements cible**.
   
    1.  Sélectionnez **Activé**.
    2.  Sous **Options**, cliquez sur **Afficher**.
    3.  Sous **SubscriptionManagers**, entrez la valeur suivante et cliquez sur **OK** : *Server=`http://<fqdnATPSensor>:5985/wsman/SubscriptionManager/WEC,Refresh=10` *(Par exemple Server=`http://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10`)
    
    ![Configurer l’image d’abonnement cible](media/wef%202%20config%20target%20sub%20manager.png)
    
5.  Cliquez sur **OK**.
6.  À partir d’une invite de commandes avec élévation de privilèges, tapez *gpupdate /force*. 

**Étape 3 : effectuer les opérations suivantes sur le capteur autonome Azure ATP** 

1. Ouvrez une invite de commandes avec élévation de privilèges et tapez *wecutil qc*.
2. Ouvrez l’**Observateur d’événements**. 
3. Cliquez avec le bouton droit sur **Abonnements** et sélectionnez **Créer un abonnement**. 
    
    1. Entrez un nom et une description pour l’abonnement. 
    2. Pour **Journal de destination**, vérifiez que **Événements transférés** est sélectionné. Pour qu’Azure ATP lise les événements, le journal de destination doit être **Événements transférés**. 
    3. Sélectionnez **Initialisation par l’ordinateur source** et cliquez sur **Sélectionner les groupes d’ordinateurs**.
        1. Cliquez sur **Ajouter un ordinateur de domaine**.
        2. Entrez le nom du contrôleur de domaine dans le champ **Entrer le nom de l’objet à sélectionner**. Ensuite, cliquez sur **Vérifier les noms**, puis sur **OK**. 
        3. Cliquez sur **OK**.
        ![Image de l’Observateur d’événements](media/wef3%20event%20viewer.png)     
    4. Cliquez sur **Sélectionner des événements**.
        1. Cliquez sur **Par journal** et sélectionnez **Sécurité**.
        2. Dans le champ **Inclut/exclut l’ID d’événement**, tapez le numéro d’événement puis cliquez sur **OK**. Par exemple, tapez 4776, comme dans l’exemple suivant :<br/>
        ![Image de filtre de requête](media/wef-4-query-filter.png)
    5. Cliquez avec le bouton droit sur l’abonnement créé et sélectionnez **État d’exécution** pour voir s’il existe des problèmes avec l’état. 
    6. Après quelques minutes, vérifiez que les événements que vous avez configurés pour être transférés apparaissent dans les événements transférés sur le capteur autonome Azure ATP.


Pour plus d’informations, consultez [Configurer les ordinateurs pour transférer et recueillir les événements](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Voir aussi

- [Installer Azure ATP](install-atp-step1.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
