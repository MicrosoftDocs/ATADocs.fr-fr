---
title: Prise en charge de plusieurs forêts dans Azure Advanced Threat Protection
description: Prise en charge de plusieurs forêts Active Directory dans Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ecac12f266a424e55266d1343a2d03a75bca8840
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79413993"
---
# <a name="azure-advanced-threat-protection-multi-forest-support"></a>Prise en charge de plusieurs forêts dans Azure Advanced Threat Protection

## <a name="multi-forest-support-set-up"></a>Configuration de la prise en charge de plusieurs forêts

Azure ATP prend en charge les organisations avec plusieurs forêts, ce qui vous permet de superviser facilement les activités et les profils des utilisateurs dans les différentes forêts.

Les organisations peuvent avoir généralement plusieurs forêts Active Directory, souvent utilisées à des fins différentes : infrastructure héritée de fusions et d’acquisitions d’entreprises, répartition géographique et limites de sécurité (forêts rouges), par exemple. Vous pouvez protéger plusieurs forêts à l’aide d’Azure ATP, et ainsi superviser et examiner votre réseau entier à partir d’un volet unique.

Avec la prise en charge de plusieurs forêts Active Directory :

- vous permet de voir et de superviser les activités effectuées par les utilisateurs dans plusieurs forêts à partir d’un seul volet ;
- améliore la détection et réduit les faux positifs grâce à l’intégration Active Directory avancée et à la résolution de comptes ;
- améliore le contrôle et facilite le déploiement ; améliore les alertes de supervision et la création de rapports pour la couverture interorganisationnelle lorsque vos contrôleurs de domaine sont supervisés à partir d’une seule console Azure ATP.

## <a name="azure-atp-detection-activity-across-multiple-forests"></a>Détection par Azure ATP des activités dans plusieurs forêts

Pour détecter les activités inter-forêts, les capteurs Azure ATP interrogent les contrôleurs de domaine dans des forêts distantes pour créer des profils pour toutes les entités impliquées, notamment les utilisateurs et les ordinateurs de forêts distantes.

- Les capteurs Azure ATP peuvent être installés sur des contrôleurs de domaine dans toutes les forêts, même celles qui n’ont pas de relation d’approbation.
- Ajoutez d’autres informations d’identification dans la page Services d’annuaire pour prendre en charge toutes les forêts non approuvées dans votre environnement.
    - Un seul titre de compétences est requis pour prendre en charge toutes les forêts avec une relation d’approbation bidirectionnelle.
    - Les informations d'identification supplémentaires ne sont nécessaires que pour chaque forêt avec une relation d’approbation non Kerberos ou sans aucune relation d’approbation.
    - Il existe une limite par défaut de 10 forêts non approuvées par instance Azure ATP. Si votre organisation possède plus de 10 forêts, contactez le support.

![Étape 1 de bienvenue Azure ATP](media/directory-services-add-no-trust-forests.png)

### <a name="requirements"></a>Configuration requise

- L’utilisateur que vous configurez dans la console Azure ATP sous **Services d’annuaire** doit être approuvé dans toutes les autres forêts et doit avoir au moins des autorisations en lecture seule pour effectuer les requêtes LDAP sur les contrôleurs de domaine.
- Si les capteurs autonomes Azure ATP sont installés sur des ordinateurs autonomes, plutôt que directement sur les contrôleurs de domaine, assurez-vous que les ordinateurs sont autorisés à communiquer avec tous les contrôleurs de domaine de forêt distante à l’aide de LDAP.

- Pour qu’Azure ATP communique avec les capteurs Azure ATP et les capteurs autonomes Azure ATP, ouvrez les ports suivants sur chaque machine sur laquelle est installée le capteur Azure ATP :

  |Protocole|Transport|Port|Vers/À partir de|Sens|
  |----|----|----|----|----|
  |**Ports Internet**||||
  |SSL (*.atp.azure.com)|TCP|443|Service cloud Azure ATP|Sortant|
  |**Ports internes**||||
  |LDAP|TCP et UDP|389|Contrôleurs de domaine|Sortant|
  |LDAP sécurisé (LDAPS)|TCP|636|Contrôleurs de domaine|Sortant|
  |LDAP vers le catalogue global|TCP|3268|Contrôleurs de domaine|Sortant|
  |LDAPS vers le catalogue global|TCP|3269|Contrôleurs de domaine|Sortant|

## <a name="multi-forest-support-network-traffic-impact"></a>Impact de la prise en charge de plusieurs forêts sur le trafic réseau

Quand Azure ATP mappe vos forêts, il utilise un processus qui impacte les éléments suivants :

- Une fois que le capteur Azure ATP est en cours d’exécution, il interroge les forêts Active Directory distantes et récupère une liste d’utilisateurs et de données machine pour la création de profil.
- Toutes les 5 minutes, chaque capteur Azure ATP interroge un contrôleur de domaine de chaque domaine de chaque forêt, pour mapper toutes les forêts dans le réseau.
- Chaque capteur Azure ATP mappe les forêts à l’aide de l’objet « trustedDomain » dans Active Directory, en se connectant et en vérifiant le type d’approbation.
- Vous pouvez également voir le trafic ad hoc lorsque le capteur Azure ATP détecte une activité entre plusieurs forêts. Lorsque cela se produit, les capteurs Azure ATP envoient une requête LDAP aux contrôleurs de domaine appropriés pour récupérer les informations d’entité.

## <a name="known-limitations"></a>Limitations connues

- Les connexions interactives effectuées par les utilisateurs dans une forêt pour accéder aux ressources d’une autre forêt ne sont pas affichées dans le tableau de bord Azure ATP.

## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement Azure ATP](https://aka.ms/aatpsizingtool)
- [Architecture Azure ATP](atp-architecture.md)
- [Installer Azure ATP](install-atp-step1.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
