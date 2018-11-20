---
title: Nouveautés d’Azure ATP | Microsoft Docs
description: Décrit les dernières versions release d’Azure ATP et fournit des informations sur les nouveautés de chaque version.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2237834e867aa6bdacbc67fcc1244f07ac88711b
ms.sourcegitcommit: 2afc1486b40431f442d51a53df06e289796de87e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560743"
---
*S’applique à : Azure Advanced Threat Protection*

# <a name="whats-new-in-azure-atp"></a>Nouveautés d’Azure ATP 

## <a name="azure-atp-release-254"></a>Azure ATP version 2.5.4
Publication : 11 novembre 2018

- **Amélioration de fonctionnalité : Des exclusions de domaine par défaut ont été ajoutées à l’alerte Communication suspecte sur DNS**<br>   Trois autres domaines courants ont été ajoutés à la liste des exclusions de domaine par défaut. La liste des exclusions reste entièrement personnalisable. Pour en savoir plus, consultez [Exclusion d’entités des détections](excluding-entities-from-detections.md). 

- **Améliorations de la documentation : Mise à jour sur les journaux SIEM et conseils pour les problèmes connus**<br>    Un mappage des externalId ainsi que des explications complémentaires ont été ajoutés aux descriptions dans les journaux SIEM. Pour en savoir plus, consultez [Informations de référence sur les journaux SIEM](cef-format-sa.md). <br>Un article a été ajouté pour fournir des conseils au sujet de problèmes connus non encore résolus. Pour en savoir plus, consultez [Problèmes connus dans Azure ATP](known-issues.md).  

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-253"></a>Azure ATP version 2.5.3
Publication : 4 novembre 2018

- **Amélioration d’alerte de sécurité : échec d’authentification suspecte**<br>
L’[alerte de sécurité d’échec d’authentification suspecte](suspicious-activity-guide.md) d’Azure ATP inclut désormais la surveillance pour la détection des attaques en force par pulvérisation de mots de passe.
Dans une attaque par **pulvérisation de mots de passe** classique, après avoir correctement dressé la liste des utilisateurs valides à partir du contrôleur de domaine, les attaquants tentent d’utiliser UN mot de passe élaboré avec soin sur tous les comptes d’utilisateur connus (un mot de passe sur de nombreux comptes). Lorsque la pulvérisation de mots de passe initiale échoue, ils réessayent en utilisant un autre mot de passe élaboré avec soin, généralement après avoir attendu 30 minutes entre les tentatives. Ce délai d’attente évite aux attaquants de déclencher la plupart des seuils de verrouillage de compte temporels. La pulvérisation de mots de passe est rapidement devenue la technique préférée des pirates et des tests d’intrusion. Les attaques par pulvérisation de mots de passe se sont révélées efficaces pour créer une brèche dans une organisation et pour effectuer des déplacements latéraux afin d’essayer d’élever des privilèges. 

- **Amélioration de fonctionnalité : Envoyer un message test Syslog**<br>   Nouvelle possibilité d’envoyer un message test Syslog pendant le processus de configuration SIEM. Consultez [Intégrer à Syslog](setting-syslog.md) pour en savoir plus. 

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-252"></a>Azure ATP version 2.5.2
Publication : 28 octobre 2018


- **Amélioration d’alerte de sécurité : Tentative d’exécution de code à distance**<br>
L’[alerte de sécurité Tentative d’exécution de code à distance](suspicious-activity-guide.md) d’Azure ATP englobe désormais la supervision des tentatives suspectes d’exécution de code PowerShell à distance sur vos contrôleurs de domaine. Remote PowerShell est une méthode courante d’exécution de commandes d’administration valides, mais elle est souvent utilisée à des fins malveillantes pour tenter d’exécuter des scripts sur des points de terminaison distants. 

