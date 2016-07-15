---
title: Konfigurieren der Ereignissammlung | Microsoft Advanced Threat Analytics
description: Beschreibt die Optionen zum Konfigurieren der Ereignissammlung mit ATA
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: 17f30cbe478a868f3b6887bf48d8084934624191


---

# Konfigurieren der Ereignissammlung
Um die Erkennungsfunktionalität zu verbessern, benötigt ATA die Windows-Ereignisprotokoll-ID 4776. Diese kann auf zwei Arten an das ATA-Gateway weitergeleitet werden: durch das Konfigurieren des ATA-Gateways zum Überwachen von SIEM-Ereignissen oder durch das [Konfigurieren der Windows-Ereignisweiterleitung](#configuring-windows-event-forwarding).

## Ereignissammlung
Zusätzlich zum Sammeln und Analysieren des Netzwerkverkehrs zu und von den Domänencontrollern kann ATA das Windows-Ereignis 4776 heranziehen, um die ATA-Erkennung von Pass-the-Hash weiter zu verbessern. Dies kann aus der SIEM heraus erfolgen oder indem Sie die Windows-Ereignisweiterleitung von Ihrem Domänencontroller aus einrichten. Die gesammelten Ereignisse versorgen ATA mit zusätzlichen Informationen, die nicht über den Netzwerkverkehr des Domänencontrollers verfügbar sind.

### SIEM/Syslog
Damit ATA Daten aus einem Syslog-Server verwenden kann, müssen folgende Schritte ausgeführt werden:

-   Konfigurieren von einem der ATA-Gateway-Server zum Lauschen auf und Übernehmen von Ereignissen, die vom SIEM-/Syslog-Server weitergeleitet werden.

-   Konfigurieren des SIEM-/Syslog-Servers zum Weiterleiten bestimmter Ereignisse an das ATA-Gateway.

> [!IMPORTANT]
> -   Es sollten nicht alle Syslog-Daten an das ATA-Gateway weitergeleitet werden.
> -   ATA unterstützt UDP-Datenverkehr vom SIEM-/Syslog-Server.

Weitere Informationen über das Konfigurieren der Weiterleitung bestimmter Ereignisse an einen anderen Server finden Sie in der Produktdokumentation des SIEM-/Syslog-Servers. 

### Windows-Ereignisweiterleitung
Wenn Sie keinen SIEM-/Syslog-Server verwenden, können Sie Ihre Windows-Domänencontroller zum Weiterleiten von Windows-Ereignis-ID 4776 konfigurieren, damit diese von ATA gesammelt und konfiguriert wird. Windows-Ereignis-ID 4776 enthält Daten über NTLM-Authentifizierungen.

## Konfigurieren des ATA-Gateways zum Abhören von SIEM-Ereignissen

1.  Aktivieren Sie in der ATA-Gateway-Konfiguration **Syslog Listener UDP**.

    Legen Sie die Abhör-IP-Adresse wie in der untenstehenden Abbildung gezeigt fest. Der Standardport lautet 514.

    ![Aktivieren des Syslog-Listener-UDP-Images](media/ATA-enable-siem-forward-events.png)

2.  Konfigurieren Sie den SIEM-/Syslog-Server zum Weiterleiten von Windows-Ereignis-ID 4776 an die oben ausgewählte IP-Adresse. Weitere Informationen zum Konfigurieren der SIEM finden Sie in der SIEM-Onlinehilfe sowie in den Optionen für technischen Support für spezielle Formatierungserfordernisse einzelner SIEM-Server.

### SIEM-Unterstützung
ATA unterstützt SIEM-Ereignisse in den folgenden Formaten:

#### RSA Security Analytics
&lt;Syslog Header&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Der Syslog-Header ist optional.

-   Das Trennzeichen „\n“ ist zwischen allen Feldern erforderlich.

-   Die Felder sind der Reihenfolge nach:

    1.  RsaSA-Konstante (muss vorhanden sein).

    2.  Zeitstempel des tatsächlichen Ereignisses (darauf achten, dass dies nicht der Zeitstempel der Ankunft beim SIEM oder des Sendens an ATA ist). Vorzugsweise auf die Millisekunde genau, dies ist sehr wichtig.

    3.  Windows-Ereignis-ID

    4.  Name des Windows-Ereignisanbieters

    5.  Name des Windows-Ereignisprotokolls

    6.  Name des Computers, der das Ereignis empfängt (in diesem Fall der DC)

    7.  Name des authentifizierenden Benutzers

    8.  Name des Quellhostnamens

    9. Ergebniscode des NTLM

-   Die Reihenfolge ist wichtig, und es sollten keine weiteren Angaben in die Nachricht eingeschlossen werden.

#### HP Arcsight
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
QRadar ermöglicht Ereignissammlung über einen Agent. Wenn die Daten mithilfe eines Agents erfasst werden, werden Zeiten ohne Millisekunden-Daten erfasst. Da ATA Millisekunden-Daten erfordert, muss QRadar so festgelegt werden, dass es die Windows-Ereignissammlung ohne Agents verwendet. Weitere Informationen finden Sie unter [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Die erforderlichen Felder sind:

- Der Agenttyp für die Sammlung
- Der Anbietername für das Windows-Ereignisprotokoll
- Die Quelle für das Windows-Ereignisprotokoll
- Der vollqualifizierte Domänenname des DCs
- Windows-Ereignis-ID

„TimeGenerated“ ist der Zeitstempel des tatsächlichen Ereignisses (dies darf nicht der Zeitstempel der Ankunft bei der SIEM oder des Sendens an ATA sein). Das Format sollte „yyyyMMddHHmmss.FFFFFF“ sein, vorzugsweise mit einer Genauigkeit im Millisekundenbereich, dies ist sehr wichtig.

„Message“ ist der ursprüngliche Ereignistext aus dem Windows-Ereignis

Stellen Sie sicher, dass „\t“ zwischen Schlüssel=Wert-Paaren steht.

>[!NOTE] 
> Verwendung von WinCollect für die Windows-Ereignissammlung wird nicht unterstützt.

## Konfigurieren der Windows-Ereignisweiterleitung
Wenn Sie nicht über einen SIEM-Server verfügen, können Sie Ihre Domänencontroller zum Weiterleiten von Windows-Ereignis-ID 4776 direkt auf einen der ATA-Gateways konfigurieren.

1.  Melden Sie sich bei allen Domänencontrollern und ATA-Gateway-Computer mit einem Domänenkonto mit Administratorrechten an.
2. Stellen Sie sicher, dass die Domänencontroller und ATA-Gateways, mit denen Sie eine Verbindung herstellen, der gleichen Domäne angehören.
3.  Geben Sie auf jedem Domänencontroller Folgendes in einem Eingabeaufforderungsfenster mit erhöhten Rechten ein:
```
winrm quickconfig
```
4.  Geben Sie auf dem ATA-Gateway an einer Eingabeaufforderung mit erhöhten Rechten den folgenden Befehl ein:
```
wecutil qc
```
5.  Navigieren Sie auf jedem Domänencontroller in **Active Directory-Benutzer und -Computer** zum Ordner **Vordefiniert**, und doppelklicken Sie auf die Gruppe **Ereignisprotokollleser**.<br>
![wef_ad_eventlogreaders](media/wef_ad_eventlogreaders.png)<br>
Klicken Sie mit der rechten Maustaste darauf, und wählen Sie **Eigenschaften** aus. Fügen Sie auf der Registerkarte **Mitglieder** die Computerkonten der einzelnen ATA-Gateways hinzu.
![wef_ad event log reader popup](media/wef_ad-event-log-reader-popup.png)
6.  Öffnen Sie auf dem ATA-Gateway die Ereignisanzeige, klicken Sie mit der rechten Maustaste auf **Abonnements**, und wählen Sie **Abonnement erstellen** aus.  

    a. Klicken Sie unter **Abonnementtyp und Quellcomputer** auf **Computer auswählen**, fügen Sie die Domänencontroller hinzu, und testen Sie die Konnektivität.
    ![wef_subscription prop](media/wef_subscription-prop.png)

    b. Klicken Sie unter **Zu sammelnde Ereignisse** auf **Ereignisse auswählen**. Wählen Sie **Nach Protokoll** aus, und scrollen Sie abwärts bis zu **Sicherheit**. Geben Sie dann unter **Ereignis-IDs ein-/ausschließen** die Zahl **4776** ein.<br>
    ![wef_4776](media/wef_4776.png)

    c. Klicken Sie unter **Benutzerkonto ändern oder erweiterte Einstellungen konfigurieren** auf **Erweitert**.
Legen Sie für das **Protokoll** **HTTP** und für **Port** **5985** fest.<br>
    ![wef_http](media/wef_http.png)

7.  [Optional:] Falls ein kürzeres Abfrageintervall gewünscht wird, legen Sie auf dem ATA-Gateway den Abonnementpuls auf 5 Sekunden fest.
    wecutil ss <CollectionName>/cm:custom wecutil ss <CollectionName> /hi:5000

8. Aktivieren Sie auf der Konfigurationsseite des ATA-Gateways die Option **Windows-Ereignisweiterleitungssammlung**.

> [!NOTE]
> Wenn Sie diese Einstellung aktivieren, sucht das ATA-Gateway im Protokoll für weitergeleitete Ereignisse nach Windows-Ereignissen, die von den Domänencontrollern an das Gateway weitergeleitet wurden.

Weitere Informationen finden Sie unter [Einrichten von Computern zum Weiterleiten und Sammeln von Ereignissen](https://technet.microsoft.com/library/cc748890).

## Siehe auch
- [Installieren von ATA](install-ata.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=Jun16_HO4-->


