---
title: 'Azure Advanced Threat Protection : évaluations de la posture de sécurité des identités concernant le spouleur d’impression'
description: Cet article propose une vue d’ensemble des rapports d’évaluation de la posture de sécurité fournis par Azure ATP concernant le spouleur d’impression.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1a7d9525-8923-4dae-af51-02a68aa61644
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3f7e6e4ad8c70e25c0b63ea17aaa8f45d4376ef9
ms.sourcegitcommit: b2b40be9ac76237c3d6b2beb06eabd92e0b399c8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87293183"
---
# <a name="security-assessment-domain-controllers-with-print-spooler-service-available"></a>Évaluation de la sécurité : Contrôleurs de domaine avec le service Spouleur d’impression disponible

![Désactiver le service Spouleur d’impression](media/atp-cas-isp-print-spooler-1.png)

## <a name="what-is-the-print-spooler-service"></a>Qu’est-ce que le service **Spouleur d’impression** ?

Le Spouleur d’impression est un service logiciel qui gère les processus d’impression. Il accepte les travaux d’impression des ordinateurs et vérifie que les ressources de l’imprimante sont disponibles. Il planifie également l’ordre dans lequel les travaux d’impression sont envoyés à la file d’attente à l’impression. Au début des ordinateurs personnels, les utilisateurs devaient attendre que les fichiers soient imprimés avant d’effectuer d’autres opérations. Grâce aux spouleurs d’impression modernes, l’impression a désormais un impact minime sur la productivité globale des utilisateurs.

## <a name="what-risks-does-the-print-spooler-service-on-domain-controllers-introduce"></a>Quels sont les risques qu’introduit le service **Spouleur d’impression** sur les contrôleurs de domaine ?

Bien que ce service soit apparemment inoffensif, tout utilisateur authentifié peut se connecter à distance au service Spouleur d’impression d’un contrôleur de domaine et demander la mise à jour des nouveaux travaux d’impression. Un utilisateur peut également demander au contrôleur de domaine d’envoyer la notification au système avec une [délégation sans contrainte](atp-cas-isp-unconstrained-kerberos.md). Ces actions testent la connexion et exposent les informations d’identification du compte d’ordinateur du contrôleur de domaine (le **Spouleur d’impression** appartient à SYSTEM).

En raison du risque d’exposition, les contrôleurs de domaine et les systèmes d’administration Active Directory doivent désactiver le service **Spouleur d’impression** . Pour ce faire, la méthode recommandée consiste à utiliser un objet de stratégie de groupe (GPO).

Bien que cette évaluation de la sécurité se concentre sur les contrôleurs de domaine, tous les serveurs sont potentiellement exposés à ce type d’attaque.

   > [!NOTE]
   > Veillez à examiner vos paramètres de **Spouleur d’impression**, configurations et dépendances avant de désactiver ce service et d’empêcher les flux de travail d’impression actifs.

## <a name="how-do-i-use-this-security-assessment"></a>Comment faire pour utiliser cette évaluation de la sécurité ?

1. Utilisez le tableau du rapport pour découvrir les contrôleurs de domaine sur lesquels le service **Spouleur d’impression** est activé.

    ![Évaluation de la sécurité pour désactiver le service Spouleur d’impression](media/atp-cas-isp-print-spooler-2.png)
1. Prenez les mesures appropriées sur les contrôleurs de domaine à risque et supprimez activement le service Spouleur d’impression : manuellement, par le biais d’un objet de stratégie de groupe ou avec d’autres types de commandes distantes.

## <a name="remediation"></a>Mise à jour

Résolvez ce problème spécifique en désactivant le service de spouleur d’impression sur tous les serveurs qui n’en ont pas besoin.

## <a name="next-steps"></a>Étapes suivantes

- [Filtrage des activités Azure ATP dans Cloud App Security](atp-activities-filtering-mcas.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
