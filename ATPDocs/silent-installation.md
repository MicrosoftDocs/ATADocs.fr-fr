---
title: Installer Microsoft Defender pour l’identité en mode silencieux
description: Cette rubrique décrit comment installer Microsoft Defender en mode silencieux pour l’identité.
ms.date: 01/11/2021
ms.topic: how-to
ms.openlocfilehash: 0c22f5bcbffd415a81b84c94570cfcd7387aab56
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534393"
---
# <a name="microsoft-defender-for-identity-switches-and-silent-installation"></a>Microsoft Defender pour les commutateurs d’identité et l’installation sans assistance

Cet article fournit des instructions et des instructions pour les [!INCLUDE [Product long](includes/product-long.md)] commutateurs et l’installation sans assistance.

## <a name="prerequisites"></a>Prérequis

[!INCLUDE [Product short](includes/product-short.md)] requiert l’installation de Microsoft .NET Framework 4,7 ou version ultérieure.

Quand vous installez [!INCLUDE [Product short](includes/product-short.md)] , .net framework 4,7 est installé automatiquement dans le cadre du déploiement de [!INCLUDE [Product short](includes/product-short.md)] si .net Framework 4,7 ou version ultérieure n’est pas déjà installé.

> [!NOTE]
> L’installation du .Net Framework 4.7 peut nécessiter le redémarrage du serveur. Lors de l’installation du [!INCLUDE [Product short](includes/product-short.md)] capteur sur les contrôleurs de domaine, envisagez de planifier une fenêtre de maintenance pour les contrôleurs de domaine.

À l’aide de l' [!INCLUDE [Product short](includes/product-short.md)] installation sans assistance, le programme d’installation est configuré pour redémarrer automatiquement le serveur à la fin de l’installation (si nécessaire). Veillez à exécuter une installation sans assistance uniquement pendant une fenêtre de maintenance. En raison d’un bogue de Windows Installer, l’indicateur *norestart* ne peut pas être utilisé de façon fiable pour s’assurer que le serveur ne redémarre pas.

Pour suivre la progression de votre déploiement, surveillez les [!INCLUDE [Product short](includes/product-short.md)] journaux du programme d’installation, qui se trouvent dans `%AppData%\Local\Temp` .

## <a name="defender-for-identity-sensor-silent-installation"></a>Defender pour l’installation sans assistance du capteur d’identité

> [!NOTE]
> Lors du déploiement silencieux du [!INCLUDE [Product short](includes/product-short.md)] capteur par le biais d’System Center Configuration Manager ou d’un autre système de déploiement de logiciels, il est recommandé de créer deux packages de déploiement :</br>- .NET Framework 4.7 (ou version ultérieure), en prévoyant éventuellement le redémarrage du contrôleur de domaine</br>- [!INCLUDE [Product short](includes/product-short.md)] cellule. </br>Rendez le [!INCLUDE [Product short](includes/product-short.md)] package de capteur dépendant du déploiement du package .NET Framework. </br>Obtenez le [package de déploiement hors connexion .NET Framework 4.7](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows).

Utilisez la commande suivante pour effectuer une installation entièrement silencieuse du [!INCLUDE [Product short](includes/product-short.md)] capteur :

**Syntaxe cmd.exe** :

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

**Syntaxe Powershell** :

```powershell
.\"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

> [!NOTE]
> Lorsque vous utilisez la syntaxe PowerShell, l’omission du préfixe **./** génère une erreur qui empêche l’installation sans assistance.

> [!NOTE]
> Copiez la clé d’accès à partir de la [!INCLUDE [Product short](includes/product-short.md)] section **configuration** du portail, **capteurs** .

**Options d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
> |Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|

**Paramètres d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |-------------|----------|---------|---------|
> |InstallationPath|InstallationPath=""|Non|Définit le chemin d’accès pour l’installation des [!INCLUDE [Product short](includes/product-short.md)] binaires de capteur. Chemin d’accès par défaut : %programfiles%\capteur Azure Advanced Threat Protection
> |AccessKey|AccessKey="\*\*"|Oui|Définit la clé d’accès utilisée pour inscrire le [!INCLUDE [Product short](includes/product-short.md)] capteur auprès de l' [!INCLUDE [Product short](includes/product-short.md)] instance.|

**Exemples** :

Utilisez la commande suivante pour installer le capteur en mode silencieux [!INCLUDE [Product short](includes/product-short.md)] :

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="mmAOkLYCzfH8L/zUIsH24BIJBevlAWu7wUcSfIkRJufpuEojaDHYdjrNs0P3zpD+/bObKfLS0puD7biT5KDf3g=="
```

## <a name="proxy-authentication"></a>Authentification du proxy

Utilisez les commandes suivantes pour effectuer l’authentification du proxy :

**Syntaxe** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="http\://proxy.contoso.com:8080"|Non|Spécifie l’URL du proxy et le numéro de port du capteur [!INCLUDE [Product short](includes/product-short.md)].|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Non|Si votre service de proxy nécessite une authentification, spécifiez un nom d’utilisateur au format DOMAINE\utilisateur.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Non|Spécifie le mot de passe du nom d’utilisateur du proxy. \* Les informations d’identification sont chiffrées et stockées en local par le capteur [!INCLUDE [Product short](includes/product-short.md)].|

Pour plus d’informations sur la configuration du proxy, consultez [configurer le proxy de point de terminaison et les paramètres de connectivité Internet pour votre [!INCLUDE [Product long](includes/product-long.md)] capteur](configure-proxy.md).

## <a name="update-the-defender-for-identity-sensor"></a>Mettre à jour l’Defender pour le capteur d’identité

Utilisez la commande suivante pour mettre à jour le capteur en mode silencieux [!INCLUDE [Product short](includes/product-short.md)] :

**Syntaxe** :

```dos
"Azure ATP sensor Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]
```

**Options d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
> |Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|

**Exemples** :

Pour mettre à jour le [!INCLUDE [Product short](includes/product-short.md)] capteur en mode silencieux :

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

<a name="silently-uninstall-sensor"></a>

## <a name="uninstall-the-defender-for-identity-sensor-silently"></a>Désinstallation de l’Defender pour le capteur d’identité en mode silencieux

Utilisez la commande suivante pour effectuer une désinstallation sans assistance du [!INCLUDE [Product short](includes/product-short.md)] capteur :

**Syntaxe** :

```dos
"Azure ATP sensor Setup.exe" [/quiet] [/Uninstall] [/Help]
```

**Options d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une désinstallation sans assistance ?|Description|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Oui|Exécute le programme de désinstallation sans afficher d’interface utilisateur, ni d’invites.|
> |Désinstaller|/uninstall|Oui|Exécute la désinstallation sans assistance du [!INCLUDE [Product short](includes/product-short.md)] capteur à partir du serveur.|
> |Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|

**Exemples** :

Pour désinstaller sans assistance le [!INCLUDE [Product short](includes/product-short.md)] capteur du serveur :

```dos
"Azure ATP sensor Setup.exe" /quiet /uninstall
```

## <a name="see-also"></a>Voir aussi

- [Prérequis de [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Installer le [!INCLUDE [Product short](includes/product-short.md)] capteur](install-step4.md)
- [Configurer le [!INCLUDE [Product short](includes/product-short.md)] capteur](install-step5.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
