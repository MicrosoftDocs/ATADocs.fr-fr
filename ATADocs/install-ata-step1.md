---
title: Installer Advanced Threat Analytics-étape 1
description: La première étape de la procédure d’installation d’ATA consiste à télécharger le centre ATA et à l’installer sur le serveur de votre choix.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/07/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d5c61390abddf29b92afc0bb6cb2336b0bc9d7ea
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690735"
---
# <a name="install-ata---step-1"></a>Installer ATA - Étape 1

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!NOTE]
> **Cycle de vie de support**
>
> La version finale d’ATA est mise à la [disposition générale](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9). ATA prendra fin au support standard le 12 janvier 2021. Le support étendu se poursuivra jusqu’au 2026 janvier. Pour plus d’informations, consultez [notre blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181).

> [!div class="step-by-step"]
> [Étape 2»](install-ata-step2.md)

Cette procédure d’installation fournit des instructions pour effectuer une nouvelle installation d’ATA 1.9. Pour plus d’informations sur la mise à jour d’un déploiement d’ATA existant à partir d’une version antérieure, consultez le [guide de migration d’ATA pour la version 1.9](ata-update-1.9-migration-guide.md).

> [!IMPORTANT]
> Si vous utilisez Windows 2012 R2, installez la mise à jour KB2934520 sur le serveur du centre ATA et sur les serveurs de passerelle ATA avant de lancer l’installation ; sinon, le programme d’installation d’ATA installe cette mise à jour qui nécessite un redémarrage pendant l’installation d’ATA.

## <a name="step-1-download-and-install-the-ata-center"></a>Étape 1. Télécharger et installer le centre ATA

Après avoir vérifié que le serveur répond à la configuration requise, vous pouvez passer à l’installation du centre ATA.

> [!NOTE]
> Si vous avez acquis une licence pour Enterprise Mobility + Security (EMS) directement sur le portail Microsoft 365 ou par le modèle CSP (Cloud Solution Partner) et que vous n’avez pas d’accès à ATA via le Centre de gestion des licences en volume Microsoft, contactez le service client Microsoft pour obtenir la procédure permettant d’activer ATA (Advanced Threat Analytics).

Effectuez les opérations suivantes sur le serveur du centre ATA.

