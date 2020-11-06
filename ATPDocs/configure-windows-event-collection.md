---
title: Configuration de la collecte d’événements Windows Microsoft Defender pour Identity
description: Cette étape de l’installation de Microsoft Defender pour Identity consiste à configurer la collecte d’événements Windows.
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
ms.openlocfilehash: 4dfaba62df29bb97009bad2440bb420f2c1477e9
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93276554"
---
# <a name="configure-windows-event-collection"></a>Configurer la collecte d’événements Windows

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

La détection [!INCLUDE [Product long](includes/product-long.md)] s’appuie sur certaines entrées du journal des événements Windows pour améliorer les détections et fournir des informations supplémentaires sur les auteurs d’actions spécifiques (par exemple, ouverture de sessions NTLM, modification de groupes de sécurité et autres événements similaires). Pour auditer les bons événements et les inclure dans le journal des événements Windows, la stratégie d’audit avancée de vos contrôleurs de domaine doit être correctement configurée. Des paramètres incorrects de stratégie d’audit avancé peuvent empêcher l’enregistrement des événements nécessaires dans le journal des événements et aboutir à une couverture incomplète de [!INCLUDE [Product short](includes/product-short.md)].

Les événements Windows suivants doivent être [configurés](#configure-audit-policies) et [collectés](#configure-event-collection) par [!INCLUDE [Product short](includes/product-short.md)] pour améliorer les fonctionnalités de détection des menaces :

- 4726 - Compte d’utilisateur supprimé
- 4728 - Membre ajouté au groupe de sécurité global
- 4729 - Membre supprimé du groupe de sécurité global
- 4730 - Groupe de sécurité global supprimé
- 4732 - Membre ajouté au groupe de sécurité local
- 4733 - Membre supprimé du groupe de sécurité global
- 4743 - Compte d’ordinateur supprimé
- 4753 - Groupe de distribution global supprimé
- 4756 - Membre ajouté au groupe de sécurité universel
- 4757 - Membre supprimé du groupe de sécurité universel
- 4758 - Groupe de sécurité universel supprimé
- 4763 - Groupe de distribution universel supprimé
- 4776 - Le contrôleur de domaine a tenté de valider les informations d’identification d’un compte (NTLM)
- 7045 - Nouveau service installé
- 8004 - Authentification NTLM

## <a name="configure-audit-policies"></a>Configurer les stratégies d’audit

Suivez les instructions ci-après pour modifier les stratégies d’audit avancées de votre contrôleur de domaine :

1. Connectez-vous au serveur en tant **qu’administrateur de domaine**.
1. Chargez l’Éditeur de gestion des stratégies de groupe. Pour cela, accédez à **Gestionnaire de serveur** > **Outils** > **Gestion des stratégies de groupe**.
1. Développez l’unité d’organisation **Contrôleurs de domaine** , cliquez avec le bouton droit sur **Stratégie Contrôleurs de domaine par défaut** , puis sélectionnez **Modifier**.

    > [!NOTE]
    > Pour définir ces stratégies, vous pouvez utiliser la stratégie des contrôleurs de domaine par défaut ou un objet de stratégie de groupe dédié.

    ![Modifier la stratégie de contrôleur de domaine](media/advanced-audit-policy-check-step-1.png)

1. À partir de la fenêtre qui s’ouvre, accédez à **Configuration ordinateur** > **Stratégies** > **Paramètres Windows** > **Paramètres de sécurité** , puis, selon la stratégie que vous souhaitez activer, effectuez les étapes suivantes :

    **Pour la configuration avancée de la stratégie d’audit**

    1. Accédez à **Configuration avancée de la stratégie d’audit** > **Stratégies d’audit**.
        ![Configuration de la stratégie d’audit avancée](media/advanced-audit-policy-check-step-2.png)
    1. Sous **Stratégies d’audit** , modifiez chacune des stratégies suivantes, puis sélectionnez **Configurer les événements d’audit suivants** pour les événements des catégories **Réussite** et **Échec**.

        | Stratégie d’audit | Sous-catégorie | Déclenche les ID d’événement |
        | --- |---|---|
        | Connexion de compte | Auditer la validation des informations d’identification | 4776 |
        | Gestion de compte | Auditer la gestion des comptes d’ordinateur | 4743 |
        | Gestion de compte | Auditer la gestion des groupes de distribution | 4753, 4763 |
        | Gestion de compte | Auditer la gestion des groupes de sécurité | 4728, 4729, 4730, 4732, 4733, 4756, 4757, 4758 |
        | Gestion de compte | Auditer la gestion des comptes d’utilisateurs | 4726 |
        | Système | Auditer l’extension du système de sécurité | 7045 |

        Par exemple, pour configurer **Auditer la gestion des groupes de sécurité** , sous **Gestion de compte** , double-cliquez sur **Auditer la gestion des groupes de sécurité** , puis sélectionnez **Configurer les événements d’audit suivants** pour les événements des catégories **Réussite** et **Échec**.

        ![Auditer la gestion des groupes de sécurité](media/advanced-audit-policy-check-step-4.png)

    <a name="ntlm-authentication-using-windows-event-8004"></a> **Pour les stratégies locales (ID d’événement : 8004)**

    > [!NOTE]
    >
    > - Les stratégies de groupe de domaine pour collecter l'événement Windows 8004 doivent être appliquées **uniquement** à des contrôleurs de domaine.
    > - Lorsque l’événement Windows 8004 est analysé par le capteur [!INCLUDE [Product short](includes/product-short.md)], les activités d’authentification NTLM [!INCLUDE [Product short](includes/product-short.md)] sont enrichies avec les données auxquelles le serveur a accédé.

    1. Accédez à **Stratégies locales** > **Options de sécurité**.
    1. Sous **Options de sécurité** , configurez les stratégies de sécurité spécifiées de la façon suivante :

        | Paramètre de stratégie de sécurité | Valeur |
        |---|---|
        | Sécurité réseau : restreindre NTLM : trafic NTLM sortant vers des serveurs distants | Auditer tout |
        | Sécurité réseau : restreindre NTLM : auditer l’authentification NTLM dans ce domaine | Activer tout |
        | Sécurité réseau : Restreindre NTLM : Auditer le trafic NTLM entrant | Activer l’audit de tous les comptes |

        Par exemple, pour configurer **Trafic NTLM sortant vers des serveurs distants** , sous **Options de sécurité** , double-cliquez sur **Sécurité réseau : Restreindre NTLM : Trafic NTLM sortant vers des serveurs distants** , puis sélectionnez **Auditer tout**.

        ![Auditer le trafic NTLM sortant vers des serveurs distants](media/advanced-audit-policy-check-step-3.png)

    > [!NOTE]
    > Si vous choisissez d’utiliser une stratégie de sécurité locale au lieu d’utiliser une stratégie de groupe, veillez à ajouter les journaux d’audit **Connexion de compte** , **Gestion de compte** et **Options de sécurité** à votre stratégie locale. Si vous configurez la stratégie d’audit avancée, vous devez forcer la [sous-catégorie de stratégie d’audit](/windows/security/threat-protection/security-policy-settings/audit-force-audit-policy-subcategory-settings-to-override).

1. Après application au moyen d’un objet GPO, les nouveaux événements sont visibles sous vos **journaux d’événements Windows**.

<!--
## [!INCLUDE [Product short](includes/product-short.md)] Advanced Audit Policy check

To make it easier to verify the current status of each of your domain controller's Advanced Audit Policies, [!INCLUDE [Product short](includes/product-short.md)] automatically checks your existing Advanced Audit Policies and issues health alerts for policy settings that require modification. Each health alert provides specific details of the domain controller, the problematic policy as well as remediation suggestions.

![Advanced Audit Policy Health Alert](media/health-alert-audit.png)

Advanced Security Audit Policy is enabled via **Default Domain Controllers Policy** GPO. These audit events are recorded on the domain controller's Windows Events.
-->

## <a name="configure-event-collection"></a>Configurer la collecte d’événements

Ces événements peuvent être collectés automatiquement par le capteur [!INCLUDE [Product short](includes/product-short.md)] ou, si celui-ci n’est pas déployé, transférés au capteur autonome [!INCLUDE [Product short](includes/product-short.md)] de plusieurs manières :

- [Configurer le capteur autonome [!INCLUDE [Product short](includes/product-short.md)]](configure-event-forwarding.md) de façon à écouter les événements SIEM
- [Configurer les transferts d’événements Windows](configure-event-forwarding.md)

> [!NOTE]
>
> - Les capteurs autonomes [!INCLUDE [Product short](includes/product-short.md)] ne prennent pas en charge la collecte d’entrées de journal du Suivi d’événements pour Windows (ETW) qui fournissent les données pour de nombreuses détections. Pour une couverture complète de votre environnement, nous vous recommandons de déployer le capteur [!INCLUDE [Product short](includes/product-short.md)].
> - Il est important d’évaluer et de vérifier vos [stratégies d’audit]() avant d’activer la collecte d’événements, pour vérifier que les contrôleurs de domaine sont correctement configurés pour enregistrer les événements nécessaires.

## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/aatpsizingtool)
- [Prérequis de [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Informations de référence sur les journaux SIEM [!INCLUDE [Product short](includes/product-short.md)]](cef-format-sa.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
