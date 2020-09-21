---
title: Installer Azure Advanced Threat Protection
description: Dans cette étape d’installation d’ATP, vous configurez des sources de données.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/19/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9b3a8e59017c5b356cee7e66b6e81151bd13997a
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90826462"
---
# <a name="configure-event-collection"></a>Configurer la collecte d’événements

Pour améliorer les capacités de détection, Azure ATP a besoin des événements Windows qui sont listés dans [Configurer la collecte des événements](configure-windows-event-collection.md#configure-event-collection). Ces événements peuvent être lus automatiquement par le capteur Azure ATP ou, si le capteur Azure ATP n’est pas déployé, ils peuvent être transférés au capteur autonome Azure ATP de deux manières : en configurant le capteur autonome Azure ATP afin qu’il reste à l’écoute des événements SIEM ou en [configurant les transferts d’événements Windows](configure-event-forwarding.md).

> [!NOTE]
>
> - Les capteurs autonomes Azure ATP ne prennent pas en charge la collecte d’entrées de journal du Suivi d’événements pour Windows (ETW) qui fournissent les données pour de nombreuses détections. Pour une couverture complète de votre environnement, nous vous recommandons de déployer le capteur Azure ATP.
> - Il est important d’exécuter le script d’audit d’Azure ATP avant de configurer la collecte d’événements, pour vérifier que les contrôleurs de domaine sont correctement configurés pour enregistrer les événements nécessaires.

Outre la collecte et l’analyse du trafic réseau à destination et en provenance des contrôleurs de domaine, Azure ATP peut utiliser des événements Windows pour améliorer les détections. Vous pouvez recevoir ces événements à partir de votre serveur SIEM ou définir le transfert d’événements Windows à partir de votre contrôleur de domaine. Les événements collectés fournissent à Azure ATP des informations supplémentaires qui ne sont pas accessibles par le biais du trafic réseau du contrôleur de domaine.

## <a name="ntlm-authentication-using-windows-event-8004"></a>Authentification NTLM avec l’événement Windows 8004

Pour configurer la collecte d’événements Windows 8004 :

1. Accédez à : Configuration de l’ordinateur\Stratégies\ Paramètres Windows\Paramètres de sécurité\Stratégies locales\Options de sécurité
1. Définissez la **stratégie de groupe de domaine** comme suit :
    - Sécurité réseau : Restreindre NTLM : Trafic NTLM sortant vers serveurs distants = **Auditer tout**
    - Sécurité réseau : Restreindre NTLM : Auditer l’authentification NTLM dans ce domaine = **Activer tout**
    - Sécurité réseau : Restreindre NTLM : Auditer le trafic NTLM entrant = **Activer l’audit pour tous les comptes**

Lorsque l’événement Windows 8004 est analysé par le capteur Azure ATP,  les activités d’authentification NTLM Azure ATP sont enrichies avec les données ayant fait l’objet d’un accès par le serveur.

## <a name="siemsyslog"></a>SIEM/Syslog

Les capteurs autonomes Azure ATP sont configurés par défaut pour recevoir les données Syslog. Pour que les capteurs autonomes Azure ATP puissent consommer les données dont vous avez besoin pour transférer vos données syslog au capteur.

> [!NOTE]
> Azure ATP écoute uniquement sur IPv4 et non sur IPv6.

> [!IMPORTANT]
>
> - Ne transférez pas toutes les données Syslog au capteur Azure ATP.
> - Azure ATP prend en charge le trafic UDP provenant du serveur SIEM/Syslog.

Pour plus d’informations sur la façon de configurer le transfert d’événements spécifiques vers un autre serveur, consultez la documentation produit de votre serveur SIEM/Syslog.

> [!NOTE]
> Si vous n’utilisez pas un serveur SIEM/Syslog, vous pouvez configurer vos contrôleurs de domaine Windows de façon à transférer tous les événements nécessaires pour qu’ils soient collectés et analysés par Azure ATP.

## <a name="configuring-the-azure-atp-sensor-to-listen-for-siem-events"></a>Configuration du capteur Azure ATP pour écouter les événements SIEM

- Configurez votre serveur SIEM ou Syslog pour transférer tous les événements requis à l’adresse IP de l’un des capteurs autonomes Azure ATP. Pour plus d’informations sur la configuration de votre serveur SIEM, consultez l’aide en ligne de SIEM ou explorez les options de support technique à votre disposition pour obtenir les formats à respecter pour chaque serveur SIEM.

Azure ATP prend en charge les événements SIEM aux formats suivants :

### <a name="rsa-security-analytics"></a>RSA Security Analytics

&lt;En-tête Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

- L’en-tête syslog est facultatif.

- Le séparateur de caractère « \n » est obligatoire entre tous les champs.
- Les champs, dans l’ordre, sont les suivants :
    1. Constante RsaSA (doit être indiquée).
    2. Horodatage de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodatage de l’arrivée au serveur SIEM ou de l’envoi à ATP). De préférence avec une précision de l’ordre de la milliseconde (ceci est important).
    3. ID de l’événement Windows
    4. Nom du fournisseur d’événements Windows
    5. Nom du journal des événements Windows
    6. Nom de l’ordinateur recevant l’événement (ici, le contrôleur de domaine).
    7. Nom de l’utilisateur qui s’authentifie.
    8. Nom de l’hôte source.
    9. Code de résultat de NTLM.
