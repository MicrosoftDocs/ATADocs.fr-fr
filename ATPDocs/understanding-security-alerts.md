---
title: Tutoriel des alertes de sécurité Microsoft Defender pour Identity
description: Cet article explique comment utiliser et comprendre les alertes de sécurité Microsoft Defender pour Identity.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ba5adecd1812d95f043d520773b1006a6e75b5b9
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93277808"
---
# <a name="understanding-security-alerts"></a>Présentation des alertes de sécurité

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Les alertes de sécurité [!INCLUDE [Product long](includes/product-long.md)] expliquent en termes clairs et à l’aide de graphismes les activités suspectes identifiées sur votre réseau ainsi que les acteurs et les ordinateurs impliqués dans les menaces. Les alertes sont classées par gravité, colorées afin de faciliter le filtrage visuel et organisées par phase de menace. Chaque alerte est conçue pour vous aider à comprendre rapidement et précisément ce qui se passe sur votre réseau. Des listes de preuves d’alertes contiennent des liens directs vers les ordinateurs et les utilisateurs impliqués, afin de rendre vos recherches plus faciles et plus directes.

Dans ce tutoriel, vous allez découvrir la structure des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] et apprendre à les utiliser :

> [!div class="checklist"]
>
> - Structure des alertes de sécurité
> - Classifications des alertes de sécurité
> - Catégories des alertes de sécurité
> - Investigation avancée des alertes de sécurité
> - Entités associées
> - [!INCLUDE [Product short](includes/product-short.md)] et résolution de noms réseau

## <a name="security-alert-structure"></a>Structure des alertes de sécurité

Chaque alerte de sécurité [!INCLUDE [Product short](includes/product-short.md)] comprend les éléments suivants :

- **Titre de l’alerte**  
Nom [!INCLUDE [Product short](includes/product-short.md)] officiel de l’alerte.
- **Description**  
Brève explication de ce qui s’est passé.
- **Preuve**  
Informations supplémentaires et pertinentes concernant ce qui s’est passé, afin de vous aider lors du processus d’investigation.
- **Téléchargement Excel**  
Rapport Excel détaillé à des fins d’analyse

![Structure des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)]](media/security-alert-structure.png)

## <a name="security-alert-classifications"></a>Classifications des alertes de sécurité

Après examen, toutes les alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] peuvent être classées comme l’un des types d’activités suivants :

- **TP (True positive)**  : action malveillante détectée par [!INCLUDE [Product short](includes/product-short.md)].

- **B-TP (benign true positive)**  : action détectée par [!INCLUDE [Product short](includes/product-short.md)] et bien réelle, mais non malveillante (par exemple, test d’intrusion ou activité connue générée par une application approuvée).

- **FP (false positive)**  : Fausse alerte, ce qui signifie que l’activité n’a pas eu lieu.

### <a name="is-the-security-alert-a-tp-b-tp-or-fp"></a>L’alerte de sécurité est-elle TP, B-TP ou FP ?

Pour chaque alerte, posez-vous les questions suivantes afin de déterminer la classification d’alerte et de vous aider à décider de la marche à suivre :

1. Quelle est la fréquence de cette alerte de sécurité spécifique dans votre environnement ?
1. L’alerte a-t-elle été déclenchée par les mêmes types d’ordinateurs ou d’utilisateurs
   (par exemple, des serveurs ayant le même rôle ou des utilisateurs du même groupe/service) ? Si les ordinateurs ou utilisateurs étaient similaires, vous pouvez décider de les exclure afin d’éviter de recevoir ultérieurement d’autres alertes FP.

Remarque : Une augmentation des alertes du même type réduit généralement le niveau d’importance/de suspicion de l’alerte. Pour les alertes répétées, vérifiez les configurations et utilisez les détails et les définitions de l’alerte de sécurité afin de comprendre exactement ce qui déclenche la répétition.

## <a name="security-alert-categories"></a>Catégories des alertes de sécurité

Les alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] sont réparties en plusieurs catégories ou phases (cf. ci-dessous), comme les phases d’une chaîne cybercriminelle standard. Apprenez-en davantage sur chaque phase et sur les alertes conçues pour détecter chaque attaque grâce aux liens suivants :

- [Alertes de reconnaissance](reconnaissance-alerts.md)
- [Alertes indiquant des informations d’identification compromises](compromised-credentials-alerts.md)
- [Alertes de mouvement latéral](lateral-movement-alerts.md)
- [Alertes de dominance du domaine](domain-dominance-alerts.md)
- [Alertes d’exfiltration](exfiltration-alerts.md)

## <a name="advanced-security-alert-investigation"></a>Investigation avancée des alertes de sécurité

Pour obtenir plus de détails sur une alerte de sécurité, téléchargez le rapport d’alerte détaillé Excel.

1. Cliquez sur les trois points dans le coin supérieur droit d’une alerte et sélectionnez *Télécharger les détails*.

Chaque téléchargement Excel d’alerte [!INCLUDE [Product short](includes/product-short.md)] comporte les informations suivantes :

- Synthèse : le premier onglet comprend les principales caractéristiques de l’alerte
  - Titre
  - Description
  - Heure de début (UTC)
  - Heure de fin (UTC)
  - Gravité : faible/moyenne/élevée
  - État : ouverte/fermée
  - Heure de mise à jour de l’état (UTC)
  - Afficher dans le navigateur
