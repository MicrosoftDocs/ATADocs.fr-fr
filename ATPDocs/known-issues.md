---
title: Problèmes connus dans Azure ATP | Microsoft Docs
description: Décrit les problèmes connus dans Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 02/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: feea1982-ba23-48be-a468-98d2586cf840
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 916a7a2b8f9782b66867860cdb7575e0069a30d4
ms.sourcegitcommit: 5e954f2f0cc14e42d68d2575dd1c2ed9eaabe891
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/25/2019
ms.locfileid: "56754359"
---
# <a name="azure-atp-known-issues"></a>Problèmes connus dans Azure ATP

Azure ATP présente parfois des limitations de conception ou de fonctionnalité qui peuvent restreindre ou changer la façon dont votre organisation utilise les services Azure ATP. Cet article décrit les problèmes connus de limitations qui n’ont pas encore de solution de contournement connue, ou dont la résolution en cours n’a pas de date de mise à jour déterminée. 

Pour voir les problèmes connus dans Azure ATP et les solutions de contournement existantes, consultez [Dépannage des problèmes connus d’Azure ATP](troubleshooting-atp-known-issues.md). Pour vérifier l’état de votre locataire Azure ATP, accédez au [Centre d’intégrité Azure ATP](atp-health-center.md). 

## <a name="dns-reconnaissance-alert"></a>Alerte Reconnaissance DNS
> [!div class="mx-tableFixed"] 

|Problème|État|
|----|----|
Le problème de l’alerte de sécurité *Reconnaissance DNS* affecte les clients en émettant des **alertes de reconnaissance DNS** faux positifs à répétition à partir d’un seul ordinateur. Si un pic **d’alertes de reconnaissance DNS** est généré à partir d’un seul ordinateur, fermez ou supprimez ces alertes jusqu’à ce que la mise à jour 2.67 soit déployée afin de résoudre ce problème. | La mise à jour 2.67 résout ce problème.|

## <a name="suspected-brute-force-attack-ldap-security-alert-display"></a>Affichage de l’alerte de sécurité Suspicion d’attaque par force brute (LDAP)
> [!div class="mx-tableFixed"] 

|Problème|État|
|----|----|
L’alerte de sécurité *Suspicion d’attaque par force brute (LDAP)* ne s’affiche pas toujours comme prévu. Dans certains scénarios, la description de l’alerte s’affiche en désordre.| Les ingénieurs cherchent actuellement une solution à ce problème.| 

## <a name="ad-groups-with-more-than-1000-members-have-limited-detail-sync"></a>Les groupes AD contenant plus de 1 000 membres limitent la synchronisation des détails
> [!div class="mx-tableFixed"]  
> 
> |Problème|État|
> |----|----|
> |Azure ATP ne prend pas en charge la synchronisation des détails des entités dans les groupes AD qui contiennent plus de 1 000 membres par groupe. Lors de l’examen des entités dans de tels groupes, certaines entités peuvent ne pas synchroniser ou afficher les détails.|Limitation de conception. Aucune solution connue.|

## <a name="report-downloads-cannot-contain-more-than-100000-entries"></a>Les téléchargements de rapports contenant plus de 100 000 entrées ne sont pas pris en charge
> [!div class="mx-tableFixed"]  
> 
> |Problème|État|
> |----|----|
> |Azure ATP ne prend pas en charge les téléchargements de rapports qui contiennent plus de 100 000 entrées par rapport. Les rapports avec plus de 100 000 entrées ne s’affichent pas intégralement.|Limitation de conception. Aucune solution connue.|

## <a name="closed-issues"></a>Problèmes fermés

Ce groupe de problèmes connus est maintenant fermé. Vérifiez le numéro de version du correctif à titre de référence.   
### <a name="remote-code-execution-attempts-using-remote-powershell-commands-or-scripts-are-not-detected-when-using-windows-server-2016---v257-december-2-2018"></a>Les tentatives d’exécution de code à distance avec des scripts ou des commandes PowerShell à distance ne sont pas détectées quand vous utilisez Windows Server 2016 - v.2.57 (2 décembre 2018)
> [!div class="mx-tableFixed"]  
> 
> |Problème|État|
> |----|----|
> |Actuellement, les tentatives d’exécution de code à distance avec des commandes PowerShell à distance ne sont pas détectées sur les machines de capteur exécutant Windows Server 2016. Les détections associées et les alertes résultantes ne sont pas disponibles.|Les ingénieurs cherchent actuellement une solution à ce problème pour ajouter la prise en charge de Windows Server 2016.|

## <a name="see-also"></a>Voir aussi

- [Dépannage des problèmes connus d’Azure ATP](troubleshooting-atp-known-issues.md)
- [Résolution des problèmes d’Azure ATP à l’aide de journaux](troubleshooting-atp-using-logs.md)
- [Nouveautés dans Azure ATP](atp-whats-new.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