- L’ordre est important, et rien d’autre ne doit figurer dans le message.

### <a name="microfocus-arcsight"></a>MicroFocus ArcSight

CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Le contrôleur de domaine a tenté de valider les informations d’identification d’un compte.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

- Doit être conforme à la définition du protocole.

- Aucun en-tête syslog.
- La partie en-tête, séparée par une barre verticale, doit exister (comme indiqué dans le protocole).
- Les clés suivantes dans la partie _Extension_ doivent être présentes dans l’événement :
  - externalId = ID de l’événement Windows.
  - rt = horodatage de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodatage de l’arrivée au serveur SIEM ou de l’envoi à ATP). De préférence avec une précision de l’ordre de la milliseconde (ceci est important).
  - cat = nom du journal des événements Windows.
  - shost = nom de l’hôte source.
  - dhost = nom de l’ordinateur recevant l’événement (ici, le contrôleur de domaine).
  - duser = utilisateur qui s’authentifie.
- L’ordre de la partie _Extension_ n’est pas important.
- Vous devez avoir une clé personnalisée et un libellé dé clé pour les deux champs suivants :
  - « EventSource »
  - « Reason or Error Code » = code de résultat de NTLM

### <a name="splunk"></a>Splunk

&lt;En-tête Syslog&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

L’ordinateur a tenté de valider les informations d’identification d’un compte.

Package d’authentification : MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Compte d’ouverture de session : Administrateur

Station de travail source : SIEM

Code d’erreur : 0x0

- L’en-tête syslog est facultatif.

- Le séparateur de caractère « \r\n » est utilisé entre tous les champs obligatoires.
- Les champs sont au format clé = valeur.
- Les clés suivantes doivent exister et avoir une valeur :
  - EventCode = ID de l’événement Windows.
  - Logfile = nom du journal des événements Windows.
  - SourceName = nom du fournisseur d’événements Windows.
  - TimeGenerated = horodatage de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodatage de l’arrivée au serveur SIEM ou de l’envoi à ATP). Le format doit être aaaaMMjjHHmmss.FFFFFF, avec de préférence une précision de l’ordre de la milliseconde (ceci est important).
  - ComputerName = nom de l’hôte source.
  - Message = texte de l’événement Windows d’origine.
- La clé et la valeur du message DOIVENT figurer en dernier.
- L’ordre n’est pas important pour les paires clé=valeur.

### <a name="qradar"></a>QRadar

QRadar permet la collecte d’événements par le biais d’un agent. Si les données sont recueillies au moyen d’un agent, le format de l’heure est collecté sans les données des millisecondes. Azure ATP nécessitant les données des millisecondes, vous devez définir QRadar pour qu’il utilise la collecte d’événements Windows sans agent. Pour plus d’informations, consultez [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar : Collecte d’événements Windows sans agent avec le protocole MSRPC").

```text
<13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0
```

Les champs requis sont les suivants :

- Type d’agent pour la collecte

- Nom du fournisseur de journaux des événements Windows
- Source du journal des événements Windows
- Nom de domaine complet du contrôleur de domaine
- ID de l’événement Windows

TimeGenerated représente l’horodatage de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodatage de l’arrivée au serveur SIEM ou de l’envoi à ATP). Le format doit être aaaaMMjjHHmmss.FFFFFF, avec de préférence une précision de l’ordre de la milliseconde (ceci est important).

Message représente le texte de l’événement Windows d’origine.

Assurez-vous que \t sépare les paires clé/valeur.

>[!NOTE]
> Utiliser WinCollect pour la collecte des événements Windows n’est pas pris en charge.

## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement Azure ATP](https://aka.ms/aatpsizingtool)
- [Informations de référence sur le journal SIEM Azure ATP](cef-format-sa.md)
- [Prérequis d’Azure ATP](prerequisites.md)
- [Consultez le forum Azure ATP !](https://aka.ms/azureatpcommunity)
