---
title: Installer Advanced Threat Analytics - Étape 7 | Microsoft Docs
description: Dans cette étape d’installation d’ATA, vous intégrez votre VPN.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 9a01cde1de4a340bca60908f5ff57e4e78efc5ca
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674620"
---
# <a name="install-ata---step-7"></a>Installer ATA - Étape 7

*S’applique à : Advanced Threat Analytics version 1.9*

> [!div class="step-by-step"]
> [« Étape 5](install-ata-step5.md)
> [Étape 8 »](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Étape 7. Intégrer le VPN

Microsoft Advanced Threat Analytics (ATA) version 1.8 peut collecter des informations de gestion de comptes dans les solutions VPN. Lors de la configuration, la page de profil de l’utilisateur contient des informations sur les connexions VPN, comme les adresses IP et les emplacements d’origine des connexions. Elles viennent en complément du processus d’investigation en fournissant des informations supplémentaires sur l’activité des utilisateurs. L’appel pour résoudre une adresse IP externe à un emplacement est anonyme. Aucun identificateur personnel n’est envoyé durant cet appel.

ATA s’intègre avec votre solution VPN en écoutant les événements de gestion de comptes RADIUS transférés aux passerelles ATA. Ce mécanisme est basé sur la gestion de comptes RADIUS standard ([RFC 2866](https://tools.ietf.org/html/rfc2866)) et les fournisseurs VPN suivants sont pris en charge :

-   Microsoft
-   F5
-   Cisco ASA

## <a name="prerequisites"></a>Prérequis

Pour activer l’intégration VPN, veillez à définir les paramètres suivants :

-   Ouvrir le port UDP 1813 sur vos passerelles ATA et vos passerelles légères ATA.

-   Le Centre ATA doit pouvoir accéder à *ti.ata.azure.com* avec HTTPS (port 443) afin d’être en mesure d’interroger l’emplacement des adresses IP entrantes.

L’exemple ci-dessous utilise Microsoft Routing and Remote Access Server (RRAS) pour décrire le processus de configuration VPN.

Si vous utilisez une solution VPN tierce, consultez sa documentation pour obtenir des instructions sur l’activation de la gestion de comptes RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Configurer la gestion de comptes RADIUS sur le système VPN

Effectuez les étapes suivantes sur votre serveur RRAS.
 
1.  Ouvrez la console Routage et accès distant.
2.  Cliquez avec le bouton droit sur le nom du serveur et cliquez sur **Propriétés**.
3.  Sous l’onglet **Sécurité**, sous **Fournisseur de comptes**, sélectionnez **Gestion de comptes RADIUS** et cliquez sur **Configurer**.

    ![Configuration de RADIUS](./media/radius-setup.png)

4.  Dans la fenêtre **Ajouter un serveur RADIUS**, tapez le **Nom du serveur** de la passerelle ATA ou de la passerelle légère ATA la plus proche. Sous **Port**, veillez à configurer la valeur par défaut 1813. Cliquez sur **Modifier** et tapez une nouvelle chaîne secrète partagée de caractères alphanumériques que vous pouvez mémoriser. Vous devez la fournir plus loin dans votre configuration ATA. Cochez la case **Envoyer des messages de comptes RADIUS actifs et inactifs** et cliquez sur **OK** dans toutes les boîtes de dialogue ouvertes.
 
     ![Configuration du VPN](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-ata"></a>Configurer le VPN dans ATA

ATA collecte les données VPN et identifie quand et où les informations d’identification sont utilisées via le VPN, puis intègre ces données dans votre investigation. Vous obtenez ainsi des informations supplémentaires qui vous aideront à étudier les alertes signalées par ATA.

Pour configurer les données VPN dans ATA :

1. Dans la console ATA, ouvrez la page Configuration d’ATA et accédez à **VPN**.
 
   ![Menu de configuration ATA](./media/config-menu.png)

2. Activez **Gestion de comptes Radius** et tapez le **Secret partagé** que vous avez configuré sur votre serveur VPN RRAS. Cliquez ensuite sur **Enregistrer**.
 

  ![Configurer le VPN ATA](./media/vpn.png)


Une fois l’activation effectuée, toutes les passerelles et passerelles légères ATA écoutent le port 1813 pour les événements de gestion de comptes RADIUS. 

Votre configuration est terminée et vous pouvez voir maintenant l’activité VPN dans la page de profil de l’utilisateur :
 
   ![Configuration du VPN](./media/vpn-user.png)

Une fois que la passerelle ATA reçoit les événements VPN et les envoie au Centre ATA pour traitement, celui-ci a besoin d’accéder à *ti.ata.azure.com* avec HTTPS (port 443) pour pouvoir résoudre les adresses IP externes dans les événements VPN de leur emplacement géographique.




> [!div class="step-by-step"]
> [« Étape 6](install-ata-step5.md)
> [Étape 8 »](install-ata-step7.md)



## <a name="related-videos"></a>Vidéos connexes
- [Vue d’ensemble du déploiement ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Sélection du type de passerelle ATA approprié](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Voir aussi
- [Guide de déploiement ATA POC](http://aka.ms/atapoc)
- [Outil de dimensionnement ATA](http://aka.ms/aatpsizingtool)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](ata-prerequisites.md)

