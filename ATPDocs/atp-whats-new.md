---
title: Nouveautés d’Azure ATP | Microsoft Docs
description: Décrit les dernières versions release d’Azure ATP et fournit des informations sur les nouveautés de chaque version.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/8/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6d794e2d30b51d78bd3e4af76d8bd4a48b2d413f
ms.sourcegitcommit: 8472f3f46fc90da7471cd1065cdb2f6a1d5a9f69
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/08/2018
---
*S’applique à : Azure Advanced Threat Protection*


# <a name="whats-new-in-azure-atp"></a>Nouveautés d’Azure ATP 



## <a name="azure-atp-release-231"></a>Azure ATP version 2.31

Publication : 6 mai 2018
 
- Des améliorations ont été apportées à la résolution de noms. Dans ce cadre, en plus de la résolution active RPC et NetBIOS, le capteur peut émettre un paquet Client Hello TLS vers le port RDP du point de terminaison (3389). 
- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes. 

## <a name="azure-atp-release-230"></a>Azure ATP version 2.30

Publication : 29 avril 2018
 
- Les activités de passage à une version antérieure de chiffrement suspectes incluent désormais une section de preuve qui décrit les symptômes détectés par Azure ATP provoquant la suspicion de l’apparition d’une activité de passage à une version antérieure de chiffrement. 
-   Azure ATP utilise désormais Azure E-mail Orchestrator pour tous les e-mails envoyés à partir de Azure ATP, y compris les activités suspectes, alertes et rapports de surveillance. Vous verrez que ces notifications par e-mail désormais suivent un format cohérent pour la facilité d’utilisation et les fichiers Excel seront liés par e-mail pour être téléchargés à partir de la console.
 
 

## <a name="azure-atp-release-229"></a>Azure ATP version 2.29

Publication : 22 avril 2018
 
- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes. 
 
 
## <a name="azure-atp-release-228"></a>Azure ATP version 2.28

Publication : 15 avril 2018
 
-   Les utilisateurs membres des groupes de rôles Utilisateurs Azure ATP et Observateurs ATP Azure sont à présent autorisés à voir les alertes de surveillance.
- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes. 


## <a name="azure-atp-release-227"></a>Azure ATP version 2.27

Publication : 8 avril 2018

- Vous avez maintenant la possibilité de fournir des commentaires utilisateur à partir de la barre de navigation supérieure. Cliquez sur l’émoticône dans la barre de menus pour envoyer un e-mail contenant vos commentaires à l’équipe Azure ATP.

- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes. 
 

## <a name="azure-atp-release-226"></a>Azure ATP version 2.26

Date de publication : 25 mars 2018

- Quand Azure ATP vous avertit d’une activité suspecte que vous identifiez comme activité positive sans gravité (une action légitime qui n’est pas une activité suspecte) vous avez la possibilité d’exclure des ordinateurs et des adresses IP pour plus de détections, notamment : rétrogradation de chiffrement, LDAP force brute, PAC falsifié, Force brute et Pass-the-hash.
-   Les performances du capteur Azure ATP ont été améliorées.
-   Une nouvelle région a été ajoutée pour le déploiement de l’espace de travail, vous pouvez désormais déployer un espace de travail en Asie. 


## <a name="azure-atp-release-225"></a>Azure ATP version 2.25

Date de publication : 18 mars 2018

- L’authentification multifacteur (MFA) est maintenant prise en charge dans Azure ATP. Les locataires qui utilisent MFA peuvent maintenant accéder au portail Azure ATP.
- Azure ATP propose désormais une page [**État du système**](https://health.atp.azure.com/) pour vous indiquer si le portail de gestion Espace de travail est opérationnel et actif, s’il existe des problèmes avec les détections et si la sonde est en mesure d’envoyer du trafic vers le cloud. Vous pouvez accéder à l’**État du système** dans la barre de menus Azure ATP.


## <a name="azure-atp-release-224"></a>Azure ATP version 2.24

Date de publication : 11 mars 2018

**Détections nouvelles et mises à jour**
  - Création de service suspect : les attaquants tentent d’exécuter des services suspects sur votre réseau. Azure ATP génère désormais une alerte quand il s’aperçoit qu’un utilisateur sur un ordinateur spécifique est en train d’exécuter un nouveau service qui semble douteux. Cette détection est basée sur des événements (pas sur le trafic réseau) et est effectuée sur un contrôleur de domaine de votre réseau qui transfère l’événement 7045 à Azure ATP. Pour plus d’informations, consultez le [Guide des activités suspectes](suspicious-activity-guide.md).

**Investigation avancée**
  - Azure ATP comprend un [profil d’entité](entity-profiles.md) complet. Le profil d’entité vous offre une plateforme conçue pour investiguer en profondeur les activités des utilisateurs, ce qui inclut les ressources auxquelles ils ont accédé, les ordinateurs sur lesquels ils se sont connectés, et bien plus encore. Le profil d’entité fournit également des données de répertoire et vous permet d’identifier les chemins de mouvement latéral potentiels à destination ou en provenance de l’entité afin d’en savoir plus sur les failles potentielles de votre organisation.

  - ATP vous permet de marquer manuellement les entités comme *sensibles* pour améliorer la détection et la surveillance. Ce marquage a un impact sur de nombreuses détections Azure ATP, telles que la détection des modifications des groupes sensibles et le [chemin de mouvement latéral](use-case-lateral-movement-path.md), qui reposent sur des entités considérées comme sensibles.

**Nouveaux rapports pour vous aider dans votre investigation**
  - Le [rapport sur les mots de passe exposés en texte clair](reports.md) vous permet de détecter quand des services envoient des informations d’identification de compte en texte brut. Vous pouvez ainsi investiguer les services et améliorer le niveau de sécurité de votre réseau. Ce rapport remplace les alertes d’activité suspecte en texte clair.
  - Le [rapport sur les chemins de mouvement latéral vers des comptes sensibles](reports.md) liste les comptes sensibles qui sont exposés via des chemins de mouvement latéral. Il vous permet de limiter ces chemins et de renforcer votre réseau pour réduire le risque de surface d’attaque. Vous pouvez ainsi empêcher le mouvement latéral pour ne pas que les attaquants se déplacent sur votre réseau entre les utilisateurs et les ordinateurs et finissent par toucher le jackpot en termes de sécurité virtuel : vos informations d’identification de compte administrateur sensibles.

- Il est à présent facile d’accéder à la documentation à partir d’un lien fourni dans les alertes d’activité suspectes qui vous permettra de voir les [étapes d’investigation que vous pouvez suivre](suspicious-activity-guide.md). 

**Améliorations des performances**
 -  L’infrastructure des capteurs Azure ATP a été améliorée au niveau des performances : la vue de synthèse du trafic permet l’optimisation du pipeline des paquets et du processeur, et réutilise les sockets sur les contrôleurs de domaine pour minimiser les sessions SSL sur ces derniers.

## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)