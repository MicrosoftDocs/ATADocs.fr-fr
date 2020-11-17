---
title: Mise à jour d’Advanced Threat Analytics vers le Guide de migration 1.9.3
description: Procédure de mise à jour d’ATA vers la version 1.9.3
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/14/2020
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 0148d8b37e116f1b2574fbedacfce6d02e0b88f2
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690820"
---
# <a name="ata-version-193"></a>Version d’ATA 1.9.3

Nous sommes heureux d’annoncer la disponibilité de Microsoft Advanced Threat Analytics 1,9 Update 3.

Cet article décrit les problèmes résolus dans Update 3 of Microsoft Advanced Threat Analytics (ATA) version 1,9. Le numéro de build de cette mise à jour est 1.9.7576.

## <a name="improvements-included-in-this-update"></a>Améliorations incluses dans cette mise à jour

- Mise à niveau de MongoDB vers la version 3.6.18 pour améliorer la prise en charge et les mises à jour de sécurité.
- Les packages BootStrap et jQuery NPM mis à niveau vers la version 3.4.1 pour les mises à jour de sécurité.
- Fonctionnalités d’accessibilité du portail améliorées.
- Préavis accru pour l’expiration du certificat Center à trois mois avant l’expiration (trois semaines auparavant). En outre, la notification fournit désormais une description plus claire de la gravité de l’échec du renouvellement du certificat.
- Amélioration des détails fournis avec les erreurs de vérification des informations d’identification lors du test des connexions des services d’annuaire.
- Le journal des erreurs contient maintenant des informations plus détaillées en cas de problèmes liés aux compteurs de performances.
- Le journal de déploiement contient maintenant des informations plus détaillées sur les problèmes de connexion au cours du déploiement de la passerelle.
- Améliorations générales apportées aux performances.

## <a name="fixed-issues-included-in-this-update"></a>Problèmes résolus dans cette mise à jour

- Résout un problème dans lequel les autorisations du journal de sécurité ne sont pas définies correctement pour certains déploiements.
- Résout un problème dans lequel certaines traductions sont manquantes pour certaines langues.
- Résout un problème dans lequel un message d’erreur peut s’afficher lorsque vous parcourez une page de profil de compte.
- Résout un problème dans lequel certaines fonctionnalités d’accessibilité ne fonctionnent pas correctement.

## <a name="how-to-get-this-update"></a>Comment obtenir cette mise à jour

Les mises à jour pour Microsoft ATA sont disponibles à partir de Microsoft Update ou par téléchargement manuel.

### <a name="microsoft-update"></a>Microsoft Update

Cette mise à jour est disponible sur Microsoft Update. Pour plus d’informations sur la façon d’utiliser Microsoft Update, consultez [Comment obtenir une mise à jour via Windows Update](https://support.microsoft.com/help/3067639).

### <a name="microsoft-download-center"></a>Centre de téléchargement Microsoft

Pour obtenir le package autonome pour cette mise à jour, accédez au site Web du centre de téléchargement Microsoft : [Téléchargez le package ATA 1.9.3 maintenant](https://www.microsoft.com/download/details.aspx?id=56725).

### <a name="prerequisites"></a>Prérequis

Pour installer cette mise à jour, une des versions ATA suivantes doit déjà être installée :

- Mise à jour 2 pour ATA 1,9 (version 1.9.7478)
- Mise à jour 2 pour ATA 1,9 (version 1.9.7475)
- Mise à jour 1 pour ATA 1.9 (version 1.9.7412)
- ATA 1.9 (version 1.9.7312)
- Mise à jour 1 pour ATA 1.8 (version 1.8.6765)
- ATA 1.8 (version 1.8.6645)

### <a name="restart-requirement"></a>Redémarrage requis

Il est possible que vous deviez redémarrer votre ordinateur après avoir appliqué cette mise à jour.

### <a name="update-replacement-information"></a>Mettre à jour les informations de remplacement

Cette mise à jour remplace Update 2 pour ATA 1,9 (version 1.9.7478).

## <a name="see-also"></a>Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Versions d’ATA](ata-versions.md)
