---
title: Problèmes connus dans Azure ATP | Microsoft Docs
description: Décrit les problèmes connus dans Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/15/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: feea1982-ba23-48be-a468-98d2586cf840
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cab7dad8187c79ff1e5068594b972f58bb19040c
ms.sourcegitcommit: 65885bab8e31dd862a4f2ae9028fb31b288d7229
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52157554"
---
*S’applique à : Azure Advanced Threat Protection*

# <a name="azure-atp-known-issues"></a>Problèmes connus dans Azure ATP

Azure ATP présente parfois des limitations de conception ou de fonctionnalité qui peuvent restreindre ou changer la façon dont votre organisation utilise les services Azure ATP. Cet article décrit les problèmes connus de limitations qui n’ont pas encore de solution de contournement connue, ou dont la résolution en cours n’a pas de date de mise à jour déterminée. 

Pour voir les problèmes connus dans Azure ATP et les solutions de contournement existantes, consultez [Dépannage des problèmes connus d’Azure ATP](troubleshooting-atp-known-issues.md). Pour vérifier l’état de votre locataire Azure ATP, accédez au [Centre d’intégrité Azure ATP](atp-health-center.md). 

## <a name="remote-code-execution-attempts-using-remote-powershell-commands-or-scripts-are-not-detected-when-using-windows-server-2016"></a>Les tentatives d’exécution de code à distance avec des scripts ou des commandes PowerShell à distance ne sont pas détectées quand vous utilisez Windows Server 2016
> [!div class="mx-tableFixed"]  
|Problème|État|
|----|----|
|Actuellement, les tentatives d’exécution de code à distance avec des commandes PowerShell à distance ne sont pas détectées sur les machines de capteur exécutant Windows Server 2016. Les détections associées et les alertes résultantes ne sont pas disponibles.|Les ingénieurs cherchent actuellement une solution à ce problème pour ajouter la prise en charge de Windows Server 2016.|

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