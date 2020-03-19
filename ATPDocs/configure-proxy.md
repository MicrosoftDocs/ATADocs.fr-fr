---
title: Configurer votre proxy ou pare-feu pour permettre la communication d’Azure ATP avec le capteur
description: Décrit comment configurer votre pare-feu ou proxy pour permettre la communication entre le service cloud Azure ATP et les capteurs Azure ATP
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a1e8065f5a1898301439c160c2a877cabe750928
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79413823"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Configurer le proxy du point de terminaison et les paramètres de connectivité Internet pour le capteur Azure ATP

Chaque capteur Azure Advanced Threat Protection (ATP) requiert une connectivité Internet au service cloud Azure ATP pour fonctionner correctement. Dans certaines organisations, les contrôleurs de domaine ne sont pas connectés directement à Internet, mais plutôt par le biais d’une connexion de proxy web. Chaque capteur Azure ATP nécessite que vous utilisiez la configuration de proxy de Microsoft Windows Internet (WinINET) pour signaler les données de capteur et communiquer avec le service Azure ATP. Si vous utilisez WinHTTP pour la configuration du proxy, vous devez toujours configurer les paramètres de proxy de navigateur Windows Internet (WinINet) pour la communication entre le capteur et le service cloud Azure ATP.

Quand vous configurez le proxy, souvenez-vous que le service de capteur Azure ATP incorporé s’exécute dans le contexte du système à l’aide du compte **LocalService** et que le service de mise à jour du capteur Azure ATP s’exécute dans le contexte du système à l’aide du compte **LocalSystem**.

> [!NOTE]
> Si vous utilisez un proxy transparent ou WPAD dans votre topologie de réseau, vous n’avez pas besoin de configurer WinINET pour votre proxy.

## <a name="configure-the-proxy"></a>Configurer le proxy

Vous pouvez configurer vos paramètres proxy pendant l'installation du capteur en utilisant les paramètres définis dans [Installation silencieuse, paramètres d'authentification proxy](https://docs.microsoft.com/azure-advanced-threat-protection/atp-silent-installation#proxy-authentication).

### <a name="proxy-authentication"></a>Authentification du proxy

Utilisez les commandes suivantes pour effectuer l’authentification du proxy :

**Syntaxe** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="https\://proxy.contoso.com:8080"|Non|Spécifie l’URL du proxy et le numéro de port pour le capteur Azure ATP.|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Non|Si votre service de proxy nécessite une authentification, spécifiez un nom d’utilisateur au format DOMAINE\utilisateur.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Non|Spécifie le mot de passe du nom d’utilisateur du proxy. *Les informations d’identification sont chiffrées et stockées localement par le capteur Azure ATP.|

Vous pouvez également configurer votre serveur proxy manuellement à l’aide d’un proxy statique basé sur le Registre pour permettre au capteur Azure ATP de signaler des données de diagnostic et de communiquer avec le service cloud Azure ATP quand un ordinateur n’est pas autorisé à se connecter à Internet.

> [!NOTE]
> Les modifications de Registre doivent être appliquées uniquement à LocalService et à LocalSystem.

Le proxy statique est configurable par le biais du Registre. Vous devez copier la configuration du proxy que vous utilisez dans le contexte de l’utilisateur pour localsystem et localservice. Pour copier vos paramètres de proxy du contexte de l’utilisateur :

1. Veillez à sauvegarder les clés de Registre avant de les modifier.

1. Dans le Registre, recherchez la valeur `DefaultConnectionSettings` comme REG_BINARY sous la clé de Registre `HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` et copiez-la.

1. Si LocalSystem n’a pas les paramètres de proxy appropriés (non configurés ou différents de Current_User), alors copiez le paramètre de proxy de Current_User vers LocalSystem. Sous la clé de Registre `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

1. Collez la valeur de Current_user `DefaultConnectionSettings` comme REG_BINARY.

1. Si LocalService n’a pas les paramètres de proxy appropriés, alors copiez le paramètre de proxy à partir de Current_User vers LocalService. Sous la clé de Registre `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

1. Collez la valeur de Current_User `DefaultConnectionSettings` comme REG_BINARY.

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
>
> - Pour garantir la sécurité maximale et la confidentialité des données, Azure ATP utilise l’authentification mutuelle basée sur les certificats entre chaque capteur Azure ATP et le back-end cloud Azure ATP. Si l’inspection SSL est utilisée dans votre environnement, assurez-vous que l’inspection est configurée pour l’authentification mutuelle, de sorte qu’elle n’interfère pas dans le processus d’authentification.
> - Vous pouvez également utiliser notre balise de service Azure (**AzureAdvancedThreatProtection**) pour activer l’accès à Azure ATP. Pour plus d’informations sur les balises de service, consultez les fichiers sur les [balises de service de réseau virtuel](https://docs.microsoft.com/azure/virtual-network/service-tags-overview) ou sur le [téléchargement des balises de service](https://www.microsoft.com/download/details.aspx?id=56519).

## <a name="see-also"></a>Voir aussi

- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
