---
title: Tutoriel de playbook Azure ATP Reconnaissance | Microsoft Docs
description: Le tutoriel de playbook Azure ATP Reconnaissance décrit comment simuler des menaces de reconnaissance pour la détection par Azure ATP.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: mlottner
ms.author: mlottner
ms.date: 03/03/2019
ms.reviewer: itargoet
ms.openlocfilehash: 20e91bc710dc184fa710cf7fd59cb9bd9d625d20
ms.sourcegitcommit: 929f28783110c7e114ab36d4cccd50563f4030df
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2019
ms.locfileid: "57253961"
---
# <a name="tutorial-reconnaissance-playbook"></a>Didacticiel : Playbook de reconnaissance

Le deuxième tutoriel de cette série en quatre parties sur les alertes de sécurité Azure ATP est un playbook de reconnaissance. L’objectif du labo d’alerte de sécurité Azure ATP est d’illustrer les capacités d’**Azure ATP** à identifier et à détecter des activités suspectes et des attaques potentielles contre votre réseau. Le playbook explique comment tester certaines détections *discrètes* d’Azure ATP et se concentre sur les fonctionnalités d’Azure ATP *basées sur la signature*. Ce playbook n’inclut pas les alertes ou les détections basées sur le Machine Learning avancé, ni les détections de comportements basées utilisateur/entité, car celles-ci nécessitent une période d’apprentissage avec un trafic réseau réel pouvant aller jusqu’à 30 jours. Pour plus d’informations sur chaque tutoriel de cette série, consultez la [vue d’ensemble du labo d’alerte de sécurité ATP](atp-playbook-lab-overview.md).

Ce playbook illustre la détection des menaces et les services d’alertes de sécurité d’Azure ATP pour des attaques simulées à partir d’outils de piratage et d’attaque courants, réels et disponibles publiquement.

Dans ce tutoriel vous allez :
> [!div class="checklist"]
> * simuler la reconnaissance de mappage de réseau ;
> * simuler la reconnaissance de service d'annuaire ;
> * simuler la reconnaissance des utilisateurs et des adresses IP (SMB) ;
> * passer en revue les alertes de sécurité à partir de la reconnaissance simulée dans Azure ATP.

## <a name="prerequisites"></a>Prérequis

[Un labo d’alerte de sécurité ATP terminé](atp-playbook-setup-lab.md)
  - Nous vous recommandons de suivre d’aussi près que possible les instructions de configuration du labo. Plus votre labo sera proche de la configuration suggérée, plus les procédures de test Azure ATP seront faciles à suivre.

## <a name="simulate-a-reconnaissance-attack"></a>Simuler une attaque de reconnaissance

Une fois qu’une personne malveillante se trouve dans votre environnement, sa campagne de reconnaissance commence. À ce stade, l’attaquant passe généralement du temps à rechercher. Il tente de détecter les ordinateurs intéressants, d’énumérer des utilisateurs et des groupes, de collecter des adresses IP importantes et de mapper les ressources et les faiblesses de votre organisation. Les activités de reconnaissance permettent aux attaquants d’acquérir une compréhension approfondie et d’effectuer le mappage complet de votre environnement pour une utilisation ultérieure.

Méthodes de test d’attaque de reconnaissance :

* Reconnaissance de mappage de réseau
* Reconnaissance de service d'annuaire
* Reconnaissance des utilisateurs et des adresses IP (SMB)

## <a name="network-mapping-reconnaissance-dns"></a>Reconnaissance de mappage de réseau (DNS)

Une des premières choses que fait un attaquant est d’essayer d’obtenir une copie de toutes les informations DNS. En cas de succès, l’attaquant obtient des informations détaillées sur votre environnement, qui peuvent éventuellement inclure des informations similaires sur vos autres environnements ou réseaux.

### <a name="run-nslookup-from-victimpc"></a>Exécuter nslookup à partir de VictimPC

