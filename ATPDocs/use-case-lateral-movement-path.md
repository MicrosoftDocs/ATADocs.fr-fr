---
title: Comprendre et utiliser des chemins de mouvement latéral avec Azure ATP
description: Cet article décrit les chemins de mouvement latéral d’Azure Advanced Threat Protection (ATP).
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e5c422a1315bccce93154c3abbc07caea8de6c06
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84775792"
---
# <a name="azure-atp-lateral-movement-paths-lmps"></a>Chemins de mouvement latéral d’Azure ATP 

> [!NOTE]
> Les fonctionnalités Azure ATP expliquées dans cette page sont également accessibles dans le nouveau [portail](https://portal.cloudappsecurity.com).

On parle de mouvement latéral quand un attaquant utilise des comptes non sensibles pour obtenir l’accès à des comptes sensibles dans votre réseau. Les attaquants utilisent le mouvement latéral pour identifier et obtenir l’accès à des ordinateurs et des comptes sensibles de votre réseau, qui partagent des informations d’identification stockées dans des comptes, des groupes et des ordinateurs. Une fois qu’un attaquant réussit à faire des mouvements latéraux jusqu’à vos cibles clés, il peut également tirer parti de vos contrôleurs de domaine et y accéder. Les attaques par mouvements latéraux sont effectuées selon la plupart des méthodes décrites dans le [Guide des activités suspectes](suspicious-activity-guide.md).

Les chemins de mouvement latéral constituent un composant clé des insights de sécurité d’Azure ATP. Les chemins de mouvement latéral d’Azure ATP sont des repères visuels qui vous aident à comprendre et à identifier rapidement la façon exacte dont les attaquants peuvent se déplacer latéralement à l’intérieur de votre réseau. L’objectif des mouvements latéraux au sein de la chaîne de destruction des cyber-attaques est pour les attaquants d’accéder et de compromettre vos comptes sensibles en utilisant des comptes non sensibles. La compromission de vos comptes sensibles leur permet de se rapprocher de leur objectif ultime, le contrôle du domaine. Pour mettre fin à la réussite de ces attaques, les chemins de mouvement latéral d’Azure ATP vous apportent une aide visuelle directe et facile à interpréter sur vos comptes les plus vulnérables et les plus sensibles. Les chemins de mouvement latéral vous aident à atténuer et à prévenir ces risques dans le futur, et à barrer l’accès aux attaquants avant qu’ils prennent le contrôle total du domaine.

![Chemin de mouvement latéral d’Azure ATP](./media/atp-lmp.png)

Les attaques par mouvements latéraux sont généralement effectuées selon différentes techniques. Certaines des méthodes les plus répandues utilisées par les attaquants sont le vol d’informations d’identification et Pass-the-Ticket. Dans les deux méthodes, vos comptes non sensibles sont utilisés pour des mouvements latéraux par les attaquants, qui exploitent des ordinateurs non sensibles partageant avec des comptes sensibles des informations d’identification stockées dans des comptes, des groupes et des ordinateurs.

## <a name="where-can-i-find-azure-atp-lmps"></a>Où puis-je trouver les chemins de mouvement latéral d’Azure ATP ?

Chaque ordinateur ou profil d’utilisateur découvert par Azure ATP se trouvant dans un chemin de mouvement latéral a un onglet **Chemins d'accès de mouvement latéral**. Les ordinateurs et les profils sans cet onglet n’ont jamais été découverts dans un chemin de mouvement latéral potentiel. 

![Onglet Chemin de mouvement latéral d’Azure ATP](./media/lateral-movement-path-tab.png)

Le chemin de mouvement latéral pour chaque entité fournit des informations différentes selon la sensibilité de l’entité : 
- Utilisateurs sensibles : les chemins de mouvement latéral potentiels conduisant à cet utilisateur sont montrés.
- Utilisateurs et ordinateurs non sensibles : les chemins de mouvement latéral potentiels auxquels l’entité est associée sont montrés. <br>

Chaque fois que l’utilisateur clique sur l’onglet, Azure ATP affiche le chemin de mouvement latéral découvert le plus récemment. Chaque chemin de mouvement latéral potentiel est enregistré pendant les 48 heures suivant la découverte. Un historique des chemins de mouvement latéral est disponible. Visualisez les chemins de mouvement latéral plus anciens qui ont été découverts par le passé en cliquant sur **Afficher une autre date**. 

![Affichage des chemins de mouvement latéral d’Azure ATP](./media/atp-lmp-complete.png)

Découvrez quand des chemins de mouvement latéral potentiels ont été identifiés et quelles entités connexes sont potentiellement concernées. 

## <a name="lmp-discovery"></a>Découverte de chemins de mouvement latéral

Sous l’onglet Activités, une indication est donnée quand un nouveau chemin de mouvement latéral potentiel a été identifié :
- Utilisateurs sensibles : quand un nouveau chemin vers un utilisateur sensible est identifié

![Chemin de mouvement latéral d’Azure ATP : utilisateur sensible identifié](./media/atp-lmp-activities.png)

- Utilisateurs et ordinateurs non sensibles : quand cette entité est identifiée dans un chemin de mouvement latéral potentiel conduisant à un utilisateur sensible.

![Chemin de mouvement latéral d’Azure ATP : utilisateur non sensible identifié](./media/atp-lateral-non-sensitive.png)

## <a name="lmp-related-entities"></a>Entités associées à un chemin de mouvement latéral
Un chemin de mouvement latéral peut désormais vous aider directement dans le processus d’investigation. Les listes d’indices d’alerte de sécurité d’Azure ATP indiquent les entités associées qui sont impliquées dans chaque chemin de mouvement latéral potentiel. Les listes d’indices aident directement votre équipe chargée de répondre aux questions de sécurité à augmenter ou à diminuer l’importance de l’alerte de sécurité et/ou de l’investigation des entités associées. Par exemple, quand une alerte de Pass-the-Ticket est émise, l’ordinateur source, l’utilisateur compromis et l’ordinateur de destination à partir desquels le ticket volé a été utilisé, font tous partie du chemin de mouvement latéral potentiel conduisant à un utilisateur sensible. L’existence du chemin de mouvement latéral détecté rend l’examen de l’alerte et l’observation de l’utilisateur suspecté encore plus importants qu’empêcher votre adversaire d’effectuer d’autres mouvements latéraux. Des indices traçables sont fournis dans les chemins de mouvement latéral pour vous permettre plus facilement et plus rapidement d’empêcher les attaquants de se déplacer dans votre réseau. 

## <a name="lateral-movement-paths-to-sensitive-accounts-report"></a>Rapport Chemins d’accès de mouvement latéral vers les comptes sensibles 
Les données sur les chemins de mouvement latéral sont également disponibles dans le [rapport Chemins d’accès de mouvement latéral vers les comptes sensibles](investigate-lateral-movement-path.md). Ce rapport liste les comptes sensibles qui sont exposés via des chemins de mouvement latéral, et il inclut les chemins qui ont été sélectionnés manuellement pour une période de temps spécifique ou qui sont inclus dans la période de temps pour les rapports planifiés.  Personnalisez la plage de dates incluses avec la sélection dans le calendrier. 

## <a name="preventative-best-practices"></a>Bonnes pratiques de prévention
Les insights de sécurité ne sont jamais trop tardifs pour empêcher l’attaque suivante et pour remédier aux dommages. Pour cette raison, l’examen d’une attaque, même pendant la phase de prise de contrôle du domaine, constitue un exemple différent, mais important. En règle générale, lors de l’examen d’une alerte de sécurité comme une exécution de code à distance, si l’alerte est un vrai positif, votre contrôleur de domaine peut déjà être compromis. Cependant, les chemins de mouvement latéral donnent des informations sur l’endroit où les attaquants ont obtenu des privilèges et sur le chemin qu’ils ont utilisé dans votre réseau. Utilisés de cette façon, les chemins de mouvement latéral peuvent également donner des insights clés sur la façon d’y remédier.  

- La meilleure façon d’empêcher l’exposition à un mouvement latéral au sein de votre organisation consiste à vérifier que les utilisateurs sensibles utilisent leurs informations d’identification d’administrateur seulement lors de la connexion à des ordinateurs où la sécurité est durcie. Dans l’exemple, vérifiez si l’administrateur qui se trouve dans le chemin a réellement besoin d’accéder à l’ordinateur partagé. Si cet accès est nécessaire, vérifiez qu’il se connecte à l’ordinateur partagé avec un nom d’utilisateur et un mot de passe autres que ses informations d’identification d’administrateur.

- Vérifiez que vos utilisateurs n’ont pas d’autorisations d’administration non nécessaires. Dans l’exemple, vérifiez si tous les membres du groupe partagé ont besoin de droits d’administration sur l’ordinateur exposé.

- Veillez à ce que les utilisateurs n’aient accès qu’aux ressources nécessaires. Dans l’exemple, Ron Harper étend considérablement l’exposition de Nick Cowley. Est-il nécessaire que Ron Harper soit inclus dans le groupe ? Serait-il possible de créer des sous-groupes pour minimiser l’exposition aux mouvements latéraux ?

**Conseil** : Quand aucun risque d’activité de chemin de mouvement latéral n’est détecté pour une entité au cours des dernières 48 heures, choisissez d’**afficher une autre date** et recherchez des chemins de mouvement latéral potentiels antérieurs. Le **rapport des chemins de mouvement latéral vers les utilisateurs sensibles** est toujours disponible si des chemins de mouvement latéral ont été détectés et vous fournit des informations sur les chemins de mouvement latéral potentiels détectés pour les utilisateurs sensibles. 

**Conseil** : Pour obtenir des instructions sur la configuration des clients et des serveurs à appliquer pour permettre à Azure ATP d’effectuer les opérations SAM-R nécessaires à la détection des chemins de mouvement latéral, voir [Configurer SAM-R](install-atp-step8-samr.md).


## <a name="investigating-lmps"></a>Examen des chemins de mouvement latéral
Pour obtenir des instructions sur la façon d’identifier et d’examiner les chemins de mouvement latéral d’Azure ATP, consultez [Examiner les chemins de mouvement latéral](investigate-lateral-movement-path.md).


## <a name="see-also"></a>Voir aussi
- [Examen des chemins de mouvement latéral d’Azure ATP](investigate-lateral-movement-path.md)
- [Configurer Azure ATP pour effectuer des appels distants vers SAM](install-atp-step8-samr.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
