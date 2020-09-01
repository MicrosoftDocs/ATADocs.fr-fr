---
title: Playbook de mouvement latéral d’alertes de sécurité Azure ATP
description: Le playbook Azure ATP décrit comment simuler des menaces de mouvement latéral pour la détection par Azure ATP.
ms.service: azure-advanced-threat-protection
ms.topic: how-to
author: shsagir
ms.author: shsagir
ms.date: 03/03/2019
ms.reviewer: itargoet
ms.openlocfilehash: 03eaafcb803a4cb443ad97f488ab83c690dadffa
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88955392"
---
# <a name="tutorial-lateral-movement-playbook"></a>Tutoriel : Playbook de mouvement latéral

Le playbook de mouvement latéral est le troisième de la série de tutoriels en quatre parties pour les alertes de sécurité Azure ATP. L’objectif du labo d’alerte de sécurité Azure ATP est d’illustrer les capacités d’**Azure ATP** à identifier et à détecter des activités suspectes et des attaques potentielles contre votre réseau. Le playbook explique comment tester certaines détections *discrètes* d’Azure ATP. Ce playbook se concentre sur les capacités d’Azure ATP basée sur la *signature* et n’inclut ni le Machine Learning avancé, ni les détections de comportements basées utilisateur ou entité (qui nécessitent une période d’apprentissage avec un trafic réseau réel pouvant aller jusqu’à 30 jours). Pour plus d’informations sur chaque tutoriel de cette série, consultez la [vue d’ensemble du labo d’alerte de sécurité ATP](atp-playbook-lab-overview.md).

Ce playbook montre certaines détections de menaces du chemin d'accès de mouvement latéral et certains services d’alertes de sécurité Azure ATP en simulant une attaque avec des outils de piratage et d’attaque courants, réels et accessibles au public.

Dans ce tutoriel vous allez :
> [!div class="checklist"]
> * collecter des codes de hachage NTLM et simuler une attaque Overpass-the-Hash pour obtenir un ticket TGT (Ticket Granting) Kerberos ;
> * usurper l’identité d’un autre utilisateur, se déplacer latéralement sur le réseau et collecter plus d’informations d’identification ;
> * simuler une attaque Pass-the-Ticket pour accéder au contrôleur de domaine ;
> * passer en revue les alertes de sécurité à partir du mouvement latéral dans Azure ATP.

## <a name="prerequisites"></a>Prérequis

1. [Un labo d’alerte de sécurité ATP terminé](atp-playbook-setup-lab.md) 
     - Nous vous recommandons de suivre d’aussi près que possible les instructions de configuration du labo. Plus votre labo sera proche de la configuration suggérée, plus les procédures de test Azure ATP seront faciles à suivre.

2. [Achèvement du didacticiel du playbook de reconnaissance](atp-playbook-reconnaissance.md)

## <a name="lateral-movement"></a>Déplacement latéral

Grâce à nos attaques simulées dans le tutoriel précédent, le playbook de reconnaissance, nous avons obtenu des informations réseau détaillées. À l’aide de ces informations, notre objectif durant cette phase de mouvement latéral du labo est d’accéder aux adresses IP de valeur critique déjà découvertes et de voir les alertes d’Azure ATP sur le déplacement. Dans la simulation de labo de reconnaissance précédente, nous avons identifié 10.0.24.6 en tant qu’adresse IP cible, celle où les informations d’identification de l’ordinateur de SamiraA étaient exposées. Nous allons simuler différentes méthodes d’attaque pour essayer de nous déplacer latéralement sur le domaine.

## <a name="dump-credentials-in-memory-from-victimpc"></a>Vider les informations d’identification en mémoire à partir de VictimPC

Au cours de nos attaques de reconnaissance factices, **VictimPC** n’a pas été exposée uniquement aux informations d’identification de JeffL. Il y a d’autres comptes utiles à découvrir sur cet ordinateur. Pour obtenir un mouvement latéral à l’aide de **VictimPC**, nous allons tenter d’énumérer des informations d’identification en mémoire sur la ressource partagée. Le vidage des informations d’identification en mémoire à l’aide de **mimikatz** est une méthode d’attaque populaire avec un outil commun.

### <a name="mimikatz-sekurlsalogonpasswords"></a>Mimikatz sekurlsa::logonpasswords

1. Ouvrez une **invite de commandes avec élévation de privilèges** sur **VictimPC**. 
1. Accédez au dossier d’outils où vous avez enregistré Mimikatz et exécutez la commande suivante :

   ``` cmd
   mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit" >> c:\temp\victimcpc.txt
   ```

