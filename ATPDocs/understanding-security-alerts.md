---
title: Tutoriel sur les alertes de sécurité Azure ATP | Microsoft Docs
d|Description: This article explains how to use and understand Azure ATP security alerts.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/13/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 671747d5-faed-4352-a871-17b58fdc6574
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 490fb20e1fc6e71031c3e3dbf55c3fa13dde4eeb
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674688"
---
# <a name="tutorial-understanding-security-alerts"></a>Tutoriel : Présentation des alertes de sécurité

Les alertes de sécurité Azure ATP expliquent en langage clair et à l’aide de graphismes les activités suspectes qui ont été identifiées sur votre réseau ainsi que les ordinateurs et les acteurs impliqués dans les menaces. Les alertes sont classées par gravité, colorées afin de faciliter le filtrage visuel et organisées par phase de menace. Chaque alerte est conçue pour vous aider à comprendre rapidement et précisément ce qui se passe sur votre réseau. Des listes de preuves d’alertes contiennent des liens directs vers les ordinateurs et les utilisateurs impliqués, afin de rendre vos recherches plus faciles et plus directes.

Dans ce tutoriel, vous allez découvrir la structure des alertes de sécurité Azure ATP et comment les utiliser : 

> [!div class="checklist"]
> * Structure des alertes de sécurité
> * Classifications des alertes de sécurité
> * Catégories des alertes de sécurité
> * Investigation avancée des alertes de sécurité
> * Entités associées
> * Azure ATP et la résolution de noms réseau


## <a name="security-alert-structure"></a>Structure des alertes de sécurité

Chaque alerte de sécurité Azure ATP comprend les éléments suivants :
 
- **Titre de l’alerte** <br> Nom Azure ATP officiel de l’alerte.
- **Description** <br> Brève explication de ce qui s’est passé.
- **Preuve** <br> Informations supplémentaires et pertinentes concernant ce qui s’est passé, afin de vous aider lors du processus d’investigation.
- **Téléchargement Excel** <br> Rapport Excel détaillé à des fins d’analyse

![Structure des alertes de sécurité Azure ATP](media/security-alert-structure.png)

## <a name="security-alert-classifications"></a>Classifications des alertes de sécurité

Après une investigation appropriée, toutes les alertes de sécurité Azure ATP peuvent être classées comme l’un des types d’activités suivants :

- **TP (True positive)**  : action malveillante détectée par Azure ATP.

- **B-TP (benign true positive)**  : action détectée par Azure ATP qui est réelle, mais pas malveillante, comme un test de pénétration ou une activité connue générée par une application approuvée.

- **FP (false positive)**  : fausse alerte. L’activité n’a pas eu lieu.

### <a name="is-the-security-alert-a-tp-b-tp-or-fp"></a>L’alerte de sécurité est-elle TP, B-TP ou FP ?

Pour chaque alerte, posez-vous les questions suivantes afin de déterminer la classification d’alerte et de vous aider à décider de la marche à suivre :

1. Quelle est la fréquence de cette alerte de sécurité spécifique dans votre environnement ?
2. L’alerte a-t-elle été déclenchée par les mêmes types d’ordinateurs ou d’utilisateurs
   (par exemple, des serveurs ayant le même rôle ou des utilisateurs du même groupe/service) ? Si les ordinateurs ou utilisateurs étaient similaires, vous pouvez décider de les exclure afin d’éviter de recevoir ultérieurement d’autres alertes FP.

Remarque : Une augmentation des alertes du même type réduit généralement le niveau d’importance/de suspicion de l’alerte. Pour les alertes répétées, vérifiez les configurations et utilisez les détails et les définitions de l’alerte de sécurité afin de comprendre exactement ce qui déclenche la répétition. 

## <a name="security-alert-categories"></a>Catégories des alertes de sécurité

Les alertes de sécurité d’Azure ATP sont divisées en catégories ou phases (voir ci-dessous), comme les phases d’une chaîne de destruction de cyberattaque standard. Apprenez-en davantage sur chaque phase et sur les alertes conçues pour détecter chaque attaque grâce aux liens suivants :

- [Alertes de reconnaissance](atp-reconnaissance-alerts.md)
- [Alertes indiquant des informations d’identification compromises](atp-compromised-credentials-alerts.md)
- [Alertes de mouvement latéral](atp-lateral-movement-alerts.md)
- [Alertes de dominance du domaine](atp-domain-dominance-alerts.md)
- [Alertes d’exfiltration](atp-exfiltration-alerts.md)

## <a name="advanced-security-alert-investigation"></a>Investigation avancée des alertes de sécurité

