---
title: Présentation et utilisation des chemins de mouvement latéral avec Microsoft Defender pour Identity
description: Cet article décrit les chemins de mouvement latéral potentiels de Microsoft Defender pour Identity.
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
ms.openlocfilehash: d6d8706e750ed7db841ea9483af8eb86f15b857c
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848888"
---
# <a name="product-long-lateral-movement-paths-lmps"></a>Chemins de mouvement latéral [!INCLUDE [Product long](includes/product-long.md)]

> [!NOTE]
> Les fonctionnalités [!INCLUDE [Product long](includes/product-long.md)] décrites sur cette page sont également accessibles sur le nouveau [portail](https://portal.cloudappsecurity.com).

On parle de mouvement latéral quand un attaquant utilise des comptes non sensibles pour obtenir l’accès à des comptes sensibles dans votre réseau. Les attaquants utilisent le mouvement latéral pour identifier et obtenir l’accès à des ordinateurs et des comptes sensibles de votre réseau, qui partagent des informations d’identification stockées dans des comptes, des groupes et des ordinateurs. Une fois qu’un attaquant réussit à faire des mouvements latéraux jusqu’à vos cibles clés, il peut également tirer parti de vos contrôleurs de domaine et y accéder. Les attaques par mouvements latéraux sont effectuées selon la plupart des méthodes décrites dans le [Guide des activités suspectes](suspicious-activity-guide.md).

Les chemins de mouvement latéral constituent l’un des composants clés des insights de sécurité de [!INCLUDE [Product long](includes/product-long.md)]. Il s’agit de repères visuels qui aident à comprendre et à identifier précisément et rapidement comment les attaquants peuvent se déplacer latéralement au sein du réseau. L’objectif des mouvements latéraux au sein de la chaîne de destruction des cyber-attaques est pour les attaquants d’accéder et de compromettre vos comptes sensibles en utilisant des comptes non sensibles. La compromission de vos comptes sensibles leur permet de se rapprocher de leur objectif ultime, le contrôle du domaine. Pour empêcher ces attaques de réussir, les chemins de mouvement latéral de [!INCLUDE [Product short](includes/product-short.md)] vous apportent une aide visuelle directe et facile à interpréter sur vos comptes les plus vulnérables et les plus sensibles. Ils vous aident à atténuer et à prévenir ces risques, ainsi qu’à barrer l’accès aux attaquants avant qu’ils prennent le contrôle total du domaine.

![Chemin de mouvement latéral [!INCLUDE [Product short](includes/product-short.md)]](media/lmp.png)

Les attaques par mouvements latéraux sont généralement effectuées selon différentes techniques. Certaines des méthodes les plus répandues utilisées par les attaquants sont le vol d’informations d’identification et Pass-the-Ticket. Dans les deux méthodes, vos comptes non sensibles sont utilisés pour des mouvements latéraux par les attaquants, qui exploitent des ordinateurs non sensibles partageant avec des comptes sensibles des informations d’identification stockées dans des comptes, des groupes et des ordinateurs.

## <a name="where-can-i-find-product-short-lmps"></a>Emplacement des chemins de mouvement latéral [!INCLUDE [Product short](includes/product-short.md)]

Chaque ordinateur ou profil d’utilisateur dont [!INCLUDE [Product short](includes/product-short.md)] a détecté qu’il se trouve dans un chemin de mouvement latéral comporte un onglet **Chemins de mouvement latéral**. Les ordinateurs et les profils sans cet onglet n’ont jamais été découverts dans un chemin de mouvement latéral potentiel.

![Onglet Chemin de mouvement latéral [!INCLUDE [Product short](includes/product-short.md)]](media/lateral-movement-path-tab.png)

Le chemin de mouvement latéral pour chaque entité fournit des informations différentes selon la sensibilité de l’entité :

- Utilisateurs sensibles : les chemins de mouvement latéral potentiels conduisant à cet utilisateur sont montrés.
- Utilisateurs et ordinateurs non sensibles : les chemins de mouvement latéral potentiels auxquels l’entité est associée sont montrés.

Chaque fois que l’utilisateur clique sur l’onglet, [!INCLUDE [Product short](includes/product-short.md)] affiche le dernier chemin de mouvement latéral découvert. Chaque chemin de mouvement latéral potentiel est enregistré pendant les 48 heures suivant la découverte. Un historique des chemins de mouvement latéral est disponible. Visualisez les chemins de mouvement latéral plus anciens qui ont été découverts par le passé en cliquant sur **Afficher une autre date**.

![Affichage Chemin de mouvement latéral [!INCLUDE [Product short](includes/product-short.md)]](media/lmp-complete.png)

Découvrez quand des chemins de mouvement latéral potentiels ont été identifiés et quelles entités connexes sont potentiellement concernées.

## <a name="lmp-discovery"></a>Découverte de chemins de mouvement latéral

Sous l’onglet Activités, une indication est donnée quand un nouveau chemin de mouvement latéral potentiel a été identifié :

- Utilisateurs sensibles : quand un nouveau chemin vers un utilisateur sensible est identifié

![Chemin de mouvement latéral [!INCLUDE [Product short](includes/product-short.md)] sensible identifié](media/lmp-activities.png)

- Utilisateurs et ordinateurs non sensibles : quand cette entité est identifiée dans un chemin de mouvement latéral potentiel conduisant à un utilisateur sensible.

![Chemin de mouvement latéral [!INCLUDE [Product short](includes/product-short.md)] non sensible identifié](media/lateral-non-sensitive.png)

## <a name="lmp-related-entities"></a>Entités associées à un chemin de mouvement latéral

Un chemin de mouvement latéral peut désormais vous aider directement dans le processus d’investigation. Les listes de preuves des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] indiquent les entités associées impliquées dans chaque chemin de mouvement latéral potentiel. Les listes d’indices aident directement votre équipe chargée de répondre aux questions de sécurité à augmenter ou à diminuer l’importance de l’alerte de sécurité et/ou de l’investigation des entités associées. Par exemple, quand une alerte de Pass-the-Ticket est émise, l’ordinateur source, l’utilisateur compromis et l’ordinateur de destination à partir desquels le ticket volé a été utilisé, font tous partie du chemin de mouvement latéral potentiel conduisant à un utilisateur sensible. L’existence du chemin de mouvement latéral détecté rend l’examen de l’alerte et l’observation de l’utilisateur suspecté encore plus importants qu’empêcher votre adversaire d’effectuer d’autres mouvements latéraux. Des indices traçables sont fournis dans les chemins de mouvement latéral pour vous permettre plus facilement et plus rapidement d’empêcher les attaquants de se déplacer dans votre réseau.

