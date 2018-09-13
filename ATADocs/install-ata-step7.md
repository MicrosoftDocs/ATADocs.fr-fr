---
title: Installer Advanced Threat Analytics - Étape 8 | Microsoft Docs
description: Lors de l’étape finale de l’installation d’ATA, vous configurez l’utilisateur Honeytoken.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f15f897539f2f41941675960e425f669cba2c878
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126023"
---
*S’applique à : Advanced Threat Analytics version 1.9*



# <a name="install-ata---step-8"></a>Installer ATA - Étape 8

>[!div class="step-by-step"]
[« Étape 7](vpn-integration-install-step.md)
[Étape 9 »](install-ata-step9-samr.md)

## <a name="step-8-configure-ip-address-exclusions-and-honeytoken-user"></a>Étape 8. Configurer des exclusions d’adresses IP et un utilisateur Honeytoken
ATA permet d’exclure des adresses IP ou utilisateurs spécifiques d’un certain nombre de détections. 

Par exemple, une **exclusion DNS Reconnaissance** peut être un analyseur de sécurité qui utilise DNS comme mécanisme d’analyse. L’exclusion aide ATA à ignorer ces analyseurs. Un appareil NAT constitue un exemple d’exclusion *Pass-the-Ticket*.    

Avec ATA, vous pouvez aussi configurer un utilisateur Honeytoken servant de piège pour les utilisateurs malveillants. Toute authentification associée à ce compte (normalement dormant) déclenche une alerte.

Pour configurer ceci, procédez comme suit :

1.  À partir de la console ATA, cliquez sur l’icône des paramètres et sélectionnez **Configuration**.

    ![Paramètres de configuration ATA](media/ATA-config-icon.png)

2.  Sous **Détection**, cliquez sur **Étiquettes d’entité**.

2. Sous **Comptes Honeytoken**, entrez le nom du compte Honeytoken. Le champ des comptes Honeytoken peut faire l’objet d’une recherche et affiche automatiquement les entités dans votre réseau.

   ![Honeytoken](media/honeytoken.png)

3. Cliquez sur **Exclusions**. Pour chaque type de menace, entrez un compte d’utilisateur ou une adresse IP à exclure de la détection de ces menaces, et cliquez sur le signe *plus*. Le champ **Ajouter une entité** (utilisateur ou ordinateur) peut faire l’objet d’une recherche et est automatiquement renseigné avec les entités de votre réseau. Pour plus d’informations, consultez [Exclusion d’entités des détections](excluding-entities-from-detections.md)

   ![Exclusions](media/exclusions.png)

4.  Cliquez sur **Save**.


Félicitations, vous avez correctement déployé Microsoft Advanced Threat Analytics !

Vérifiez la chronologie des attaques pour afficher les activités suspectes détectées et rechercher des utilisateurs ou des ordinateurs, puis afficher leurs profils.

ATA démarre immédiatement l’analyse pour rechercher les activités suspectes. Certaines activités, telles que certaines liées au comportement, ne sont disponibles qu’une fois qu’ATA a eu le temps de créer des profils de comportements (procédure qui prend au minimum trois semaines).

Pour vérifier qu’ATA est opérationnel et qu’il détecte les violations dans votre réseau, vous pouvez consulter le [Scénario de simulation d’attaque Advanced Threat Analytics](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook).


>[!div class="step-by-step"]
[« Étape 7](vpn-integration-install-step.md)
[Étape 9 »](install-ata-step9-samr.md)


## <a name="related-videos"></a>Vidéos connexes
- [Vue d’ensemble du déploiement ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Sélection du type de passerelle ATA approprié](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Voir aussi
- [Guide de déploiement ATA POC](http://aka.ms/atapoc)
- [Outil de dimensionnement ATA](http://aka.ms/atasizingtool)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](ata-prerequisites.md)

