---
title: Présentation des alertes d’intégrité Microsoft Defender pour Identity
description: Cet article décrit toutes les alertes d’intégrité pour chaque composant, en listant la cause et les étapes nécessaires pour résoudre le problème.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4fb7bf73ed996007e3a3c84b568afe373d822fd6
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93277096"
---
# <a name="understanding-product-long-sensor-health-alerts"></a>Présentation des alertes d’intégrité du capteur [!INCLUDE [Product long](includes/product-long.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Le centre d’intégrité [!INCLUDE [Product long](includes/product-long.md)] vous informe en cas de problème dans votre instance [!INCLUDE [Product short](includes/product-short.md)] en déclenchant une alerte d’intégrité. Cet article décrit toutes les alertes d’intégrité pour chaque composant, en répertoriant la cause et les étapes nécessaires pour résoudre le problème.

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Tous les contrôleurs de domaine ne sont pas accessibles par un capteur

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le capteur [!INCLUDE [Product short](includes/product-short.md)] est actuellement hors connexion en raison de problèmes de connectivité avec tous les contrôleurs de domaine configurés.|La capacité de [!INCLUDE [Product short](includes/product-short.md)] à détecter les activités suspectes liées aux contrôleurs de domaine supervisés par ce capteur [!INCLUDE [Product short](includes/product-short.md)] s’en trouve affectée.| Vérifiez que les contrôleurs de domaine sont fonctionnels et que ce capteur [!INCLUDE [Product short](includes/product-short.md)] peut y ouvrir des connexions LDAP. En outre, dans **Paramètres** veillez à configurer un compte de service de répertoire pour chaque forêt déployée.|Moyenne|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>L’ensemble ou une partie des cartes réseau de capture sur un capteur ne sont pas disponibles

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|L’ensemble ou une partie des adaptateurs de réseau de capture sélectionnés sur le capteur [!INCLUDE [Product short](includes/product-short.md)] sont désactivés ou déconnectés.|Le trafic réseau de l’ensemble ou d’une partie des contrôleurs de domaine n’est plus capturé par le capteur [!INCLUDE [Product short](includes/product-short.md)]. Ceci a un impact sur la possibilité de détecter les activités suspectes liées à ces contrôleurs de domaine.|Veillez à ce que les adaptateurs de réseau de capture sélectionnés sur le capteur [!INCLUDE [Product short](includes/product-short.md)] soient activés et connectés.|Moyenne|

