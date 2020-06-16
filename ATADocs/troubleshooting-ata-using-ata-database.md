---
title: Résolution des problèmes de Advanced Threat Analytics à l’aide de la base de données
description: Décrit comment vous pouvez utiliser la base de données ATA pour résoudre les problèmes
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 269646c7547b0a9a3538405a4180d063e27e0455
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84774908"
---
# <a name="troubleshooting-ata-using-the-ata-database"></a>Résolution des problèmes liés à ATA à l’aide de la base de données ATA

*S’applique à : Advanced Threat Analytics version 1.9*

ATA utilise MongoDB comme base de données.
Vous pouvez interagir avec la base de données à l’aide de la ligne de commande par défaut ou d’un outil d’interface utilisateur pour effectuer la résolution des problèmes et des tâches avancées.

## <a name="interacting-with-the-database"></a>Interaction avec la base de données
La procédure par défaut et la plus simple pour interroger la base de données consiste à utiliser l’interpréteur de commandes Mongo :

1.  Ouvrez une fenêtre de ligne de commande et modifiez le chemin au dossier bin MongoDB. Le chemin par défaut est : **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

2.  Exécutez : `mongo.exe ATA`. Veillez à taper ATA tout en majuscules.

> [!div class="mx-tableFixed"]
> 
> |Comment...|Syntaxe|Notes|
> |-------------|----------|---------|
> |Rechercher des collections dans la base de données.|`show collections`|Utile en tant que test de bout en bout pour constater que le trafic est écrit dans la base de données et que l’événement 4776 est reçu par ATA.|
> |Obtenir les détails d’un utilisateur/ordinateur/groupe (UniqueEntity), par exemple un ID d’utilisateur.|`db.UniqueEntity.find({CompleteSearchNames: "<name of entity in lower case>"})`||
> |Rechercher le trafic d’authentification Kerberos provenant d’un ordinateur donné lors d’une journée spécifique.|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Pour obtenir l’&lt;ID de l’ordinateur source&gt;, vous pouvez interroger les collections UniqueEntity, comme illustré dans l’exemple.<br /><br />Chaque type d’activité réseau, par exemple les authentifications Kerberos, possède sa propre collection par date UTC.|
> |Apporter des modifications de configuration avancée. Dans cet exemple, affectons la valeur 10 000 à la taille de la file d’attente d’envoi pour toutes les passerelles ATA.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

Voici un exemple de code qui utilise la syntaxe fournie précédemment. Si vous étudiez une activité suspecte qui s’est produite le 20/10/2015 et que vous souhaitez en savoir plus sur les activités NTLM effectuées par « John Doe » ce jour-là :<br /><br />Tout d’abord, recherchez l’ID de « John Doe »

`db.UniqueEntity.find({Name: "John Doe"})`<br>Notez son ID comme indiqué par la valeur `_id`. Dans notre exemple, supposons que l’ID est `123bdd24-b269-h6e1-9c72-7737as875351`<br>Recherchez ensuite la collection avec la date la plus proche qui est antérieure à la date que vous recherchez, dans l'exemple 20/10/2015.<br>Recherchez ensuite les activités NTLM du compte de John Doe : 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`

## <a name="see-also"></a>Voir aussi
- [Configuration requise pour ATA](ata-prerequisites.md)
- [Planification de la capacité ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