1. Ouvrez **c:\\temp\\victimpc.txt** pour afficher les informations d’identification collectées et écrites par Mimikatz dans le fichier txt.
    ![Résultat de Mimikatz, y compris le code de hachage NTLM de RonHD](media/playbook-lateral-sekurlsa-logonpasswords-output.png)

1. Nous avons pu collecter le code de hachage NTLM de RonHD à partir de la mémoire avec mimikatz. Nous aurons besoin du code de hachage NTLM sous peu.

   > [!Important]
   > - Il est prévu et normal que les codes de hachage illustrés dans cet exemple soient différents des codes de hachage que vous voyez dans votre propre environnement de labo. L’objectif de cet exercice est de vous aider à comprendre comment les codes de hachage ont été obtenus, d’obtenir leurs valeurs et de les utiliser dans les étapes suivantes. </br> </br>
   > - Les informations d’identification du compte d’ordinateur ont également été exposées lors de cette collecte. Alors que la valeur d’informations d’identification du compte d’ordinateur n’est pas utile dans notre labo actuel, n’oubliez pas de qu'il s’agit d’un autre moyen utilisé par les attaquants réel pour obtenir un mouvement latéral dans votre environnement.

### <a name="gather-more-information-about-the-ronhd-account"></a>Collecter plus d’informations sur le compte RonHD

Un attaquant peut ne pas savoir initialement qui est RonHD ou ne pas connaître sa valeur en tant que cible. Tout qu’il sait est qu’il peut utiliser les informations d’identification s’il est avantageux de le faire. Toutefois, à l’aide de la commande **net** nous, agissant comme un attaquant, pouvons découvrir de quels groupes RonHD est membre.

À partir de **VictimPC**, exécutez la commande suivante :

   ``` cmd
   net user ronhd /domain
   ```

![Reconnaissance sur le compte de RonHD](media/playbook-lateral-sekurlsa-logonpasswords-ronhd_discovery.png)

Il ressort des résultats que RonHD est membre du groupe de sécurité « Support technique ». Nous savons que RonHD nous donne des privilèges liés au compte *et* avec le groupe de sécurité du support technique.

### <a name="mimikatz-sekurlsapth"></a>Mimikatz sekurlsa::pth

À l’aide d’une technique courante appelée **Overpass-the-Hash**, le code de hachage NTLM collecté est utilisé pour obtenir un Ticket TGT (Ticket Granting). Avec le ticket TGT d’un utilisateur, un attaquant peut usurper l’identité un utilisateur compromis tels que RonHD. En usurpant l’identité en tant que RonHD, nous pouvons accéder à n’importe quelle ressource de domaine à laquelle l’utilisateur compromis ou ses groupes de sécurité respectifs ont accès.

1. À partir de **VictimPC**, accédez au répertoire contenant le dossier **Mimikatz.exe**. emplacement de stockage sur votre système de fichiers et exécutez la commande suivante :

   ``` cmd
   mimikatz.exe "privilege::debug" "sekurlsa::pth /user:ronhd /ntlm:96def1a633fc6790124d5f8fe21cc72b /domain:contoso.azure" "exit"
   ```

   > [!Note]
   > Si votre code de hachage pour RonHD était différent dans les étapes précédentes, remplacez le code de hachage NTLM ci-dessus par le code de hachage collecté auprès de *victimpc.txt*.

    ![Overpass-the-hash par le biais de mimikatz](media/playbook-lateral-opth1.png)

1. Vérifiez qu’une nouvelle invite de commandes s’ouvre. Elle s’exécute en tant que RonHD, mais il est possible que cela ne soit pas *encore* évident. Ne fermez pas la nouvelle invite de commande, car vous allez l’utiliser ensuite.

Azure ATP ne détecte pas un code de hachage passé sur une ressource locale. Azure ATP détecte lorsqu’un code de hachage est **utilisé à partir d’une ressource pour accéder à une autre** ressource ou à un autre service.

### <a name="additional-lateral-move"></a>Déplacement latéral supplémentaire

Maintenant, avec les informations d’identification de RonHD, pouvons-nous accéder aux informations d’identification de JeffL, ce qui n’était pas possible avant ?
Nous allons utiliser **PowerSploit** ```Get-NetLocalGroup``` pour nous aider à répondre à cette question.

