---
title: Installieren von Microsoft Defender for Identity
description: In diesem Schritt der Microsoft Defender for Identity-Installation konfigurieren Sie Datenquellen.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7624f2d959e37b2bf88d4b14c31c5a6f1ddd6853
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848226"
---
# <a name="configure-event-collection"></a>Konfigurieren der Ereignissammlung

Zur Erweiterung der Erkennungsfunktionen benötigt [!INCLUDE [Product long](includes/product-long.md)] die Windows-Ereignisse, die unter [Konfigurieren der Ereignissammlung](configure-windows-event-collection.md#configure-event-collection) aufgeführt sind. Diese Ereignisse können entweder automatisch vom [!INCLUDE [Product short](includes/product-short.md)]-Sensor gelesen oder – falls dieser nicht bereitgestellt wurde – an den eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor weitergeleitet werden. Dazu gibt es zwei Möglichkeiten: die Konfiguration des eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensors, sodass dieser auf SIEM-Ereignisse lauscht, oder die [Konfiguration der Windows-Ereignisweiterleitung](configure-event-forwarding.md).

> [!NOTE]
>
> - Eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensoren unterstützen keine Erfassung von Protokolleinträgen für die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die Daten für mehrere Erkennungen bereitstellen. Zur vollständigen Erfassung Ihrer Umgebung empfiehlt sich die Bereitstellung des [!INCLUDE [Product short](includes/product-short.md)]-Sensors.
> - Es ist wichtig, vor der Konfiguration der Ereignissammlung das [!INCLUDE [Product short](includes/product-short.md)]-Überwachungsskript auszuführen, um sicherzustellen, dass die Domänencontroller ordnungsgemäß für die Aufzeichnung der benötigten Ereignisse konfiguriert sind.

Zusätzlich zum Erfassen und Analysieren des Netzwerkverkehrs zu und von den Domänencontrollern kann [!INCLUDE [Product short](includes/product-short.md)]Windows-Ereignisse heranziehen, um Erkennungen zu erweitern. Diese Ereignisse können von SIEM erhalten oder durch Festlegen der Windows-Ereignisweiterleitung von Ihrem Domänencontroller aus abgerufen werden. Die erfassten Ereignisse bieten [!INCLUDE [Product short](includes/product-short.md)] zusätzliche Informationen, die über den Netzwerkverkehr des Domänencontrollers nicht verfügbar sind.

## <a name="ntlm-authentication-using-windows-event-8004"></a>NTLM-Authentifizierung mithilfe des Windows-Ereignisses 8004

So konfigurieren Sie die Windows-Ereignis 8004-Sammlung:

1. Navigieren Sie zu: *Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Sicherheitsoptionen*
1. Legen Sie die **Domänengruppenrichtlinie** wie folgt fest:
    - Netzwerksicherheit: Beschränken von NTLM: Ausgehender NTLM-Datenverkehr zu Remoteservern = **Alle überwachen**
    - Netzwerksicherheit: Beschränken von NTLM: NTLM-Authentifizierung in dieser Domäne überwachen = **Alle aktivieren**
    - Netzwerksicherheit: Beschränken von NTLM: Eingehenden NTLM-Datenverkehr überwachen = **Überwachung für alle Konten aktivieren**

Bei der Analyse des Windows-Ereignisses 8004 durch den [!INCLUDE [Product short](includes/product-short.md)]-Sensor werden [!INCLUDE [Product short](includes/product-short.md)]-NTLM-Authentifizierungsaktivitäten durch die Daten ergänzt, auf die auf dem Server zugegriffen wird.

## <a name="siemsyslog"></a>SIEM/Syslog

Eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensoren sind standardmäßig für den Empfang von Syslog-Daten konfiguriert. Damit eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensoren diese Daten nutzen können, müssen Sie die Syslog-Daten an diese Sensoren weiterleiten.

> [!NOTE]
> [!INCLUDE [Product short](includes/product-short.md)] lauscht nur auf IPv4, nicht auf IPv6.

> [!IMPORTANT]
>
> - Leiten Sie nicht alle Syslog-Daten an den [!INCLUDE [Product short](includes/product-short.md)]-Sensor weiter.
> - [!INCLUDE [Product short](includes/product-short.md)] unterstützt UDP-Datenverkehr vom SIEM-/Syslog-Server.

Weitere Informationen über das Konfigurieren der Weiterleitung bestimmter Ereignisse an einen anderen Server finden Sie in der Produktdokumentation des SIEM-/Syslog-Servers.

> [!NOTE]
> Wenn Sie keinen SIEM-/Syslog-Server verwenden, können Sie Ihre Windows-Domänencontroller zum Weiterleiten von allen erforderlichen Ereignissen konfigurieren, damit diese von [!INCLUDE [Product short](includes/product-short.md)] erfasst und analysiert werden.

## <a name="configuring-the-product-short-sensor-to-listen-for-siem-events"></a>Konfigurieren des [!INCLUDE [Product short](includes/product-short.md)]-Sensors zum Lauschen auf SIEM-Ereignisse

- Konfigurieren Sie den SIEM-/Syslog-Server zum Weiterleiten aller erforderlichen Ereignisse an die IP-Adresse eines eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensors. Weitere Informationen zum Konfigurieren der SIEM finden Sie in der SIEM-Onlinehilfe sowie in den Optionen für technischen Support für spezielle Formatierungsanforderungen einzelner SIEM-Server.

[!INCLUDE [Product short](includes/product-short.md)] unterstützt SIEM-Ereignisse in den folgenden Formaten:

### <a name="rsa-security-analytics"></a>RSA Security Analytics

&lt;Syslog Header&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

- Der Syslog-Header ist optional.

- Das Trennzeichen „\n“ ist zwischen allen Feldern erforderlich.
- Die Felder sind der Reihenfolge nach:
    1. RsaSA-Konstante (muss vorhanden sein).
    2. Der Zeitstempel des tatsächlichen Ereignisses (dies darf nicht der Zeitstempel des Eingangs beim SIEM-System oder des Sendens an [!INCLUDE [Product short](includes/product-short.md)] sein). Vorzugsweise auf die Millisekunde genau, dies ist wichtig.
    3. Die Windows-Ereignis-ID
    4. Der Name des Windows-Ereignisanbieters
    5. Der Name des Windows-Ereignisprotokolls
    6. Name des Computers, der das Ereignis empfängt (in diesem Fall der DC)
    7. Name des authentifizierenden Benutzers
    8. Name des Quellhostnamens
    9. Ergebniscode des NTLM
- Die Reihenfolge ist wichtig, und es sollten keine weiteren Angaben in die Nachricht eingeschlossen werden.

### <a name="microfocus-arcsight"></a>MicroFocus ArcSight

CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Der Domänencontroller hat versucht, die Anmeldeinformationen für ein Konto zu bestätigen.|Niedrig| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Grund oder Fehlercode

- Muss der Protokolldefinition entsprechen.

- Kein Syslog-Header.
- Der Headerteil (der Teil, der durch einen senkrechten Strich abgetrennt ist) muss vorhanden sein (wie im Protokoll angegeben).
- Die folgenden Schlüssel im Teil _Erweiterung_ müssen im Ereignis vorhanden sein:
  - externalId = Windows-Ereignis-ID
  - rt = Zeitstempel des tatsächlichen Ereignisses (dies darf nicht der Zeitstempel des Eingangs beim SIEM-System oder des Sendens an [!INCLUDE [Product short](includes/product-short.md)] sein). Vorzugsweise auf die Millisekunde genau, dies ist wichtig.
  - cat = Name des Windows-Ereignisprotokolls
  - shost = Name des Quellhostnamens
  - dhost = Name des Computers, der das Ereignis empfängt (in diesem Fall der DC)
  - duser = Name des authentifizierenden Benutzers
- Die Reihenfolge ist für den Teil _Erweiterung_ unerheblich
- Für die folgenden beiden Felder müssen ein benutzerdefinierter Schlüssel und ein keyLabel vorhanden sein:
  - „EventSource“
  - „Ursache oder Fehlercode“ = Ergebniscode des NTLM

### <a name="splunk"></a>Splunk

&lt;Syslog Header&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

Es wurde versucht, die Anmeldeinformationen für ein Konto zu überprüfen.

Authentifizierungspaket: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Anmeldekonto: Administrator

Quellarbeitsstation: SIEM

Fehlercode: 0x0

- Der Syslog-Header ist optional.

- Zwischen allen erforderlichen Feldern befindet sich das Trennzeichen „\r\n“. Beachten Sie, dass dies Steuerzeichen für den Zeilenumbruch (CRLF bzw. „0D0A“ in Hexadezimalnotation) und keine Literalzeichen sind.
- Die Felder weisen das Format „Schlüssel = Wert“ auf.
- Die folgenden Schlüssel müssen vorhanden sein und einen Wert aufweisen:
  - EventCode = Windows-Ereignis-ID
  - Logfile = Name des Windows-Ereignisprotokolls
  - SourceName = Name des Windows-Ereignisanbieters
  - TimeGenerated = der Zeitstempel des tatsächlichen Ereignisses (dies darf nicht der Zeitstempel des Eingangs beim SIEM-System oder des Sendens an [!INCLUDE [Product short](includes/product-short.md)] sein). Als Format muss „yyyyMMddHHmmss.FFFFFF“ verwendet werden, vorzugsweise mit einer Genauigkeit im Millisekundenbereich, dies ist wichtig.
  - ComputerName = Name des Quellhostnamens
  - Message = ursprünglicher Ereignistext aus dem Windows-Ereignis
- Der Schlüssel „Message“ und dessen Wert müssen als letzte Elemente auftreten.
- Die Reihenfolge der „Schlüssel = Wert“-Paare ist unerheblich.

### <a name="qradar"></a>QRadar

QRadar ermöglicht Ereignissammlung über einen Agent. Wenn die Daten mithilfe eines Agents erfasst werden, werden Zeiten ohne Millisekunden-Daten erfasst. Da [!INCLUDE [Product short](includes/product-short.md)] Millisekunden-Daten erfordert, muss QRadar auf die Verwendung der Windows-Ereignissammlung ohne Agents festgelegt werden. Weitere Informationen finden Sie unter [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol (QRadar: Auflistung von Windows-Ereignissen ohne Agent mithilfe des MSRPC-Protokolls)").

```text
<13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0
```

Die erforderlichen Felder sind:

- Der Agenttyp für die Sammlung

- Der Anbietername für das Windows-Ereignisprotokoll
- Die Quelle für das Windows-Ereignisprotokoll
- Der vollqualifizierte Domänenname des DCs
- Die Windows-Ereignis-ID

TimeGenerated ist der Zeitstempel des tatsächlichen Ereignisses (dies darf nicht der Zeitstempel des Eingangs beim SIEM-System oder des Sendens an [!INCLUDE [Product short](includes/product-short.md)] sein). Als Format muss „yyyyMMddHHmmss.FFFFFF“ verwendet werden, vorzugsweise mit einer Genauigkeit im Millisekundenbereich, dies ist wichtig.

„Message“ ist der ursprüngliche Ereignistext aus dem Windows-Ereignis

Stellen Sie sicher, dass „\t“ zwischen Schlüssel=Wert-Paaren steht.

>[!NOTE]
> Verwendung von WinCollect für die Windows-Ereignissammlung wird nicht unterstützt.

## <a name="see-also"></a>Weitere Informationen

- [[!INCLUDE [Product short](includes/product-short.md)]-Tool zur Größenanpassung](https://aka.ms/aatpsizingtool)
- [Referenz zum SIEM-Protokoll für [!INCLUDE [Product short](includes/product-short.md)]](cef-format-sa.md)
- [Voraussetzungen für [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
