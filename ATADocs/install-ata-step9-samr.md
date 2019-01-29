---
title: Configurer SAM-R pour activer la détection de chemin de mouvement latéral dans Advanced Threat Analytics | Microsoft Docs
description: Décrit comment configurer SAM-R pour activer la détection de chemin de mouvement latéral dans Advanced Threat Analytics (ATA)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/30/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 39d1e03eda182b797412e94ff5427bc74956113a
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54841013"
---
# <a name="install-ata---step-9"></a>Installer ATA - Étape 9

*S’applique à : Advanced Threat Analytics version 1.9*

> [!div class="step-by-step"]
> [« Étape 8](install-ata-step7.md)

## <a name="step-9-configure-sam-r-required-permissions"></a>Étape 9. Configurer les autorisations requises SAM-R

La détection de [chemin de mouvement latéral](use-case-lateral-movement-path.md) s’appuie sur des requêtes qui identifient les administrateurs locaux sur des ordinateurs spécifiques. Ces requêtes sont effectuées à l’aide du protocole SAM-R, via le compte du service ATA créé à l’[étape 2. Se connecter à AD](install-ata-step2.md).
 
Pour vous assurer que les clients et serveurs Windows autorisent le compte de service ATA à effectuer cette opération SAM-R, vous devez modifier votre **stratégie de groupe** de manière à ajouter le compte de service ATA en plus des comptes configurés listés dans la stratégie **Accès réseau**.

1. Recherchez la stratégie :

   - Nom de la stratégie : Accès réseau : Restreindre les clients autorisés à effectuer des appels distants à SAM
   - Emplacement : Configuration de l’ordinateur, Paramètres Windows, Paramètres de sécurité, Stratégies locales, Options de sécurité
  
   ![Recherchez la stratégie](./media/samr-policy-location.png)

2. Ajoutez le service ATA à la liste des comptes approuvés en mesure d’effectuer cette action sur vos systèmes Windows récents.
 
   ![Ajoutez le service](./media/samr-add-service.png)

3. Le **service ATA** (service ATA créé pendant l’installation) a désormais les privilèges appropriés pour exécuter SAM-R dans l’environnement.

> [!NOTE]
> Avant d’appliquer de nouvelles stratégies, assurez-vous que votre environnement reste sécurisé, sans affecter la compatibilité de votre application en activant et en vérifiant vos modifications proposées en mode audit. 

 Pour plus d’informations sur SAM-R et la stratégie de groupe, voir [Accès réseau : Restreindre les clients autorisés à effectuer des appels distants à SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


> [!div class="step-by-step"]
> [« Étape 8](install-ata-step7.md)

## <a name="see-also"></a>Voir aussi
- [Guide de déploiement ATA POC](http://aka.ms/atapoc)
- [Outil de dimensionnement ATA](http://aka.ms/atasizingtool)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](ata-prerequisites.md)