Pour tester la reconnaissance DNS, nous utilisons l’outil de ligne de commande natif, *nslookup*, pour lancer un transfert de zone DNS. Les serveurs DNS avec une configuration correcte refusent les requêtes de ce type et n’autorisent pas la tentative de transfert de zone.  

Connectez-vous à **VictimPC** avec les informations d’identification JeffL compromises. Exécutez la commande suivante :

``` cmd
nslookup
```

Tapez **serveur**, puis le nom de domaine complet ou l’adresse IP du contrôleur de domaine où le capteur ATP est installé.

```nslookup
server contosodc.contoso.azure
```

Essayons de transférer le domaine.

```nslookup
ls -d contoso.azure
```

- Remplacez contosodc.contoso.azure et contoso.azure par le nom de domaine complet de votre capteur Azure ATP et le nom de domaine respectivement.

 ![tentative de commande nslookup pour copier le serveur DNS -échec](media/playbook-recon-nslookup.png)

Si **ContsoDC** est votre premier capteur déployé, attendez 15 minutes pour permettre à la base de données principale de terminer le déploiement des microservices nécessaires.

### <a name="network-mapping-reconnaissance-dns-detected-in-azure-atp"></a>Reconnaissance de mappage de réseau (DNS) détectée dans Azure ATP

La visibilité de ce type de tentative (réussie ou non) est essentielle pour la protection contre les menaces de domaine. Étant donné que nous venons d’installer l’environnement, nous devons accéder à la chronologie des activités logiques pour voir l’activité. 

Dans la recherche Azure ATP, tapez **VictimPC**, puis cliquez dessus pour afficher la chronologie.

![Reconnaissance DNS détectée par Azure ATP, vue de haut niveau](media/playbook-recon-nslookupdetection1.png)

Recherchez l’activité « Requête AXFR ». Azure ATP détecte ce type de reconnaissance sur votre serveur DNS. 
  - Si vous avez un grand nombre d’activités, cliquez sur **Filtrer par** et décochez tous les types à l’exception de « Requête DNS ».

![Vue détaillée de la détection de reconnaissance DNS dans Azure ATP](media/playbook-recon-nslookupdetection2.png)

Si votre analyste de sécurité a déterminé cette activité provenant d’un scanner de sécurité, le périphérique spécifique peut être exclu d’autres alertes de détection. Dans la zone supérieure droite de l’alerte, cliquez sur les trois points. Ensuite, sélectionnez **Fermer et exclure MySecurityScanner**. Ceci garantit que cette alerte ne s’affiche pas à nouveau en cas de détection par « MySecurityScanner ».

La détection d’erreurs peut s’avérer aussi instructive que la détection d’attaques réussies contre un environnement. Le portail Azure ATP nous permet de voir le résultat exact des actions effectuées par un attaquant possible. Dans notre histoire d’attaque de reconnaissance DNS simulée, nous avons, en tant qu’attaquants, été empêchés de vider les enregistrements DNS du domaine. Votre équipe SecOps s’est rendu compte de notre tentative d’attaque et de la machine que nous avons utilisée lors de notre tentative grâce à l’alerte de sécurité Azure ATP.

## <a name="directory-service-reconnaissance"></a>Reconnaissance de service d'annuaire

L’objectif de reconnaissance suivant d’un attaquant est de tenter d’énumérer tous les utilisateurs et groupes de la forêt. Azure ATP supprime l’activité d’énumération de services d’annuaire de votre chronologie d’activités suspectes jusqu'à ce qu'une période d'apprentissage de 30 jours soit terminée. Pendant la période d’apprentissage, Azure ATP apprend ce qui est normal et anormal pour votre réseau. Après la période d’apprentissage de 30 jours, des événements anormaux d’énumération de services d’annuaire appellent une alerte de sécurité. Pendant la période d’apprentissage de 30 jours, vous pouvez voir les détections Azure ATP de ces activités à l’aide de la chronologie des activités d’une entité dans votre réseau. Les détections Azure ATP de ces activités sont présentées dans ce labo.

