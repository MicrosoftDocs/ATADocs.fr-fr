---
title: Compréhension des alertes d’intégrité Azure ATP
description: Décrit comment utiliser les journaux Azure ATP pour résoudre des problèmes
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/17/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: d0551e91-3b21-47d5-ad9d-3362df6d47c0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 503b8ac25a8ab812ca48eba138a7eafefe3168c0
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84772358"
---
# <a name="understanding-azure-atp-sensor-health-alerts"></a>Présentation des alertes d’intégrité du capteur Azure ATP

Le centre d’intégrité Azure ATP vous informe de l’existence d’un problème dans votre instance Azure ATP en déclenchant une alerte d’intégrité. Cet article décrit toutes les alertes d’intégrité pour chaque composant, en répertoriant la cause et les étapes nécessaires pour résoudre le problème.

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Tous les contrôleurs de domaine ne sont pas accessibles par un capteur

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le capteur Azure ATP est actuellement hors connexion en raison de problèmes de connectivité avec tous les contrôleurs de domaine configurés.|Ceci a un impact sur la capacité d’Azure ATP à détecter les activités suspectes liées à des contrôleurs de domaine surveillés par ce capteur Azure ATP.| Vérifiez que les contrôleurs de domaine sont fonctionnels et que ce capteur Azure ATP peut les utiliser pour ouvrir des connexions LDAP. En outre, dans **Paramètres** veillez à configurer un compte de service de répertoire pour chaque forêt déployée.|Moyenne|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>L’ensemble ou une partie des cartes réseau de capture sur un capteur ne sont pas disponibles

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|L’ensemble ou une partie des cartes réseau de capture sélectionnées sur le capteur Azure ATP sont désactivées ou déconnectées.|Le trafic réseau pour l’ensemble ou une partie des contrôleurs de domaine n’est plus capturé par le capteur Azure ATP. Ceci a un impact sur la possibilité de détecter les activités suspectes liées à ces contrôleurs de domaine.|Vérifiez que ces cartes réseau de capture sélectionnées sur le capteur Azure ATP sont activées et connectées.|Moyenne|

