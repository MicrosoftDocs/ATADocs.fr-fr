---
title: Forum aux questions Azure Advanced Threat Protection | Microsoft Docs
description: Fournit une liste de questions fréquemment posées sur Azure ATP et les réponses correspondantes
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 04/07/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 677dec4468fa272b55d5f9c20c3163fea5770f20
ms.sourcegitcommit: 7a32dcb65edc38fb9b3d340763045b21ea92feee
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59745804"
---
# <a name="azure-atp-frequently-asked-questions"></a>Forum aux questions Azure ATP
Cet article fournit une liste de questions fréquemment posées sur Azure ATP et leur réponse, classées selon les catégories suivantes : 
- [Qu’est-ce qu’Azure ATP ?](#what-is-azure-atp)
- [Gestion des licences et confidentialité](#licensing-and-privacy)
- [Déploiement](#deployment)
- [Fonctionnement](#operation)
- [Résolution des problèmes](#troubleshooting)

## <a name="what-is-azure-atp"></a>Qu’est-ce qu’Azure ATP ?

### <a name="what-can-azure-atp-detect"></a>Que peut détecter Azure ATP ?

Azure ATP détecte les techniques et attaques malveillantes connues, les problèmes de sécurité et les risques qui menacent votre réseau.
Pour obtenir la liste complète des détections fournies par Azure ATP, consultez [Quelles sont les détections effectuées par Azure ATP ?](suspicious-activity-guide.md).

### <a name="what-data-does-azure-atp-collect"></a>Quelles sont les données collectées par Azure ATP ? 

Azure ATP collecte et stocke des informations provenant de vos serveurs configurés (contrôleurs de domaine, serveurs membres, etc.) dans une base de données spécifique au service à des fins d’administration, de suivi et de création de rapports. Les informations collectées comprennent le trafic réseau vers et depuis des contrôleurs de domaine (par exemple, l’authentification Kerberos, l’authentification NTLM, les requêtes DNS), les journaux de sécurité (par exemple, les événements de sécurité Windows), les informations Active Directory (structure, sous-réseaux, sites) et les informations sur les entités (par exemple, les noms, les adresses e-mail et les numéros de téléphone). 

Microsoft utilise ces données pour : 

-   identifier de manière proactive les indicateurs d’attaque dans votre organisation ; 
-   générer des alertes si une possible attaque a été détectée ; 
-   fournir à vos opérations de sécurité une vue sur les entités liées aux signaux des menaces de votre réseau, ce qui vous permet de rechercher et de détecter la présence de menaces de sécurité sur le réseau. 

Microsoft n’exploite pas vos données à des fins publicitaires ni autres que la fourniture du service. 

### <a name="does-azure-atp-only-leverage-traffic-from-active-directory"></a>Azure ATP analyse-t-il seulement le trafic provenant d’Active Directory ?

En plus d’analyser le trafic Active Directory avec une technologie d’inspection approfondie des paquets, Azure ATP collecte également les événements Windows pertinents de votre contrôleur de domaine et crée des profils d’entité selon les informations d’Active Directory Domain Services. Azure ATP prend également en charge la réception de la gestion des comptes RADIUS des journaux VPN provenant de divers fournisseurs (Microsoft, Cisco, F5 et Checkpoint).

### <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>Azure ATP surveille-t-il uniquement les appareils joints à un domaine ?
Non. Azure ATP surveille tous les appareils du réseau qui effectuent des demandes d’authentification et d’autorisation auprès d’Active Directory, notamment les appareils non-Windows et les appareils mobiles.

### <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>Azure ATP surveille-t-il les comptes d’ordinateurs et les comptes d’utilisateurs ?
Oui. Étant donné que les comptes d’ordinateurs (de même que toute autre entité) peuvent être utilisés pour effectuer des activités malveillantes, Azure ATP surveille le comportement de tous les comptes d’ordinateurs et de toutes les autres entités dans l’environnement.

## <a name="licensing-and-privacy"></a>Gestion des licences et confidentialité 

### <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>Où puis-je obtenir une licence pour Azure Advanced Threat Protection (ATP) ?

Azure ATP est disponible dans le cadre de la suite Enterprise Mobility + Security 5 (EMS E5) et sous forme de licence autonome. Vous pouvez acquérir une licence directement sur le [portail Microsoft 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) ou via le modèle de licence de fournisseur de solutions cloud (CSP).

### <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Cette offre va-t-elle faire partie d’Azure Active Directory ou du service Active Directory local ?
La solution Azure ATP est pour l’instant une offre autonome. Elle ne fait partie ni d’Azure Active Directory, ni du service Active Directory local.

### <a name="is-my-data-isolated-from-other-customer-data"></a>Est-ce que mes données sont isolées des données des autres clients ? 

Oui, vos données sont isolées par l’authentification de l’accès et la séparation logique basée sur les identificateurs client. Chaque client peut uniquement accéder aux données collectées dans sa propre organisation et aux données génériques fournies par Microsoft.

### <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>Ai-je la possibilité de sélectionner l’emplacement où stocker mes données ? 

Non. Une fois créée, votre instance Azure ATP est automatiquement stockée dans le centre de données du pays le plus proche de l’emplacement géographique de votre locataire AAD. Après avoir créé votre instance Azure ATP, vous ne pouvez pas déplacer les données Azure ATP dans un autre centre de données.                

### <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Comment est-ce que Microsoft empêche les activités internes malveillantes et les abus de rôles dotés de privilèges élevés ? 

Les développeurs et administrateurs Microsoft, par conception, ont reçu des privilèges suffisants pour effectuer les tâches qui leur ont été affectées afin de faire fonctionner et évoluer le service. Microsoft déploie des combinaisons de contrôles préventifs, défensifs et réactifs favorisant la protection contre les activités de développement et/ou d’administration non autorisées, comprenant les mécanismes suivants : 

-   contrôles d’accès stricts aux données sensibles ; 
-   combinaisons de contrôles améliorant la détection indépendante des activités malveillantes ; 
-   niveaux multiples de surveillance, d’enregistrement et de génération de rapports. 

En outre, Microsoft effectue des vérifications des antécédents sur certains membres du personnel d’exploitation et limite l’accès aux applications, aux systèmes et à l’infrastructure réseau par rapport au niveau de ces vérifications. Le personnel d’exploitation suit un processus formel quand il doit accéder au compte d’un client ou à des informations associées dans l’exercice de ses fonctions. 

## <a name="deployment"></a>Déploiement

### <a name="how-many-azure-atp-sensors-do-i-need"></a>De combien de capteurs Azure ATP ai-je besoin ?

Chaque contrôleur de domaine dans l’environnement doit être couvert par un capteur autonome ou capteur ATP. Pour plus d’informations, consultez [Dimensionnement du capteur Azure ATP](atp-capacity-planning.md#sizing). 

### <a name="does-azure-atp-work-with-encrypted-traffic"></a>Azure ATP prend-il en charge le trafic chiffré ?
Les protocoles réseau avec le trafic chiffré (par exemple LDAPS et IPSEC) ne sont pas chiffrés, mais ils sont analysés par les capteurs.

### <a name="does-azure-atp-work-with-kerberos-armoring"></a>Azure ATP fonctionne-t-il avec le blindage Kerberos ?
L’activation du blindage Kerberos, également appelé FAST (Flexible Authentication Secure Tunneling), est prise en charge par Azure ATP, à l’exception de la détection d’attaques de type « Overpass-the-Hash » qui ne fonctionne pas avec le blindage Kerberos.

### <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>Comment puis-je surveiller un contrôleur de domaine virtuel à l’aide d’Azure ATP ?
La plupart des contrôleurs de domaine virtuels peuvent être couverts par le capteur Azure ATP ; pour déterminer si celui-ci est approprié pour votre environnement, consultez [Planification de la capacité Azure ATP](atp-capacity-planning.md).

Si un contrôleur de domaine virtuel ne peut pas être couvert par le capteur Azure ATP, vous pouvez avoir un capteur autonome Azure ATP virtuel ou physique, comme décrit dans [Configurer la mise en miroir des ports](configure-port-mirroring.md).  <br />Le moyen le plus simple consiste à configurer un capteur autonome Azure ATP virtuel sur chaque hôte où figure un contrôleur de domaine virtuel.<br />Si vos contrôleurs de domaine virtuels passent d’un hôte à l’autre, vous devez effectuer l’une des étapes suivantes :

-   Quand le contrôleur de domaine virtuel passe à un autre hôte, préconfigurez le capteur autonome Azure ATP sur cet hôte pour qu’il reçoive le trafic du contrôleur de domaine virtuel ayant récemment été déplacé.
-   Associez le capteur autonome Azure ATP virtuel au contrôleur de domaine virtuel. Ainsi, s’il est déplacé, le capteur autonome Azure ATP est déplacé en même temps.
-   Certains commutateurs virtuels peuvent envoyer le trafic entre les hôtes.

### <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>Comment configurer les capteurs Azure ATP pour communiquer avec le service cloud Azure ATP en présence d’un proxy ?

Pour que vos contrôleurs de domaine communiquent avec le service cloud, vous devez ouvrir le port 443 dans votre pare-feu/proxy sur *.atp.azure.com. Pour obtenir des instructions sur la façon de procéder, consultez [Configurer votre proxy ou pare-feu pour permettre la communication avec les capteurs Azure ATP](configure-proxy.md).

### <a name="can-azure-atp-monitored-domain-controllers-be-virtualized-on-your-iaas-solution"></a>Les contrôleurs de domaine supervisés par Azure ATP peuvent-ils être virtualisés dans votre solution IaaS ?
Oui, vous pouvez utiliser le capteur Azure ATP pour surveiller les contrôleurs de domaine qui se trouvent dans n’importe quelle solution IaaS.

### <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>Azure ATP peut-il prendre en charge plusieurs domaines et plusieurs forêts ?
Azure Advanced Threat Protection prend en charge les environnements à plusieurs domaines et plusieurs forêts. Pour plus d’informations et les exigences de confiance, consultez [Prise en charge de plusieurs forêts](atp-multi-forest.md).

### <a name="can-you-see-the-overall-health-of-the-deployment"></a>Puis-je examiner l’intégrité globale du déploiement ?
Oui. Vous pouvez examiner l’intégrité globale du déploiement ainsi que les problèmes spécifiques liés à la configuration, à la connectivité, etc. Dès qu’un problème se produit, vous êtes averti par des alertes Azure ATP.

## <a name="operation"></a>Opération

### <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>De quelle façon Azure ATP s’intègre-t-il aux serveurs SIEM ?
Vous pouvez configurer Azure ATP de façon à envoyer une alerte Syslog à n’importe quel serveur SIEM avec le format CEF, dans le cadre des alertes d’intégrité et quand une alerte de sécurité est détectée. Pour plus d’informations, consultez [Informations de référence sur le journal SIEM](cef-format-sa.md).

### <a name="why-are-certain-accounts-considered-sensitive"></a>Pourquoi certains comptes sont-ils considérés comme sensibles ?
Cela arrive quand un compte est membre de groupes désignés comme sensibles (par exemple, « Administrateurs de domaine »).

Pour comprendre pourquoi un compte est sensible, vous pouvez examiner son appartenance au groupe pour déterminer à quels groupes sensibles il appartient. Le groupe auquel il appartient peut également être sensible en raison d’un autre groupe ; dans ce cas, répétez la procédure jusqu’à ce que vous trouviez le groupe sensible de plus haut niveau. Vous pouvez aussi [marquer manuellement des comptes comme étant sensibles](sensitive-accounts.md).

### <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Est-ce que je dois écrire mes propres règles et créer un seuil/une ligne de base ?
Avec Azure Advanced Threat Protection, il est inutile de créer et d’ajuster des règles, des seuils ou des lignes de base. Azure ATP analyse les comportements des utilisateurs, des appareils et des ressources, ainsi que leurs relations mutuelles, et peut détecter rapidement les activités suspectes et les attaques connues. Trois semaines après son déploiement, Azure ATP commence à détecter les activités comportementales suspectes. En revanche, la détection des attaques malveillantes et des problèmes de sécurité connus est opérationnelle immédiatement après le déploiement.

### <a name="which-traffic-does-azure-atp-generate-in-the-network-from-domain-controllers-and-why"></a>Quel trafic Azure ATP génère-t-il dans le réseau à partir des contrôleurs de domaine, et pourquoi ? 

Azure ATP génère le trafic à partir des contrôleurs de domaine sur les ordinateurs de l’organisation dans l’un de trois scénarios :
1. **Résolution de nom réseau**<br>
   Azure ATP capture le trafic et les événements, pour apprendre et dresser le profil des utilisateurs et des activités de l’ordinateur sur le réseau. Pour apprendre et dresser le profil des activités en fonction des ordinateurs de l’organisation, Azure ATP a besoin relier les adresses IP aux comptes d’ordinateurs. Pour relier les adresses IP au nom des ordinateurs, les capteurs Azure ATP demandent l’adresse IP pour le nom d’ordinateur *sous-jacent* à l’adresse IP. <br>
 
   Les requêtes sont effectuées à l’aide d’une des quatre méthodes : 
    - NTLM sur RPC (port TCP 135)
    - NetBIOS (port UDP 137)
    - RDP (port TCP 3389)
    - Interroger le serveur DNS à l’aide de la recherche DNS inversée de l’adresse IP (UDP 53)
    
    Après avoir récupéré le nom d’ordinateur, les capteurs Azure ATP vérifient les détails dans Active Directory pour voir s’il existe un objet ordinateur corrélé à ce nom d’ordinateur. Si une correspondance est trouvée, une association est établie entre l’adresse IP et l’objet ordinateur correspondant.
2. **Chemin de mouvement latéral (LMP)**<br>
    Pour générer des chemins de mouvement latéral potentiels pour les utilisateurs sensibles, Azure ATP requiert des informations sur les administrateurs locaux des ordinateurs. Dans ce scénario, le capteur Azure ATP utilise SAM-R (TCP 445) pour interroger l’adresse IP identifiée dans le trafic réseau, afin de déterminer les administrateurs locaux de l’ordinateur. Pour en savoir plus sur Azure ATP et SAM-R, consultez [Configurer les autorisations requises SAM-R](install-atp-step8-samr.md). 

3. **Interrogation d’Active Directory à l’aide de LDAP** pour les données d’entité<br>
    Les capteurs Azure ATP interrogent le contrôleur de domaine à partir du domaine auquel l’entité appartient. Il peut s’agir du même capteur ou d’un autre contrôleur de domaine de ce domaine. 

|Protocole|Service|Port|Source| Sens|
|---------|---------|---------|---------|--------|
|LDAP|TCP et UDP|389|Contrôleurs de domaine|Sortant|
|LDAP sécurisé (LDAPS)|TCP|636|Contrôleurs de domaine|Sortant|
|LDAP vers le catalogue global|TCP|3268|Contrôleurs de domaine|Sortant|
|LDAPS vers le catalogue global|TCP|3269|Contrôleurs de domaine|Sortant|
|

### <a name="why-dont-activities-always-show-both-the-source-user-and-computer"></a>Pourquoi les activités n’affichent-elles pas toujours l’utilisateur source et l’ordinateur source ?

Azure ATP capture les activités sur de nombreux protocoles différents. Dans certains cas, Azure ATP ne reçoit pas les données de l’utilisateur source dans le trafic. Azure ATP tente de mettre en corrélation la session de l’utilisateur et l’activité, et lorsque la tentative réussit, l’utilisateur source de l’activité est affiché. Lorsque la tentative de corrélation de l’utilisateur échoue, seul l’ordinateur source s’affiche. 

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>Que dois-je faire si le capteur autonome ou le capteur Azure ATP ne démarre pas ?
Examinez l’erreur la plus récente dans le [journal](troubleshooting-atp-using-logs.md) des erreurs actuel (où Azure ATP est installé, sous le dossier « Logs »).


## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Résolution des problèmes](troubleshooting-atp-known-issues.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
