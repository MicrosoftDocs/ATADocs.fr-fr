---
title: Mise à jour des capteurs Microsoft Defender pour Identity
description: Explique comment mettre à jour et différer les mises à jour de capteurs dans Microsoft Defender pour Identity.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 094e853cb3c58ad43d9b52898e3bc7b2bcd72bca
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93274239"
---
# <a name="update-product-long-sensors"></a>Mise à jour des capteurs [!INCLUDE [Product long](includes/product-long.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Il est essentiel de maintenir les capteurs [!INCLUDE [Product long](includes/product-long.md)] à jour pour bénéficier de la meilleure protection possible dans votre organisation.

Le service [!INCLUDE [Product long](includes/product-long.md)] est en général mis à jour plusieurs fois par mois : nouvelles détections, nouvelles fonctionnalités et amélioration du niveau de performance. Elles s’accompagnent souvent d’une mise à jour mineure des capteurs. Les capteurs [!INCLUDE [Product short](includes/product-short.md)] et les mises à jour correspondantes ne possèdent jamais d’autorisations d’accès en écriture à vos contrôleurs de domaine. Les mises à jour contrôlent seulement les capteurs [!INCLUDE [Product short](includes/product-short.md)] et leurs fonctionnalités de détection.

## <a name="product-short-sensor-update-types"></a>Types de mises à jour des capteurs [!INCLUDE [Product short](includes/product-short.md)]

Les capteurs [!INCLUDE [Product short](includes/product-short.md)] acceptent deux types de mises à jour :

- Mises à jour des versions mineures :
  - Fréquentes
  - Sans installation MSI ni modification du Registre
  - Redémarré : services de capteur [!INCLUDE [Product short](includes/product-short.md)]
  - Pas de redémarrage : services de contrôleur de domaine et système d’exploitation du serveur

- Mises à jour des versions majeures :
  - Rares
  - Modifications importantes
  - Redémarré : services de capteur [!INCLUDE [Product short](includes/product-short.md)]
  - Redémarrage potentiellement requis : services de contrôleur de domaine et système d’exploitation du serveur

> [!NOTE]
>
> - Contrôlez le redémarrage automatique des capteurs (pour les mises à jour **majeures** ) sur la page de configuration du portail [!INCLUDE [Product short](includes/product-short.md)].
> - Le capteur [!INCLUDE [Product short](includes/product-short.md)] réserve toujours au moins 15 % de la mémoire et du processeur disponibles sur le contrôleur de domaine sur lequel il est installé. Si le service [!INCLUDE [Product short](includes/product-short.md)] consomme trop de mémoire, il est automatiquement arrêté et redémarré par le service de mise à jour des capteurs [!INCLUDE [Product short](includes/product-short.md)].

## <a name="delayed-sensor-update"></a>Mise à jour différée des capteurs

Compte tenu du rythme rapide de développement de [!INCLUDE [Product short](includes/product-short.md)] et de publication des mises à jour, vous pouvez décider de définir un sous-groupe de capteurs comme anneau de mise à jour différée. Le processus de mise à jour des capteurs sera ainsi progressif. [!INCLUDE [Product short](includes/product-short.md)] vous permet de choisir la façon dont vos capteurs sont mis à jour et de définir chacun d’eux comme candidat à la **Mise à jour différée**.

Les capteurs non sélectionnés pour la mise à jour différée sont automatiquement mis à jour à chaque mise à jour du service [!INCLUDE [Product short](includes/product-short.md)]. Les capteurs définis sur **Mise à jour différée** sont mis à jour après un délai de 72 heures suivant la publication officielle de la mise à jour du service.

L’option **Mise à jour différée** permet de sélectionner certains capteurs comme boucle de mise à jour automatique, sur laquelle toutes les mises à jour sont déployées automatiquement, et de configurer le reste des capteurs pour une mise à jour différée. Cette méthode vous laisse le temps de vérifier que la mise à jour automatique des premiers capteurs a réussi.

