---
title: Nouveautés d’Azure ATP (Azure Advanced Threat Protection)
description: Cet article est mis à jour fréquemment pour vous informer des nouveautés de la dernière version d’Azure ATP (Azure Advanced Threat Protection).
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: d70da8a6ae853c2b4f72ffb47286b22e163f336d
ms.sourcegitcommit: 9f1a94cdd3abfa9e4921d9534e9b4add5e692592
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87800226"
---
# <a name="whats-new-in-azure-advanced-threat-protection-azure-atp"></a>Nouveautés d’Azure ATP (Azure Advanced Threat Protection)

Cet article est fréquemment mis à jour pour vous informer des nouveautés des dernières versions d’Azure ATP.

Pour plus d’informations sur les versions antérieures d’Azure ATP jusqu’à la version 2.55 (comprise), voir la [Référence sur les versions d’Azure ATP](atp-release-reference.md).

Flux RSS : Recevez une notification quand cette page est mise à jour en copiant et collant l’URL suivante dans votre lecteur de flux : `https://docs.microsoft.com/api/search/rss?search=%22This+article+is+updated+frequently+to+let+you+know+what%27s+new+in+the+latest+release+of+Azure+ATP%22&locale=en-us`

## <a name="azure-atp-release-2121"></a>Azure ATP version 2.121

Publication : 2 août 2020

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2120"></a>Azure ATP version 2.120

Publication le 26 juillet 2020

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2119"></a>Azure ATP version 2.119

Publication : 5 juillet 2020

