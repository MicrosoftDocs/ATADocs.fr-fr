---
title: Tutoriel sur les alertes d’exfiltration Azure ATP | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of exfiltration phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 02/11/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 452d951c-5f49-4a21-ae10-9fb38c3de302
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 94e73ecb2980c851aec6ff391c49fff88e4961c8
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56263639"
---
# <a name="tutorial-exfiltration-alerts"></a>Didacticiel : Alertes d’exfiltration  

En général, les attaques sont lancées contre des entités accessibles, par exemple un utilisateur avec des privilèges peu élevés, puis rapidement, elles se déplacent latéralement jusqu’à ce que l’attaquant parvienne à accéder à des ressources importantes, comme des comptes sensibles, des administrateurs de domaine ou des données hautement sensibles. Azure ATP identifie ces menaces avancées à la source tout au long de la chaîne d’annihilation des attaques et les classifie selon les phases suivantes :

1. [Reconnaissance](atp-reconnaissance-alerts.md)
2. [Informations d’identification compromises](atp-compromised-credentials-alerts.md)
3. [Mouvements latéraux](atp-lateral-movement-alerts.md)
4. [Dominance du domaine](atp-domain-dominance-alerts.md)
5. **Exfiltration**

Pour en savoir plus sur la structure et les composants courants de toutes les alertes de sécurité Azure ATP, consultez [Présentation des alertes de sécurité](understanding-security-alerts.md).

Les alertes de sécurité suivantes vous aident à identifier et à résoudre les activités suspectes de la phase **Exfiltration** détectées par Azure ATP sur votre réseau. Dans ce tutoriel, vous allez apprendre à comprendre, classifier, prévenir et empêcher les attaques suivantes :

> [!div class="checklist"]
> * Communication suspecte sur DNS (ID externe 2031)
> * Exfiltration de données sur SMB (ID externe 2030)

## <a name="suspicious-communication-over-dns-external-id-2031"></a>Communication suspecte sur DNS (ID externe 2031) 

*Nom précédent* : Communication suspecte sur DNS

**Description**

Dans la plupart des organisations, le protocole DNS n’est généralement pas surveillé et les activités malveillantes sont rarement bloquées. Un attaquant peut alors accéder à une machine compromise afin d’utiliser le protocole DNS de manière abusive. Des communications malveillantes via DNS peuvent être utilisées pour l’exfiltration des données, la commande et le contrôle et/ou pour l’affranchissement des limitations du réseau d’entreprise.

**TP, B-TP ou FP ?**
 
Certaines entreprises utilisent DNS de manière légitime pour les communications régulières. Pour déterminer l’état de l’alerte de sécurité :

1. Vérifiez si le domaine de requête inscrit appartient à une source approuvée, comme votre fournisseur d’antivirus.  
    - Considérez-la comme une activité **B-TP** si le domaine est connu et approuvé et que les requêtes DNS sont autorisées. *Fermez* l’alerte de sécurité et excluez le domaine des alertes ultérieures.  
    - Si le domaine de requête inscrit n’est pas approuvé, identifiez le processus qui crée la requête sur l’ordinateur source. Utilisez le [Moniteur de processus](https://docs.microsoft.com/sysinternals/downloads/procmon) pour vous aider dans cette tâche.

**Comprendre l’étendue de la violation**

1. Sur l’ordinateur de destination, qui doit être un serveur DNS, vérifiez les enregistrements du domaine en question.
    - Avec quelle adresse IP est-il associé ?
    - Qui est le propriétaire du domaine ?
    - Où se trouve l’adresse IP ?
1. Examinez les [ordinateurs source et de destination](investigate-a-computer.md).

**Suggestions de correction et étapes préventives**

1. Incluez l’ordinateur source.
    - Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    - Recherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.
2. Si après votre investigation le domaine de requête inscrit demeure non approuvé, nous vous recommandons de bloquer le domaine de destination afin d’éviter toute communication future.

> [!NOTE]
> Les alertes de sécurité *Communications suspectes via DNS* indiquent le domaine suspecté. Les nouveaux domaines, ou les domaines récemment ajoutés qui ne sont pas encore connus ou reconnus par Azure ATP, mais qui sont connus de votre organisation ou en font partie, peuvent être fermés.

## <a name="data-exfiltration-over-smb-external-id-2030"></a>Exfiltration de données sur SMB (ID externe 2030)

**Description** Les contrôleurs de domaine contiennent les données les plus sensibles de l’organisation. Pour la plupart des attaquants, l’une des priorités consiste à accéder au contrôleur de domaine afin de dérober vos données les plus sensibles. Par exemple, l’exfiltration du fichier Ntds.dit, stocké sur le contrôleur de domaine, permet à un attaquant de falsifier des tickets TGT (Ticket Granting Ticket) Kerberos fournissant une autorisation d’accès à n’importe quelle ressource. Les tickets TGT Kerberos falsifiés permettent à l’attaquant d’affecter au délai d’expiration du ticket n’importe quelle valeur arbitraire. Une alerte Azure ATP d’**exfiltration de données sur SMB** se déclenche quand des transferts de données suspects sont observés à partir de vos contrôleurs de domaine supervisés.

**TP, B-TP ou FP**
1. Ces utilisateurs sont-ils censés copier ces fichiers sur cet ordinateur ?  
    - Si la réponse à cette question est **oui**, **fermez** l’alerte de sécurité comme s’agissant d’une activité **B-TP** et excluez l’ordinateur.

**Comprendre l’étendue de la violation**
1. Examinez les [utilisateurs sources](investigate-a-user.md).  
2. Examinez les [ordinateurs sources et de destination](investigate-a-computer.md) des copies. 

**Suggestions de correction et étapes préventives**
1. Réinitialisez le mot de passe des utilisateurs sources et activez MFA.
2. Incluez l’ordinateur source.
    - Trouvez l’outil qui a effectué l’attaque et supprimez-le.
    - Recherchez les fichiers qui ont été copiés et supprimez-les. 
    <br>Vérifiez s’il y a eu d’autres activités sur ces fichiers. Ont-ils été transférés vers un autre emplacement ? Vérifiez s’ils ont été transférés hors du réseau de l’organisation. 
    - Recherchez les utilisateurs connectés au moment de l’activité, car ils peuvent également être compromis. Réinitialisez leurs mots de passe et activez l’authentification multifacteur.
3. Si l’un des fichiers est le fichier **ntds.dit** :
    - Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
    - Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. L’invalidation de tous les tickets Kerberos dans le domaine signifie que **tous** les services seront interrompus et ne refonctionneront qu’une fois qu’ils auront été renouvelés ou, dans certains cas, redémarrés.

    - **Planifiez soigneusement avant d’effectuer la double réinitialisation KRBTGT. Celle-ci impacte tous les ordinateurs, serveurs et utilisateurs de l’environnement.**

   - Fermez toutes les sessions existantes sur les contrôleurs de domaine. 

## <a name="see-also"></a>Voir aussi

- [Examiner un ordinateur](investigate-a-computer.md)
- [Utilisation des alertes de sécurité](working-with-suspicious-activities.md)
- [Utilisation des chemins de mouvement latéral](use-case-lateral-movement-path.md)
- [Alertes de reconnaissance](atp-reconnaissance-alerts.md)
- [Alertes indiquant des informations d’identification compromises](atp-compromised-credentials-alerts.md)
- [Alertes de mouvement latéral](atp-lateral-movement-alerts.md)
- [Alertes de dominance du domaine](atp-domain-dominance-alerts.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
