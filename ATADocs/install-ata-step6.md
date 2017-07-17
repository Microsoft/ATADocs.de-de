---
title: "Installieren von Advanced Threat Analytics – Schritt 6 | Microsoft-Dokumentation"
description: In diesem Schritt bei der ATA-Installation konfigurieren Sie Datenquellen.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/5/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ffab11a99ae62c1c0b37c43ee212d87508f886b8
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/05/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# Installieren von ATA – Schritt 6
<a id="install-ata---step-6" class="xliff"></a>

>[!div class="step-by-step"]
[« Schritt 5](install-ata-step5.md)

## Schritt 6: Konfigurieren der Ereignissammlung und VPN
<a id="step-6-configure-event-collection-and-vpn" class="xliff"></a>
### Konfigurieren der Ereignissammlung
<a id="configure-event-collection" class="xliff"></a>
Um die Erkennungsfunktionalität zu verbessern, benötigt ATA die folgenden Windows-Ereignisse: 4776, 4732, 4733, 4728, 4729, 4756, 4757. Diese können entweder automatisch vom ATA-Lightweight-Gateway gelesen werden, oder, falls das ATA-Lightweight-Gateway nicht bereitgestellt wurde, an das ATA-Gateway weitergeleitet werden. Dazu gibt es zwei Möglichkeiten: zum einen das Konfigurieren des ATA-Gateways, sodass es auf SIEM-Ereignisse lauscht, oder das [Konfigurieren der Windows-Ereignisweiterleitung](#configuring-windows-event-forwarding).

> [!NOTE]
> Für die ATA-Version 1.8 und höher ist die Konfiguration der Ereignissammlung nicht länger für ATA-Lightweight-Gateways erforderlich. Das ATA-Lightweight-Gateway kann jetzt Ereignisse lokal lesen, ohne die Ereignisweiterleitung zu konfigurieren.

Zusätzlich zum Sammeln und Analysieren des Netzwerkverkehrs zu und von den Domänencontrollern kann ATA Windows-Ereignisse heranziehen, um Erkennungen weiter zu verbessern. Es werden das Ereignis 4776 für die integrierte Windows-Authentifizierung verwendet, die unterschiedliche Erkennungen verbessert, sowie die Ereignisse 4732, 4733, 4728, 4729, 4756 und 4757 zur Verbesserung der Erkennung sensibler Gruppenänderungen. Dies kann aus SIEM heraus empfangen werden oder indem Sie die Windows-Ereignisweiterleitung von Ihrem Domänencontroller aus einrichten. Die gesammelten Ereignisse versorgen ATA mit zusätzlichen Informationen, die nicht über den Netzwerkverkehr des Domänencontrollers verfügbar sind.

#### SIEM/Syslog
<a id="siemsyslog" class="xliff"></a>
Damit ATA Daten aus einem Syslog-Server verwenden kann, müssen folgende Schritte ausgeführt werden:

-   Konfigurieren Ihres ATA-Gateway-Server zum Lauschen auf und Übernehmen von Ereignissen, die vom SIEM-/Syslog-Server weitergeleitet werden.
> [!NOTE]
> ATA lauscht nur auf IPv4, nicht auf IPv6. 
-   Konfigurieren des SIEM-/Syslog-Servers zum Weiterleiten bestimmter Ereignisse an das ATA-Gateway.

> [!IMPORTANT]
> -   Es sollten nicht alle Syslog-Daten an das ATA-Gateway weitergeleitet werden.
> -   ATA unterstützt UDP-Datenverkehr vom SIEM-/Syslog-Server.

Weitere Informationen über das Konfigurieren der Weiterleitung bestimmter Ereignisse an einen anderen Server finden Sie in der Produktdokumentation des SIEM-/Syslog-Servers. 

> [!NOTE]
>Wenn Sie keinen SIEM-/Syslog-Server verwenden, können Sie Ihre Windows-Domänencontroller zum Weiterleiten von Windows-Ereignis-ID 4776 konfigurieren, damit diese von ATA gesammelt und konfiguriert wird. Windows-Ereignis-ID 4776 enthält Daten über NTLM-Authentifizierungen.

#### Konfigurieren des ATA-Gateways zum Überwachen von SIEM-Ereignissen
<a id="configuring-the-ata-gateway-to-listen-for-siem-events" class="xliff"></a>

1.  Klicken Sie in der ATA-Konfiguration unter **Datenquellen** auf **SIEM**, aktivieren Sie **Syslog**, und klicken Sie auf **Speichern**.

    ![Aktivieren des Syslog-Listener-UDP-Images](media/ATA-enable-siem-forward-events.png)

2.  Konfigurieren Sie den SIEM-/Syslog-Server zum Weiterleiten von Windows-Ereignis-ID 4776 an die IP-Adresse von einem der ATA-Gateways. Weitere Informationen zum Konfigurieren der SIEM finden Sie in der SIEM-Onlinehilfe sowie in den Optionen für technischen Support für spezielle Formatierungserfordernisse einzelner SIEM-Server.

ATA unterstützt SIEM-Ereignisse in den folgenden Formaten:  

#### RSA Security Analytics
<a id="rsa-security-analytics" class="xliff"></a>
&lt;Syslog Header&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Der Syslog-Header ist optional.

-   Das Trennzeichen „\n“ ist zwischen allen Feldern erforderlich.

-   Die Felder sind der Reihenfolge nach:

    1.  RsaSA-Konstante (muss vorhanden sein).

    2.  Zeitstempel des tatsächlichen Ereignisses (darauf achten, dass dies nicht der Zeitstempel der Ankunft beim SIEM oder des Sendens an ATA ist). Vorzugsweise auf die Millisekunde genau, dies ist sehr wichtig.

    3.  Die Windows-Ereignis-ID

    4.  Der Name des Windows-Ereignisanbieters

    5.  Der Name des Windows-Ereignisprotokolls

    6.  Name des Computers, der das Ereignis empfängt (in diesem Fall der DC)

    7.  Name des authentifizierenden Benutzers

    8.  Name des Quellhostnamens

    9. Ergebniscode des NTLM

-   Die Reihenfolge ist wichtig, und es sollten keine weiteren Angaben in die Nachricht eingeschlossen werden.

#### HP Arcsight
<a id="hp-arcsight" class="xliff"></a>
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Der Domänencontroller hat versucht, die Anmeldeinformationen für ein Konto zu bestätigen.|Niedrig| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Grund oder Fehlercode

-   Muss der Protokolldefinition entsprechen.

-   Kein Syslog-Header.

-   Der Headerteil (der Teil, der durch einen senkrechten Strich abgetrennt ist) muss vorhanden sein (wie im Protokoll angegeben).

-   Die folgenden Schlüssel im Teil _Erweiterung_ müssen im Ereignis vorhanden sein:

    -   externalId = Windows-Ereignis-ID

    -   rt = Zeitstempel des tatsächlichen Ereignisses (darauf achten, dass dies nicht der Zeitstempel der Ankunft bei der SIEM oder des Sendens an uns ist). Vorzugsweise auf die Millisekunde genau, dies ist sehr wichtig.

    -   cat = Name des Windows-Ereignisprotokolls

    -   shost = Name des Quellhostnamens

    -   dhost = Name des Computers, der das Ereignis empfängt (in diesem Fall der DC)

    -   duser = Name des authentifizierenden Benutzers

-   Die Reihenfolge ist für den Teil _Erweiterung_ unerheblich

-   Für die folgenden beiden Felder müssen ein benutzerdefinierter Schlüssel und ein keyLabel vorhanden sein:

    -   „EventSource“

    -   „Ursache oder Fehlercode“ = Ergebniscode des NTLM

#### Splunk
<a id="splunk" class="xliff"></a>
&lt;Syslog Header&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

Es wurde versucht, die Anmeldeinformationen für ein Konto zu überprüfen.

Authentifizierungspaket: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Anmeldekonto: Administrator

Quellarbeitsstation:       SIEM

Fehlercode:         0x0

-   Der Syslog-Header ist optional.

-   Zwischen allen erforderlichen Feldern befindet sich das Trennzeichen „\r\n“.

-   Die Felder weisen das Format „Schlüssel = Wert“ auf.

-   Die folgenden Schlüssel müssen vorhanden sein und einen Wert haben:

    -   EventCode = Windows-Ereignis-ID

    -   Logfile = Name des Windows-Ereignisprotokolls

    -   SourceName = Name des Windows-Ereignisanbieters

    -   TimeGenerated = Zeitstempel des tatsächlichen Ereignisses (dies darf nicht der Zeitstempel der Ankunft bei der SIEM oder des Sendens an ATA sein). Das Format sollte „yyyyMMddHHmmss.FFFFFF“ sein, vorzugsweise mit einer Genauigkeit im Millisekundenbereich, dies ist sehr wichtig.

    -   ComputerName = Name des Quellhostnamens

    -   Message = ursprünglicher Ereignistext aus dem Windows-Ereignis

-   Der Schlüssel „Message“ und dessen Wert müssen als letzte Elemente auftreten.

-   Die Reihenfolge der „Schlüssel = Wert“-Paare ist unerheblich.

#### QRadar
<a id="qradar" class="xliff"></a>
QRadar ermöglicht Ereignissammlung über einen Agent. Wenn die Daten mithilfe eines Agents erfasst werden, werden Zeiten ohne Millisekunden-Daten erfasst. Da ATA Millisekunden-Daten erfordert, muss QRadar so festgelegt werden, dass es die Windows-Ereignissammlung ohne Agents verwendet. Weitere Informationen finden Sie unter [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Die erforderlichen Felder sind:

- Der Agenttyp für die Sammlung
- Der Anbietername für das Windows-Ereignisprotokoll
- Die Quelle für das Windows-Ereignisprotokoll
- Der vollqualifizierte Domänenname des DCs
- Die Windows-Ereignis-ID

„TimeGenerated“ ist der Zeitstempel des tatsächlichen Ereignisses (dies darf nicht der Zeitstempel der Ankunft bei der SIEM oder des Sendens an ATA sein). Das Format sollte „yyyyMMddHHmmss.FFFFFF“ sein, vorzugsweise mit einer Genauigkeit im Millisekundenbereich, dies ist sehr wichtig.

„Message“ ist der ursprüngliche Ereignistext aus dem Windows-Ereignis

Stellen Sie sicher, dass „\t“ zwischen Schlüssel=Wert-Paaren steht.

>[!NOTE] 
> Verwendung von WinCollect für die Windows-Ereignissammlung wird nicht unterstützt.


### Konfigurieren des VPN
<a id="configuring-vpn" class="xliff"></a>

ATA sammelt VPN-Daten, die bei der Profilerstellung der Orte helfen, von denen aus sich Computer mit dem Netzwerk verbinden.

Zum Konfigurieren von VPN-Daten, gehen Sie unter **Konfiguration** > **VPN**, und geben Sie das **gemeinsame Geheimnis Ihrer Radius-Kontoführung** Ihres VPN an.

![Konfigurieren des VPN](./media/vpn.png)

Um das gemeinsame Geheimnis zu erhalten, beziehen Sie sich auf die VPN-Dokumentation. Die unterstützten VPN-Lieferanten sind folgende:

- Microsoft
- F5
- Check Point
- Cisco ASA



>[!div class="step-by-step"]
[« Schritt 5](install-ata-step5.md)
[Schritt 7 »](install-ata-step7.md)


## Weitere Informationen
<a id="see-also" class="xliff"></a>

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)
