---
title: "Qu’est-ce qu’Advanced Threat Protection ? (ATP) | Microsoft Docs"
description: "Explique ce qu’est Azure Advanced Threat Protection (ATP) et quels types d’activités suspectes il peut détecter"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5ccac90a171c895ee8b4d5336a125ccd7fa66239
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
---
*S’applique à : Azure Advanced Threat Protection*


# <a name="what-is-azure-advanced-threat-protection"></a>Qu’est-ce qu’Advanced Threat Protection ?
Azure Advanced Threat Protection (ATP) est un service cloud qui vous aide à protéger vos environnements hybrides d’entreprise contre de nombreux types de cyberattaques ciblées avancées et contre les menaces internes.

## <a name="how-azure-atp-works"></a>Fonctionnement d’Azure ATP

Azure ATP s’appuie sur un moteur d’analyse réseau propriétaire pour capturer et analyser le trafic réseau de plusieurs protocoles (comme Kerberos, DNS, RPC, NTLM et d’autres) pour l’authentification, l’autorisation et la collecte d’informations. Ces informations sont collectées par Azure ATP via :

-   Déploiement de capteurs Azure ATP directement sur vos contrôleurs de domaine
-   Mise en miroir des ports des contrôleurs de domaine et des serveurs DNS vers le capteur autonome Azure ATP

Azure ATP prend les informations de plusieurs sources de données, comme les journaux et les événements de votre réseau, pour apprendre le comportement des utilisateurs et d’autres entités de l’organisation, puis générer ainsi un profil de leur comportement.
Azure ATP peut recevoir des événements et des journaux des éléments suivants :

-   Intégration SIEM
-   Windows Event Forwarding (WEF)
-   Directement depuis le collecteur d’événements Windows (pour le capteur)
-   Gestion de comptes RADIUS à partir des réseaux VPN


Pour plus d’informations sur l’architecture Azure ATP, consultez [Architecture Azure ATP](atp-architecture.md).

## <a name="what-does-azure-atp-do"></a>Que fait Azure ATP ?

La technologie Azure ATP détecte des activités suspectes multiples en se focalisant sur plusieurs phases de la chaîne de frappe de cyberattaques, notamment :

-   Reconnaissance, au cours de laquelle les personnes malveillantes vont recueillir des informations sur la façon dont l’environnement est construit, sur les différents assets, et sur les entités qui existent. Elles élaborent généralement leur plan pour les prochaines phases de l’attaque.
-   Cycle de mouvement latéral, pendant lequel un attaquant investit temps et efforts dans la l'élargissement de sa surface d’attaque au sein de votre réseau.
-   Dominance de domaine (persistance), pendant laquelle un attaquant capture les informations lui permettant de reprendre sa campagne à l’aide de différents ensembles de points d’entrée, d’informations d’identification et de techniques. 

Ces phases d’une cyber-attaque sont similaires et prévisibles, quel que soit le type de société visée ou le type d’informations ciblées.
Azure ATP recherche trois principaux types d’attaques : les attaques malveillantes, le comportement anormal, et les risques et problèmes de sécurité.

Les **attaques malveillantes** sont détectées de façon déterministe ainsi que par l’analytique d’un comportement anormal. La liste complète des types d’attaques connus comprend :

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   Faux PAC (MS14-068)
-   Golden Ticket
-   Réplication malveillante
-   Énumération des services d’annuaires
-   Énumération des sessions SMB
-   Reconnaissance DNS
-   Force brute horizontale 
-   Force brute verticale
-   Skeleton Key
-   Protocole inhabituel
-   Passage à une version antérieure du chiffrement
-   Exécution à distance
-   Création de service malveillant


Azure ATP détecte ces activités suspectes et expose les informations dans le portail de l’espace de travail Azure ATP, avec une vue claire précisant qui, quoi, quand et comment. Comme vous pouvez le voir, en surveillant ce tableau de bord simple et convivial, vous êtes averti qu’Azure ATP soupçonne qu’une attaque pass-the-ticket a été tentée sur les ordinateurs Client 1 et Client 2 de votre réseau.

 ![exemple d’écran Azure ATP pour pass-the-ticket](media/pass-the-ticket-sa.png)


Azure ATP détecte également les **risques et problèmes de sécurité**, notamment :

-   Protocoles faibles
-   Vulnérabilités de protocole connues
-   [Chemin de mouvement latéral vers les comptes sensibles](use-case-lateral-movement-path.md)

# <a name="what-threats-does-azure-atp-look-for"></a>Quelles sont les menaces recherchées par Azure ATP ?

Azure ATP fournit une fonctionnalité de détection pour les différentes phases d’une attaque avancée : reconnaissance, compromission des informations d’identification, mouvement latéral, élévation des privilèges, contrôle du domaine, etc. Les attaques avancées et les menaces internes peuvent ainsi être détectées avant de pouvoir causer des dommages pour votre entreprise.

Chaque type de détection correspond à un ensemble d’activités suspectes liées à la phase en question, chacune de ces activités correspondant elle-même à différents types d’attaques possibles.
Les phases de la chaîne de frappe où Azure ATP fournit une détection sont mises en surbrillance dans l’image suivante :

![Focus d’Azure ATP sur l’activité latérale dans la chaîne de frappe des attaques](media/attack-kill-chain-small.jpg)


Pour plus d’informations, consultez [Gestion des activités suspectes](working-with-suspicious-activities.md) et [Guide Azure ATP des activités suspectes](suspicious-activity-guide.md).

## <a name="whats-next"></a>Étapes suivantes

-   Pour plus d’informations sur la façon dont Azure ATP s’intègre à votre réseau, consultez [Architecture Azure ATP](atp-architecture.md)

-   Pour commencer le déploiement d’ATP, consultez [Installer ATP](install-atp-step1.md)


## <a name="see-also"></a>Voir aussi
- [Forum aux questions Azure ATP](atp-technical-faq.md)
- [Consultez le forum ATP !](https://aka.ms/azureatpcommunity)
