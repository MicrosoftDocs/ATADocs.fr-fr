---
title: Installer Advanced Threat Analytics en mode silencieux
description: Cet article explique comment installer ATA en mode silencieux.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/20/2020
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 74d610899023eba93da568360a99505119d13e70
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90908856"
---
# <a name="ata-silent-installation"></a>Installation en mode silencieux ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Cet article fournit des instructions pour installer ATA sans assistance.

## <a name="prerequisites"></a>Prérequis

ATA version 1,9 nécessite l’installation de Microsoft .NET Framework 4.6.1.

Quand vous installez ou mettez à jour ATA, .Net Framework 4.6.1 est automatiquement installé dans le cadre du déploiement de Microsoft ATA.

> [!Note]
> L’installation de .Net Framework 4.6.1 peut nécessiter le redémarrage du serveur. Quand vous installez la passerelle ATA sur des contrôleurs de domaine, pensez à planifier une fenêtre de maintenance pour ces derniers. Quand vous utilisez la méthode d’installation d’ATA sans assistance, le programme d’installation est configuré pour redémarrer automatiquement le serveur à la fin de l’installation (si nécessaire). En raison d’un bogue de Windows Installer, l’indicateur norestart ne peut pas être utilisé de façon fiable pour vérifier que le serveur ne redémarre pas : veillez donc à exécuter seulement une installation sans assistance pendant une fenêtre de maintenance.

Pour suivre la progression du déploiement, surveillez les journaux du programme d’installation d’ATA, qui se trouvent dans **%AppData%\Local\Temp**.

## <a name="install-the-ata-center"></a>Installer le centre ATA

Utilisez la commande suivante pour installer le centre ATA :

**Syntaxe** :

```dos
"Microsoft ATA Center Setup.exe" [/quiet] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments="/q"] [InstallationPath="<InstallPath>"] [DatabaseDataPath= "<DBPath>"] [CertificateThumbprint="<CertThumbprint>"]
```

**Options d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |---|---|---|---|
> |Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
> |Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|
> |LicenseAccepted|--LicenseAccepted|Oui|Indique que la licence a été lue et approuvée. Doit être définie sur installation sans assistance.|

**Paramètres d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |---|---|---|---|
>|InstallationPath|InstallationPath="<InstallPath>"|Non|Définit le chemin de l’installation des fichiers binaires ATA. Chemin par défaut : C:\Program Files\Microsoft Advanced Threat Analytics\Center|
>|DatabaseDataPath|DatabaseDataPath= "<DBPath>"|Non|Définit le chemin du dossier des données de la base de données ATA. Chemin par défaut : C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|
>|CenterCertificateThumbprint|CenterCertificateThumbprint="<CertThumbprint>"|Non|Définit l’empreinte numérique du certificat pour le centre ATA. Ce certificat est utilisé pour sécuriser la communication entre la passerelle ATA et le centre ATA et pour valider l’identité du site Web de la console ATA. Si ce paramètre n’est pas défini, l’installation génère un certificat auto-signé.|

**Exemple** :

Pour installer le centre ATA avec les chemins d’installation par défaut et l’empreinte numérique du certificat défini par l’utilisateur :

```dos
"Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F"
```

## <a name="update-the-ata-center"></a>Mettez à jour le centre ATA.

Utilisez la commande suivante pour mettre à jour le centre ATA :

**Syntaxe** :

```dos
"Microsoft ATA Center Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]
```

**Options d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |---|---|---|---|
> |Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
> |Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|

Pendant la mise à jour d’ATA, le programme d’installation détecte automatiquement qu’ATA est déjà installé sur le serveur, et aucune option d’installation de mise à jour n’est requise.

**Exemples** :

Pour mettre à jour le centre ATA sans assistance. Dans les environnements de grande taille, la mise à jour du centre ATA peut prendre un certain temps. Surveillez les journaux ATA pour suivre la progression de la mise à jour.

