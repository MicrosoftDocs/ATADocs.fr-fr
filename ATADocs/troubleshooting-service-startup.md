---
title: Résolution des problèmes de démarrage du service Advanced Threat Analytics
description: Décrit comment résoudre les problèmes de démarrage d’ATA
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d4e5dda205aba4737e074853f22659c6e74a98d5
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910738"
---
# <a name="troubleshooting-service-startup"></a>Résolution des problèmes de démarrage du service

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="troubleshooting-ata-center-service-startup"></a>Résolution des problèmes de démarrage du service Centre ATA

Si votre centre ATA ne démarre pas, effectuez la procédure de dépannage suivante :

1. Exécutez la commande Windows PowerShell suivante : `Get-Service Pla | Select Status`
   pour vérifier que le service Compteur de performances est en cours d’exécution. Si ce n’est pas le cas, c’est qu’il s’agit d’un problème de la plateforme, et vous devez faire en sorte que ce service fonctionne à nouveau.
1. S’il était en cours d’exécution, essayez de le redémarrer et vérifiez si le problème est résolu :  `Restart-Service Pla`
1. Essayez de créer manuellement un nouveau collecteur de données (n’importe quel collecteur fera l’affaire, vous pouvez même collecter par exemple l’utilisation de l’UC de l’ordinateur).
S’il peut démarrer, la plateforme est probablement opérationnelle. Sinon, il s’agit toujours d’un problème de plateforme.

1. Essayez de recréer manuellement le collecteur de données ATA à l’aide d’une invite de commandes avec élévation de privilèges en exécutant ces commandes :

```dos
sc stop ATACenter
logman stop "Microsoft ATA Center"
logman export "Microsoft ATA Center" -xml c:\center.xml
logman delete "Microsoft ATA Center"
logman import "Microsoft ATA Center" -xml c:\center.xml
logman start "Microsoft ATA Center"
sc start ATACenter
```

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>Résolution des problèmes de démarrage de la passerelle légère ATA

**Symptôme**

Votre passerelle ATA ne démarre pas et vous obtenez cette erreur :<br></br>
*System.Net.Http.HttpRequestException : Le code d’état de la réponse n’indique pas de réussite : 500 (Erreur interne du serveur)*

**Description**

Cela se produit parce que, dans le cadre du processus d’installation de la passerelle légère, ATA alloue un seuil de processeur qui permet à la passerelle légère d’utiliser le processeur avec une mémoire tampon de 15 %. Si vous avez configuré indépendamment un seuil à l’aide de la clé de Registre : ce conflit empêche la passerelle légère de démarrer. 

**Résolution :**

1. Sous les clés de Registre, s’il existe une valeur DWORD appelée **Désactiver les compteurs de performances** , assurez-vous qu’elle est définie sur **0**:

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance
```

1. Ensuite, redémarrez le service Pla. La passerelle légère ATA détecte automatiquement le changement et redémarre le service.

## <a name="see-also"></a>Voir aussi

- [Configuration requise pour ATA](ata-prerequisites.md)
- [Planification de la capacité ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
