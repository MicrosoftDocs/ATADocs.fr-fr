---
title: Installer Azure Advanced Threat Protection | Microsoft Docs
description: L’étape 5 de la procédure d’installation d’Azure ATP permet de configurer les paramètres du capteur autonome Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cb9987645ffd1546b50117c984a138e8d3169657
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085263"
---
# <a name="install-azure-atp---step-5"></a>Installer Azure ATP – Étape 5

> [!div class="step-by-step"]
> [« Étape 4](install-atp-step4.md)
> [Étape 6 »](install-atp-step6-vpn.md)



## <a name="configure-azure-atp-sensor-settings"></a>Configurer les paramètres du capteur Azure ATP
Une fois le capteur Azure ATP installé, effectuez les étapes suivantes pour configurer ses paramètres.

1.  Dans le portail Azure ATP, accédez à **Configuration** et, sous la section **Système**, sélectionnez **Capteurs**.
   
    ![Image de la configuration des paramètres du capteur](media/atp-sensor-config.png)


2. Cliquez sur le capteur que vous voulez configurer et entrez les informations suivantes :

   ![Image de la configuration des paramètres du capteur](media/atp-sensor-config-2.png)

   - **Description** : entrez une description du capteur Azure ATP (facultatif).
   - **Contrôleurs de domaine (FQDN)** (requis pour le capteur autonome Azure ATP, non modifiable pour le capteur Azure ATP) : Entrez le nom de domaine complet de votre contrôleur de domaine et cliquez sur le signe plus (+) pour l’ajouter à la liste. Par exemple, **dc01.contoso.com**.

     Les informations suivantes s’appliquent aux serveurs que vous entrez dans la liste **Contrôleurs de domaine** :
     - Tous les contrôleurs de domaine dont le trafic est surveillé par l’intermédiaire de la mise en miroir des ports par le capteur autonome Azure ATP doivent figurer dans la liste **Contrôleurs de domaine**. Si un contrôleur de domaine n’est pas répertorié dans la liste **Contrôleurs de domaine**, il est possible que la détection des activités suspectes ne fonctionne pas comme prévu.
     - Au moins un contrôleur de domaine figurant dans la liste doit être un catalogue général. Azure ATP peut ainsi résoudre les objets d’ordinateur et d’utilisateur dans d’autres domaines de la forêt.

   - **Adaptateurs de réseau de capture** (obligatoire) :
   
    - Dans le cas des capteurs Azure ATP, il s’agit de toutes les cartes réseau utilisées pour la communication avec les autres ordinateurs de votre organisation.
    - Dans le cas d’un capteur autonome Azure ATP sur un serveur dédié, sélectionnez les cartes réseau qui sont configurées en tant que port miroir de destination. Elles reçoivent le trafic du contrôleur de domaine mis en miroir.

  - **Candidat synchronisateur de domaine** : 
    
    - Le candidat synchronisateur de domaine est responsable de la synchronisation entre Azure ATP et votre domaine Active Directory. Selon la taille du domaine, la synchronisation initiale peut prendre du temps et consommer beaucoup de ressources. Azure ATP vous recommande de désigner au moins un contrôleur de domaine comme candidat synchronisateur de domaine dans chaque domaine. Si vous ne le faites pas, Azure ATP effectuera seulement une analyse passive de votre réseau et ne collectera donc peut-être pas toutes les informations sur les valeurs des entités et les changements détectés dans Active Directory. Le fait de désigner au moins un **candidat synchronisateur de domaine** par domaine garantit qu’Azure ATP pourra analyser activement votre réseau en permanence et collecter l’ensemble de ces informations.
  
    - par défaut, les capteurs Azure ATP ne sont pas des candidats synchronisateurs de domaine, contrairement aux capteurs autonomes Azure ATP. Pour désigner manuellement un capteur Azure ATP comme candidat synchronisateur de domaine, définissez l’option **Candidat synchronisateur de domaine** sur **Activé** dans l’écran de configuration.   
        
    - Il est recommandé de ne pas activer les capteurs Azure ATP de site distant comme des candidats synchronisateurs de domaine.
   
    - Ne désignez pas des contrôleurs de domaine en lecture seule comme candidats synchronisateurs de domaine. Pour plus d’informations sur la synchronisation de domaine Azure ATP, consultez [Architecture Azure ATP](atp-architecture.md#azure-atp-sensor-features).
  
3. Cliquez sur **Save**.


## <a name="validate-installations"></a>Valider les installations
Pour vous assurer que le capteur Azure ATP a été déployé avec succès, effectuez les étapes suivantes :

1. Vérifiez que le service nommé **Capteur Azure - Protection avancée contre les menaces** est en cours d’exécution. Après avoir enregistré les paramètres du capteur Azure ATP, vous devrez peut-être patienter quelques secondes avant le démarrage du service.

2. Si le service ne démarre pas, examinez le fichier Microsoft.Tri.sensor-Errors.log situé dans le dossier par défaut suivant : %programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs.
 
   >[!NOTE]
   > La version d’Azure ATP est fréquemment mise à jour. Pour vérifier la version, dans le portail Azure ATP, accédez à **Configuration**, puis à **À propos**. 

3. Accédez à l’URL de votre instance Azure ATP. Dans le portail Azure ATP, recherchez un élément dans la barre de recherche, tel qu’un utilisateur ou un groupe de votre domaine.



> [!div class="step-by-step"]
> [« Étape 4](install-atp-step4.md)
> [Étape 6 »](install-atp-step6-vpn.md)



## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