```dos
"Microsoft ATA Center Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

## <a name="uninstall-the-ata-center-silently"></a>Désinstaller le centre ATA sans assistance

Utilisez la commande suivante pour effectuer une désinstallation sans assistance du centre ATA :

**Syntaxe** :

```dos
"Microsoft ATA Center Setup.exe" [/quiet] [/Uninstall] [/Help] [--DeleteExistingDatabaseData]
```

**Options d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une désinstallation sans assistance ?|Description|
> |---|---|---|---|
> |Quiet|/quiet|Oui|Exécute le programme de désinstallation sans afficher d’interface utilisateur, ni d’invites.|
> |Désinstaller|/uninstall|Oui|Exécute la désinstallation sans assistance du centre ATA du serveur.|
> |Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|

**Paramètres d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une désinstallation sans assistance ?|Description|
> |---|---|---|---|
> |DeleteExistingDatabaseData|DeleteExistingDatabaseData|Non|Supprime tous les fichiers de la base de données existante.|

**Exemples** :

Pour désinstaller sans assistance le centre ATA du serveur, en supprimant toutes les données de base de données existantes :

```dos
"Microsoft ATA Center Setup.exe" /quiet /uninstall --DeleteExistingDatabaseData
```

## <a name="ata-gateway-silent-installation"></a>Installation sans assistance de la passerelle ATA

> [!NOTE]
> En cas de déploiement sans assistance de la passerelle légère ATA avec System Center Configuration Manager ou un autre système de déploiement de logiciels, il est recommandé de créer deux packages de déploiement :</br>- .NET Framework 4.6.1, avec redémarrage du contrôleur de domaine ;</br>- la passerelle ATA. </br>Faites en sorte que le package de la passerelle ATA dépende du déploiement du package .NET Framework. </br>Obtenir le [package de déploiement hors connexion .NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49982).

Utilisez la commande suivante pour installer la passerelle ATA sans assistance :

**Syntaxe** :

```dos
"Microsoft ATA Gateway Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"] [ConsoleAccountName="<AccountName>"] [ConsoleAccountPassword="<AccountPassword>"]
```

> [!NOTE]
> Si vous travaillez sur un ordinateur joint au domaine et que vous vous êtes connecté à l’aide de votre nom d’utilisateur et de votre mot de passe d’administrateur ATA, vous n’avez pas à fournir vos informations d’identification ici.

**Options d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |---|---|---|---|
> |Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
> |Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|

**Paramètres d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |---|---|---|---|
>|InstallationPath|InstallationPath="<InstallPath>"|Non|Définit le chemin de l’installation des fichiers binaires ATA. Chemin par défaut : C:\Program Files\Microsoft Advanced Threat Analytics\Center
>|ConsoleAccountName|ConsoleAccountName="<AccountName>"|Oui|Définit le nom du compte d’utilisateur (user@domain.com) qui est utilisé pour inscrire la passerelle ATA auprès du centre ATA.|
>|ConsoleAccountPassword|ConsoleAccountPassword="<AccountPassword>"|Oui|Définit le mot de passe du compte d’utilisateur (user@domain.com) qui est utilisé pour inscrire la passerelle ATA auprès du centre ATA.|

**Exemples** :

pour installer la passerelle ATA sans assistance, connectez-vous à l’ordinateur joint au domaine avec vos informations d’identification d’administration ATA, pour éviter d’avoir à spécifier les informations d’identification dans le cadre de l'installation. Sinon, inscrivez-le auprès du centre ATA en utilisant les informations d’identification spécifiées :

```dos
"Microsoft ATA Gateway Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" ConsoleAccountName="user@contoso.com" ConsoleAccountPassword="userpwd"
```

## <a name="update-the-ata-gateway"></a>Mettre à jour la passerelle ATA

Utilisez la commande suivante pour mettre à jour la passerelle ATA sans assistance :

**Syntaxe** :

```dos
"Microsoft ATA Gateway Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]
```

**Options d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |---|---|---|---|
> |Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
> |Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|

**Exemples** :

Pour mettre à jour la passerelle ATA sans assistance :

```dos
"Microsoft ATA Gateway Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

## <a name="uninstall-the-ata-gateway-silently"></a>Désinstaller la passerelle ATA sans assistance

Utilisez la commande suivante pour effectuer une désinstallation sans assistance de la passerelle ATA :

**Syntaxe** :

```dos
"Microsoft ATA Gateway Setup.exe" [/quiet] [/Uninstall] [/Help]
```

**Options d’installation** :

> [!div class="mx-tableFixed"]
>
> |Nom|Syntaxe|Obligatoire pour une désinstallation sans assistance ?|Description|
> |---|---|---|---|
> |Quiet|/quiet|Oui|Exécute le programme de désinstallation sans afficher d’interface utilisateur, ni d’invites.|
> |Désinstaller|/uninstall|Oui|Exécute la désinstallation sans assistance de la passerelle ATA du serveur.|
> |Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|

**Exemples** :

Pour désinstaller sans assistance la passerelle ATA du serveur :

```dos
"Microsoft ATA Gateway Setup.exe" /quiet /uninstall
```

## <a name="see-also"></a>Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](ata-prerequisites.md)