## <a name="directory-services-user-credentials-are-incorrect"></a>Les informations d'identification de l'utilisateur des services d'annuaire sont incorrectes

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Les informations d’identification du compte d'utilisateur des services d'annuaire sont incorrectes.|Cela a un impact sur la capacité des capteurs à détecter les activités à l’aide de requêtes LDAP sur les contrôleurs de domaine.|- Pour des comptes AD **standard**  : Vérifiez que le nom d’utilisateur, le mot de passe et le domaine dans la page de configuration **Services d’annuaire** sont corrects.<br>- Pour **Comptes de service administré du groupe :** Vérifiez que le nom d’utilisateur et le domaine dans la page de configuration **Services d’annuaire** sont corrects. Vérifiez également tous les autres composants requis du **compte gMSA** décrits dans la page [Se connecter à votre forêt Active Directory](install-step2.md#prerequisites).|Moyenne|

## <a name="low-success-rate-of-active-name-resolution"></a>Taux de réussite faible dans la résolution de noms active

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Les capteurs [!INCLUDE [Product short](includes/product-short.md)] indiqués ne parviennent pas à résoudre les adresses IP en noms d’appareils dans plus de 90 % des cas en utilisant les techniques suivantes :<br />- NTLM sur RPC<br />- NetBIOS<br />- DNS inversé|Les capacités de détection de [!INCLUDE [Product short](includes/product-short.md)] s’en trouvent affectées, et le nombre de fausses alertes positives risque d’augmenter.|- Pour NTLM sur RPC : vérifiez que le port 135 est ouvert pour la communication entrante provenant des capteurs [!INCLUDE [Product short](includes/product-short.md)], sur tous les ordinateurs de l’environnement.<br />- Pour DNS inversé : Vérifiez que le capteur peut atteindre le serveur DNS et que les zones de recherche inversée sont activées.<br />- Pour NetBIOS : vérifiez que le port 137 est ouvert pour la communication entrante provenant des capteurs [!INCLUDE [Product short](includes/product-short.md)], sur tous les ordinateurs de l’environnement.<br />En outre, assurez-vous que la configuration du réseau (par exemple, les pare-feu) n'empêche pas la communication vers les ports concernés.|Faible|

## <a name="no-traffic-received-from-domain-controller"></a>Aucun trafic reçu du contrôleur de domaine

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Aucun trafic n’a été reçu du contrôleur de domaine par le biais de ce capteur [!INCLUDE [Product short](includes/product-short.md)].|Il est possible que la mise en miroir de ports des contrôleurs de domaine au capteur [!INCLUDE [Product short](includes/product-short.md)] ne soit pas encore configurée ou ne fonctionne pas.|Vérifiez que la [mise en miroir de ports est configurée correctement sur vos appareils réseau](configure-port-mirroring.md).<br></br>Sur l’adaptateur de réseau de capture du capteur [!INCLUDE [Product short](includes/product-short.md)], désactivez ces fonctionnalités dans Paramètres avancés :<br></br>RSC (Receive Segment Coalescing) (IPv4)<br></br>RSC (Receive Segment Coalescing) (IPv6)|Moyenne|

## <a name="read-only-user-password-to-expire-shortly"></a>Le mot de passe de l’utilisateur en lecture seule est sur le point d’expirer

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le mot de passe de l’utilisateur en lecture seule, utilisé pour effectuer la résolution des entités sur Active Directory, expire dans moins de 30 jours.|Si le mot de passe de cet utilisateur expire, tous les capteurs [!INCLUDE [Product short](includes/product-short.md)] cessent de fonctionner, et aucune nouvelle donnée n’est collectée.|[Changez le mot de passe de connectivité du domaine](modifying-config-dcpassword.md), puis mettez à jour le mot de passe sur le portail [!INCLUDE [Product short](includes/product-short.md)].|Moyenne|

## <a name="read-only-user-password-expired"></a>Le mot de passe de l’utilisateur en lecture seule a expiré

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le mot de passe de l’utilisateur en lecture seule, utilisé pour d’obtenir des données de l’annuaire, a expiré.|Tous les capteurs [!INCLUDE [Product short](includes/product-short.md)] cessent (ou cesseront bientôt) de fonctionner, et aucune nouvelle donnée n’est collectée.|[Changez le mot de passe de connectivité du domaine](modifying-config-dcpassword.md), puis mettez à jour le mot de passe sur le portail [!INCLUDE [Product short](includes/product-short.md)].|Importante|

## <a name="sensor-outdated"></a>Capteur obsolète

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|L’un des capteurs [!INCLUDE [Product short](includes/product-short.md)] est obsolète.|L’un des capteurs [!INCLUDE [Product short](includes/product-short.md)] possède une version qui ne lui permet pas de communiquer avec l’infrastructure cloud [!INCLUDE [Product short](includes/product-short.md)].|Mettez à jour le capteur manuellement et vérifiez ce qui empêche la mise à jour automatique du capteur. Si cela ne fonctionne pas, téléchargez le dernier package d’installation du capteur, puis désinstallez et réinstallez le capteur. Pour plus d’informations, consultez [Installation du capteur [!INCLUDE [Product short](includes/product-short.md)]](install-step4.md).|Moyenne|

## <a name="sensor-reached-a-memory-resource-limit"></a>Le capteur a atteint la limite des ressources mémoire

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le capteur [!INCLUDE [Product short](includes/product-short.md)] s’est arrêté et redémarre automatiquement pour éviter que le contrôleur de domaine ne présente un problème de mémoire insuffisante.|Le capteur [!INCLUDE [Product short](includes/product-short.md)] s’applique à lui-même des limitations de mémoire pour éviter que le contrôleur de domaine ne présente des limitations de ressources. Ce cas de figure se produit quand l’utilisation de la mémoire sur le contrôleur de domaine est élevée. Les données provenant de ce contrôleur de domaine ne sont que partiellement suivies.|Augmentez la quantité de mémoire (RAM) sur le contrôleur de domaine ou ajoutez des contrôleurs de domaine dans ce site afin de mieux répartir la charge de ce contrôleur de domaine.|Moyenne|

## <a name="sensor-service-failed-to-start"></a>Échec du démarrage du service de capteur

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le démarrage du service de capteur [!INCLUDE [Product short](includes/product-short.md)] a échoué pendant au moins 30 minutes.|La capacité à détecter les activités suspectes provenant des contrôleurs de domaine supervisés par ce capteur [!INCLUDE [Product short](includes/product-short.md)] peut s’en trouver affectée.|Analysez les journaux du capteur [!INCLUDE [Product short](includes/product-short.md)] pour comprendre la cause racine de l’échec du service de capteur [!INCLUDE [Product short](includes/product-short.md)].|Importante|

## <a name="sensor-stopped-communicating"></a>Le capteur a cessé de communiquer

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Aucune communication n’a été reçue du capteur [!INCLUDE [Product short](includes/product-short.md)]. L’intervalle de temps par défaut pour cette alerte est de 5 minutes.|Le trafic réseau n’est plus capturé par l’adaptateur réseau sur le capteur [!INCLUDE [Product short](includes/product-short.md)]. La capacité de Defender pour Identity à détecter les activités suspectes s’en trouve affectée, car le trafic réseau ne pourra pas atteindre le service cloud [!INCLUDE [Product short](includes/product-short.md)].|Vérifiez que le port utilisé pour la communication entre le capteur [!INCLUDE [Product short](includes/product-short.md)] et le service cloud [!INCLUDE [Product short](includes/product-short.md)] n’est pas bloqué par des routeurs ni des pare-feu.|Moyenne|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Certains contrôleurs de domaine ne sont pas accessibles par un capteur

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|L’un des capteurs [!INCLUDE [Product short](includes/product-short.md)] présente des fonctionnalités limitées en raison de problèmes de connectivité avec certains des contrôleurs de domaine configurés.|La détection Pass-the-hash risque d’être moins précise si certains des contrôleurs de domaine ne peuvent pas être interrogés par le capteur [!INCLUDE [Product short](includes/product-short.md)].|Vérifiez que les contrôleurs de domaine sont fonctionnels et que ce capteur [!INCLUDE [Product short](includes/product-short.md)] peut y ouvrir des connexions LDAP.|Moyenne|

## <a name="some-windows-events-are-not-being-analyzed"></a>Certains événements Windows ne sont pas en cours d’analyse

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le capteur [!INCLUDE [Product short](includes/product-short.md)] reçoit plus d’événements qu’il ne peut en traiter.|Certains événements Windows ne sont pas analysés. La capacité à détecter les activités suspectes provenant des contrôleurs de domaine supervisés par ce capteur [!INCLUDE [Product short](includes/product-short.md)] peut s’en trouver affectée.|Vérifiez que seuls les événements nécessaires sont transférés au capteur [!INCLUDE [Product short](includes/product-short.md)] ou essayez d’en transférer une partie à un autre capteur [!INCLUDE [Product short](includes/product-short.md)].|Moyenne|

## <a name="some-network-traffic-could-not-be-analyzed"></a>Une partie du trafic réseau n’a pas pu être analysée

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le capteur [!INCLUDE [Product short](includes/product-short.md)] reçoit plus de trafic réseau qu’il ne peut en traiter.|Une partie du trafic réseau n’a pas pu être analysée. La capacité à détecter les activités suspectes provenant des contrôleurs de domaine supervisés par ce capteur [!INCLUDE [Product short](includes/product-short.md)] peut s’en trouver affectée.|Envisagez [d’ajouter des processeurs et de la mémoire](capacity-planning.md) selon les besoins. S’il s’agit d’un capteur [!INCLUDE [Product short](includes/product-short.md)] autonome, réduisez le nombre de contrôleurs de domaine supervisés.<br></br>Cela peut également se produire si vous utilisez des contrôleurs de domaine sur des machines virtuelles VMware. Pour éviter ces alertes, vous pouvez vérifier que les paramètres suivants sont définis sur 0 ou sont désactivés dans la machine virtuelle :<br></br>- TsoEnable<br></br>- LargeSendOffload(IPv4)<br></br>- IPv4 TSO Offload<br></br>Pensez aussi à désactiver IPv4 Giant TSO Offload. Pour plus d’informations, voir la documentation VMware.|Moyenne|

## <a name="some-etw-events-are-not-being-analyzed"></a>Certains événements ETW ne sont pas en cours d’analyse

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le capteur [!INCLUDE [Product short](includes/product-short.md)] reçoit plus d’événements Suivi d’événements pour Windows (ETW) qu’il ne peut en traiter.|Certains événements Suivi d’événements pour Windows (ETW) ne sont pas analysés. La capacité à détecter les activités suspectes provenant des contrôleurs de domaine supervisés par ce capteur [!INCLUDE [Product short](includes/product-short.md)] peut s’en trouver affectée.|Vérifiez que seuls les événements nécessaires sont transférés au capteur [!INCLUDE [Product short](includes/product-short.md)] ou essayez d’en transférer une partie à un autre capteur [!INCLUDE [Product short](includes/product-short.md)].|Moyenne|

<!--
## Windows events missing from domain controller audit policy

|Alert|Description|Resolution|Severity|
|----|----|----|----|
| Windows events missing from domain controller audit policy|For the correct events to be audited and included in the Windows Event Log, your domain controllers require accurate Advanced Audit Policy settings. Incorrect Advanced Audit Policy settings leave critical events out of your logs, and result in incomplete [!INCLUDE [Product short](includes/product-short.md)] coverage.|Review your [Advanced Audit policy](configure-windows-event-collection.md) and modify as needed. | Medium|
-->

## <a name="see-also"></a>Voir aussi

- [Prérequis de [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Planification de capacité [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
