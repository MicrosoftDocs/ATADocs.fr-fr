---
title: Configurer votre proxy ou pare-feu pour permettre la communication d’Azure ATP avec le capteur
description: Décrit comment configurer votre pare-feu ou proxy pour permettre la communication entre le service cloud Azure ATP et les capteurs Azure ATP
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 69a05db012422fef78d7f693f0e12ffebe31c72b
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912442"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Configurer le proxy du point de terminaison et les paramètres de connectivité Internet pour le capteur Azure ATP

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Chaque capteur Azure Advanced Threat Protection (ATP) a besoin d’une connectivité Internet au service cloud Azure ATP pour signaler les données de capteur et fonctionner correctement. Dans certaines organisations, les contrôleurs de domaine ne sont pas connectés directement à Internet, mais plutôt par le biais d’une connexion de proxy web.

Pour configurer votre serveur proxy, nous vous recommandons d’utiliser la ligne de commande pour vous assurer que seuls les services de capteur Azure ATP communiquent via le proxy.

## <a name="configure-proxy-server-using-the-command-line"></a>Configurer un serveur proxy à l’aide de la ligne de commande

Vous pouvez configurer votre serveur proxy lors de l’installation du capteur à l’aide des commutateurs de ligne de commande suivants.

### <a name="syntax"></a>Syntaxe

"Azure ATP sensor Setup.exe" [/quiet] [/Help] [ProxyUrl="https://proxy.internal.com"] [ProxyUserName="domain\proxyuser"] [ProxyUserPassword="ProxyPassword"]

### <a name="switch-descriptions"></a>Descriptions des commutateurs

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="http\://proxy.contoso.com:8080"|Non|Spécifie l’URL du proxy et le numéro de port pour le capteur Azure ATP.|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Non|Si votre service de proxy nécessite une authentification, spécifiez un nom d’utilisateur au format DOMAINE\utilisateur.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Non|Spécifie le mot de passe du nom d’utilisateur du proxy. *Les informations d’identification sont chiffrées et stockées localement par le capteur Azure ATP.|

## <a name="alternative-methods-to-configure-your-proxy-server"></a>Autres méthodes pour configurer votre serveur proxy

Vous pouvez utiliser l’une des méthodes alternatives suivantes pour configurer votre serveur proxy. Quand vous configurez les paramètres de proxy avec ces méthodes, les autres services qui s’exécutent dans le contexte en tant que Système local ou Service local dirigent également le trafic via le proxy.

- [Configurer le serveur proxy avec WinINet](#configure-proxy-server-using-wininet)
- [Configurer le serveur proxy avec le Registre](#configure-proxy-server-using-the-registry)

### <a name="configure-proxy-server-using-wininet"></a>Configurer le serveur proxy avec WinINet

Vous pouvez configurer votre serveur proxy à l’aide d’une configuration de proxy Microsoft Windows Internet (WinINet) pour permettre au capteur Azure ATP de signaler des données de diagnostic et de communiquer avec le service cloud Azure ATP quand un ordinateur n’est pas autorisé à se connecter à Internet. Si vous utilisez WinHTTP pour la configuration du proxy, vous devez toujours configurer les paramètres de proxy de navigateur Windows Internet (WinINet) pour la communication entre le capteur et le service cloud Azure ATP.

Quand vous configurez le proxy, souvenez-vous que le service de capteur Azure ATP incorporé s’exécute dans le contexte du système à l’aide du compte **LocalService** et que le service de mise à jour du capteur Azure ATP s’exécute dans le contexte du système à l’aide du compte **LocalSystem**.

> [!NOTE]
> Si vous utilisez un proxy transparent ou WPAD dans votre topologie de réseau, vous n’avez pas besoin de configurer WinINet pour votre proxy.

### <a name="configure-proxy-server-using-the-registry"></a>Configurer le serveur proxy avec le Registre

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

Pour activer l’accès à Azure ATP, nous recommandons d’autoriser le trafic vers les URL suivantes. Les URL mappent automatiquement vers l’emplacement de service correspondant à votre instance Azure ATP.

- `<your-instance-name>.atp.azure.com` – pour la connectivité de la console. Par exemple, `contoso-corp.atp.azure.com`

- `<your-instance-name>sensorapi.atp.azure.com` – pour la connectivité des capteurs. Par exemple, `contoso-corpsensorapi.atp.azure.com`

Vous pouvez également utiliser les plages d’adresses IP dans notre étiquette de service Azure (**AzureAdvancedThreatProtection**) pour activer l’accès à Azure ATP. Pour plus d’informations sur les balises de service, consultez les fichiers sur les [balises de service de réseau virtuel](/azure/virtual-network/service-tags-overview) ou sur le [téléchargement des balises de service](https://www.microsoft.com/download/details.aspx?id=56519).

Sinon, si vous avez besoin d’un contrôle plus précis, autorisez le trafic vers les points de terminaison appropriés dans le tableau suivant :

|Emplacement du service|Enregistrement DNS *.atp.azure.com|
|----|----|
|FR |`triprd1wcusw2sensorapi.atp.azure.com`<br>`triprd1wcuswb3sensorapi.atp.azure.com`<br>`triprd1wcuse3sensorapi.atp.azure.com`|
|US GCC High|`https://triff1wcva2sensorapi.atp.azure.us`|
|Europe|`triprd1wceun2sensorapi.atp.azure.com`<br>`triprd1wceuw3sensorapi.atp.azure.com`|
|Asia|`triprd1wcasse2sensorapi.atp.azure.com`|
|Royaume-Uni|`triprd1wcuks2sensorapi.atp.azure.com`|

> [!NOTE]
>
> - Pour garantir la sécurité maximale et la confidentialité des données, Azure ATP utilise l’authentification mutuelle basée sur les certificats entre chaque capteur Azure ATP et le back-end cloud Azure ATP. Si l’inspection SSL est utilisée dans votre environnement, assurez-vous que l’inspection est configurée pour l’authentification mutuelle, de sorte qu’elle n’interfère pas dans le processus d’authentification.
> - Parfois, les adresses IP du service Azure ATP peuvent changer. Par conséquent, si vous configurez manuellement des adresses IP ou si votre proxy résout automatiquement les noms DNS en leur adresse IP et les utilise, vous devez vérifier régulièrement que les adresses IP configurées sont toujours à jour.

## <a name="see-also"></a>Voir aussi

- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)