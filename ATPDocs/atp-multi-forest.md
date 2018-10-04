---
title: Prise en charge multi-forêt dans Azure Advanced Threat Protection | Microsoft Docs
description: Comment configurer la prise en charge de plusieurs forêts Active Directory dans Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/20/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ad120cfe3e736935a557f66417794cd531fa5b2e
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454086"
---
*S’applique à : Azure Advanced Threat Protection*

# <a name="install-azure-atp---step-9"></a>Installer Azure ATP - Étape 9

> [!div class="step-by-step"]
> [« Étape 8](install-atp-step8-samr.md)

## <a name="step-9--set-up-azure-advanced-threat-protection-multi-forest-support"></a>Étape 9.  Configurer la prise en charge multi-forêt dans Azure Advanced Threat Protection

Azure ATP peut gérer les organisations qui ont plusieurs forêts, ce qui vous permet de surveiller facilement les activités et les profils des utilisateurs dans les différentes forêts dans un volet unique. 

Les organisations peuvent avoir généralement plusieurs forêts Active Directory, souvent utilisées à des fins différentes : infrastructure héritée de fusions et d’acquisitions d’entreprises, répartition géographique et limites de sécurité (forêts rouges), par exemple. Vous pouvez protéger plusieurs forêts à l’aide d’Azure ATP, ce qui vous offre la possibilité de surveiller et d’investiguer à partir d’un volet unique.

Avec la prise en charge de plusieurs forêts Active Directory :
-   permet de voir et d’examiner les activités effectuées par les utilisateurs dans différentes forêts sur un seul écran ; 
-   améliore la détection et réduit les faux positifs grâce à l’intégration Active Directory avancée et à la résolution de comptes ; 
-   améliore le contrôle et facilite le déploiement ; améliore les alertes de supervision et la création de rapports pour la couverture interorganisationnelle lorsque vos contrôleurs de domaine sont supervisés à partir d’une seule console Azure ATP.


## <a name="how-azure-atp-detects-activities-across-multiple-forests"></a>Comment Azure ATP détecte les activités sur plusieurs forêts 

Pour détecter les activités inter-forêts, les capteurs Azure ATP interrogent les contrôleurs de domaine dans des forêts distantes pour créer des profils pour toutes les entités impliquées, notamment les utilisateurs et les ordinateurs de forêts distantes. 

> [!NOTE]
> - Les capteurs Azure ATP peuvent être installés sur toutes les forêts (à condition qu’il existe une relation d’approbation à sens unique minimale).
> - L’utilisateur que vous configurez dans la console Azure ATP sous **Services d’annuaire** doit être approuvé dans toutes les autres forêts.


Si vous avez des forêts sur lesquelles aucun capteur Azure ATP n’est installé, Azure ATP peut quand même afficher et surveiller les activités provenant de ces forêts. Les capteurs ATP installés peuvent interroger tous les contrôleurs de domaine de forêt distante connectés pour résoudre les utilisateurs et les ordinateurs, et créer des profils pour chacun d’eux. 

## <a name="installation-requirements"></a>Conditions d’installation requises 

-   Si les capteurs autonomes Azure ATP sont installés sur des ordinateurs autonomes, plutôt que directement sur les contrôleurs de domaine, assurez-vous que les ordinateurs sont autorisés à communiquer avec tous les contrôleurs de domaine de forêt distante à l’aide de LDAP. 
- L’utilisateur que vous configurez dans la console Azure ATP sous **Services d’annuaire** doit être approuvé dans toutes les autres forêts et doit avoir au moins des autorisations en lecture seule pour effectuer les requêtes LDAP des contrôleurs de domaine.

- Pour qu’Azure ATP communique avec les capteurs ATP et les capteurs autonomes ATP, ouvrez les ports suivants sur chaque ordinateur sur lequel est installé le capteur ATP :

 
  |Protocole|Transport|Port|Vers/À partir de|Sens|
  |----|----|----|----|----|
  |**Ports Internet**||||
  |SSL (*.atp.azure.com)|TCP|443|Service cloud Azure ATP|Sortant|
  |**Ports internes**||||           
  |LDAP|TCP et UDP|389|Contrôleurs de domaine|Sortant|
  |LDAP sécurisé (LDAPS)|TCP|636|Contrôleurs de domaine|Sortant|
  |LDAP vers le catalogue global|TCP|3268|Contrôleurs de domaine|Sortant|
  |LDAPS vers le catalogue global|TCP|3269|Contrôleurs de domaine|Sortant|


## <a name="multi-forest-support-network-traffic-impact"></a>Impact de la prise en charge multi-forêt sur le trafic réseau 

Quand Azure ATP mappe vos forêts, il utilise un processus qui impacte les éléments suivants :

-   Une fois que le capteur Azure ATP est en cours d’exécution, il interroge les forêts Active Directory distantes et récupère une liste d’utilisateurs et de données machine pour la création de profil.
-   Toutes les 5 minutes, chaque capteur Azure ATP interroge un contrôleur de domaine de chaque domaine de chaque forêt, pour mapper toutes les forêts dans le réseau.
-   Chaque capteur Azure ATP mappe les forêts à l’aide de l’objet « trustedDomain » dans Active Directory, en se connectant et en vérifiant le type d’approbation.
-   Vous pouvez également voir le trafic ad hoc lorsque le capteur ATP détecte une activité inter-forêt. Lorsque cela se produit, les capteurs ATP envoient une requête LDAP aux contrôleurs de domaine appropriés pour récupérer les informations d’entité. 

## <a name="known-limitations"></a>Limitations connues
-   Les connexions interactives effectuées par les utilisateurs dans une forêt pour accéder aux ressources d’une autre forêt ne sont pas affichées dans le tableau de bord Azure ATP.


> [!div class="step-by-step"]
> [« Étape 8](install-atp-step8-samr.md)


## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement ATP](http://aka.ms/aatpsizingtool)
- [Architecture ATP](atp-architecture.md)
- [Installer ATP](install-atp-step1.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)

