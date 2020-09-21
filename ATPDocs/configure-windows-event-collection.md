---
title: Configurer la collection d’événements Windows dans Azure Advanced Threat Protection
description: Dans cette étape d’installation d’ATP, vous configurez la collection d’événements.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/04/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 55e5962ed3d9e9a1a922b47daf46bdb0c2b0d91d
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90826224"
---
# <a name="configure-windows-event-collection"></a>Configurer la collecte d’événements Windows

La détection Azure Advanced Threat Protection (Azure ATP) s’appuie sur certaines entrées du journal des événements Windows pour améliorer certaines détections et fournir des informations supplémentaires sur les personnes qui ont effectué des actions telles qu’une ouverture de session NTLM, une modification des groupes de sécurité, et autres événements similaires. Pour auditer les bons événements et les inclure dans le journal des événements Windows, la stratégie d’audit avancée de vos contrôleurs de domaine doit être correctement configurée. Des paramètres de stratégie d’audit avancés incorrects peuvent empêcher l’enregistrement des événements nécessaires dans le journal des événements, et aboutir à une couverture incomplète d’Azure ATP.

Pour améliorer les fonctionnalités de détection des menaces, Azure ATP a besoin de [configurer](#configure-audit-policies) et de [collecter](#configure-event-collection) les événements Windows suivants :

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
1. Développez l’unité d’organisation **Contrôleurs de domaine**, cliquez avec le bouton droit sur **Stratégie Contrôleurs de domaine par défaut**, puis sélectionnez **Modifier**.

    > [!NOTE]
    > Pour définir ces stratégies, vous pouvez utiliser la stratégie des contrôleurs de domaine par défaut ou un objet de stratégie de groupe dédié.

    ![Modifier la stratégie de contrôleur de domaine](media/atp-advanced-audit-policy-check-step-1.png)

1. À partir de la fenêtre qui s’ouvre, accédez à **Configuration ordinateur** > **Stratégies** > **Paramètres Windows** > **Paramètres de sécurité**, puis, selon la stratégie que vous souhaitez activer, effectuez les étapes suivantes :

    **Pour la configuration avancée de la stratégie d’audit**

    1. Accédez à **Configuration avancée de la stratégie d’audit** > **Stratégies d’audit**.
        ![Configuration de la stratégie d’audit avancée](media/atp-advanced-audit-policy-check-step-2.png)
    1. Sous **Stratégies d’audit**, modifiez chacune des stratégies suivantes, puis sélectionnez **Configurer les événements d’audit suivants** pour les événements des catégories **Réussite** et **Échec**.

        | Stratégie d’audit | Sous-catégorie | Déclenche les ID d’événement |
        | --- |---|---|
        | Connexion de compte | Auditer la validation des informations d’identification | 4776 |
        | Gestion de compte | Auditer la gestion des comptes d’ordinateur | 4743 |
        | Gestion de compte | Auditer la gestion des groupes de distribution | 4753, 4763 |
        | Gestion de compte | Auditer la gestion des groupes de sécurité | 4728, 4729, 4730, 4732, 4733, 4756, 4757, 4758 |
        | Gestion de compte | Auditer la gestion des comptes d’utilisateurs | 4726 |
        | Système | Auditer l’extension du système de sécurité | 7045 |

        Par exemple, pour configurer **Auditer la gestion des groupes de sécurité**, sous **Gestion de compte**, double-cliquez sur **Auditer la gestion des groupes de sécurité**, puis sélectionnez **Configurer les événements d’audit suivants** pour les événements des catégories **Réussite** et **Échec**.

        ![Auditer la gestion des groupes de sécurité](media/atp-advanced-audit-policy-check-step-4.png)

    <a name="ntlm-authentication-using-windows-event-8004"></a> **Pour les stratégies locales (ID d’événement : 8004)**

    > [!NOTE]
    >
    > - Les stratégies de groupe de domaine pour collecter l'événement Windows 8004 doivent être appliquées **uniquement** à des contrôleurs de domaine.
    > - Lorsque l’événement Windows 8004 est analysé par le capteur Azure ATP, les activités d’authentification NTLM Azure ATP sont enrichies avec les données ayant fait l’objet d’un accès par le serveur.

    1. Accédez à **Stratégies locales** > **Options de sécurité**.
    1. Sous **Options de sécurité**, configurez les stratégies de sécurité spécifiées de la façon suivante :

        | Paramètre de stratégie de sécurité | Valeur |
        |---|---|
        | Sécurité réseau : restreindre NTLM : trafic NTLM sortant vers des serveurs distants | Auditer tout |
        | Sécurité réseau : restreindre NTLM : auditer l’authentification NTLM dans ce domaine | Activer tout |
        | Sécurité réseau : Restreindre NTLM : Auditer le trafic NTLM entrant | Activer l’audit de tous les comptes |

        Par exemple, pour configurer **Trafic NTLM sortant vers des serveurs distants**, sous **Options de sécurité**, double-cliquez sur **Sécurité réseau : Restreindre NTLM : Trafic NTLM sortant vers des serveurs distants**, puis sélectionnez **Auditer tout**.

        ![Auditer le trafic NTLM sortant vers des serveurs distants](media/atp-advanced-audit-policy-check-step-3.png)

    > [!NOTE]
    > Si vous choisissez d’utiliser une stratégie de sécurité locale au lieu d’utiliser une stratégie de groupe, veillez à ajouter les journaux d’audit **Connexion de compte**, **Gestion de compte** et **Options de sécurité** à votre stratégie locale. Si vous configurez la stratégie d’audit avancée, vous devez forcer la [sous-catégorie de stratégie d’audit](/windows/security/threat-protection/security-policy-settings/audit-force-audit-policy-subcategory-settings-to-override).

1. Après application au moyen d’un objet GPO, les nouveaux événements sont visibles sous vos **journaux d’événements Windows**.

<!--
## Azure ATP Advanced Audit Policy check

To make it easier to verify the current status of each of your domain controller's Advanced Audit Policies, Azure ATP automatically checks your existing Advanced Audit Policies and issues health alerts for policy settings that require modification. Each health alert provides specific details of the domain controller, the problematic policy as well as remediation suggestions.

![Advanced Audit Policy Health Alert](media/atp-health-alert-audit.png)

Advanced Security Audit Policy is enabled via **Default Domain Controllers Policy** GPO. These audit events are recorded on the domain controller's Windows Events.
-->

## <a name="configure-event-collection"></a>Configurer la collecte d’événements

Ces événements peuvent être collectés automatiquement par le capteur Azure ATP ou, si celui-ci n’est pas déployé, vous pouvez les transférer au capteur autonome Azure ATP de l’une des manières suivantes :

- [Configurer le capteur autonome Azure ATP](configure-event-forwarding.md) pour écouter les événements SIEM
- [Configurer les transferts d’événements Windows](configure-event-forwarding.md)

> [!NOTE]
>
> - Les capteurs autonomes Azure ATP ne prennent pas en charge la collecte d’entrées de journal du Suivi d’événements pour Windows (ETW) qui fournissent les données pour de nombreuses détections. Pour une couverture complète de votre environnement, nous vous recommandons de déployer le capteur Azure ATP.
> - Il est important d’évaluer et de vérifier vos [stratégies d’audit]() avant d’activer la collecte d’événements, pour vérifier que les contrôleurs de domaine sont correctement configurés pour enregistrer les événements nécessaires.

## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement Azure ATP](https://aka.ms/aatpsizingtool)
- [Prérequis d’Azure ATP](prerequisites.md)
- [Informations de référence sur le journal SIEM Azure ATP](cef-format-sa.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)