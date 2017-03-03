---
title: Konfigurieren der Ereignissammlung in Advanced Threat Analytics | Microsoft-Dokumentation
description: Beschreibt die Optionen zum Konfigurieren der Ereignissammlung mit ATA
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 6fddbbae0a0734834a21975c7690e06ac28dc64d
ms.openlocfilehash: e31e3b8a94c8beef22be2f06ecaeb89545b3f62d
ms.lasthandoff: 02/21/2017


---

*Gilt für: Advanced Threat Analytics Version 1.6 und 1.7*



# <a name="configure-event-collection"></a>Konfigurieren der Ereignissammlung
Um die Erkennungsfunktionalität zu verbessern, benötigt ATA die Windows-Ereignisprotokoll-ID 4776. Diese kann auf zwei Arten an das ATA-Gateway weitergeleitet werden: durch das Konfigurieren des ATA-Gateways zum Überwachen von SIEM-Ereignissen oder durch das [Konfigurieren der Windows-Ereignisweiterleitung](#configuring-windows-event-forwarding).

## <a name="event-collection"></a>Ereignissammlung
Zusätzlich zum Sammeln und Analysieren des Netzwerkverkehrs zu und von den Domänencontrollern kann ATA das Windows-Ereignis 4776 heranziehen, um die ATA-Erkennung von Pass-the-Hash weiter zu verbessern. Dies kann aus SIEM heraus empfangen werden oder indem Sie die Windows-Ereignisweiterleitung von Ihrem Domänencontroller aus einrichten. Die gesammelten Ereignisse versorgen ATA mit zusätzlichen Informationen, die nicht über den Netzwerkverkehr des Domänencontrollers verfügbar sind.

### <a name="siemsyslog"></a>SIEM/Syslog
Damit ATA Daten aus einem Syslog-Server verwenden kann, müssen folgende Schritte ausgeführt werden:

-   Konfigurieren Ihres ATA-Gateway-Server zum Lauschen auf und Übernehmen von Ereignissen, die vom SIEM-/Syslog-Server weitergeleitet werden.
> [!NOTE]
> ATA lauscht nur auf IPv4, nicht auf IPv6. 
-   Konfigurieren des SIEM-/Syslog-Servers zum Weiterleiten bestimmter Ereignisse an das ATA-Gateway.

> [!IMPORTANT]
> -   Es sollten nicht alle Syslog-Daten an das ATA-Gateway weitergeleitet werden.
> -   ATA unterstützt UDP-Datenverkehr vom SIEM-/Syslog-Server.

Weitere Informationen über das Konfigurieren der Weiterleitung bestimmter Ereignisse an einen anderen Server finden Sie in der Produktdokumentation des SIEM-/Syslog-Servers. 

### <a name="windows-event-forwarding"></a>Windows-Ereignisweiterleitung
Wenn Sie keinen SIEM-/Syslog-Server verwenden, können Sie Ihre Windows-Domänencontroller zum Weiterleiten von Windows-Ereignis-ID 4776 konfigurieren, damit diese von ATA gesammelt und konfiguriert wird. Windows-Ereignis-ID 4776 enthält Daten über NTLM-Authentifizierungen.

## <a name="configuring-the-ata-gateway-to-listen-for-siem-events"></a>Konfigurieren des ATA-Gateways zum Überwachen von SIEM-Ereignissen

1.  Aktivieren Sie in der ATA-Konsole unter „Ereignisse“ **Syslog** und drücken Sie auf **Speichern**.

    ![Aktivieren des Syslog-Listener-UDP-Images](media/ATA-enable-siem-forward-events.png)

2.  Konfigurieren Sie den SIEM-/Syslog-Server zum Weiterleiten von Windows-Ereignis-ID 4776 an die IP-Adresse von einem der ATA-Gateways. Weitere Informationen zum Konfigurieren der SIEM finden Sie in der SIEM-Onlinehilfe sowie in den Optionen für technischen Support für spezielle Formatierungserfordernisse einzelner SIEM-Server.

### <a name="siem-support"></a>SIEM-Unterstützung
ATA unterstützt SIEM-Ereignisse in den folgenden Formaten:  

#### <a name="rsa-security-analytics"></a>RSA Security Analytics
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

#### <a name="hp-arcsight"></a>HP Arcsight
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

#### <a name="splunk"></a>Splunk
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

#### <a name="qradar"></a>QRadar
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

## <a name="configuring-windows-event-forwarding"></a>Konfigurieren der Windows-Ereignisweiterleitung

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>Konfiguration der Windows-Ereignisweiterleitung für ATA-Gateways mit Portspiegelung

Nachdem Sie die Portspiegelung von den Domänencontrollern zum ATA-Gateway konfiguriert haben, befolgen Sie die unten aufgeführten Anweisungen, um die Windows-Ereignisweiterleitung (Windows Event Forwarding; WEF) mithilfe der quellinitiierten Konfiguration zu konfigurieren. Dies ist eine Möglichkeit, die Windows-Ereignisweiterleitung zu konfigurieren. 

**Schritt 1: Fügen Sie das Netzwerkdienstkonto zur Domäne „Ereignisprotokolllesergruppe“ hinzu.** 

In diesem Szenario gehen wir davon aus, dass der ATA-Gateway Mitglied einer Domäne ist.

1.    Öffnen Sie „Active Directory-Benutzer und -Computer“, navigieren Sie zum Ordner **Vordefiniert**, und doppelklicken Sie auf **Ereignisprotokollleser**. 
2.    Wählen Sie **Mitglieder** aus.
4.    Wenn **Netzwerkdienst** nicht aufgelistet ist, klicken Sie auf **Hinzufügen**, und geben Sie **Netzwerkdienst** in das Feld **Geben Sie die zu verwendenden Objektnamen ein** ein. Klicken Sie anschließend auf **Namen überprüfen**, und klicken Sie zweimal auf **OK**. 

Bitte beachten Sie, dass Sie die Domänencontroller neu starten müssen, nachdem Sie den **Netzwerkdienst** der **Ereignisprotokollleser**-Gruppe hinzugefügt haben, damit die Änderungen in Kraft treten können.

**Schritt 2: Erstellen Sie eine Richtlinie auf den Domänencontrollern, um die Einstellung „Ziel-Abonnement-Manager konfigurieren“ festzulegen.** 
> [!Note] 
> Sie können eine Gruppenrichtlinie für diese Einstellungen erstellen und die Gruppenrichtlinie auf jeden Domänencontroller anwenden, der vom ATA-Gateway überwacht wird. Die folgenden Schritte ändern die lokale Richtlinie des Domänencontrollers.     

1.    Führen Sie den folgenden Befehl auf jedem Domänencontroller aus: *winrm quickconfig*
2.  Geben Sie an einer Eingabeaufforderung *gpedit.msc* ein.
3.    Erweitern Sie **Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Ereignisweiterleitung**.

 ![Local policy group editor image](media/wef 1 local group policy editor.png)

4.    Doppelklicken Sie auf **Ziel-Abonnement-Manager konfigurieren**.
   
    1.    Wählen Sie **Aktiviert** aus.
    2.    Klicken Sie unter **Optionen** auf **Anzeigen**.
    3.    Geben Sie unter **SubscriptionManagers** den folgenden Wert ein, und klicken Sie auf **OK**: *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (z.B.: Server=http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
 
   ![Configure target subscription image](media/wef 2 config target sub manager.png)
   
    5.    Klicken Sie auf **OK**.
    6.    Geben Sie von einer Eingabeaufforderung mit erhöhten Rechten aus *gpupdate /force* ein. 

**Schritt 3: Führen Sie die folgenden Schritte auf dem ATA-Gateway aus.** 

1.    Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie *wecutil.qc* ein.
2.    Öffnen Sie die **Ereignisanzeige**. 
3.    Klicken Sie mit der rechten Maustaste auf **Abonnements** und wählen Sie **Erstellen von Abonnements** aus. 

   1.    Geben Sie einen Namen und eine Beschreibung für das Abonnement ein. 
   2.    Bestätigen Sie für **Zielprotokoll**, dass **Weitergeleitete Ereignisse** aktiviert ist. Damit ATA die Ereignisse lesen kann, muss das Zielprotokoll **Weitergeleitete Ereignisse** sein. 
   3.    Wählen Sie **Quellcomputerinitiiert** aus, und klicken Sie auf **Computergruppen auswählen** aus.
        1.    Klicken Sie auf **Domänencomputer hinzufügen**.
        2.    Geben Sie den Namen des Domänencontrollers in das Feld **Namen des auszuwählenden Objekts eingeben** ein. Klicken Sie anschließend auf **Namen überprüfen**, und klicken Sie auf **OK**. 
       
        ![Event Viewer image](media/wef3 event viewer.png)
   
        
        3.    Klicken Sie auf **OK**.
   4.    Klicken Sie auf **Ereignisse auswählen**.

        1. Klicken Sie auf **Per Protokoll** und wählen Sie **Sicherheit** aus.
        2. Tippen Sie im Feld **Ereignis-IDs ein-/ausschließen** **4776** ein, und klicken Sie auf **OK**. 

 ![Query filter image](media/wef 4 query filter.png)

   5.    Klicken Sie mit der mit der rechten Maustaste auf das erstellte Abonnement, und wählen Sie **Laufzeitstatus** aus, um festzustellen, ob es Probleme mit dem Status gibt. 
   6.    Überprüfen Sie nach einigen Minuten, ob das Ereignis 4776 im ATA-Gateway in „Weitergeleitete Ereignisse“ angezeigt wird.


### <a name="wef-configuration-for-the-ata-lightweight-gateway"></a>WEF-Konfiguration für das ATA-Lightweight-Gateway
Bei der Installation des ATA-Lightweight-Gateways auf Ihren Domänencontrollern können Sie Ihre Domänencontroller zum Weiterleiten der Ereignisse an sich selbst festlegen. Führen Sie die folgenden Schritte aus, um die Windows-Ereignisweiterleitung bei der Verwendung des ATA-Lightweight-Gateways zu konfigurieren. Dies ist eine Möglichkeit, die Windows-Ereignisweiterleitung zu konfigurieren.  

**Schritt 1: Fügen Sie das Netzwerkdienstkonto zur Domäne „Ereignisprotokolllesergruppe“ hinzu.** 

1.    Öffnen Sie „Active Directory-Benutzer und -Computer“, navigieren Sie zum Ordner **Vordefiniert**, und doppelklicken Sie auf **Ereignisprotokollleser**. 
2.    Wählen Sie **Mitglieder** aus.
3.    Wenn **Netzwerkdienst** nicht aufgelistet ist, klicken Sie auf **Hinzufügen**, und geben Sie **Netzwerkdienst** in das Feld **Geben Sie die zu verwendenden Objektnamen ein** ein. Klicken Sie anschließend auf **Namen überprüfen**, und klicken Sie zweimal auf **OK**. 

**Schritt 2: Führen Sie die folgenden Schritte auf dem Domänencontroller aus, nachdem der ATA-Lightweight-Gateway installiert wurde.** 

1.    Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie *winrm quickconfig* und *wecutil qc* ein. 
2.    Öffnen Sie die **Ereignisanzeige**. 
3.    Klicken Sie mit der rechten Maustaste auf **Abonnements** und wählen Sie **Erstellen von Abonnements** aus. 

   1.    Geben Sie einen Namen und eine Beschreibung für das Abonnement ein. 
   2.    Bestätigen Sie für **Zielprotokoll**, dass **Weitergeleitete Ereignisse** aktiviert ist. Damit ATA die Ereignisse lesen kann, muss das Zielprotokoll „Weitergeleitete Ereignisse“ sein.

        1.    Wählen Sie **Sammlungsinitiiert** aus, und klicken Sie auf **Computer auswählen**. Klicken Sie anschließend auf **Add Domain Computer** (Domänencomputer hinzufügen).
        2.    Geben Sie den Namen des Domänencontrollers in **Namen des auszuwählenden Objekts eingeben** ein. Klicken Sie anschließend auf **Namen überprüfen**, und klicken Sie auf **OK**.

            ![Subscription properties image](media/wef 5 sub properties computers.png)

        3.    Klicken Sie auf **OK**.
   3.    Klicken Sie auf **Ereignisse auswählen**.

        1.    Klicken Sie auf **Per Protokoll** und wählen Sie **Sicherheit** aus.
        2.    Tippen Sie **Includes/Excludes Event ID** (Ereignis-IDs ein-/ausschließen) *4776* ein, und klicken Sie auf **OK**. 

![Query filter image](media/wef 4 query filter.png)


  4.    Klicken Sie mit der mit der rechten Maustaste auf das erstellte Abonnement, und wählen Sie **Laufzeitstatus** aus, um festzustellen, ob es Probleme mit dem Status gibt. 

> [!Note] 
> Möglicherweise müssen Sie den Domänencontroller neu starten, bevor die Einstellung wirksam wird. 

Überprüfen Sie nach einigen Minuten, ob das Ereignis 4776 im ATA-Gateway in „Weitergeleitete Ereignisse“ angezeigt wird.



Weitere Informationen finden Sie unter [Einrichten von Computern zum Weiterleiten und Sammeln von Ereignissen](https://technet.microsoft.com/library/cc748890).

## <a name="see-also"></a>Weitere Informationen
- [Installieren von ATA](install-ata-step1.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

