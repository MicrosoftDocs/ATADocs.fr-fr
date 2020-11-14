---
title: Prérequis de Microsoft Defender pour Identity
description: Décrit les conditions requises pour réussir le déploiement de Microsoft Defender pour Identity dans votre environnement
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e3b5b67ad5330fd7be41ed63e6db105e2f1d4a9e
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275637"
---
# <a name="product-long-prerequisites"></a>Prérequis de [!INCLUDE [Product long](includes/product-long.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Cet article décrit les conditions requises pour réussir le déploiement de [!INCLUDE [Product long](includes/product-long.md)] dans votre environnement.

>[!NOTE]
> Pour plus d’informations sur la façon de planifier les ressources et la capacité, consultez [Planification de la capacité [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md).

[!INCLUDE [Product short](includes/product-short.md)] se compose du service cloud [!INCLUDE [Product short](includes/product-short.md)], qui est constitué du portail [!INCLUDE [Product short](includes/product-short.md)]et du capteur [!INCLUDE [Product short](includes/product-short.md)]. Pour plus d’informations sur chaque composant de [!INCLUDE [Product short](includes/product-short.md)], consultez [Architecture de [!INCLUDE [Product short](includes/product-short.md)]](architecture.md).

[!INCLUDE [Product short](includes/product-short.md)] protège vos utilisateurs Active Directory locaux et/ou utilisateurs synchronisés avec Azure Active Directory. Pour protéger un environnement composé uniquement d’utilisateurs AAD, consultez [Protection d’identité AAD](/azure/active-directory/identity-protection/overview).

Pour créer votre instance de [!INCLUDE [Product short](includes/product-short.md)], vous avez besoin d’un locataire AAD avec au moins un administrateur général/de sécurité. Chaque instance [!INCLUDE [Product short](includes/product-short.md)] prend en charge une limite de forêt Active Directory multiple et le niveau fonctionnel de forêt (FFL) Windows 2003 et versions ultérieures.

Ce guide des prérequis comprend les sections suivantes qui vous permettent de vérifier que vous avez tout ce qu’il faut pour déployer [!INCLUDE [Product short](includes/product-short.md)].

[Avant de commencer](#before-you-start) : Liste les informations à rassembler ainsi que les comptes et les entités réseau dont vous devez disposer avant de commencer l’installation.

[Portail [!INCLUDE [Product short](includes/product-short.md)]](#azure-atp-portal-requirements) : Décrit les exigences pour le navigateur du portail [!INCLUDE [Product short](includes/product-short.md)].

[Capteur [!INCLUDE [Product short](includes/product-short.md)]](#azure-atp-sensor-requirements) : Liste le matériel du capteur [!INCLUDE [Product short](includes/product-short.md)] ainsi que la configuration logicielle requise.

[Capteur autonome [!INCLUDE [Product short](includes/product-short.md)]](#azure-atp-standalone-sensor-requirements) : Le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] est installé sur un serveur dédié et nécessite la configuration de mise en miroir des ports sur le contrôleur de domaine pour recevoir le trafic réseau.

> [!NOTE]
> Les capteurs autonomes [!INCLUDE [Product short](includes/product-short.md)] ne prennent pas en charge la collecte d’entrées de journal du Suivi d’événements pour Windows (ETW) qui fournissent les données pour de nombreuses détections. Pour une couverture complète de votre environnement, nous vous recommandons de déployer le capteur [!INCLUDE [Product short](includes/product-short.md)].

## <a name="before-you-start"></a>Avant de commencer

Cette section liste les informations que vous devez rassembler ainsi que les comptes et les informations d’entité réseau dont vous devez disposer avant de procéder à l’installation de [!INCLUDE [Product short](includes/product-short.md)].

- Vous pouvez acquérir une licence pour EMS E5 (Enterprise Mobility + Security 5) directement via le [portail Microsoft 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) ou utiliser le modèle de licence CSP (Cloud Solution Partner). Des licences [!INCLUDE [Product short](includes/product-short.md)] autonomes sont également disponibles.

- Vérifiez que le ou les contrôleurs de domaine sur lesquels vous prévoyez d’installer des capteurs [!INCLUDE [Product short](includes/product-short.md)] ont une connectivité Internet au service cloud [!INCLUDE [Product short](includes/product-short.md)]. Le capteur [!INCLUDE [Product short](includes/product-short.md)] prend en charge l’utilisation d’un proxy. Pour plus d’informations sur la configuration du proxy, consultez [Configuration d’un proxy pour [!INCLUDE [Product short](includes/product-short.md)]](configure-proxy.md).

- Au moins l’un des comptes de services d’annuaire suivants, avec accès en lecture à tous les objets dans les domaines analysés :
  - Un mot de passe et un compte d’utilisateur AD **standard**. Requis pour les capteurs exécutant Windows Server 2008 R2 SP1.
  - Un **compte de service administré du groupe** (gMSA). Requiert Windows Server 2012 ou version ultérieure.  
  Tous les capteurs doivent disposer des autorisations pour récupérer le mot de passe du compte gMSA.  
  Pour en savoir plus sur les comptes gMSA, consultez [Prise en main des comptes de service administré de groupe](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts#BKMK_CreateGMSA).

    Le tableau suivant indique les comptes d’utilisateurs AD qui peuvent être utilisés avec les versions de serveur suivantes :

    |Type de compte|Windows Server 2008 R2 SP1|Windows Server 2012 ou version ultérieure|
    |---|---|---|
    |Compte d’utilisateur AD **standard**|Oui|Oui|
    |Compte **gMSA**|Non|Oui|

    > [!NOTE]
    >
    > - Pour les ordinateurs du capteur exécutant Windows Server 2012 et versions ultérieures, nous vous recommandons d’utiliser un compte **gMSA** pour améliorer la sécurité et la gestion automatique des mots de passe.
    > - Si vous avez plusieurs capteurs, certains exécutant Windows Server 2008 et d’autres qui exécutent Windows Server 2012 ou version ultérieure, en plus de la recommandation d’utiliser un compte **gMSA** , vous devez également utiliser au moins un compte d’utilisateur AD **standard**.
    > - Si vous avez défini des listes de contrôle d’accès (ACL) personnalisées sur différentes unités d’organisation dans votre domaine, vérifiez que l’utilisateur sélectionné dispose d’autorisations d’accès en lecture à ces unités d’organisation.

- Si vous exécutez Wireshark sur le capteur autonome [!INCLUDE [Product short](includes/product-short.md)], redémarrez le service de capteur [!INCLUDE [Product short](includes/product-short.md)] après avoir arrêté la capture Wireshark. Si vous ne redémarrez pas le service de capteur, le capteur arrête la capture du trafic.

- Si vous essayez d’installer le capteur [!INCLUDE [Product short](includes/product-short.md)] sur un ordinateur configuré avec une carte d’association de cartes réseau, vous recevrez une erreur d’installation. Si vous souhaitez installer le capteur [!INCLUDE [Product short](includes/product-short.md)] sur un ordinateur configuré avec une association de cartes réseau, consultez [Problème d’association de cartes réseau du capteur [!INCLUDE [Product short](includes/product-short.md)]](troubleshooting-known-issues.md#nic-teaming).

- Recommandation relative au conteneur **Objets supprimés**  : L’utilisateur doit disposer d’autorisations en lecture seule sur le conteneur Objets supprimés. Des autorisations en lecture seule sur ce conteneur permettent à [!INCLUDE [Product short](includes/product-short.md)] de détecter les suppressions d’utilisateurs dans votre annuaire Active Directory. Pour plus d’informations sur la configuration des autorisations en lecture seule sur le conteneur Objets supprimés, consultez la section **Modification des autorisations sur un conteneur d’objets supprimés** de l’article [Afficher ou définir des autorisations sur un objet annuaire](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824(v=ws.10)).

- **Honeytoken** facultatif : Compte d’un utilisateur sans activité réseau. Ce compte est configuré comme utilisateur honeytoken [!INCLUDE [Product short](includes/product-short.md)]. Pour plus d’informations sur l’utilisation des honeytokens, consultez [Configurer des exclusions et un utilisateur honeytoken](install-step7.md).

- Facultatif : Quand vous déployez le capteur autonome, vous devez transférer les [événements Windows](configure-windows-event-collection.md#configure-event-collection) à [!INCLUDE [Product short](includes/product-short.md)] pour continuer à améliorer les détections basées sur l’authentification [!INCLUDE [Product short](includes/product-short.md)], les ajouts aux groupes sensibles et les détections de création de services suspects.  Le capteur [!INCLUDE [Product short](includes/product-short.md)] reçoit automatiquement ces événements. Dans le capteur autonome [!INCLUDE [Product short](includes/product-short.md)], vous pouvez recevoir ces événements de votre serveur SIEM ou en définissant les transferts d’événements Windows à partir de votre contrôleur de domaine. Les événements collectés fournissent à [!INCLUDE [Product short](includes/product-short.md)] des informations supplémentaires qui ne sont pas accessibles par le biais du trafic réseau du contrôleur de domaine.

<a name="azure-atp-portal-requirements"></a>

## <a name="product-short-portal-requirements"></a>Exigences pour le portail [!INCLUDE [Product short](includes/product-short.md)]

L’accès au portail [!INCLUDE [Product short](includes/product-short.md)] s’effectue via un navigateur. Les navigateurs et paramètres suivants sont pris en charge :

- Un navigateur qui prend en charge TLS 1.2, par exemple :
  - Microsoft Edge
  - Internet Explorer 11 et versions ultérieures
  - Google Chrome 30.0 et versions ultérieures
- Largeur d’écran d’une résolution minimale de 1 700 pixels
- Pare-feu/proxy ouvert : pour communiquer avec le service cloud [!INCLUDE [Product short](includes/product-short.md)], vous devez ouvrir le port 443 dans votre pare-feu/proxy sur *.atp.azure.com.

    > [!NOTE]
    > Vous pouvez également utiliser notre étiquette de service Azure ( **AzureAdvancedThreatProtection** ) pour activer l’accès à [!INCLUDE [Product short](includes/product-short.md)]. Pour plus d’informations sur les balises de service, consultez les fichiers sur les [balises de service de réseau virtuel](/azure/virtual-network/service-tags-overview) ou sur le [téléchargement des balises de service](https://www.microsoft.com/download/details.aspx?id=56519).

 ![Diagramme de l’architecture [!INCLUDE [Product short](includes/product-short.md)]](media/architecture-topology.png)

> [!NOTE]
> Par défaut, [!INCLUDE [Product short](includes/product-short.md)] prend en charge jusqu’à 200 capteurs. Si vous voulez installer plus de capteurs, contactez le support [!INCLUDE [Product short](includes/product-short.md)].

## <a name="product-short-network-name-resolution-nnr-requirements"></a>Exigences pour [!INCLUDE [Product short](includes/product-short.md)] NNR (Network Name Resolution, résolution de noms réseau)

La résolution de noms réseau (NNR) est l’un des principaux composants de la fonctionnalité [!INCLUDE [Product short](includes/product-short.md)]. Pour résoudre les adresses IP en noms d’ordinateur, les capteurs [!INCLUDE [Product short](includes/product-short.md)] recherchent les adresses IP à l’aide des méthodes suivantes :

- NTLM sur RPC (port TCP 135)
- NetBIOS (port UDP 137)
- RDP (port TCP 3389), seulement le premier paquet de **Client hello**
- Interroge le serveur DNS par recherche DNS inversée de l’adresse IP (UDP 53)

Pour que les trois premières méthodes fonctionnent, les ports appropriés doivent être ouverts en entrée depuis les capteurs [!INCLUDE [Product short](includes/product-short.md)] vers les appareils du réseau. Pour en savoir plus sur [!INCLUDE [Product short](includes/product-short.md)] et NNR, consultez [Stratégie [!INCLUDE [Product short](includes/product-short.md)] NNR](nnr-policy.md).

Pour obtenir les meilleurs résultats, nous vous recommandons d’utiliser toutes les méthodes. Si ce n’est pas possible, vous devez utiliser la méthode de recherche DNS et au moins l’une des autres méthodes.

<a name="azure-atp-sensor-requirements"></a>

## <a name="product-short-sensor-requirements"></a>Exigences pour le capteur [!INCLUDE [Product short](includes/product-short.md)]

Cette section décrit les exigences pour le capteur [!INCLUDE [Product short](includes/product-short.md)].

### <a name="general"></a>Général

Le capteur [!INCLUDE [Product short](includes/product-short.md)] prend en charge l’installation sur un contrôleur de domaine sous Windows Server 2008 R2 SP1 (Server Core non inclus), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (Windows Server Core inclus mais pas Windows Nano Server), Windows Server 2019\* (Server Core inclus mais pas Nano Server), comme indiqué dans le tableau suivant.

| Version du système d'exploitation   | Server avec Expérience utilisateur | Server Core | Nano Server    |
| -------------------------- | ------------------------------ | ----------- | -------------- |
| Windows Server 2008 R2 SP1 | &#10004;                       | &#10060;    | Non applicable |
| Windows Server 2012        | &#10004;                       | &#10004;    | Non applicable |
| Windows Server 2012 R2     | &#10004;                       | &#10004;    | Non applicable |
| Windows Server 2016        | &#10004;                       | &#10004;    | &#10060;       |
| Windows Server 2019\*      | &#10004;                       | &#10004;    | &#10060;       |

\* Nécessite [KB4487044](https://support.microsoft.com/help/4487044/windows-10-update-kb4487044). Les capteurs installés sur Server 2019 sans cette mise à jour seront automatiquement arrêtés.

Le contrôleur de domaine peut être un contrôleur de domaine en lecture seule (RODC).

Pour que vos contrôleurs de domaine communiquent avec le service cloud, vous devez ouvrir le port 443 dans vos pare-feu et proxies sur \*.atp.azure.com.

Pendant l’installation, si .NET Framework 4.7 (ou version ultérieure) n’est pas installé, celui-ci est installé automatiquement et peut nécessiter un redémarrage du contrôleur de domaine. Cette étape peut également être requise si un redémarrage est déjà en attente.

> [!NOTE]
> Un minimum de 5 Go d’espace disque sont nécessaires et 10 Go sont recommandés. Cela inclut l’espace nécessaire pour les fichiers binaires [!INCLUDE [Product short](includes/product-short.md)], les journaux [!INCLUDE [Product short](includes/product-short.md)] et les journaux de performances.

### <a name="server-specifications"></a>Spécifications du serveur

Le capteur [!INCLUDE [Product short](includes/product-short.md)] nécessite au minimum deux cœurs et 6 Go de RAM sur le contrôleur de domaine.
Pour bénéficier de performances optimales, choisissez **Hautes performances** comme **Option d’alimentation** de la machine exécutant le capteur [!INCLUDE [Product short](includes/product-short.md)].

Vous pouvez déployer les capteurs [!INCLUDE [Product short](includes/product-short.md)] sur des contrôleurs de domaine de différentes charges et tailles, en fonction de la quantité de trafic réseau vers et depuis les contrôleurs de domaine et de la quantité de ressources installées.

Pour les systèmes d’exploitation Windows 2008R2 et 2012, le capteur [!INCLUDE [Product short](includes/product-short.md)] n’est pas pris en charge en mode [Groupe multiprocesseur](/windows/win32/procthread/processor-groups). Pour plus d’informations sur le mode Groupe multiprocesseur, consultez la [résolution des problèmes](troubleshooting-known-issues.md#multi-processor-group-mode).

>[!NOTE]
> En cas d’exécution en tant que machine virtuelle, la mémoire dynamique ou toute autre fonctionnalité d’augmentation de la mémoire n’est pas prise en charge.

Pour plus d’informations sur la configuration matérielle requise pour le capteur [!INCLUDE [Product short](includes/product-short.md)], consultez [Planification de la capacité [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md).

### <a name="time-synchronization"></a>Synchronisation de l’heure

L’heure des serveurs et contrôleurs de domaine sur lesquels le capteur est installé doit être synchronisée pour que tout écart entre eux ne dépasse pas cinq minutes.

### <a name="network-adapters"></a>Cartes réseau

Le capteur [!INCLUDE [Product short](includes/product-short.md)] supervise le trafic local sur toutes les cartes réseau du contrôleur de domaine.  
Après le déploiement, utilisez le portail [!INCLUDE [Product short](includes/product-short.md)] pour changer les cartes réseau qui font l’objet d’une supervision.

Le capteur n’est pas pris en charge sur les contrôleurs de domaine exécutant Windows 2008 R2 avec l’association de carte réseau Broadcom activée.

### <a name="ports"></a>Ports

Le tableau suivant liste les ports qui, au minimum, sont requis par le capteur [!INCLUDE [Product short](includes/product-short.md)] :

|Protocole|Transport|Port|Du|À|
|------------|-------------|--------|-----------|
|**Ports Internet**|||||
|SSL (*.atp.azure.com)|TCP|443|Capteur [!INCLUDE [Product short](includes/product-short.md)]|Service cloud [!INCLUDE [Product short](includes/product-short.md)]|
|SSL (localhost)|TCP|444|Capteur [!INCLUDE [Product short](includes/product-short.md)]|localhost|
|**Ports internes**|||||
|DNS|TCP et UDP|53|Capteur [!INCLUDE [Product short](includes/product-short.md)]|Serveurs DNS|
|Netlogon (SMB, CIFS, SAM-R)|TCP/UDP|445|Capteur [!INCLUDE [Product short](includes/product-short.md)]|Tous les appareils sur le réseau|
|RADIUS|UDP|1813|RADIUS|Capteur [!INCLUDE [Product short](includes/product-short.md)]|
|**Ports NNR**\*|||||
|NTLM sur RPC|TCP|Port 135|[!INCLUDE [Product short](includes/product-short.md)]s|Tous les appareils sur le réseau|
|NetBIOS|UDP|137|[!INCLUDE [Product short](includes/product-short.md)]s|Tous les appareils sur le réseau|
|RDP|TCP|3389, seulement le premier paquet de Client hello|[!INCLUDE [Product short](includes/product-short.md)]s|Tous les appareils sur le réseau|

\* Un de ces ports est obligatoire, mais nous vous recommandons de les ouvrir tous.

### <a name="windows-event-logs"></a>Journaux d'événements Windows

La détection [!INCLUDE [Product short](includes/product-short.md)] s’appuie sur des [journaux d’événements Windows](configure-windows-event-collection.md#configure-event-collection) spécifiques que le capteur analyse à partir de vos contrôleurs de domaine. Pour auditer les bons événements et les inclure dans le journal des événements Windows, la stratégie d’audit avancée de vos contrôleurs de domaine doit être correctement configurée. Pour plus d’informations sur la configuration des stratégies appropriées, consultez [Stratégie d'audit avancée](configure-windows-event-collection.md). Pour [vous assurer que l’événement Windows 8004 est audité](configure-windows-event-collection.md#configure-audit-policies) en fonction des besoins du service, vérifiez vos [paramètres d’audit NTLM](/archive/blogs/askds/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7).

> [!NOTE]
> À l’aide du compte d’utilisateur du service d’annuaire, le capteur interroge les points de terminaison de votre organisation à la recherche des administrateurs locaux en utilisant SAM-R (ouverture de session réseau) pour générer le [graphe des chemins de mouvement latéral](use-case-lateral-movement-path.md). Pour plus d’informations, consultez [Configurer les autorisations requises SAM-R](install-step8-samr.md).

<a name="azure-atp-standalone-sensor-requirements"></a>

## <a name="product-short-standalone-sensor-requirements"></a>Conditions requises pour le capteur autonome [!INCLUDE [Product short](includes/product-short.md)]

Cette section décrit les conditions requises pour le capteur autonome [!INCLUDE [Product short](includes/product-short.md)].

> [!NOTE]
> Les capteurs autonomes [!INCLUDE [Product short](includes/product-short.md)] ne prennent pas en charge la collecte d’entrées de journal du Suivi d’événements pour Windows (ETW) qui fournissent les données pour de nombreuses détections. Pour une couverture complète de votre environnement, nous vous recommandons de déployer le capteur [!INCLUDE [Product short](includes/product-short.md)].

### <a name="general"></a>Général

L’installation du capteur autonome [!INCLUDE [Product short](includes/product-short.md)] sur un serveur Windows Server 2012 R2 ou Windows Server 2016 (dont Server Core) est prise en charge.
Le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] peut être installé sur un serveur membre d’un domaine ou d’un groupe de travail.
Le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] peut servir à superviser les contrôleurs de domaine avec le niveau fonctionnel de domaine Windows 2003 et versions ultérieures.

Pour que votre capteur autonome communique avec le service cloud, vous devez ouvrir le port 443 dans vos pare-feux et proxies sur *.atp.azure.com.

Pour plus d’informations sur l’utilisation de machines virtuelles avec le capteur autonome [!INCLUDE [Product short](includes/product-short.md)], consultez [Configurer la mise en miroir des ports](configure-port-mirroring.md).

> [!NOTE]
> Un minimum de 5 Go d’espace disque sont nécessaires et 10 Go sont recommandés. Cela inclut l’espace nécessaire pour les fichiers binaires [!INCLUDE [Product short](includes/product-short.md)], les journaux [!INCLUDE [Product short](includes/product-short.md)] et les journaux de performances.

### <a name="server-specifications"></a>Spécifications du serveur

Pour des performances optimales, choisissez **Hautes performances** comme **Option d’alimentation** de la machine exécutant le capteur autonome [!INCLUDE [Product short](includes/product-short.md)].

Les capteurs autonomes [!INCLUDE [Product short](includes/product-short.md)] peuvent prendre en charge la supervision de plusieurs contrôleurs de domaine, en fonction du volume du trafic réseau à destination et en provenance des contrôleurs de domaine.

>[!NOTE]
> En cas d’exécution en tant que machine virtuelle, la mémoire dynamique ou toute autre fonctionnalité d’augmentation de la mémoire n’est pas prise en charge.

Pour plus d’informations sur la configuration matérielle requise pour le capteur autonome [!INCLUDE [Product short](includes/product-short.md)], consultez [Planification de la capacité [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md).

### <a name="time-synchronization"></a>Synchronisation de l’heure

L’heure des serveurs et contrôleurs de domaine sur lesquels le capteur est installé doit être synchronisée pour que tout écart entre eux ne dépasse pas cinq minutes.

### <a name="network-adapters"></a>Cartes réseau

Le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] nécessite au moins une carte de gestion et au moins une carte de capture :

- **Carte de gestion**  : cette carte est utilisée pour les communications sur votre réseau d’entreprise. Le capteur utilise cette carte pour interroger le contrôleur de domaine qu’il protège et procéder à la résolution des comptes d’ordinateur.

    Elle doit être configurée avec les paramètres suivants :

    - Adresse IP statique (passerelle par défaut incluse)

    - Serveurs DNS préféré et auxiliaire

    - Le **Suffixe DNS pour cette connexion** doit être le nom DNS du domaine pour chaque domaine surveillé.

        ![Configurer le suffixe DNS dans les paramètres TCP/IP avancés](media/dns-suffix.png)

        > [!NOTE]
        > Si le capteur autonome [!INCLUDE [Product short](includes/product-short.md)] est membre du domaine, le suffixe peut être configuré automatiquement.

- **Carte de capture**  : cette carte est utilisée pour capturer le trafic à destination et en provenance des contrôleurs de domaine.

    > [!IMPORTANT]
    >
    > - Configurez la mise en miroir des ports de la carte de capture comme la destination du trafic réseau des contrôleurs de domaine. Pour plus d’informations, consultez [Configurer la mise en miroir des ports](configure-port-mirroring.md). En règle générale, vous devez collaborer avec l’équipe de virtualisation ou de mise en réseau pour configurer la mise en miroir des ports.
    > - Configurez une adresse IP statique non routable (avec masque /32) pour votre environnement, sans passerelle de capteur par défaut ni adresse de serveur DNS, par exemple, 10.10.0.10/32. Cela permet de garantir que la carte réseau de capture peut capturer le volume maximum de trafic et que la carte réseau de gestion est utilisée pour envoyer et recevoir le trafic réseau demandé.

### <a name="ports"></a>Ports

Le tableau suivant liste les ports qui, au minimum, doivent être configurés sur la carte de gestion pour répondre aux conditions requises du capteur autonome [!INCLUDE [Product short](includes/product-short.md)] :

|Protocole|Transport|Port|Du|À|
|------------|-------------|--------|-----------|
|**Ports Internet**||||
|SSL (*.atp.azure.com)|TCP|443|Capteur [!INCLUDE [Product short](includes/product-short.md)]|Service cloud [!INCLUDE [Product short](includes/product-short.md)]|
|SSL (localhost)|TCP|444|Capteur [!INCLUDE [Product short](includes/product-short.md)]|localhost|
|**Ports internes**||||
|LDAP|TCP et UDP|389|Capteur [!INCLUDE [Product short](includes/product-short.md)]|Contrôleurs de domaine|
|LDAP sécurisé (LDAPS)|TCP|636|Capteur [!INCLUDE [Product short](includes/product-short.md)]|Contrôleurs de domaine|
|LDAP vers le catalogue global|TCP|3268|Capteur [!INCLUDE [Product short](includes/product-short.md)]|Contrôleurs de domaine|
|LDAPS vers le catalogue global|TCP|3269|Capteur [!INCLUDE [Product short](includes/product-short.md)]|Contrôleurs de domaine|
|Kerberos|TCP et UDP|88|Capteur [!INCLUDE [Product short](includes/product-short.md)]|Contrôleurs de domaine|
|Netlogon (SMB, CIFS, SAM-R)|TCP et UDP|445|Capteur [!INCLUDE [Product short](includes/product-short.md)]|Tous les appareils sur le réseau|
|Horloge Windows|UDP|123|Capteur [!INCLUDE [Product short](includes/product-short.md)]|Contrôleurs de domaine|
|DNS|TCP et UDP|53|Capteur [!INCLUDE [Product short](includes/product-short.md)]|Serveurs DNS|
|Syslog (facultatif)|TCP/UDP|514, selon la configuration|Serveur SIEM|Capteur [!INCLUDE [Product short](includes/product-short.md)]|
|RADIUS|UDP|1813|RADIUS|Capteur [!INCLUDE [Product short](includes/product-short.md)]|
|**Ports NNR** \*|||||
|NTLM sur RPC|TCP|135|[!INCLUDE [Product short](includes/product-short.md)]s|Tous les appareils sur le réseau|
|NetBIOS|UDP|137|[!INCLUDE [Product short](includes/product-short.md)]s|Tous les appareils sur le réseau|
|RDP|TCP|3389, seulement le premier paquet de Client hello|[!INCLUDE [Product short](includes/product-short.md)]s|Tous les appareils sur le réseau|

\* Un de ces ports est obligatoire, mais nous vous recommandons de les ouvrir tous.

> [!NOTE]
>
> - À l’aide du compte d’utilisateur du service d’annuaire, le capteur interroge les points de terminaison de votre organisation à la recherche des administrateurs locaux en utilisant SAM-R (ouverture de session réseau) pour générer le [graphe des chemins de mouvement latéral](use-case-lateral-movement-path.md). Pour plus d’informations, consultez [Configurer les autorisations requises SAM-R](install-step8-samr.md).

## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/aatpsizingtool)
- [Architecture [!INCLUDE [Product short](includes/product-short.md)]](architecture.md)
- [Installer [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Résolution de nom réseau (NNR)](nnr-policy.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
