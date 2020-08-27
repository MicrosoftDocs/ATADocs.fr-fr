---
title: Configurer le transfert d’événements Windows dans Advanced Threat Analytics
description: Décrit les options de configuration du transfert des événements Windows avec ATA
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a23a590357a7c4fc6f04ccd33c747586d571a447
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88954882"
---
# <a name="configuring-windows-event-forwarding"></a>Configuration du transfert d’événements Windows

*S’applique à : Advanced Threat Analytics version 1.9*

> [!NOTE]
> Pour les versions 1.8 et ultérieures d’ATA, la configuration de la collecte d’événements n’est plus nécessaire pour les passerelles légères ATA. La passerelle légère ATA lit désormais les événements localement, sans qu’il soit nécessaire de configurer le transfert d’événements.

Pour améliorer les capacités de détection, ATA a besoin des événements Windows suivants : 4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045. Ils peuvent être lus automatiquement par la passerelle légère ATA ou, si la passerelle légère ATA n’est pas déployée, ils peuvent être transférés à la passerelle ATA de deux manières : en configurant la passerelle ATA afin qu’elle reste à l’écoute des événements SIEM ou en configurant le transfert d’événements Windows.

> [!NOTE]
> Si vous n’utilisez pas Server Core, [wecutil](/windows-server/administration/windows-commands/wecutil) peut être utilisé pour créer et gérer des abonnements aux événements qui sont transférés à partir d’ordinateurs distants.

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>Configuration WEF pour la passerelle ATA avec mise en miroir de ports

Après avoir configuré la mise en miroir des ports depuis les contrôleurs de domaine sur la passerelle ATA, utilisez les instructions ci-dessous pour configurer les transferts d’événements Windows à l’aide de la configuration Initialisation par la source. Il s’agit de l’une des façons de configurer Windows Event Forwarding. 

**Étape 1 : Ajouter le compte de service réseau au groupe Lecteurs du journal des événements de domaine** 

Dans ce scénario, nous partons du principe que la passerelle ATA est un membre du domaine.

1. Ouvrez Utilisateurs et ordinateurs Active Directory, accédez au dossier **BuiltIn** et double-cliquez sur **Lecteurs des journaux d’événements**. 
1. Sélectionnez **Membres**.
1. Si **Service réseau** ne figure pas dans la liste, cliquez sur **Ajouter** et tapez **Service réseau** dans le champ **Entrez les noms d’objets à sélectionner**. Ensuite, cliquez sur **Vérifier les noms** et cliquez deux fois sur **OK**. 

Après avoir ajouté le **Service réseau** au groupe **Lecteurs des journaux d’événements**, redémarrez les contrôleurs de domaine pour que la modification prenne effet.

**Étape 2 : Créer une stratégie sur les contrôleurs de domaine pour définir le paramètre Configurer le gestionnaire d’abonnements cible** 
> [!Note] 
> Vous pouvez créer une stratégie de groupe pour ces paramètres et appliquer la stratégie de groupe à chaque contrôleur de domaine surveillé par la passerelle ATA. Les étapes ci-dessous modifient la stratégie locale du contrôleur de domaine.  

1. Exécutez la commande suivante sur chaque contrôleur de domaine : *winrm quickconfig*
1. Sur la ligne de commande, tapez *gpedit.msc*.
1. Développez **Configuration ordinateur > Modèles d’administration > Composants Windows > Transfert d’événements**.

    ![Image de l’éditeur de groupe de stratégie locale](media/wef%201%20local%20group%20policy%20editor.png)

1. Double-cliquez sur **Configurer le Gestionnaire d’abonnements cible**.
   
   1.  Sélectionnez **Activé**.
   2.  Sous **Options**, cliquez sur **Afficher**.

   3.  Sous **SubscriptionManagers**, entrez la valeur suivante et cliquez sur **OK** : *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* 
      
        *(Par exemple : Server=`http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10`)*
      
        ![Configurer l’image d’abonnement cible](media/wef%202%20config%20target%20sub%20manager.png)
      
   4.  Cliquez sur **OK**.
   5.  À partir d’une invite de commandes avec élévation de privilèges, tapez *gpupdate /force*. 

**Étape 3 : Effectuer les opérations suivantes sur la passerelle ATA** 

1. Ouvrez une invite de commandes avec élévation de privilèges et tapez *wecutil qc*.
1. Ouvrez l’**Observateur d’événements**. 
1. Cliquez avec le bouton droit sur **Abonnements** et sélectionnez **Créer un abonnement**. 

    1. Entrez un nom et une description pour l’abonnement. 
    2. Pour **Journal de destination**, vérifiez que **Événements transférés** est sélectionné. Pour qu’ATA lise les événements, le journal de destination doit être **Événements transférés**. 
    3. Sélectionnez **Initialisation par l’ordinateur source** et cliquez sur **Sélectionner les groupes d’ordinateurs**.
        1. Cliquez sur **Ajouter un ordinateur de domaine**.
        2. Entrez le nom du contrôleur de domaine dans le champ **Entrer le nom de l’objet à sélectionner**. Ensuite, cliquez sur **Vérifier les noms**, puis sur **OK**.  
          ![Image de l’Observateur d’événements](media/wef3%20event%20viewer.png)  
        3. Cliquez sur **OK**.
    4. Cliquez sur **Sélectionner des événements**.
        1. Cliquez sur **Par journal** et sélectionnez **Sécurité**.
        2. Dans le champ **Inclut/exclut l’ID d’événement**, tapez le numéro d’événement puis cliquez sur **OK**. Par exemple, tapez 4776, comme dans l’exemple suivant.

        ![Image de filtre de requête](media/wef%204%20query%20filter.png)

    5. Cliquez avec le bouton droit sur l’abonnement créé et sélectionnez **État d’exécution** pour voir s’il existe des problèmes avec l’état. 
    6. Après quelques minutes, vérifiez que les événements que vous avez configurés pour être transférés apparaissent dans les événements transférés sur la passerelle ATA.


Pour plus d'informations, voir : [Configurer les ordinateurs de façon à transférer et à recueillir les événements](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc748890(v=ws.11))

## <a name="see-also"></a>Voir aussi
- [Installer ATA](install-ata-step1.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)