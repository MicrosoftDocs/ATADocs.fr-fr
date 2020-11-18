---
title: Configuration du transfert d’événements Windows dans Microsoft Defender pour Identity
description: Décrit les options de configuration du transfert d’événements Windows avec Microsoft Defender pour Identity.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8f30530929793bb338c7202eeedebc47b883e6c0
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848684"
---
# <a name="configuring-windows-event-forwarding"></a>Configuration du transfert d’événements Windows

> [!NOTE]
> Le capteur [!INCLUDE [Product long](includes/product-long.md)] lit automatiquement les événements en local, sans qu’il ne soit nécessaire de configurer le transfert d’événements.

Pour améliorer les capacités de détection, [!INCLUDE [Product short](includes/product-short.md)] a besoin des événements Windows qui figurent dans [Configurer la collecte des événements](configure-windows-event-collection.md#configure-event-collection). Ils peuvent être lus automatiquement par le capteur [!INCLUDE [Product short](includes/product-short.md)] ou, si celui-ci n’est pas déployé, transférés au capteur autonome [!INCLUDE [Product short](includes/product-short.md)] de deux manières : en configurant le capteur autonome de façon à écouter les événements SIEM ou en configurant le transfert d’événements Windows.

> [!NOTE]
>
> - Les capteurs autonomes [!INCLUDE [Product short](includes/product-short.md)] ne prennent pas en charge la collecte d’entrées de journal du Suivi d’événements pour Windows (ETW) qui fournissent les données pour de nombreuses détections. Pour une couverture complète de votre environnement, nous vous recommandons de déployer le capteur [!INCLUDE [Product short](includes/product-short.md)].
> - Vérifiez que le contrôleur de domaine est correctement configuré pour capturer les événements requis.

## <a name="wef-configuration-for-product-short-standalone-sensors-with-port-mirroring"></a>Configuration WEF du capteur autonome [!INCLUDE [Product short](includes/product-short.md)] avec mise en miroir de ports

Une fois que vous avez configuré la mise en miroir de ports des contrôleurs de domaine au capteur autonome [!INCLUDE [Product short](includes/product-short.md)], suivez les instructions ci-dessous pour configurer le transfert d’événements Windows selon la configuration Initialisation par la source. Il s’agit de l’une des façons de configurer Windows Event Forwarding.

**Étape 1 : Ajouter le compte de service réseau au groupe Lecteurs du journal des événements de domaine**

Dans ce scénario, nous partons du principe que le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] est membre du domaine.

1. Ouvrez Utilisateurs et ordinateurs Active Directory, accédez au dossier **BuiltIn** et double-cliquez sur **Lecteurs des journaux d’événements**.
1. Sélectionnez **Membres**.
1. Si **Service réseau** ne figure pas dans la liste, cliquez sur **Ajouter** et tapez **Service réseau** dans le champ **Entrez les noms d’objets à sélectionner**. Ensuite, cliquez sur **Vérifier les noms** et cliquez deux fois sur **OK**.

Après avoir ajouté le **Service réseau** au groupe **Lecteurs des journaux d’événements**, redémarrez les contrôleurs de domaine pour que la modification prenne effet.

**Étape 2 : Créer une stratégie sur les contrôleurs de domaine pour définir le paramètre Configurer le gestionnaire d’abonnements cible**

> [!Note]
> Vous pouvez créer une stratégie de groupe pour ces paramètres et l’appliquer à chacun des contrôleurs de domaine supervisés par le capteur autonome [!INCLUDE [Product short](includes/product-short.md)]. Les étapes suivantes modifient la stratégie locale du contrôleur de domaine.

1. Exécutez la commande suivante sur chaque contrôleur de domaine : *winrm quickconfig*
1. Sur la ligne de commande, tapez *gpedit.msc*.
1. Développez **Configuration ordinateur > Modèles d’administration > Composants Windows > Transfert d’événements**.

    ![Image de l’éditeur de groupe de stratégie locale](media/wef-1-local-group-policy-editor.png)

1. Double-cliquez sur **Configurer le Gestionnaire d’abonnements cible**.

    1. Sélectionnez **Activé**.
    1. Sous **Options**, cliquez sur **Afficher**.
    1. Sous **SubscriptionManagers**, entrez la valeur suivante et cliquez sur **OK** :  `Server=http\://\<fqdnMicrosoftDefenderForIdentitySensor>:5985/wsman/SubscriptionManager/WEC,Refresh=10` (par exemple, `Server=http\://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10`).

    ![Configurer l’image d’abonnement cible](media/wef-2-config-target-sub-manager.png)

1. Cliquez sur **OK**.
1. À partir d’une invite de commandes avec élévation de privilèges, tapez *gpupdate /force*.

**Étape 3 : Procéder comme suit sur le capteur autonome [!INCLUDE [Product short](includes/product-short.md)]**

1. Ouvrez une invite de commandes avec élévation de privilèges et tapez *wecutil qc*.
1. Ouvrez l’**Observateur d’événements**.
1. Cliquez avec le bouton droit sur **Abonnements** et sélectionnez **Créer un abonnement**.

    1. Entrez un nom et une description pour l’abonnement.
    1. Pour **Journal de destination**, vérifiez que **Événements transférés** est sélectionné. Le journal de destination doit être **Événements transférés** pour que [!INCLUDE [Product short](includes/product-short.md)] puisse lire les événements.
    1. Sélectionnez **Initialisation par l’ordinateur source** et cliquez sur **Sélectionner les groupes d’ordinateurs**.
        1. Cliquez sur **Ajouter un ordinateur de domaine**.
        1. Entrez le nom du contrôleur de domaine dans le champ **Entrer le nom de l’objet à sélectionner**. Ensuite, cliquez sur **Vérifier les noms**, puis sur **OK**.
        1. Cliquez sur **OK**.
        ![Image de l’Observateur d’événements](media/wef-3-event-viewer.png)
    1. Cliquez sur **Sélectionner des événements**.
        1. Cliquez sur **Par journal** et sélectionnez **Sécurité**.
        1. Dans le champ **Inclut/exclut l’ID d’événement**, tapez le numéro d’événement puis cliquez sur **OK**. Par exemple, tapez 4776, comme dans l’exemple suivant :<br/>
        ![Image de filtre de requête](media/wef-4-query-filter.png)
    1. Cliquez avec le bouton droit sur l’abonnement créé et sélectionnez **État d’exécution** pour voir s’il existe des problèmes avec l’état.
    1. Après quelques minutes, vérifiez que les événements configurés apparaissent bien dans les événements transférés sur le capteur autonome [!INCLUDE [Product short](includes/product-short.md)].

Pour plus d'informations, voir : [Configurer les ordinateurs de façon à transférer et à recueillir les événements](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc748890(v=ws.11))

## <a name="see-also"></a>Voir aussi

- [Installer [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
