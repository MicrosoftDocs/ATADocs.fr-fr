---
title: 'Démarrage rapide : Télécharger le package d’installation de capteur Azure ATP'
description: La troisième étape de la procédure d’installation d’Azure ATP vous permet de télécharger le package d’installation du capteur Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 02/19/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.openlocfilehash: 04e1df3e375d48c17a42590521b9de06373f4799
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910228"
---
# <a name="quickstart-download-the-azure-atp-sensor-setup-package"></a>Démarrage rapide : Télécharger le package d’installation de capteur Azure ATP

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Dans ce guide de démarrage rapide, vous allez télécharger le package d’installation du capteur Azure ATP à partir du portail.

## <a name="prerequisites"></a>Prérequis

- Une [instance Azure ATP](install-step1.md) qui est [connectée à Active Directory](install-step2.md).

## <a name="download-the-setup-package"></a>Télécharger le package d’installation

Après avoir configuré les paramètres de connectivité du domaine, vous pouvez télécharger le package d’installation de capteur Azure ATP. Pour plus d’informations sur le capteur Azure ATP, consultez [Architecture Azure ATP](architecture.md).

Cliquez sur **Télécharger** dans la liste des étapes en haut de la page pour accéder à la page **Capteur**.

![Paramètres de configuration de capteur Azure ATP](media/atp-sensor-config.png)

 Pour accéder ultérieurement à l’écran de configuration du capteur, cliquez sur l’**icône de paramètres** (en haut à droite) et sélectionnez **Configuration** puis, sous **Système**, cliquez sur **Capteur**.  

1. Cliquez sur **capteur**.
1. Enregistrez le package localement.
1. Copiez la **clé d’** **accès**. Le capteur Azure ATP a besoin de la clé d’accès pour se connecter à votre instance Azure ATP. La clé d’accès est un mot de passe à usage unique pour le déploiement du capteur, après quoi toutes les communications sont effectuées à l’aide de certificats pour l’authentification et le chiffrement TLS. Utilisez le bouton **Regénérer** si vous avez besoin de regénérer la clé d’accès. Vous pouvez le faire sans que cela n’affecte les capteurs déjà déployés, car elle est utilisée uniquement pour l’inscription initiale du capteur.
1. Copiez le package sur le serveur dédié ou le contrôleur de domaine sur lequel vous installez le capteur Azure ATP. Vous pouvez aussi ouvrir le portail Azure ATP à partir du serveur dédié ou du contrôleur de domaine et ignorer cette étape.

Le fichier zip comprend les fichiers suivants :

- Programme d’installation du capteur Azure ATP

- Fichier de paramètres de configuration contenant les informations requises pour vous connecter au service cloud Azure ATP

## <a name="next-steps"></a>Étapes suivantes

> [!div class="step-by-step"]
> [« Étape 2 : Se connecter à Active Directory](install-step2.md)
> [Étape 4 : Installer le capteur Azure ATP »](install-step4.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://aka.ms/azureatpcommunity) dès aujourd’hui !
