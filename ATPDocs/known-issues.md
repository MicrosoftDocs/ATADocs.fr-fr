---
title: Problèmes connus dans Azure ATP | Microsoft Docs
description: Décrit les problèmes connus dans Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: feea1982-ba23-48be-a468-98d2586cf840
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c1c5aa0359ac0d24d2bf3fc3033986657c3fc897
ms.sourcegitcommit: 2afc1486b40431f442d51a53df06e289796de87e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51561426"
---
*S’applique à : Azure Advanced Threat Protection*

# <a name="azure-atp-known-issues"></a>Problèmes connus dans Azure ATP

Azure ATP présente parfois des limitations de conception ou de fonctionnalité qui peuvent restreindre ou changer la façon dont votre organisation utilise les services Azure ATP. Cet article décrit les problèmes connus de limitations qui n’ont pas encore de solution de contournement connue, ou dont la résolution en cours n’a pas de date de mise à jour déterminée. 

Pour voir les problèmes connus dans Azure ATP et les solutions de contournement existantes, consultez [Dépannage des problèmes connus d’Azure ATP](troubleshooting-atp-known-issues.md). Pour vérifier l’état de votre locataire Azure ATP, accédez au [Centre d’intégrité Azure ATP](atp-health-center.md). 

## <a name="winrm-not-supported-using-windows-server-2016"></a>WinRM ne prend pas en charge Windows Server 2016
> [!div class="mx-tableFixed"]  
|Problème|État|
|----|----|
|WinRM ne prend pas en charge Windows Server 2016. La détection connexe et les alertes qui en résultent (tentatives d’exécution de code à distance) ne sont pas disponibles pour les machines exécutant Windows Server 2016.|Les ingénieurs cherchent actuellement une solution à ce problème pour ajouter la prise en charge de Windows Server 2016.|

## <a name="ad-groups-with-more-than-1000-members-have-limited-detail-sync"></a>Les groupes AD contenant plus de 1 000 membres limitent la synchronisation des détails
> [!div class="mx-tableFixed"]  
|Problème|État|
|----|----|
|Azure ATP ne prend pas en charge la synchronisation des détails des entités dans les groupes AD qui contiennent plus de 1 000 membres par groupe. Lors de l’examen des entités dans de tels groupes, certaines entités peuvent ne pas synchroniser ou afficher les détails.|Limitation de conception. Aucune solution connue.|

## <a name="report-downloads-cannot-contain-more-than-100000-entries"></a>Les téléchargements de rapports contenant plus de 100 000 entrées ne sont pas pris en charge
> [!div class="mx-tableFixed"]  
|Problème|État|
|----|----|
|Azure ATP ne prend pas en charge les téléchargements de rapports qui contiennent plus de 100 000 entrées par rapport. Les rapports avec plus de 100 000 entrées ne s’affichent pas intégralement.|Limitation de conception. Aucune solution connue.|

## <a name="see-also"></a>Voir aussi

- [Dépannage des problèmes connus d’Azure ATP](troubleshooting-atp-known-issues.md)
- [Résolution des problèmes d’Azure ATP à l’aide de journaux](troubleshooting-atp-using-logs.md)
- [Nouveautés dans Azure ATP](atp-whats-new.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)