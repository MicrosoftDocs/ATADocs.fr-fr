---
title: Mettre à jour vos capteurs Azure ATP | Microsoft Docs
description: Décrit comment mettre à jour et différer la mise à jour des capteurs dans Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/14/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 603d9e09-a07d-4357-862f-d5682c8bc3dd
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f2df8f8f59edff7ebda3f86aae26b899913d57f8
ms.sourcegitcommit: e2daa0f93d97d552cfbf1577fbd05a547b63e95b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54314327"
---
*S’applique à : Azure - Protection avancée contre les menaces*


# <a name="update-azure-atp-sensors"></a>Mettre à jour les capteurs Azure ATP
Il est essentiel de garder Azure - Protection avancée contre les menaces à jour pour bénéficier de la meilleure protection possible dans votre organisation.

Le service Azure ATP est mis à jour plusieurs fois par mois avec des correctifs de bogues, des améliorations de performance et de nouvelles détections. Ces mises à jour nécessitent parfois une mise à jour correspondante pour les capteurs. 

Si vous ne mettez pas à jour vos capteurs, ces derniers risquent de ne pas pouvoir communiquer avec le service cloud Azure ATP, ce qui peut entraîner une dégradation du service. 

L’authentification entre vos capteurs et le service cloud Azure est mutuelle, forte et basée sur les certificats. 

Chaque mise à jour est testée et validée sur tous les systèmes d’exploitation pris en charge pour minimiser l’impact sur votre réseau et vos opérations.

### <a name="azure-atp-sensor-update-types"></a>Types de mise à jour des capteurs Azure ATP   

Les capteurs Azure ATP prennent en charge deux types de mises à jour :
- Mises à jour des versions mineures : 
  - Fréquentes 
  - N’exigent aucune installation MSI ni aucun changement de Registre
  - Redémarrages du service de capteur Azure ATP
  - Les contrôleurs de domaine et le serveur n’ont pas besoin d’être redémarrés

- Mises à jour des versions majeures :
 - Rares
 - Peut nécessiter un redémarrage des contrôleurs de domaine et des serveurs
 - Contiennent des changements importants 

> [!NOTE]
>- Le redémarrage automatique des capteurs (dans les mises à jour importantes) peut être contrôlé dans la page de configuration. 
> - Le capteur Azure ATP conserve toujours au moins 15 % de la mémoire et de l’UC disponibles. Si le service consomme trop de mémoire, il est redémarré automatiquement par le service de mise à jour de capteur Azure ATP.

## <a name="delayed-sensor-update"></a>Mise à jour différée des capteurs
Pour un processus de mise à jour plus progressif, Azure ATP vous permet de définir un capteur comme candidat à une **Mise à jour différée**. 

En règle générale, les capteurs se mettent à jour automatiquement lorsque le service cloud Azure ATP est mis à jour. Les capteurs définis sur **Mise à jour différée** se mettent à jour 24 heures après la mise à jour initiale du service cloud.

Cela vous permet de sélectionner des capteurs spécifiques sur lesquels la mise à jour est déployée automatiquement et de mettre à jour le reste de vos capteurs plus tard, uniquement après avoir vu que la mise à jour initiale s’est bien passée.

> [!NOTE]
> Si une erreur se produit et qu’un capteur ne se met pas à jour, ouvrez un ticket de support. Pour renforcer votre proxy en ne communiquant qu’avec votre instance, consultez [Configuration du proxy](configure-proxy.md).

Pour définir un capteur sur une mise à jour différée :

1. Dans le portail Azure ATP, cliquez sur l’icône des paramètres, puis sélectionnez **Configuration**.
2. Cliquez sur l’onglet **Mises à jour**.
3. Dans la ligne du tableau, à côté de chaque capteur que vous voulez différer, positionnez le curseur **Mise à jour différée** sur **Activé**.
4. Cliquez sur **Save**.
 
## <a name="sensor-update-process"></a>Processus de mise à jour des capteurs

À intervalles réguliers de quelques minutes, les capteurs Azure ATP vérifient s’ils ont la version la plus récente. Une fois que le service cloud Azure ATP est mis à jour avec une version plus récente, le service de capteur Azure ATP démarre le processus de mise à jour :

1. Le service cloud Azure ATP effectue la mise à jour avec la dernière version.
2. Le service de mise à jour de capteur Azure ATP découvre qu’il y a une version mise à jour.
3. Les capteurs qui ne sont pas définis sur **Mise à jour différée** démarrent le processus de mise à jour :
  1. Le service de mise à jour de capteur Azure ATP tire la version mise à jour du service cloud (au format de fichier cab).
  2. Le service de mise à jour de capteur Azure ATP valide la signature du fichier.
  3. Le service de mise à jour de capteur Azure ATP extrait le fichier cab vers un nouveau dossier dans le dossier d’installation du capteur. Par défaut, il est extrait dans *C:\Program Files\Azure Advanced Threat Protection Sensor\<numéro de version >*
  4. Le service de mise à jour de capteur Azure ATP redémarre le service de capteur Azure ATP.
  5. Le service de capteur Azure ATP pointe vers les nouveaux fichiers extraits à partir du fichier cab.
  > [!NOTE]
  >Une mise à jour mineure des capteurs n’installe pas de MSI, ni ne change aucune valeur de Registre ni aucun fichier système. Même un redémarrage en attente n’impacte pas la mise à jour des capteurs. 
  6. Les capteurs s’exécutent en fonction de la version qui vient d’être mise à jour.
  7. Un capteur reçoit l’autorisation du service cloud Azure. Cela peut être vérifié dans la page **Mises à jour**.
  8. Le capteur suivant démarre le processus de mise à jour. 

4. 24 heures après la mise à jour du service cloud Azure ATP, les capteurs sélectionnés pour une **Mise à jour différée** démarrent le processus de mise à jour.

![mise à jour des capteurs](./media/sensor-update.png)


En cas d’échec de la mise à jour, si le capteur n’a pas terminé le processus de mise à jour, une alerte de supervision appropriée est déclenchée et envoyée comme notification.

![capteur obsolète](./media/sensor-outdated.png)


## <a name="see-also"></a>Voir aussi

- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)