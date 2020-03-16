---
title: Nouveautés d’Advanced Threat Analytics version 1,6
description: Répertorie les nouveautés d’ATA version 1.6, ainsi que les problèmes connus
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 27b139e5-12b9-4953-8f53-eb58e8ce0038
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c87966ee2d8f53187bcc412cb027b19c4ddcf891
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79412548"
---
# <a name="whats-new-in-ata-version-16"></a>Nouveautés d’ATA version 1.6
Ces notes de publication fournissent des informations sur les problèmes connus de cette version d’Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-16-update"></a>Quelles sont les nouveautés d’ATA 1.6 ?
La mise à jour vers ATA 1.6 comprend des améliorations dans les domaines suivants :

-   Nouvelles détections

-   Détections existantes plus efficaces

-   Passerelle légère ATA

-   Mises à jour automatiques

-   Performances accrues du centre ATA

-   Réduction des besoins de stockage

-   Prise en charge d’IBM QRadar

### <a name="new-detections"></a>Nouvelles détections


- **Demande d’information privée de protection contre les données malveillantes** L’API de protection des données (DPAPI) est un service de protection des données avec mot de passe. De nombreuses applications qui stockent les secrets des utilisateurs, comme les mots de passe de sites web et les informations d’identification de partage de fichiers, utilisent ce service de protection. Pour prendre en charge les scénarios de perte du mot de passe, les utilisateurs peuvent déchiffrer des données protégées à l’aide d’une clé de récupération qui ne fait pas appel à leur mot de passe. Dans un environnement de domaine, des attaquants peuvent dérober à distance la clé de récupération et s’en servir pour déchiffrer des données protégées sur tous les ordinateurs joints au domaine.


- **Énumération de sessions Net** La reconnaissance est une étape clé de la chaîne de destruction d’une attaque avancée. Les contrôleurs de domaine fonctionnent comme des serveurs de fichiers pour les besoins de la distribution de l’objet de stratégie de groupe. Pour cela, ils utilisent le protocole SMB (Server Message Block). Dans le cadre de la phase de reconnaissance, des attaquants peuvent interroger le contrôleur de domaine pour toutes les sessions SMB actives sur le serveur. Ils ont ainsi la possibilité d’accéder à tous les utilisateurs et à toutes les adresses IP associés à ces sessions SMB. L’énumération de sessions SMB peut être mise à profit par des attaquants pour cibler des comptes sensibles et faciliter les mouvements latéraux sur le réseau.


- **Demandes de réplication malveillantes** Dans les environnements Active Directory, la réplication se produit régulièrement entre contrôleurs de domaine. Un attaquant peut usurper une requête de réplication Active Directory (parfois en empruntant l’identité d’un contrôleur de domaine). Cette usurpation d’identité permet à un attaquant de récupérer les données stockées dans Active Directory, y compris les hachages de mot de passe, sans utiliser de techniques plus envahissantes, comme le cliché instantané de volume.


- **Détection de la vulnérabilité MS11-013**  
Dans Kerberos, une vulnérabilité menant à l’élévation de privilèges peut entraîner la falsification de certains aspects d’un ticket de service Kerberos. Si un utilisateur malveillant ou un attaquant parvient à exploiter cette vulnérabilité, il peut obtenir un jeton avec des privilèges élevés sur le contrôleur de domaine.


- **Implémentation de protocole inhabituelle** Les demandes d’authentification (Kerberos ou NTLM) sont généralement effectuées à l’aide d’un ensemble standard de méthodes et de protocoles. Toutefois, pour s’authentifier, la demande doit simplement respecter un ensemble spécifique d’exigences. Des attaquants peuvent implémenter ces protocoles avec des écarts mineurs par rapport à l’implémentation standard dans l’environnement. Ces écarts peuvent indiquer une tentative d’attaque de type Pass-The-Hash, force brute, etc.


