---
title: Installer Advanced Threat Analytics - Étape 6 | Microsoft Docs
description: Dans cette étape d’installation d’ATA, vous configurez des sources de données.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0481668b3156c616d2556155b615e7a0c58cf459
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2019
ms.locfileid: "58675011"
---
# <a name="install-ata---step-6"></a>Installer ATA - Étape 6

*S’applique à : Advanced Threat Analytics version 1.9*

> [!div class="step-by-step"]
> [« Étape 5](install-ata-step5.md)
> [Étape 7 »](vpn-integration-install-step.md)

## <a name="step-6-configure-event-collection"></a>Étape 6. Configurer la collecte d’événements
### <a name="configure-event-collection"></a>Configurer la collecte d’événements

Pour améliorer les capacités de détection, ATA a besoin des événements Windows suivants : 4776, 4732, 4733, 4728, 4729, 4756, 4757 et 7045. Ils peuvent être lus automatiquement par la passerelle légère ATA ou, si la passerelle légère ATA n’est pas déployée, ils peuvent être transférés à la passerelle ATA de deux manières : en configurant la passerelle ATA pour l’écoute des événements SIEM ou en [configurant le transfert d’événements Windows](configure-event-collection.md). 

> [!NOTE]
> Pour les versions 1.8 et ultérieures d’ATA, la configuration de la collecte d’événements n’est plus nécessaire pour les passerelles légères ATA. La passerelle légère ATA peut désormais lire les événements localement, sans qu’il soit nécessaire de configurer le transfert d’événements.

Outre la collecte et l’analyse du trafic réseau à destination et en provenance des contrôleurs de domaine, ATA peut utiliser des événements Windows pour améliorer les détections. Il utilise l’événement 4776 pour NTLM, qui améliore plusieurs détections et les événements 4732, 4733, 4728, 4729, 4756 et 4757 pour améliorer la détection des modifications de groupes sensibles. Vous pouvez soit recevoir cet événement de votre serveur SIEM, soit définir le transfert d’événements Windows à partir de votre contrôleur de domaine. Les événements collectés fournissent à ATA des informations supplémentaires qui ne sont pas accessibles par le biais du trafic réseau du contrôleur de domaine.

#### <a name="siemsyslog"></a>SIEM/Syslog
Pour qu’ATA puisse consommer des données provenant d’un serveur Syslog, vous devez effectuer les étapes suivantes :

-   Configurez vos serveurs de passerelle ATA pour écouter et accepter les événements transférés à partir du serveur SIEM/Syslog.

> [!NOTE]
> ATA écoute uniquement sur IPv4 et non sur IPv6. 
> -   Configurez votre serveur SIEM/Syslog de façon à transférer des événements spécifiques à la passerelle ATA.
> 
> [!IMPORTANT]
> -   Ne transférez pas toutes les données Syslog vers la passerelle ATA.
> -   ATA prend en charge le trafic UDP provenant du serveur SIEM/Syslog.

Pour plus d’informations sur la façon de configurer le transfert d’événements spécifiques vers un autre serveur, consultez la documentation produit de votre serveur SIEM/Syslog. 

> [!NOTE]
>Si vous n’utilisez pas un serveur SIEM/Syslog, vous pouvez configurer vos contrôleurs de domaine Windows de façon à transférer l’événement Windows associé à l’ID 4776 pour qu’il soit collecté et analysé par ATA. L’événement Windows associé à l’ID 4776 fournit des données relatives aux authentifications NTLM.

#### <a name="configuring-the-ata-gateway-to-listen-for-siem-events"></a>Configuration de la passerelle ATA pour écouter les événements SIEM

1.  Dans la configuration ATA, sous **Sources de données**, cliquez sur **SIEM** et activez **Syslog**, puis cliquez sur **Enregistrer**.

    ![Image de l’activation du protocole UDP de l’écouteur syslog](media/ATA-enable-siem-forward-events.png)

2.  Configurez votre serveur SIEM ou Syslog pour transférer l’événement Windows associé à l’ID 4776 vers l’adresse IP de l’une des passerelles ATA. Pour plus d’informations sur la configuration de votre serveur SIEM, consultez l’aide en ligne de SIEM ou explorez les options de support technique à votre disposition pour obtenir les formats à respecter pour chaque serveur SIEM.

ATA prend en charge les événements SIEM aux formats suivants :  

#### <a name="rsa-security-analytics"></a>RSA Security Analytics
&lt;En-tête Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   L’en-tête syslog est facultatif.

-   Le séparateur de caractère « \n » est obligatoire entre tous les champs.