Pour obtenir plus de détails sur une alerte de sécurité, téléchargez le rapport d’alerte détaillé Excel.

1. Cliquez sur les trois points dans le coin supérieur droit d’une alerte et sélectionnez *Télécharger les détails*.
 
Chaque téléchargement Excel d’alerte Azure ATP fournit les informations suivantes :   
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
- Toutes les activités brutes capturées par les capteurs Azure ATP associés à l’alerte (activités d’événements ou réseau), notamment :
  - Activités réseau
  - Activités d’événements

![Entités impliquées](media/involved-entities.png)

### <a name="related-entities"></a>Entités associées

Dans chaque alerte, le dernier onglet présente les **entités connexes**. Les entités associées sont toutes les entités impliquées dans une activité suspecte, sans la séparation du « rôle » qu’elles ont joué dans l’alerte. Chaque entité a deux fichiers Json : le Json d’entité unique et le Json de profil d’entité unique. Utilisez ces deux fichiers Json pour en savoir plus sur l’entité et pour faciliter l’investigation de l’alerte. 
 
**Json d’entité unique**
 
Inclut les données qu’Azure ATP a apprises à partir d’Active Directory concernant le compte. Cela comprend tous les attributs, comme *Distinguished Name*, *SID*, <em>LockoutTime et *PasswordExpiryTime</em>. Pour les comptes d’utilisateur, inclut les données telles que *Department*, *Mail* et *PhoneNumber*. Pour les comptes d’ordinateur, inclut les données comme *OperatingSystem*, <em>IsDomainController et *DnsName</em>.

**Json de profil d’entité unique**

Inclut toutes les données qu’Azure ATP a profilé sur l’entité. Azure ATP utilise les activités d’événements et les activités réseau capturées pour en savoir plus sur les utilisateurs et les ordinateurs de l’environnement. Azure ATP profile les informations pertinentes par entité. Ces informations contribuent aux fonctionnalités d’identification des menaces d’Azure ATP.

![Entités associées](media/related-entities.png)
 
### <a name="how-can-i-use-azure-atp-information-in-an-investigation"></a>Comment puis-je utiliser les informations d’Azure ATP lors d’une investigation ? 

Les investigations peuvent être aussi détaillées qu’il le faut. Voici quelques idées de méthodes d’investigation à l’aide des données fournies par Azure ATP.

- Vérifiez si tous les utilisateurs associés appartiennent au même groupe ou service.
- Les utilisateurs associés partagent-ils des ressources, des applications ou des ordinateurs ?
- Un compte est-il actif alors que son PasswordExpiryTime est déjà passé ?

## <a name="azure-atp-and-nnr-network-name-resolution"></a>Azure ATP et la résolution de noms réseau

Les fonctionnalités de détection d’Azure ATP s’appuient sur la résolution de noms réseau active pour résoudre les adresses IP aux ordinateurs de votre organisation. Avec la résolution de noms réseau, Azure ATP peut corréler les activités brutes (contenant des adresses IP) aux ordinateurs concernés impliqués dans chaque activité. Sur la base des activités brutes, Azure ATP profile les entités, notamment les ordinateurs, et génère des alertes.

Les données de résolution de noms réseau sont cruciales pour détecter les alertes suivantes :
- Suspicion d’usurpation d’identité (pass-the-ticket) 
- Suspicion d’attaque DCSync (réplication de services d’annuaire)
- Reconnaissance de mappage de réseau (DNS)

Utilisez les informations de résolution de noms réseau fournies sous l’onglet **Activités réseau** du rapport d’alerte pour déterminer si une alerte est un **FP**. En cas d’alerte **FP**, il est courant que le résultat de certitude de résolution de noms réseau soit donné avec une confiance faible.

Les données des rapports téléchargés apparaissent dans deux colonnes : 
- **Ordinateur source/de destination** 

    - *Certitude* : une certitude de faible résolution peut indiquer une résolution de noms incorrecte.
- **Ordinateur source/de destination**
    - *Méthode de résolution* : indique les méthodes de résolution de noms réseau utilisées pour résoudre l’adresse IP à l’ordinateur de l’organisation.

![Activités réseau](media/network-activities.png)

Pour plus d’informations sur l’utilisation des alertes de sécurité d’Azure ATP, consultez [Utilisation des alertes de sécurité](working-with-suspicious-activities.md).

## <a name="see-also"></a>Voir aussi

- [Examiner un utilisateur](investigate-a-user.md)
- [Examiner un ordinateur](investigate-a-computer.md)
- [Utilisation des chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
