---
title: Configuration d’exclusions de détection et de comptes honeytoken dans Azure Advanced Threat Protection | Microsoft Docs
description: Configuration d’exclusions de détection et de comptes honeytoken
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 12/02/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 045d5d9bd76712ea77201f39ab9d8d5125d90e36
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56263554"
---
# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>Configurer des exclusions d’adresses IP et de comptes honeytoken

Azure ATP permet d’exclure des adresses IP ou des utilisateurs spécifiques d’un certain nombre de détections. 

Par exemple, une **exclusion DNS Reconnaissance** peut être un analyseur de sécurité qui utilise DNS comme mécanisme d’analyse. L’exclusion permet à Azure ATP d’ignorer ces analyseurs.  

Avec Azure ATP, vous pouvez aussi configurer des comptes honeytoken servant de pièges pour les utilisateurs malveillants. Toute authentification associée à ces comptes honeytoken (normalement dormants) déclenche une alerte.

Pour la configuration, procédez comme suit :

1.  Dans le portail Azure ATP, cliquez sur l’icône des paramètres, puis sélectionnez **Configuration**.

    ![Paramètres de configuration d’Azure ATP](media/atp-config-menu.png)

2.  Sous **Détection**, cliquez sur **Étiquettes d’entité**.

3. Sous **Comptes Honeytoken**, entrez le nom du compte Honeytoken et cliquez sur le signe **+**. Le champ des comptes Honeytoken peut faire l’objet d’une recherche et affiche automatiquement les entités dans votre réseau. Cliquez sur **Save**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Cliquez sur **Exclusions**. Pour chaque type de menace, entrez un compte d’utilisateur ou une adresse IP à exclure de la détection. 
5. Cliquez sur le signe *plus*. Le champ **Ajouter une entité** (utilisateur ou ordinateur) peut faire l’objet d’une recherche et est automatiquement renseigné avec les entités de votre réseau. Pour plus d’informations, consultez [Exclusion d’entités des détections](excluding-entities-from-detections.md) et le [Guide des alertes de sécurité](suspicious-activity-guide.md).

   ![Exclusions](media/exclusions.png)

6.  Cliquez sur **Save**.


Félicitations, vous avez correctement déployé Azure Advanced Threat Protection !

Vérifiez la chronologie des attaques pour afficher les alertes de sécurité détectées et rechercher des utilisateurs ou des ordinateurs et afficher leurs profils.

L’analyse d’Azure ATP démarre immédiatement. Certaines détections, telles que les modifications anormales de groupe, nécessitent une période d’apprentissage et ne sont pas disponibles immédiatement après le déploiement d’Azure ATP.


## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consulter le forum Azure ATP](https://aka.ms/azureatpcommunity)