-   Les champs, dans l’ordre, sont les suivants :

    1.  Constante RsaSA (doit être indiquée).

    2.  Horodateur de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodateur de l’arrivée au serveur SIEM ou de l’envoi à ATA). De préférence avec une précision de l’ordre de la milliseconde (ceci est important).

    3.  ID de l’événement Windows

    4.  Nom du fournisseur d’événements Windows

    5.  Nom du journal des événements Windows

    6.  Nom de l’ordinateur recevant l’événement (ici, le contrôleur de domaine).

    7.  Nom de l’utilisateur qui s’authentifie.

    8.  Nom de l’hôte source.

    9. Code de résultat de NTLM.

-   L’ordre est important, et rien d’autre ne doit figurer dans le message.

#### <a name="hp-arcsight"></a>HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Le contrôleur de domaine a tenté de valider les informations d’identification d’un compte.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   Doit être conforme à la définition du protocole.

-   Aucun en-tête syslog.

-   La partie en-tête, séparée par une barre verticale, doit exister (comme indiqué dans le protocole).

-   Les clés suivantes dans la partie _Extension_ doivent être présentes dans l’événement :

    -   externalId = ID de l’événement Windows.

    -   rt = Horodateur de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodateur de l’arrivée au serveur SIEM ou de l’envoi à ATA). De préférence avec une précision de l’ordre de la milliseconde (ceci est important).

    -   cat = nom du journal des événements Windows.

    -   shost = nom de l’hôte source.

    -   dhost = nom de l’ordinateur recevant l’événement (ici, le contrôleur de domaine).

    -   duser = utilisateur qui s’authentifie.

-   L’ordre de la partie _Extension_ n’est pas important.

-   Vous devez avoir une clé personnalisée et un libellé dé clé pour les deux champs suivants :

    -   « EventSource »

    -   « Reason or Error Code » = code de résultat de NTLM

#### <a name="splunk"></a>Splunk
&lt;En-tête Syslog&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

L’ordinateur a tenté de valider les informations d’identification d’un compte.

Package d’authentification :              MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Compte d’ouverture de session : Administrateur

Station de travail source :       SIEM

Code d’erreur :         0x0

-   L’en-tête syslog est facultatif.

-   Le séparateur de caractère « \r\n » est utilisé entre tous les champs obligatoires.

-   Les champs sont au format clé = valeur.

-   Les clés suivantes doivent exister et avoir une valeur :

    -   EventCode = ID de l’événement Windows.

    -   Logfile = nom du journal des événements Windows.

    -   SourceName = nom du fournisseur d’événements Windows.

    -   TimeGenerated = horodateur de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodateur de l’arrivée au serveur SIEM ou de l’envoi à ATA). Le format doit être aaaaMMjjHHmmss.FFFFFF, avec de préférence une précision de l’ordre de la milliseconde (ceci est important).

    -   ComputerName = nom de l’hôte source.

    -   Message = texte de l’événement Windows d’origine.

-   La clé et la valeur du message DOIVENT figurer en dernier.

-   L’ordre n’est pas important pour les paires clé=valeur.

#### <a name="qradar"></a>QRadar
QRadar permet la collecte d’événements par le biais d’un agent. Si les données sont recueillies au moyen d’un agent, le format de l’heure est collecté sans les données des millisecondes. ATA nécessitant les données des millisecondes, vous devez définir QRadar pour qu’il utilise la collecte d’événements de Windows sans agent. Pour plus d'informations, voir [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar : Collecte d’événements Windows sans agent avec le protocole MSRPC").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Les champs requis sont les suivants :

- Type d’agent pour la collecte
- Nom du fournisseur de journaux des événements Windows
- Source du journal des événements Windows
- Nom de domaine complet du contrôleur de domaine
- ID de l’événement Windows

TimeGenerated représente l’horodateur de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodateur de l’arrivée au serveur SIEM ou de l’envoi à ATA). Le format doit être aaaaMMjjHHmmss.FFFFFF, avec de préférence une précision de l’ordre de la milliseconde (ceci est important).

Message représente le texte de l’événement Windows d’origine.

Assurez-vous que \t sépare les paires clé/valeur.

>[!NOTE] 
> Utiliser WinCollect pour la collecte des événements Windows n’est pas pris en charge.



> [!div class="step-by-step"]
> [« Étape 5](install-ata-step5.md)
> [Étape 7 »](vpn-integration-install-step.md)



## <a name="related-videos"></a>Vidéos connexes
- [Vue d’ensemble du déploiement ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Sélection du type de passerelle ATA approprié](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Voir aussi
- [Guide de déploiement ATA POC](http://aka.ms/atapoc)
- [Outil de dimensionnement ATA](http://aka.ms/atasizingtool)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](ata-prerequisites.md)

