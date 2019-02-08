---
title: Mettre à jour vos capteurs Azure ATP | Microsoft Docs
description: Décrit comment mettre à jour et différer la mise à jour des capteurs dans Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/20/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 603d9e09-a07d-4357-862f-d5682c8bc3dd
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c7b131bffdca092d6355a7f8cb4d280c2388b8eb
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54840809"
---
# <a name="update-azure-atp-sensors"></a>Mettre à jour les capteurs Azure ATP

Il est essentiel de maintenir Azure Advanced Threat Protection à jour pour bénéficier de la meilleure protection possible dans votre organisation.

Le service Azure ATP est en général mis à jour plusieurs fois par mois : nouvelles détections, nouvelles fonctionnalités et améliorations des performances. Elles s’accompagnent souvent d’une mise à jour mineure des capteurs. Les capteurs Azure ATP et les mises à jour correspondantes n’ont jamais d’autorisations d’accès en écriture à vos contrôleurs de domaine. Les mises à jour contrôlent seulement les capteurs Azure ATP et leurs fonctionnalités de détection. 

### <a name="azure-atp-sensor-update-types"></a>Types de mise à jour des capteurs Azure ATP   

Les capteurs Azure ATP acceptent deux types de mises à jour :
- Mises à jour des versions mineures : 
    - Fréquentes 
    - Sans installation MSI ni modification du Registre
    - Redémarrage : services de capteur Azure ATP 
    - Pas de redémarrage : services de contrôleur de domaine et système d’exploitation du serveur

- Mises à jour des versions majeures :
    - Rares
    - Modifications importantes 
    - Redémarrage : services de capteur Azure ATP
    - Redémarrage potentiellement requis : services de contrôleur de domaine et système d’exploitation du serveur

> [!NOTE]
>- Contrôlez les redémarrages automatiques des capteurs (pour les mises à jour **majeures**) sur la page de configuration du portail Azure ATP. 
> - Le capteur Azure ATP réserve toujours au moins 15 % de la mémoire et du processeur disponibles sur le contrôleur de domaine sur lequel il est installé. Si le service Azure ATP consomme trop de mémoire, il est automatiquement arrêté et redémarré par le service de mise à jour des capteurs Azure ATP.

### <a name="update-requirement"></a>Obligation de mise à jour

Les capteurs en retard de plus d’une mise à jour ne peuvent plus communiquer avec le service cloud Azure ATP, ce qui risque de provoquer une indisponibilité du service Azure ATP et un défaut de protection pour votre organisation.  

## <a name="delayed-sensor-update"></a>Mise à jour différée des capteurs

Compte tenu du rythme rapide de développement d’Azure ATP et de publication des mises à jour, vous pouvez décider de définir un sous-groupe de capteurs comme boucle de mise à jour différée afin de rendre progressif le processus de mise à jour des capteurs. Azure ATP vous permet de choisir la façon dont vos capteurs sont mis à jour et de définir chacun d’eux comme candidat à la **Mise à jour différée**.  

Les capteurs non sélectionnés pour la mise à jour différée sont automatiquement mis à jour à chaque mise à jour du service Azure ATP. Les capteurs définis sur **Mise à jour différée** sont mis à jour après un délai de 72 heures suivant la publication officielle de la mise à jour du service. 

L’option **Mise à jour différée** permet de sélectionner certains capteurs comme boucle de mise à jour automatique, sur laquelle toutes les mises à jour sont déployées automatiquement, et de configurer le reste des capteurs pour une mise à jour différée. Cette méthode vous laisse le temps de vérifier que la mise à jour automatique des premiers capteurs a réussi.

> [!NOTE]
> Si une erreur se produit et qu’un capteur ne se met pas à jour, ouvrez un ticket de support. Pour renforcer votre proxy en ne communiquant qu’avec votre instance, consultez [Configuration du proxy](configure-proxy.md).
L’authentification entre vos capteurs et le service cloud Azure est mutuelle, forte et basée sur les certificats. 

Chaque mise à jour est testée et validée sur tous les systèmes d’exploitation pris en charge pour minimiser l’impact sur votre réseau et vos opérations.


Pour définir un capteur sur une mise à jour différée :

1. Dans le portail Azure ATP, cliquez sur l’icône des paramètres, puis sélectionnez **Configuration**.
2. Cliquez sur l’onglet **Mises à jour**.
3. Dans la ligne du tableau, à côté de chaque capteur que vous voulez différer, positionnez le curseur **Mise à jour différée** sur **Activé**.
4. Cliquez sur **Save**.
 
## <a name="sensor-update-process"></a>Processus de mise à jour des capteurs

À intervalles réguliers de quelques minutes, les capteurs Azure ATP vérifient s’ils ont la version la plus récente. Une fois que le service cloud Azure ATP est mis à jour avec une version plus récente, le service de capteur Azure ATP démarre le processus de mise à jour :

1. Le service cloud Azure ATP se met à jour (dernière version).
2. Le service de mise à jour des capteurs Azure ATP détecte la version mise à jour.
3. Les capteurs qui ne sont pas définis sur **Mise à jour différée** commencent un par un le processus de mise à jour :
   1. Le service de mise à jour des capteurs Azure ATP récupère la version mise à jour auprès du service cloud (au format de fichier .cab).
   2. Le service de mise à jour des capteurs Azure ATP valide la signature du fichier.
   3. Le service de mise à jour des capteurs Azure ATP extrait le fichier .cab dans un nouveau dossier du dossier d’installation du capteur, par défaut *C:\Program Files\Azure Advanced Threat Protection Sensor\<numéro de version>*.
   4. Le service de capteur Azure ATP pointe vers les nouveaux fichiers extraits à partir du fichier .cab.    
   5. Le service de mise à jour des capteurs Azure ATP redémarre le service de capteur Azure ATP.
       > [!NOTE]
      >Les mises à jour mineures de capteurs n’installent aucun MSI et ne modifient ni valeurs de Registre ni fichiers système. Elles ne sont pas non plus affectées par les redémarrages en attente. 
   6. Les capteurs s’exécutent en fonction de la version mise à jour.
   7. Le capteur reçoit l’autorisation du service cloud Azure. Vous pouvez vérifier le statut du capteur sur la page **Mises à jour**.
   8. Le capteur suivant démarre le processus de mise à jour. 

4. 72 heures après la mise à jour du service cloud Azure ATP, les capteurs sélectionnés pour la **Mise à jour différée** commencent leur processus de mise à jour, identique à celui des capteurs mis à jour automatiquement.

![Mise à jour des capteurs](./media/sensor-update.png)


En cas d’échec du processus de mise à jour sur un capteur, une alerte de monitoring est déclenchée et envoyée sous forme de notification.

![Échec de la mise à jour d’un capteur](./media/sensor-outdated.png)


## <a name="see-also"></a>Voir aussi

- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)