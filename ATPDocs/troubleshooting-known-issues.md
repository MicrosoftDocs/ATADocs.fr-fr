---
title: Dépannage de Microsoft Defender pour identifier les problèmes connus
description: Décrit comment vous pouvez résoudre les problèmes liés à l’identité dans Microsoft Defender.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/07/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fffb94b42e49280949dbdb67926841ebaea8ba2a
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848922"
---
# <a name="troubleshooting-product-long-known-issues"></a>Résolution des [!INCLUDE [Product long](includes/product-long.md)] problèmes connus

## <a name="sensor-failure-communication-error"></a>Erreur d’échec de communication du capteur

Si vous recevez l’erreur d’échec du capteur suivante :

System.Net.Http.HttpRequestException: An error occurred while sending the request. ---> System.Net.WebException: Impossible de se connecter au serveur distant ---> System.Net.Sockets.SocketException: Échec de la tentative de connexion parce que la partie connectée n'a pas répondu correctement après un certain laps de temps ou la connexion établie a échoué parce que l'hôte connecté n'a pas pu répondre...

**Résolution :**

Assurez-vous que la communication n’est pas bloquée pour localhost, port TCP 444. Pour en savoir plus sur les [!INCLUDE [Product long](includes/product-long.md)] conditions préalables, consultez [ports](prerequisites.md#ports).

## <a name="deployment-log-location"></a>Emplacement des journaux de déploiement

Les [!INCLUDE [Product short](includes/product-short.md)] journaux de déploiement se trouvent dans le répertoire Temp de l’utilisateur qui a installé le produit. Dans l'emplacement d'installation par défaut, il s’agit de : C:\Users\Administrator\AppData\Local\Temp (ou d’un répertoire au-dessus de %temp%). Pour plus d’informations, consultez [résolution des problèmes [!INCLUDE [Product short](includes/product-short.md)] à l’aide des journaux](troubleshooting-using-logs.md)

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Le problème d’authentification du proxy se présente sous la forme d’erreur de licence

Si, lors de l’installation du capteur, vous recevez l’erreur suivante :  **The sensor failed to register due to licensing issues.**

**Entrées du journal de déploiement :**

[1C60:1AA8][2018-03-24T23:59:13]i000: 2018-03-25 02:59:13.1237 Info  InteractiveDeploymentManager ValidateCreateSensorAsync a retourné [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-24T23:59:56]i000: 2018-03-25 02:59:56.4856 Info  InteractiveDeploymentManager ValidateCreateSensorAsync a retourné [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-25T00:27:56]i000: 2018-03-25 03:27:56.7399 Debug SensorBootstrapperApplication Engine.Quit [deploymentResultStatus=1602 isRestartRequired=False]] [1C60:15B8][2018-03-25T00:27:56]i500: Shutting down, exit code: 0x642

**Cause :**

Dans certains cas, lors de la communication via un proxy, lors de l’authentification, il peut répondre au [!INCLUDE [Product short](includes/product-short.md)] capteur avec l’erreur 401 ou 403 au lieu de l’erreur 407. Le [!INCLUDE [Product short](includes/product-short.md)] capteur interprétera l’erreur 401 ou 403 comme un problème de licence et non comme un problème d’authentification du proxy.

**Résolution :**

Assurez-vous que le capteur peut naviguer vers *.atp.azure.com via le proxy configuré sans authentification. Pour plus d'informations, consultez [Configurer le proxy pour activer la communication](configure-proxy.md).

## <a name="proxy-authentication-problem-presents-as-a-connection-error"></a>Le problème d’authentification du proxy se présente sous la forme d’une erreur de connexion

Si, lors de l’installation du capteur, vous recevez l’erreur suivante : **Échec de la connexion du capteur au service.**

**Cause :**

Le problème peut être causé par une erreur de configuration de proxy transparente sur Server Core, comme les certificats racines requis par [!INCLUDE [Product short](includes/product-short.md)] ne sont pas actuels ou manquants.

**Résolution :**

Exécutez l’applet de commande PowerShell suivante pour vérifier que le [!INCLUDE [Product short](includes/product-short.md)] certificat racine approuvé du service existe sur Server Core. L’exemple suivant utilise « DigiCert Baltimore Root » et « DigiCert Global Root ».

