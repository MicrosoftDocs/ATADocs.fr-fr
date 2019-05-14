---
title: Nouveautés de la version 1.8 d’ATA | Microsoft Docs
description: Liste les nouveautés de la version 1.8 d’ATA ainsi que les problèmes connus
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 9/03/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 1f623642813c0474ddf3c7d050a91aebbd1b40b7
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196911"
---
# <a name="whats-new-in-ata-version-18"></a>Nouveautés de la version 1.8 d’ATA

La dernière version de la mise à jour d’ATA peut être [téléchargée à partir du Centre de téléchargement](https://www.microsoft.com/download/details.aspx?id=55536) ou la version complète peut être téléchargée à partir du [centre d’évaluation](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Ces notes de publication fournissent des informations sur les mises à jour, les nouvelles fonctionnalités, les correctifs de bogue et les problèmes connus de cette version d’Advanced Threat Analytics.



## <a name="new--updated-detections"></a>Détections nouvelles et mises à jour

- L’implémentation de protocole inhabituelle a été améliorée pour pouvoir détecter le logiciel malveillant WannaCry.

- NOUVEAU ! **Modification anormale des groupes sensibles** : Dans le cadre de la phase d’élévation de privilèges, l’attaquant modifie des groupes avec des privilèges élevés pour avoir accès à des ressources sensibles. ATA détecte désormais quand une modification anormale est effectuée dans un groupe avec privilèges élevés.
- NOUVEAU ! **Échecs d’authentification suspects** (comportement par force brute) : L’attaquant tente d’utiliser la force brute sur des informations d’identification pour compromettre des comptes. ATA déclenche désormais une alerte quand un comportement anormal d’authentification ayant échoué est détecté.   

- **Tentative d’exécution à distance - WMI exec** : L’attaquant peut tenter de contrôler votre réseau en exécutant du code à distance sur votre contrôleur de domaine. ATA a amélioré la détection de l’exécution à distance pour inclure la détection des méthodes WMI qui permettent d’exécuter du code à distance.

- Reconnaissance à l’aide de requêtes du service d’annuaire : Cette détection a été améliorée pour être en mesure d’intercepter les requêtes sur une seule entité sensible et de réduire le nombre de faux positifs générés dans la version précédente. Si vous avez désactivé cette option dans la version 1.7, l’installation de la version 1.8 l’active désormais automatiquement.

- Activité Golden Ticket Kerberos : ATA 1.8 inclut une technique supplémentaire pour détecter les attaques par golden ticket.
    - ATA détecte désormais les activités suspectes dans lesquelles la durée de vie du golden ticket a expiré. Si un ticket Kerberos est utilisé plus longtemps que la durée de vie autorisée, ATA le détecte comme une activité suspecte de création d’un golden ticket.
- Des améliorations ont été apportées aux détections suivantes pour supprimer les faux positifs connus :  
    - Détection de l’élévation des privilèges (faux PAC) 
    - Activité de passage à une version antérieure du chiffrement (Skeleton Key)
    - Implémentation de protocole inhabituelle
    - Relation de confiance rompue

## <a name="improved-triage-of-suspicious-activities"></a>Triage amélioré des activités suspectes

-   NOUVEAU ! ATA 1.8 vous permet d’exécuter les actions suivantes sur les activités suspectes pendant le processus de triage : 
    - **Exclure des entités** pour qu’elles ne puissent pas lancer des activités suspectes afin d’empêcher ATA de déclencher des alertes quand il détecte des vrais positifs sans gravité (par exemple, un administrateur qui exécute du code à distance ou la détection des analyseurs de sécurité).
    - **Supprimer les activités suspectes récurrentes** dans les alertes.
    - **Supprimer les activités suspectes** de la chronologie des attaques.
-   Le processus de suivi des alertes d’activité suspecte est désormais plus efficace. La chronologie des activités suspectes a été repensée. Dans ATA 1.8, vous pouvez voir bien plus de d’activités suspectes dans un même écran, avec des informations plus pertinentes pour le triage et l’examen. 

## <a name="new-reports-to-help-you-investigate"></a>Nouveaux rapports pour vous aider dans votre analyse 
-   NOUVEAU ! Le **rapport de synthèse** a été ajouté pour vous permettre de consulter toutes les données synthétisées par ATA, notamment les activités suspectes, les problèmes d’intégrité et bien plus encore. Vous pouvez même définir un rapport personnalisé généré automatiquement sur une base régulière.
-   NOUVEAU ! Le **rapport des groupes sensibles** a été ajouté pour vous permettre de consulter toutes les modifications apportées dans les groupes sensibles sur une certaine période.


## <a name="infrastructure-improvements"></a>Améliorations de l’infrastructure

-   Les performances du centre ATA ont été améliorées. Dans ATA 1.8, le centre ATA peut traiter plus de 1 million de paquets par seconde.
-   La passerelle légère ATA peut désormais lire les événements localement, sans qu’il soit nécessaire de configurer le transfert d’événements.
-   Vous pouvez maintenant configurer séparément la messagerie pour surveiller les alertes et les activités suspectes.

## <a name="security-improvements"></a>Améliorations apportées à la sécurité

-   NOUVEAU ! **Authentification unique pour la gestion d’ATA**. ATA prend en charge l’authentification unique intégrée à l’authentification Windows : si vous avez déjà ouvert une session sur votre ordinateur, ATA utilise ce jeton pour vous connecter à la console ATA. Vous pouvez aussi vous connecter à l’aide d’une carte à puce. Les scripts d’installation sans assistance pour la passerelle ATA et la passerelle légère ATA utilisent désormais le contexte de l’utilisateur connecté, sans demander les informations d’identification.
-   Les privilèges sur le système local ont été supprimés du processus de passerelle ATA, vous pouvez maintenant utiliser des comptes virtuels (disponibles uniquement sur les passerelles ATA autonomes), des comptes de service administrés et des comptes de service administrés de groupe pour exécuter le processus de passerelle ATA.   
-   Des journaux d’audit pour le centre et les passerelles ATA ont été ajoutés et toutes les actions sont maintenant consignées dans le journal des événements Windows.
-   La prise en charge des certificats KSP a été ajoutée pour le centre ATA.

## <a name="additional-changes"></a>Autres modifications

- La possibilité d’ajouter des notes a été supprimée dans les activités suspectes
- Les recommandations sur la limitation des activités suspectes ont été supprimées de la chronologie Activités suspectes.
- Depuis ATA version 1.8, les passerelles ATA et les passerelles légères gèrent leurs propres certificats et n’ont besoin d’aucune interaction de la part de l’administrateur pour les gérer.

## <a name="known-issues"></a>Problèmes connus

> [!WARNING]
> Afin d’éviter ces problèmes connus, effectuez les mises à jour ou les déploiements avec la version 1.8 Update 1.

### <a name="ata-gateway-on-windows-server-core"></a>Passerelle ATA sur Windows Server Core

**Symptômes :** La mise à niveau d’une passerelle ATA vers la version 1.8 sur Windows Server 2012 R2 Core avec .NET Framework 4.7 peut échouer avec l’erreur : *La passerelle Microsoft Advanced Threat Analytics a cessé de fonctionner*. 

![Erreur de base de passerelle](./media/gateway-core-error.png)

Sur Windows Server 2016 Core, vous ne verrez peut-être pas l’erreur mais le processus échouera quand vous essaierez d’effectuer l’installation. Les événements 1000 et 1001 (blocage du processus) seront consignés dans le journal des événements d’application sur le serveur.

**Description** : Un problème s’est produit avec .NET Framework 4.7, provoquant l’échec du chargement des applications qui utilisent la technologie WPF (comme ATA). Pour plus d’informations, consultez [l’article KB 4034015](https://support.microsoft.com/help/4034015/wpf-window-can-t-be-loaded-after-you-install-the-net-framework-4-7-on). 

**Solution de contournement** : Désinstallez .NET 4.7 [Consultez l’article KB 3186497](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows) pour revenir à la version 4.6.2 de .NET, puis mettez à jour votre passerelle ATA vers la version 1.8. Après la mise à niveau d’ATA, vous pouvez réinstaller .NET 4.7.  Pour corriger ce problème, une mise à jour sera publiée dans une prochaine version.

### <a name="lightweight-gateway-event-log-permissions"></a>Autorisations du journal des événements de la passerelle légère

**Symptômes :** Quand vous mettez à niveau ATA vers la version 1.8, les applications ou les services qui avaient déjà des autorisations d’accès au journal des événements de sécurité peuvent perdre ces autorisations. 

**Description** : Afin de faciliter le déploiement d’ATA, ATA 1.8 accède à votre journal des événements de sécurité directement, sans nécessiter la configuration du transfert des événements Windows. En même temps, ATA s’exécute comme un service local avec un faible niveau d’autorisation pour maintenir une sécurité plus stricte. Afin de fournir l’accès pour qu’ATA puisse lire les événements, le service ATA s’accorde lui-même des autorisations dans le journal des événements de sécurité. Quand ce cas se produit, les autorisations précédemment définies pour d’autres services peuvent être désactivées.

**Solution de contournement** : Exécutez le script Windows PowerShell suivant. Cette action supprime les autorisations qui n’ont pas été correctement ajoutées dans le Registre à partir d’ATA et les ajoute par le biais d’une autre API. Cela peut restaurer les autorisations pour d’autres applications. Si ce n’est pas le cas, elles devront être restaurées manuellement. Pour corriger ce problème, une mise à jour sera publiée dans une prochaine version. 

       $ATADaclEntry = "(A;;0x1;;;S-1-5-80-1717699148-1527177629-2874996750-2971184233-2178472682)"
        try {
        $SecurityDescriptor = Get-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        $ATASddl = "O:BAG:SYD:" + $ATADaclEntry 
        if($SecurityDescriptor.CustomSD -eq $ATASddl) {
        Remove-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        }
    }
    catch
    {
    # registry key does not exist
    }

    $EventLogConfiguration = New-Object -TypeName System.Diagnostics.Eventing.Reader.EventLogConfiguration("Security")
    $EventLogConfiguration.SecurityDescriptor = $EventLogConfiguration.SecurityDescriptor + $ATADaclEntry

### <a name="proxy-interference"></a>Interférence de proxy

**Symptômes :** Après la mise à niveau vers ATA 1.8, le service de passerelle ATA peut ne pas démarrer. L’exception suivante peut être présente dans le journal des erreurs ATA : *System.Net.Http.HttpRequestException: An error occurred while sending the request. ---> System.Net.WebException: Le serveur distant a retourné une erreur : (407) Authentification proxy requise.*

**Description** : À compter d’ATA 1.8, la passerelle ATA communique avec le centre ATA via le protocole HTTP. Si l’ordinateur sur lequel vous avez installé la passerelle ATA utilise un serveur proxy pour se connecter au centre ATA, il peut rompre cette communication. 

**Solution de contournement** : Désactivez l’utilisation d’un serveur proxy sur le compte du service de passerelle ATA. Pour corriger ce problème, une mise à jour sera publiée dans une prochaine version.

### <a name="report-settings-reset"></a>Réinitialisation des paramètres des rapports

**Symptômes :** Tous les paramètres qui ont été définis pour les rapports planifiés sont réinitialisés quand vous effectuez la mise à jour vers la version 1.8 Update 1.

**Description** : La mise à jour de la version 1.8 vers la version 1.8 Update 1 entraîne la réinitialisation des paramètres des rapports planifiés.

**Solution de contournement** : Avant d’effectuer la mise à jour vers la version 1.8 Update 1, faites une copie des paramètres des rapports pour pouvoir ensuite les entrer à nouveau. Vous pouvez aussi le faire via un script. Pour plus d’informations, consultez [Exporter et importer la configuration d’ATA](ata-configuration-file.md).


## <a name="see-also"></a>Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Mise à jour d’ATA vers la version 1.8 : guide de migration](ata-update-1.8-migration-guide.md)

