---
title: Vérification de la stratégie d’audit avancée Azure Advanced Threat Protection | Microsoft Docs
description: Cet article fournit une vue d’ensemble de la vérification de la stratégie d’audit avancée d’Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ab1e8dd9-a6c2-4c68-89d5-343b8ec56142
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9d9294a22d1e3fd1847d42bd376e65fd114b04bf
ms.sourcegitcommit: a2f6b52f66c89b9f2ca7410426b759a0b0de8d31
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/06/2018
ms.locfileid: "52981936"
---
*S'applique à : Azure - Protection avancée contre les menaces*


# <a name="azure-atp-advanced-audit-policy-check"></a>Vérification de la stratégie d’audit avancée Azure ATP

La détection Azure ATP s’appuie sur des journaux d’événements Windows spécifiques pour bénéficier d’une visibilité dans certains scénarios, notamment les ouvertures de session NTLM, les modifications du groupe de sécurité et les événements similaires. Pour auditer les bons événements et les inclure dans le journal des événements Windows, la stratégie d’audit avancée de vos contrôleurs de domaine doit être correctement configurée. Une configuration incorrecte exclurait certains événements critiques de vos journaux, entraînant une couverture Azure ATP incomplète.

Pour faciliter la vérification de l’état actuel de chacune des stratégies d’audit d’avancées de votre contrôleur de domaine, Azure ATP vérifie automatiquement vos stratégies d’audit avancées existantes et émet des alertes d’intégrité si des paramètres de stratégie doivent être modifiés. Chaque alerte d’intégrité fournit des détails spécifiques du contrôleur de domaine, la stratégie problématique ainsi que des suggestions de correction.

![Alerte d’intégrité relative à la stratégie d’audit avancée](media/atp-health-alert-audit-policy.png)


La stratégie d’audit de sécurité avancée peut être activée via l’objet de stratégie de groupe **Contrôleurs de domaine par défaut**. Ces événements d’audit sont enregistrés dans les événements Windows du contrôleur de domaine. 



<br>Suivez les instructions ci-après pour modifier les stratégies d’audit avancées de votre contrôleur de domaine :

1. Connectez-vous au serveur en tant **qu’administrateur de domaine**.
2. Chargez l’Éditeur de gestion des stratégies de groupe. Pour cela, accédez à **Gestionnaire de serveur** > **Outils** > **Gestion des stratégies de groupe**. 
3. Développez l’unité d’organisation **Contrôleurs de domaine**, cliquez avec le bouton droit sur **Stratégie Contrôleurs de domaine par défaut**, puis sélectionnez **Modifier**. 

    ![Modifier la stratégie de contrôleur de domaine](media/atp-advanced-audit-policy-check-step-1.png)

4. Dans la fenêtre qui s’ouvre, accédez à **Configuration ordinateur** > **Stratégies** > **Paramètres Windows** > **Paramètres de sécurité** > **Configuration avancée de la stratégie d’audit**.

    ![Configuration avancée de la stratégie d’audit](media/atp-advanced-audit-policy-check-step-2.png)

5. Accédez au compte d’ouverture de session, double-cliquez sur **Validation des informations d’identification d’audit**, puis sélectionnez **Configurer les événements d’audit suivants** pour les événements de réussite et d’échec. 

    ![Validation des informations d’identification](media/atp-advanced-audit-policy-check-step-3.png)

6. Accédez à Gestion de compte, double-cliquez sur **Auditer la gestion des groupes de sécurité**, puis sélectionnez **Configurer les événements d’audit suivants** pour les événements de réussite et d’échec.

    ![Auditer la gestion des groupes de sécurité](media/atp-advanced-audit-policy-check-step-4.png)

    > [!NOTE]
    > Si vous choisissez d’utiliser une stratégie locale, ajoutez les journaux d’audit **Connexion de compte** et **Gestion de compte** à votre stratégie locale. Si vous configurez la stratégie d’audit avancée, vous devez forcer la [sous-catégorie de stratégie d’audit](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/audit-force-audit-policy-subcategory-settings-to-override).

7. Après application au moyen d’un objet GPO, les nouveaux événements sont visibles sous vos **journaux d’événements Windows**.

## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
