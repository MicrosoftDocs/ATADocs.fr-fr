---
title: 'Démarrage rapide : Télécharger le package d’installation du capteur Microsoft Defender pour Identity'
description: L’étape 3 de l’installation de Microsoft Defender pour Identity vous aide à télécharger le package d’installation du capteur Defender pour Identity.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 10/26/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b2d1978a822b8062422c41696043b1563d8bc893
ms.sourcegitcommit: 07a855b87931875bdeca14b152b13a36db79bfa8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2020
ms.locfileid: "94848514"
---
# <a name="quickstart-download-the-product-long-sensor-setup-package"></a>Démarrage rapide : Télécharger le package d’installation du capteur [!INCLUDE [Product long](includes/product-long.md)]

Dans ce guide de démarrage rapide, vous allez télécharger le package d’installation du capteur [!INCLUDE [Product long](includes/product-long.md)] à partir du portail.

## <a name="prerequisites"></a>Prérequis

- Une [instance [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md) qui est [connectée à Active Directory](install-step2.md).

## <a name="download-the-setup-package"></a>Télécharger le package d’installation

Après avoir configuré les paramètres de connectivité du domaine, vous pouvez télécharger le package d’installation du capteur [!INCLUDE [Product short](includes/product-short.md)]. Pour plus d’informations sur le capteur [!INCLUDE [Product short](includes/product-short.md)], consultez [Architecture [!INCLUDE [Product short](includes/product-short.md)]](architecture.md).

Cliquez sur **Télécharger** dans la liste des étapes en haut de la page pour accéder à la page **Capteurs**.

![Paramètres de configuration du capteur [!INCLUDE [Product short](includes/product-short.md)]](media/sensor-config.png)

Pour accéder ultérieurement à l’écran de configuration du capteur, sélectionnez **Configuration** puis, sous **Système**, cliquez sur **Capteurs**.  

1. Cliquez sur **Télécharger** pour enregistrer le package localement.
1. Copiez la **clé d’** **accès**. Le capteur [!INCLUDE [Product short](includes/product-short.md)] a besoin de la clé d’accès pour se connecter à votre instance [!INCLUDE [Product short](includes/product-short.md)]. La clé d’accès est un mot de passe à usage unique pour le déploiement du capteur, après quoi toutes les communications sont effectuées à l’aide de certificats pour l’authentification et le chiffrement TLS. Utilisez le bouton **Regénérer** si vous avez besoin de regénérer la clé d’accès. Vous pouvez le faire sans que cela n’affecte les capteurs déjà déployés, car elle est utilisée uniquement pour l’inscription initiale du capteur.
1. Copiez le package sur le serveur dédié ou le contrôleur de domaine sur lequel vous installez le capteur [!INCLUDE [Product short](includes/product-short.md)]. Vous pouvez aussi ouvrir le portail [!INCLUDE [Product short](includes/product-short.md)] à partir du serveur dédié ou du contrôleur de domaine et ignorer cette étape.

Le fichier zip comprend les fichiers suivants :

- Programme d’installation du capteur [!INCLUDE [Product short](includes/product-short.md)]

- Fichier de paramètres de configuration contenant les informations requises pour vous connecter au service cloud [!INCLUDE [Product short](includes/product-short.md)]

## <a name="next-steps"></a>Étapes suivantes

> [!div class="step-by-step"]
> [« Étape 2 : Se connecter à Active Directory](install-step2.md)
> [Étape 4 : Installer le capteur [!INCLUDE [Product short](includes/product-short.md)] »](install-step4.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter de [!INCLUDE [Product short](includes/product-short.md)] et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity) !
