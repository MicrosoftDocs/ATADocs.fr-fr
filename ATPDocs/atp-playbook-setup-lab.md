---
title: Tutoriel sur la configuration du labo d’alertes de sécurité Azure ATP | Microsoft Docs
description: Dans ce tutoriel, vous allez configurer un labo de test Azure ATP pour simuler des menaces devant être détectées par Azure ATP.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: shsagir
ms.author: shsagir
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: 8c3238c07c05bf307c91753e6d69b35b376a3c21
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75908515"
---
# <a name="tutorial-setup-an-atp-security-alert-lab"></a>Tutoriel : Configurer un labo d’alertes de sécurité ATP 

 L’objectif du labo d’alerte de sécurité Azure ATP est d’illustrer les capacités d’**Azure ATP** à identifier et à détecter des activités suspectes et des attaques potentielles contre votre réseau. Ce premier tutoriel d’une série en quatre parties vous explique comment créer un environnement de labo de tests de détections *discrètes* d’Azure ATP. Ce labo d’alertes de sécurité se concentre sur les fonctionnalités d’Azure ATP basées sur la *signature*. Ce labo n’inclut pas le Machine Learning avancé, ni les détections de comportements basées sur utilisateur ou l’entité, car celles-ci nécessitent une période d’apprentissage avec un trafic réseau réel pouvant aller jusqu’à 30 jours. Pour plus d’informations sur chaque tutoriel de cette série, consultez la [vue d’ensemble du labo d’alerte de sécurité ATP](atp-playbook-lab-overview.md). 


Dans ce tutoriel vous allez : 

> [!div class="checklist"]
> * configurer votre serveur de labo et vos ordinateurs ;
> * configurer Active Directory avec des utilisateurs et des groupes ;
> * installer et configurer Azure ATP ;
> * configurer les stratégies locales pour votre serveur et vos ordinateurs ;
> * simuler un scénario de gestion du support technique à l’aide d’une tâche planifiée.

## <a name="prerequisites"></a>Prérequis

