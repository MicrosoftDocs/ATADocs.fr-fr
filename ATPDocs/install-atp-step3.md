---
title: Installer Azure - Protection avancée contre les menaces – Étape 3 | Microsoft Docs
description: La troisième étape de la procédure d’installation d’Azure ATP vous permet de télécharger le package d’installation de capteur autonome Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 96d459bd00d39bb21ce363d079b5b24ceca4ace7
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454018"
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="install-azure-atp---step-3"></a>Installer Azure ATP – Étape 3

> [!div class="step-by-step"]
> [« Étape 2](install-atp-step2.md)
> [Étape 4 »](install-atp-step4.md)

## <a name="step-3-download-the-azure-atp-sensor-setup-package"></a>Étape 3. Télécharger le package d’installation de capteur Azure ATP
Après avoir configuré les paramètres de connectivité du domaine, vous pouvez télécharger le package d’installation de capteur Azure ATP. Le package d’installation de capteur Azure ATP peut être installé sur un serveur dédié ou sur un contrôleur de domaine. Lorsque vous l’installez directement sur un contrôleur de domaine, il est installé en tant que capteur Azure ATP. Si vous l’installez sur un serveur dédié et utilisez la mise en miroir de port, il est installé en tant que capteur autonome Azure ATP. Pour plus d’informations sur le capteur Azure ATP, consultez [Architecture Azure ATP](atp-architecture.md). 

Cliquez sur **Télécharger** dans la liste des étapes en haut de la page pour accéder à la page **Capteur**.

![Paramètres de configuration de capteur Azure ATP](media/atp-sensor-config.png)

> [!NOTE] 
> Pour accéder ultérieurement à l’écran de configuration de capteur, cliquez sur l’**icône de paramètres** (en haut à droite) et sélectionnez **Configuration**, puis, sous **Système**, cliquez sur **capteur**.  

1.  Cliquez sur **capteur**.
2.  Enregistrez le package localement.
3.  Copiez la **clé d’accès**. La clé d’accès est nécessaire à la connexion du capteur Azure ATP à votre espace de travail Azure ATP. La clé d’accès est un mot de passe à usage unique pour le déploiement du capteur, après quoi toutes les communications sont effectuées à l’aide de certificats pour l’authentification et le chiffrement TLS. Utilisez le bouton **Régénérer** si vous avez besoin de regénérer la clé d’accès. Vous pouvez le faire sans que cela n’affecte les capteurs déjà déployés, car elle est utilisée uniquement pour l’inscription initiale du capteur.
4.  Copiez le package sur le serveur dédié ou le contrôleur de domaine sur lequel vous installez le capteur Azure ATP. Vous pouvez également ouvrir le portail d’espace de travail Azure ATP à partir du serveur dédié ou du contrôleur de domaine et ignorer cette étape.

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

- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)