Pour illustrer une méthode de reconnaissance de service d’annuaire commune, nous utilisons le fichier binaire Microsoft natif, *réseau*. Après notre tentative, l’examen de la chronologie des activités de JeffL, notre utilisateur compromis, indique la détection de cette activité sur Azure ATP.

### <a name="directory-service-enumeration-via-net-from-victimpc"></a>Énumération de services d’annuaire par le biais du *réseau* de VictimPC

N’importe quel ordinateur ou utilisateur authentifié peut potentiellement énumérer d’autres utilisateurs et groupes dans un domaine. Cette capacité d’énumération est requise pour le bon fonctionnement de la plupart des applications. Notre utilisateur compromis, JeffL, est un compte de domaine non privilégié. Lors de cette attaque simulée, nous verrons exactement comment même un compte de domaine non privilégié peut toujours fournir des points de données à un attaquant.

1. À partir de **VictimPC**, exécutez la commande suivante :

    ``` cmd
    net user /domain
    ```

   La sortie affiche tous les utilisateurs dans le domaine Contoso.Azure.

   ![Énumérer tous les utilisateurs dans le domaine](media/playbook-recon-dsenumeration-netusers.png)

2. Essayons d’énumérer tous les groupes dans le domaine. Exécutez la commande suivante :

    ``` cmd
    net group /domain
    ```

   La sortie affiche tous les groupes dans le domaine Contoso.Azure. Notez le groupe de sécurité qui n’est pas un groupe par défaut : **Support technique**.

   ![Énumérer tous les groupes dans le domaine](media/playbook-recon-dsenumeration-netgroups.png)

3. À présent, essayons d’énumérer uniquement le groupe d’administrateurs du domaine. Exécutez la commande suivante :

    ``` cmd
    net group "Domain Admins" /domain
    ```

   ![Énumérer tous les membres du groupe d’administrateurs du domaine](media/playbook-recon-dsenumeration-netdomainadmins.png)

    En agissant comme un attaquant, nous avons appris qu’il y a deux membres du groupe d’administrateurs du domaine : **SamiraA** et **ContosoAdmin** (administrateur intégré pour le contrôleur de domaine). Sachant qu’il n’y a pas de limite de sécurité entre notre domaine et la forêt, l’étape suivante consiste à essayer d’énumérer les administrateurs de l’entreprise.

4. Pour tenter d’énumérer les administrateurs de l’entreprise, exécutez la commande suivante :

    ``` cmd
   net group "Enterprise Admins" /domain
   ```

   Nous avons appris qu’il n'y a qu’un seul administrateur d’entreprise, ContosoAdmin. Ces informations n’étaient pas importantes dans la mesure où nous savions déjà qu'il n’y a pas de limite de sécurité entre notre domaine et la forêt.

   ![Administrateurs de l’entreprise énumérés dans le domaine](media/playbook-recon-dsenumeration-netenterpriseadmins.png)

Avec les informations collectées lors de notre reconnaissance, nous connaissons maintenant le groupe de sécurité du support technique. Ces informations ne sont cependant pas *encore* intéressantes. Nous savons également que **SamiraA** est un membre du groupe d’administrateurs du domaine. Si nous pouvons collecter les informations d’identification de SamiraA, nous pouvons accéder au contrôleur de domaine proprement dit.

### <a name="directory-service-enumeration-detected-in-azure-atp"></a>Énumération des services d’annuaire détectée dans Azure ATP

Si notre labo avait une *activité réelle en direct pendant 30 jours une fois Azure ATP installé*, l’activité que nous venons d’avoir en tant que JeffL serait potentiellement considérée comme anormale. Une activité anormale s’afficherait dans la chronologie des activités suspectes. Cependant, étant donné que nous venons d’installer l’environnement, nous devons accéder à la chronologie des activités logiques.

Dans la recherche Azure ATP, voyons à quoi ressemble la chronologie d’activité logique de JeffL :

![Rechercher une entité spécifique dans la chronologie des activités logiques](media/playbook-recon-dsenumeration-searchlogicalactivity.png)

