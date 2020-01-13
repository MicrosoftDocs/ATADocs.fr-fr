---
title: Mise à jour d’Advanced Threat Analytics vers la version 1.9.1 - Guide de migration | Microsoft Docs
description: Procédure de mise à jour d’ATA vers la version 1.9.1
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 12/10/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 86566cbb893fc92f87fbd085e5087714d647f646
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75907262"
---
# <a name="ata-version-191"></a>ATA version 1.9.1


Cet article décrit les problèmes résolus dans la mise à jour 1 de Microsoft Advanced Threat Analytics (ATA) version 1.9. Le numéro de build de cette mise à jour est 1.9.7412.

## <a name="fixed-issues-included-in-this-update"></a>Problèmes résolus dans cette mise à jour

- Possibilité de défaillances de la migration entre les versions 1.8 et 1.9 d’ATA pour les bases de données volumineuses.
- Lorsque vous utilisez la dernière version du navigateur Microsoft Edge et que vous changez d’utilisateur, le navigateur peut se bloquer.
- Dans certains scénarios, la page de profil utilisateur ne contient pas d'informations sur les données du répertoire.
- Lorsque vous ajoutez un utilisateur à la liste d’exclusion pour la détection d’un comportement anormal, l’exclusion n’est pas toujours appliquée. 
- Version de base de données MongoDB mise à jour.
- Resynchronisation incohérente après une mise à niveau vers la version 1.9 de toutes les entités Active Directory vers ATA.
- Exportations incohérentes d’activités suspectes vers Microsoft Excel. Défaillance occasionnelle avec génération d’erreurs.  


## <a name="improvements-included-in-this-update"></a>Améliorations incluses dans cette mise à jour
- Modifications requises pour la certification de normes d’accessibilité de Microsoft (MAS).
- Inclut des correctifs de performance et de sécurité supplémentaires.

## <a name="get-this-update"></a>Obtenir cette mise à jour

Les mises à jour pour Microsoft Advanced Threat Analytics version 1.9 sont disponibles sur le site web Microsoft Update ou par téléchargement manuel.

### <a name="microsoft-update"></a>Microsoft Update
Cette mise à jour est disponible sur Microsoft Update. Pour plus d’informations sur la façon d’utiliser Microsoft Update, consultez [Comment obtenir une mise à jour via Windows Update](https://support.microsoft.com/help/3067639).

### <a name="manual-download"></a>Téléchargement manuel
Pour obtenir le package autonome pour cette mise à jour, accédez au site Web du centre de téléchargement Microsoft : [Téléchargez le package ATA 1,9 maintenant](https://www.microsoft.com/en-us/download/details.aspx?id=56725).

### <a name="prerequisites"></a>Configuration requise
Pour installer cette mise à jour, vous devez avoir préalablement installé ATA version 1.9 (1.9.7312), la mise à jour 1 pour ATA version 1.8 (1.8.6765) ou ATA version 1.8 (1.8.6645).

### <a name="restart-requirement"></a>Exigence de redémarrage
Il est possible que vous deviez redémarrer votre ordinateur après avoir appliqué cette mise à jour.

### <a name="update-replacement-information"></a>Mettre à jour les informations de remplacement
Cette mise à jour remplace ATA version 1.9 (1.9.7312).


## <a name="see-also"></a>Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Versions d’ATA](ata-versions.md)