1. [Un contrôleur de domaine du labo et deux stations de travail de labo](#servers-and-computers).
   - Continuez et [alimentez Active Directory (AD) avec des utilisateurs](#bkmk_hydrate).
1. Une [instance Azure ATP](install-atp-step1.md) qui est [connectée à AD](install-atp-step2.md).
1. [Téléchargez](install-atp-step3.md) et [installez la dernière version du capteur Azure ATP](install-atp-step4.md) sur le contrôleur de domaine de votre labo.
1. Vous êtes familiarisé avec les [stations de travail à accès privilégié](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/privileged-access-workstations) et la [stratégie SAMR](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).

## <a name="recommendations"></a>Recommandations

Nous vous recommandons de suivre d’aussi près que possible les instructions de configuration du labo. Plus votre labo sera proche de la configuration suggérée, plus les procédures de test Azure ATP seront faciles à suivre. Une fois que le labo sera configuré, vous serez prêt à effectuer des actions avec les outils de recherche de piratage suggérés et à passer en revue les détections de ces actions par Azure ATP.

Votre configuration complète du labo doit ressembler le plus possible au diagramme suivant :

![Configuration du labo de test Azure ATP](media/playbook-atp-setup-lab.png)

### <a name="servers-and-computers"></a>Serveurs et ordinateurs

Ce tableau détaille les ordinateurs et les configurations nécessaires. Les adresses IP sont fournies à titre de référence uniquement afin que vous puissiez suivre facilement.

Dans les exemples pour ces tutoriels, le nom NetBIOS de la forêt est **CONTOSO. AZURE**.

|  FQDN | Système d’exploitation | IP | Fonction |
|------|-------|---------|--------------|
| ContosoDC.contoso.azure | Windows Server 2012 R2 | 10.0.24.4 | Contrôleur de domaine avec le capteur Azure ATP installé localement |
| VictimPC.contoso.azure | Windows 10 | 10.0.24.5 |PC de la victime |
| AdminPC.contoso.azure | Windows 10  | 10.0.24.6 | PC de l’administrateur de domaine (parfois appelé « Station de travail d’administrateur sécurisée » ou « Station de travail d’administrateur privilégiée ») |

### <a name="active-directory-users-and-groups"></a>Utilisateurs et groupes Active Directory

Dans ce labo, il y a trois principaux utilisateurs et un compte de service. Le compte de service est destiné à Azure ATP et est utilisé pour la synchronisation LDAP et pour SAMR.

Il existe un groupe de sécurité « Support technique » (SG) dont Ron HelpDesk est membre. Ce groupe de sécurité imite le support technique. Le groupe de sécurité est associé à un objet de stratégie de groupe qui donne des droits d’administrateur local aux membres de notre support technique sur leurs ordinateurs respectifs. Cette configuration est utilisée pour simuler un modèle réaliste d’administration dans un environnement de production.

| Nom complet    | Compte SAM |Fonction|
|--------------|------------|--------------------------------------------------------------------------------------------------|
| Jeff Leatherman  | JeffL  | Bientôt victime d’une attaque par hameçonnage d’une efficacité impressionnante  |
| Ron HelpDesk  | RonHD  |Ron est la « personne à contacter » de l’équipe informatique de Contoso. RonHD est membre du groupe de sécurité « Support technique » . |
| Samira Abbasi | SamiraA  | Chez Contoso, cet utilisateur est notre administrateur de domaine. |
| Service Azure ATP | AATPService | Compte de service d’Azure ATP |

## <a name="azure-atp-base-lab-environment"></a>Environnement de labo de base Azure ATP

Pour configurer le labo de base, nous allons ajouter des utilisateurs et des groupes à Active Directory, modifier une stratégie SAM et un groupe sensible dans Azure ATP.

### <a name="bkmk_hydrate"></a> Alimenter Active Directory avec des utilisateurs sur ContosoDC

Pour simplifier le labo, nous avons automatisé le processus de création d’utilisateurs et de groupes fictifs dans Active Directory. Ce script est exécuté comme une condition préalable à ce tutoriel. Vous pouvez utiliser ou modifier le script pour alimenter l’environnement Active Directory de votre labo. Si vous préférez ne pas utiliser de script, vous pouvez le faire manuellement.

En tant qu’administrateur de domaine, sur ContosoDC, exécutez la commande suivante pour alimenter Active Directory avec des utilisateurs :

``` PowerShell

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

# Take note of the "AATPService" user below which will be our service account for Azure ATP.
# Create new AD user Azure ATP Service

New-ADUser -Name AatpService -DisplayName "Azure ATP/ATA Service" -PasswordNeverExpires $true -AccountPassword $AATPService -Enabled $true

```

### <a name="configure-sam-r-capabilities-from-contosodc"></a>Configurer les fonctionnalités SAM-R à partir de ContosoDC

Pour autoriser le Service Azure ATP à effectuer correctement une énumération SAM-R et créer des chemins de mouvement latéral, vous devez modifier la stratégie SAM.

1. Recherchez votre stratégie SAM sous : **Stratégies \> Paramètres Windows \> Paramètres de sécurité \> Stratégies locales \> Options de sécurité\> « Accès réseau : restreindre les clients autorisés à passer des appels distants à SAM »** _

    ![Modifier la stratégie de groupe pour autoriser Azure ATP à utiliser les fonctionnalités de chemin d’accès de mouvement latéral.](media/playbook-labsetup-localgrouppolicies3.png)

2. Ajoutez le compte de service Azure ATP à la liste des comptes approuvés pour effectuer cette action sur vos systèmes Windows modernes.

    ![Ajoutez le service](./media/samr-add-service.png)

### <a name="add-sensitive-group-to-azure-atp"></a>Ajouter un groupe sensible à Azure ATP

L’ajout du groupe de sécurité « Support technique » en tant que **groupe sensible** vous permettra d’utiliser la fonctionnalité de graphique de mouvement latéral d’Azure ATP. Le balisage d’utilisateurs et de groupes très sensibles qui ne sont pas nécessairement des administrateurs de domaine mais disposent de privilèges pour de nombreuses ressources est une meilleure pratique.

1. Dans le portail Azure ATP, cliquez sur l’icône d’engrenage **Configuration** dans la barre de menus.

2. Sous **Détection**, cliquez sur **Étiquettes d’entité**.

    ![Étiquettes d’entité Azure ATP](media/entity-tags.png)

3. Dans la section **Sensible**, tapez le nom « Support technique » pour **Groupes sensibles**, puis cliquez sur le signe **+** pour les ajouter.

    ![Étiquetez le « Support technique » comme groupe sensible Azure ATP afin d’activer les graphes de mouvement latéral et les rapports pour ce groupe privilégié](media/playbook-labsetup-helpdesksensitivegroup.png)

4. Cliquez sur **Save**.

### <a name="azure-atp-lab-base-setup-checklist"></a>Liste de vérification de la configuration de base du labo Azure ATP

À ce stade, vous devez avoir un labo Azure ATP de base. Azure ATP doit être prêt à l’emploi et les utilisateurs sont en attente. Passez en revue la liste de vérification pour vous assurer que le labo de base est terminé.  

| Étape    | Action | État |
|--------------|------------|------------------|
| 1  | Capteur Azure ATP installé sur ContosoDC (condition préalable)| - [ ] |
| 2  | Les utilisateurs et les groupes sont créés dans Active Directory  | - [ ] |
| 3  | Privilèges du compte de service Azure ATP configurés correctement pour SAMR | - [ ] |
| 4  | Groupe de sécurité de support technique ajouté en tant que **groupe sensible** dans Azure ATP| - [ ] |

## <a name="set-up-the-lab-workstations"></a>Configurer les stations de travail du labo

Après avoir vérifié que votre laboratoire Azure ATP de base est configuré, vous pouvez commencer à configurer la station de travail pour préparer les trois tutoriels suivants de cette série. Nous allons alimenter notre VictimPC et AdminPC pour donner une apparence active à ce labo.

### <a name="victimpc-local-policies"></a>Stratégies VictimPC locales

L’étape suivante pour votre labo consiste à terminer la configuration de la stratégie locale. **VictimPC** a JeffL et le groupe de sécurité du support technique en tant que membres du groupe d’administrateurs locaux. Comme dans de nombreuses organisations, JeffL est un administrateur sur son propre appareil, **VictimPC**.

En tant qu’administrateur local, configurez des stratégies locales en exécutant le script PowerShell automatisé :

``` PowerShell
# Add JeffL to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\JeffL"
# Add Helpdesk to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
```

Inspectez le groupe d’administrateurs sur **VictimPC** et assurez-vous qu’il semble avoir au moins le support technique et JeffL en tant que membres :

![le support technique et JeffV doivent se trouver dans le groupe des administrateurs locaux pour VictimPC](media/playbook-labsetup-localgrouppolicies2.png)

### <a name="helpdesk-simulation"></a> Simulez la prise en charge du support technique sur VictimPC

Pour simuler un réseau actif et géré, créez une tâche planifiée sur la machine **VictimPC** afin d’exécuter le processus « cmd.exe » en tant que **RonHD**.

1. À partir d’une **console PowerShell avec élévation de privilèges** sur VictimPC, exécutez le code suivant :

    ``` PowerShell
    $action = New-ScheduledTaskAction -Execute 'cmd.exe'
    $trigger = New-ScheduledTaskTrigger -AtLogOn
    $runAs = 'Contoso\RonHD'
    $ronHHDPass = 'FightingTiger$'
    Register-ScheduledTask -TaskName "RonHD Cmd.exe - AATP SA Playbook" -Trigger $trigger -User $runAs -Password $ronHHDPass -Action $action
    ```

2. Connectez-vous à la machine en tant que **JeffL**. Le processus de Cmd.exe démarre dans le contexte de RonHD après l’ouverture de session, simulant la gestion de la machine par le support technique.

### <a name="turn-off-antivirus-on-victimpc"></a>Désactivez l’antivirus sur VictimPC

À des fins de test, désactivez toutes les solutions antivirus en cours d’exécution dans l’environnement de labo. Ceci nous permet de nous concentrer sur Azure ATP pendant ces exercices, et non sur les techniques permettant d’échapper à l’antivirus.

Si vous ne commencez pas par désactiver les solutions antivirus, il vous sera impossible de télécharger certains des outils dans la section suivante. De plus, si l’antivirus est activé une fois que les outils d’attaque sont préparés, vous devrez télécharger à nouveau les outils après la désactivation de l’antivirus.

### <a name="stage-common-hacker-tools"></a>Préparez les outils de piratage courants

> [!WARNING]
> Les outils suivants sont présentés uniquement à des fins de recherche. Microsoft ne possède **pas** ces outils et ne peut pas garantir ni ne garantit leur comportement. Ces outils ne doivent être exécutés **que** dans un environnement de labo de test.

Pour exécuter les playbooks d’alerte de sécurité Azure ATP, les outils suivants sont nécessaires.

| Outil | Adresse URL |
|----|-----|
| Mimikatz | [GitHub – Mimikatz](https://github.com/gentilkiwi/mimikatz) |
| PowerSploit | [GitHub – PowerSploit](https://github.com/PowerShellMafia/PowerSploit) |
| PsExec | [Microsoft Docs](https://docs.microsoft.com/sysinternals/downloads/psexec) |
| NetSess | [Outils JoeWare](https://www.joeware.net/freetools) |

Nous remercions les auteurs de ces outils de recherche d’avoir permis à la communauté de mieux comprendre les cyber risques et leur impact.

### <a name="adminpc-local-policies"></a>Stratégies AdminPC locales

**AdminPC** a besoin d’un **support technique** ajouté au groupe d’administrateurs locaux. Ensuite, supprimez « Administrateurs de domaine » du groupe d’administrateurs locaux. Cette étape permet de s’assurer que Samira, un administrateur de domaine, n’est pas un administrateur d’AdminPC. Il s’agit d’une meilleure pratique en matière de traitement des informations d’identification. Effectuez cette étape manuellement ou utilisez le script PowerShell fourni.

1. Ajoutez **Support technique** à **AdminPC** et *supprimez* « Administrateurs du domaine » du groupe d’administrateurs locaux en exécutant le script PowerShell suivant :

    ``` PowerShell
   # Add Helpdesk to local Administrators group
   Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
   # Remove Domain Admins from local Administrators group
   Remove-LocalGroupMember -Group "Administrators" -Member "Domain Admins"

   ```

2. Après avoir exécuté le script, **Support technique** se trouve dans la liste locale **Administrateurs** > **Membres** d’**AdminPC**.
![Support technique dans le groupe d’administrateurs locaux pour AdminPC](media/playbook-labsetup-localgrouppolicies1.png)

### <a name="simulate-domain-activities-from-adminpc"></a>Simulez des activités de domaine à partir d’AdminPC

Des activités de domaine simulées sont nécessaires à partir de SamiraA. Cette étape peut être effectuée manuellement, ou à l’aide du script PowerShell fourni. Le script PowerShell accède au contrôleur de domaine toutes les 5 minutes et entraîne dans l’activité réseau simulée en tant que Samira.

En tant que **SamiraA**, exécutez le script suivant dans une invite PowerShell d’AdminPC :

```PowerShell

while ($true)
{
    Invoke-Expression "dir \\ContosoDC\c$"
    Start-Sleep -Seconds 300
}

```

### <a name="workstation-setup-checklist"></a>Liste de vérification de la configuration de la station de travail

Passez en revue la liste de vérification pour vous assurer que la configuration de la station de travail est terminée.

| Étape    | Action | État |
|--------------|------------|------------------|
| 1  | Ajouter JeffL et le support technique en tant qu’administrateurs locaux sur VictimPC | - [ ] |
| 2  | Créer une tâche planifiée exécutée en tant que RonHD sur VictimPC | - [ ] |
| 3  | Désactivez la solution antivirus sur VictimPC | - [ ] |
| 4  | Outils de piratage préparés sur VictimPC| - [ ] |
| 5  | Ajouter Support technique et supprimer Administrateurs du domaine du groupe d’administrateurs locaux d’AdminPC| - [ ] |
| 6  | Exécutez le script PowerShell en tant que Samira pour simuler des activités de domaine | - [ ] |

## <a name="mission-accomplished"></a>Mission accomplie !

Votre labo Azure ATP est maintenant prêt à l’emploi. Les méthodes utilisées dans cette configuration ont été choisies sachant que les ressources doivent être gérées (par *quelque chose* ou *quelqu'un*) et que la gestion nécessite des privilèges d’administrateur local. Il y a d’autres manières de simuler un flux de travail de gestion dans le labo :

- Connexion et déconnexion de VictimPC avec le compte de RonHD
- Ajout d’une autre version d’une tâche planifiée
- Une session RDP
- Exécution d’un « runas » dans la ligne de commande

 Pour de meilleurs résultats, choisissez une méthode de simulation que vous pouvez automatiser dans votre labo à des fins de cohérence.


## <a name="next-steps"></a>Étapes suivantes

Testez votre environnement de labo Azure ATP à l’aide des playbooks d’alertes de sécurité d’Azure ATP pour chaque phase de la chaîne de destruction de cyber-attaque en commençant par la phase de reconnaissance.  

> [!div class="nextstepaction"]
> [Playbook de reconnaissance Azure ATP](atp-playbook-reconnaissance.md)


## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) dès aujourd’hui !