## <a name="lateral-movement-paths-to-sensitive-accounts-report"></a>Rapport Chemins d’accès de mouvement latéral vers les comptes sensibles

Les données sur les chemins de mouvement latéral sont également disponibles dans le [rapport Chemins d’accès de mouvement latéral vers les comptes sensibles](investigate-lateral-movement-path.md). Ce rapport liste les comptes sensibles qui sont exposés via des chemins de mouvement latéral, et il inclut les chemins qui ont été sélectionnés manuellement pour une période de temps spécifique ou qui sont inclus dans la période de temps pour les rapports planifiés.  Personnalisez la plage de dates incluses avec la sélection dans le calendrier.

## <a name="preventative-best-practices"></a>Bonnes pratiques de prévention

Les insights de sécurité ne sont jamais trop tardifs pour empêcher l’attaque suivante et pour remédier aux dommages. Pour cette raison, l’examen d’une attaque, même pendant la phase de prise de contrôle du domaine, constitue un exemple différent, mais important. En règle générale, lors de l’examen d’une alerte de sécurité comme une exécution de code à distance, si l’alerte est un vrai positif, votre contrôleur de domaine peut déjà être compromis. Cependant, les chemins de mouvement latéral donnent des informations sur l’endroit où les attaquants ont obtenu des privilèges et sur le chemin qu’ils ont utilisé dans votre réseau. Utilisés de cette façon, les chemins de mouvement latéral peuvent également donner des insights clés sur la façon d’y remédier.

- La meilleure façon d’empêcher l’exposition à un mouvement latéral au sein de votre organisation consiste à vérifier que les utilisateurs sensibles utilisent leurs informations d’identification d’administrateur seulement lors de la connexion à des ordinateurs où la sécurité est durcie. Dans l’exemple, vérifiez si l’administrateur qui se trouve dans le chemin a réellement besoin d’accéder à l’ordinateur partagé. Si cet accès est nécessaire, vérifiez qu’il se connecte à l’ordinateur partagé avec un nom d’utilisateur et un mot de passe autres que ses informations d’identification d’administration.

- Vérifiez que vos utilisateurs n’ont pas d’autorisations d’administration non nécessaires. Dans l’exemple, vérifiez si tous les membres du groupe partagé ont besoin de droits d’administration sur l’ordinateur exposé.

- Veillez à ce que les utilisateurs n’aient accès qu’aux ressources nécessaires. Dans l’exemple, Ron Harper étend considérablement l’exposition de Nick Cowley. Est-il nécessaire que Ron Harper soit inclus dans le groupe ? Serait-il possible de créer des sous-groupes pour minimiser l’exposition aux mouvements latéraux ?

**Conseil** : Quand aucun risque d’activité de chemin de mouvement latéral n’est détecté pour une entité au cours des dernières 48 heures, choisissez d’**afficher une autre date** et recherchez des chemins de mouvement latéral potentiels antérieurs. Le **rapport des chemins de mouvement latéral vers les utilisateurs sensibles** est toujours disponible si des chemins de mouvement latéral ont été détectés et vous fournit des informations sur les chemins de mouvement latéral potentiels détectés pour les utilisateurs sensibles.

**Conseil** : pour savoir comment configurer vos clients et serveurs de façon à autoriser [!INCLUDE [Product short](includes/product-short.md)] à effectuer les opérations SAM-R nécessaires à la détection des chemins de mouvement latéral, consultez [Configuration de SAM-R](install-step8-samr.md).

## <a name="investigating-lmps"></a>Examen des chemins de mouvement latéral

Pour savoir comment identifier et examiner les chemins de mouvement latéral [!INCLUDE [Product short](includes/product-short.md)], consultez [Examen des chemins de mouvement latéral](investigate-lateral-movement-path.md).

## <a name="see-also"></a>Voir aussi

- [Examen des chemins de mouvement latéral [!INCLUDE [Product short](includes/product-short.md)]](investigate-lateral-movement-path.md)
- [Configuration de [!INCLUDE [Product short](includes/product-short.md)] pour effectuer des appels distants à SAM](install-step8-samr.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
