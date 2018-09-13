---
title: Installieren von Azure Advanced Threat Protection | Microsoft-Dokumentation
description: In diesem Schritt bei der ATP-Installation konfigurieren Sie Datenquellen.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/15/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 91e3caf8e15313069e4c2cec194a11855fd45c24
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126177"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="configure-event-collection"></a>Konfigurieren der Ereignissammlung

Um die Erkennungsfunktionalität zu verbessern, benötigt Azure ATP die folgenden Windows-Ereignisse: 4776, 4732, 4733, 4728, 4729, 4756, 4757 und 7045. Diese können entweder automatisch vom Azure ATP-Sensor gelesen oder, falls dieser nicht bereitgestellt wurde, an den eigenständigen Azure ATP-Sensor weitergeleitet werden. Dazu gibt es zwei Möglichkeiten: die Konfiguration des eigenständigen Azure ATP-Sensors, sodass dieser auf SIEM-Ereignisse lauscht, oder die [Konfiguration der Windows-Ereignisweiterleitung](configure-event-forwarding.md).

> [!NOTE]
> Es ist wichtig, das ATA-Überwachungsskript vor der Konfiguration der Ereignissammlung auszuführen, um sicherzustellen, dass die Domänencontroller ordnungsgemäß für die Aufzeichnung der benötigten Ereignisse konfiguriert sind. 

Zusätzlich zum Sammeln und Analysieren des Netzwerkverkehrs zu und von den Domänencontrollern kann Azure ATP Windows-Ereignisse heranziehen, um Erkennungen weiter zu verbessern. Das Ereignis 4776 für NTLM wird verwendet, um verschiedene Erkennungen zu verbessern, und die Ereignisse 4732, 4733, 4728, 4729, 4756, 4757 und 7045 dienen zur Verbesserung der Erkennung sensibler Gruppenänderungen und zur Diensterstellung. Dies kann aus SIEM heraus empfangen werden oder indem Sie die Windows-Ereignisweiterleitung von Ihrem Domänencontroller aus einrichten. Die gesammelten Ereignisse versorgen Azure ATP mit zusätzlichen Informationen, die nicht über den Datenverkehr des Domänencontrollers verfügbar sind.

## <a name="siemsyslog"></a>SIEM/Syslog
Damit Azure ATP Daten von einem Syslog-Server verwenden kann, müssen folgende Schritte ausgeführt werden:

-   Konfigurieren Ihres Azure ATP-Sensors zum Lauschen auf und Übernehmen von Ereignissen, die vom SIEM-/Syslog-Server weitergeleitet werden.

 > [!NOTE]
 > Azure ATP lauscht nur auf IPv4, nicht auf IPv6. 

-   Konfigurieren des SIEM-/Syslog-Servers zum Weiterleiten bestimmter Ereignisse an den Azure ATP-Sensor.

> [!IMPORTANT]
> -   Es sollten nicht alle Syslog-Daten an den Azure ATP-Sensor weitergeleitet werden.
> -   Azure ATP unterstützt UDP-Datenverkehr vom SIEM-/Syslog-Server.

Weitere Informationen über das Konfigurieren der Weiterleitung bestimmter Ereignisse an einen anderen Server finden Sie in der Produktdokumentation des SIEM-/Syslog-Servers. 

> [!NOTE]
>Wenn Sie keinen SIEM-/Syslog-Server verwenden, können Sie Ihre Windows-Domänencontroller zum Weiterleiten von allen erforderlichen Ereignissen konfigurieren, damit diese von ATP gesammelt und konfiguriert wird.

## <a name="configuring-the-azure-atp-sensor-to-listen-for-siem-events"></a>Konfigurieren des Azure ATP-Sensors zum Lauschen auf SIEM-Ereignisse

1.  Klicken Sie in der Azure ATP-Konfiguration unter **Datenquellen** auf **SIEM**, aktivieren Sie **Syslog**, und klicken Sie auf **Speichern**.

    ![Aktivieren des Syslog-Listener-UDP-Images](media/atp-siem-config.png)

2.  Konfigurieren Sie den SIEM-/Syslog-Server zum Weiterleiten aller erforderlichen Ereignisse an die IP-Adresse von einer der Azure ATP-Sensoren. Weitere Informationen zum Konfigurieren der SIEM finden Sie in der SIEM-Onlinehilfe sowie in den Optionen für technischen Support für spezielle Formatierungsanforderungen einzelner SIEM-Server.

Azure ATP unterstützt SIEM-Ereignisse in den folgenden Formaten:  

## <a name="rsa-security-analytics"></a>RSA Security Analytics
&lt;Syslog Header&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Der Syslog-Header ist optional.

-   Das Trennzeichen „\n“ ist zwischen allen Feldern erforderlich.