- **Amélioration de fonctionnalité : Définir une planification de rapport**
<br>Vous pouvez désormais définir une heure de planification spécifique pour vos rapports Azure ATP à l’aide de la fonction [rapports](reports.md#). 

- **Ajout de configuration : Contrôle d’accès en fonction du rôle de locataire (RBAC)**
<br>Configurez les rôles de sécurité de votre locataire dans le Centre d’administration Azure Active Directory (AAD) directement à partir du nouveau lien Administrateur du portail Azure ATP. 

- **Révision de la structure et du contenu de la documentation**
<br>Le contenu de la documentation Azure ATP a fait récemment l’objet de modifications avec l’ajout de nouveaux articles listant toutes les activités supervisées dans Azure ATP, des instructions pour filtrer les activités, ainsi qu’une remise à plat de la structure du site de la documentation pour l’utiliser plus facilement :
  - [Activités supervisées par Azure ATP](monitored-activities.md) 
  - [Filtrage des activités dans Azure ATP](atp-activities-search.md) 
  - [Documentation Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/)  

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-251"></a>Azure ATP version 2.5.1
Publication : 21 octobre 2018

- Maintenant, vous pouvez activer/désactiver l’**intégration WD-ATP** à partir de l’écran [Configuration](integrate-wd-atp.md#how-to-integrate-azure-atp-with-windows-defender-atp) du portail Azure ATP. (Pour accéder à cette fonctionnalité, l’utilisateur Azure ATP doit être administrateur général ou de la sécurité sur le locataire AAD).

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-250"></a>Azure ATP version 2.50
Publication : 14 octobre 2018
- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes.


## <a name="azure-atp-release-249"></a>Azure ATP version 2.49
Publication : 7 octobre 2018
-   **Nouvelles détections : Communication DNS suspecte** (préversion)<br>Nouvelle détection ajoutée pour renforcer la protection contre les attaques de communication suspecte sur le DNS :

    -   Cette détection permet de détecter les attaques contre le protocole DNS. Dans la plupart des organisations, le protocole DNS n’est pas supervisé et les activités malveillantes sont rarement bloquées. Un attaquant peut alors accéder à une machine compromise afin d’utiliser le protocole DNS de manière abusive. Des communications malveillantes via DNS peuvent être utilisées pour l’exfiltration, des commandes et le contrôle des données, et/ou l’affranchissement des limitations du réseau d’entreprise.

- **Nouvelle fonctionnalité** <br>**Rôle d’utilisateur** Azure ATP amélioré avec les fonctionnalités suivantes :
  - Changer l’état des alertes de sécurité (rouvrir, fermer, exclure, supprimer)
  - Définir des rapports planifiés
  - Définir des étiquettes d’entité (sensible et honeytoken)
  - Exclusion de la détection
  - Changer la langue
  - Définir des notifications via e-mail ou Syslog


- Une augmentation temporaire des alertes de sécurité **Reconnaissance à l’aide de requêtes de services d’annuaire** qui s’est produite le 16 septembre 2018 a été identifiée et résolue. 

- Cette version comprend aussi des correctifs et des améliorations visant plusieurs problèmes.


## <a name="azure-atp-release-248"></a>Azure ATP version 2.48
Publication : 16 septembre 2018
- **Alerte de sécurité :** Reconnaissance à l’aide de requêtes de services d’annuaire

  Cette alerte de sécurité a désormais une infographie et des preuves améliorées. 

- **Exclure des entités des détections** 

  Pour réduire les faux positifs, vous pouvez maintenant choisir d’exclure des entités des détections suivantes : 
  - Connexion VPN suspecte (exclusion d’utilisateur)
  - Promotion du contrôleur de domaine suspect (attaque potentielle DcShadow)
  - Demande de réplication suspecte (attaque potentielle DcShadow)

- Cette version comprend aussi des correctifs et des améliorations visant plusieurs problèmes.


## <a name="azure-atp-release-247"></a>Azure ATP version 2.47
Publication : 2 septembre 2018

- **Vérification des stratégies d’audit avancées d’Azure ATP**
 
Azure - Protection avancée contre les menaces (Azure ATP) vérifie maintenant les stratégies d’audit avancées existantes de votre contrôleur de domaine et recommande des modifications à apporter aux stratégies, de façon à fournir une couverture maximale du service Azure ATP pour votre organisation. 

**Cette nouvelle vérification vous permet de :**
  -  Identifier les événements manquants dans vos journaux des événements Windows, qui sont actuellement exclus de votre couverture Azure ATP.
  -  Vérifiez les paramètres idéaux et apporter des modifications sur la base des recommandations fournies quant aux alertes d’intégrité.
  -  Une même alerte d’intégrité agrégée est émise pour tous vos contrôleurs de domaine, avec des suggestions de correction (le cas échéant, si nécessaire).

Examinez comment [configurer les stratégies d’audit avancées](atp-advanced-audit-policy.md) pour vérifier que votre système est configuré correctement. 
- Cette version comprend aussi des correctifs et des améliorations visant plusieurs problèmes.

## <a name="azure-atp-release-246"></a>Azure ATP version 2.46

Publication : 26 août 2018

- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes.

## <a name="azure-atp-release-245"></a>Azure ATP version 2.45

Publication : 19 août 2018

- **Azure ATP ajoute le Suivi d’événements pour Windows (ETW) comme source de données supplémentaires**  <br> Suivi d’événements pour Windows (ETW) ajouté en tant que source de données supplémentaire en plus du trafic réseau existant et des événements Windows. ETW fournit des détections d’activité suspecte supplémentaires, notamment : les promotions du contrôleur de domaine suspect et les demandes de réplication de contrôleur de domaine suspectes (deux attaques DCShadow potentielles). <br>
Seuls les capteurs ATP installés sur les contrôleurs de domaine prennent en charge les détections basées sur ETW. Les détections ETW ne sont pas prises en charge par les capteurs autonomes ATP. <br>  

- **Quatre nouvelles détections maintenant en disponibilité générale** <br>
  - Connexion VPN suspecte
  - Golden Ticket Kerberos - compte inexistant 
  - Promotion du contrôleur de domaine suspect (attaque DCShadow potentielle) - détection basée sur ETW, disponible uniquement avec les capteurs ATP 
  - Demande de réplication du contrôleur de domaine suspecte (attaque DCShadow potentielle) - détection basée sur ETW, disponible uniquement avec les capteurs ATP

- Cette version comprend aussi des correctifs et des améliorations visant plusieurs problèmes.


## <a name="azure-atp-release-244"></a>Azure ATP version 2.44

Publication : 12 août 2018

- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes.
- Les fichiers journaux créés sur l’ordinateur du capteur n’incluent plus le journal « Exception Statistic ».


## <a name="azure-atp-release-243"></a>Azure ATP version 2.43

Publication : 5 août 2018

- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes.



## <a name="azure-atp-release-242"></a>Azure ATP version 2.42

Publication : 29 juillet 2018

- Cette version comprend des correctifs et des améliorations visant plusieurs problèmes. 


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
- [Présentation d’Azure - Protection avancée contre les menaces](what-is-atp.md)
- [Forum Aux Questions](atp-technical-faq.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md) (configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)