- **Amélioration de fonctionnalité : Nouvel onglet *Contrôleurs de domaine exclus* dans le rapport Excel**  
Pour améliorer la justesse de notre calcul de couverture de contrôleur de domaine, nous allons exclure les contrôleurs de domaine ayant des approbations externes du calcul visant à atteindre 100 % de couverture. Les contrôleurs de domaine exclus apparaîtront sous le nouvel onglet *Contrôleurs de domaine exclus* dans le téléchargement du rapport Excel de couverture de domaine. Pour plus d’informations sur le téléchargement du rapport, consultez [État des contrôleurs de domaine](atp-sensor-monitoring.md#domain-controller-status).
- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2118"></a>Azure ATP version 2.118

Publication : 28 juin 2020

- **Nouvelles évaluations de sécurité**  
Les évaluations de sécurité Azure ATP incluent désormais les nouvelles évaluations suivantes :
  - **Chemins de mouvement latéral les plus risqués**  
    Cette évaluation supervise en permanence votre environnement pour identifier les comptes **sensibles** dont les chemins de mouvement latéral sont les plus risqués du point de vue de la sécurité. Vous en êtes informé à travers des rapports qui vous aident à gérer votre environnement. Les chemins sont considérés à risque s’ils comptent au moins trois comptes non sensibles susceptibles d’exposer le compte sensible à une subtilisation d’informations d’identification par des acteurs malveillants. Pour plus d’informations, consultez [Évaluation de la sécurité : Chemins de mouvement latéral les plus risqués](atp-cas-isp-riskiest-lmp.md).
  - **Attributs de compte non sécurisé**  
    Cette évaluation Azure ATP supervise en permanence votre environnement pour identifier les comptes dont les valeurs d’attributs présentent un risque de sécurité. Vous en êtes informé à travers des rapports qui vous aident à protéger votre environnement. Pour plus d’informations, consultez [Évaluation de la sécurité : Attributs de compte non sécurisé](atp-cas-isp-unsecure-account-attributes.md).

- **Mise à jour de la définition de confidentialité**  
Nous étendons notre définition de confidentialité aux comptes locaux pour inclure les entités qui sont autorisées à utiliser la réplication Active Directory.

## <a name="azure-atp-release-2117"></a>Azure ATP version 2.117

Publication : 14 juin 2020

- **Amélioration de fonctionnalité : Détails supplémentaires sur les activités qui sont disponibles dans l’expérience unifiée SecOps**  
Nous avons enrichi les informations d’appareil que nous envoyons à Cloud App Security, notamment les noms d’appareil, les adresses IP, les UPN de compte et les ports utilisés. Pour plus d’informations sur l’intégration à Cloud App Security, consultez [Utilisation d’Azure ATP avec Cloud App Security](atp-mcas-integration.md).

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2116"></a>Azure ATP version 2.116

Publication : 7 juin 2020

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2115"></a>Azure ATP version 2.115

Publication : 31 mai 2020

- **Nouvelles évaluations de sécurité**  
Les évaluations de sécurité Azure ATP incluent désormais les nouvelles évaluations suivantes :
  - **Attributs d’historique SID non sécurisés**  
    Cette évaluation fournit des rapports sur les attributs d’historique SID qui peuvent être utilisés par des personnes malveillantes pour accéder à votre environnement. Pour plus d’informations, consultez [Évaluation de la sécurité : Attributs d’historique SID non sécurisés](atp-cas-isp-unsecure-sid-history-attribute.md).
  - **Utilisation de Microsoft LAPS**  
    Cette évaluation permet de connaître les comptes d’administrateur locaux qui n’utilisent pas la solution LAPS pour sécuriser leur mot de passe. L’utilisation de LAPS simplifie la gestion des mots de passe et contribue également à la défense contre les cyberattaques. Pour plus d’informations, consultez [Évaluation de la sécurité : Utilisation de Microsoft LAPS](atp-cas-isp-laps.md).

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2114"></a>Azure ATP version 2.114

Publication : 17 mai 2020

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2113"></a>Azure ATP version 2.113

Publication : 5 mai 2020

- **Amélioration de fonctionnalité : Enrichissement des activités d’accès aux ressources avec NTLMv1**  
À partir de cette version, Azure ATP fournit des informations pour les activités d’accès aux ressources indiquant si la ressource utilise l’authentification NTLMv1. Non sécurisée, cette configuration de ressource comporte un risque que des acteurs malveillants puissent tourner l’application à leur avantage. Pour plus d’informations sur le risque, consultez [Utilisation des protocoles hérités](atp-cas-isp-legacy-protocols.md).

- **Amélioration de fonctionnalité : Alerte suite à une suspicion d’attaque par force brute (Kerberos, NTLM)**  
L’attaque par force brute est utilisée par les attaquants pour pénétrer dans votre organisation et constitue une méthode clé pour découvrir les menaces et les risques dans Azure ATP. Pour vous permettre de vous concentrer sur les risques critiques pour vos utilisateurs, cette mise à jour facilite et accélère l’analyse et l’atténuation des risques, en limitant et en hiérarchisant le volume d’alertes.

## <a name="azure-atp-release-2112"></a>Azure ATP version 2.112

Date de publication : 15 mars 2020

- **Intégration automatique des nouvelles instances d’Azure ATP avec Microsoft Cloud App Security**  
Lors de la création d’une instance d’Azure ATP (anciennement Workspace), l’intégration avec Microsoft Cloud App Security est activée par défaut. Pour plus d’informations sur l’intégration, consultez [Utilisation d’Azure ATP avec Microsoft Cloud App Security](atp-mcas-integration.md).

- **Nouvelles activités analysées**  
Les analyses d’activité suivantes sont maintenant disponibles :
  - ouverture de session interactive avec un certificat ;
  - échec de l’ouverture de session avec un certificat ;
  - accès délégué aux ressources.

    En savoir plus sur les [activités surveillées par Azure ATP](monitored-activities.md)et la manière de [filtrer et de rechercher des activités surveillées](atp-activities-search.md) dans le portail.

- **Amélioration de fonctionnalité : Enrichissement des activités d’accès aux ressources**  
À partir de cette version, Azure ATP fournit des informations pour les activités d’accès aux ressources indiquant si la ressource est approuvée pour la délégation non contrainte. Non sécurisée, cette configuration de ressource comporte un risque que des acteurs malveillants puissent tourner l’application à leur avantage. Pour plus d'informations sur le risque, consultez [Évaluation de sécurité : Délégation Kerberos non sécurisée](atp-cas-isp-unconstrained-kerberos.md).

- **Manipulation présumée de paquet SMB (exploitation CVE-2020-0796) - (préversion)**  
L’alerte de sécurité [Manipulation présumée de paquet SMB](atp-lateral-movement-alerts.md#suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406) d’Azure ATP est maintenant en préversion publique. Avec ce système de détection, une alerte de sécurité Azure ATP est déclenchée lorsque des paquets SMBv3 suspectées d’exploiter la faille de sécurité [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796) sont effectuées sur un contrôleur de domaine dans le réseau.

## <a name="azure-atp-release-2111"></a>Azure ATP version 2.111

Date de publication : 1er mars 2020

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2110"></a>Azure ATP version 2.110

Publication : 23 février 2020

- **Nouvelle évaluation de la sécurité : contrôleurs de domaine non supervisés**  
Les évaluations de la sécurité Azure ATP incluent désormais un rapport sur les contrôleurs de domaine non supervisés et les serveurs sans capteur pour vous aider à gérer la couverture complète de votre environnement. Pour plus d’informations, consultez [Contrôleurs de domaine non supervisés](atp-cas-isp-unmonitored-domain-controller.md).

## <a name="azure-atp-release-2109"></a>Azure ATP version 2.109

Mise en production : 16 février 2020

- **Amélioration de fonctionnalité : entités sensibles**  
À partir de cette version (2.109), les ordinateurs identifiés comme Autorité de certification, DHCP ou serveurs de noms de domaine par Azure ATP sont désormais automatiquement marqués comme **Sensibles**.

## <a name="azure-atp-release-2108"></a>Azure ATP version 2.108

Mise en production : 9 février 2020

- **Nouvelle fonctionnalité : Support des comptes de service administré du groupe**  
Azure ATP prend désormais en charge l’utilisation de comptes de service administré du groupe (gMSA) pour renforcer la sécurité lors de la connexion des capteurs Azure ATP à vos forêts Azure Active Directory (AD). Pour plus d’informations sur l’utilisation de gMSA avec des capteurs Azure ATP, consultez [Se connecter à votre forêt Active Directory](install-atp-step2.md#prerequisites).

- **Amélioration de fonctionnalité : Rapport planifié avec trop de données**  
Lorsqu’un rapport planifié contient trop de données, l’e-mail vous en informe maintenant en affichant le texte suivant : La période spécifiée contient trop de données pour générer un rapport. Cela remplace le comportement précédent de la découverte du fait uniquement après avoir cliqué sur le lien de rapport dans l’e-mail.

- **Amélioration de fonctionnalité : Logique de la couverture des contrôleurs de domaine mis à jour**  
Nous avons mis à jour notre logique de rapport de couverture des contrôleurs de domaine pour inclure des informations supplémentaires à partir d’Azure AD, ce qui permet d’obtenir une vue plus précise des contrôleurs de domaine sans capteurs. Cette nouvelle logique doit également avoir un impact positif sur le score sécurisé Microsoft correspondant.

## <a name="azure-atp-release-2107"></a>Azure ATP version 2.107

Mise en production : 3 février 2020

- **Nouvelle activité supervisée : Modification de l’historique des SID**  
La modification de l’historique des SID est désormais une activité surveillée et filtrable. En savoir plus sur les [activités surveillées par Azure ATP](monitored-activities.md)et la manière de [filtrer et de rechercher des activités surveillées](atp-activities-search.md) dans le portail.

- **Amélioration de fonctionnalité : Les alertes fermées ou supprimées ne sont plus rouvertes**  
Une fois qu’une alerte est fermée ou supprimée sur le portail Azure ATP, si la même activité est à nouveau détectée peu de temps après, une nouvelle alerte est ouverte. Auparavant, dans les mêmes conditions, l’alerte était rouverte.

- **TLS 1.2 requis pour l’accès au portail et les capteurs**  
TLS 1.2 est désormais requis pour utiliser les capteurs Azure ATP et le service cloud. L’accès au portail Azure ATP n’est plus possible en utilisant des navigateurs qui ne prennent pas en charge TLS 1.2.

## <a name="azure-atp-release-2106"></a>Azure ATP version 2.106

Publication : 19 janvier 2020

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2105"></a>Azure ATP version 2.105

Publication : 12 mai 2020

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2104"></a>Azure ATP version 2.104

Mise en production le 23 septembre 2019

- **Expirations de la version du capteur éliminées**  
Les packages de déploiement de capteur Azure ATP et d’installation de capteur n’expirent plus après un certain nombre de versions et ne sont désormais mis à jour qu’une seule fois. Le résultat de cette fonctionnalité est que les packages d’installation du capteur téléchargés peuvent désormais être installés même si ils sont antérieurs que notre nombre maximum de versions écoulées.

- **Confirmer la compromission**  
Vous pouvez maintenant confirmer la compromission d’utilisateurs Office 365 spécifiques et définir leur niveau de risque sur **haut**. Ce flux de travail permet à vos équipes d’opérations de sécurité de réduire les seuils de délai de résolution des incidents de sécurité. En savoir plus sur [comment confirmer la compromission](https://docs.microsoft.com/cloud-app-security/tutorial-ueba?branch=pr-en-us-1204#phase-4-protect-your-organization) à l’aide de Azure ATP et Cloud App Security.

- **Nouvelle bannière d’expérience**  
Sur les pages du portail Azure ATP où une nouvelle expérience est disponible dans le portail Cloud App Security, de nouvelles bannières s’affichent pour décrire ce qui est disponible avec les liens d’accès.

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2103"></a>Azure ATP version 2.103

Publication : 15 décembre 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2102"></a>Azure ATP version 2.102

Publication : 8 septembre 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2101"></a>Azure ATP version 2.101

Publication : 24 novembre 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-2100"></a>Azure ATP version 2.100

Publication : 17 novembre 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-299"></a>Azure ATP version 2.99

Publication : 3 novembre 2019

- **Amélioration de fonctionnalité :  ajout de la notification de l’interface utilisateur relative à la disponibilité du portail Cloud App Security au portail Azure ATP**  
Pour garantir que tous les utilisateurs soient informés de la disponibilité des fonctionnalités améliorées disponibles à l’aide du portail Cloud App Security, la notification a été ajoutée pour le portail à partir de la chronologie d’alerte Azure ATP existante.

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-298"></a>Azure ATP version 2.98

Publication : 27 octobre 2019

- **Amélioration de fonctionnalité : alerte de suspicion d’attaque par force brute**  
Amélioration de l’[alerte de suspicion d’attaque par force brute (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033) à l’aide d’une analyse supplémentaire et amélioration de la logique de détection pour réduire les résultats d’alerte **vrai positif (B-TP)** et **faux positif (FP)** .

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-297"></a>Azure ATP version 2.97

Publication : 6 octobre 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-296"></a>Azure ATP version 2.96

Publication : 22 septembre 2019

- **Données d’authentification NTLM enrichies avec l’événement Windows 8004**  
Les capteurs Azure ATP sont désormais en mesure de lire et d’enrichir automatiquement les activités d’authentification NTLM avec vos données de serveur ayant fait l’objet d’un accès lorsque l’audit NTLM et l’événement Windows 8004 sont activés. Azure ATP analyse l’événement Windows 8004 pour les authentifications NTLM afin d’enrichir les données d’authentification NTLM utilisées pour l’analyse des menaces et les alertes Azure ATP. Cette fonctionnalité améliorée fournit une activité d’accès aux ressources via les données NTLM ainsi que des activités d’échecs de connexion enrichies, y compris l’ordinateur de destination auquel l’utilisateur a tenté d’accéder sans succès.

    En savoir plus sur les activités d’authentification NTLM [avec l’événement Windows 8004](configure-windows-event-collection.md#ntlm-authentication-using-windows-event-8004).

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-295"></a>Azure ATP version 2.95

Publication : 15 septembre 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-294"></a>Azure ATP version 2.94

Publication : 8 septembre 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-293"></a>Azure ATP version 2.93

Publication : 1er septembre 2019

-   Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-292"></a>Azure ATP version 2.92

Publication : 25 août 2019

-   Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-291"></a>Azure ATP version 2.91

Publication : 18 août 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-290"></a>Azure ATP version 2.90

Publication : 11 août 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-289"></a>Azure ATP version 2.89

Publication : 4 août 2019

- **Améliorations des méthodes des capteurs**  
Afin d’éviter la génération d’un trafic NTLM excessif lors de la création d’évaluations précises d’un chemin de mouvement latéral (Lateral Movement Path ou LMP), des améliorations ont été apportées aux méthodes des capteurs Azure ATP pour réduire l’utilisation de NTLM et utiliser Kerberos de manière plus significative.

- **Amélioration de l’alerte : Suspicion d’utilisation de golden ticket (compte inexistant)**  
Des changements du nom SAM ont été ajoutés aux types de preuves énumérés dans ce type d'alerte. Pour en savoir plus sur l'alerte, notamment comment prévenir ce type d'activité et y remédier, voir [Suspicion d'utilisation de golden ticket (compte inexistant)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027).

- **Disponibilité générale : Falsification de l’authentification NTLM suspectée**  
L'alerte [Falsification de l’authentification NTLM suspectée](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039) n'est plus en mode préversion et est maintenant généralement disponible.

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-288"></a>Azure ATP version 2.88

Publication : 28 juillet 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-287"></a>Azure ATP version 2.87

Publication : 21 juillet 2019

- **Amélioration de fonctionnalité : Collecte automatisée d’événements Syslog pour les capteurs autonomes Azure ATP**  
Les connexions Syslog entrantes pour les capteurs autonomes Azure ATP sont maintenant entièrement automatisées, tout en supprimant le bouton bascule de l’écran de configuration. Ces modifications n’ont aucun effet sur les connexions Syslog sortantes.

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-286"></a>Azure ATP version 2.86

Publication : 14 juillet 2019

- **Nouvelle alerte de sécurité : Falsification de l’authentification NTLM suspectée (ID externe 2039)**  
La nouvelle alerte de sécurité [Falsification de l’authentification NTLM suspectée](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039) d’Azure ATP est désormais en préversion publique.    Dans cette détection, une alerte de sécurité Azure ATP est déclenchée quand l’utilisation d’une attaque de l’intercepteur (« man in the middle ») est suspectée, avec contournement de la vérification de l’intégrité des messages (MIC) NTLM, une faille de sécurité détaillée dans Microsoft [CVE-2019-040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040). Ces types d’attaques tentent de rétrograder les fonctionnalités de sécurité de NTLM et de s’authentifier, avec l’objectif ultime d’effectuer des mouvements transversaux réussis.

- **Amélioration de fonctionnalité : Identification complète du système d'exploitation d'un appareil**  
Jusqu’à présent, Azure ATP fournissait des informations sur le système d’exploitation de l’appareil pour l’entité en fonction de l’attribut disponible dans Active Directory. Avant, si les informations du système d’exploitation n’étaient pas disponibles dans Active Directory, elles ne l’étaient pas non plus dans les pages des entités Azure ATP. À compter de cette version, Azure ATP fournit ces informations pour les appareils où Active Directory ne dispose pas des informations ou qui ne sont pas inscrits dans Active Directory, en utilisant des méthodes complètes d'identification du système d'exploitation de l’appareil.

    L’ajout d’informations complètes sur le système d'exploitation de l’appareil permet d’identifier les appareils non inscrits et non-Windows, tout en facilitant vos processus d’investigation. Pour plus d’informations sur la résolution de noms réseau dans Azure ATP, consultez [Comprendre la résolution de noms réseau (NNR)](atp-nnr-policy.md).  

- **Nouvelle fonctionnalité : Proxy authentifié - préversion**  
Azure ATP prend désormais en charge les proxys authentifiés. Spécifiez l’URL du proxy en utilisant la ligne de commande du capteur et spécifiez le nom d’utilisateur/mot de passe pour utiliser des proxys qui nécessitent une authentification. Pour plus d’informations sur l’utilisation des proxys authentifiés, consultez [Configurer le proxy](https://docs.microsoft.com/azure-advanced-threat-protection/configure-proxy#configure-the-proxy).

- **Amélioration de fonctionnalité : Processus de synchronisateur de domaine automatisé**  
Le processus de désignation et d’étiquetage des contrôleurs de domaine en tant que candidats synchronisateurs de domaine lors de l’installation et de la configuration continue est désormais entièrement automatisé. L’option permettant de sélectionner/désélectionner manuellement les contrôleurs de domaine en tant que candidats synchronisateur de domaine est supprimée.

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-285"></a>Azure ATP version 2.85

Publication : 7 juillet 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-284"></a>Azure ATP version 2.84

Publication : 1er juillet 2019

- **Prise en charge d’un nouvel emplacement : Centre de données Azure au Royaume-Uni**  
Les instances Azure ATP sont désormais prises en charge dans le centre de données Azure au Royaume-Uni. Pour en savoir plus sur la création d’instances Azure ATP et les emplacements de leurs centres de données correspondants, consultez l’[étape 1 de l’installation d’Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step1).

- **Amélioration de fonctionnalité : Nouveau nom et nouvelles fonctionnalités pour l’alerte Ajouts suspects à des groupes sensibles (ID externe 2024)**  
L’alerte **Ajouts suspects à des groupes sensibles** était précédemment appelée **Modifications suspectes des groupes sensibles**. L’ID externe de l’alerte (ID 2024) ne change pas. Ce changement de nom reflète plus fidèlement l’objectif de l’alerte qui est de vous alerter en cas d’ajout à vos groupes **sensibles**. L’alerte améliorée comprend également de nouvelles preuves et des descriptions améliorées. Pour plus d’informations, consultez [Ajouts suspects à des groupes sensibles](https://docs.microsoft.com/azure-advanced-threat-protection/atp-domain-dominance-alerts#suspicious-additions-to-sensitive-groups-external-id-2024).  

- **Nouvelle fonctionnalité de la documentation : Guide permettant de passer d’Advanced Threat Analytics à Azure ATP**  
Ce nouvel article liste les prérequis, les conseils de planification ainsi que les étapes de configuration et de vérification pour passer d’ATA au service Azure ATP. Pour plus d’informations, consultez [Passer d’ATA à Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/ata-atp-move-overview).

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-283"></a>Azure ATP version 2.83

Publication : 23 juin 2019

- **Amélioration de fonctionnalité : Alerte Création de service malveillant (ID externe 2026)**  
Cette alerte propose désormais une page améliorée avec des preuves supplémentaires et une nouvelle description. Pour plus d’informations, consultez l’[alerte de sécurité concernant la création d’un service suspect](https://docs.microsoft.com/azure-advanced-threat-protection/atp-domain-dominance-alerts#suspicious-service-creation-external-id-2026).

- **Prise en charge du nommage d’instance : possibilité d’ajouter un préfixe de domaine composé uniquement de chiffres**  
Il est désormais possible de créer des instances Azure ATP à l’aide de préfixes de domaine initial contenant uniquement des chiffres. Par exemple, l’utilisation du préfixe de domaine initial 123456.contoso.com est à présent pris en charge.

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-282"></a>Azure ATP version 2.82

Publication : 18 juin 2019

- **Nouvelle préversion publique**  
L’expérience d’examen des menaces d’identité d’Azure ATP est désormais en **préversion publique** et disponible sur tous les locataires Azure ATP protégés. Consultez [Expérience d’examen d’Azure ATP avec Microsoft Cloud App Security](atp-mcas-integration.md) pour en savoir plus.

- **Disponibilité générale**  
La prise en charge d’Azure ATP pour les forêts non approuvées est maintenant disponible de façon générale. Pour en savoir plus, consultez [Prise en charge de plusieurs forêts dans Azure Advanced Threat Protection](atp-multi-forest.md).

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-281"></a>Azure ATP version 2.81

Publication : 10 juin 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-280"></a>Azure ATP version 2.80

Publication : 2 juin 2019

- **Amélioration de fonctionnalité : Alerte de connexion VPN suspecte**  
Cette alerte inclut désormais une description plus détaillée des preuves pour offrir une meilleure convivialité. Pour plus d’informations sur les fonctionnalités d’alerte, les suggestions de correction et la prévention, consultez la [description de l’alerte de connexion VPN suspecte](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025).

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-279"></a>Azure ATP version 2.79

Publication : le 26 mai 2019

- **Disponibilité générale : Reconnaissance de principal de sécurité (LDAP) (ID externe 2038)**

    Cette alerte est maintenant en disponibilité générale. Pour plus d’informations sur l’alerte, les fonctionnalités d’alerte et les suggestions de correction et la prévention, consultez [Description de l’alerte Reconnaissance de principal de sécurité (LDAP)](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-278"></a>Azure ATP version 2.78

Publication : le 19 mai 2019

- **Amélioration de fonctionnalité : entités sensibles**  
Marquage sensible manuel pour les serveurs Exchange

    Il est maintenant possible de marquer manuellement des entités comme serveurs Exchange lors de la configuration.

    Pour marquer manuellement une entité comme serveur Exchange :
    1. Sur le portail Azure ATP, accédez au menu **Configuration**.
    2. Sous **Détection**, sélectionnez **Étiquettes d’entité**, puis **Sensible**.
    3. Sélectionnez **Serveurs Exchange**, puis ajoutez l’entité à marquer.

    Un ordinateur marqué comme serveur Exchange s’affiche comme tel. Il porte l’étiquette Sensible,  qui apparaît dans son profil d’entité. Il est pris en compte dans toutes les détections liées aux comptes sensibles et aux chemins de mouvement latéral.

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-277"></a>Azure ATP version 2.77

Publication le 12 mai 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-276"></a>Azure ATP version 2.76

Publication le 6 mai 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-275"></a>Azure ATP version 2.75

Publication le 28 avril 2019

- **Amélioration de fonctionnalité : entités sensibles**  
À partir de cette version (2.75), les ordinateurs identifiés comme serveurs Exchange par Azure ATP sont désormais automatiquement marqués comme **Sensibles**.  

    Les entités qui sont automatiquement marquées comme étant **Sensibles** parce qu’elles fonctionnent en tant que serveurs Exchange indiquent cette classification comme raison.

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-274"></a>Azure ATP version 2.74

Publication le 14 avril 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-273"></a>Azure ATP version 2.73

Publication : 10 avril 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-272"></a>Azure ATP version 2.72

Date de publication : 31 mars 2019

- **Amélioration de fonctionnalité : Profondeur de l’étendue du chemin de mouvement latéral (LMP)**  
Les chemins de mouvement latéral (LMP) constituent une méthode clé pour la détection des menaces et des risques dans Azure ATP. Pour mieux cibler les risques critiques pouvant affecter vos utilisateurs les plus sensibles, cette mise à jour permet d’analyser et de corriger plus rapidement et facilement ces risques au niveau de chaque LMP, en limitant l’étendue et la profondeur de chaque graphique affiché.

    Consultez la section [Chemins de mouvement latéral](use-case-lateral-movement-path.md) pour en savoir plus sur la façon dont Azure ATP utilise les LMP pour atténuer les risques d’accès à chaque entité dans votre environnement.

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-271"></a>Azure ATP version 2.71

Date de publication : 24 mars 2019

- **Amélioration de fonctionnalité : Alertes d’intégrité de résolution de noms réseau (NNR)**  
Des alertes d’intégrité ont été ajoutées pour les niveaux de confiance associés à des alertes de sécurité Azure ATP qui reposent sur la résolution NNR. Chacune comprend des recommandations actionnables et détaillées aidant à résoudre les faibles taux de réussite NNR.

    Pour plus d’informations sur la façon dont Azure ATP utilise la résolution NNR et sur son importance pour l’exactitude des alertes, voir [Présentation de la résolution de noms réseau](atp-nnr-policy.md).

- **Prise en charge serveur : ajout de Server 2019 avec KB4487044**  
Windows Server 2019 est maintenant pris en charge, avec le niveau de correctif KB4487044. L’utilisation de Server 2019 sans le correctif, non prise en charge, est bloquée à partir de cette mise à jour.

- **Amélioration de fonctionnalité : Exclusion d’alertes en fonction des utilisateurs**  
Les options d’exclusion d’alertes étendues permettent à présent d’exclure certains utilisateurs de certaines alertes. Les exclusions sont utiles pour éviter les situations dans lesquelles l’utilisation ou la configuration de certains types de logiciels internes déclenche régulièrement des alertes de sécurité sans gravité.

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-270"></a>Azure ATP version 2.70

Date de publication : 17 mars 2019

- **Amélioration de fonctionnalité : Ajout du niveau de confiance Résolution de noms réseau (NNR) à plusieurs alertes**  La Résolution de noms de réseau (NNR) est utilisée pour aider à identifier l’identité de l’entité source des attaques suspectées. En ajoutant les niveaux de confiance NNR aux listes de preuves des alertes Azure ATP, vous pouvez instantanément évaluer et comprendre le niveau de confiance NNR relatif aux sources possibles identifiés et corriger en conséquence.

    Une preuve de niveau de confiance NNR a été ajoutée aux alertes suivantes :
  - [Reconnaissance de mappage de réseau (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)
  - [Suspicion d’usurpation d’identité (pass-the-ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)
  - [Suspicion d’attaque de relais NTLM (compte Exchange) - préversion](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)
  - [Suspicion d’attaque DCSync (réplication de services d’annuaire)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)

- **Scénario d’alerte d’intégrité supplémentaire : Échec du démarrage du service de capteur Azure ATP**  
Dans les instances où le capteur Azure ATP n’a pas réussi à démarrer en raison d’un problème de pilote de capture réseau, une alerte d’intégrité de capteur est désormais déclenchée. [Résolution des problèmes de capteur Azure ATP avec les journaux Azure ATP](troubleshooting-atp-using-logs.md) pour plus d’informations sur les journaux Azure ATP et comment les utiliser.

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-269"></a>Azure ATP version 2.69

Date de publication : 10 mars 2019

- **Amélioration de fonctionnalité : Alerte de suspicion d’usurpation d’identité (pass-the-ticket)**   Cette alerte présente maintenant de nouvelles preuves montrant les détails des connexions établies avec le protocole Bureau à distance (RDP). La preuve ajoutée simplifie la résolution du problème connu des alertes B-TP (Begnin-True Positive) causées par l’utilisation de Credential Guard à distance sur les connexions RDP.

- **Amélioration de fonctionnalité : Alerte d’exécution de code à distance sur DNS**  
Cette alerte présente maintenant une nouvelle preuve montrant l’état de mise à jour de sécurité de votre contrôleur de domaine pour vous informer si des mises à jour sont requises.

- **Nouvelle fonctionnalité de la documentation : Alerte de sécurité Azure ATP MITRE ATT&CK Matrix&trade;**  
Pour expliquer et simplifier la relation entre les alertes de sécurité Azure ATP et la matrice connue MITRE ATT&CK Matrix, nous avons ajouté les techniques MITRE appropriées aux listes des alertes de sécurité Azure ATP. Cette référence supplémentaire permet de comprendre plus facilement la technique d’attaque présumée potentiellement utilisée quand une alerte de sécurité Azure ATP est déclenchée. Découvrez plus en détail le [guide des alertes de sécurité Azure ATP](suspicious-activity-guide.md).  

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-268"></a>Azure ATP version 2.68

Date de publication : 3 mars 2019

- **Amélioration de fonctionnalité : alerte de suspicion d’attaque par force brute (LDAP)**  
Des améliorations significatives ont été apportées à la convivialité de cette alerte de sécurité, y compris une description révisée, la fourniture d'informations supplémentaires sur les sources et des détails sur les tentatives de deviner des informations pour y remédier plus rapidement.  
En savoir plus sur les alertes de sécurité relatives à la [suspicion d’attaque par force brute (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004).

- **Nouvelle fonctionnalité de la documentation : labo d’alertes de sécurité**  
Pour expliquer la puissance d’Azure ATP dans la détection des menaces réelles pour votre environnement de travail, nous avons ajouté un nouveau **labo d’alertes de sécurité** à cette documentation. Le **labo d’alertes de sécurité** vous aide à configurer rapidement un labo ou un environnement de test et explique la meilleure posture défensive contre les menaces et attaques réelles courantes.  

    Le [labo pas à pas](atp-playbook-lab-overview.md) est conçu pour vous garantir un temps de création minimal et plus de temps pour en savoir plus sur votre paysage de menaces ainsi que sur les alertes Azure ATP et les moyens de protection disponibles. Nous attendons vos commentaires avec impatience.

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-267"></a>Azure ATP version 2.67

Date de publication : 24 février 2019

- **Nouvelle alerte de sécurité : Reconnaissance de principal de sécurité (LDAP) – (préversion)**  
L’alerte de sécurité [Reconnaissance de principal de sécurité (LDAP) : préversion](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038) d’Azure ATP est désormais disponible en préversion publique.    Dans cette détection, une alerte de sécurité Azure ATP est déclenchée lorsque la reconnaissance de principal de sécurité est utilisée par les attaquants pour obtenir des informations critiques sur l’environnement de domaine. Ces informations aident les attaquants à mapper la structure de domaine et à identifier des comptes privilégiés pour une utilisation dans les étapes ultérieures de leur chaîne d’attaque.

    Le protocole LDAP est l’une des méthodes les plus populaires utilisées à des fins légitimes et malveillantes pour interroger Active Directory. La reconnaissance de principal de sécurité basée sur LDAP est couramment utilisée en tant que première phase d’une attaque Kerberoasting. Les attaques Kerberoasting sont utilisées pour obtenir la liste cible des noms de principal de sécurité (SPN), pour lesquels les attaquants tentent ensuite d’obtenir des tickets TGS (Ticket Granting Server).

- **Amélioration de fonctionnalité : Alerte Reconnaissance d’énumération de compte (NTLM)**  
Amélioration de l’alerte **Reconnaissance d’énumération de compte (NTLM)** à l’aide d’une analyse supplémentaire et logique de détection améliorée pour réduire les résultats de l’alerte **B-TP** et **FP**.

- **Amélioration de fonctionnalité : Alerte Reconnaissance de mappage de réseau (DNS)**  
Nouveaux types de détections ajoutés aux alertes Reconnaissance de mappage de réseau (DNS). Outre la détection des requêtes AXFR suspectes, Azure ATP détecte désormais les types suspects de requêtes provenant de serveurs non DNS utilisant un nombre excessif de requêtes.

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-266"></a>Azure ATP version 2.66

Date de publication : 17 février 2019

- **Amélioration de fonctionnalité : Suspicion d’attaque DCSync (réplication de services d’annuaire)**  
Des améliorations ont été apportées à la convivialité de cette alerte de sécurité, y compris une description révisée, la fourniture d'informations supplémentaires sur les sources, de nouvelles données infographiques et d'autres preuves.
En savoir plus sur les alertes de sécurité relatives à la [Suspicion d’attaque DCSync (réplication de services d’annuaire)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006).

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-265"></a>Azure ATP version 2.65

Date de publication : 10 février 2019

- **Nouvelle alerte de sécurité : Suspicion d’attaque de relais NTLM (compte Exchange) - (préversion)**  
L’alerte de sécurité [Suspicion d’attaque de relais NTLM (compte Exchange) - (préversion)](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037) d’Azure ATP est maintenant en préversion publique.    Dans cette détection, une alerte de sécurité Azure ATP est déclenchée quand une utilisation d’informations d’identification d’un compte Exchange à partir d’une source suspecte est identifiée. Ces types d’attaques tentent de tirer parti des techniques de relais NTLM pour obtenir des privilèges Exchange d’un contrôleur de domaine ; elles sont appelées **ExchangePriv**. En savoir plus sur la technique **ExchangePriv** dans l’[avis ADV190007](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV190007) publié pour la première fois le 31 janvier 2019 et dans la [réponse à l’alerte Azure ATP](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/How-to-win-the-latest-security-race-over-NTLM-relay/ba-p/334511).  

- **Disponibilité générale : Exécution de code à distance sur DNS**  
Cette alerte est maintenant en disponibilité générale. Pour plus d’informations et de caractéristiques d’alerte, consultez la [page de description de l’alerte de l’exécution de code à distance via DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036).

- **Disponibilité générale : Exfiltration de données sur SMB**  
Cette alerte est maintenant en disponibilité générale. Pour plus d’informations et de caractéristiques d’alerte, consultez la [page de description de l’alerte de l’exfiltration de données via SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030).

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-264"></a>Azure ATP version 2.64

Date de publication : 4 février 2019

- **Disponibilité générale : Suspicion d’utilisation de golden ticket (anomalie de ticket)**  
Cette alerte est maintenant en disponibilité générale. Pour plus d’informations et de caractéristiques d’alerte, consultez la [page de description de l’alerte d’utilisation du golden ticket (anomalie de ticket)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032).

- **Amélioration de fonctionnalité : Reconnaissance de mappage de réseau (DNS)**  
Logique de détection d’alerte améliorée déployée pour cette alerte afin de minimiser les faux positifs et réduire le bruit des alertes. Cette alerte a maintenant une période d’apprentissage de huit jours avant que l’alerte ne soit éventuellement déclenchée pour la première fois. Pour plus d’informations sur cette alerte, consultez la [page de description de l’alerte de reconnaissance de mappage de réseau (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007).

    **En raison de l’amélioration de cette alerte, la méthode nslookup ne doit plus être utilisée pour tester la connectivité d’Azure ATP lors de la configuration initiale.**

- **Amélioration de fonctionnalité :**  
Cette version inclut des pages d’alerte repensées et de nouveaux éléments de preuve, offrant une meilleure investigation des alertes.
  - [Suspicion d’attaque par force brute (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)
  - [Page de description de l’alerte Suspicion d’utilisation de golden ticket (anomalie de temps)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)
  - [Suspicion d’attaque over-pass-the-hash (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)
  - [Suspicion d’utilisation du framework de piratage Metasploit](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)
  - [Suspicion d’attaque de ransomware WannaCry](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-263"></a>Azure ATP version 2.63

Date de publication : 27 janvier 2019

- **Nouvelle fonctionnalité : Prise en charge des forêts non approuvées (préversion)**  
La prise en charge des capteurs Azure ATP dans des forêts non approuvées est désormais disponible en préversion publique.
À partir de la page **Services d’annuaire** du portail Azure ATP, configurez les informations d’identification supplémentaires requises pour permettre aux capteurs Azure ATP de se connecter à plusieurs forêts Active Directory et à envoyer des rapports au service Azure ATP. Pour en savoir plus, consultez [Prise en charge de plusieurs forêts dans Azure Advanced Threat Protection](atp-multi-forest.md).

- **Nouvelle fonctionnalité : Couverture des contrôleurs de domaine**  
Azure ATP fournit maintenant des informations de couverture pour les contrôleurs de domaine Azure ATP qui sont supervisés.  
À partir de la page **Capteurs** du portail Azure ATP, vérifiez le nombre de contrôleurs de domaine supervisés et non supervisés qu’Azure ATP a détectés dans votre environnement. Téléchargez la liste des contrôleurs de domaine supervisés pour effectuer une analyse plus approfondie et établir un plan d’action. Pour en savoir plus, consultez le guide pratique [Supervision des contrôleurs de domaine](atp-sensor-monitoring.md).

- **Amélioration de fonctionnalité : Reconnaissance d’énumération de compte**  
La détection de reconnaissance d’énumération de compte Azure ATP émet désormais des alertes quand elle détecte des tentatives d’énumération à l’aide de Kerberos ou de NTLM. Avant, la détection fonctionnait uniquement pour les tentatives à l’aide de Kerberos. Pour en savoir plus, consultez [Alertes de reconnaissance d’Azure ATP](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003).

- **Amélioration de fonctionnalité : Alerte de tentative d’exécution de code à distance**
  - Toutes les activités d’exécution à distance, telles que la création de service, l’exécution de WMI et l’exécution du nouveau **PowerShell**, ont été ajoutées à la chronologie des profils de la machine de destination. La machine de destination est le contrôleur de domaine sur lequel la commande a été exécutée.
  - L’exécution de **PowerShell** a été ajoutée à la liste des activités d’exécution de code à distance listées dans la chronologie des alertes des profils d’entités.
  - Pour en savoir plus, consultez [Tentative d’exécution de code à distance](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019).  

- **Problème avec le service LSASS Windows Server 2019 et Azure ATP**  
En réponse aux commentaires de clients concernant l’utilisation d’Azure ATP avec des contrôleurs de domaine exécutant Windows Server 2019, cette mise à jour inclut une logique supplémentaire visant à éviter le déclenchement du comportement signalé sur les machines Windows Server 2019. La prise en charge complète du capteur Azure ATP sur Windows Server 2019 sera introduite dans une mise à jour ultérieure d’Azure ATP. L’installation et l’exécution d’Azure ATP sur des machines Windows Server 2019 ne sont **pas** actuellement prises en charge. Pour en savoir plus, consultez [Configuration requise pour le capteur Azure ATP](atp-prerequisites.md#azure-atp-sensor-requirements).

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-262"></a>Azure ATP version 2.62

Publiée le 20 janvier 2019

- **Nouvelle alerte de sécurité : Exécution de code à distance sur DNS (préversion)**  
L’alerte de sécurité [Exécution de code à distance sur DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036) d’Azure ATP est maintenant disponible en préversion publique.    Avec ce système de détection, une alerte de sécurité Azure ATP est déclenchée lorsque des requêtes DNS suspectées d’exploiter la faille de sécurité [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) sont effectuées sur un contrôleur de domaine dans le réseau.

- **Amélioration de fonctionnalité : Mise à jour des capteurs différée de 72 heures**  
L’option permettant de différer la mise à jour de certains capteurs après chaque nouvelle version d’Azure ATP a été modifiée (72 heures au lieu de 24 heures). Pour connaître les instructions de configuration, voir [Mise à jour des capteurs Azure ATP](sensor-update.md).

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-261"></a>Azure ATP version 2.61

Publiée le 13 janvier 2019

- **Nouvelle alerte de sécurité : Exfiltration de données sur SMB - (préversion)**  
L’alerte de sécurité Azure ATP [Exfiltration de données sur SMB](atp-exfiltration-alerts.md) est désormais disponible en préversion publique. Les attaquants ayant des droits d’administrateur de domaine peuvent compromettre le compte KRBTGT. Avec le compte KRBTGT, les attaquants peuvent créer un ticket TGT Kerberos qui fournit une autorisation d’accès à n’importe quelle ressource.

- **Amélioration de fonctionnalité : alerte de sécurité Tentative d’exécution de code à distance**  
Une nouvelle description de l’alerte et des preuves supplémentaires ont été ajoutées pour faciliter la compréhension de l’alerte et fournir de meilleurs workflows d’investigation.

- **Amélioration de fonctionnalité : activités logiques de requêtes DNS**  
Des types de requêtes supplémentaires ont été ajoutés aux [activités supervisées Azure ATP](monitored-activities.md), notamment : **TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**.

- **Amélioration de fonctionnalité : Utilisation de Golden Ticket suspectée (anomalie de ticket) et Utilisation de Golden Ticket suspectée (compte inexistant)**  
Une logique de détection améliorée a été appliquée à deux alertes afin de réduire le nombre d’alertes FP et de fournir des résultats plus précis.

- **Amélioration de fonctionnalité : documentation sur les alertes de sécurité Azure ATP**  
La documentation sur les alertes de sécurité Azure ATP a été améliorée et développée afin d’inclure de meilleures descriptions des alertes, des classifications d’alertes plus précises ainsi que des explications des preuves, des mises à jour et de la prévention. Familiarisez-vous avec la nouvelle conception de la documentation sur les alertes de sécurité à l’aide des liens suivants :
  - [Alertes de sécurité Azure ATP](suspicious-activity-guide.md)
  - [Comprendre les alertes de sécurité](understanding-security-alerts.md)
    - [Alertes de la phase de reconnaissance](atp-reconnaissance-alerts.md)
    - [Alertes de la phase des informations d’identification compromises](atp-compromised-credentials-alerts.md)
    - [Alertes de la phase de mouvement latéral](atp-lateral-movement-alerts.md)
    - [Alertes de la phase de dominance du domaine](atp-domain-dominance-alerts.md)
    - [Alertes de la phase d’exfiltration](atp-exfiltration-alerts.md)
  - [Examiner un ordinateur](investigate-a-computer.md)
  - [Examiner un utilisateur](investigate-a-user.md)

- Cette version contient également des améliorations et des correctifs de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-260"></a>Azure ATP version 2.60

Mise en production du 6 janvier 2019

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-259"></a>Azure ATP version 2.59

Publication : 16 décembre 2018

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-258"></a>Azure ATP version 2.58

Mise en production du 9 décembre 2018

- **Amélioration de l’alerte de sécurité : Fractionnement d’alerte d’implémentation de protocole inhabituelle**  
La série d’alertes de sécurité d’Azure ATP pour l’implémentation de protocoles inhabituels qui partageaient jusqu’à présent un ID externe (2002) est maintenant divisée en quatre alertes distinctes, avec un ID externe unique chacune.

### <a name="new-alert-externalids"></a>Nouvelles externalId d’alerte

> [!div class="mx-tableFixed"]
> |Nouveau nom de l’alerte de sécurité|Ancien nom de l’alerte de sécurité|ID externe unique|
> |---------|----------|---------|
> |Suspicion d’attaque par force brute (SMB)|Implémentation de protocole inhabituelle (utilisation potentielle d’outils malveillants comme Hydra)|2033
> |Suspicion d’attaque over-pass-the-hash (Kerberos)|Implémentation inhabituelle du protocole Kerberos (attaque overpass-the-hash potentielle)|2002|
> |Suspicion d’utilisation du framework de piratage Metasploit|Implémentation de protocole inhabituelle (utilisation potentielle d’outils de piratage Metasploit)|2034
> |Suspicion d’attaque de ransomware WannaCry|Implémentation de protocole inhabituelle (attaque ransomware WannaCry potentielle)|2035
> |

- **Nouvelle activité supervisée : Copie des fichiers via SMB**  
La copie des fichiers à l’aide de SMB est maintenant une activité surveillée et filtrable. En savoir plus sur les [activités surveillées par Azure ATP](monitored-activities.md)et la manière de [filtrer et de rechercher des activités surveillées](atp-activities-search.md) dans le portail.

- **Amélioration de l’image des chemins de mouvement latéral**  
Lors de l'affichage de grands chemins de mouvement latéral, Azure ATP ne met désormais en surbrillance que les nœuds connectés à une entité sélectionnée au lieu d'estomper les autres nœuds. Ce changement introduit une amélioration significative de la vitesse de rendu des chemins de mouvement latéral volumineux.

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-257"></a>Azure ATP version 2.57

Publication : 2 décembre 2018

- **Nouvelle alerte de sécurité : Suspicion d’utilisation de golden ticket - anomalie de ticket (préversion)**  
L’alerte de sécurité d’Azure ATP [Suspicion d’utilisation de golden ticket - anomalie de ticket](suspicious-activity-guide.md) est désormais disponible dans la préversion publique.    Les attaquants ayant des droits d’administrateur de domaine peuvent compromettre le compte KRBTGT. Avec le compte KRBTGT, les attaquants peuvent créer un ticket TGT Kerberos qui fournit une autorisation sur n’importe quelle ressource.

    Ce ticket TGT falsifié est appelé « golden ticket », car il permet aux attaquants d’obtenir une persistance réseau durable. Les golden tickets falsifiés de ce type ont des caractéristiques uniques qui peuvent être identifiées par cette nouvelle détection.

- **Amélioration de fonctionnalité : création automatisée d’instance (espace de travail) Azure ATP**  
À compter de ce jour, les *espaces de travail* Azure ATP sont renommés *instances* Azure ATP. Azure ATP prend désormais en charge une instance Azure ATP par compte Azure ATP. Les nouveaux clients créent leurs instances à l’aide de l’Assistant Création d’instance du [portail Azure ATP](https://portal.atp.azure.com). Les espaces de travail Azure ATP existants sont convertis automatiquement en instances Azure ATP avec cette mise à jour.  

  - Création d’instance simplifiée pour un déploiement et une protection plus rapides en utilisant la procédure [Création de votre instance Azure ATP](install-atp-step1.md).
  - Toutes les garanties de [conformité et de confidentialité des données](atp-privacy-compliance.md) sont inchangées.

  Pour en savoir plus sur les instances Azure ATP, consultez [Créer votre instance Azure ATP](install-atp-step1.md).

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

## <a name="azure-atp-release-256"></a>Azure ATP version 2.56

Publication : 25 novembre 2018

- **Amélioration de fonctionnalité : Chemins de mouvement latéral**  
Deux fonctionnalités supplémentaires ont été ajoutées pour améliorer les capacités de chemin de mouvement latéral d’Azure ATP :

  - L’historique des chemins de mouvement latéral est maintenant enregistré et détectable par entité et en cas d’utilisation de rapports Chemins de mouvement latéral.
  - Vous pouvez suivre une entité dans un chemin de mouvement latéral via la chronologie des activités et investiguer en utilisant une preuve supplémentaire fournie pour la détection de chemins d’attaque potentiels.

  Consultez [Chemins de mouvement latéral d’Azure ATP](use-case-lateral-movement-path.md) pour savoir comment tirer parti des chemins de mouvement latéral améliorés dans vos investigations.

- **Améliorations de la documentation : chemins de mouvement latéral, noms des alertes de sécurité**  
Les articles Azure ATP décrivant les caractéristiques de la fonctionnalité des chemins de mouvement latéral ont été mis à jour et complétés, et une correspondance entre les anciens et les nouveaux noms d’alertes de sécurité et les externalIds a été ajoutée.
  - Pour plus d’informations, consultez [Chemins de mouvement latéral d’Azure ATP](use-case-lateral-movement-path.md), [Utilisation des chemins de mouvement latéral](investigate-lateral-movement-path.md) et [Guide des alertes de sécurité](suspicious-activity-guide.md).

- Cette version contient des améliorations et des corrections de bogues pour l’infrastructure des capteurs internes.

Pour plus d’informations sur chacune des versions antérieures à la version 2.55 d’Azure ATP (comprise), voir la [Référence sur les versions d’Azure ATP](atp-release-reference.md).

## <a name="see-also"></a>Voir aussi

- [Présentation d’Azure Advanced Threat Protection](what-is-atp.md)
- [Forum Aux Questions](atp-technical-faq.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
