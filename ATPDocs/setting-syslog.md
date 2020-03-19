---
title: Définition des paramètres Syslog dans Azure Advanced Threat Protection
description: Décrit le mode de notification d’Azure ATP (par e-mail ou transfert d’événements Azure ATP) quand il détecte des activités suspectes
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a6b1cfb304787fbed3d02968221e1eeada605712
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79410933"
---
# <a name="integrate-with-syslog"></a>Intégrer à Syslog

> [!NOTE]
> Les fonctionnalités Azure ATP expliquées dans cette page sont également accessibles dans le nouveau [portail](https://portal.cloudappsecurity.com).

Azure ATP peut vous informer quand il détecte des activités suspectes et émettre des alertes de sécurité ou d’intégrité en envoyant des notifications à votre serveur Syslog. Les alertes sont envoyées par le capteur Azure ATP qui a détecté l’activité directement vers le serveur syslog. 


Une fois que vous avez activé les notifications Syslog, vous pouvez définir les éléments suivants :

   |Champ|Description|
   |---------|---------------|
   |capteur|Sélectionnez un capteur désigné comme responsable de l’agrégation de tous les événements Syslog et de leur transfert vers votre serveur SIEM.|
   |Point de terminaison de service|Nom de domaine complet du serveur Syslog et modifiez éventuellement le numéro de port (par défaut, 514)|
   |Transport|Peut être UDP, TCP ou TLS (Syslog sécurisé)|
   |Format|Il s’agit du format utilisé par Azure ATP pour envoyer des événements au serveur SIEM : RFC 5424 ou 3164.|

1. Avant de configurer les notifications Syslog, collaborez avec votre administrateur SIEM pour connaître les informations suivantes :

   -   Nom de domaine complet ou adresse IP du serveur SIEM

   -   Port sur lequel écoute le serveur SIEM

   -   Mode de transport à utiliser : UDP, TCP ou TLS (Syslog sécurisé)

   -   Format sous lequel envoyer les données, RFC 3164 ou 5424

1. Ouvrez le portail Azure ATP. 
2. Cliquez sur **Paramètres**.
3. Dans le sous-menu **Notifications et rapports**, sélectionnez **Notifications**. 
1. Dans l’option **Service Syslog**, cliquez sur **Configurer**.
1. Sélectionnez le **Capteur**. 
1. Entrez l’URL du **Point de terminaison de service**.
1. Sélectionnez le protocole de **Transport** (TCP ou UDP). 
1. Sélectionnez le format (RFC 3164 ou RFC 5424). 
1. Sélectionnez **Envoyer un message de test à syslog**, puis vérifiez que le message est reçu dans votre solution d’infrastructure Syslog. 
1. Cliquez sur **Save**. 

Pour passer en revue ou modifier vos paramètres Syslog.  

3. Cliquez sur **Notifications**, puis, sous **Notifications Syslog**, cliquez sur **Configurer** et entrez les informations suivantes :

   ![Image des paramètres du serveur Syslog Azure ATP](media/atp-syslog.png)

4. Vous pouvez sélectionner les événements à envoyer à votre serveur Syslog. Sous **Notifications Syslog**, spécifiez quelles notifications doivent être envoyées à votre serveur Syslog : nouvelles alertes de sécurité, alertes de sécurité mises à jour et nouveaux problèmes d’intégrité.

> [!NOTE]
> Si vous envisagez de créer l’automatisation ou des scripts pour les journaux Azure ATP SIEM, nous vous recommandons d’utiliser le champ **externalId** afin d’identifier le type d’alerte au lieu d’utiliser le nom de l’alerte à cet effet. Les noms d’alerte peuvent parfois être modifiés alors que l’**externalId** de chaque alerte est définitif. Pour en savoir plus, consultez [Informations de référence sur le journal SIEM Azure ATP](cef-format-sa.md). 


## <a name="see-also"></a>Voir aussi

- [Utilisation de comptes sensibles](sensitive-accounts.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
