---
title: 'Démarrage rapide : Télécharger le package d’installation du capteur Azure ATP | Microsoft Docs'
description: La troisième étape de la procédure d’installation d’Azure ATP vous permet de télécharger le package d’installation du capteur Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
ms.date: 02/05/2019
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.openlocfilehash: 8648e3bacadaa64570e127ce3728c33f87d3393c
ms.sourcegitcommit: 96752da28f43896e7b8e5945947b32c4810bdff6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/07/2019
ms.locfileid: "55831427"
---
# <a name="quickstart-download-the-azure-atp-sensor-setup-package"></a>Démarrage rapide : Télécharger le package d’installation de capteur Azure ATP

Dans ce guide de démarrage rapide, vous allez télécharger le package d’installation du capteur Azure ATP à partir du portail.

## <a name="prerequisites"></a>Prérequis

- Une [instance Azure ATP](install-atp-step1.md) qui est [connectée à Active Directory](install-atp-step2.md).

## <a name="download-the-setup-package"></a>Télécharger le package d’installation

Après avoir configuré les paramètres de connectivité du domaine, vous pouvez télécharger le package d’installation de capteur Azure ATP. Le package d’installation de capteur Azure ATP peut être installé sur un serveur dédié ou sur un contrôleur de domaine. Quand vous l’installez directement sur un contrôleur de domaine, il est installé en tant que capteur Azure ATP. Si vous l’installez sur un serveur dédié et que vous utilisez la mise en miroir de port, il est installé en tant que capteur autonome Azure ATP. Pour plus d’informations sur le capteur Azure ATP, consultez [Architecture Azure ATP](atp-architecture.md). 

Cliquez sur **Télécharger** dans la liste des étapes en haut de la page pour accéder à la page **Capteur**.

![Paramètres de configuration de capteur Azure ATP](media/atp-sensor-config.png)

 Pour accéder ultérieurement à l’écran de configuration du capteur, cliquez sur l’**icône de paramètres** (en haut à droite) et sélectionnez **Configuration** puis, sous **Système**, cliquez sur **Capteur**.  

1. Cliquez sur **capteur**.
2. Enregistrez le package localement.
3. Copiez la **clé** **d’accès**. Le capteur Azure ATP a besoin de la clé d’accès pour se connecter à votre instance Azure ATP. La clé d’accès est un mot de passe à usage unique pour le déploiement du capteur, après quoi toutes les communications sont effectuées à l’aide de certificats pour l’authentification et le chiffrement TLS. Utilisez le bouton **Regénérer** si vous avez besoin de regénérer la clé d’accès. Vous pouvez le faire sans que cela n’affecte les capteurs déjà déployés, car elle est utilisée uniquement pour l’inscription initiale du capteur.
4. Copiez le package sur le serveur dédié ou le contrôleur de domaine sur lequel vous installez le capteur Azure ATP. Vous pouvez aussi ouvrir le portail Azure ATP à partir du serveur dédié ou du contrôleur de domaine et ignorer cette étape.

Le fichier zip comprend les fichiers suivants :

- Programme d’installation du capteur Azure ATP

- Fichier de paramètres de configuration contenant les informations requises pour vous connecter au service cloud Azure ATP

## <a name="next-steps"></a>Étapes suivantes

> [!div class="step-by-step"]
> [« Étape 2 : Se connecter à Active Directory](install-atp-step2.md)
> [Étape 4 : Installer le capteur Azure ATP »](install-atp-step4.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://aka.ms/azureatpcommunity) dès aujourd’hui !