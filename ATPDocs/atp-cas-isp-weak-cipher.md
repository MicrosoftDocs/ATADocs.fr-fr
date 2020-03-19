---
title: 'Azure Advanced Threat Protection : rapport d’évaluation de la posture de sécurité des identités concernant les chiffrements faibles'
description: Cet article propose une vue d’ensemble du rapport d’évaluation de la posture de sécurité des identités fourni par Azure ATP concernant les chiffrements faibles.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: cc82212b-7d25-4ec7-828d-2475ff40d685
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f73edb6278d4b6ddebe13e1ed01f78d66988f392
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79413143"
---
# <a name="security-assessment-weak-cipher-usage"></a>Évaluation de la sécurité : Utilisation de chiffrements faibles


## <a name="what-are-weak-ciphers"></a>Qu’entend-on par « chiffrements faibles » ? 

Le chiffrement s’appuie sur des algorithmes de chiffrement (« ciphers ») pour chiffrer nos données. Citons par exemple RC4 (Rivest Cipher 4, également connu sous le nom de ARC4 ou ARCFOUR qui signifie Alleged RC4). Bien que RC4 soit remarquable en termes de simplicité et de rapidité, sa sécurité peut être compromise en raison de multiples vulnérabilités qui ont été découvertes depuis la version originale. RC4 est particulièrement vulnérable quand le début du flux de clés de sortie n’est pas supprimé ou quand des clés non aléatoires ou associées sont utilisées. 

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Comment faire pour utiliser cette évaluation de la sécurité afin d’améliorer la sécurité de mon organisation ? 

1. Passez en revue l’évaluation de la sécurité concernant l’utilisation de chiffrements faibles. 
    ![Passer en revue l’évaluation de l’utilisation de chiffrements faibles](media/atp-cas-isp-weak-cipher-2.png)
1. Cherchez à savoir pourquoi les clients et les serveurs identifiés utilisent des chiffrements faibles.   
1. Corrigez les problèmes et désactivez l’utilisation de RC4 et/ou d’autres chiffrements faibles (comme DES/3DES). 
1. Pour en savoir plus sur la désactivation de RC4, consultez l’[avis de sécurité Microsoft](https://support.microsoft.com/help/2868725/microsoft-security-advisory-update-for-disabling-rc4). 

## <a name="remediation"></a>Mise à jour

Définissez les clés de Registre suivantes pour désactiver les clients et les serveurs qui utilisent les suites de chiffrement RC4. Une fois cette opération effectuée, tout serveur ou client qui communique avec un autre client ou serveur nécessitant l’utilisation de RC4 peut empêcher l’établissement d’une connexion. Les clients sur lesquels ce paramètre est déployé ne pourront pas se connecter aux sites nécessitant RC4, et les serveurs déployant ce paramètre ne pourront pas traiter les clients nécessitant l’utilisation de RC4.

> [!NOTE]
>Veillez à tester les paramètres suivants dans un environnement contrôlé avant de les activer en production. 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128]   "Enabled"=dword:00000000 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128]   "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128]   "Enabled"=dword:00000000

Pour en savoir plus sur le téléchargement et la mise à jour des modifications du Registre, consultez l’[avis de sécurité Microsoft](https://docs.microsoft.com/security-updates/SecurityAdvisories/2013/2868725).


## <a name="next-steps"></a>Étapes suivantes
- [Filtrage des activités Azure ATP dans Cloud App Security](atp-activities-filtering-mcas.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
