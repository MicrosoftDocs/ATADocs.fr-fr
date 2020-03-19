---
title: Playbook de contrôle du domaine Azure ATP
description: Le playbook Azure ATP de contrôle du domaine décrit comment simuler des attaques de contrôle du domaine devant être détectées par Azure ATP
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: shsagir
ms.author: shsagir
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: b5903123e992f7540dd660da605a1568bf76ef91
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414588"
---
# <a name="tutorial-domain-dominance-playbook"></a>Tutoriel : Playbook de contrôle du domaine

Le dernier tutoriel de cette série en quatre parties sur les alertes de sécurité Azure ATP est un playbook de contrôle du domaine. L’objectif du labo d’alerte de sécurité Azure ATP est d’illustrer les capacités d’**Azure ATP** à identifier et à détecter des attaques potentielles contre votre réseau. Le labo explique comment tester certaines détections *discrètes* d’Azure ATP à l’aide des fonctionnalités d’Azure ATP *basées sur la signature*. Les tutoriels n’incluent ni le Machine Learning avancé Azure ATP, ni les détections et les alertes de comportement d’utilisateurs ou basées sur des entités. Ces types de détections et d’alertes ne sont pas inclus dans le test, car ils nécessitent une période d’apprentissage et un trafic réseau réel pouvant aller jusqu’à 30 jours. Pour plus d’informations sur chaque tutoriel de cette série, consultez la [vue d’ensemble du labo d’alerte de sécurité ATP](atp-playbook-lab-overview.md).

Ce playbook montre certaines détections de menaces de contrôle du domaine et certains services d’alertes de sécurité d’Azure ATP à l’aide d’attaques simulées à partir d’outils de piratage et d’attaque courants, réels et accessibles au public. Les méthodes concernées sont généralement utilisées à ce stade de la chaîne de destruction de cyberattaque pour obtenir le contrôle persistant du domaine.

Dans ce tutoriel, vous allez simuler des tentatives de prendre le contrôle persistant du domaine afin de passer en revue chacune des détections d’Azure ATP pour les méthodes courantes suivantes :

> [!div class="checklist"]
> * Exécution de code à distance
> * API de protection des données (DPAPI)
> * Réplication malveillante
> * Création de service
> * Skeleton Key
> * Golden Ticket


## <a name="prerequisites"></a>Prérequis

1. [Un labo d’alerte de sécurité ATP terminé](atp-playbook-setup-lab.md) 
     - Nous vous recommandons de suivre d’aussi près que possible les instructions de configuration du labo. Plus votre labo sera proche de la configuration suggérée, plus les procédures de test Azure ATP seront faciles à suivre.

2. [Dernière étape du didacticiel du playbook de mouvement latéral](atp-playbook-lateral-movement.md)

## <a name="domain-dominance"></a>Contrôle du domaine

Dans la chaîne de destruction de cyberattaque, pendant la phase de contrôle du domaine, un attaquant a déjà obtenu des informations d’identification légitimes pour accéder à votre contrôleur de domaine. Le fait qu’un attaquant ait accès à votre contrôleur de domaine signifie que tous les niveaux de votre réseau peuvent subir des dommages. Outre les dommages immédiats, les attaquants, en particulier les plus sophistiqués, aiment placer des *stratégies d’assurance* supplémentaires dans les environnements qu’ils ont compromis. Lors de telles attaques, même si la mise en danger et les actions initiales de l’attaquant sont découvertes, ce dernier a toujours d’autres possibilités de rester dans votre domaine, ce qui augmente ses chances de réussite à long terme.

### <a name="remote-code-execution"></a>Exécution de code à distance

L’exécution de code à distance porte bien son nom. Des attaquants se donnent les moyens d’exécuter du code à distance sur une ressource, dans notre cas un contrôleur de domaine. Nous allons essayer d’utiliser conjointement ces outils courants pour exécuter du code à distance et prendre le contrôle permanent du contrôleur de domaine, puis de voir ce qu’Azure ATP nous montre.

- Windows Management Instrumentation (WMI)
- PsExec à partir de SysInternals

À l’aide de WMI via la ligne de commande, essayez de créer localement un processus sur le contrôleur de domaine pour créer un utilisateur nommé « InsertedUser » avec le mot de passe : pa$ $w0rd1.

1. Ouvrez la ligne de commande en cours d’exécution dans le contexte de *SamiraA* à partir de **VictimPC** et exécutez la commande suivante :

   ``` cmd
   wmic /node:ContosoDC process call create "net user /add InsertedUser pa$$w0rd1"
   ```

