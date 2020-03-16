---
title: Configurer SAM-R pour activer la détection de chemin de mouvement latéral dans Advanced Threat Analytics
description: Décrit comment configurer SAM-R pour activer la détection de chemin de mouvement latéral dans Advanced Threat Analytics (ATA)
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/08/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fa47a151ae8131039a5f7822acc5b541deb5c621
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79413976"
---
# <a name="install-ata---step-9"></a>Installer ATA - Étape 9

*S’applique à : Advanced Threat Analytics version 1.9*

> [!div class="step-by-step"]
> [« Étape 8](install-ata-step7.md)

> [!NOTE]
> Avant d’appliquer une nouvelle stratégie, assurez-vous toujours que votre environnement reste sécurisé, sans impact sur la compatibilité des applications en activant et en vérifiant vos modifications proposées en mode audit. 

## <a name="step-9-configure-sam-r-required-permissions"></a>Étape 9. Configurer les autorisations requises SAM-R

La détection de [chemin de mouvement latéral](use-case-lateral-movement-path.md) s’appuie sur des requêtes qui identifient les administrateurs locaux sur des ordinateurs spécifiques. Ces requêtes sont effectuées à l’aide du protocole SAM-R, via le compte de service ATA créé à l' [étape 2. Connectez-vous à AD](install-ata-step2.md).
 
Pour vous assurer que les clients et serveurs Windows autorisent le compte de service ATA à effectuer cette opération SAM-R, vous devez modifier votre **stratégie de groupe** de manière à ajouter le compte de service ATA en plus des comptes configurés listés dans la stratégie **Accès réseau**. Cette stratégie de groupe doit être appliquée à tous les appareils de votre organisation. 

1. Recherchez la stratégie :

   - Nom de la stratégie : Accès réseau : restreindre les clients autorisés à effectuer des appels distants vers SAM
   - Emplacement : Configuration ordinateur, Paramètres Windows, Paramètres de sécurité, Stratégies locales, Options de sécurité
  
   ![Recherchez la stratégie](./media/samr-policy-location.png)

2. Ajoutez le service ATA à la liste des comptes approuvés en mesure d’effectuer cette action sur vos systèmes Windows récents.
 
   ![Ajoutez le service](./media/samr-add-service.png)

3. Le **service ATA** (service ATA créé pendant l’installation) a désormais les privilèges appropriés pour exécuter SAM-R dans l’environnement.

 Pour plus d’informations sur SAM-R et la stratégie de groupe, consultez [Accès réseau : restreindre les clients autorisés à effectuer des appels distants vers SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


> [!div class="step-by-step"]
> [« Étape 8](install-ata-step7.md)

## <a name="see-also"></a>Voir aussi
- [Guide de déploiement ATA POC](https://aka.ms/atapoc)
- [Outil de dimensionnement ATA](https://aka.ms/atasizingtool)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
