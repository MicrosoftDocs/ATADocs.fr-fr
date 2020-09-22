---
title: 'Démarrage rapide : Planification de votre déploiement Azure Advanced Threat Protection'
description: Vous aide à planifier votre déploiement et à déterminer le nombre de serveurs Azure ATP nécessaires pour prendre en charge votre réseau
author: shsagir
ms.author: shsagir
ms.date: 05/20/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 6955ea798cc138142f0b3f4443df777ed2d07cac
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913252"
---
# <a name="quickstart-plan-capacity-for-azure-atp"></a>Démarrage rapide : Planifier la capacité pour Azure ATP

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Ce démarrage rapide vous aide à déterminer le nombre de capteurs Azure ATP dont vous avez besoin.

## <a name="prerequisites"></a>Prérequis

- Téléchargez [l’Outil de dimensionnement Azure ATP](https://aka.ms/aatpsizingtool).
- Examinez l’article [Architecture Azure ATP](architecture.md).
- Examinez l’article [Prérequis d’Azure ATP](prerequisites.md).

## <a name="use-the-sizing-tool"></a>Utiliser l’outil de dimensionnement

La manière recommandée la plus simple de déterminer la capacité pour votre déploiement Azure ATP est d’utiliser l’outil de dimensionnement Azure ATP. Si vous ne parvenez pas à utiliser l’outil, vous pouvez collecter manuellement les informations sur le trafic. Pour plus d’informations la méthode manuelle, consultez la section [Estimateur de trafic du contrôleur de domaine](#manual-sizing) au bas de cet article.

1. Exécutez l’outil de dimensionnement Azure ATP, **TriSizingTool.exe**, à partir du fichier zip que vous avez téléchargé.
1. Lorsque l’exécution de l’outil est terminée, ouvrez le fichier Excel des résultats.
1. Dans le fichier Excel, recherchez et cliquez sur la feuille **Résumé Azure ATP**. L’autre feuille n’est pas nécessaire, car elle concerne la planification d’ATA.
    ![Exemple d’outil de planification des capacités](media/capacity-tool.png)

1. Recherchez le champ **Paquets occupés/s** dans le tableau du capteur Azure ATP du fichier Excel des résultats et prenez note de celui-ci.
1. Faites correspondre votre champ **Paquets occupés/s** au champ **PAQUETS PAR SECONDE** dans la section [Tableau du capteur Azure ATP](#sizing) de cet article. Utilisez les champs pour déterminer la mémoire et le processeur qui seront utilisés par le capteur.

## <a name="azure-atp-sensor-sizing"></a><a name="sizing"></a> Dimensionnement du capteur Azure ATP

Un capteur Azure ATP peut prendre en charge la surveillance d’un contrôleur de domaine en fonction de la quantité de trafic réseau qu’il génère. Le tableau suivant est une estimation. La quantité finale analysée par le capteur étant dépendante du volume et de la distribution du trafic.

La capacité de processeur et de mémoire vive (RAM) suivante fait référence à la **consommation propre du capteur**, et pas à la capacité du contrôleur de domaine.

|Paquets par seconde|Processeur (cœurs)\*|Mémoire\*\* (Go)|
|----|----|-----|
|0 à 1 000|0,25|2,50|
|1 000 à 5 000|0,75|6,00|
|5 000 à 10 000|1,00|6,50|
|10 000 à 20 000|2,00|9,00|
|20 000 à 50 000|3,50|9,50|
|50 000 à 75 000 |3,50|9,50|
|75 000 à 100 000|3,50|9,50|

\* Cela comprend des cœurs physiques, et non des cœurs hyper-thread.  
\*\* Mémoire vive (RAM)

Lorsque vous déterminez le dimensionnement, notez les éléments suivants :

- Nombre total de cœurs que le service de capteur va utiliser.  
Nous vous recommandons de ne pas utiliser des cœurs hyper-thread. L’utilisation de cœurs hyper-thread peut entraîner des problèmes d’intégrité du capteur Azure ATP.
- Quantité totale de mémoire que le service de capteur va utiliser.
- Si le contrôleur de domaine n’a pas les ressources demandées par le capteur Azure ATP, ses performances ne sont pas affectées. Mais le capteur Azure ATP risque de ne pas fonctionner comme prévu.
- En cas d’exécution en tant que machine virtuelle, toute la mémoire doit être allouée à la machine virtuelle à tout moment.
- Pour bénéficier de performances optimales, choisissez **Hautes performances** comme **Option d’alimentation** pour le capteur Azure ATP.
- Au moins 2 cœurs sont nécessaires.
- Au moins 6 Go d’espace disque sont nécessaires, 10 Go sont recommandés, ce qui inclut l’espace nécessaire pour les fichiers binaires et les journaux Azure ATP.

### <a name="dynamic-memory"></a>Mémoire dynamique

> [!NOTE]
> En cas d’exécution en tant que machine virtuelle, toute la mémoire doit être allouée à la machine virtuelle à tout moment.

|Machine virtuelle en cours d’exécution sur|Description|
|------------|-------------|
|Hyper-V|Assurez-vous que l’option **Activer la mémoire dynamique** n’est pas activée pour la machine virtuelle.|
|VMWare|Assurez-vous que la quantité de mémoire configurée et la mémoire réservée sont identiques ou sélectionnez l’option suivante dans le paramètre de la machine virtuelle – **Réserver toute la mémoire invitée (tout verrouillé)** .|
|Autre hôte de virtualisation|Reportez-vous à la documentation donnée par le fournisseur pour savoir comment s’assurer que la mémoire est entièrement allouée à la machine virtuelle à tout moment. |

## <a name="domain-controller-traffic-estimation"></a><a name="manual-sizing"></a> Estimation du trafic des contrôleurs de domaine

Si, pour une raison quelconque, vous ne pouvez pas utiliser l’outil de dimensionnement Azure ATP, collectez manuellement les informations du compteur de paquets/s de tous vos contrôleurs de domaine. Collectez les informations pendant 24 heures avec un intervalle de collecte court, environ 5 secondes. Ensuite, pour chaque contrôleur de domaine, calculez la moyenne quotidienne et la moyenne des périodes les plus actives (15 minutes). Les sections suivantes expliquent comment collecter le compteur de paquets/s dans un contrôleur de domaine.

Il existe différents outils qui permettent de détecter le nombre moyen de paquets par seconde de vos contrôleurs de domaine. Si vous n’avez pas d’outil permettant d’effectuer le suivi de ce compteur, vous pouvez utiliser l’Analyseur de performances pour collecter les informations nécessaires.

Pour déterminer le nombre de paquets par seconde, effectuez les étapes suivantes pour chaque contrôleur de domaine :

1. Ouvrez l’Analyseur de performances.

    ![Image de l’Analyseur de performances](media/atp-traffic-estimation-1.png)

1. Développez **Ensembles de collecteurs de données**.

    ![Image d’Ensembles de collecteurs de données](media/atp-traffic-estimation-2.png)

1. Cliquez avec le bouton de droite sur **Défini par l’utilisateur**, puis sélectionnez **Nouveau** &gt; **Ensemble de collecteurs de données**.

    ![Image du nouvel ensemble de collecteurs de données](media/atp-traffic-estimation-3.png)

1. Entrez un nom pour l’ensemble de collecteurs, puis sélectionnez **Créer manuellement (avancé)** .

1. Sous **Quel type de données inclure ?** , sélectionnez **Créer des journaux de données et Compteur de performances**.

    ![Image du type de données pour le nouvel ensemble de collecteurs de données](media/atp-traffic-estimation-5.png)

1. Sous **Quels compteurs de performance enregistrer dans un journal ?** , cliquez sur **Ajouter**.

1. Développez **Carte réseau**. Sélectionnez **Paquets/s**, puis l’instance appropriée. Si vous n’êtes pas sûr, vous pouvez sélectionner **&lt;Toutes les instances&gt;** , puis cliquer sur **Ajouter** et **OK**.

    > [!NOTE]
    > Pour effectuer cette opération dans une ligne de commande, exécutez `ipconfig /all` pour afficher le nom de la carte réseau et sa configuration.

    ![Image de l’ajout du compteur de performances](media/atp-traffic-estimation-7.png)

1. Remplacez la valeur **Intervalle d’échantillonnage** par **cinq secondes**.

1. Définissez l’emplacement où vous voulez enregistrer les données.

1. Sous **Créer l’ensemble de collecteurs de données**, sélectionnez **Démarrer maintenant cet ensemble de collecteurs de données**, puis cliquez sur **Terminer**.

    Vous devez maintenant voir l’ensemble de collecteurs de données que vous venez de créer avec un triangle vert indiquant qu’il est activé.

1. Au bout de 24 heures, arrêtez l’ensemble de collecteurs de données en cliquant dessus avec le bouton droit et en sélectionnant **Arrêter**.

    ![Image de l’arrêt de l’ensemble de collecteurs de données](media/atp-traffic-estimation-12.png)

1. Dans l’Explorateur de fichiers, accédez au dossier où le fichier .blg a été enregistré, puis double-cliquez dessus pour l’ouvrir dans l’Analyseur de performances.

1. Sélectionnez le compteur Paquets par seconde, puis enregistrez les valeurs moyenne et maximale.

    ![Image du compteur Paquets par seconde](media/atp-traffic-estimation-14.png)

## <a name="next-steps"></a>Étapes suivantes

Ce démarrage rapide vous a aidé à déterminer le nombre de capteurs Azure ATP dont vous avez besoin. Vous avez également déterminé de dimensionnement des capteurs. Pour créer une instance Azure ATP, passez au démarrage rapide suivant.

> [!div class="nextstepaction"]
> [Créer votre instance Azure ATP](install-step1.md)

## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://aka.ms/azureatpcommunity) dès aujourd’hui !
