---
title: Tutoriel de configuration du labo des alertes de sécurité Microsoft Defender pour Identity
description: Ce tutoriel vise à configurer un labo de test Microsoft Defender pour Identity pour simuler des menaces à des fins de détection par Defender pour Identity.
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e175744d29cac82c29dc1f072a145ee68770dcf7
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847052"
---
# <a name="tutorial-setup-a-product-long-security-alert-lab"></a>Tutoriel : Configuration d’un labo d’alertes de sécurité [!INCLUDE [Product long](includes/product-long.md)]

L’objectif du labo des alertes de sécurité [!INCLUDE [Product long](includes/product-long.md)] est d’illustrer les fonctionnalités de **[!INCLUDE [Product short](includes/product-short.md)]** concernant l’identification et la détection des activités suspectes et des attaques potentielles du réseau. Ce premier tutoriel d’une série en quatre parties explique comment créer un environnement labo permettant de tester les détections *discrètes* de [!INCLUDE [Product short](includes/product-short.md)]. Le labo des alertes de sécurité se concentre sur les fonctionnalités liées à la *signature* de [!INCLUDE [Product short](includes/product-short.md)]. Ce labo n’inclut pas le Machine Learning avancé, ni les détections de comportements basées sur utilisateur ou l’entité, car celles-ci nécessitent une période d’apprentissage avec un trafic réseau réel pouvant aller jusqu’à 30 jours. Pour plus d’informations sur les différents tutoriels de cette série, consultez la [vue d’ensemble des labos des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)]](playbook-lab-overview.md).

Ce didacticiel vous apprendra à effectuer les opérations suivantes :

> [!div class="checklist"]
>
> - configurer votre serveur de labo et vos ordinateurs ;
> - configurer Active Directory avec des utilisateurs et des groupes ;
> - configurer [!INCLUDE [Product short](includes/product-short.md)] ;
> - configurer les stratégies locales pour votre serveur et vos ordinateurs ;
> - simuler un scénario de gestion du support technique à l’aide d’une tâche planifiée.

## <a name="prerequisites"></a>Prérequis

