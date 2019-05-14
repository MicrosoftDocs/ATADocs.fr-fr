---
title: Mise à jour d’Advanced Threat Analytics vers la version 1.9.2 - Guide de migration | Microsoft Docs
description: Procédure de mise à jour d’ATA vers la version 1.9.2
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/02/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 22420ea90bc922684a4e99ad303bba831f3a45e7
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196076"
---
# <a name="ata-version-192"></a>ATA version 1.9.2


Nous sommes heureux d’annoncer la disponibilité de Microsoft Advanced Threat Analytics 1.9 Update 2.

Cet article décrit les problèmes résolus dans la mise à jour 2 de Microsoft Advanced Threat Analytics (ATA) version 1.9. Le numéro de build de cette mise à jour est 1.9.7478.

## <a name="improvements-included-in-this-update"></a>Améliorations incluses dans cette mise à jour

Cette mise à jour inclut Windows Server 2019 (inclut les versions Core mais pas Nano) comme système d’exploitation pris en charge à la fois pour les composants du centre, de la passerelle et de la passerelle légère.

Cette mise à jour inclut également des améliorations au niveau de la stabilité et des performances, ainsi que des correctifs pour les problèmes signalés par les clients.

## <a name="fixed-issues-included-in-this-update"></a>Problèmes résolus dans cette mise à jour

- Résout un problème dans lequel l’écran des données du répertoire affiche les appartenances du gestionnaire direct et les appartenances récursives.
- Résout un problème dans lequel la configuration de l’URL du centre ATA n’affiche pas toujours les adresses IP locales ou le nom de l’ordinateur local.
- Résout un problème de téléchargement des alertes d’intégrité lorsque l’alerte d’intégrité contient une passerelle inexistante.
- Résout des problèmes de traduction.
- Résout un problème dans lequel la version de la base de données MongoDB n’a pas été mise à jour.
- Résout un cas rare dans lequel des problèmes de mémoire élevée se sont produits pendant une synchronisation Active Directory.
- Résout un cas rare dans lequel la console autorisait uniquement la sélection d’un certificat non pris en charge.
- Résout un cas rare dans lequel une instance de faux positif du message « Suspicion d’usurpation d’identité fondée sur un comportement inhabituel » a été reçue.
- Résout un cas rare dans quel un saut de chronologie se produisait quand des alertes étaient automatiquement mises à jour.

## <a name="get-this-update"></a>Obtenir cette mise à jour

Pour obtenir le package autonome pour cette mise à jour, accédez au site web Centre de téléchargement Microsoft : [Télécharger le package ATA 1.9.2 maintenant](https://www.microsoft.com/en-us/download/details.aspx?id=56725).

### <a name="prerequisites"></a>Prérequis

Pour installer cette mise à jour, une des versions ATA suivantes doit déjà être installée : 
- Mise à jour 1 pour ATA 1.9 (version 1.9.7412)
- ATA 1.9 (version 1.9.7312)
- Mise à jour 1 pour ATA 1.8 (version 1.8.6765)
- ATA 1.8 (version 1.8.6645)

### <a name="restart-requirement"></a>Exigence de redémarrage

Il est possible que vous deviez redémarrer votre ordinateur après avoir appliqué cette mise à jour.

### <a name="update-replacement-information"></a>Mettre à jour les informations de remplacement

Cette mise à jour remplace ATA version 1.9.1 (1.9.7412).


## <a name="see-also"></a>Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Versions d’ATA](ata-versions.md)