```powershell
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "D4DE20D05E66FC53FE1A50882C78DB2852CAE474"} | fl
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "df3c24f9bfd666761b268073fe06d1cc8d4f82a4"} | fl
```

```Output
Subject      : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Issuer       : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Thumbprint   : D4DE20D05E66FC53FE1A50882C78DB2852CAE474
FriendlyName : DigiCert Baltimore Root
NotBefore    : 5/12/2000 11:46:00 AM
NotAfter     : 5/12/2025 4:59:00 PM
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}

Subject      : CN=DigiCert Global Root G2, OU=www.digicert.com, O=DigiCert Inc, C=US
Issuer       : CN=DigiCert Global Root G2, OU=www.digicert.com, O=DigiCert Inc, C=US
Thumbprint   : DF3C24F9BFD666761B268073FE06D1CC8D4F82A4
FriendlyName : DigiCert Global Root G2
NotBefore    : 01/08/2013 15:00:00
NotAfter     : 15/01/2038 14:00:00
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}
```

Si vous ne voyez pas la sortie attendue, effectuez les étapes suivantes :

1. Téléchargez le [certificat racine Baltimore CyberTrust](https://cacert.omniroot.com/bc2025.crt) et [DigiCert Global Root G2](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt) sur la machine Server Core.
1. Exécutez l’applet de commande PowerShell suivante pour installer le certificat.

    ```powershell
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\bc2025.crt" -CertStoreLocation Cert:\LocalMachine\Root
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\DigiCertGlobalRootG2.crt" -CertStoreLocation Cert:\LocalMachine\Root
    ```

## <a name="silent-installation-error-when-attempting-to-use-powershell"></a>Erreur d’installation sans assistance lors de la tentative d’utilisation de PowerShell

Si, lors de l’installation sans assistance d’un capteur, vous tentez d’utiliser PowerShell, vous obtenez l’erreur suivante :

```powershell
"Azure ATP sensor Setup.exe" "/quiet" NetFrameworkCommandLineArguments="/q" Acce ... Unexpected token '"/quiet"' in expression or statement."
```

**Cause :**

L’omission du préfixe ./ requis pour l’installation lors de l’utilisation de PowerShell entraîne cette erreur.

**Résolution :**

Utilisez la commande complète pour installer correctement.

```powershell
./"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

## <a name="product-short-sensor-nic-teaming-issue"></a>[!INCLUDE [Product short](includes/product-short.md)] problème d’association de cartes réseau de capteur <a name="nic-teaming"></a>

Si vous tentez d’installer le [!INCLUDE [Product short](includes/product-short.md)] capteur sur un ordinateur configuré avec un adaptateur d’association de cartes réseau, vous recevez une erreur d’installation. Si vous souhaitez installer le [!INCLUDE [Product short](includes/product-short.md)] capteur sur un ordinateur configuré avec l’Association de cartes réseau, suivez ces instructions :

1. Téléchargez le programme d’installation de Npcap version 1,0 à partir de  [https://nmap.org/npcap/](https://nmap.org/npcap/dist/npcap-1.00.exe) .
    - Vous pouvez également demander la version OEM du pilote Npcap (qui prend en charge l’installation sans assistance) de l’équipe de support.
    - Les copies de Npcap n’entrent pas en compte dans les cinq limites de licence utilisateur de cinq ou cinq ordinateurs, si elles sont installées et utilisées uniquement avec [!INCLUDE [Product short](includes/product-short.md)] . Pour plus d’informations, consultez [Gestion des licences NPCAP](https://github.com/nmap/npcap/blob/master/LICENSE).

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

Pour les systèmes d’exploitation Windows 2008R2 et 2012, le capteur [!INCLUDE [Product short](includes/product-short.md)] n’est pas pris en charge en mode Groupe multiprocesseur.

Solutions de contournement possibles :

- Si l’hyperthreading est activé, désactivez-le. Cela peut suffisamment réduire le nombre de cœurs logiques pour éviter d’avoir à exécuter en mode **Groupe multiprocesseur**.

- Si votre ordinateur dispose de moins de 64 cœurs logiques et s’exécute sur un hôte HP, vous pourrez peut-être modifier le paramètre BIOS **Optimisation de la taille du groupe NUMA** de la valeur par défaut **En cluster** à la valeur **Plat**.

## <a name="microsoft-defender-for-endpoint-integration-issue"></a>Problème d’intégration de Microsoft Defender for Endpoint

[!INCLUDE [Product short](includes/product-short.md)] vous permet d’intégrer [!INCLUDE [Product short](includes/product-short.md)] Microsoft Defender for Endpoint. Pour plus d’informations, consultez [intégration [!INCLUDE [Product short](includes/product-short.md)] à Microsoft Defender pour le point de terminaison](integrate-mde.md) .

## <a name="vmware-virtual-machine-sensor-issue"></a>Problème de capteur pour la machine virtuelle VMware

Si vous disposez [!INCLUDE [Product short](includes/product-short.md)] d’un capteur sur des machines virtuelles VMware, vous risquez de recevoir une alerte d’intégrité indiquant que **le trafic réseau n’est pas analysé**. Ce scénario se produit à cause d’une différence de configuration dans VMware.

Pour résoudre le problème

Définissez le paramètre suivant sur **Désactivé** dans la configuration de carte réseau de la machine virtuelle : **IPv4 TSO Offload**.

 ![Problème de capteur VMware](media/vm-sensor-issue.png)

Utilisez la commande suivante pour vérifier si le déchargement d’envoi volumineux (LSO) est activé ou désactivé :

`Get-NetAdapterAdvancedProperty | Where-Object DisplayName -Match "^Large*"`

![Vérifier l’état de LSO](media/missing-network-traffic-health-alert.png)

Si LSO est activé, utilisez la commande suivante pour le désactiver :

`Disable-NetAdapterLso -Name {name of adapter}`

![Désactiver l’état LSO](media/disable-lso-vmware.png)

## <a name="sensor-failed-to-retrieve-group-managed-service-account-gmsa-credentials"></a>Le capteur n’a pas réussi à récupérer les informations d'identification du compte de service administré du groupe (gMSA)

Si vous recevez l’alerte d’intégrité suivante : **Les informations d'identification de l'utilisateur des services d'annuaire sont incorrectes**

**Entrées du journal du capteur :**

2020-02-17 14:01:36.5315 Info ImpersonationManager CreateImpersonatorAsync a démarré [UserName=account_name Domain=domain1.test.local IsGroupManagedServiceAccount=True] 2020-02-17 14:01:36.5750 Info ImpersonationManager CreateImpersonatorAsync a terminé [UserName=account_name Domain=domain1.test.local IsSuccess=False]

**Entrées du journal de mise à jour du capteur :**

2020-02-17 14:02:19.6258 Warn GroupManagedServiceAccountImpersonationHelper GetGroupManagedServiceAccountAccessTokenAsync a échoué, le mot de passe GMSA n’a pas pu être récupéré [errorCode=AccessDenied AccountName=account_name DomainDnsName=domain1.test.local]

**Cause :**

Le capteur n’a pas pu récupérer le compte gMSA désigné à partir du [!INCLUDE [Product short](includes/product-short.md)] portail.

**Résolution :**

Assurez-vous que les informations d’identification du compte gMSA sont correctes et que le capteur a été autorisé à récupérer les informations d’identification du compte. Dans la stratégie appliquée, vous devrez peut-être ajouter le compte gMSA aux attributions des droits utilisateur **Ouvrir une session en tant que service**.

## <a name="report-downloads-cannot-contain-more-than-300000-entries"></a>Les téléchargements de rapports contenant plus de 300 000 entrées ne sont pas pris en charge

[!INCLUDE [Product short](includes/product-short.md)] ne prend pas en charge les téléchargements de rapports contenant plus de 300 000 entrées par rapport. Les rapports de plus de 300 000 entrées ne s’affichent pas intégralement.

**Cause :**

Il s’agit d’une limitation de conception.

**Résolution :**

Aucune solution connue.

## <a name="see-also"></a>Voir aussi

- [Prérequis de [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Planification de capacité [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
