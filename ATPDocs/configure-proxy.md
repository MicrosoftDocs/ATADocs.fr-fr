---
title: Configuration d’un proxy ou d’un pare-feu pour permettre la communication entre Microsoft Defender pour Identity et le capteur
description: Explique comment configurer un pare-feu ou un proxy de façon à permettre la communication entre le service Cloud Microsoft Defender pour Identity et les capteurs Microsoft Defender pour Identity.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 4606ab39457cbf1210974cb9f150d7410051c361
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543431"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-product-long-sensor"></a>Configuration des paramètres de proxy du point de terminaison et de connectivité Internet d’un capteur [!INCLUDE [Product long](includes/product-long.md)]

Chaque capteur [!INCLUDE [Product long](includes/product-long.md)] a besoin d’une connectivité Internet au service cloud [!INCLUDE [Product short](includes/product-short.md)] pour pouvoir envoyer ses données et fonctionner correctement. Dans certaines organisations, les contrôleurs de domaine ne sont pas connectés directement à Internet, mais plutôt par le biais d’une connexion de proxy web.

Pour configurer votre serveur proxy, nous vous recommandons de veiller à ce que seuls les services de capteur [!INCLUDE [Product short](includes/product-short.md)] communiquent via le proxy en ligne de commande.

## <a name="configure-proxy-server-using-the-command-line"></a>Configurer un serveur proxy à l’aide de la ligne de commande

Vous pouvez configurer votre serveur proxy lors de l’installation du capteur à l’aide des commutateurs de ligne de commande suivants.

### <a name="syntax"></a>Syntaxe

"Azure ATP sensor Setup.exe" [/quiet] [/Help] [ProxyUrl="http://proxy.internal.com"] [ProxyUserName="domain\proxyuser"] [ProxyUserPassword="ProxyPassword"]

### <a name="switch-descriptions"></a>Descriptions des commutateurs

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="http\://proxy.contoso.com:8080"|Non|Spécifie l’URL du proxy et le numéro de port du capteur [!INCLUDE [Product short](includes/product-short.md)].|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Non|Si votre service de proxy nécessite une authentification, spécifiez un nom d’utilisateur au format DOMAINE\utilisateur.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Non|Spécifie le mot de passe du nom d’utilisateur du proxy. \* Les informations d’identification sont chiffrées et stockées en local par le capteur [!INCLUDE [Product short](includes/product-short.md)].|

## <a name="alternative-methods-to-configure-your-proxy-server"></a>Autres méthodes pour configurer votre serveur proxy

Vous pouvez utiliser l’une des méthodes alternatives suivantes pour configurer votre serveur proxy. Quand vous configurez les paramètres de proxy avec ces méthodes, les autres services qui s’exécutent dans le contexte en tant que Système local ou Service local dirigent également le trafic via le proxy.

- [Configurer le serveur proxy avec WinINet](#configure-proxy-server-using-wininet)
- [Configurer le serveur proxy avec le Registre](#configure-proxy-server-using-the-registry)

### <a name="configure-proxy-server-using-wininet"></a>Configurer le serveur proxy avec WinINet

Vous pouvez configurer votre serveur proxy suivant la configuration Microsoft Windows Internet (WinInet) pour permettre au capteur [!INCLUDE [Product short](includes/product-short.md)] d’envoyer des données de diagnostic et de communiquer avec le service cloud [!INCLUDE [Product short](includes/product-short.md)] quand un ordinateur n’est pas autorisé à se connecter à Internet. Si vous utilisez WinHTTP pour la configuration du proxy, vous devez quand même configurer les paramètres de proxy de navigateur Windows Internet (WinInet) pour la communication entre le capteur et le service cloud [!INCLUDE [Product short](includes/product-short.md)].

Quand vous configurez le proxy, n’oubliez pas que le service de capteur [!INCLUDE [Product short](includes/product-short.md)] incorporé s’exécute dans le contexte du système à l’aide du compte **LocalService**, tandis que le service de mise à jour du capteur [!INCLUDE [Product short](includes/product-short.md)] s’exécute dans le contexte du système à l’aide du compte **LocalSystem**.

> [!NOTE]
> Si vous utilisez un proxy transparent ou WPAD dans votre topologie de réseau, vous n’avez pas besoin de configurer WinINet pour votre proxy.

### <a name="configure-proxy-server-using-the-registry"></a>Configurer le serveur proxy avec le Registre

Vous pouvez également configurer manuellement votre serveur proxy à l’aide d’un proxy statique basé sur le Registre pour permettre au capteur [!INCLUDE [Product short](includes/product-short.md)] d’envoyer des données de diagnostic et de communiquer avec le service cloud [!INCLUDE [Product short](includes/product-short.md)] quand un ordinateur n’est pas autorisé à se connecter à Internet.

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

<a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>

## <a name="enable-access-to-product-short-service-urls-in-the-proxy-server"></a>Activation de l’accès aux URL du service [!INCLUDE [Product short](includes/product-short.md)] dans le serveur proxy

Pour activer l’accès à [!INCLUDE [Product short](includes/product-short.md)], nous vous recommandons d’autoriser le trafic à destination des URL suivantes. Les URL sont automatiquement mappées avec l’emplacement du service correspondant dans votre instance [!INCLUDE [Product short](includes/product-short.md)].

- `<your-instance-name>.atp.azure.com` – pour la connectivité de la console. Par exemple, `contoso-corp.atp.azure.com`

- `<your-instance-name>sensorapi.atp.azure.com` – pour la connectivité des capteurs. Par exemple, `contoso-corpsensorapi.atp.azure.com`

Vous pouvez également utiliser les plages d’adresses IP dans notre étiquette de service Azure (**AzureAdvancedThreatProtection**) pour activer l’accès à [!INCLUDE [Product short](includes/product-short.md)]. Pour plus d’informations sur les balises de service, consultez les fichiers sur les [balises de service de réseau virtuel](/azure/virtual-network/service-tags-overview) ou sur le [téléchargement des balises de service](https://www.microsoft.com/download/details.aspx?id=56519).

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
> - Pour garantir une sécurité et une confidentialité des données maximales, [!INCLUDE [Product short](includes/product-short.md)] utilise l’authentification mutuelle par certificat entre chaque capteur [!INCLUDE [Product short](includes/product-short.md)] et le back-end cloud [!INCLUDE [Product short](includes/product-short.md)]. Si l’inspection SSL est utilisée dans votre environnement, assurez-vous que l’inspection est configurée pour l’authentification mutuelle, de sorte qu’elle n’interfère pas dans le processus d’authentification.
> - Les adresses IP du service [!INCLUDE [Product short](includes/product-short.md)] sont susceptibles de changer de temps en temps. Par conséquent, si vous configurez manuellement des adresses IP ou si votre proxy résout automatiquement les noms DNS en leur adresse IP et les utilise, vous devez vérifier régulièrement que les adresses IP configurées sont toujours à jour.

## <a name="see-also"></a>Voir aussi

- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
