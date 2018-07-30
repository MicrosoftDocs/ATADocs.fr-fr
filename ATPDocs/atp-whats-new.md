---
title: Nouveautés d’Azure ATP | Microsoft Docs
description: Décrit les dernières versions release d’Azure ATP et fournit des informations sur les nouveautés de chaque version.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: be3a4315384d5df03b1f04f0a71a960c66858b05
ms.sourcegitcommit: 63a36cd96aec30e90dd77bee1d0bddb13d2c4c64
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39227221"
---
*S’applique à : Azure Advanced Threat Protection*


# <a name="whats-new-in-azure-atp"></a>Nouveautés d’Azure ATP 


## <a name="azure-atp-release-241"></a>Azure ATP version 2.41

Publication : 22 juillet 2018

- **La prise en charge des forêts multiples Azure ATP est progressivement déployée (préversion)** <br> Azure ATP est maintenant capable de gérer les organisations qui ont plusieurs forêts, ce qui permet d’effectuer le monitoring des activités et de profiler les utilisateurs sur les différentes forêts. Cette nouvelle fonctionnalité :

  - permet de voir et d’examiner les activités effectuées par les utilisateurs dans différentes forêts sur un seul écran ;
  - améliore la détection et réduit les faux positifs grâce à l’intégration Active Directory avancée et à la résolution de comptes ;
  - fournit de meilleures alertes de monitoring et fonctionnalités de création de rapports pour une couverture interorganisationnelle.


-   **Nouvelles détections : DCShadow**<br>Deux nouvelles détections ont été ajoutées pour vous protéger contre les attaques DCShadow (« Domain Controller Shadow ») :

    -   Promotion des contrôleurs de domaine suspects (attaque potentielle DCShadow) : cette détection permet de détecter les attaques selon lesquelles un ordinateur emprunte l’identité d’un contrôleur de domaine, puis essaie d’utiliser la réplication pour propager les modifications à d’autres contrôleurs de domaine dans votre domaine.

    -   Demande de réplication suspecte (attaque potentielle DCShadow) : cette détection permet de protéger contre les attaques qui tentent d’effectuer une promotion au statut de contrôleur de domaine sur des ordinateurs qui ne l’ont pas afin de modifier les objets annuaire.

-   **Amélioration des informations sur le passage à une version antérieure du chiffrement**<br>La détection du passage à une version antérieure du chiffrement donne maintenant des informations supplémentaires sur le type d’attaque détecté : Overpass-the-Hash, golden ticket et Skeleton Key. Par ailleurs, ces alertes ont été agrégées pour faciliter les recherches.
- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes. 



## <a name="azure-atp-release-240"></a>Azure ATP version 2.40

Publication : 15 juillet 2018

- La détection pass-the-ticket comprend maintenant une section de preuve dans la page des détails de l’alerte. Vous bénéficiez ainsi d’informations supplémentaires pour investiguer l’alerte.

- Les indicateurs de contrôle d’accès utilisateur, qui se trouvent dans le profil de l’utilisateur sous Données d’annuaire, ont maintenant une légende qui vous permettra de mieux comprendre quels sont les attributs activés et désactivés.  

## <a name="azure-atp-release-239"></a>Azure ATP version 2.39

Publication : 5 juillet 2018
-   **Ajout d’une nouvelle détection : golden ticket Kerberos - compte non existant** (préversion)<br>Cette nouvelle détection vous aide à protéger votre organisation contre les attaques dans lesquelles un golden ticket est créé pour un compte qui n’existe pas dans votre domaine. Pour plus d’informations, consultez le [Guide Azure - Protection avancée contre les menaces (ATP) des activités suspectes](suspicious-activity-guide.md#golden-ticket)

- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes. 


## <a name="azure-atp-release-238"></a>Azure ATP version 2.38

Publication : 1er juillet 2018

- Cette version inclut des correctifs et des améliorations pour plusieurs problèmes, ainsi que des améliorations du portail Azure ATP.

## <a name="azure-atp-release-237"></a>Azure ATP version 2.37

Publication : 24 juin 2018

- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes. 

## <a name="azure-atp-release-236"></a>Azure ATP version 2.36

Publication : 17 juin 2018

- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes. 


## <a name="azure-atp-release-235"></a>Azure ATP version 2.35

Publication : 10 juin 2018
 
- **Nouvelles détections en préversion**<br></br>À partir de maintenant, Azure ATP tire parti du fait qu’il est un service cloud, où les nouvelles fonctionnalités peuvent être livrées par cycles rapides, pour vous fournir de nouvelles détections aussi vite que possible. Ces nouvelles détections sont marquées en « préversion » lors de leur publication. En général, une nouvelle détection passe de préversion à disposition générale en quelques semaines. Par défaut, vous voyez les détections en préversion. Si vous ne voulez pas les voir, consultez [Détections en préversion](working-with-suspicious-activities.md#preview-detections).
 
- **Détection de VPN suspect**<br></br>Cette version introduit une préversion de la détection de VPN suspect. Azure ATP apprend le comportement VPN des utilisateurs, notamment les ordinateurs auxquels se connectent les utilisateurs et les emplacements à partir desquels ils se connectent, et vous alerte quand il détecte un écart avec le comportement attendu. Pour plus d’informations, consultez [Détection de VPN suspect](suspicious-activity-guide.md#suspicious-vpn-detection).

- **Mise à jour différée**<br></br>Vous avez maintenant la possibilité de définir des capteurs Azure ATP pour différer les mises à jour chaque fois qu’Azure ATP se met à jour. Vous pouvez définir chaque capteur Azure ATP sur **Mise à jour différée** pour déclencher la mise à jour 24 heures après la mise à jour du service cloud Azure ATP. Cette fonctionnalité vous permet de tester la mise à jour sur des capteurs de test spécifiques et de mettre à jour vos capteurs de production seulement après. Si vous découvrez un problème pendant le premier cycle de mise à jour, ouvrez un ticket de support. Pour plus d’informations, consultez [Mettre à jour les capteurs Azure ATP](sensor-update.md).

- **Mise à jour de la détection d’implémentation de protocole inhabituelle**<br></br>La détection d’implémentation de protocole inhabituelle fournit des informations supplémentaires. Maintenant, vous pouvez voir quel outil d’attaque potentiel Azure ATP soupçonne d’agir sur votre réseau. Pour plus d’informations, consultez le [Guide des activités suspectes](suspicious-activity-guide.md).
 
- **Alerte de capteur obsolète**<br></br>Azure ATP inclut une nouvelle alerte de monitoring pour vous permettre de savoir si un capteur a plus de trois versions de retard. Si vous voyez cette alerte, vous devez mettre à jour le capteur ou rechercher pourquoi le capteur n’est pas mis à jour automatiquement. Si l’alerte persiste, désinstallez et réinstallez le capteur.

- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes. 

## <a name="azure-atp-release-234"></a>Azure ATP version 2.34

Publication : 3 juin 2018
 
- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes. 

 
## <a name="azure-atp-release-233"></a>Azure ATP version 2.33

Publication : 27 mai 2018

- Fonctionnalité en préversion : Azure ATP prend désormais en charge de nouvelles langues et 13 nouveaux paramètres régionaux :
    - Tchèque
    - Hongrois
    - Italien
    - Coréen
    - Néerlandais
    - Polonais
    - Portugais (Brésil)
    - Portugais (Portugal)
    - Russie
    - Suédois
    - Turc
    - Chinois (Chine)
    - Chinois (Taïwan)



## <a name="azure-atp-release-232"></a>Azure ATP version 2.32

Publication : 13 mai 2018
 
- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes. 

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