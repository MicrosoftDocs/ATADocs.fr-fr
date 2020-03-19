---
title: Dépannage des problèmes connus d’Azure ATP
description: Décrit comment résoudre les problèmes d’Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/18/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 61415f1a5f74a216dd0c505b6e92419601e08941
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414639"
---
# <a name="troubleshooting-azure-atp-known-issues"></a>Dépannage des problèmes connus d’Azure ATP

## <a name="sensor-failure-communication-error"></a>Erreur d’échec de communication du capteur

Si vous recevez l’erreur d’échec du capteur suivante :

System.Net.Http.HttpRequestException: An error occurred while sending the request. ---> System.Net.WebException: Impossible de se connecter au serveur distant ---> System.Net.Sockets.SocketException: Échec de la tentative de connexion parce que la partie connectée n'a pas répondu correctement après un certain laps de temps ou la connexion établie a échoué parce que l'hôte connecté n'a pas pu répondre...

**Résolution :**

Assurez-vous que la communication n’est pas bloquée pour localhost, port TCP 444. Pour en savoir plus sur les prérequis Azure ATP, consultez les [ports](atp-prerequisites.md#ports).

## <a name="deployment-log-location"></a>Emplacement des journaux de déploiement

Les journaux de déploiement Azure ATP se trouvent dans le répertoire temp de l’utilisateur qui a installé le produit. Dans l'emplacement d'installation par défaut, il s’agit de : C:\Users\Administrator\AppData\Local\Temp (ou d’un répertoire au-dessus de %temp%). Pour plus d'informations, consultez [Résolution des problèmes liés à ATP à l’aide des journaux](troubleshooting-atp-using-logs.md)

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Le problème d’authentification du proxy se présente sous la forme d’erreur de licence

Si, lors de l’installation du capteur, vous recevez l’erreur suivante :  **The sensor failed to register due to licensing issues.**

**Entrées du journal de déploiement :**

[1C60:1AA8][2018-03-24T23:59:13]i000: 2018-03-25 02:59:13.1237 Info  InteractiveDeploymentManager ValidateCreateSensorAsync a retourné [validateCreateSensorResult=LicenseInvalid]]  
[1C60:1AA8][2018-03-24T23:59:56]i000: 2018-03-25 02:59:56.4856 Info  InteractiveDeploymentManager ValidateCreateSensorAsync a retourné [validateCreateSensorResult=LicenseInvalid]]  
[1C60:1AA8][2018-03-25T00:27:56]i000: 2018-03-25 03:27:56.7399 Debug SensorBootstrapperApplication Engine.Quit [deploymentResultStatus=1602 isRestartRequired=False]]  
[1C60:15B8][2018-03-25T00:27:56]i500: Shutting down, exit code: 0x642

**Cause :**

Dans certains cas, lors de la communication via un proxy, lors de l’authentification, il peut répondre au capteur Azure ATP avec l’erreur 401 ou 403 au lieu de l’erreur 407. Le capteur Azure ATP interprétera l’erreur 401 ou 403 comme un problème de licence et non comme un problème d’authentification du proxy.

**Résolution :**

Assurez-vous que le capteur peut naviguer vers *.atp.azure.com via le proxy configuré sans authentification. Pour plus d'informations, consultez [Configurer le proxy pour activer la communication](configure-proxy.md).

## <a name="silent-installation-error-when-attempting-to-use-powershell"></a>Erreur d’installation sans assistance lors de la tentative d’utilisation de PowerShell

Si, lors de l’installation sans assistance d’un capteur, vous tentez d’utiliser PowerShell, vous obtenez l’erreur suivante :

    "Azure ATP sensor Setup.exe" "/quiet" NetFrameworkCommandLineArguments="/q" Acce ... Unexpected token '"/quiet"' in expression or statement."

**Cause :** L’omission du préfixe ./ requis pour l’installation lors de l’utilisation de PowerShell entraîne cette erreur.

**Résolution :** Utilisez la commande complète pour installer correctement.

