---
title: Configurer la collection d’événements Windows dans Azure Advanced Threat Protection | Microsoft Docs
description: Dans cette étape d’installation d’ATP, vous configurez la collection d’événements.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 54a1d8311c0c0a717ad5a205248d366c65fc010a
ms.sourcegitcommit: c625acd3e44a3ba9619638f84264b3b271383e3a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/25/2020
ms.locfileid: "77590520"
---
# <a name="configure-windows-event-collection"></a>Configurer la collecte d’événements Windows

Pour améliorer les capacités de détection de menaces, Azure Advanced Threat Protection (Azure ATP) a besoin des événements Windows suivants : 4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045 et 8004. Ces événements peuvent être lus automatiquement par le capteur Azure ATP ou, si le capteur Azure ATP n’est pas déployé, ils peuvent être transférés au capteur autonome Azure ATP de deux manières : en [configurant le capteur autonome Azure ATP](configure-event-forwarding.md) afin qu’il reste à l’écoute des événements SIEM ou en [configurant les transferts d’événements Windows](configure-event-forwarding.md).

> [!NOTE]
>
> - Les capteurs autonomes Azure ATP ne prennent pas en charge tous les types de sources de données, ce qui entraîne des détections manquées. Pour une couverture complète de votre environnement, nous vous recommandons de déployer le capteur Azure ATP.
> - Il est important d’évaluer et de vérifier vos [stratégies d’audit](atp-advanced-audit-policy.md) avant d’activer la collecte d’événements, pour vérifier que les contrôleurs de domaine sont correctement configurés pour enregistrer les événements nécessaires.

Outre la collecte et l’analyse du trafic réseau à destination et en provenance des contrôleurs de domaine, Azure ATP peut utiliser des événements Windows pour améliorer les détections. Azure ATP utilise les événements Windows 4776 et 8004 pour NTLM, ce qui améliore plusieurs détections, et les événements 4732, 4733, 4728, 4729, 4756, 4757, 7045 et 8004 pour améliorer la détection des modifications de groupes sensibles et la création de services. Vous pouvez recevoir ces événements à partir de votre serveur SIEM ou définir le transfert d’événements Windows à partir de votre contrôleur de domaine. Les événements collectés fournissent à Azure ATP des informations supplémentaires qui ne sont pas accessibles par le biais du trafic réseau du contrôleur de domaine.

> [!NOTE]
> Les stratégies de groupe de domaine pour collecter l'événement Windows 8004 doivent être appliquées **uniquement** à des contrôleurs de domaine.

## <a name="ntlm-authentication-using-windows-event-8004"></a>Authentification NTLM avec l’événement Windows 8004

Pour configurer la collecte d’événements Windows 8004 :

1. Accédez à : Configuration de l’ordinateur\Stratégies\ Paramètres Windows\Paramètres de sécurité\Stratégies locales\Options de sécurité
2. Configurez ou créez une **stratégie de groupe de domaines** appliquée aux contrôleurs de domaine dans chaque domaine comme suit :
   - Sécurité réseau : Restreindre NTLM : Trafic NTLM sortant vers serveurs distants = **Auditer tout**
   - Sécurité réseau : Restreindre NTLM : Auditer l’authentification NTLM dans ce domaine = **Activer tout**
   - Sécurité réseau : Restreindre NTLM : Auditer le trafic NTLM entrant = **Activer l’audit pour tous les comptes**

Lorsque l’événement Windows 8004 est analysé par le capteur Azure ATP, les activités d’authentification NTLM Azure ATP sont enrichies avec les données ayant fait l’objet d’un accès par le serveur.

## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement Azure ATP](https://aka.ms/aatpsizingtool)
- [Informations de référence sur le journal SIEM Azure ATP](cef-format-sa.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
