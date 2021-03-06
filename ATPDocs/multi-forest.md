---
title: Microsoft Defender pour la prise en charge de plusieurs forêts d’identité
description: Prise en charge de plusieurs forêts Active Directory dans Microsoft Defender pour l’identité.
ms.date: 10/26/2020
ms.topic: conceptual
ms.openlocfilehash: c0a5c135d73ecbcdd23b6ed2ea8a12a212a0f23d
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533662"
---
# <a name="microsoft-defender-for-identity-multi-forest-support"></a>Microsoft Defender pour la prise en charge de plusieurs forêts d’identité

## <a name="multi-forest-support-set-up"></a>Configuration de la prise en charge de plusieurs forêts

[!INCLUDE [Product long](includes/product-long.md)] prend en charge les organisations avec plusieurs forêts, ce qui vous permet de surveiller facilement l’activité et de profiler les utilisateurs entre les forêts.

Les organisations peuvent avoir généralement plusieurs forêts Active Directory, souvent utilisées à des fins différentes : infrastructure héritée de fusions et d’acquisitions d’entreprises, répartition géographique et limites de sécurité (forêts rouges), par exemple. Vous pouvez protéger plusieurs forêts à l’aide de [!INCLUDE [Product short](includes/product-short.md)] , ce qui vous permet de surveiller et d’examiner l’ensemble de votre réseau via un seul volet.

Avec la prise en charge de plusieurs forêts Active Directory :

- vous permet de voir et de superviser les activités effectuées par les utilisateurs dans plusieurs forêts à partir d’un seul volet ;
- améliore la détection et réduit les faux positifs grâce à l’intégration Active Directory avancée et à la résolution de comptes ;
- améliore le contrôle et facilite le déploiement ; Alertes d’intégrité et rapports améliorés pour la couverture inter-organisationnelle lorsque vos contrôleurs de domaine sont tous analysés à partir d’une [!INCLUDE [Product short](includes/product-short.md)] console unique.

## <a name="defender-for-identity-detection-activity-across-multiple-forests"></a>Defender pour l’activité de détection d’identité dans plusieurs forêts

Pour détecter les activités inter-forêts, [!INCLUDE [Product short](includes/product-short.md)] les capteurs interrogent les contrôleurs de domaine dans les forêts distantes pour créer des profils pour toutes les entités impliquées, (y compris les utilisateurs et les ordinateurs des forêts distantes).

- [!INCLUDE [Product short](includes/product-short.md)] les capteurs peuvent être installés sur les contrôleurs de domaine dans toutes les forêts, y compris les forêts sans approbation.
- Ajoutez des informations d’identification supplémentaires sur la page services d’annuaire pour prendre en charge les forêts non approuvées dans votre environnement.
  - Une seule information d’identification est requise pour prendre en charge toutes les forêts avec une relation d’approbation bidirectionnelle.
  - Les informations d’identification supplémentaires sont requises uniquement pour chaque forêt disposant d’une approbation non-Kerberos ou d’aucune approbation.
  - Il existe une limite par défaut de 10 forêts non approuvées par [!INCLUDE [Product short](includes/product-short.md)] instance. Si votre organisation possède plus de 10 forêts, contactez le support.

![Étape 1 de bienvenue [!INCLUDE [Product short](includes/product-short.md)]](media/directory-services-add-no-trust-forests.png)

### <a name="requirements"></a>Spécifications

- L’utilisateur que vous configurez dans la [!INCLUDE [Product short](includes/product-short.md)] console sous **services d’annuaire** doit être approuvé dans toutes les autres forêts et doit avoir au moins l’autorisation lecture seule pour exécuter des requêtes LDAP sur les contrôleurs de domaine.
- Si des [!INCLUDE [Product short](includes/product-short.md)] capteurs autonomes sont installés sur des ordinateurs autonomes, plutôt que directement sur les contrôleurs de domaine, assurez-vous que les ordinateurs sont autorisés à communiquer avec tous les contrôleurs de domaine de la forêt distante à l’aide de LDAP.

- Pour [!INCLUDE [Product short](includes/product-short.md)] que puisse communiquer avec les capteurs [!INCLUDE [Product short](includes/product-short.md)] et les [!INCLUDE [Product short](includes/product-short.md)] capteurs autonomes, ouvrez les ports suivants sur chaque ordinateur sur lequel le [!INCLUDE [Product short](includes/product-short.md)] capteur est installé :

  |Protocole|Transport|Port|Vers/À partir de|Sens|
  |----|----|----|----|----|
  |**Ports Internet**||||
  |SSL (*.atp.azure.com)|TCP|443|Service cloud [!INCLUDE [Product short](includes/product-short.md)]|Sortant|
  |**Ports internes**||||
  |LDAP|TCP et UDP|389|Contrôleurs de domaine|Sortant|
  |LDAP sécurisé (LDAPS)|TCP|636|Contrôleurs de domaine|Sortant|
  |LDAP vers le catalogue global|TCP|3268|Contrôleurs de domaine|Sortant|
  |LDAPS vers le catalogue global|TCP|3269|Contrôleurs de domaine|Sortant|

## <a name="multi-forest-support-network-traffic-impact"></a>Impact de la prise en charge de plusieurs forêts sur le trafic réseau

Lorsque [!INCLUDE [Product short](includes/product-short.md)] mappe vos forêts, il utilise un processus qui a un impact sur les éléments suivants :

- Une fois le [!INCLUDE [Product short](includes/product-short.md)] capteur en cours d’exécution, il interroge les forêts Active Directory distantes et récupère la liste des utilisateurs et des données de l’ordinateur pour la création du profil.
- Toutes les 5 minutes, chaque [!INCLUDE [Product short](includes/product-short.md)] capteur interroge un contrôleur de domaine de chaque domaine, à partir de chaque forêt, pour mapper toutes les forêts du réseau.
- Chaque [!INCLUDE [Product short](includes/product-short.md)] capteur mappe les forêts à l’aide de l’objet « trustedDomain » dans Active Directory, en se connectant et en vérifiant le type d’approbation.
- Vous pouvez également voir le trafic ad hoc lorsque le [!INCLUDE [Product short](includes/product-short.md)] capteur détecte une activité inter-forêts. Dans ce cas, les [!INCLUDE [Product short](includes/product-short.md)] capteurs envoient une requête LDAP aux contrôleurs de domaine appropriés afin de récupérer les informations d’entité.

## <a name="known-limitations"></a>Limitations connues

- Les ouvertures de session interactives effectuées par les utilisateurs dans une forêt pour accéder aux ressources d’une autre forêt ne sont pas affichées dans le [!INCLUDE [Product short](includes/product-short.md)] tableau de bord.

## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/aatpsizingtool)
- [Architecture [!INCLUDE [Product short](includes/product-short.md)]](architecture.md)
- [Installer [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