1. Dans la console de commande ouverte en raison de notre attaque précédente, en cours d’exécution en tant que RonHD, exécutez les éléments suivants :

   ``` PowerShell
   powershell
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
   Import-Module C:\tools\PowerSploit\PowerSploit.psm1 -Force
   Get-NetLocalGroup 10.0.24.6
   ```

    ![Obtenir les administrateurs locaux pour 10.0.24.6 via PowerSploit](media/playbook-lateral-adminpcsamr.png)

   Dans les coulisses, cet exemple utilise la gestion des actifs logiciels à distance pour identifier les administrateurs locaux pour l’adresse IP que nous avons découvert précédemment et qui a été exposée à un compte d’administrateur de domaine.

   Notre résultat doit ressembler à :

    ![Résultat de PowerSploit Get-NetLocalGroup](media/playbook-lateral-adminpcsamr_results.png)

   Cet ordinateur a deux administrateurs locaux, l’administrateur intégré « ContosoAdmin » et « Support technique ». Nous savons que RonHD est membre du groupe de sécurité « Support technique ». On nous a également donné le nom de l’ordinateur, AdminPC. Étant donné que nous avons les informations d’identification de RonHD, nous devrions pouvoir les utiliser pour nous déplacer latéralement vers AdminPC et d’accéder à cet ordinateur.

1. À partir de la *même invite de commandes, qui s’exécute dans le contexte de RonHD*, tapez **quitter** sortir de PowerShell si nécessaire. Exécutez ensuite la commande suivante :

   ``` cmd
   dir \\adminpc\c$
   ```

1. Nous avons pu accéder à AdminPC. Voyons quels tickets nous avons. Dans la même invite de commandes, exécutez la commande suivante :

   ``` cmd
   klist
   ```

    ![Utilisez klist pour nous montrer des tickets Kerberos dans notre processus cmd.exe en cours](media/playbook-lateral-klist.png)

Vous pouvez voir que, pour ce processus particulier, nous avons un TGT de RonHD en mémoire. Nous avons effectué avec succès une attaque Overpass-the-Hash dans notre labo. Nous avons converti le code de hachage NTLM compromis précédemment et l’avons utilisé pour obtenir un TGT Kerberos. Ce TGT Kerberos a été ensuite utilisé pour accéder à une autre ressource réseau, dans le cas présent, AdminPC. 

### <a name="overpass-the-hash-detected-in-azure-atp"></a>Overpass-the-Hash détecté dans Azure ATP

En examinant la console Azure ATP, nous pouvons voir les opérations suivantes :

![Détection de l’attaque Overpass-the-Hash par Azure ATP](media/playbook-lateral-opthdetection.png)

Azure ATP a détecté que le compte de RonHD a été compromis sur VictimPC, puis utilisé pour réussir à obtenir un TGT Kerberos. Si nous cliquons sur le nom de RonHD dans l’alerte, nous sommes dirigés vers la chronologie des activités logiques de RonHD, où nous pouvons approfondir notre recherche.

![Afficher la détection dans la chronologie des activités logiques](media/playbook-lateral-opthlogicalactivity.png)

Dans le centre d’opérations de sécurité, l’attention de notre analyste de sécurité est attirée par les informations d’identification compromises et il peut examiner rapidement les ressources ayant fait l’objet d’un accès.

## <a name="domain-escalation"></a>Élévation de domaine

Du fait de notre attaque simulée, nous n’avons pas seulement accès à AdminPC, mais nous avons également validé des privilèges d’administrateur sur AdminPC. Nous pouvons maintenant nous déplacer latéralement vers AdminPC et collecter des informations d’identification supplémentaires.

Nous allons ici :

* préparer Mimikatz sur AdminPC ;
* collecter des tickets sur AdminPC ;
* effectuer Pass-the-ticket pour devenir SamiraA.

### <a name="pass-the-ticket"></a>Pass-the-ticket

À partir de l’invite de commandes exécutée dans le contexte de *RonHD* sur **VictimPC**, accédez à l’emplacement où se trouvent nos outils d’attaque courants. Ensuite, exécutez xcopy pour les déplacer vers l’ordinateur AdminPC :

``` cmd
xcopy mimikatz.exe \\adminpc\c$\temp
```

Appuyez sur ```d``` lorsque vous y êtes invité, en indiquant que le dossier « temp » est un répertoire sur AdminPC.

![Copier des fichiers vers AdminPC](media/playbook-escalation-xcopy1.png)

### <a name="mimikatz-sekurlsatickets"></a>Mimikatz sekurlsa::tickets

Avec Mimikatz préparé sur AdminPC, nous allons utiliser PsExec pour l’exécuter à distance.

1. Allez à l’emplacement de PsExec et exécutez la commande suivante :

   ``` cmd
   PsExec.exe \\AdminPC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "sekurlsa::tickets /export" "exit")
   ```

   Cette commande exécute et exporte les tickets trouvés dans le processus LSASS.exe et les place dans le répertoire actuel, sur AdminPC.

1. Nous devons copier les tickets pour les faire revenir d’AdminPC à VictimPC. Comme nous nous intéressons uniquement aux tickets de SamiraA pour cet exemple, exécutez la commande suivante :

   ``` cmd
   xcopy \\adminpc\c$\temp\*SamiraA* c:\temp\adminpc_tickets
   ```

    ![Exporter les informations d’identification collectées d’AdminPC vers VictimPC](media/playbook-escalation-export_tickets2.png)