1. [Un contrôleur de domaine du labo et deux stations de travail de labo](#servers-and-computers).
    - Continuez et [alimentez Active Directory (AD) avec des utilisateurs](#bkmk_hydrate).

1. Une [instance [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md) [connectée à AD](install-step2.md).
1. [Téléchargez](install-step3.md) et [installez la dernière version du capteur [!INCLUDE [Product short](includes/product-short.md)]](install-step4.md) sur le contrôleur de domaine de votre labo.
1. Vous êtes familiarisé avec les [stations de travail à accès privilégié](/windows-server/identity/securing-privileged-access/privileged-access-workstations) et la [stratégie SAMR](/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).

## <a name="recommendations"></a>Recommandations

Nous vous recommandons de suivre d’aussi près que possible les instructions de configuration du labo. Plus votre labo sera proche de la configuration suggérée, plus les procédures de test [!INCLUDE [Product short](includes/product-short.md)] seront faciles à suivre. Une fois que vous l’aurez configuré, vous pourrez effectuer des actions avec les outils de recherche de piratage suggérés et vérifier leur détection par [!INCLUDE [Product short](includes/product-short.md)].

Votre configuration complète du labo doit ressembler le plus possible au diagramme suivant :

![Configuration du labo de test [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-setup-lab.png)

### <a name="servers-and-computers"></a>Serveurs et ordinateurs

Ce tableau détaille les ordinateurs et les configurations nécessaires. Les adresses IP sont fournies à titre de référence uniquement afin que vous puissiez suivre facilement.

Dans les exemples pour ces tutoriels, le nom NetBIOS de la forêt est **CONTOSO. AZURE**.

| FQDN | Système d''exploitation | IP | Objectif |
|------|-------|---------|--------------|
| ContosoDC.contoso.azure | Windows Server 2012 R2 | 10.0.24.4 | Contrôleur de domaine avec le capteur [!INCLUDE [Product short](includes/product-short.md)] installé en local |
| VictimPC.contoso.azure | Windows 10 | 10.0.24.5 |PC de la victime |
| AdminPC.contoso.azure | Windows 10  | 10.0.24.6 | PC de l’administrateur de domaine (parfois appelé « Station de travail d’administrateur sécurisée » ou « Station de travail d’administrateur privilégiée ») |

### <a name="active-directory-users-and-groups"></a>Utilisateurs et groupes Active Directory

Dans ce labo, il y a trois principaux utilisateurs et un compte de service. Le compte de service, destiné à [!INCLUDE [Product short](includes/product-short.md)], sert à la fois à la synchronisation LDAP et à SAM-R.

Il existe un groupe de sécurité « Support technique » dont Ron HelpDesk est membre. Ce groupe de sécurité imite le support technique. Le groupe de sécurité est associé à un objet de stratégie de groupe qui donne des droits d’administrateur local aux membres de notre support technique sur leurs ordinateurs respectifs. Cette configuration est utilisée pour simuler un modèle réaliste d’administration dans un environnement de production.

| Complète | Nom complet | Compte SAM | Objectif |
|--|--|--|
| Jeff Leatherman | JeffL | Bientôt victime d’une attaque par hameçonnage d’une efficacité impressionnante |
| Ron HelpDesk | RonHD | Ron est la « personne à contacter » de l’équipe informatique de Contoso. RonHD est membre du groupe de sécurité « Support technique » . |
| Samira Abbasi | SamiraA | Chez Contoso, cet utilisateur est notre administrateur de domaine. |
| [!INCLUDE [Product short](includes/product-short.md)] | AATPService | Compte de service de [!INCLUDE [Product short](includes/product-short.md)] | account |

## <a name="product-short-base-lab-environment"></a>Environnement de labo de base [!INCLUDE [Product short](includes/product-short.md)]

Pour configurer le labo de base, nous allons ajouter des utilisateurs et des groupes à Active Directory, puis modifier une stratégie SAM et un groupe sensible dans [!INCLUDE [Product short](includes/product-short.md)].

### <a name="hydrate-active-directory-users-on-contosodc"></a><a name="bkmk_hydrate"></a> Alimenter Active Directory avec des utilisateurs sur ContosoDC

Pour simplifier le labo, nous avons automatisé le processus de création d’utilisateurs et de groupes fictifs dans Active Directory. Ce script est exécuté comme une condition préalable à ce tutoriel. Vous pouvez utiliser ou modifier le script pour alimenter l’environnement Active Directory de votre labo. Si vous préférez ne pas utiliser de script, vous pouvez le faire manuellement.

En tant qu’administrateur de domaine, sur ContosoDC, exécutez la commande suivante pour alimenter Active Directory avec des utilisateurs :

```powerShell
# Store the user passwords as variables
$SamiraASecurePass = ConvertTo-SecureString -String 'NinjaCat123' -AsPlainText -Force
$ronHdSecurePass = ConvertTo-SecureString -String 'FightingTiger$' -AsPlainText -Force
$jefflSecurePass = ConvertTo-SecureString -String 'Password$fun' -AsPlainText -Force
$AATPService = ConvertTo-SecureString -String 'Password123!@#' -AsPlainText -Force

# Create new AD user SamiraA and add her to the domain admins group
New-ADUser -Name SamiraA -DisplayName "Samira Abbasi" -PasswordNeverExpires $true -AccountPassword $samiraASecurePass -Enabled $true
Add-ADGroupMember -Identity "Domain Admins" -Members SamiraA

# Create new AD user RonHD, create new Helpdesk SG, add RonHD to the Helpdesk SG
New-ADUser -Name RonHD -DisplayName "Ron Helpdesk" -PasswordNeverExpires $true -AccountPassword $ronHdSecurePass -Enabled $true
New-ADGroup -Name Helpdesk -GroupScope Global -GroupCategory Security
Add-ADGroupMember -Identity "Helpdesk" -Members "RonHD"

# Create new AD user JeffL
New-ADUser -Name JeffL -DisplayName "Jeff Leatherman" -PasswordNeverExpires $true -AccountPassword $jefflSecurePass -Enabled $true

# Take note of the "AATPService" user below which will be our service account for [!INCLUDE [Product short](includes/product-short.md)].
# Create new AD user [!INCLUDE [Product short](includes/product-short.md)] Service

New-ADUser -Name AatpService -DisplayName "Azure ATP/ATA Service" -PasswordNeverExpires $true -AccountPassword $AATPService -Enabled $true
```

### <a name="configure-sam-r-capabilities-from-contosodc"></a>Configurer les fonctionnalités SAM-R à partir de ContosoDC

Pour autoriser le Service [!INCLUDE [Product short](includes/product-short.md)] à effectuer correctement une énumération SAM-R et à créer des chemins de mouvement latéral, vous devez modifier la stratégie SAM.

1. Recherchez votre stratégie SAM sous : **Stratégies \> Paramètres Windows \> Paramètres de sécurité \> Stratégies locales \> Options de sécurité \> « Accès réseau : restreindre les clients autorisés à passer des appels distants à SAM »** .

    ![Modification de la stratégie de groupe pour autoriser [!INCLUDE [Product short](includes/product-short.md)] à utiliser les fonctionnalités de chemin de mouvement latéral](media/playbook-labsetup-localgrouppolicies3.png)

1. Ajoutez le compte de service [!INCLUDE [Product short](includes/product-short.md)], AATPService, à la liste des comptes approuvés capables d’effectuer cette action sur vos systèmes Windows modernes.

    ![Ajoutez le service](media/samr-add-service.png)

### <a name="add-sensitive-group-to-product-short"></a>Ajout d’un groupe sensible à [!INCLUDE [Product short](includes/product-short.md)]

Après avoir ajouté le groupe de sécurité « Support technique » comme **Groupe sensible**, vous pourrez utiliser la fonctionnalité de graphe de mouvement latéral de [!INCLUDE [Product short](includes/product-short.md)]. Le balisage d’utilisateurs et de groupes très sensibles qui ne sont pas nécessairement des administrateurs de domaine mais disposent de privilèges pour de nombreuses ressources est une meilleure pratique.

1. Sur le portail [!INCLUDE [Product short](includes/product-short.md)], cliquez sur **Configuration**.

1. Sous **Détection**, sélectionnez **Étiquettes d’entité**.

    ![Étiquettes d’entité [!INCLUDE [Product short](includes/product-short.md)]](media/entity-tags.png)
1. Dans la section **Sensible**, tapez le nom « Support technique » pour **Groupes sensibles**, puis cliquez sur le signe **+** pour les ajouter.
    ](media/playbook-labsetup-helpdesksensitivegroup.png)Étiquetage de « Support technique » comme groupe sensible [!INCLUDE [Product short](includes/product-short.md)] pour activer les graphes et les rapports de mouvement latéral de ce groupe privilégié![
1. Cliquez sur **Enregistrer**.

### <a name="product-short-lab-base-setup-checklist"></a>Liste de contrôle de la configuration de base du labo [!INCLUDE [Product short](includes/product-short.md)]

Vous disposez maintenant d’un labo [!INCLUDE [Product short](includes/product-short.md)] de base. [!INCLUDE [Product short](includes/product-short.md)] est prêt à l’emploi, et les utilisateurs en attente. Passez en revue la liste de vérification pour vous assurer que le labo de base est terminé.

| Étape  | Étape | Action | État |
|--|--|--|
| 1 | Capteur [!INCLUDE [Product short](includes/product-short.md)] installé sur ContosoDC (prérequis) | - [ ] |
| 2 | Les utilisateurs et les groupes sont créés dans Active Directory | - [ ] |
| 3 | Privilèges du compte de service [!INCLUDE [Product short](includes/product-short.md)] configurés correctement pour SAM-R | - [ ] |
| 4 | Groupe de sécurité Support technique ajouté comme **Groupe sensible** dans [!INCLUDE [Product short](includes/product-short.md)] | - [ ] |](includes/product-other.md)]| - [ ] |

## <a name="set-up-the-lab-workstations"></a>Configurer les stations de travail du labo

Une fois que vous avez vérifié que votre labo [!INCLUDE [Product short](includes/product-short.md)] de base est configuré, vous pouvez commencer à configurer la station de travail pour préparer les trois tutoriels suivants de cette série. Nous allons alimenter notre VictimPC et AdminPC pour donner une apparence active à ce labo.

### <a name="victimpc-local-policies"></a>Stratégies VictimPC locales

L’étape suivante pour votre labo consiste à terminer la configuration de la stratégie locale. **VictimPC** a JeffL et le groupe de sécurité du support technique en tant que membres du groupe d’administrateurs locaux. Comme dans de nombreuses organisations, JeffL est un administrateur sur son propre appareil, **VictimPC**.

En tant qu’administrateur local, configurez des stratégies locales en exécutant le script PowerShell automatisé :

```powerShell
# Add JeffL to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\JeffL"
# Add Helpdesk to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
```

Inspectez le groupe d’administrateurs sur **VictimPC** et assurez-vous qu’il semble avoir au moins le support technique et JeffL en tant que membres :

![le support technique et JeffV doivent se trouver dans le groupe des administrateurs locaux pour VictimPC](media/playbook-labsetup-localgrouppolicies2.png)

### <a name="simulate-helpdesk-support-on-victimpc"></a><a name="helpdesk-simulation"></a> Simulez la prise en charge du support technique sur VictimPC

Pour simuler un réseau actif et géré, créez une tâche planifiée sur la machine **VictimPC** afin d’exécuter le processus « cmd.exe » en tant que **RonHD**.

1. À partir d’une **console PowerShell avec élévation de privilèges** sur VictimPC, exécutez le code suivant :

    ```powerShell
    $action = New-ScheduledTaskAction -Execute 'cmd.exe'
    $trigger = New-ScheduledTaskTrigger -AtLogOn
    $runAs = 'Contoso\RonHD'
    $ronHHDPass = 'FightingTiger$'
    Register-ScheduledTask -TaskName "RonHD Cmd.exe - AATP SA Playbook" -Trigger $trigger -User $runAs -Password $ronHHDPass -Action $action
    ```

1. Connectez-vous à la machine en tant que **JeffL**. Le processus de Cmd.exe démarre dans le contexte de RonHD après l’ouverture de session, simulant la gestion de la machine par le support technique.

### <a name="turn-off-antivirus-on-victimpc"></a>Désactivez l’antivirus sur VictimPC

À des fins de test, désactivez toutes les solutions antivirus en cours d’exécution dans l’environnement de labo. Vous pourrez ainsi vous concentrer sur [!INCLUDE [Product short](includes/product-short.md)] pendant ces exercices, plutôt que sur les techniques permettant de contourner l’antivirus.

Si vous ne commencez pas par désactiver les solutions antivirus, il vous sera impossible de télécharger certains des outils dans la section suivante. De plus, si l’antivirus est activé une fois que les outils d’attaque sont préparés, vous devrez télécharger à nouveau les outils après la désactivation de l’antivirus.

### <a name="stage-common-hacker-tools"></a>Préparez les outils de piratage courants

> [!WARNING]
> Les outils suivants sont présentés uniquement à des fins de recherche. Microsoft ne possède **pas** ces outils et ne peut pas garantir ni ne garantit leur comportement. Ces outils ne doivent être exécutés **que** dans un environnement de labo de test.

Les outils suivants sont nécessaires pour exécuter les playbooks des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)].

