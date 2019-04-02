---
title: Configurer votre proxy ou pare-feu pour permettre la communication d’Azure ATP avec le capteur | Microsoft Docs
description: Décrit comment configurer votre pare-feu ou proxy pour permettre la communication entre le service cloud Azure ATP et les capteurs Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4bb2c2941cc0571b066f2fa4806217a67ebc7849
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2019
ms.locfileid: "58673786"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Configurer le proxy du point de terminaison et les paramètres de connectivité Internet pour le capteur Azure ATP

Chaque capteur Azure Advanced Threat Protection (ATP) requiert une connectivité Internet au service cloud Azure ATP pour fonctionner correctement. Dans certaines organisations, les contrôleurs de domaine ne sont pas connectés directement à Internet, mais plutôt par le biais d’une connexion de proxy web. Chaque capteur Azure ATP nécessite que vous utilisiez la configuration de proxy de Microsoft Windows Internet (WinINET) pour signaler les données de capteur et communiquer avec le service Azure ATP. Si vous utilisez WinHTTP pour la configuration du proxy, vous devez toujours configurer les paramètres de proxy de navigateur Windows Internet (WinINet) pour la communication entre le capteur et le service cloud Azure ATP.


Quand vous configurez le proxy, vous devez savoir que le service de capteur Azure ATP incorporé s’exécute dans le contexte du système à l’aide du compte **LocalService**, et que le service de mise à jour du capteur Azure ATP s’exécute dans le contexte du système à l’aide du compte **LocalSystem**. 

> [!NOTE]
> Si vous utilisez un proxy transparent ou WPAD dans votre topologie de réseau, vous n’avez pas besoin de configurer WinINET pour votre proxy.

## <a name="configure-the-proxy"></a>Configurer le proxy 

Configurez votre serveur proxy manuellement à l’aide d’un proxy statique basé sur le Registre pour permettre au capteur Azure ATP de signaler des données de diagnostic et de communiquer avec le service cloud Azure ATP quand un ordinateur n’est pas autorisé à se connecter à Internet.

> [!NOTE]
> Les modifications de Registre doivent être appliquées uniquement à LocalService et à LocalSystem.

Le proxy statique est configurable par le biais du Registre. Vous devez copier la configuration du proxy que vous utilisez dans le contexte de l’utilisateur pour localsystem et localservice. Pour copier vos paramètres de proxy du contexte de l’utilisateur :

1.   Veillez à sauvegarder les clés de Registre avant de les modifier.

2. Dans le Registre, recherchez la valeur `DefaultConnectionSettings` comme REG_BINARY sous la clé de Registre `HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` et copiez-la.
 
2.  Si LocalSystem n’a pas les paramètres de proxy appropriés (non configurés ou différents de Current_User), alors copiez le paramètre de proxy de Current_User vers LocalSystem. Sous la clé de Registre `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

3.  Collez la valeur de Current_user `DefaultConnectionSettings` comme REG_BINARY.

4.  Si LocalService n’a pas les paramètres de proxy appropriés, alors copiez le paramètre de proxy à partir de Current_User vers LocalService. Sous la clé de Registre `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

5.  Collez la valeur de Current_User `DefaultConnectionSettings` comme REG_BINARY.

> [!NOTE]
> Toutes les applications sont concernées, notamment les services Windows qui utilisent WinINET avec le contexte LocalService, LocalSytem.


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Activer l’accès aux URL du service Azure ATP dans le serveur proxy

Pour activer l’accès à Azure ATP, autorisez le trafic vers les URL suivantes :

- \<<nom-instance>.atp.azure.com (pour la connectivité de la console). Par exemple, « Contoso-corp.atp.azure.com »

- \<<nom-instance>sensorapi.atp.azure.com (pour la connectivité des capteurs). Par exemple, « contoso-corpsensorapi.atp.azure.com »

Les URL précédentes mappent automatiquement vers l’emplacement de service correspondant à votre instance Azure ATP. Si vous avez besoin d’un contrôle plus précis, autorisez le trafic vers les points de terminaison appropriés dans le tableau suivant :

|Emplacement du service|Enregistrement DNS *.atp.azure.com|
|----|----|
|FR |triprd1wcusw1sensorapi.atp.azure.com<br>triprd1wcuswb1sensorapi.atp.azure.com<br>triprd1wcuse1sensorapi.atp.azure.com|
|Europe|triprd1wceun1sensorapi.atp.azure.com<br>triprd1wceuw1sensorapi.atp.azure.com|
|Asie|triprd1wcasse1sensorapi.atp.azure.com|

 
> [!NOTE]
> Lors de l’inspection SSL sur le trafic réseau Azure ATP (entre le capteur et le service Azure ATP), l’inspection SSL doit prendre en charge une inspection mutuelle.


## <a name="see-also"></a>Voir aussi
- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