1. Nous allons effacer nos traces sur AdminPC en supprimant nos fichiers.

   ``` cmd
   rmdir \\adminpc\c$\temp /s /q
   ```

   > [!Note]
   > Les pirates plus sophistiquées ne touchent pas au disque lorsqu’ils exécutent du code arbitraire sur un ordinateur après avoir obtenu des privilèges d’administrateur sur ce dernier.

   Sur notre **VictimPC**, ces tickets collectés se trouvent dans notre dossier **c:\temp\adminpc_tickets** :

    ![C:\temp\tickets est résultat mimikatz exporté à partir d’AdminPC](media/playbook-escalation-export_tickets4.png)


### <a name="mimikatz-kerberosptt"></a>Mimikatz Kerberos::ptt

Avec les tickets localement sur VictimPC, il est maintenant temps de devenir SamiraA par « En passant le Ticket ».

1. À partir de l’emplacement de **Mimikatz** sur le système de fichiers de **VictimPC**, ouvrez une nouvelle **invite de commandes avec élévation de privilèges** et exécutez la commande suivante :

   ``` cmd
   mimikatz.exe "privilege::debug" "kerberos::ptt c:\temp\adminpc_tickets" "exit"
   ```

    ![Importez les tickets volés dans le processus cmd.exe](media/playbook-escalation-ptt1.png)

1. Dans la même invite de commandes avec élévation de privilèges, vous devez valider que la session d’invite de commandes comprend les tickets adéquats. Exécutez la commande suivante :

   ``` cmd
   klist
   ```

    ![Exécutez klist pour afficher les tickets importés dans le processus CMD](media/playbook-escalation-ptt2.png)

1. Notez que ces tickets restent inutilisés. En agissant comme un attaquant, nous avons réussi à « passer le ticket ». Nous avons collecté les informations d’identification de SamirA dans AdminPC avant de les passer à un autre processus s’exécutant sur VictimPC.

   > [!Note]
   > Comme dans Pass-the-Hash, Azure ATP ne sait pas que le ticket a été passé à l’activité du client local. Cependant, Azure ATP détecte l’activité *une fois que le ticket est utilisé*, autrement dit, exploité pour accéder à une autre ressource/un autre service.

1. Terminez votre attaque simulée en accédant au contrôleur de domaine à partir de **VictimPC**. Dans l’invite de commandes maintenant en cours d’exécution avec les tickets de SamirA en mémoire, exécutez :

   ``` cmd
   dir \\ContosoDC\c$
   ```

    ![Accédez au lecteur c:\ de ContosoDC à l’aide des informations d’identification de SamirA](media/playbook-escalation-ptt3.png)

Bravo ! Nos attaques fictives nous ont permis d’accéder en tant qu’administrateur à notre contrôleur de domaine et de réussir à compromettre le domaine/la forêt Active Directory de notre labo.

### <a name="pass-the-ticket-detection-in-azure-atp"></a>Passer la détection de ticket dans Azure ATP

La plupart des outils de sécurité n’ont aucun moyen de détecter l’utilisation d’informations d’identification légitimes pour accéder à une ressource légitime. En revanche, qu’est-ce qui est l’objet d’une détection et d’une alerte par Azure ATP dans cette chaîne d’événements ?

- Azure ATP a détecté le vol des tickets de Samira sur AdminPC et le mouvement vers VictimPC.
- Le portail Azure ATP indique exactement les ressources qui étaient accessibles à l’aide des tickets volés.
- Il fournit des informations clés et des preuves pour identifier exactement où commencer votre investigation et quelles mesures prendre pour y remédier.

Les détections Azure ATP et les informations d’alerte ont une valeur critique pour toute équipe de réponse à des incidents forensiques numériques (DFIR). Vous pouvez non seulement voir les informations d’identification volées, mais encore découvrir les ressources ayant fait l’objet d’un accès et d’une compromission avec le ticket volé.

![Azure ATP détecte Pass-the-Ticket avec une suppression de deux heures](media/playbook-escalation-pttdetection.png)

> [!NOTE]
> Cet événement ne s’affichera sur la console Azure ATP que dans **2 heures**. Les événements de ce type sont délibérément supprimés pendant cet intervalle de temps pour réduire les faux positifs.

## <a name="next-steps"></a>Étapes suivantes
La phase suivante dans la chaîne de destruction d’attaque est le contrôle du domaine.

> [!div class="nextstepaction"]
> [Playbook de contrôle du domaine Azure ATP](atp-playbook-domain-dominance.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) dès aujourd’hui !