> [!NOTE]
> Si une erreur se produit et qu’un capteur ne se met pas à jour, ouvrez un ticket de support. Pour renforcer votre proxy en ne communiquant qu’avec votre instance, consultez [Configuration du proxy](configure-proxy.md).
L’authentification entre vos capteurs et le service cloud Azure est mutuelle, forte et basée sur les certificats.

Chaque mise à jour est testée et validée sur tous les systèmes d’exploitation pris en charge pour minimiser l’impact sur votre réseau et vos opérations.

Pour définir un capteur sur une mise à jour différée :

1. Sur le portail [!INCLUDE [Product short](includes/product-short.md)], cliquez sur l’icône des paramètres, puis sélectionnez **Configuration**.
1. Cliquez sur l’onglet **Mises à jour**.
1. Dans la ligne du tableau, à côté de chaque capteur que vous voulez différer, positionnez le curseur **Mise à jour différée** sur **Activé**.
1. Cliquez sur **Save**.

## <a name="sensor-update-process"></a>Processus de mise à jour des capteurs

À intervalles réguliers de quelques minutes, les capteurs [!INCLUDE [Product short](includes/product-short.md)] vérifient s’ils possèdent la dernière version. Une fois la version du service cloud [!INCLUDE [Product short](includes/product-short.md)] mise à jour, le service de capteur [!INCLUDE [Product short](includes/product-short.md)] commence le processus de mise à jour :

1. Le service cloud [!INCLUDE [Product short](includes/product-short.md)] se met à jour (dernière version).
1. Le service de mise à jour des capteurs [!INCLUDE [Product short](includes/product-short.md)] détecte la version mise à jour.
1. Les capteurs qui ne sont pas définis sur **Mise à jour différée** commencent un par un le processus de mise à jour :
    1. Le service de mise à jour des capteurs [!INCLUDE [Product short](includes/product-short.md)] récupère la version mise à jour auprès du service cloud (au format de fichier .cab).
    1. Le service de mise à jour des capteurs [!INCLUDE [Product short](includes/product-short.md)] valide la signature du fichier.
    1. Le service de mise à jour des capteurs [!INCLUDE [Product short](includes/product-short.md)] extrait le fichier .cab dans un nouveau dossier à l’intérieur du dossier d’installation du capteur, par défaut *C:\Program Files\Azure Advanced Threat Protection Sensor\<version number>* .
    1. Le service de capteur [!INCLUDE [Product short](includes/product-short.md)] pointe vers les nouveaux fichiers extraits à partir du fichier .cab.
    1. Le service de mise à jour des capteurs [!INCLUDE [Product short](includes/product-short.md)] redémarre le service de capteur [!INCLUDE [Product short](includes/product-short.md)].
        > [!NOTE]
        > Les mises à jour mineures de capteurs n’installent aucun MSI et ne modifient ni valeurs de Registre ni fichiers système. Elles ne sont pas non plus affectées par les redémarrages en attente.
    1. Les capteurs s’exécutent en fonction de la version mise à jour.
    1. Le capteur reçoit l’autorisation du service cloud Azure. Vous pouvez vérifier le statut du capteur sur la page **Mises à jour**.
    1. Le capteur suivant démarre le processus de mise à jour.

1. 72 heures après la mise à jour du service cloud [!INCLUDE [Product short](includes/product-short.md)], les capteurs sélectionnés pour la **Mise à jour différée** commencent leur processus de mise à jour, identique à celui des capteurs mis à jour automatiquement.

![Mise à jour des capteurs](media/sensor-update.png)

En cas d’échec du processus de mise à jour sur un capteur, une alerte d’intégrité est déclenchée et envoyée sous forme de notification.

![Échec de la mise à jour d’un capteur](media/sensor-outdated.png)

## <a name="see-also"></a>Voir aussi

- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Prérequis de [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Consulter le forum [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity)
