---
title: Définition des paramètres de notification par e-mail dans Advanced Threat Analytics | Microsoft Docs
description: Décrit comment faire en sorte qu’ATA vous avertisse (par courrier électronique ou transfert d’événements ATA) quand il détecte des activités suspectes
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: bff20bf7-8b53-49da-81e5-b818a1c3b24e
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: dad6dca2a22e27702f21f77c685d90749963cfac
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54840592"
---
# <a name="provide-ata-with-your-email-server-settings"></a>Fournir à ATA les paramètres de votre serveur de messagerie

*S’applique à : Advanced Threat Analytics version 1.9*

ATA peut vous avertir quand il détecte une activité suspecte. Pour qu’ATA puisse envoyer des notifications par courrier électronique, vous devez d’abord configurer les **paramètres du serveur de messagerie**.

1. Sur le serveur du centre ATA, cliquez sur l’icône **Microsoft Advanced Threat Analytics Management**(Gestion de Microsoft Advanced Threat Analytics) sur le Bureau.

2. Entrez votre nom d’utilisateur et votre mot de passe, puis cliquez sur **Se connecter**.

3. Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

   ![Icône des paramètres de configuration ATA](media/ATA-config-icon.png)

4. Dans la section **Notifications** sous **Serveur de messagerie**, entrez les informations suivantes :


   |              Champ              |                                                                                                 Description                                                                                                  |               Valeur                |
   |---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|
   | Point de terminaison du serveur SMTP (obligatoire) |                                                            Entrez le nom de domaine complet de votre serveur SMTP et modifiez éventuellement le numéro de port (par défaut, 25).                                                            | Par exemple :<br />smtp.contoso.com |
   |               SSL               |                                              Activez/désactivez SSL si le serveur SMTP exigeait SSL. **Remarque :** si vous activez SSL, vous devez également modifier le numéro de port.                                               |        La valeur par défaut est désactivée         |
   |         Authentification          | Activez l’authentification si votre serveur SMTP l’exige. **Remarque :** si vous activez l’authentification, vous devez indiquer le nom d’utilisateur et le mot de passe d’un compte de courrier qui a l’autorisation de se connecter au serveur SMTP. |        La valeur par défaut est désactivée         |
   |      Envoyer depuis (obligatoire)       |                                                                        Entrez une adresse de messagerie à partir de laquelle le courrier sera envoyé.                                                                         | Par exemple :<br />ATA@contoso.com  |

   ![Image des paramètres du serveur de messagerie ATA](media/ata-email-server.png)

## <a name="provide-ata-with-your-syslog-server-settings"></a>Fournir à ATA les paramètres de votre serveur Syslog
ATA peut vous avertir quand il détecte une activité suspecte en envoyant la notification à votre serveur Syslog. Si vous activez les notifications Syslog, vous pouvez définir les éléments associés suivants.

1. Avant de configurer les notifications Syslog, collaborez avec votre administrateur SIEM pour connaître les informations suivantes :

   -   Nom de domaine complet ou adresse IP du serveur SIEM

   -   Port sur lequel écoute le serveur SIEM

   -   Mode de transport à utiliser : UDP, TCP ou TLS (Syslog sécurisé)

   -   Format sous lequel envoyer les données, RFC 3164 ou 5424

2. Sur le serveur du centre ATA, cliquez sur l’icône **Microsoft Advanced Threat Analytics Management**(Gestion de Microsoft Advanced Threat Analytics) sur le Bureau.

3. Entrez votre nom d’utilisateur et votre mot de passe, puis cliquez sur **Se connecter**.

4. Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

   ![Icône des paramètres de configuration ATA](media/ATA-config-icon.png)

5. Dans la section Notifications, sélectionnez **Serveur Syslog** et entrez les informations suivantes :

   |Champ|Description|
   |---------|---------------|
   |Point de terminaison du serveur Syslog|Nom de domaine complet du serveur Syslog et modifiez éventuellement le numéro de port (par défaut, 514)|
   |Transport|Peut être UDP, TCP ou TLS (Syslog sécurisé)|
   |Format|Il s’agit du format utilisé par ATA pour envoyer des événements au serveur SIEM : RFC 5424 ou 3164.|

   ![Image des paramètres du serveur Syslog ATA](media/ata-syslog-server-settings.png)



## <a name="see-also"></a>Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
