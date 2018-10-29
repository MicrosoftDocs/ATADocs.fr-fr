---
title: Dépannage des problèmes connus d’Azure ATP | Microsoft Docs
description: Décrit comment résoudre les problèmes d’Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e65133fdd09f821c633a3095ae419df01da98b16
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783710"
---
*S’applique à : Azure Advanced Threat Protection*


# <a name="troubleshooting-azure-atp-known-issues"></a>Dépannage des problèmes connus d’Azure ATP 


## <a name="deployment-log-location"></a>Emplacement des journaux de déploiement
 
Les journaux de déploiement Azure ATP se trouvent dans le répertoire temp de l’utilisateur qui a installé le produit. À l’emplacement d’installation par défaut, ce répertoire se trouve ici : C:\Users\Administrator\AppData\Local\Temp (ou un répertoire au-dessus de %temp%). Pour plus d'informations, consultez [Résolution des problèmes liés à ATP à l’aide des journaux](troubleshooting-atp-using-logs.md)

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Le problème d’authentification du proxy se présente sous la forme d’erreur de licence

Si vous recevez l’erreur suivante lors de l’installation du capteur : **Impossible d’enregistrer le capteur en raison de problèmes de licence**

Les entrées de journal de déploiement : [1C60:1AA8][2018-03-24T23:59:13]i000: 2018-03-25 02:59:13.1237 Info  InteractiveDeploymentManager ValidateCreateSensorAsync renvoient [\[]validateCreateSensorResult=LicenseInvalid[\]] [1C60:1AA8][2018-03-24T23:59:56]i000: 2018-03-25 02:59:56.4856 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [\[]validateCreateSensorResult=LicenseInvalid[\]] [1C60:1AA8][2018-03-25T00:27:56]i000: 2018-03-25 03:27:56.7399 Debug SensorBootstrapperApplication Engine.Quit [\[]deploymentResultStatus=1602 isRestartRequired=False[\]] [1C60:15B8][2018-03-25T00:27:56]i500: Arrêt, code de  sortie : 0x642


**Cause :**

Dans certains cas, lors de la communication via un proxy, lors de l’authentification, il peut répondre au capteur Azure ATP avec l’erreur 401 ou 403 au lieu de l’erreur 407. Le capteur Azure ATP interprétera l’erreur 401 ou 403 comme un problème de licence et non comme un problème d’authentification du proxy. 

**Résolution :**

Assurez-vous que le capteur peut naviguer vers *.atp.azure.com via le proxy configuré sans authentification. Pour plus d'informations, consultez [Configurer le proxy pour activer la communication](configure-proxy.md).




## Problème d’association de cartes réseau du capteur Azure ATP <a name="nic-teaming"></a>

Si vous essayez d’installer le capteur ATP sur un ordinateur configuré avec une carte d’association de cartes réseau, vous recevez une erreur d’installation. Si vous souhaitez installer le capteur ATP sur une machine configurée avec une association de cartes réseau, suivez ces instructions :

Si vous n’avez pas encore installé le capteur :

1.  Téléchargez Npcap depuis [https://nmap.org/npcap/](https://nmap.org/npcap/).
2.  Désinstallez WinPcap, s’il était installé.
3.  Installez Npcap avec les options suivantes : loopback_support=no & winpcap_mode=yes
4.  Installez le package du capteur.

Si vous avez déjà installé le capteur :

1.  Téléchargez Npcap depuis [https://nmap.org/npcap/](https://nmap.org/npcap/).
2.  Désinstallez le capteur.
3.  Désinstallez WinPcap.
4.  Installez Npcap avec les options suivantes : loopback_support=no & winpcap_mode=yes
5.  Réinstallez le package du capteur.

## <a name="windows-defender-atp-integration-issue"></a>Problème d’intégration Windows Defender ATP

Azure - Protection avancée contre les menaces vous permet d’intégrer Azure ATP et Windows Defender ATP. Pour plus d’informations, consultez [Intégration d’Azure ATP et de Windows Defender ATP](integrate-wd-atp.md). 

## <a name="vmware-virtual-machine-sensor-issue"></a>Problème de capteur pour la machine virtuelle VMware

Si vous avez un capteur Azure ATP sur des machines virtuelles VMware, vous pouvez recevoir l’alerte de surveillance **Une partie du trafic réseau n’est pas analysée**. Ce scénario se produit à cause d’une différence de configuration dans VMware.

Pour résoudre ce problème :

Définissez les paramètres suivants avec les valeurs **0** ou **Désactivé** dans la configuration de carte réseau de la machine virtuelle : TsoEnable, LargeSendOffload, TSO Offload, Giant TSO Offload.
> [!NOTE]
> Pour les capteurs Azure ATP, il vous suffit de désactiver **IPv4 TSO Offload** dans la configuration de la carte réseau.

 ![Problème de capteur VMware](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Consulter le forum Azure ATP](https://aka.ms/azureatpcommunity)