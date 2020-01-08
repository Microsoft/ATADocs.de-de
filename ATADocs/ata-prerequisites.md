---
title: Advanced Threat Analytics-Voraussetzungen | Microsoft-Dokumentation
description: Beschreibt die Voraussetzungen für eine erfolgreiche Bereitstellung von ATA in Ihrer Umgebung.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e84bbb84859d316d4900d0f09e71142627df1ae8
ms.sourcegitcommit: 0f3ee3241895359d5cecd845827cfba1fdca9317
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/29/2019
ms.locfileid: "75543169"
---
# <a name="ata-prerequisites"></a>Voraussetzungen für ATA

*Gilt für: Advanced Threat Analytics Version 1.9*

In diesem Artikel werden die Voraussetzungen für eine erfolgreiche Bereitstellung von ATA in Ihrer Umgebung beschrieben.

> [!NOTE]
> Informationen zum Planen von Ressourcen und Kapazitäten finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).


ATA besteht aus ATA Center, dem ATA-Gateway und/oder dem ATA-Lightweight-Gateway. Weitere Informationen zu ATA-Komponenten finden Sie unter [ATA-Architektur](ata-architecture.md).

Das ATA-System arbeitet auf der Gesamtstrukturbegrenzung von Active Directory und unterstützt die Gesamtstruktur-Funktionsebene (Forest Functional Level; FFL) von Windows 2003 und höher.