-   Die Felder sind der Reihenfolge nach:

    1.  RsaSA-Konstante (muss vorhanden sein).

    2.  Zeitstempel des tatsächlichen Ereignisses (darauf achten, dass dies nicht der Zeitstempel der Ankunft beim SIEM oder des Sendens an ATP ist). Vorzugsweise auf die Millisekunde genau, dies ist wichtig.

    3.  Die Windows-Ereignis-ID

    4.  Der Name des Windows-Ereignisanbieters

    5.  Der Name des Windows-Ereignisprotokolls

    6.  Name des Computers, der das Ereignis empfängt (in diesem Fall der DC)

    7.  Name des authentifizierenden Benutzers

    8.  Name des Quellhostnamens

    9. Ergebniscode des NTLM

-   Die Reihenfolge ist wichtig, und es sollten keine weiteren Angaben in die Nachricht eingeschlossen werden.

## <a name="hp-arcsight"></a>HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Der Domänencontroller hat versucht, die Anmeldeinformationen für ein Konto zu bestätigen.|Niedrig| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Grund oder Fehlercode

-   Muss der Protokolldefinition entsprechen.

-   Kein Syslog-Header.

-   Der Headerteil (der Teil, der durch einen senkrechten Strich abgetrennt ist) muss vorhanden sein (wie im Protokoll angegeben).

-   Die folgenden Schlüssel im Teil _Erweiterung_ müssen im Ereignis vorhanden sein:

    -   externalId = Windows-Ereignis-ID

    -   rt= Zeitstempel des tatsächlichen Ereignisses (darauf achten, dass dies nicht der Zeitstempel der Ankunft beim SIEM oder des Sendens an ATP ist). Vorzugsweise auf die Millisekunde genau, dies ist wichtig.

    -   cat = Name des Windows-Ereignisprotokolls

    -   shost = Name des Quellhostnamens

    -   dhost = Name des Computers, der das Ereignis empfängt (in diesem Fall der DC)

    -   duser = Name des authentifizierenden Benutzers

-   Die Reihenfolge ist für den Teil _Erweiterung_ unerheblich

-   Für die folgenden beiden Felder müssen ein benutzerdefinierter Schlüssel und ein keyLabel vorhanden sein:

    -   „EventSource“

    -   „Ursache oder Fehlercode“ = Ergebniscode des NTLM

## <a name="splunk"></a>Splunk
&lt;Syslog Header&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

Es wurde versucht, die Anmeldeinformationen für ein Konto zu überprüfen.

Authentifizierungspaket: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Anmeldekonto: Administrator

Quellarbeitsstation:       SIEM

Fehlercode:         0x0

-   Der Syslog-Header ist optional.

-   Zwischen allen erforderlichen Feldern befindet sich das Trennzeichen „\r\n“.

-   Die Felder weisen das Format „Schlüssel = Wert“ auf.

-   Die folgenden Schlüssel müssen vorhanden sein und einen Wert aufweisen:

    -   EventCode = Windows-Ereignis-ID

    -   Logfile = Name des Windows-Ereignisprotokolls

    -   SourceName = Name des Windows-Ereignisanbieters

    -   TimeGenerated = Zeitstempel des tatsächlichen Ereignisses (dies darf nicht der Zeitstempel der Ankunft bei der SIEM oder des Sendens an ATP sein). Als Format muss „yyyyMMddHHmmss.FFFFFF“ verwendet werden, vorzugsweise mit einer Genauigkeit im Millisekundenbereich, dies ist wichtig.

    -   ComputerName = Name des Quellhostnamens

    -   Message = ursprünglicher Ereignistext aus dem Windows-Ereignis

-   Der Schlüssel „Message“ und dessen Wert müssen als letzte Elemente auftreten.

-   Die Reihenfolge der „Schlüssel = Wert“-Paare ist unerheblich.

## <a name="qradar"></a>QRadar
QRadar ermöglicht Ereignissammlung über einen Agent. Wenn die Daten mithilfe eines Agents erfasst werden, werden Zeiten ohne Millisekunden-Daten erfasst. Da Azure ATP Millisekunden-Daten erfordert, muss QRadar so festgelegt werden, dass es die Windows-Ereignissammlung ohne Agents verwendet. Weitere Informationen finden Sie unter [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol (QRadar: Auflistung von Windows-Ereignissen ohne Agent mithilfe des MSRPC-Protokolls)").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Die erforderlichen Felder sind:

- Der Agenttyp für die Sammlung
- Der Anbietername für das Windows-Ereignisprotokoll
- Die Quelle für das Windows-Ereignisprotokoll
- Der vollqualifizierte Domänenname des DCs
- Die Windows-Ereignis-ID

„TimeGenerated“ ist der Zeitstempel des tatsächlichen Ereignisses (dies darf nicht der Zeitstempel der Ankunft bei der SIEM oder des Sendens an ATP sein). Als Format muss „yyyyMMddHHmmss.FFFFFF“ verwendet werden, vorzugsweise mit einer Genauigkeit im Millisekundenbereich, dies ist wichtig.

„Message“ ist der ursprüngliche Ereignistext aus dem Windows-Ereignis

Stellen Sie sicher, dass „\t“ zwischen Schlüssel=Wert-Paaren steht.

>[!NOTE] 
> Verwendung von WinCollect für die Windows-Ereignissammlung wird nicht unterstützt.




## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Referenz zum Azure ATP-SIEM-Protokoll](cef-format-sa.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