```powershell
./"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

## Problème d’association de cartes réseau du capteur Azure ATP <a name="nic-teaming"></a>

Si vous essayez d’installer le capteur ATP sur un ordinateur configuré avec une carte d’association de cartes réseau, vous recevez une erreur d’installation. Si vous souhaitez installer le capteur ATP sur une machine configurée avec une association de cartes réseau, suivez ces instructions :

1. Téléchargez le programme d’installation Npcap version 0.9984 à partir de  [https://nmap.org/npcap/](https://nmap.org/npcap/dist/npcap-0.9984.exe).
    - Vous pouvez également demander la version OEM du pilote Npcap (qui prend en charge l’installation sans assistance) de l’équipe de support.
    - Les copies de Npcap ne sont pas prises en compte dans les cinq limites de licence utilisateur de cinq ou cinq ordinateurs, si elles sont installées et utilisées uniquement conjointement avec Azure ATP. Pour plus d’informations, consultez [Gestion des licences NPCAP](https://github.com/nmap/npcap/blob/master/LICENSE).

Si vous n’avez pas encore installé le capteur :

1. Désinstallez WinPcap, s’il était installé.
1. Installez Npcap avec les options suivantes : loopback_support=no & winpcap_mode=yes.
    - Si vous utilisez le programme d’installation de l’interface utilisateur graphique, désactivez le **support de bouclage** et sélectionnez mode **WinPcap**.
1. Installez le package du capteur.

Si vous avez déjà installé le capteur :

1. Désinstallez le capteur.
1. Désinstallez WinPcap.
1. Installez Npcap avec les options suivantes : loopback_support=no & winpcap_mode=yes
    - Si vous utilisez le programme d’installation de l’interface utilisateur graphique, désactivez le **support de bouclage** et sélectionnez mode **WinPcap**.
1. Réinstallez le package du capteur.

## <a name="multi-processor-group-mode"></a>Mode Groupe multiprocesseur

Pour les systèmes d’exploitation Windows 2008R2 et 2012, le capteur Azure ATP n’est pas pris en charge en mode Groupe multiprocesseur.

Solutions de contournement possibles :

- Si l’hyperthreading est activé, désactivez-le. Cela peut suffisamment réduire le nombre de cœurs logiques pour éviter d’avoir à exécuter en mode **Groupe multiprocesseur**.

- Si votre ordinateur dispose de moins de 64 cœurs logiques et s’exécute sur un hôte HP, vous pourrez peut-être modifier le paramètre BIOS **Optimisation de la taille du groupe NUMA** de la valeur par défaut **En cluster** à la valeur **Plat**.

## <a name="windows-defender-atp-integration-issue"></a>Problème d’intégration Windows Defender ATP

Azure Advanced Threat Protection vous permet d’intégrer Azure ATP et Windows Defender ATP. Pour plus d’informations, consultez [Intégration d’Azure ATP et de Windows Defender ATP](integrate-wd-atp.md).

## <a name="vmware-virtual-machine-sensor-issue"></a>Problème de capteur pour la machine virtuelle VMware

Si vous avez un capteur Azure ATP sur des machines virtuelles VMware, vous pouvez recevoir l’alerte de surveillance **Une partie du trafic réseau n’est pas analysée**. Ce scénario se produit à cause d’une différence de configuration dans VMware.

Pour résoudre le problème

Définissez le paramètre suivant sur **Désactivé** dans la configuration de carte réseau de la machine virtuelle : **IPv4 TSO Offload**.

 ![Problème de capteur VMware](./media/vm-sensor-issue.png)

Utilisez la commande suivante pour vérifier si le déchargement d’envoi volumineux (LSO) est activé ou désactivé :

`Get-NetAdapterAdvancedProperty | Where-Object DisplayName -Match "^Large*"`

![Vérifier l’état de LSO](./media/missing-network-traffic-health-alert.png)

Si LSO est activé, utilisez la commande suivante pour le désactiver :

`Disable-NetAdapterLso -Name {name of adapter}`

![Désactiver l’état LSO](./media/disable-lso-vmware.png)

## <a name="sensor-failed-to-retrieve-group-managed-service-account-gmsa-credentials"></a>Le capteur n’a pas réussi à récupérer les informations d'identification du compte de service administré du groupe (gMSA)

Si vous recevez l’alerte de surveillance suivante : **Les informations d'identification de l'utilisateur des services d'annuaire sont incorrectes**

**Entrées du journal du capteur :**

2020-02-17 14:01:36.5315 Info ImpersonationManager CreateImpersonatorAsync a démarré [UserName=account_name Domain=domain1.test.local IsGroupManagedServiceAccount=True]  
2020-02-17 14:01:36.5750 Info ImpersonationManager CreateImpersonatorAsync a terminé [UserName=account_name Domain=domain1.test.local IsSuccess=False]

**Entrées du journal de mise à jour du capteur :**

2020-02-17 14:02:19.6258 Warn GroupManagedServiceAccountImpersonationHelper GetGroupManagedServiceAccountAccessTokenAsync a échoué, le mot de passe GMSA n’a pas pu être récupéré [errorCode=AccessDenied AccountName=account_name DomainDnsName=domain1.test.local]

**Cause :**

le capteur n’a pas pu récupérer le compte gMSA désigné à partir du portail Azure ATP.

**Résolution :**

Assurez-vous que les informations d’identification du compte gMSA sont correctes et que le capteur a été autorisé à récupérer les informations d’identification du compte.

## <a name="see-also"></a>Voir aussi

- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
