---
title: Configurer Microsoft Defender pour les paramètres de capteur d’identité conceptuel
description: L’étape 5 de l’installation de Microsoft Defender for Identity vous aide à configurer les paramètres de votre Defender pour le capteur autonome d’identité.
ms.date: 09/15/2019
ms.topic: how-to
ms.openlocfilehash: 329bfd4f6de2e15865c81d22651e833a63d07b6d
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543108"
---
# <a name="configure-product-long-sensor-settings"></a>Configurer les [!INCLUDE [Product long](includes/product-long.md)] paramètres du capteur

Dans cet article, vous allez apprendre à configurer correctement les [!INCLUDE [Product long](includes/product-long.md)] paramètres de capteur pour commencer à afficher les données. Vous devez effectuer une configuration et une intégration supplémentaires pour tirer parti des [!INCLUDE [Product short](includes/product-short.md)] fonctionnalités complètes de.

## <a name="prerequisites"></a>Prérequis

- Une [instance [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md) qui est [connectée à Active Directory](install-step2.md).
- Une copie téléchargée de votre [package d’installation du capteur [!INCLUDE [Product short](includes/product-short.md)]](install-step3.md) et la clé d’accès.

## <a name="configure-sensor-settings"></a>Configurer les paramètres du capteur

Une fois le [!INCLUDE [Product short](includes/product-short.md)] capteur installé, procédez comme suit pour configurer les [!INCLUDE [Product short](includes/product-short.md)] paramètres du capteur.

1. Cliquez sur **lancer** pour ouvrir votre navigateur et vous connecter au [!INCLUDE [Product short](includes/product-short.md)] portail.

1. Dans le [!INCLUDE [Product short](includes/product-short.md)] portail, accédez à **configuration** et, sous **système**, sélectionnez **capteurs**.

    ![Page Capteur](media/sensor-config.png)

1. Cliquez sur le capteur que vous voulez configurer et entrez les informations suivantes :

    ![Configurer les paramètres du capteur](media/sensor-config-2.png)

    - **Description**: entrez une description pour le [!INCLUDE [Product short](includes/product-short.md)] capteur (facultatif).
    - **Contrôleurs de domaine (FQDN)** (requis pour le [!INCLUDE [Product short](includes/product-short.md)] capteur autonome, il ne peut pas être modifié pour le [!INCLUDE [Product short](includes/product-short.md)] capteur) : entrez le nom de domaine complet de votre contrôleur de domaine, puis cliquez sur le signe plus (+) pour l’ajouter à la liste. Par exemple, **dc01.contoso.com**.

    Les informations suivantes s’appliquent aux serveurs que vous entrez dans la liste **Contrôleurs de domaine** :
    - Tous les contrôleurs de domaine dont le trafic est surveillé via la mise en miroir des ports par le [!INCLUDE [Product short](includes/product-short.md)] capteur autonome doivent être répertoriés dans la liste **contrôleurs de domaine** . Si un contrôleur de domaine ne figure pas dans la liste **Contrôleurs de domaine**, il est possible que la détection des activités suspectes ne fonctionne pas comme prévu.
    - Au moins un contrôleur de domaine figurant dans la liste doit être un catalogue général. Cela permet [!INCLUDE [Product short](includes/product-short.md)] à de résoudre les objets ordinateur et utilisateur dans d’autres domaines de la forêt.

    - **Adaptateurs de réseau de capture** (obligatoire) :

    - Pour [!INCLUDE [Product short](includes/product-short.md)] les capteurs, toutes les cartes réseau utilisées pour la communication avec les autres ordinateurs de votre organisation.
    - Pour le [!INCLUDE [Product short](includes/product-short.md)] capteur autonome sur un serveur dédié, sélectionnez les cartes réseau qui sont configurées en tant que port miroir de destination. Ces cartes réseau reçoivent le trafic du contrôleur de domaine mis en miroir.

1. Cliquez sur **Save**.

## <a name="validate-installations"></a>Valider les installations

Pour vérifier que le [!INCLUDE [Product short](includes/product-short.md)] capteur a été correctement déployé, vérifiez les points suivants :

1. Vérifiez que le service nommé **Capteur Azure Advanced Threat Protection** est en cours d’exécution. Une fois que vous avez enregistré les [!INCLUDE [Product short](includes/product-short.md)] paramètres du capteur, le démarrage du service peut prendre quelques secondes.

1. Si le service ne démarre pas, examinez le fichier « Microsoft.Tri.sensor-Errors.log » qui se trouve dans le dossier par défaut suivant : « %programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs ».

    >[!NOTE]
    > La version des [!INCLUDE [Product short](includes/product-short.md)] mises à jour fréquemment, pour vérifier la version la plus récente, dans le [!INCLUDE [Product short](includes/product-short.md)] portail, accédez à **configuration** , puis **à propos** de.

1. Accédez à l' [!INCLUDE [Product short](includes/product-short.md)] URL de votre instance. Dans le [!INCLUDE [Product short](includes/product-short.md)] portail, recherchez un objet dans la barre de recherche, tel qu’un utilisateur ou un groupe sur votre domaine.

1. Vérifiez [!INCLUDE [Product short](includes/product-short.md)] la connectivité sur tout périphérique de domaine en procédant comme suit :
    1. Ouvrez une invite de commandes
    1. Tapez `nslookup`
    1. Tapez **Server** , puis le nom de domaine complet ou l’adresse IP du contrôleur de domaine sur lequel le [!INCLUDE [Product short](includes/product-short.md)] capteur est installé. Par exemple : `server contosodc.contoso.azure`
        - Veillez à remplacer ContosoDC. contoso. Azure et contoso. Azure par le nom de domaine complet (FQDN) de votre [!INCLUDE [Product short](includes/product-short.md)] capteur et de votre nom de domaine, respectivement.
    1. Tapez `ls -d contoso.azure`
    1. Répétez les étapes 3 et 4 pour chaque capteur que vous souhaitez tester.
    1. À partir de la [!INCLUDE [Product short](includes/product-short.md)] console, ouvrez le profil d’entité de l’ordinateur à partir duquel vous avez exécuté le test de connectivité.
    1. Vérifiez l’activité logique associée et confirmez la.

    > [!NOTE]
    >Si le contrôleur de domaine que vous souhaitez tester est votre premier capteur déployé, attendez au moins 15 minutes pour autoriser la base de données principale à terminer le déploiement initial des microservices nécessaires avant d’essayer de vérifier l’activité logique associée pour ce contrôleur de domaine.

## <a name="next-steps"></a>Étapes suivantes

- [Configuration du proxy](configure-proxy.md)
- [Stratégie d’audit avancée](configure-windows-event-collection.md)
- [Configuration de [!INCLUDE [Product short](includes/product-short.md)] pour effectuer des appels distants à SAM](install-step8-samr.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter de [!INCLUDE [Product short](includes/product-short.md)] et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity) !