- Toutes les entités impliquées (comptes, ordinateurs et ressources) sont listées, réparties en fonction de leur rôle.
  - Source, destination ou attaquée, en fonction de l’alerte.
- La plupart des onglets contiennent les données suivantes pour chaque entité :
  - Nom
  - Détails
  - Type
  - SamName
  - Ordinateur source
  - Utilisateur source (s’il est disponible)
  - Contrôleurs de domaine
  - Ressource sollicitée : heure, ordinateur, nom, détails, type, service.
  - Onglets supplémentaires par alerte :
    - Sur les comptes attaqués quand l’attaque suspectée a utilisé la Force Brute.
    - Sur les serveurs DNS (Domain Name System) quand l’attaque suspectée a impliqué la reconnaissance de mappage réseau (DNS).
  - Entités associées : ID, type, nom, Json d’entité unique, Json de profil d’entité unique
- Toutes les activités (événements ou réseau) brutes capturées par les capteurs [!INCLUDE [Product short](includes/product-short.md)] associés à l’alerte, notamment :
  - Activités réseau
  - Activités d’événements

![Entités impliquées](media/involved-entities.png)

### <a name="related-entities"></a>Entités associées

Dans chaque alerte, le dernier onglet présente les **entités connexes**. Les entités associées correspondent à l’ensemble des entités impliquées dans une activité suspecte, sans séparation liée au « rôle » qu’elles ont joué dans l’alerte. Chaque entité a deux fichiers Json : le Json d’entité unique et le Json de profil d’entité unique. Utilisez ces deux fichiers Json pour en savoir plus sur l’entité et pour faciliter l’investigation de l’alerte.

**Json d’entité unique**

Comprend les données relatives au compte apprises par [!INCLUDE [Product short](includes/product-short.md)] à partir d’Active Directory. Sont inclus tous les attributs (par exemple, *Distinguished Name* , *SID* , *LockoutTime* et *PasswordExpiryTime* ). Pour les comptes d’utilisateur, inclut les données telles que *Department* , *Mail* et *PhoneNumber*. Pour les comptes d’ordinateur, sont incluses des données comme *OperatingSystem* , *IsDomainController* et *DnsName*.

**Json de profil d’entité unique**

Comprend toutes les données profilées par [!INCLUDE [Product short](includes/product-short.md)] sur l’entité. [!INCLUDE [Product short](includes/product-short.md)] utilise les activités réseau et les activités d’événements capturées pour caractériser les utilisateurs et les ordinateurs de l’environnement. Il profile les informations pertinentes entité par entité. Ces informations contribuent aux fonctionnalités d’identification des menaces de [!INCLUDE [Product short](includes/product-short.md)].

![Entités associées](media/related-entities.png)

### <a name="how-can-i-use-product-short-information-in-an-investigation"></a>Utilité des informations de [!INCLUDE [Product short](includes/product-short.md)] dans le cadre d’un examen

Les investigations peuvent être aussi détaillées qu’il le faut. Voici quelques méthodes d’examen possibles à l’aide des données fournies par [!INCLUDE [Product short](includes/product-short.md)].

- Vérifiez si tous les utilisateurs associés appartiennent au même groupe ou service.
- Les utilisateurs associés partagent-ils des ressources, des applications ou des ordinateurs ?
- Un compte est-il actif alors que son PasswordExpiryTime est déjà passé ?

## <a name="product-short-and-nnr-network-name-resolution"></a>[!INCLUDE [Product short](includes/product-short.md)] et résolution de noms réseau

Les fonctionnalités de détection de [!INCLUDE [Product short](includes/product-short.md)] s’appuient sur la résolution de noms réseau active pour faire correspondre les adresses IP avec les ordinateurs de votre organisation. [!INCLUDE [Product short](includes/product-short.md)] peut ainsi corréler les activités brutes (contenant des adresses IP) aux ordinateurs concernés impliqués dans chacune d’elles. À partir des activités brutes, il profile les entités, notamment les ordinateurs, et génère des alertes.

Les données de résolution de noms réseau sont cruciales pour détecter les alertes suivantes :

- Suspicion d’usurpation d’identité (pass-the-ticket)
- Suspicion d’attaque DCSync (réplication de services d’annuaire)
- Reconnaissance de mappage de réseau (DNS)

Utilisez les informations de résolution de noms réseau fournies sous l’onglet **Activités réseau** du rapport d’alerte pour déterminer si une alerte est un **FP**. En cas d’alerte **FP** , il est courant que le résultat de certitude de résolution de noms réseau soit donné avec une confiance faible.

Les données des rapports téléchargés apparaissent dans deux colonnes :

- **Ordinateur source/de destination**

  - *Certitude*  : une certitude de faible résolution peut indiquer une résolution de noms incorrecte.
- **Ordinateur source/de destination**
  - *Méthode de résolution*  : indique les méthodes de résolution de noms réseau utilisées pour résoudre l’adresse IP à l’ordinateur de l’organisation.

![Activités réseau](media/network-activities.png)

Pour plus d’informations sur l’utilisation des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)], consultez [Utilisation des alertes de sécurité](working-with-suspicious-activities.md).

## <a name="see-also"></a>Voir aussi

- [Examiner un utilisateur](investigate-a-user.md)
- [Examiner un ordinateur](investigate-a-computer.md)
- [Utilisation des chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
