---
title: Installer sans assistance Azure Advanced Threat Protection | Microsoft Docs
description: Cet article décrit comment installer sans assistance Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 12/05/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1b82f850fd2159ec779243b888d2493d1ab28695
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56263815"
---
# <a name="azure-atp-switches-and-silent-installation"></a>Commutateurs et installation sans assistance d’Azure ATP
Cet article fournit des instructions pour les commutateurs et l’installation sans assistance d’Azure ATP.

## <a name="prerequisites"></a>Prérequis

Azure ATP nécessite l’installation de Microsoft .NET Framework 4.7. 

Quand vous installez Azure ATP, le .Net Framework 4.7 est automatiquement installé dans le cadre du déploiement d’Azure ATP.

> [!IMPORTANT] 
> Vérifiez que la dernière version du .Net Framework est installée. Si une version antérieure du .Net est installée, votre installation sans assistance d’Azure ATP reste bloquée dans une boucle et échoue. 

> [!NOTE] 
> L’installation du .Net Framework 4.7 peut nécessiter le redémarrage du serveur. Quand vous installez le capteur Azure ATP sur des contrôleurs de domaine, pensez à planifier une fenêtre de maintenance pour ces derniers.
Quand vous utilisez l’installation sans assistance d’Azure ATP, le programme d’installation est configuré pour redémarrer automatiquement le serveur à la fin de l’installation (si nécessaire). Veillez à exécuter une installation sans assistance uniquement pendant une fenêtre de maintenance. En raison d’un bogue de Windows Installer, l’indicateur *norestart* ne peut pas être utilisé de façon fiable pour s’assurer que le serveur ne redémarre pas.

Pour suivre la progression du déploiement, surveillez les journaux d’installation d’Azure ATP, qui se trouvent dans **%AppData%\Local\Temp**.


## <a name="azure-atp-sensor-silent-installation"></a>Installation sans assistance du capteur Azure ATP

> [!NOTE]
> En cas de déploiement sans assistance du capteur Azure ATP avec System Center Configuration Manager ou un autre système de déploiement de logiciels, il est recommandé de créer deux packages de déploiement :</br>- .NET Framework 4.7, en prévoyant éventuellement le redémarrage du contrôleur de domaine</br>- Capteur Azure ATP </br>Rendez le package du capteur Azure ATP dépendant du déploiement du package .NET Framework. </br>Obtenez le [package de déploiement hors connexion .NET Framework 4.7](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows). 


Utilisez la commande suivante pour effectuer une installation sans assistance complète du capteur Azure ATP :


**Syntaxe** :

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"

> [!NOTE]
> Copiez la clé d’accès à partir de la section **Configuration**, page **Capteur** du portail Azure ATP.


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
> |AccessKey|AccessKey="\*\*"|Oui|Définit la clé d’accès utilisée pour inscrire le capteur Azure ATP auprès de l’instance Azure ATP.|

**Exemples** : Utilisez la commande suivante pour installer sans assistance le capteur Azure ATP :

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="mmAOkLYCzfH8L/zUIsH24BIJBevlAWu7wUcSfIkRJufpuEojaDHYdjrNs0P3zpD+/bObKfLS0puD7biT5KDf3g=="


## <a name="update-the-azure-atp-sensor"></a>Mettre à jour le capteur Azure ATP

Utilisez la commande suivante pour mettre à jour sans assistance le capteur Azure ATP :

**Syntaxe** :

    Azure ATP sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Options d’installation** :

> [!div class="mx-tableFixed"]
> 
> |Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
> |Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|


**Exemples** : pour mettre à jour le capteur Azure ATP sans assistance :

    Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Désinstaller sans assistance le capteur Azure ATP

Utilisez la commande suivante pour effectuer une désinstallation sans assistance du capteur Azure ATP : **Syntaxe** :

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]

**Options d’installation** :

> [!div class="mx-tableFixed"]
> 
> |Nom|Syntaxe|Obligatoire pour une désinstallation sans assistance ?|Description|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Oui|Exécute le programme de désinstallation sans afficher d’interface utilisateur, ni d’invites.|
> |Désinstaller|/uninstall|Oui|Exécute la désinstallation sans assistance du capteur Azure ATP du serveur.|
> |Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|

**Exemples** : pour désinstaller le capteur Azure ATP du serveur sans assistance :


    Azure ATP sensor Setup.exe /quiet /uninstall




## <a name="see-also"></a>Voir aussi

- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Installer le capteur Azure ATP](install-atp-step4.md)
- [Configurer le capteur Azure ATP](install-atp-step5.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
