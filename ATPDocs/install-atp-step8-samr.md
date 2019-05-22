---
title: Configurer SAM-R pour activer la détection de chemin de mouvement latéral dans Azure ATP | Microsoft Docs
description: Explique comment configurer Azure ATP pour effectuer des appels distants vers SAM
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 05/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 95579a90534a04449edd08968948498c4d33bb64
ms.sourcegitcommit: 5d93b0e59080c2d872672bf77a1a40c548c1016d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65760305"
---
# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>Configurer Azure ATP pour effectuer des appels distants vers SAM
La fonctionnalité de détection de [chemins de mouvement latéral](use-case-lateral-movement-path.md) d’Azure ATP a recours à des requêtes pour identifier les administrateurs locaux sur des machines spécifiques. Ces requêtes sont effectuées à l’aide du protocole SAM-R, via le compte du service Azure ATP créé pendant l’installation d’Azure ATP : [Étape 2. Se connecter à AD](install-atp-step2.md).

## <a name="configure-sam-r-required-permissions"></a>Configurer les autorisations requises SAM-R
Pour vous assurer que les clients et serveurs Windows autorisent votre compte Azure ATP à exécuter SAM-R, vous devez modifier la **stratégie de groupe** de manière à ajouter le compte de service Azure ATP en plus des comptes configurés listés dans la stratégie **Accès réseau**. Veillez à appliquer les stratégies de groupe à tous les ordinateurs. 

> [!Note]
> Avant d’appliquer de nouvelles stratégies telles que celle-ci, il est essentiel de vous assurer que votre environnement reste sécurisé et qu’aucun changement n’impacte la compatibilité de votre application. Commencez par activer puis vérifier la compatibilité des changements proposés en mode audit avant de les apporter à votre environnement de production.

1. Recherchez la stratégie :

   - Nom de la stratégie : Accès réseau : Restreindre les clients autorisés à effectuer des appels distants à SAM
   - Emplacement : Configuration de l’ordinateur, Paramètres Windows, Paramètres de sécurité, Stratégies locales, Options de sécurité
  
   ![Recherchez la stratégie](./media/samr-policy-location.png)

2. Ajoutez le service Azure ATP à la liste des comptes approuvés en mesure d’effectuer cette action sur vos systèmes Windows modernes.
 
   ![Ajoutez le service](./media/samr-add-service.png)

3. **AATP Service** (le service Azure ATP créé pendant l’installation) a désormais les privilèges requis pour exécuter SAM-R dans l’environnement.



Pour plus d’informations sur SAM-R et sur cette stratégie de groupe, voir [Accès réseau : Restreindre les clients autorisés à effectuer des appels distants à SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).



## <a name="see-also"></a>Voir aussi
- [Examen des attaques par chemin de mouvement latéral avec Azure ATP](use-case-lateral-movement-path.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