| Outil | URL |
|----|-----|
| Mimikatz | [GitHub – Mimikatz](https://github.com/gentilkiwi/mimikatz) |
| PowerSploit | [GitHub – PowerSploit](https://github.com/PowerShellMafia/PowerSploit) |
| PsExec | [Microsoft Docs](/sysinternals/downloads/psexec) |
| NetSess | [Outils JoeWare](https://www.joeware.net/freetools) |

Nous remercions les auteurs de ces outils de recherche d’avoir permis à la communauté de mieux comprendre les cyber risques et leur impact.

### <a name="adminpc-local-policies"></a>Stratégies AdminPC locales

**AdminPC** a besoin d’un **support technique** ajouté au groupe d’administrateurs locaux. Ensuite, supprimez « Administrateurs de domaine » du groupe d’administrateurs locaux. Cette étape permet de s’assurer que Samira, un administrateur de domaine, n’est pas un administrateur d’AdminPC. Il s’agit d’une meilleure pratique en matière de traitement des informations d’identification. Effectuez cette étape manuellement ou utilisez le script PowerShell fourni.

1. Ajoutez **Support technique** à **AdminPC** et *supprimez* « Administrateurs du domaine » du groupe d’administrateurs locaux en exécutant le script PowerShell suivant :

    ```powerShell
    # Add Helpdesk to local Administrators group
    Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
    # Remove Domain Admins from local Administrators group
    Remove-LocalGroupMember -Group "Administrators" -Member "Domain Admins"
    ```

1. Après avoir exécuté le script, **Support technique** se trouve dans la liste locale **Administrateurs** > **Membres** d’**AdminPC**.
![Support technique dans le groupe d’administrateurs locaux pour AdminPC](media/playbook-labsetup-localgrouppolicies1.png)

### <a name="simulate-domain-activities-from-adminpc"></a>Simulez des activités de domaine à partir d’AdminPC

Des activités de domaine simulées sont nécessaires à partir de SamiraA. Cette étape peut être effectuée manuellement, ou à l’aide du script PowerShell fourni. Le script PowerShell accède au contrôleur de domaine toutes les 5 minutes et entraîne dans l’activité réseau simulée en tant que Samira.

En tant que **SamiraA**, exécutez le script suivant dans une invite PowerShell d’AdminPC :

```powerShell
while ($true)
{
    Invoke-Expression "dir \\ContosoDC\c$"
    Start-Sleep -Seconds 300
}
```

### <a name="workstation-setup-checklist"></a>Liste de vérification de la configuration de la station de travail

Passez en revue la liste de vérification pour vous assurer que la configuration de la station de travail est terminée.

| Étape | Agir| Étape | Action | État |
|--|--|--|
| 1 | Ajouter JeffL et le support technique en tant qu’administrateurs locaux sur VictimPC | - [ ] |
| 2 | Créer une tâche planifiée exécutée en tant que RonHD sur VictimPC | - [ ] |
| 3 | Désactivez la solution antivirus sur VictimPC | - [ ] |
| 4 | Outils de piratage préparés sur VictimPC | - [ ] |
| 5 | Ajouter Support technique et supprimer Administrateurs du domaine du groupe d’administrateurs locaux d’AdminPC | - [ ] |
| 6 | Exécutez le script PowerShell en tant que Samira pour simuler des activités de domaine | - [ ] |Exécution du script PowerShell en tant que SamiraA pour simuler des activités de domaine | - [ ] |

## <a name="mission-accomplished"></a>Mission accomplie !

Votre labo [!INCLUDE [Product short](includes/product-short.md)] est maintenant prêt à l’emploi. Les méthodes utilisées dans cette configuration ont été choisies sachant que les ressources doivent être gérées (par *quelque chose* ou *quelqu'un*) et que la gestion nécessite des privilèges d’administrateur local. Il y a d’autres manières de simuler un flux de travail de gestion dans le labo :

- Connexion et déconnexion de VictimPC avec le compte de RonHD
- Ajout d’une autre version d’une tâche planifiée
- Une session RDP
- Exécution de « runas » en ligne de commande

Pour de meilleurs résultats, choisissez une méthode de simulation que vous pouvez automatiser dans votre labo à des fins de cohérence.

## <a name="next-steps"></a>Étapes suivantes

Testez votre environnement de labo [!INCLUDE [Product short](includes/product-short.md)] à l’aide des playbooks des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] pour chacune des phases de la chaîne de cyberattaque, en commençant par la phase de reconnaissance.

> [!div class="nextstepaction"]
> [Playbook de reconnaissance [!INCLUDE [Product short](includes/product-short.md)]](playbook-reconnaissance.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter de [!INCLUDE [Product short](includes/product-short.md)] et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté [!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) !