2. L’utilisateur étant maintenant créé, ajoutez-le au groupe « Administrateurs » sur le contrôleur de domaine :

   ``` cmd
   PsExec.exe \\ContosoDC -accepteula net localgroup "Administrators" InsertedUser /add
   ```

   ![Utilisez l’exécution de code à distance (PsExec) pour ajouter le nouvel utilisateur au groupe des administrateurs sur le contrôleur de domaine](media/playbook-dominance-psexec_addtoadmins.png)

3. Accédez à **Utilisateurs et ordinateurs Active Directory (ADUC)** sur **ContosoDC** et recherchez **InsertedUser**. 

4. Cliquez avec le bouton droit sur **Propriétés** et vérifiez l’appartenance.

   ![Afficher les propriétés d'« InsertedUser »](media/playbook-dominance-inserteduser_properties.png)

En agissant comme un attaquant, vous avez pu créer un nouvel utilisateur dans votre labo à l’aide de WMI. Vous avez également ajouté le nouvel utilisateur au groupe Administrateurs à l’aide de PsExec. Du point de vue de la persistance, d’autres informations d’identification légitimes indépendantes ont été créées sur le contrôleur de domaine. De nouvelles informations d’identification permettent à un attaquant d’avoir accès en permanence au contrôleur de domaine si l’accès précédemment obtenu avec des informations d'identification a été découvert et supprimé.

### <a name="remote-code-execution-detection-in-azure-atp"></a>Détection de l’exécution de code à distance dans Azure ATP

Connectez-vous au portail Azure ATP pour vérifier ce qui, le cas échéant, a été détecté par Azure ATP à la suite de notre dernière attaque simulée :

![Détection de l’exécution de code à distance par Azure ATP](media/playbook-dominance-wmipsexecdetected.png)

Azure ATP a détecté les exécutions de code à distance de WMI et de PsExec.

En raison du chiffrement de la session WMI, certaines valeurs telles que les méthodes WMI réelles ou le résultat de l’attaque ne sont pas visibles. Toutefois, la détection de ces actions par Azure ATP nous fournit des informations idéales pour prendre des mesures défensives.  

VictimPC, l’ordinateur, ne doit jamais exécuter de code à distance sur les contrôleurs de domaine.

Comme Azure ATP apprend qui est inséré dans les groupes de sécurité au fil du temps, des activités suspectes similaires sont identifiées comme étant anormales au fil du temps. Dans la mesure où ce labo a été créé récemment et est toujours en période d’apprentissage, cette activité ne s’affichera pas en tant qu’alerte. La détection de modification du groupe de sécurité par Azure ATP peut être validée en vérifiant la chronologie des activités. Azure ATP vous permet également de créer des rapports sur toutes les modifications du groupe de sécurité, Ils peuvent vous être envoyés par e-mail de manière proactive.

Accédez à la page **Administrateur** dans le portail Azure ATP à l’aide de l’outil de recherche. La détection de l’insertion d’utilisateurs par Azure ATP s’affiche dans la chronologie des activités du groupe d’administrateurs.

![L’affichage a ajouté un utilisateur au groupe de sécurité sensible](media/playbook-dominance-admininserteduser.png)

### <a name="data-protection-api-dpapi"></a>API de protection des données (DPAPI)

L’API de protection des données (DPAPI) est utilisée par Windows pour protéger en toute sécurité les mots de passe enregistrés par les navigateurs et les fichiers chiffrés, ainsi que les autres données sensibles. Les contrôleurs de domaine détiennent une clé principale qui peut déchiffrer *tous* les secrets sur des machines Windows jointes au domaine.

À l’aide de **mimikatz**, nous allons tenter d’exporter la clé principale à partir du contrôleur de domaine. 

1. Exécutez la commande suivante sur le contrôleur de domaine :

   ``` cmd
   mimikatz.exe "privilege::debug" "lsadump::backupkeys /system:ContosoDC.contoso.azure /export" "exit"
   ```

   ![Utilisation de mimikatz pour exporter la clé de sauvegarde DPAPI à partir d’Active Directory](media/playbook-dominance-dpapi_mimikatz.png)

2. Vérifiez que le fichier de clé principale a bien été exporté. Recherchez dans le répertoire à partir duquel vous avez exécuté mimikatz.exe pour afficher les fichiers .der, .pfx, .pvk et .key créés. Copiez la clé héritée à partir de l’invite de commandes.

En tant qu’attaquants, nous disposons maintenant de la clé qui nous permettra de déchiffrer les fichiers chiffrés par DPAPI/les données sensibles à partir de *n’importe quelle* machine dans toute la forêt.

### <a name="dpapi-detection-in-azure-atp"></a>Détection de DPAPI dans Azure ATP

À l’aide du portail Azure ATP, vérifions qu’Azure ATP a réussi à détecter notre attaque sur la DPAPI :

![Azure ATP a détecté la demande DPAPI](media/playbook-dominance-dpapidetected.png)

### <a name="malicious-replication"></a>Réplication malveillante

La réplication malveillante permet à un attaquant de répliquer les informations de l’utilisateur à l’aide des informations d'identification de l’administrateur de domaine (ou d’un équivalent). La réplication malveillante permet essentiellement à un attaquant de collecter à distance des informations d’identification. Le compte le plus critique en termes de tentatives de collecte est apparemment « krbtgt », car il s’agit de la clé principale utilisée pour signer tous les tickets Kerberos.

Les deux jeux d’outils de piratage courants permettant aux attaquants de tenter une réplication malveillante sont **Mimikatz** et **Impacket** de Core Security.

#### <a name="mimikatz-lsadumpdcsync"></a>Mimikatz lsadump::dcsync

À partir de **VictimPC**, dans le contexte de **SamirA**, exécutez la commande Mimikatz suivante :

``` cmd
mimikatz.exe "lsadump::dcsync /domain:contoso.azure /user:krbtgt" "exit" >> c:\temp\ContosoDC_krbtgt-export.txt
```

Nous avons répliqué les informations de compte « krbtgt » sur : c:\\temp\\ContosoDC_krbtgt-export.txt

![Réplication malveillante via mimikatz](media/playbook-dominance-maliciousrep_mimikatz.png)

#### <a name="malicious-replication-detection-in-azure-atp"></a>Détection de réplication malveillantes dans Azure ATP

À l’aide du portail Azure ATP, vérifiez que le SOC est au courant de la réplication malveillante que nous avons simulée à partir de VictimPC.

![Réplication malveillante détectée par Azure ATP](media/playbook-dominance-maliciousrep_detected.png)

### <a name="skeleton-key"></a>Skeleton Key

Une autre méthode de contrôle de domaine utilisée par les attaquants est connue sous le nom de **Skeleton Key**. À l’aide d’un Skeleton Key créé par l’attaquant, l’attaquant peut usurper l’identité de *n’importe quel utilisateur* à *tout moment*. Lors d’une attaque Skeleton Key, chaque utilisateur peut toujours se connecter avec son mot de passe normal, mais chacun de ses comptes est également doté d’un mot de passe principal. Le nouveau mot de passe principal ou Skeleton Key donne accès au compte à toute personne qui le connaît. Une attaque Skeleton Key est effectuée par le biais d’une mise à jour corrective du processus LSASS.exe sur le contrôleur de domaine, ce qui oblige les utilisateurs à s’authentifier via un type de chiffrement d’une version antérieure.

Utilisons un Skeleton Key pour voir comment fonctionne ce type d’attaque :

1. Déplacez **mimikatz** vers **ContosoDC** à l’aide des informations d'identification de **SamirA** collectées préalablement. Veillez à transmettre l’architecture appropriée de **mimikatz.exe** selon le type d’architecture du contrôleur de domaine (64 bits ou 32 bits). À partir du dossier **mimikatz**, exécutez :

   ``` cmd
   xcopy mimikatz.exe \\ContosoDC\c$\temp
   ```

2. Une fois **mimikatz** transféré sur le contrôleur de domaine, l’exécuter à distance par le biais de PsExec :

   ``` cmd
   PsExec.exe \\ContosoDC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "misc::skeleton" ^& "exit")
   ```

3. Vous avez réussi à corriger le processus LSASS sur **ContosoDC**.

   ![Attaque Skeleton Key par le biais de mimikatz](media/playbook-dominance-skeletonkey.png)

### <a name="exploiting-the-skeleton-key-patched-lsass"></a>Exploitation du Skeleton Key corrigé LSASS

Sur **VictimPC**, ouvrez une invite de commande (dans le contexte de **JeffL**), exécutez la commande suivante pour tenter de devenir le contexte de RonHD.

``` cmd
runas /user:ronhd@contoso.azure "notepad"
```

Lorsque vous y êtes invité, utilisez le mot de passe incorrect exprès. Cette action prouve que le compte a *toujours* un mot de passe après l’exécution de l’attaque.  

![Utilisation d’un mot de passe *incorrect* après une attaque Skeleton Key (cette méthode fonctionne exactement comme indiqué)](media/playbook-dominance-skeletonkey_wrong.png)

Mais Skeleton Key ajoute un mot de passe supplémentaire à chaque compte. Effectuez à nouveau la commande « runas », mais cette fois utilisez « mimikatz » comme mot de passe.

``` cmd
runas /user:ronhd@contoso.azure "notepad"
```

Cette commande crée un nouveau processus, *le bloc-notes*, qui s’exécute dans le contexte de RonHD. **Skeleton Key peut être effectué pour _n’importe quel_ compte, notamment les comptes de services et les comptes d’ordinateurs.**

> [!Important]
> Il est important de redémarrer ContosoDC après avoir exécuté l’attaque Skeleton Key. Sinon, le processus LSASS.exe sur ContosoDC sera corrigé et modifié, entraînant la rétrogradation de chaque demande d’authentification à RC4.

### <a name="skeleton-key-attack-detection-in-azure-atp"></a>Détection d’attaque Skeleton Key dans Azure ATP

Qu’est-ce qu’Azure ATP a détecté et signalé pendant que tout cela se passait ?

![Attaque Skeleton Key détectée par Azure ATP](media/playbook-dominance-skeletonkey_detected.png)

Azure ATP a pu détecter la méthode de chiffrement suspecte de l’authentification préalable utilisée pour cet utilisateur.

### <a name="golden-ticket---existing-user"></a>Golden ticket – utilisateur existant

Après avoir volé le « Golden Ticket », (compte « krbtgt ») comme c’est expliqué [ici par le biais de la réplication malveillante](#malicious-replication), un attaquant est en mesure de signer des tickets *comme s’il était le contrôleur de domaine*. **Mimikatz**, le SID de domaine et le compte « krbtgt » volé sont tous nécessaires pour accomplir cette attaque. Non seulement nous pouvons générer des tickets pour un utilisateur, mais encore nous pouvons générer des tickets pour des utilisateurs qui n’existent même pas.

1. En tant que JeffL, exécutez la commande sur ci-dessous sur **VictimPC** pour acquérir le SID du domaine :

   ``` cmd
   whoami /user
   ```

   ![SID pour utilisateur de golden ticket](media/playbook-dominance-golden_whoamisid.png)

2. Identifiez et copier le SID de domaine mis en surbrillance dans la capture d’écran ci-dessus.

3. À l’aide de **mimikatz**, prenez le SID de domaine copié ainsi que le code de hachage NTLM « krbtgt » volé de l’utilisateur pour générer le TGT. Insérez le texte suivant dans un cmd.exe comme JeffL :

   ``` cmd
   mimikatz.exe "privilege::debug" "kerberos::golden /domain:contoso.azure /sid:S-1-5-21-2839646386-741382897-445212193 /krbtgt:c96537e5dca507ee7cfdede66d33103e /user:SamiraA /ticket:c:\temp\GTSamiraA_2018-11-28.kirbi /ptt" "exit"
   ```

   ![Créer le Golden Ticket](media/playbook-dominance-golden_generate.png)

   La partie ```/ptt``` de la commande nous a permis de passer immédiatement le ticket généré en mémoire.

4. Assurons-nous que les informations d’identification sont en mémoire.  Exécutez ```klist``` dans la console.

   ![résultats klist après la transmission du ticket généré](media/playbook-dominance-golden_klist.png)

5. En tant qu’attaquant, exécutez la commande pass-the-ticket suivante à utiliser sur le contrôleur de domaine :

   ``` cmd
   dir \\ContosoDC\c$
   ```

   Bravo ! Vous avez généré un **faux** golden ticket pour SamiraA.

   ![Exécutez golden ticket via mimikatz](media/playbook-dominance-golden_ptt.png)

Pourquoi cela a-t-il fonctionné ? L’attaque golden ticket fonctionne, car le ticket généré était correctement signé avec la clé « KRBTGT » que nous avons récoltée précédemment. Ce ticket nous permet, en tant qu’attaquant, d’accéder à ContosoDC et de nous ajouter à n’importe quel groupe de sécurité que nous souhaitons utiliser.

#### <a name="golden-ticket--existing-user-attack-detection"></a>Golden ticket – détection d’une attaque utilisateur existante

Azure ATP utilise plusieurs méthodes pour détecter des attaques présumées de ce type. Dans ce scénario précis, Azure ATP a détecté le passage à une version antérieure du chiffrement du faux ticket.

![Détection du golden ticket](media/playbook-dominance-golden_detected.png)

> [!Important]
>Rappel. Tant que le KRBTGT récolté par un attaquant reste valide dans un environnement, les tickets générés avec lui le restent également. Dans ce cas, l’attaquant réussit à avoir le contrôle persistant du domaine jusqu’à ce que le [KRBTGT soit réinitialisé à deux reprises](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/ad-forest-recovery-resetting-the-krbtgt-password).

## <a name="next-steps"></a>Étapes suivantes

* [Guide des alertes de sécurité d’Azure ATP](suspicious-activity-guide.md)
* [Examiner les chemins de mouvement latéral avec Azure ATP](use-case-lateral-movement-path.md)
* [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) dès aujourd’hui !