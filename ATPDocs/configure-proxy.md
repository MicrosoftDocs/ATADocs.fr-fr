---
title: Configurer votre proxy ou pare-feu pour permettre la communication d’Azure ATP avec le capteur | Microsoft Docs
description: Décrit comment configurer votre pare-feu ou proxy pour permettre la communication entre le service cloud Azure ATP et les capteurs Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/29/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2f39c0d3628c3a3cc9e034fa1da8bb5a66bc704b
ms.sourcegitcommit: 3eade64779002d2c8ae005565bc69e1b3f89fb7d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34560239"
---
*S’applique à : Azure Advanced Threat Protection*



# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Configurer le proxy du point de terminaison et les paramètres de connectivité Internet pour le capteur Azure ATP

Chaque capteur Azure ATP requiert une connectivité Internet au service cloud Azure ATP pour fonctionner correctement. Dans certaines organisations, les contrôleurs de domaine ne sont pas connectés directement à Internet, mais plutôt par le biais d’une connexion de proxy web. Chaque capteur Azure ATP nécessite que vous utilisiez la configuration de proxy de Microsoft Windows Internet (WinINET) pour signaler les données de capteur et communiquer avec le service Azure ATP. Si vous utilisez WinHTTP pour la configuration du proxy, vous devez toujours configurer les paramètres de proxy de navigateur Windows Internet (WinINet) pour la communication entre le capteur et le service cloud Azure ATP.


Quand vous configurez le proxy, vous devez savoir que le service de capteur Azure ATP incorporé s’exécute dans le contexte du système à l’aide du compte **LocalService** et que le service de mise à jour du capteur Azure ATP s’exécute dans le contexte du système à l’aide de **LocalSystem** compte. 

> [!NOTE]
> Si vous utilisez un proxy transparent ou WPAD dans votre topologie de réseau, vous n’avez pas besoin de configurer WinINET pour votre proxy.

## <a name="configure-the-proxy"></a>Configurer le proxy 

Configurez votre serveur proxy manuellement à l’aide d’un proxy statique basé sur le Registre pour permettre au capteur Azure ATP de signaler des données de diagnostic et de communiquer avec le service cloud Azure ATP quand un ordinateur n’est pas autorisé à se connecter à Internet.

> [!NOTE]
> Les modifications de Registre doivent être appliquées uniquement à LocalService et à LocalSystem.

Le proxy statique est configurable par le biais du Registre. Vous devez copier la configuration du proxy que vous utilisez dans le contexte de l’utilisateur pour localsystem et localservice. Pour copier vos paramètres de proxy du contexte de l’utilisateur :

1.   Veillez à sauvegarder les clés de Registre avant de les modifier.

2. Dans le Registre, recherchez la valeur `DefaultConnectionSetting` comme REG_BINARY sous la clé de Registre `HKCU\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting` et copiez-la.
 
2.  Si LocalSystem n’a pas les paramètres de proxy appropriés (non configurés ou différents de Current_User), alors copiez le paramètre de proxy de Current_User vers LocalSystem. Sous la clé de Registre `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

3.  Collez la valeur de Current_user `DefaultConnectionSetting` comme REG_BINARY.

4.  Si LocalService n’a pas les paramètres de proxy appropriés, alors copiez le paramètre de proxy à partir de Current_User vers LocalService. Sous la clé de Registre `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

5.  Collez la valeur de Current_User `DefaultConnectionSetting` comme REG_BINARY.

> [!NOTE]
> Toutes les applications sont concernées, notamment les services Windows qui utilisent WinINET avec le contexte LocalService, LocalSytem.


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Activer l’accès aux URL du service Azure ATP dans le serveur proxy

Si un proxy ou pare-feu bloque tout le trafic par défaut et autorise uniquement des domaines spécifiques ou que l’analyse HTTPS (inspection SSL) est activée, vérifiez que les URL suivantes sont autorisées pour permettre la communication avec le service Azure ATP dans le port 443 :

|Emplacement du service|Enregistrement DNS .Atp.Azure.com|
|----|----|
|FR |triprd1wcusw1sensorapi.atp.azure.com<br>triprd1wcuswb1sensorapi.atp.azure.com<br>triprd1wcuse1sensorapi.atp.azure.com|
|Europe|triprd1wceun1sensorapi.atp.azure.com<br>triprd1wceuw1sensorapi.atp.azure.com|
|Asie|triprd1wcasse1sensorapi.atp.azure.com|


Vous pouvez également renforcer les règles du pare-feu ou du proxy pour un espace de travail que vous avez créé, en définissant une règle pour les enregistrements DNS suivants :
- <nom-espace de travail>.atp.azure.com : pour la connectivité de la console. Par exemple, contosoATP.atp.azure.com
- <nom-espace de travail>sensorapi.atp.azure.com : pour la connectivité des capteurs. Par exemple, contosoATPsensorapi.atp.azure.com

 
> [!NOTE]
> Lors de l’inspection SSL sur le trafic réseau Azure ATP (entre le capteur et le service Azure ATP), l’inspection SSL doit prendre en charge une inspection mutuelle.


## <a name="see-also"></a>Voir aussi
- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)