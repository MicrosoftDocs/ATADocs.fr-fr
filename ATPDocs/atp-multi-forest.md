---
title: Prise en charge multi-forêt dans Azure Advanced Threat Protection | Microsoft Docs
description: Comment configurer la prise en charge de plusieurs forêts Active Directory dans Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/17/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c76e459709c786082bea7566a61e5384a235eda4
ms.sourcegitcommit: 8feb9b65dc0e1de0ace00aca11784e54f9852a15
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39098181"
---
*S’applique à : Azure Advanced Threat Protection*

# <a name="install-azure-atp---step-9"></a>Installer Azure ATP - Étape 9

>[!div class="step-by-step"]
[« Étape 8](install-atp-step8-samr.md)

## <a name="step-9--set-up-azure-advanced-threat-protection-multi-forest-support"></a>Étape 9.  Configurer la prise en charge multi-forêt dans Azure Advanced Threat Protection

Azure ATP peut gérer les organisations qui ont plusieurs forêts, ce qui vous permet de surveiller les activités et les profils des utilisateurs dans les différentes forêts. 

Une organisation peut avoir plusieurs forêts Active Directory, souvent utilisées à des fins différentes : infrastructure héritée de fusions et d’acquisitions d’entreprises, répartition géographique et limites de sécurité (forêts rouges), par exemple. Vous pouvez protéger plusieurs forêts à l’aide d’Azure ATP en réunissant toutes les données dans un seul espace de travail principal, ce qui vous offre la possibilité de surveiller et d’investiguer à partir d’un seul écran.

Avec la prise en charge de plusieurs forêts Active Directory :
-   Vous pouvez voir et investiguer les activités effectuées par les utilisateurs dans plusieurs forêts à partir d’un seul écran. 
-   La prise en charge multi-forêt améliore la détection et réduit les faux positifs en fournissant une intégration Active Directory et une résolution de comptes avancées. 
-   Étant donné qu’avec la prise en charge multi-forêt vous n’avez plus besoin de plusieurs espaces de travail, vous bénéficiez d’un plus grand contrôle et d’un déploiement plus simple, car vous centralisez la surveillance de tous vos contrôleurs de domaine sur une seule console Azure ATP qui offre de meilleures alertes et de meilleurs rapports de monitoring pour une couverture inter-organisation.


## <a name="how-azure-atp-detects-activities-across-multiple-forests"></a>Comment Azure ATP détecte les activités sur plusieurs forêts 

Pour détecter les activités inter-forêts, les capteurs Azure ATP interrogent les contrôleurs de domaine dans des forêts distantes pour créer des profils pour toutes les entités impliquées, notamment les utilisateurs et les ordinateurs de forêts distantes. 

> [!NOTE]
> - Pour que cela fonctionne, la forêt sur laquelle sont installés les capteurs Azure ATP doit être approuvée par toutes les autres forêts.
> - L’utilisateur que vous configurez dans la console Azure ATP sous **Services d’annuaire** doit être approuvé dans toutes les autres forêts.


Si vous avez des forêts sur lesquelles aucun capteur Azure ATP n’est installé, Azure ATP peut quand même afficher et surveiller les activités provenant de ces forêts. Les capteurs ATP installés peuvent interroger tous les contrôleurs de domaine de forêt distante connectés pour résoudre les utilisateurs et les ordinateurs et créer des profils pour chacun d’eux. 

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


>[!div class="step-by-step"]
[« Étape 8](install-atp-step8-samr.md)


## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement ATA](http://aka.ms/aatpsizingtool)
- [Architecture d’ATA](atp-architecture.md)
- [Installer ATA](install-atp-step1.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)

