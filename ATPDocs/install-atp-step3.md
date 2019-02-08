---
title: Installer Azure Advanced Threat Protection | Microsoft Docs
description: La troisième étape de la procédure d’installation d’Azure ATP vous permet de télécharger le package d’installation du capteur Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4816fe56b8a28d349c970be5a304d025875de748
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085229"
---
# <a name="install-azure-atp---step-3"></a>Installer Azure ATP – Étape 3

> [!div class="step-by-step"]
> [« Étape 2](install-atp-step2.md)
> [Étape 4 »](install-atp-step4.md)

## <a name="download-the-azure-atp-sensor-setup-package"></a>Télécharger le package d’installation de capteur Azure ATP
Après avoir configuré les paramètres de connectivité du domaine, vous pouvez télécharger le package d’installation de capteur Azure ATP. Le package d’installation de capteur Azure ATP peut être installé sur un serveur dédié ou sur un contrôleur de domaine. Lorsque vous l’installez directement sur un contrôleur de domaine, il est installé en tant que capteur Azure ATP. Si vous l’installez sur un serveur dédié et utilisez la mise en miroir de port, il est installé en tant que capteur autonome Azure ATP. Pour plus d’informations sur le capteur Azure ATP, consultez [Architecture Azure ATP](atp-architecture.md). 

Cliquez sur **Télécharger** dans la liste des étapes en haut de la page pour accéder à la page **Capteur**.

![Paramètres de configuration de capteur Azure ATP](media/atp-sensor-config.png)

> [!NOTE] 
> Pour accéder ultérieurement à l’écran de configuration de capteur, cliquez sur l’**icône de paramètres** (en haut à droite) et sélectionnez **Configuration**, puis, sous **Système**, cliquez sur **capteur**.  

1.  Cliquez sur **capteur**.
2.  Enregistrez le package localement.
3.  Copiez la **clé** **d’accès**. Le capteur Azure ATP a besoin de la clé d’accès pour se connecter à votre instance Azure ATP. La clé d’accès est un mot de passe à usage unique pour le déploiement du capteur, après quoi toutes les communications sont effectuées à l’aide de certificats pour l’authentification et le chiffrement TLS. Utilisez le bouton **Régénérer** si vous avez besoin de regénérer la clé d’accès. Vous pouvez le faire sans que cela n’affecte les capteurs déjà déployés, car elle est utilisée uniquement pour l’inscription initiale du capteur.
4.  Copiez le package sur le serveur dédié ou le contrôleur de domaine sur lequel vous installez le capteur Azure ATP. Vous pouvez aussi ouvrir le portail Azure ATP à partir du serveur dédié ou du contrôleur de domaine et ignorer cette étape.

Le fichier zip comprend les fichiers suivants :

-   Programme d’installation du capteur Azure ATP

-   Fichier de paramètres de configuration contenant les informations requises pour vous connecter au service cloud Azure ATP


> [!div class="step-by-step"]
> [« Étape 2](install-atp-step2.md)
> [Étape 4 »](install-atp-step4.md)


## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)

- [Configurer la collecte d’événements](configure-event-collection.md)

- [Prérequis d’Azure ATP](atp-prerequisites.md)

- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)