1. Téléchargez ATA à partir du centre de gestion des [licences en volume Microsoft](https://www.microsoft.com/Licensing/servicecenter/default.aspx) ou à partir du [Centre d’évaluation TechNet](https://www.microsoft.com/evalcenter/) ou de [MSDN](/powerapps/developer/common-data-service/org-service/subscribe-sdk-assembly-updates-using-nuget).

1. Connectez-vous à l’ordinateur sur lequel vous installez le centre ATA en tant qu’utilisateur membre du groupe Administrateurs local.

1. Exécutez **Microsoft ATA Center Setup.EXE**, puis suivez les instructions de l’Assistant Installation.

    > [!NOTE]
    > Veillez à exécuter le fichier d’installation à partir d’un lecteur local, et non à partir d’un fichier ISO monté, pour éviter les problèmes liés à un redémarrage obligatoire dans le cadre de l’installation.

1. Si Microsoft .NET Framework n’est pas installé, vous êtes invité à l’installer lorsque vous démarrez l’installation. Vous pouvez être invité à effectuer un redémarrage après avoir installé le .NET Framework.
1. Sur la page **Bienvenue** , sélectionnez la langue à utiliser pour les écrans d’installation d’ATA, puis cliquez sur **suivant**.

1. Lisez les Termes du contrat de licence logiciel Microsoft ; si vous les acceptez, cochez la case correspondante, puis cliquez sur **Suivant**.

1. Nous recommandons de configurer la mise à jour automatique pour ATA. Si Windows n’est pas configuré pour se mettre à jour automatiquement sur votre ordinateur, l’écran **Utiliser Microsoft Update pour maintenir l’ordinateur à jour et sécurisé** apparaît.
    ![Image montrant comment maintenir ATA à jour](media/ata_ms_update.png)

1. Sélectionnez **Utiliser Microsoft Update lorsque je recherche des mises à jour (recommandé)**. Les paramètres Windows sont modifiés de manière à récupérer les mises à jour des autres produits Microsoft (y compris ATA).

    ![Image de mise à jour automatique de Windows](media/ata_installupdatesautomatically.png)

1. Dans la page **Configurer le centre**, entrez les informations suivantes en fonction de votre environnement :

    |Champ|Description|Commentaires|
    |---------|---------------|------------|
    |Chemin d’installation|Il s’agit de l’emplacement où est installé le centre ATA. L’emplacement par défaut est le suivant : %programfiles%\Microsoft Advanced Threat Analytics\Center|Conservez la valeur par défaut|
    |Chemin d’accès des données de la base de données|Il s’agit de l’emplacement dans lequel les fichiers de la base de données MongoDB sont enregistrés. L’emplacement par défaut est le suivant : %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data.|Modifiez cette valeur pour pointer vers un emplacement capable de prendre en charge l’évolution de vos besoins en matière de redimensionnement. **Remarque :** <ul><li>Dans les environnements de production, vous devez utiliser un lecteur avec suffisamment d'espace (tel que déterminé par la planification de la capacité).</li><li>Pour les déploiements volumineux, la base de données doit figurer sur un disque physique distinct.</li></ul>Pour plus d’informations sur le redimensionnement, consultez [Planification de la capacité ATA](ata-capacity-planning.md).|
    |Certificat SSL du service du centre|Il s’agit du certificat utilisé par le service du centre ATA et de la console ATA.|Cliquez sur l’icône en forme de clé pour sélectionner un certificat installé ou utilisez la case à cocher pour créer un certificat auto-signé.|

    ![Image de la configuration du centre ATA](media/ATA-Center-Configuration.png)

    > [!NOTE]
    > Veillez à attirer l’attention sur les alertes d’intégrité concernant l’état du certificat SSL du Service Center et les avertissements d’expiration. Si le certificat expire, vous devrez redéployer complètement ATA.

1. Cliquez sur **Installer** pour installer le centre ATA et ses composants.  
Les composants suivants sont installés et configurés pendant l’installation du centre ATA :

    - Service du centre ATA

    - MongoDB

    - Jeu d’éléments de collecte de données de l’Analyseur de performances personnalisé

    - Certificats auto-signés (s’ils ont été sélectionnés pendant l’installation)

1. Une fois l’installation terminée, cliquez sur **Lancer** pour ouvrir la Console ATA et effectuer la configuration sur la page **Configuration**.
    La page de paramètres **Général** s’ouvre automatiquement pour vous permettre de poursuivre la configuration et le déploiement des passerelles ATA.
    Étant donné que vous vous connectez au site à l’aide d’une adresse IP, vous recevez un avertissement lié au certificat. Ce comportement étant normal, cliquez sur **Poursuivre sur ce site web**.

### <a name="validate-installation"></a>Valider l’installation

1. Vérifiez que le service nommé **Microsoft Advanced Threat Analytics Center** est en cours d’exécution.
1. Sur le bureau, cliquez sur le raccourci **Microsoft Advanced Threat Analytics** pour vous connecter à la console ATA. Connectez-vous avec les informations d’identification d’utilisateur que vous avez utilisées pour installer le centre ATA.

### <a name="set-anti-virus-exclusions"></a>Définir des exclusions d’antivirus

Après avoir installé le centre ATA, excluez le répertoire de base de données MongoDB de l’analyse continue de votre application antivirus. L’emplacement par défaut dans la base de données est : **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data**.

Veillez à également exclure les dossiers et les processus suivants de l’analyse antivirus :

**Dossiers**  
C:\Program Files\Microsoft Advanced Threat Analytics\Center\ParentKerberosAsBloomFilters  
C:\Program Files\Microsoft Advanced Threat Analytics\Center\ParentKerberosTgsBloomFilters  
C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup  
C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs

**Processus**  
mongod.exe  
Microsoft.Tri.Center.exe

Si vous avez installé ATA dans un autre répertoire, modifiez les chemins d’accès des dossiers en fonction de votre installation.

> [!div class="step-by-step"]
> [«Pré-installation](configure-port-mirroring.md) 
>  [Étape 2»](install-ata-step2.md)

## <a name="related-videos"></a>Vidéos connexes

- [Sélection du type de passerelle ATA approprié](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)
- [Vue d’ensemble du déploiement ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)

## <a name="see-also"></a>Voir aussi

- [Guide de déploiement ATA POC](https://aka.ms/atapoc)
- [Outil de dimensionnement ATA](https://aka.ms/atasizingtool)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](ata-prerequisites.md)