### <a name="improvements-to-existing-detections"></a>Détections existantes plus efficaces
ATA 1.6 comporte une logique de détection améliorée qui réduit le nombre de faux positifs et de faux négatifs lors des détections d’attaques existantes (telles que Golden Ticket, honeytoken, la force brute et l’exécution à distance).

### <a name="the-ata-lightweight-gateway"></a>Passerelle légère ATA
Cette version d’ATA introduit une nouvelle option de déploiement pour la passerelle ATA : vous pouvez désormais installer une passerelle ATA directement sur le contrôleur de domaine. Cette option de déploiement supprime les fonctionnalités non critiques de la passerelle ATA et offre une gestion dynamique des ressources en fonction des ressources disponibles sur le contrôleur de domaine. Vous pouvez donc vérifier que les opérations existantes du contrôleur de domaine ne sont pas affectées. La passerelle légère ATA réduit le coût du déploiement d’ATA. En même temps, elle facilite le déploiement dans les succursales, ces dernières se caractérisant par des ressources matérielles avec des capacités limitées ou l’impossibilité de configurer la prise en charge de la mise en miroir des ports.
Pour plus d’informations sur la passerelle légère ATA, consultez [Architecture d’ATA](ata-architecture.md#ata-gateway-and-ata-lightweight-gateway).

Pour plus d’informations sur les considérations relatives au déploiement et le choix du type de passerelle adapté à vos besoins, consultez [Planification de la capacité ATA](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment).


### <a name="automatic-updates"></a>Mises à jour automatiques
À compter de la version 1.6, il est possible de mettre à jour le centre ATA à l’aide de Microsoft Update. Par ailleurs, les passerelles ATA peuvent être automatiquement mises à jour par le biais de leur canal de communication standard au centre ATA.
### <a name="improved-ata-center-performance"></a>Performances accrues du centre ATA
Dans cette version, grâce à la réduction de la charge de la base de données et à l’exécution plus efficace de toutes les détections, un même centre ATA peut surveiller davantage de contrôleurs de domaine.

### <a name="lower-storage-requirements"></a>Réduction des besoins de stockage
ATA 1.6 nécessite désormais beaucoup moins d’espace pour exécuter la base de données ATA : seulement 20 % de l’espace de stockage utilisé dans les versions précédentes.

### <a name="support-for-ibm-qradar"></a>Prise en charge d’IBM QRadar
Outre les solutions SIEM déjà prises en charge, ATA peut à présent recevoir des événements de la solution SIEM QRadar d’IBM.

## <a name="known-issues"></a>Problèmes connus
Les problèmes connus de cette version sont les suivants :

### <a name="failure-to-recognize-new-path-in-manually-moved-databases"></a>Échec de la reconnaissance d’un nouveau chemin dans les bases de données déplacées manuellement

Dans les déploiements dans lesquels la base de données fait l’objet d’un déplacement manuel, le déploiement d’ATA n’utilise pas le nouveau chemin de la base de données pour la mise à jour. Ce chemin de base de données déplacé manuellement peut entraîner les problèmes suivants :


- ATA peut utiliser tout l’espace libre sur le lecteur système du centre ATA, sans supprimer de façon circulaire les anciennes activités réseau.


- La mise à jour vers ATA 1.6 peut échouer au niveau des vérifications de la disponibilité antérieures à la mise à jour, comme le montre l’image ci-dessous.
    ![Échec de la vérification de la disponibilité](media/ata_failed_readinesschecks.png)
    
    > [!IMPORTANT]
    > Avant de mettre à jour ATA vers la version 1.6, mettez à jour le chemin correct de la base de données dans la clé de Registre suivante : `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath`
    
### <a name="migration-failure-when-updating-from-ata-15"></a>Échec de la migration en cas de mise à jour à partir d’ATA 1.5
Quand vous effectuez la mise à jour vers ATA 1.6, le processus peut échouer avec le code d’erreur suivant :

![Erreur de mise à jour d’ATA vers la version 1.6](http://i.imgur.com/QrLSApr.png) Si vous recevez cette erreur, examinez le journal de déploiement qui se trouve dans **C:\Users\<utilisateur>\AppData\Local\Temp**, puis recherchez l’exception suivante :

    System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> MongoDB.Driver.MongoWriteException: A write operation resulted in an error. E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : "<guid>" } ---> MongoDB.Driver.MongoBulkWriteException`1: A bulk write operation resulted in one or more errors.  E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : " <guid> " }

Vous pouvez également voir cette erreur : System.ArgumentNullException : La valeur ne peut pas être Null.
    
Si vous voyez l’une de ces erreurs, effectuez la solution de contournement suivante :

**Solution de contournement** : 

1.  Déplacez dans un dossier temporaire le dossier « data_old » (qui se trouve généralement dans %ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin).
2.  Désinstallez le centre ATA v1.5 et supprimez toutes les données de la base de données.
![Désinstaller ATA 1.5](http://i.imgur.com/x4nJycx.png)
3.  Réinstallez le centre ATA v1.5. Veillez à utiliser la même configuration que l’installation précédente d’ATA 1.5 (certificats, adresses IP, chemin de la base de données, etc.).
4.  Arrêtez ces services dans l’ordre suivant :
    1.  Microsoft Advanced Threat Analytics Center
    2.  MongoDB
5.  Remplacez les fichiers de la base de données MongoDB par les fichiers contenus dans le dossier « data_old ».
6.  Démarrez ces services dans l’ordre suivant :
    1.  MongoDB
    2.  Microsoft Advanced Threat Analytics Center
7.  Passez en revue les journaux pour vérifier que le produit s’exécute sans erreur.
8.  [Téléchargez](https://aka.ms/ataremoveduplicateprofiles "Télécharger") l’outil « RemoveDuplicateProfiles. exe » et copiez-le dans le chemin d’installation principal (%ProgramFiles%\Microsoft Advanced Threat Analytics\Center)
9.  À partir d’une invite de commandes avec élévation de privilèges, exécutez `RemoveDuplicateProfiles.exe` et attendez la fin de l’opération.
10. À partir du répertoire …\Microsoft Advanced Threat Analytics\Center\MongoDB\bin **Mongo ATA**, tapez la commande suivante :

          db.SuspiciousActivities.remove({ "_t" : "RemoteExecutionSuspiciousActivity", "DetailsRecords" : { "$elemMatch" : { "ReturnCode" : null } } }, { "_id" : 1 });

![Solution de contournement de la mise à jour](http://i.imgur.com/Nj99X2f.png)

Cette commande doit retourner `WriteResult({ "nRemoved" : XX })` où « XX » est le nombre d’activités suspectes qui ont été supprimées. Si le nombre est supérieur à 0, quittez l’invite de commandes et continuez le processus de mise à jour.


### <a name="net-framework-461-requires-restarting-the-server"></a>Le .NET Framework 4.6.1 nécessite le redémarrage du serveur

![Redémarrage du .NET Framework](media/ata-net-framework-restart.png)

### <a name="historical-network-activities-no-longer-migrated"></a>L’historique des activités réseau n’est plus migré
Cette version d’ATA offre un moteur de détection amélioré qui accroît la précision des détections et qui réduit considérablement le nombre de faux positifs, en particulier ceux associés aux attaques de type Pass-the-Hash.
Le nouveau moteur de détection amélioré repose sur la technologie de détection inline. Celle-ci permet de détecter des attaques sans accéder à l’historique des activités réseau, d’où une augmentation significative des performances du centre ATA. Cela signifie également qu’il est inutile de migrer l’historique des activités réseau pendant la procédure de mise à jour.
Au cas où vous auriez besoin des données par la suite, la procédure de mise à jour d’ATA les exporte dans un fichier JSON à l’emplacement `<Center Installation Path>\Migration`.

## <a name="see-also"></a>Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Mise à jour d’ATA vers la version 1.6 : guide de migration](ata-update-1.6-migration-guide.md)
