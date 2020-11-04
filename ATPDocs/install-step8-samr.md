---
title: Configurer SAM-R pour activer la détection de chemin de mouvement latéral dans Microsoft Defender pour l’identité
description: Explique comment configurer Microsoft Defender pour l’identité pour effectuer des appels distants à SAM.
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
ms.openlocfilehash: 9e1bfe428a466e4870613798e4af116f27d63647
ms.sourcegitcommit: 218ba562a2a109ff456b011004530f503a4e82c6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2020
ms.locfileid: "93342502"
---
# <a name="configure-product-long-to-make-remote-calls-to-sam"></a>Configurer [!INCLUDE [Product long](includes/product-long.md)] pour effectuer des appels distants à Sam

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[!INCLUDE [Product long](includes/product-long.md)]la détection de [chemin de mouvement latéral](use-case-lateral-movement-path.md) s’appuie sur les requêtes qui identifient les administrateurs locaux sur des ordinateurs spécifiques. Ces requêtes sont exécutées avec le protocole SAM-R, en utilisant le [!INCLUDE [Product short](includes/product-short.md)] compte de service créé lors de l' [!INCLUDE [Product short](includes/product-short.md)] étape d’installation  [2. Connectez-vous à AD](install-step2.md).

## <a name="configure-sam-r-required-permissions"></a>Configurer les autorisations requises SAM-R

Pour vous assurer que les clients et serveurs Windows autorisent votre [!INCLUDE [Product short](includes/product-short.md)] compte à exécuter Sam-R, une modification doit être apportée à **stratégie de groupe** pour ajouter le [!INCLUDE [Product short](includes/product-short.md)] compte de service en plus des comptes configurés figurant dans la stratégie d' **accès réseau** . Veillez à appliquer les stratégies de groupe à tous les ordinateurs **à l’exception des contrôleurs de domaine**.

> [!Note]
> Avant d’appliquer de nouvelles stratégies telles que celle-ci, il est essentiel de vous assurer que votre environnement reste sécurisé et qu’aucun changement n’impacte la compatibilité de votre application. Commencez par activer puis vérifier la compatibilité des changements proposés en mode audit avant de les apporter à votre environnement de production.

1. Recherchez la stratégie :

   - Nom de la stratégie : Accès réseau : Restreindre les clients autorisés à effectuer des appels distants à SAM
   - Emplacement : Configuration de l’ordinateur, Paramètres Windows, Paramètres de sécurité, Stratégies locales, Options de sécurité

    ![Recherchez la stratégie](media/samr-policy-location.png)

1. Ajoutez le [!INCLUDE [Product short](includes/product-short.md)] service à la liste des comptes approuvés en mesure d’effectuer cette action sur vos systèmes Windows modernes.

    ![Ajoutez le service](media/samr-add-service.png)

3. Le **service AATP** (le [!INCLUDE [Product short](includes/product-short.md)] service créé lors de l’installation) dispose désormais des privilèges nécessaires pour exécuter Sam-R dans l’environnement.

Pour plus d’informations sur SAM-R et sur cette stratégie de groupe, voir [Accès réseau : Restreindre les clients autorisés à effectuer des appels distants à SAM](/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).

## <a name="see-also"></a>Voir aussi

- [Examen des attaques par chemin de mouvement latéral [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [Consultez le [!INCLUDE [Product short](includes/product-short.md)] Forum !](https://aka.ms/MDIcommunity)