Nous pouvons voir lorsque JeffL est connecté à VictimPC à l’aide du protocole Kerberos. En outre, nous voyons que JeffL a énuméré tous les utilisateurs du domaine à partir de VictimPC.

![Chronologie de l’activité logique de JeffL](media/playbook-recon-dsenumeration-jeffvlogicalactivity.png)

De nombreuses activités sont consignées dans la chronologie des activités logiques, qui est une fonctionnalité majeure pour la forensique numérique et la réponse aux incidents (DFIR). Vous pouvez même voir des activités lorsque la détection initiale n’est pas venue d’Azure ATP, mais de Windows Defender ATP, d’Office 365 et autres.

En jetant un coup d’œil à la **page de ContosoDC**, nous pouvons également voir les ordinateurs auxquels JeffL s’est connecté.

![JeffL connecté aux ordinateurs](media/playbook-recon-dsenumeration-jeffvloggedin.png)

Nous pouvons également obtenir des données de répertoire, notamment les appartenances et les contrôles d’accès de JeffL, le tout à partir d’Azure ATP.

![Données de répertoire de JeffL dans Azure ATP](media/playbook-recon-dsenumeration-jeffvdirectorydata.png)

Notre attention se tourne maintenant vers l’énumération de sessions SMB.

## <a name="user-and-ip-address-reconnaissance-smb"></a>Reconnaissance des utilisateurs et des adresses IP (SMB)

Le dossier sysvol d’Active Directory est l’un des partages réseau dans l’environnement, même si ce n’est pas *le* plus important. Chaque ordinateur et utilisateur doit pouvoir accéder à ce partage réseau en particulier pour extraire des stratégies de groupe. Une énumération de sessions actives avec le dossier sysvol peut fournir peut obtenir une mine d’informations à un attaquant.

Notre prochaine étape est une énumération de sessions SMB sur la ressource ContosoDC. Nous souhaitons savoir qui d’autre a des sessions avec le partage SMB et *à partir de quelle adresse IP*.

### <a name="use-joewares-netsessexe-from-victimpc"></a>Utiliser NetSess.exe de JoeWare à partir de VictimPC

Exécution de l’outil **NetSess** de JoeWare sur ContosoDC dans le contexte d’un utilisateur authentifié, dans notre cas ContosoDC :

``` cmd
NetSess.exe ContosoDC
```

![Les attaquants utilisent la reconnaissance SMB pour identifier les utilisateurs et leurs adresses IP.](media/playbook-recon-smbrecon.png)

Nous savons déjà que SamiraA est un administrateur de domaine. Cette attaque nous a permis d’obtenir l’adresse IP de SamiraA, à savoir 10.0.24.6. En tant qu’attaquant, nous avons appris qui nous devons exactement compromettre. Nous avons également l’emplacement réseau où ces informations d’identification sont enregistrées.

### <a name="user-and-ip-address-reconnaissance-smb-detected-in-azure-atp"></a>Reconnaissance des utilisateurs et des adresses IP (SMB) détectée dans Azure ATP

Maintenant, nous pouvons voir ce qu’Azure ATP a détecté pour nous :

![Détection de reconnaissance de SMB d’Azure ATP](media/playbook-recon-smbrecon-detection1.png)

Non seulement nous sommes alertés de cette activité, mais encore nous sommes informés des comptes exposés et de leurs adresses IP respectives *à ce moment précis*. En tant que centre des opérations de sécurité (SOC), nous n’avons pas seulement la tentative et son état, mais également ce qui a été renvoyé à l’attaquant. Ces informations facilitent notre enquête.


## <a name="next-steps"></a>Étapes suivantes

La phase suivante dans la chaîne de destruction d’attaque est généralement une tentative de mouvement latéral.

> [!div class="nextstepaction"]
> [Playbook des mouvements latéraux d’Azure ATP](atp-playbook-lateral-movement.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) dès aujourd’hui !

