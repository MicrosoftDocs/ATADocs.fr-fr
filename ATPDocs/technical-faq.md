---
title: Forum aux questions sur Microsoft Defender for Identity
description: Fournit une liste de questions fréquemment posées sur Microsoft Defender pour l’identité et les réponses associées.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ccb3ee9afe32615246f8e6dc63e181475094a8b7
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93274370"
---
# <a name="product-long-frequently-asked-questions"></a>[!INCLUDE [Product long](includes/product-long.md)] Forum aux questions

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Cet article fournit une liste des questions fréquemment posées et des réponses sur [!INCLUDE [Product long](includes/product-long.md)] divisées dans les catégories suivantes :

- [Quoi [!INCLUDE [Product short](includes/product-short.md)]](#what-is-azure-atp)
- [Gestion des licences et confidentialité](#licensing-and-privacy)
- [Déploiement](#deployment)
- [Fonctionnement](#operation)
- [Résolution des problèmes](#troubleshooting)

<a name="what-is-azure-atp"></a>

## <a name="what-is-product-short"></a>Qu’est-ce que c’est [!INCLUDE [Product short](includes/product-short.md)] ?

### <a name="what-can-product-short-detect"></a>Que peut [!INCLUDE [Product short](includes/product-short.md)] détecter ?

[!INCLUDE [Product short](includes/product-short.md)] détecte les attaques et les techniques malveillantes connues, les problèmes de sécurité et les risques liés à votre réseau.
Pour obtenir la liste complète des [!INCLUDE [Product short](includes/product-short.md)] détections, consultez [Quelles sont les détections [!INCLUDE [Product short](includes/product-short.md)] effectuées ?](suspicious-activity-guide.md).

### <a name="what-data-does-product-short-collect"></a>Quelles sont les données [!INCLUDE [Product short](includes/product-short.md)] collectées ?

[!INCLUDE [Product short](includes/product-short.md)] collecte et stocke des informations à partir de vos serveurs configurés (contrôleurs de domaine, serveurs membres, etc.) dans une base de données spécifique au service à des fins d’administration, de suivi et de création de rapports. Les informations collectées comprennent le trafic réseau vers et depuis des contrôleurs de domaine (par exemple, l’authentification Kerberos, l’authentification NTLM, les requêtes DNS), les journaux de sécurité (par exemple, les événements de sécurité Windows), les informations Active Directory (structure, sous-réseaux, sites) et les informations sur les entités (par exemple, les noms, les adresses e-mail et les numéros de téléphone).

Microsoft utilise ces données pour :

- identifier de manière proactive les indicateurs d’attaque dans votre organisation ;
- générer des alertes si une possible attaque a été détectée ;
- fournir à vos opérations de sécurité une vue sur les entités liées aux signaux des menaces de votre réseau, ce qui vous permet de rechercher et de détecter la présence de menaces de sécurité sur le réseau.

Microsoft n’exploite pas vos données à des fins publicitaires ni autres que la fourniture du service.

### <a name="how-many-directory-service-credentials-does-product-short-support"></a>Combien d’informations d’identification du service d’annuaire [!INCLUDE [Product short](includes/product-short.md)] prennent en charge ?

[!INCLUDE [Product short](includes/product-short.md)] prend actuellement en charge l’ajout de 10 informations d’identification de service d’annuaire différentes pour prendre en charge Active Directory environnements avec des forêts non approuvées. Si vous avez besoin de comptes supplémentaires, ouvrez un ticket de support.

### <a name="does-product-short-only-leverage-traffic-from-active-directory"></a>N’utilise-t- [!INCLUDE [Product short](includes/product-short.md)] il que le trafic provenant de Active Directory ?

Outre l’analyse du trafic Active Directory à l’aide de la technologie d’inspection approfondie des paquets, [!INCLUDE [Product short](includes/product-short.md)] collecte également les événements Windows pertinents à partir de votre contrôleur de domaine et crée des profils d’entité basés sur les informations de Active Directory Domain Services. [!INCLUDE [Product short](includes/product-short.md)] prend également en charge la gestion de la comptabilité RADIUS des journaux VPN de différents fournisseurs (Microsoft, Cisco, F5 et Checkpoint).

### <a name="does-product-short-monitor-only-domain-joined-devices"></a>N' [!INCLUDE [Product short](includes/product-short.md)] analyse que les appareils joints à un domaine ?

Non. [!INCLUDE [Product short](includes/product-short.md)] surveille tous les appareils du réseau qui effectuent des demandes d’authentification et d’autorisation sur Active Directory, y compris les appareils non-Windows et mobiles.

### <a name="does-product-short-monitor-computer-accounts-as-well-as-user-accounts"></a>Est-il [!INCLUDE [Product short](includes/product-short.md)] possible de surveiller les comptes d’ordinateur ainsi que les comptes d’utilisateur ?

Oui. Étant donné que les comptes d’ordinateurs (ainsi que toutes les autres entités) peuvent être utilisés pour effectuer des activités malveillantes, [!INCLUDE [Product short](includes/product-short.md)] surveille le comportement de tous les comptes d’ordinateur et toutes les autres entités de l’environnement.

### <a name="what-is-the-difference-between-advanced-threat-analytics-ata-and-product-short"></a>Quelle est la différence entre Advanced Threat Analytics (ATA) et [!INCLUDE [Product short](includes/product-short.md)] ?

ATA est une solution locale autonome avec plusieurs composants, tels que le centre ATA qui nécessite du matériel dédié localement.

[!INCLUDE [Product short](includes/product-short.md)] est une solution de sécurité basée sur le Cloud qui exploite vos signaux de Active Directory (Azure AD) locaux. La solution est très scalable et fréquemment mise à jour.

La version finale d’ATA est mise à la [disposition générale](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9). ATA prendra fin au support standard le 12 janvier 2021. Le support étendu se poursuivra jusqu’au 2026 janvier. Pour plus d’informations, consultez [notre blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181).

Contrairement au capteur ATA, le [!INCLUDE [Product short](includes/product-short.md)] capteur utilise également des sources de données telles que suivi d’v nements pour Windows (ETW) permettant [!INCLUDE [Product short](includes/product-short.md)] de fournir des détections supplémentaires.

[!INCLUDE [Product short](includes/product-short.md)]les mises à jour fréquentes de incluent les fonctionnalités suivantes :

- **Prise en charge [des environnements multiforêts](multi-forest.md)**  : Permet aux organisations d’avoir une visibilité sur les forêts AD.

- **[Évaluations de la posture de sécurité des identités](isp-overview.md)**  : Identifie les configurations incorrectes et les composants exploitables courants, et fournit des voies d’atténuation pour réduire la surface d’attaque.

- **[Fonctions UEBA](/cloud-app-security/tutorial-ueba)**  : Insights sur les risques de chaque utilisateur via le scoring des priorités d’investigation des utilisateurs. Le score peut assister SecOps dans leurs investigations et aider les analystes à comprendre les activités inhabituelles de l’utilisateur et de l’organisation.

- **Intégrations natives**  : Intègre Microsoft Cloud App Security et Azure AD Identity Protection pour fournir une vue hybride de ce qui se produit dans les environnements locaux et hybrides.

- **Contribue à Microsoft 365 Defender** : fournit des données d’alerte et de menace à Microsoft 365 Defender. Microsoft 365 Defender tire parti du portefeuille de sécurité Microsoft 365 (identités, points de terminaison, données et applications) pour analyser automatiquement les données de menace inter-domaines, en créant une image complète de chaque attaque dans un tableau de bord unique. Grâce à cette richesse et à la clarté, les défenseurs peuvent se concentrer sur les menaces critiques et la recherche de failles sophistiquées, en faisant confiance à Microsoft 365 l’automatisation puissante de Defender arrête les attaques n’importe où dans la chaîne de suppression et rétablit l’organisation dans un état sécurisé.

## <a name="licensing-and-privacy"></a>Gestion des licences et confidentialité

### <a name="where-can-i-get-a-license-for-product-long"></a>Où puis-je obtenir une licence [!INCLUDE [Product long](includes/product-long.md)] ?

[!INCLUDE [Product short](includes/product-short.md)] est disponible dans le cadre de Enterprise Mobility + Security 5 suite (EMS E5) et en tant que licence autonome. Vous pouvez acquérir une licence directement sur le [portail Microsoft 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) ou via le modèle de licence de fournisseur de solutions cloud (CSP).

### <a name="does-product-short-need-only-a-single-license-or-does-it-require-a-license-for-every-user-i-want-to-protect"></a>N’a [!INCLUDE [Product short](includes/product-short.md)] -t-il besoin que d’une seule licence ou nécessite-t-elle une licence pour chaque utilisateur que je souhaite protéger ?

Pour plus d’informations sur les [!INCLUDE [Product short](includes/product-short.md)] licences requises, consultez le [ [!INCLUDE [Product short](includes/product-short.md)] Guide des licences](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance#azure-advanced-threat-protection).

### <a name="is-my-data-isolated-from-other-customer-data"></a>Est-ce que mes données sont isolées des données des autres clients ?

Oui, vos données sont isolées par l’authentification de l’accès et la séparation logique basée sur les identificateurs client. Chaque client peut uniquement accéder aux données collectées dans sa propre organisation et aux données génériques fournies par Microsoft.

### <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>Ai-je la possibilité de sélectionner l’emplacement où stocker mes données ?

Non. Lorsque votre [!INCLUDE [Product short](includes/product-short.md)] instance est créée, elle est stockée automatiquement dans le centre de données du pays le plus proche de l’emplacement géographique de votre locataire AAD. [!INCLUDE [Product short](includes/product-short.md)] les données ne peuvent pas être déplacées une fois votre [!INCLUDE [Product short](includes/product-short.md)] instance créée dans un autre centre de données.

### <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Comment est-ce que Microsoft empêche les activités internes malveillantes et les abus de rôles dotés de privilèges élevés ?

Les développeurs et administrateurs Microsoft, par conception, ont reçu des privilèges suffisants pour effectuer les tâches qui leur ont été affectées afin de faire fonctionner et évoluer le service. Microsoft déploie des combinaisons de contrôles préventifs, défensifs et réactifs favorisant la protection contre les activités de développement et/ou d’administration non autorisées, comprenant les mécanismes suivants :

- contrôles d’accès stricts aux données sensibles ;
- combinaisons de contrôles améliorant la détection indépendante des activités malveillantes ;
- niveaux multiples de surveillance, d’enregistrement et de génération de rapports.

En outre, Microsoft effectue des vérifications des antécédents sur certains membres du personnel d’exploitation et limite l’accès aux applications, aux systèmes et à l’infrastructure réseau par rapport au niveau de ces vérifications. Le personnel d’exploitation suit un processus formel quand il doit accéder au compte d’un client ou à des informations associées dans l’exercice de ses fonctions.

## <a name="deployment"></a>Déploiement

### <a name="how-many-product-short-sensors-do-i-need"></a>De combien de [!INCLUDE [Product short](includes/product-short.md)] capteurs ai-je besoin ?

Chaque contrôleur de domaine dans l’environnement doit être couvert par un capteur [!INCLUDE [Product short](includes/product-short.md)] ou un capteur autonome. Pour plus d’informations, consultez [ [!INCLUDE [Product short](includes/product-short.md)] dimensionnement du capteur](capacity-planning.md#sizing).

### <a name="does-product-short-work-with-encrypted-traffic"></a>Fonctionne-t- [!INCLUDE [Product short](includes/product-short.md)] il avec le trafic chiffré ?

Les protocoles réseau avec le trafic chiffré (par exemple AtSvc et WMI) ne sont pas chiffrés, mais ils sont analysés par les capteurs.

### <a name="does-product-short-work-with-kerberos-armoring"></a>Fonctionne-t- [!INCLUDE [Product short](includes/product-short.md)] il avec le blindage Kerberos ?

L’activation du blindage Kerberos, également appelée FAST (flexible Authentication Secure Tunneling), est prise en charge par [!INCLUDE [Product short](includes/product-short.md)] , à l’exception de la détection de hachage excessive, qui ne fonctionne pas avec le blindage Kerberos.

### <a name="how-do-i-monitor-a-virtual-domain-controller-using-product-short"></a>Comment faire surveiller un contrôleur de domaine virtuel à l’aide de [!INCLUDE [Product short](includes/product-short.md)] ?

La plupart des contrôleurs de domaine virtuels peuvent être couverts par le [!INCLUDE [Product short](includes/product-short.md)] capteur, afin de déterminer si le capteur convient à [!INCLUDE [Product short](includes/product-short.md)] votre environnement, consultez [ [!INCLUDE [Product short](includes/product-short.md)] planification](capacity-planning.md)de la capacité.

Si un contrôleur de domaine virtuel ne peut pas être couvert par le [!INCLUDE [Product short](includes/product-short.md)] capteur, vous pouvez disposer d’un capteur autonome virtuel ou physique, [!INCLUDE [Product short](includes/product-short.md)] comme décrit dans [configurer la mise en miroir des ports](configure-port-mirroring.md).  
Le moyen le plus simple consiste à avoir un [!INCLUDE [Product short](includes/product-short.md)] capteur autonome virtuel sur chaque ordinateur hôte où se trouve un contrôleur de domaine virtuel.  
Si vos contrôleurs de domaine virtuels passent d’un hôte à l’autre, vous devez effectuer l’une des étapes suivantes :

- Lorsque le contrôleur de domaine virtuel est déplacé vers un autre hôte, préconfigurez le [!INCLUDE [Product short](includes/product-short.md)] capteur autonome dans cet hôte pour recevoir le trafic à partir du contrôleur de domaine virtuel récemment déplacé.
- Assurez-vous d’affilier le [!INCLUDE [Product short](includes/product-short.md)] capteur autonome virtuel au contrôleur de domaine virtuel, de sorte que, s’il est déplacé, le [!INCLUDE [Product short](includes/product-short.md)] capteur autonome le déplace.
- Certains commutateurs virtuels peuvent envoyer le trafic entre les hôtes.

### <a name="how-do-i-configure-the-product-short-sensors-to-communicate-with-product-short-cloud-service-when-i-have-a-proxy"></a>Comment faire configurer les [!INCLUDE [Product short](includes/product-short.md)] capteurs pour communiquer avec le [!INCLUDE [Product short](includes/product-short.md)] service Cloud lorsque j’ai un proxy ?

Pour que vos contrôleurs de domaine communiquent avec le service cloud, vous devez ouvrir le port 443 dans votre pare-feu/proxy sur *.atp.azure.com. Pour obtenir des instructions sur la procédure à suivre, consultez [configurer votre proxy ou pare-feu pour activer la communication avec les [!INCLUDE [Product short](includes/product-short.md)] capteurs](configure-proxy.md).

### <a name="can-product-short-monitored-domain-controllers-be-virtualized-on-your-iaas-solution"></a>[!INCLUDE [Product short](includes/product-short.md)]Les contrôleurs de domaine peuvent-ils être virtualisés sur votre solution IaaS ?

Oui, vous pouvez utiliser le [!INCLUDE [Product short](includes/product-short.md)] capteur pour surveiller les contrôleurs de domaine qui se trouvent dans n’importe quelle solution IaaS.

### <a name="can-product-short-support-multi-domain-and-multi-forest"></a>Peut [!INCLUDE [Product short](includes/product-short.md)] prendre en charge plusieurs domaines et plusieurs forêts ?

[!INCLUDE [Product short](includes/product-short.md)] prend en charge les environnements à plusieurs domaines et plusieurs forêts. Pour plus d’informations et les exigences de confiance, consultez [Prise en charge de plusieurs forêts](multi-forest.md).

### <a name="can-you-see-the-overall-health-of-the-deployment"></a>Puis-je examiner l’intégrité globale du déploiement ?

Oui, vous pouvez afficher l’intégrité globale du déploiement, ainsi que les problèmes spécifiques liés à la configuration, la connectivité, etc., et vous êtes alerté lorsqu’ils se produisent avec des [!INCLUDE [Product short](includes/product-short.md)] alertes d’intégrité.

## <a name="operation"></a>Opération

### <a name="what-kind-of-integration-does-product-short-have-with-siems"></a>Quel type d’intégration [!INCLUDE [Product short](includes/product-short.md)] avec Siems ?

[!INCLUDE [Product short](includes/product-short.md)] peut être configuré pour envoyer une alerte syslog, à n’importe quel serveur SIEM utilisant le format CEF, pour les alertes d’intégrité et lorsqu’une alerte de sécurité est détectée. Pour plus d’informations, consultez [Informations de référence sur le journal SIEM](cef-format-sa.md).

### <a name="why-are-certain-accounts-considered-sensitive"></a>Pourquoi certains comptes sont-ils considérés comme sensibles ?

Cela arrive quand un compte est membre de groupes désignés comme sensibles (par exemple, « Administrateurs de domaine »).

Pour comprendre pourquoi un compte est sensible, vous pouvez examiner son appartenance au groupe pour déterminer à quels groupes sensibles il appartient. Le groupe auquel il appartient peut également être sensible en raison d’un autre groupe ; dans ce cas, répétez la procédure jusqu’à ce que vous trouviez le groupe sensible de plus haut niveau. Vous pouvez aussi [marquer manuellement des comptes comme étant sensibles](sensitive-accounts.md).

### <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Est-ce que je dois écrire mes propres règles et créer un seuil/une ligne de base ?

Avec [!INCLUDE [Product short](includes/product-short.md)] , il n’est pas nécessaire de créer des règles, des seuils ou des lignes de base, puis de les affiner. [!INCLUDE [Product short](includes/product-short.md)] analyse les comportements des utilisateurs, des appareils et des ressources, ainsi que leurs relations entre eux, et peut détecter rapidement les activités suspectes et les attaques connues. Trois semaines après le déploiement, [!INCLUDE [Product short](includes/product-short.md)] commence à détecter les activités suspectes comportementales. En revanche, [!INCLUDE [Product short](includes/product-short.md)] va commencer à détecter les attaques malveillantes connues et les problèmes de sécurité immédiatement après le déploiement.

### <a name="which-traffic-does-product-short-generate-in-the-network-from-domain-controllers-and-why"></a>Quel trafic génère-t- [!INCLUDE [Product short](includes/product-short.md)] il dans le réseau à partir de contrôleurs de domaine et pourquoi ?

[!INCLUDE [Product short](includes/product-short.md)] génère le trafic des contrôleurs de domaine vers les ordinateurs de l’organisation dans l’un des trois scénarios suivants :

1. **Résolution de nom réseau**  
[!INCLUDE [Product short](includes/product-short.md)] capture le trafic et les événements, l’apprentissage et le profilage des utilisateurs et des activités informatiques sur le réseau. Pour apprendre et profiler les activités conformément aux ordinateurs de l’organisation, [!INCLUDE [Product short](includes/product-short.md)] doit résoudre les adresses IP en comptes d’ordinateur. Pour résoudre les adresses IP en capteurs de noms d’ordinateur [!INCLUDE [Product short](includes/product-short.md)] , demandez l’adresse IP du nom de l’ordinateur *derrière* l’adresse IP.

    Les requêtes sont effectuées à l’aide d’une des quatre méthodes :
    - NTLM sur RPC (port TCP 135)
    - NetBIOS (port UDP 137)
    - RDP (port TCP 3389)
    - Interroger le serveur DNS à l’aide de la recherche DNS inversée de l’adresse IP (UDP 53)

    Après avoir obtenu le nom de l’ordinateur,  [!INCLUDE [Product short](includes/product-short.md)] les capteurs vérifient les détails dans Active Directory pour voir s’il existe un objet ordinateur corrélé portant le même nom d’ordinateur. Si une correspondance est trouvée, une association est établie entre l’adresse IP et l’objet ordinateur correspondant.
2. **Chemin de mouvement latéral (LMP)**  
Pour créer des LMPs potentiels pour les utilisateurs sensibles, vous [!INCLUDE [Product short](includes/product-short.md)] devez disposer d’informations sur les administrateurs locaux sur les ordinateurs. Dans ce scénario, le [!INCLUDE [Product short](includes/product-short.md)] capteur utilise Sam-R (TCP 445) pour interroger l’adresse IP identifiée dans le trafic réseau afin de déterminer les administrateurs locaux de l’ordinateur. Pour en savoir plus sur [!INCLUDE [Product short](includes/product-short.md)] et Sam-r, consultez [configurer les autorisations requises Sam-r](install-step8-samr.md).

3. **Interrogation d’Active Directory à l’aide de LDAP** pour les données d’entité  
[!INCLUDE [Product short](includes/product-short.md)] les capteurs interrogent le contrôleur de domaine à partir du domaine auquel appartient l’entité. Il peut s’agir du même capteur ou d’un autre contrôleur de domaine de ce domaine.

|Protocole|Service|Port|Source| Sens|
|---------|---------|---------|---------|--------|
|LDAP|TCP et UDP|389|Contrôleurs de domaine|Sortant|
|LDAP sécurisé (LDAPS)|TCP|636|Contrôleurs de domaine|Sortant|
|LDAP vers le catalogue global|TCP|3268|Contrôleurs de domaine|Sortant|
|LDAPS vers le catalogue global|TCP|3269|Contrôleurs de domaine|Sortant|

### <a name="why-dont-activities-always-show-both-the-source-user-and-computer"></a>Pourquoi les activités n’affichent-elles pas toujours l’utilisateur source et l’ordinateur source ?

[!INCLUDE [Product short](includes/product-short.md)] capture des activités sur de nombreux protocoles différents. Dans certains cas, [!INCLUDE [Product short](includes/product-short.md)] ne reçoit pas les données de l’utilisateur source dans le trafic. [!INCLUDE [Product short](includes/product-short.md)] tente de mettre en corrélation la session de l’utilisateur avec l’activité et, lorsque la tentative est réussie, l’utilisateur source de l’activité s’affiche. Lorsque la tentative de corrélation de l’utilisateur échoue, seul l’ordinateur source s’affiche.

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="what-should-i-do-if-the-product-short-sensor-or-standalone-sensor-doesnt-start"></a>Que dois-je faire si le capteur [!INCLUDE [Product short](includes/product-short.md)] ou le capteur autonome ne démarre pas ?

Examinez l’erreur la plus récente dans le [Journal](troubleshooting-using-logs.md) des erreurs actuel (où [!INCLUDE [Product short](includes/product-short.md)] est installé dans le dossier « logs »).

## <a name="see-also"></a>Voir aussi

- [[!INCLUDE [Product short](includes/product-short.md)] conditions préalables](prerequisites.md)
- [[!INCLUDE [Product short](includes/product-short.md)] planification de la capacité](capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Résolution des problèmes](troubleshooting-known-issues.md)
- [Consultez le [!INCLUDE [Product short](includes/product-short.md)] Forum !](https://aka.ms/MDIcommunity)
