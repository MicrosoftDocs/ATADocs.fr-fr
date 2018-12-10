---
title: Définition des paramètres Syslog dans Azure - Protection avancée contre les menaces | Microsoft Docs
description: Décrit le mode de notification d’Azure ATP (par e-mail ou transfert d’événements Azure ATP) quand il détecte des activités suspectes
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5d3eb4dbc714e7de4d586e686cd26ead83fceda8
ms.sourcegitcommit: f4f2a1b2c674c4dba7a46ece0624f5ea10c4865e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2018
ms.locfileid: "52744674"
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="integrate-with-syslog"></a>Intégrer à Syslog

Azure ATP peut vous informer quand il détecte des activités suspectes et émet des alertes de sécurité ou des alertes d’intégrité, en envoyant la notification à votre serveur Syslog. Si vous activez les notifications Syslog, vous pouvez définir les éléments suivants :

1.  Avant de configurer les notifications Syslog, collaborez avec votre administrateur SIEM pour connaître les informations suivantes :

    -   Nom de domaine complet ou adresse IP du serveur SIEM

    -   Port sur lequel écoute le serveur SIEM

    -   Mode de transport à utiliser : UDP, TCP ou TLS (Syslog sécurisé)

    -   Format sous lequel envoyer les données, RFC 3164 ou 5424

2.  Entrez l’URL de l’instance.

3.  Entrez votre nom d’utilisateur et votre mot de passe Azure Active Directory, puis cliquez sur **Se connecter**.

4.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône de paramètres de configuration d’Azure ATP](media/ATP-config-menu.png)

5.  Cliquez sur **Notifications**, puis, sous **Notifications Syslog**, cliquez sur **Configurer** et entrez les informations suivantes :

    |Champ|Description|
    |---------|---------------|
    |capteur|Sélectionnez un capteur désigné comme responsable de l’agrégation de tous les événements Syslog et de leur transfert vers votre serveur SIEM.|
    |Point de terminaison de service|Nom de domaine complet du serveur Syslog et modifiez éventuellement le numéro de port (par défaut, 514)|
    |Transport|Peut être UDP, TCP ou TLS (Syslog sécurisé)|
    |Format|Il s’agit du format utilisé par Azure ATP pour envoyer des événements au serveur SIEM : RFC 5424 ou 3164.|

 ![Image des paramètres du serveur Syslog Azure ATP](media/atp-syslog.png)

6. Vous pouvez sélectionner les événements à envoyer à votre serveur Syslog. Sous **Notifications Syslog**, spécifiez quelles notifications doivent être envoyées à votre serveur Syslog : nouvelles alertes de sécurité, alertes de sécurité mises à jour et nouveaux problèmes d’intégrité.

> [!NOTE]
> Si vous envisagez de créer l’automatisation ou des scripts pour les journaux Azure ATP SIEM, nous vous recommandons d’utiliser le champ **externalId** afin d’identifier le type d’alerte au lieu d’utiliser le nom de l’alerte à cet effet. Les noms d’alerte peuvent parfois être modifiés alors que l’**externalId** de chaque alerte est définitif. Pour en savoir plus, consultez [Informations de référence sur le journal SIEM Azure ATP](cef-format-sa.md). 


## <a name="see-also"></a>Voir aussi

- [Utilisation de comptes sensibles](sensitive-accounts.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)