Vorbereitungen: in diesem Abschnitt werden die Informationen aufgelistet, die [Sie vor dem](#before-you-start)Starten der ATA-Installation sammeln sollten, sowie die Konten und Netzwerk Einheiten.

[ATA Center](#ata-center-requirements): in diesem Abschnitt werden die Hardware-und Softwareanforderungen von ATA Center sowie die Einstellungen aufgelistet, die Sie auf dem ATA Center-Server konfigurieren müssen.

[ATA-Gateway:](#ata-gateway-requirements) In diesem Abschnitt werden die Hardware- und Softwarevoraussetzungen für das ATA-Gateway sowie die Einstellungen aufgeführt, die Sie für die ATA-Gatewayserver konfigurieren müssen.

[ATA-Lightweight-Gateway:](#ata-lightweight-gateway-requirements) In diesem Abschnitt sind die Hardware- und Softwareanforderungen für das ATA-Lightweight-Gateway aufgeführt.

[ATA-Konsole](#ata-console): In diesem Abschnitt werden die Browseranforderungen für die Ausführung der ATA-Konsole aufgeführt.

![ATA-Architekturdiagramm](media/ATA-architecture-topology.jpg)

## <a name="before-you-start"></a>Bevor Sie beginnen
In diesem Abschnitt werden die Informationen aufgeführt, die Sie sammeln sollten, und Konten und Netzwerkentitäten genannt, die vor der ATA-Installation vorhanden sein sollten.


-   Benutzerkonto und -kennwort mit Lesezugriff auf alle Objekte in den überwachten Domänen.

    > [!NOTE]
    > Wenn Sie benutzerdefinierte ACLs für verschiedene Organisationseinheiten (OU) in Ihrer Domäne festgelegt haben, stellen Sie sicher, dass der ausgewählte Benutzer Leseberechtigungen für diese Organisationseinheiten hat.

-   Installieren Sie Microsoft Message Analyzer nicht auf einem ATA-Gateway oder einem Lightweight-Gateway. Der Treiber von Message Analyzer steht mit dem Treiber des ATA-Gateways und des Lightweight-Gateways in Konflikt. Wenn Sie Wireshark auf einem ATA-Gateway ausführen, müssen Sie den Dienst Microsoft Advanced Threat Analytics Gateway neu starten, nachdem Sie das Erfassen mit Wireshark abgeschlossen haben. Wenn dies nicht der Fall ist, beendet das Gateway die Erfassung von Datenverkehr. Das Ausführen von Wireshark auf einem ATA-Lightweight-Gateway besitzt keine Auswirkungen auf das ATA-Lightweight-Gateway.

-    Empfohlen: Benutzer sollten über schreibgeschützten Zugriff auf den Container mit gelöschten Objekten verfügen. So kann ATA eine Massenlöschung von Objekten in der Domäne erkennen. Informationen zum Konfigurieren des schreibgeschützten Zugriffs auf den Container mit gelöschten Objekten finden Sie im Abschnitt **Changing permissions on a deleted object container** (Ändern von Berechtigungen für einen Container mit gelöschten Objekten) im Artikel [View or Set Permissions on a Directory Object](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) (Anzeigen und Festlegen von Berechtigungen für ein Verzeichnisobjekt).

-   Optional: ein Benutzerkonto eines Benutzers ohne Netzwerkaktivitäten. Dieses Konto kann als ATA-Honeytoken-Benutzer konfiguriert werden. Zum Konfigurieren eines Kontos als Honeytoken-Benutzer ist nur der Benutzername erforderlich. Weitere Informationen zum Konfigurieren von Honeytoken finden Sie unter [Konfigurieren von IP-Adressausschlüssen und Honeytoken-Benutzern](install-ata-step7.md).

-   Optional: Zusätzlich zum Sammeln und Analysieren des Netzwerkverkehrs zu und von den Domänencontrollern kann ATA die Windows-Ereignisse 4776, 4732, 4733, 4728, 4729, 4756 und 4757 heranziehen, um die ATA-Erkennung von Pass-the-Hash weiter zu verbessern. Diese Ereignisse können von SIEM erhalten oder durch Festlegen der Windows-Ereignisweiterleitung von Ihrem Domänencontroller aus abgerufen werden. Die gesammelten Ereignisse versorgen ATA mit zusätzlichen Informationen, die nicht über den Netzwerkverkehr des Domänencontrollers verfügbar sind.


## <a name="ata-center-requirements"></a>Voraussetzungen für ATA Center
In diesem Abschnitt werden die Voraussetzungen für ATA Center aufgeführt.

### <a name="general"></a>Allgemein
ATA Center unterstützt die Installation auf einem Server mit Windows Server 2012 R2, Windows Server 2016 und Windows Server 2019. 

 > [!NOTE]
 > ATA Center unterstützt Windows Server Core nicht.

ATA Center kann auf einem Server installiert werden, der Mitglied einer Domäne oder Arbeitsgruppe ist.

Vergewissern Sie sich vor der Installation von ATA Center, das auf Windows 2012 R2 ausgeführt wird, dass das folgende Update installiert wurde: [KB2919355](https://support.microsoft.com/kb/2919355/).

Dies können Sie überprüfen, indem Sie das folgende Windows PowerShell-Cmdlet ausführen: `[Get-HotFix -Id kb2919355]`.

Die Installation von ATA Center als virtueller Computer wird unterstützt. 

### <a name="dynamic-memory"></a>Dynamischer Arbeitsspeicher

> [!NOTE] 
> Wenn das Center als virtueller Computer (VM) ausgeführt wird, ist es erforderlich, dass der gesamte Arbeitsspeicher dem virtuellen Computer ständig zugeordnet wird.

|VM-Host|Description|
|------------|-------------|
|Hyper-V|Stellen Sie sicher, dass **Dynamischen Arbeitsspeicher aktivieren** für den virtuellen Computer nicht aktiviert ist.|
|VMWare|Stellen Sie sicher, dass die konfigurierte und die reservierte Arbeitsspeichermenge gleich sind, oder wählen Sie in den VM-Einstellungen die folgende Option aus: **Gesamten Gastarbeitsspeicher reservieren (alle gesperrt)** .|
|Anderer Virtualisierungshost|Informieren Sie sich in der Dokumentation des Herstellers, wie Sie sicherstellen, dass der Arbeitsspeicher zu jedem Zeitpunkt vollständig dem virtuellen Computer zugewiesen ist. |
|

Wenn Sie ATA Center als virtuellen Computer ausführen, fahren Sie vor dem Erstellen eines neuen Prüfpunkts den Server herunter, um eine potenzielle Beschädigung der Datenbank zu verhindern.

### <a name="server-specifications"></a>Serverspezifikationen

Wenn Sie auf einem physischen Server arbeiten, erfordert die ATA-Datenbank, dass Sie den nicht einheitlichen Speicherzugriff (Non-Uniform Memory Access, NUMA) im BIOS **deaktivieren**. Das System bezieht sich möglicherweise als Knotenüberlappung auf NUMA. In diesem Fall müssen Sie die Knotenüberlappung **aktivieren**, um NUMA zu deaktivieren. Weitere Informationen finden Sie in der BIOS-Dokumentation.<br>

Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** von ATA Center auf **Hohe Leistung** fest.<br>
Die erforderlichen Serverspezifikationen hängen von der Anzahl der überwachten Domänencontroller und der Auslastung der einzelnen Domänencontroller ab. Weitere Informationen finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).

Für Windows-Betriebssysteme 2008R2 und 2012 wird das Gateway im Modus für [mehrere Prozessor Gruppen](https://docs.microsoft.com/windows/win32/procthread/processor-groups) nicht unterstützt. Weitere Informationen über den Modus „Mehrere Prozessorgruppen“ finden Sie unter [Problembehandlung](troubleshooting-ata-known-errors.md#multi-processor-group-mode). 

### <a name="time-synchronization"></a>Zeitsynchronisierung

Die Zeitsynchronisierung des ATA Center-Servers, der ATA-Gatewayserver und der Domänencontroller muss in einem Bereich von fünf Minuten zueinander liegen.


### <a name="network-adapters"></a>Netzwerkadapter

Sie benötigen Folgendes:
-   Mindestens einen Netzwerkadapter (wenn Sie physische Server in einer VLAN-Umgebung verwenden, empfiehlt es sich, zwei Netzwerkadapter zu verwenden)

-   Eine IP-Adresse für die Kommunikation zwischen ATA Center und dem ATA-Gateway, die mithilfe von SSL über Port 443 verschlüsselt wird. (Der ATA-Diensts bindet an alle IP-Adressen, die ATA Center auf Port 443 hat.)

### <a name="ports"></a>Ports
In der folgenden Tabelle sind die Ports aufgelistet, die mindestens geöffnet werden müssen, damit ATA Center ordnungsgemäß funktioniert.

|Protokoll|Transport|Port|Zu/Von|Richtung|
|------------|-------------|--------|-----------|-------------|
|**SSL** (ATA-Kommunikation)|TCP|443|ATA-Gateway|Eingehende Verbindungen|
|**HTTP** (optional)|TCP|80|Unternehmensnetzwerk|Eingehende Verbindungen|
|**HTTPS**|TCP|443|Unternehmensnetzwerk und ATA-Gateway|Eingehende Verbindungen|
|**SMTP** (optional)|TCP|25|SMTP-Server|Outbound|
|**SMTPS** (optional)|TCP|465|SMTP-Server|Outbound|
|**Syslog** (optional)|TCP/UPS/TLS (konfigurierbar)|514 (Standard)|Syslog-Server|Outbound|
|**LDAP**|TCP und UDP|389|Domänencontroller|Outbound|
|**LDAPS** (optional)|TCP|636|Domänencontroller|Outbound|
|**DNS**|TCP und UDP|53|DNS-Server|Outbound|
|**Kerberos** (optional, wenn eine Domäne verknüpft ist)|TCP und UDP|88|Domänencontroller|Outbound|
|**Windows Time** (optional, wenn eine Domäne verknüpft ist)|UDP|123|Domänencontroller|Outbound|

> [!NOTE]
> LDAP ist erforderlich, um die Anmeldeinformationen, die zwischen den ATA-Gateways und den Domänencontrollern verwendet werden sollen, zu testen. Bei dem Test zwischen ATA Center und einem Domänencontroller wird die Gültigkeit dieser Anmeldeinformationen überprüft. Danach verwendet ATA-Gateway LDAP im Rahmen seines normalen Auflösungsprozesses.

### <a name="certificates"></a>Zertifikate

Um die Installation und Bereitstellung von ATA zu beschleunigen, können Sie während dieser Installation selbstsignierte Zertifikate installieren. Wenn Sie selbstsignierte Zertifikate verwendet haben, empfiehlt es sich nach der ersten Bereitstellung, die selbstsignierten Zertifikate durch Zertifikate einer internen Zertifizierungsstelle zu ersetzen, damit ATA Center diese verwendet.


Stellen Sie sicher, dass das ATA-Center und die ATA-Gateways Zugriff auf den CRL-Verteilungspunkt haben. Wenn sie keinen Zugriff auf das Internet haben, führen Sie [das Verfahren zum manuellen Importieren einer Zertifikatsperrliste](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx) durch. Achten Sie dabei darauf, alle CRL-Verteilungspunkte für die gesamte Kette zu installieren.

Ein Zertifikat muss Folgendes besitzen:
-   Einen privaten Schlüssel
-   Den Anbietertyp „Kryptografiedienstanbieter“ (CSP) oder „Schlüsselspeicheranbieter“ (KSP)
-   Eine Länge von 2048 Bits für öffentliche Schlüssel
-   Einen festgelegten Wert für die Flags KeyEncipherment und ServerAuthentication
-   Den KeySpec- bzw. KeyNumber-Wert „KeyExchange“ (AT\_KEYEXCHANGE).
    Der Wert "Signature" (bei\_Signatur) wird *nicht* unterstützt. 
-   Alle Gatewaycomputer müssen in der Lage sein, das ausgewählte Center Zertifikat vollständig zu validieren und zu vertrauen.

Sie können beispielsweise den **Standardwebserver** oder **Computervorlagen** verwenden.

> [!WARNING]
> Die Erneuerung eines vorhandenen Zertifikats wird nicht unterstützt. Zertifikate lassen sich nur erneuern, indem ein neues Zertifikat erstellt und ATA für die Verwendung des neuen Zertifikats konfiguriert wird.


> [!NOTE]
> - Wenn Sie von anderen Computern aus auf die ATA-Konsole zugreifen werden, stellen Sie sicher, dass diese Computer dem von ATA Center verwendeten Zertifikat vertrauen. Andernfalls wird auf einer Warnseite die Meldung angezeigt, dass ein Problem mit dem Sicherheitszertifikat der Website vorliegt, bevor die Anmeldeseite geöffnet wird.
> - Ab ATA Version 1.8 verwalten die ATA-Gateways und Lightweight-Gateways ihre eigenen Zertifikate, sodass keine Administratorinteraktion für die Verwaltung nötig ist.

## <a name="ata-gateway-requirements"></a>Voraussetzungen für das ATA-Gateway
In diesem Abschnitt sind die Voraussetzungen für das ATA-Gateway aufgeführt.
### <a name="general"></a>Allgemein
Das ATA-Gateway unterstützt die Installation auf einem Server mit Windows Server 2012 R2, Windows Server 2016 oder Windows Server 2019 (einschließlich Server Core).
Das ATA-Gateway kann auf einem Server installiert werden, der Mitglied einer Domäne oder Arbeitsgruppe ist.
Das ATA-Gateway kann zur Überwachung von Domänencontrollern mit der Domänenfunktionsebene Windows 2003 und höher verwendet werden.

Vergewissern Sie sich vor der Installation des ATA-Gateways mit Windows 2012 R2, dass das folgende Update installiert wurde: [KB2919355](https://support.microsoft.com/kb/2919355/).

Dies können Sie überprüfen, indem Sie das folgende Windows PowerShell-Cmdlet ausführen: `[Get-HotFix -Id kb2919355]`.


Informationen zur Verwendung von virtuellen Computern mit dem ATA-Gateway finden Sie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md).

> [!NOTE]
> Mindestens 5 GB Speicherplatz wird benötigt, 10 GB wird empfohlen. Dies umfasst den Speicherplatz, der für die ATA-Binärdateien, ATA-Protokolle und [Leistungsprotokolle](troubleshooting-ata-using-perf-counters.md) benötigt wird.

### <a name="server-specifications"></a>Serverspezifikationen
Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des ATA-Gateways auf **Hohe Leistung** fest.<br>
Ein ATA-Gateway kann die Überwachung von mehreren Domänencontrollern unterstützen, abhängig vom Umfang des Netzwerkverkehrs zu und von den Domänencontrollern.

Weitere Informationen zum dynamischen Arbeitsspeicher oder zu anderen Speicherverwaltungsfunktionen für virtuelle Computer finden Sie unter [dynamischer Arbeitsspeicher](#dynamic-memory).

Weitere Informationen zu den Hardwareanforderungen des ATA-Gateways finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Zeitsynchronisierung
Die Zeitsynchronisierung des ATA Center-Servers, der ATA-Gatewayserver und der Domänencontroller muss in einem Bereich von fünf Minuten zueinander liegen.

### <a name="network-adapters"></a>Netzwerkadapter
Das ATA-Gateway erfordert mindestens einen Verwaltungsadapter und mindestens einen Erfassungsadapter:

-   **Verwaltungsadapter:** wird für die Kommunikation im Unternehmensnetzwerk verwendet. Dieser Adapter sollte mit den folgenden Einstellungen konfiguriert werden:

    -   Statische IP-Adresse, einschließlich des Standardgateways

    -   Bevorzugte und alternative DNS-Server

    -   Das **DNS-Suffix für diese Verbindung** sollte der DNS-Name der Domäne für jede Domäne sein, die überwacht wird.

        ![Konfigurieren Sie das DNS-Suffix in den erweiterten TCP/IP-Einstellungen.](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Wenn das ATA-Gateway Mitglied der Domäne ist, erfolgt diese Konfiguration möglicherweise automatisch.

-   **Erfassungsadapter**: wird verwendet, um den Datenverkehr zu und von den Domänencontrollern zu erfassen.

    > [!IMPORTANT]
    > -   Konfigurieren Sie die Portspiegelung für den Erfassungsadapter als Ziel des Domänencontroller-Netzwerkdatenverkehrs. Weitere Informationen finden Sie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md). In der Regel müssen Sie mit dem Netzwerk- oder Virtualisierungsteam zusammenarbeiten, um die Portspiegelung zu konfigurieren.
    > -   Konfigurieren Sie eine statische, nicht routingfähige IP-Adresse für Ihre Umgebung ohne Standardgateway und ohne DNS-Serveradressen. Beispiel: 1.1.1.1/32. Dadurch wird sichergestellt, dass der Erfassungsnetzwerkadapter die maximale Menge an Datenverkehr erfassen kann und der Verwaltungsnetzwerkadapter zum Senden und Empfangen des erforderlichen Netzwerkdatenverkehrs verwendet wird.

### <a name="ports"></a>Ports
In der folgenden Tabelle sind die Ports aufgeführt, die für den Verwaltungsadapter des ATA-Gateways mindestens konfiguriert werden müssen:

|Protokoll|Transport|Port|Zu/Von|Richtung|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP und UDP|389|Domänencontroller|Outbound|
|Sicheres LDAP (LDAPS)|TCP|636|Domänencontroller|Outbound|
|LDAP an globalen Katalog|TCP|3268|Domänencontroller|Outbound|
|LDAPs an globalen Katalog|TCP|3269|Domänencontroller|Outbound|
|Kerberos|TCP und UDP|88|Domänencontroller|Outbound|
|Netlogon (SMB, CIFS, SAM-R)|TCP und UDP|445|Alle Geräte im Netzwerk|Outbound|
|Windows-Zeitdienst|UDP|123|Domänencontroller|Outbound|
|Domain Name System|TCP und UDP|53|DNS-Server|Outbound|
|NTLM über RPC|TCP|135|Alle Geräte im Netzwerk|Both|
|NetBIOS|UDP|137|Alle Geräte im Netzwerk|Both|
|SSL|TCP|443|ATA Center|Outbound|
|Syslog (optional)|UDP|514|SIEM-Server|Eingehende Verbindungen|


> [!NOTE]
> Als Teil des vom ATA-Gateway durchgeführten Auflösungsprozesses müssen die folgenden eingehenden Ports für Geräte im Netzwerk geöffnet werden.
>
> -   NTLM über RPC (TCP-Port 135)
> -   NetBIOS (UDP-Port 137)
> - Bei Verwendung des Verzeichnisdienst-Benutzerkontos fragt der ATA Gateway mithilfe von SAM-R (Netzwerkanmeldung) Endpunkte in Ihrer Organisation für lokale Administratoren ab, um [den Graph des Lateral-Movement-Pfads](use-case-lateral-movement-path.md) zu erstellen. Weitere Informationen finden Sie unter [Erforderliche Berechtigung für SAM-R konfigurieren](install-ata-step9-samr.md).
> - Die folgenden Ports müssen auf eingehenden Geräten im Netzwerk des ATA-Gateways freigegeben sein:
>   -   NTLM über RPC (TCP-Port 135) für Lösungszwecke
>   -   NetBIOS (UDP-Port 137) für Lösungszwecke

## <a name="ata-lightweight-gateway-requirements"></a>ATA-Lightweight-Gateway-Anforderungen
In diesem Abschnitt sind die Voraussetzungen für das ATA-Lightweight-Gateway aufgeführt.
### <a name="general"></a>Allgemein
Das ATA-Lightweight-Gateway unterstützt die Installation auf einem Domänencontroller mit Windows Server 2008 R2 SP1 (ohne Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 und Windows Server 2019 (mit Core, jedoch ohne Nano).

Beim Domänencontroller kann es sich um einen schreibgeschützten Domänencontroller (Read Only Domain Controller, RODC) handeln.

Vergewissern Sie sich vor der Installation des ATA-Lightweight-Gateways auf einem Domänencontroller unter Windows Server 2012 R2, dass das folgende Update installiert wurde: [KB2919355](https://support.microsoft.com/kb/2919355/).

Dies können Sie überprüfen, indem Sie dieses Windows PowerShell-Cmdlet ausführen: `[Get-HotFix -Id kb2919355]`.

Wenn die Installation unter Windows Server 2012 R2 Server Core erfolgt, muss auch das folgende Update installiert werden: [KB3000850](https://support.microsoft.com/help/3000850/november-2014-update-rollup-for-windows-rt-8.1%2c-windows-8.1%2c-and-windows-server-2012-r2).

 Dies können Sie überprüfen, indem Sie dieses Windows PowerShell-Cmdlet ausführen: `[Get-HotFix -Id kb3000850]`.


Während der Installation wird .NET Framework 4.6.1 installiert und verursacht möglicherweise den Neustart des Domänencontrollers.


> [!NOTE]
> Mindestens 5 GB Speicherplatz wird benötigt, 10 GB wird empfohlen. Dies umfasst den Speicherplatz, der für die ATA-Binärdateien, ATA-Protokolle und [Leistungsprotokolle](troubleshooting-ata-using-perf-counters.md) benötigt wird.

### <a name="server-specifications"></a>Serverspezifikationen

Das ATA-Lightweight-Gateway erfordert mindestens 2 Kerne und 6 GB RAM auf dem Domänencontroller.
Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des ATA-Lightweight-Gateways auf **Hohe Leistung** fest.
Das ATA-Lightweight-Gateway kann auf den Domänencontrollern verschiedener Auslastungen und Größen bereitgestellt werden, abhängig vom Umfang des Netzwerkverkehrs zwischen den Domänencontrollern und der auf dem Domänencontroller installierten Ressourcen.

Weitere Informationen zum dynamischen Arbeitsspeicher oder zu anderen Speicherverwaltungsfunktionen für virtuelle Computer finden Sie unter [dynamischer Arbeitsspeicher](#dynamic-memory).

Weitere Informationen zu den Hardwareanforderungen des ATA-Lightweight-Gateways finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Zeitsynchronisierung

Die Zeitsynchronisierung des ATA Center-Servers, der ATA-Lightweight-Gatewayserver und der Domänencontroller muss in einem Bereich von fünf Minuten zueinander liegen.

### <a name="network-adapters"></a>Netzwerkadapter

Das ATA-Lightweight-Gateway überwacht den lokalen Datenverkehr auf allen Netzwerkadaptern des Domänencontrollers. <br>
Nach der Bereitstellung können Sie die ATA-Konsole verwenden, wenn Sie die überwachten Netzwerkadapter jemals ändern möchten.

> [!NOTE]
> Das Lightweight-Gateway wird nicht in Domänencontrollern unter Windows 2008 R2 mit aktivierten Teamvorgängen für Broadcom-Netzwerkadapter unterstützt.

### <a name="ports"></a>Ports
In der folgenden Tabelle sind die Ports aufgeführt, die für das ATA-Lightweight-Gateway mindestens konfiguriert werden müssen.

|Protokoll|Transport|Port|Zu/Von|Richtung|
|------------|-------------|--------|-----------|-------------|
|Domain Name System|TCP und UDP|53|DNS-Server|Outbound|
|NTLM über RPC|TCP|135|Alle Geräte im Netzwerk|Both|
|NetBIOS|UDP|137|Alle Geräte im Netzwerk|Both|
|SSL|TCP|443|ATA Center|Outbound|
|Syslog (optional)|UDP|514|SIEM-Server|Eingehende Verbindungen|
|Netlogon (SMB, CIFS, SAM-R)|TCP und UDP|445|Alle Geräte im Netzwerk|Outbound|

> [!NOTE]
> Als Teil des vom ATA-Lightweight-Gateway durchgeführten Auflösungsprozesses müssen die folgenden eingehenden Ports für Geräte im Netzwerk geöffnet werden.
>
> -   NTLM über RPC
> -   NetBIOS
> - Bei Verwendung des Verzeichnisdienst-Benutzerkontos fragt der ATA-Lightweight-Gateway mithilfe von SAM-R (Netzwerkanmeldung) Endpunkte in Ihrer Organisation für lokale Administratoren ab, um [den Graph des Lateral-Movement-Pfads](use-case-lateral-movement-path.md) zu erstellen. Weitere Informationen finden Sie unter [Erforderliche Berechtigung für SAM-R konfigurieren](install-ata-step9-samr.md).
> - Die folgenden Ports müssen auf eingehenden Geräten im Netzwerk des ATA-Gateways freigegeben sein:
>   -   NTLM über RPC (TCP-Port 135) für Lösungszwecke
>   -   NetBIOS (UDP-Port 137) für Lösungszwecke

## <a name="ata-console"></a>ATA-Konsole
Der Zugriff auf die ATA-Konsole erfolgt über einen Browser. Folgende Browser und Einstellungen werden unterstützt:

-   Internet Explorer Version 10 oder höher

-   Microsoft Edge

-   Google Chrome 40 und höher

-   Mindestauflösung der Bildschirmbreite: 1.700 Pixel

## <a name="related-videos"></a>Verwandte Videos
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Weitere Informationen:
- [Tool zur Bemessung von ATA-Gateways](https://aka.ms/atasizingtool)
- [ATA-Architektur](ata-architecture.md)
- [Installieren von ATA](install-ata-step1.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)