## <a name="directory-services-user-credentials-are-incorrect"></a>Les informations d'identification de l'utilisateur des services d'annuaire sont incorrectes

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Les informations d’identification du compte d'utilisateur des services d'annuaire sont incorrectes.|Cela a un impact sur la capacité des capteurs à détecter les activités à l’aide de requêtes LDAP sur les contrôleurs de domaine.|- Pour des comptes AD **standard** : Vérifiez que le nom d’utilisateur, le mot de passe et le domaine dans la page de configuration **Services d’annuaire** sont corrects.<br>- Pour **Comptes de service administré du groupe :** Vérifiez que le nom d’utilisateur et le domaine dans la page de configuration **Services d’annuaire** sont corrects. Vérifiez également tous les autres composants requis du **compte gMSA** décrits dans la page [Se connecter à votre forêt Active Directory](install-atp-step2.md#prerequisites).|Moyenne|

## <a name="low-success-rate-of-active-name-resolution"></a>Taux de réussite faible dans la résolution de noms active

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Les capteurs Azure ATP répertoriés ne parviennent pas à résoudre les adresses IP en noms d’appareils dans plus de 90 % des cas en utilisant les méthodes suivantes :<br />- NTLM sur RPC<br />- NetBIOS<br />- DNS inversé|Cela a un impact sur les capacités de détection d’Azure ATP et pourrait augmenter le nombre de fausses alertes positives.|- Pour NTLM sur RPC : Vérifiez que le port 135 est ouvert aux communications entrantes issues des capteurs Azure ATP, sur tous les ordinateurs de l’environnement.<br />- Pour DNS inversé : Vérifiez que le capteur peut atteindre le serveur DNS et que les zones de recherche inversée sont activées.<br />- Pour NetBIOS : Vérifiez que le port 137 est ouvert aux communications entrantes issues des capteurs Azure ATP, sur tous les ordinateurs de l’environnement.<br />En outre, assurez-vous que la configuration du réseau (par exemple, les pare-feu) n'empêche pas la communication vers les ports concernés.|Faible|

## <a name="no-traffic-received-from-domain-controller"></a>Aucun trafic reçu du contrôleur de domaine

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Aucun trafic n’a été reçu du contrôleur de domaine via ce capteur Azure ATP.|Ceci peut indiquer que la mise en miroir de ports des contrôleurs de domaine vers le capteur Azure ATP n’est pas encore configurée ou ne fonctionne pas.|Vérifiez que la [mise en miroir de ports est configurée correctement sur vos appareils réseau](configure-port-mirroring.md).<br></br>Sur la carte réseau de capture du capteur Azure ATP, désactivez ces fonctionnalités dans Paramètres avancés :<br></br>RSC (Receive Segment Coalescing) (IPv4)<br></br>RSC (Receive Segment Coalescing) (IPv6)|Moyenne|

## <a name="read-only-user-password-to-expire-shortly"></a>Le mot de passe de l’utilisateur en lecture seule est sur le point d’expirer

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le mot de passe de l’utilisateur en lecture seule, utilisé pour effectuer la résolution des entités sur Active Directory, expire dans moins de 30 jours.|Si le mot de passe pour cet utilisateur expire, tous les capteurs Azure ATP cessent de fonctionner et aucune nouvelle donnée n’est collectée.|[Changez le mot de passe de connectivité du domaine](modifying-atp-config-dcpassword.md), puis mettez à jour le mot de passe dans le portail Azure ATP.|Moyenne|

## <a name="read-only-user-password-expired"></a>Le mot de passe de l’utilisateur en lecture seule a expiré

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le mot de passe de l’utilisateur en lecture seule, utilisé pour d’obtenir des données de l’annuaire, a expiré.|Tous les capteurs Azure ATP cessent de fonctionner (ou le feront sous peu) et aucune nouvelle donnée n’est collectée.|[Changez le mot de passe de connectivité du domaine](modifying-atp-config-dcpassword.md), puis mettez à jour le mot de passe dans le portail Azure ATP.|Importante|

## <a name="sensor-outdated"></a>Capteur obsolète

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Un capteur Azure ATP est obsolète.|Un capteur Azure ATP exécute une version qui ne peut pas communiquer avec l’infrastructure cloud Azure ATP.|Mettez à jour le capteur manuellement et vérifiez ce qui empêche la mise à jour automatique du capteur. Si cela ne fonctionne pas, téléchargez le dernier package d’installation du capteur, puis désinstallez et réinstallez le capteur. Pour plus d’informations, consultez [Installation du capteur Azure ATP](install-atp-step4.md).|Moyenne|

## <a name="sensor-reached-a-memory-resource-limit"></a>Le capteur a atteint la limite des ressources mémoire

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le capteur Azure ATP s’est arrêté et redémarre automatiquement pour éviter que le contrôleur de domaine ne soit face à une mémoire insuffisante.|Le capteur Azure ATP s’applique à lui-même des limitations de mémoire pour éviter que le contrôleur de domaine ne connaisse des limitations de ressources. Ce cas de figure se produit quand l’utilisation de la mémoire sur le contrôleur de domaine est élevée. Les données provenant de ce contrôleur de domaine ne sont que partiellement suivies.|Augmentez la quantité de mémoire (RAM) sur le contrôleur de domaine ou ajoutez des contrôleurs de domaine dans ce site afin de mieux répartir la charge de ce contrôleur de domaine.|Moyenne|

## <a name="sensor-service-failed-to-start"></a>Échec du démarrage du service de capteur

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le démarrage du service de capteur Azure ATP échoue pendant au moins 30 minutes.|Ceci peut impacter la capacité à détecter les activités suspectes provenant des contrôleurs de domaine surveillés par ce capteur Azure ATP.|Surveillez les journaux du capteur Azure ATP pour comprendre la cause principale de l’échec du service de capteur Azure ATP.|Importante|

## <a name="sensor-stopped-communicating"></a>Le capteur a cessé de communiquer

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Aucune communication n’a été reçue du capteur Azure ATP. L’intervalle de temps par défaut pour cette alerte est de 5 minutes.|Le trafic réseau n’est plus capturé par la carte réseau sur le capteur Azure ATP. Ceci a un impact sur la capacité d’ATA à détecter les activités suspectes, car le trafic réseau ne pourra pas atteindre le service cloud Azure ATP.|Vérifiez que le port utilisé pour la communication entre le capteur Azure ATP et le service cloud Azure ATP n’est pas bloqué par un routeur ni un pare-feu.|Moyenne|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Certains contrôleurs de domaine ne sont pas accessibles par un capteur

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Un capteur Azure ATP a des fonctionnalités limitées en raison de problèmes de connectivité avec certains des contrôleurs de domaine configurés.|La détection d’attaques de type « Pass-The-Hash » peut être moins précise quand certains contrôleurs de domaine ne peuvent pas être interrogés par le capteur Azure ATP.|Vérifiez que les contrôleurs de domaine sont fonctionnels et que ce capteur Azure ATP peut les utiliser pour ouvrir des connexions LDAP.|Moyenne|

## <a name="some-forwarded-events-could-not-be-analyzed"></a>Certains événements transférés n’ont pas pu être analysés

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le capteur Azure ATP reçoit plus d’événements que ce qu’il ne peut traiter.|Certains événements transférés n’ont pas pu être analysés, ce qui peut impacter la capacité à détecter les activités suspectes provenant des contrôleurs de domaine supervisés par ce capteur Azure ATP.|Vérifiez que seuls les événements nécessaires sont transférés vers le capteur Azure ATP ou essayez de transférer certains des événements vers un autre capteur Azure ATP.|Moyenne|

## <a name="some-network-traffic-could-not-be-analyzed"></a>Une partie du trafic réseau n’a pas pu être analysée

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le capteur Azure ATP reçoit plus de trafic réseau que ce qu’il ne peut traiter.|Une partie du trafic réseau n’a pas pu être analysée, ce qui peut impacter la capacité à détecter les activités suspectes provenant des contrôleurs de domaine supervisés par ce capteur Azure ATP.|Envisagez [d’ajouter des processeurs et de la mémoire](atp-capacity-planning.md) selon les besoins. S’il s’agit d’un capteur Azure ATP autonome, réduisez le nombre de contrôleurs de domaine surveillés.<br></br>Cela peut également se produire si vous utilisez des contrôleurs de domaine sur des machines virtuelles VMware. Pour éviter ces alertes, vous pouvez vérifier que les paramètres suivants sont définis sur 0 ou sont désactivés dans la machine virtuelle :<br></br>- TsoEnable<br></br>- LargeSendOffload(IPv4)<br></br>- IPv4 TSO Offload<br></br>Pensez aussi à désactiver IPv4 Giant TSO Offload. Pour plus d’informations, voir la documentation VMware.|Moyenne|

## <a name="some-windows-events-could-not-be-analyzed"></a>Certains événements Windows n’ont pas pu être analysés

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
|Le capteur Azure ATP reçoit plus d’événements du suivi d’événements pour Windows (ETW) que ce qu’il peut traiter.|Certains événements du suivi d’événements pour Windows (ETW) n’ont pas pu être analysés, ce qui peut impacter la capacité à détecter les activités suspectes provenant des contrôleurs de domaine supervisés par ce capteur Azure ATP.|Vérifiez que seuls les événements nécessaires sont transférés vers le capteur Azure ATP ou essayez de transférer certains des événements vers un autre capteur Azure ATP.|Moyenne|

## <a name="windows-events-missing-from-domain-controller-audit-policy"></a>Événements Windows absents de la stratégie d’audit du contrôleur de domaine

|Alerte|Description|Résolution|Gravité|
|----|----|----|----|
| Événements Windows absents de la stratégie d’audit du contrôleur de domaine|Pour auditer les bons événements et les inclure dans le journal des événements Windows, la stratégie d’audit avancée de vos contrôleurs de domaine doit être correctement configurée. Une configuration incorrecte exclurait certains événements critiques de vos journaux, entraînant une couverture Azure ATP incomplète.|Examinez votre [stratégie d’audit avancée](atp-advanced-audit-policy.md) et modifiez-la si nécessaire. | Moyenne|

## <a name="see-also"></a>Voir aussi

- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
