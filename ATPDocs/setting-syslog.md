---
title: Définition des paramètres de notification par e-mail dans Azure - Protection avancée contre les menaces | Microsoft Docs
description: Décrit le mode de notification d’Azure ATP (par e-mail ou transfert d’événements Azure ATP) quand il détecte des activités suspectes
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 74fe9976df769ae01c58a5d66ca491c3fa8958d9
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
ms.locfileid: "29444865"
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="integrate-with-syslog"></a>Intégrer à Syslog

Azure ATP peut vous informer quand il détecte des activités suspectes ou des alertes d’intégrité en envoyant la notification à votre serveur Syslog. Si vous activez les notifications Syslog, vous pouvez définir les éléments associés suivants.

1.  Avant de configurer les notifications Syslog, collaborez avec votre administrateur SIEM pour connaître les informations suivantes :

    -   Nom de domaine complet ou adresse IP du serveur SIEM

    -   Port sur lequel écoute le serveur SIEM

    -   Mode de transport à utiliser : UDP, TCP ou TLS (Syslog sécurisé)

    -   Format sous lequel envoyer les données, RFC 3164 ou 5424

2.  Entrez l’URL du portail d’espace de travail.

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


## <a name="see-also"></a>Voir aussi

- [Utilisation de comptes sensibles](sensitive-accounts.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)