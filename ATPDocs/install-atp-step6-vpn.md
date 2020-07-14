---
title: Installer l’intégration VPN d’Azure Advanced Threat Protection
description: Collectez des informations de gestion des comptes pour Azure ATP en intégrant un VPN.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/05/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9ad0662a0b468bbe67bb8b699b57358c0c512348
ms.sourcegitcommit: 424567ef02d97454e72241837f69fa6a928709ba
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86175736"
---
# <a name="integrate-vpn"></a>Intégrer le VPN

Azure Advanced Threat Protection (ATP) peut collecter des informations de gestion de comptes dans les solutions VPN. Lors de la configuration, la page de profil de l’utilisateur contient des informations sur les connexions VPN, comme les adresses IP et les emplacements d’origine des connexions. Elles viennent en complément du processus d’investigation en fournissant des informations supplémentaires sur l’activité des utilisateurs, ainsi qu’une nouvelle détection pour les connexions VPN anormales. L’appel pour résoudre une adresse IP externe à un emplacement est anonyme. Aucun identificateur personnel n’est envoyé durant cet appel.

Azure ATP s’intègre à votre solution VPN en écoutant les événements de gestion de comptes RADIUS transférés aux capteurs Azure ATP. Ce mécanisme est basé sur la gestion de comptes RADIUS standard ([RFC 2866](https://tools.ietf.org/html/rfc2866)) et les fournisseurs VPN suivants sont pris en charge :

- Microsoft
- F5
- Check Point
- Cisco ASA

## <a name="prerequisites"></a>Prérequis

Pour activer l’intégration VPN, veillez à définir les paramètres suivants :

- Ouvrez le port UDP 1813 sur vos capteurs Azure ATP et/ou vos capteurs autonomes Azure ATP.

> [!NOTE]
> En activant la **Gestion des comptes RADIUS**, le capteur Azure ATP active une stratégie de pare-feu Windows préprovisionnée appelée **Capteur Azure Advanced Threat Protection** pour autoriser la gestion de comptes RADIUS entrante sur le port UDP 1813.

L’exemple ci-dessous utilise Microsoft Routing and Remote Access Server (RRAS) pour décrire le processus de configuration VPN.

Si vous utilisez une solution VPN tierce, consultez sa documentation pour obtenir des instructions sur l’activation de la gestion de comptes RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Configurer la gestion de comptes RADIUS sur le système VPN

Effectuez les étapes suivantes sur votre serveur RRAS.

1. Ouvrez la console Routage et accès distant.
1. Cliquez avec le bouton droit sur le nom du serveur et cliquez sur **Propriétés**.
1. Sous l’onglet **Sécurité**, sous **Fournisseur de comptes**, sélectionnez **Gestion de comptes RADIUS** et cliquez sur **Configurer**.

    ![Configuration de RADIUS](./media/radius-setup.png)

1. Dans la fenêtre **Ajouter un serveur RADIUS**, tapez le **nom du serveur** du capteur Azure ATP le plus proche (disposant d’une connectivité réseau). Pour une disponibilité élevée, vous pouvez ajouter d’autres capteurs Azure ATP en tant que serveurs RADIUS. Sous **Port**, veillez à configurer la valeur par défaut 1813. Cliquez sur **Modifier** et tapez une nouvelle chaîne secrète partagée de caractères alphanumériques. Notez la nouvelle chaîne secrète partagée, car vous en aurez besoin par la suite pour configurer Azure ATP. Cochez la case **Envoyer des messages de comptes RADIUS actifs et inactifs** et cliquez sur **OK** dans toutes les boîtes de dialogue ouvertes.

    ![Configuration du VPN](./media/vpn-set-accounting.png)

### <a name="configure-vpn-in-atp"></a>Configurer le VPN dans ATP

Azure ATP collecte les données des VPN qui vous aident à profiler les emplacements depuis lesquels les ordinateurs se connectent au réseau et à détecter les connexions VPN anormales.

Pour configurer les données VPN dans ATP :

1. Dans le portail Azure ATP, cliquez sur l’icône de configuration (engrenage), puis sur **VPN**.
1. Activez **Gestion de comptes Radius** et tapez le **Secret partagé** que vous avez configuré sur votre serveur VPN RRAS. Cliquez ensuite sur **Enregistrer**.

    ![Configurer le VPN Azure ATP](./media/atp-vpn-radius.png)

Une fois l’activation effectuée, tous les capteurs Azure ATP sont à l’écoute des événements de gestion de comptes RADIUS sur le port 1813 : la configuration de votre est terminée.

 Une fois que le capteur Azure ATP a reçu les événements VPN et les envoie au service cloud Azure ATP en vue de leur traitement, le profil d’entité indique différents emplacements VPN d’accès et les activités figurant dans le profil indiquent les emplacements.

## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement Azure ATP](https://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
