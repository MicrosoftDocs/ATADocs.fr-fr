---
title: Installer Microsoft Defender pour l’intégration de l’identité VPN
description: Collectez les informations de comptabilité pour Microsoft Defender pour l’identité en intégrant un VPN.
ms.date: 12/23/2020
ms.topic: how-to
ms.openlocfilehash: 80b4bdf29db05d0c2f42887dacff223b3067ba49
ms.sourcegitcommit: e2b4ad613aa171f604ae526f0cba05fe79f4a8cb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2020
ms.locfileid: "97753403"
---
# <a name="integrate-vpn"></a>Intégrer le VPN

[!INCLUDE [Product long](includes/product-long.md)] peut collecter des informations de gestion de comptes à partir de solutions VPN. Lors de la configuration, la page de profil de l’utilisateur contient des informations sur les connexions VPN, comme les adresses IP et les emplacements d’origine des connexions. Elles viennent en complément du processus d’investigation en fournissant des informations supplémentaires sur l’activité des utilisateurs, ainsi qu’une nouvelle détection pour les connexions VPN anormales. L’appel pour résoudre une adresse IP externe à un emplacement est anonyme. Aucun identificateur personnel n’est envoyé durant cet appel.

[!INCLUDE [Product short](includes/product-short.md)] s’intègre à votre solution VPN en écoutant les événements de gestion de comptes RADIUS transférés aux [!INCLUDE [Product short](includes/product-short.md)] capteurs. Ce mécanisme est basé sur la gestion de comptes RADIUS standard ([RFC 2866](https://tools.ietf.org/html/rfc2866)) et les fournisseurs VPN suivants sont pris en charge :

- Microsoft
- F5
- Check Point
- Cisco ASA

## <a name="prerequisites"></a>Prérequis

Pour activer l’intégration VPN, veillez à définir les paramètres suivants :

- Ouvrez le port UDP 1813 sur vos [!INCLUDE [Product short](includes/product-short.md)] capteurs et/ou [!INCLUDE [Product short](includes/product-short.md)] capteurs autonomes.

> [!NOTE]
>
> - Si vous activez la **gestion des comptes RADIUS**, le [!INCLUDE [Product short](includes/product-short.md)] capteur active une stratégie de pare-feu Windows préconfigurée appelée **[!INCLUDE [Product long](includes/product-long.md)] capteur** pour autoriser la gestion de comptes RADIUS entrante sur le port UDP 1813.
> - L’intégration VPN n’est pas prise en charge dans les environnements adhérant aux normes FIPS (Federal Information Processing Standards)

L’exemple ci-dessous utilise Microsoft Routing and Remote Access Server (RRAS) pour décrire le processus de configuration VPN.

Si vous utilisez une solution VPN tierce, consultez sa documentation pour obtenir des instructions sur l’activation de la gestion de comptes RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Configurer la gestion de comptes RADIUS sur le système VPN

Effectuez les étapes suivantes sur votre serveur RRAS.

1. Ouvrez la console Routage et accès distant.
1. Cliquez avec le bouton droit sur le nom du serveur et cliquez sur **Propriétés**.
1. Sous l’onglet **Sécurité**, sous **Fournisseur de comptes**, sélectionnez **Gestion de comptes RADIUS** et cliquez sur **Configurer**.

    ![Configuration de RADIUS](media/radius-setup.png)

1. Dans la fenêtre **Ajouter un serveur RADIUS** , tapez le **nom du serveur** du capteur le plus proche [!INCLUDE [Product short](includes/product-short.md)] (qui dispose d’une connectivité réseau). Pour la haute disponibilité, vous pouvez ajouter des [!INCLUDE [Product short](includes/product-short.md)] capteurs supplémentaires en tant que serveurs RADIUS. Sous **Port**, veillez à configurer la valeur par défaut 1813. Cliquez sur **Modifier** et tapez une nouvelle chaîne secrète partagée de caractères alphanumériques. Prenez note de la nouvelle chaîne secrète partagée, car vous devrez la remplir ultérieurement pendant la [!INCLUDE [Product short](includes/product-short.md)] Configuration. Cochez la case **Envoyer des messages de comptes RADIUS actifs et inactifs** et cliquez sur **OK** dans toutes les boîtes de dialogue ouvertes.

    ![Configuration du VPN](media/vpn-set-accounting.png)

### <a name="configure-vpn-in-product-short"></a>Configurer un VPN dans [!INCLUDE [Product short](includes/product-short.md)]

[!INCLUDE [Product short](includes/product-short.md)] collecte des données VPN qui aident à profiler les emplacements à partir desquels les ordinateurs se connectent au réseau et à pouvoir détecter les connexions VPN suspectes.

Pour configurer les données VPN dans [!INCLUDE [Product short](includes/product-short.md)] :

1. Dans le [!INCLUDE [Product short](includes/product-short.md)] portail, cliquez sur le roue dentée de configuration, puis sur **VPN**.
1. Activez **Gestion de comptes Radius** et tapez le **Secret partagé** que vous avez configuré sur votre serveur VPN RRAS. Cliquez ensuite sur **Enregistrer**.

    ![Configurer [ ! INCLUDe [Product Short] (includes/Product-Short. MD)] VPN](media/vpn-radius.png)

Une fois cette option activée, tous les [!INCLUDE [Product short](includes/product-short.md)] capteurs écoutent le port 1813 pour les événements de gestion des comptes RADIUS et la configuration de votre VPN est terminée.

 Une fois que le [!INCLUDE [Product short](includes/product-short.md)] capteur reçoit les événements VPN et les envoie au [!INCLUDE [Product short](includes/product-short.md)] service Cloud en vue de leur traitement, le profil d’entité indique des emplacements et des activités VPN à accès distinct dans le profil qui indiquent des emplacements.

## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis de [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
