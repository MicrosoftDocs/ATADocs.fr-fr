---
title: Configurer SAM-R pour activer la détection de chemin de mouvement latéral dans Azure ATP | Microsoft Docs
description: Décrit comment configurer SAM-R pour activer la détection de chemin de mouvement latéral dans Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/29/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 24b42c5425933d8931a85e0ba454a69e0ca94a21
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2018
ms.locfileid: "32298290"
---
*S’applique à : Azure - Protection avancée contre les menaces*

# <a name="install-azure-atp---step-8"></a>Installer Azure ATP – Étape 8

>[!div class="step-by-step"]
[« Étape 7 ](install-atp-step7.md)

## <a name="step-8-configure-sam-r-required-permissions"></a>Étape 8. Configurer les autorisations requises SAM-R

La détection de [chemin de mouvement latéral](use-case-lateral-movement-path.md) s’appuie sur des requêtes qui identifient les administrateurs locaux sur des ordinateurs spécifiques. Ces requêtes sont effectuées à l’aide du protocole SAM-R, via le compte du service Azure ATP créé à l’[étape 2. Se connecter à AD](install-atp-step2.md).
 
Pour vous assurer que les clients et serveurs Windows autorisent le compte Azure ATP à effectuer cette opération SAM-R, vous devez modifier la **stratégie de groupe** de manière à ajouter le compte de service Azure ATP en plus des comptes configurés listés dans la stratégie **Accès réseau**.

1. Recherchez la stratégie :

 - Nom de la stratégie : Accès réseau : restreindre les clients autorisés à effectuer des appels distants vers SAM
 - Emplacement : Configuration ordinateur, Paramètres Windows, Paramètres de sécurité, Stratégies locales, Options de sécurité
  
  ![Recherchez la stratégie](./media/samr-policy-location.png)

2. Ajoutez le service Azure ATP à la liste des comptes approuvés en mesure d’effectuer cette action sur vos systèmes Windows modernes.
 
  ![Ajoutez le service](./media/samr-add-service.png)

3. **AATP Service** (le service Azure ATP créé pendant l’installation) a désormais les privilèges appropriés pour exécuter SAMR dans l’environnement.

Pour plus d’informations sur SAM-R et cette stratégie de groupe, consultez [Accès réseau : restreindre les clients autorisés à effectuer des appels distants vers SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[« Étape 7 ](install-atp-step7.md)



## <a name="see-also"></a>Voir aussi
- [Examen des attaques par chemin de mouvement latéral avec Azure ATP](use-case-lateral-movement-path.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)