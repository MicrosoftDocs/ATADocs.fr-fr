---
title: 'Démarrage rapide : Configurer les paramètres du capteur Azure ATP | Microsoft Docs'
description: L’étape 5 de la procédure d’installation d’Azure ATP permet de configurer les paramètres du capteur autonome Azure ATP.
author: mlottner
ms.author: mlottner
ms.date: 02/06/2018
ms.topic: quickstart
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 661e9ec9a40f45c0dc323b5a9d612b03a3128cb7
ms.sourcegitcommit: 96752da28f43896e7b8e5945947b32c4810bdff6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/07/2019
ms.locfileid: "55831444"
---
# <a name="quickstart-configure-azure-atp-sensor-settings"></a>Démarrage rapide : Configurer les paramètres du capteur Azure ATP

Dans ce guide de démarrage rapide, vous allez configurer les paramètres du capteur Azure ATP pour commencer à voir des données. Vous devez effectuer une configuration et une intégration supplémentaires pour tirer parti des fonctionnalités Azure ATP.  

## <a name="prerequisites"></a>Prérequis

- Une [instance Azure ATP](install-atp-step1.md) qui est [connectée à Active Directory](install-atp-step2.md).
- Une copie téléchargée de votre [package d’installation du capteur ATP](install-atp-step3.md) et la clé d’accès.

## <a name="configure-sensor-settings"></a>Configurer les paramètres du capteur

Une fois le capteur Azure ATP installé, effectuez les étapes suivantes pour configurer ses paramètres.

1.  Dans le portail Azure ATP, accédez à **Configuration** et, sous la section **Système**, sélectionnez **Capteurs**.
   
    ![Image de la configuration des paramètres du capteur](media/atp-sensor-config.png)


2. Cliquez sur le capteur que vous voulez configurer et entrez les informations suivantes :

   ![Image de la configuration des paramètres du capteur](media/atp-sensor-config-2.png)

   - **Description** : entrez une description du capteur Azure ATP (facultatif).
   - **Contrôleurs de domaine (FQDN)** (nécessaire pour le capteur autonome Azure ATP, non modifiable pour le capteur Azure ATP) : Entrez le nom de domaine complet de votre contrôleur de domaine et cliquez sur le signe plus (+) pour l’ajouter à la liste. Par exemple, **dc01.contoso.com**.

     Les informations suivantes s’appliquent aux serveurs que vous entrez dans la liste **Contrôleurs de domaine** :
     - Tous les contrôleurs de domaine dont le trafic est surveillé par l’intermédiaire de la mise en miroir des ports par le capteur autonome Azure ATP doivent figurer dans la liste **Contrôleurs de domaine**. Si un contrôleur de domaine ne figure pas dans la liste **Contrôleurs de domaine**, il est possible que la détection des activités suspectes ne fonctionne pas comme prévu.
     - Au moins un contrôleur de domaine figurant dans la liste doit être un catalogue général. Azure ATP peut ainsi résoudre les objets d’ordinateur et d’utilisateur dans d’autres domaines de la forêt.

   - **Adaptateurs de réseau de capture** (obligatoire) :
   
    - Dans le cas des capteurs Azure ATP, il s’agit de toutes les cartes réseau utilisées pour la communication avec les autres ordinateurs de votre organisation.
    - Dans le cas d’un capteur autonome Azure ATP sur un serveur dédié, sélectionnez les cartes réseau qui sont configurées en tant que port miroir de destination. Ces cartes réseau reçoivent le trafic du contrôleur de domaine mis en miroir.

  - **Candidat synchronisateur de domaine** : 
    
    - Le candidat synchronisateur de domaine est responsable de la synchronisation entre Azure ATP et votre domaine Active Directory. Selon la taille du domaine, la synchronisation initiale peut prendre du temps et consommer beaucoup de ressources. Azure ATP vous recommande de désigner au moins un contrôleur de domaine comme candidat synchronisateur de domaine dans chaque domaine. Si vous ne le faites pas, Azure ATP effectuera seulement une analyse passive de votre réseau et ne collectera donc peut-être pas toutes les informations sur les valeurs des entités et les changements détectés dans Active Directory. Le fait de désigner au moins un **candidat synchronisateur de domaine** par domaine garantit qu’Azure ATP pourra analyser activement votre réseau en permanence et collecter l’ensemble de ces informations.
  
    - Par défaut, les capteurs Azure ATP ne sont pas des candidats synchronisateurs de domaine, contrairement aux capteurs autonomes Azure ATP. Pour désigner manuellement un capteur Azure ATP comme candidat synchronisateur de domaine, définissez l’option **Candidat synchronisateur de domaine** sur **Activé** dans l’écran de configuration.
        
    - Il est recommandé de désactiver les capteurs Azure ATP de site distant comme candidats synchronisateurs de domaine.
   
    - Ne désignez pas des contrôleurs de domaine en lecture seule comme candidats synchronisateurs de domaine. Pour plus d’informations sur la synchronisation de domaine Azure ATP, consultez [Architecture Azure ATP](atp-architecture.md#azure-atp-sensor-features).
  
3. Cliquez sur **Save**.


## <a name="validate-installations"></a>Valider les installations
Pour vous assurer que le capteur Azure ATP a été déployé avec succès, effectuez les étapes suivantes :

1. Vérifiez que le service nommé **Capteur Azure Advanced Threat Protection** est en cours d’exécution. Après avoir enregistré les paramètres du capteur Azure ATP, vous devrez peut-être patienter quelques secondes avant le démarrage du service.

2. Si le service ne démarre pas, examinez le fichier « Microsoft.Tri.sensor-Errors.log » qui se trouve dans le dossier par défaut suivant : « %programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs ».
 
   >[!NOTE]
   > La version d’Azure ATP est fréquemment mise à jour. Pour vérifier la version, dans le portail Azure ATP, accédez à **Configuration**, puis à **À propos**. 

3. Accédez à l’URL de votre instance Azure ATP. Dans le portail Azure ATP, recherchez un élément dans la barre de recherche, comme un utilisateur ou un groupe de votre domaine.

## <a name="next-steps"></a>Étapes suivantes

- [Configuration du proxy](configure-proxy.md)
- [Stratégie d’audit avancée](atp-advanced-audit-policy.md)
- [Configurer Azure ATP pour effectuer des appels distants vers SAM](install-atp-step8-samr.md)


## <a name="join-the-community"></a>Rejoindre la communauté

Vous avez d’autres questions ou vous voulez discuter d’Azure ATP et de la sécurité associée avec d’autres utilisateurs ? Rejoignez la [Communauté Azure ATP](https://aka.ms/azureatpcommunity) dès aujourd’hui !
