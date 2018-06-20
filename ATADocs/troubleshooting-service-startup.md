---
title: Résolution des problèmes de démarrage du service Advanced Threat Analytics | Microsoft Docs
description: Décrit comment résoudre les problèmes de démarrage d’ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 87d3f1de8167c1198e6b334826f90df83cc96780
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009266"
---
*S’applique à : Advanced Threat Analytics version 1.9*



# <a name="troubleshooting-service-startup"></a>Résolution des problèmes de démarrage du service

## <a name="troubleshooting-ata-center-service-startup"></a>Résolution des problèmes de démarrage du service Centre ATA

Si votre centre ATA ne démarre pas, effectuez la procédure de dépannage suivante :

1.  Exécutez la commande Windows PowerShell suivante : `Get-Service Pla | Select Status` pour vérifier que le service de compteur de performances est en cours d’exécution. Si ce n’est pas le cas, c’est qu’il s’agit d’un problème de la plateforme, et vous devez faire en sorte que ce service fonctionne à nouveau.
2.  S’il était en cours d’exécution, essayez de le redémarrer et vérifiez si cela résout le problème : `Restart-Service Pla`
3.  Essayez de créer manuellement un nouveau collecteur de données (n’importe quel collecteur fera l’affaire, vous pouvez même collecter par exemple l’utilisation de l’UC de l’ordinateur).
S’il peut démarrer, la plateforme est probablement opérationnelle. Sinon, il s’agit toujours d’un problème de plateforme.

4.  Essayez de recréer manuellement le collecteur de données ATA à l’aide d’une invite de commandes avec élévation de privilèges en exécutant ces commandes :

        sc stop ATACenter
        logman stop "Microsoft ATA Center"
        logman export "Microsoft ATA Center" -xml c:\center.xml
        logman delete "Microsoft ATA Center"
        logman import "Microsoft ATA Center" -xml c:\center.xml
        logman start "Microsoft ATA Center"
        sc start ATACenter

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>Résolution des problèmes de démarrage de la passerelle légère ATA

**Symptôme**

Votre passerelle ATA ne démarre pas et vous obtenez cette erreur :<br></br>
*System.Net.Http.HttpRequestException : Le code d’état de la réponse n’indique pas de réussite : 500 (Erreur interne du serveur)*

**Description**

Cela se produit parce que, dans le cadre du processus d’installation de la passerelle légère, ATA alloue un seuil de processeur qui permet à la passerelle légère d’utiliser le processeur avec une mémoire tampon de 15 %. Si vous avez configuré indépendamment un seuil à l’aide de la clé de Registre : ce conflit empêche la passerelle légère de démarrer. 

**Résolution**

1. Sous les clés de Registre, si vous trouvez une valeur DWORD appelée **Désactiver les compteurs de performances**, vérifiez qu’elle est définie sur **0** : `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance`
 
2. Ensuite, redémarrez le service Pla. La passerelle légère ATA détecte automatiquement le changement et redémarre le service.


## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Planification de la capacité d’ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
