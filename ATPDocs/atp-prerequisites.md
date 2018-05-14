---
title: Voraussetzungen für Azure Advanced Threat Protection | Microsoft Dokumentation
description: Beschreibt die Voraussetzungen für eine erfolgreiche Bereitstellung von Azure ATP in Ihrer Umgebung.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/8/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ae859121fbe856c93b8568ef38bf0b4bdb77837a
ms.sourcegitcommit: 8472f3f46fc90da7471cd1065cdb2f6a1d5a9f69
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/08/2018
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="azure-atp-prerequisites"></a>Voraussetzungen für Azure ATP
Dieser Artikel beschreibt die Voraussetzungen für eine erfolgreiche Bereitstellung von Azure ATP in Ihrer Umgebung.

>[!NOTE]
> Informationen zum Planen von Ressourcen und Kapazitäten finden Sie unter [Azure ATP-Kapazitätsplanung](atp-capacity-planning.md).


Azure ATP besteht aus dem Azure ATP-Clouddienst, der aus dem Arbeitsbereich-Verwaltungsportal und dem Arbeitsbereichsportal besteht, dem eigenständigen Azure ATP-Sensor und/oder dem Azure ATP-Sensor. Weitere Informationen zu den Azure ATP-Komponenten finden Sie unter [Azure ATP-Architektur](atp-architecture.md).

Jeder Azure ATP-Arbeitsbereich unterstützt eine Active Directory-Gesamtstrukturbegrenzung und die Gesamtstrukturfunktionsebene (Forest Functional Level; FFL) von Windows 2003 und höher. Für Bereitstellungen mit mehreren Gesamtstrukturen ist ein separater Azure ATP-Arbeitsbereich für jede Gesamtstruktur erforderlich.


[Vorbereitung](#before-you-start): In diesem Abschnitt werden die Informationen aufgeführt, die Sie sammeln sollten, und Konten und Netzwerkentitäten genannt, die vor der Installation von Azure ATP vorhanden sein sollten.

[Azure ATP-Arbeitsbereich-Verwaltungsportal](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): In diesem Abschnitt werden die Browseranforderungen für das Arbeitsbereich-Verwaltungsportal beschrieben.

[Azure ATP-Arbeitsbereichsportal](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): In diesem Abschnitt werden die Browseranforderungen für das Ausführen des Azure ATP-Arbeitsbereichsportals beschrieben.

[Eigenständiger Azure ATP-Sensor](#azure-atp-sensor-requirements): In diesem Abschnitt werden die Hardware- und Softwareanforderungen für den eigenständigen Azure ATP-Sensor beschrieben und Einstellungen genannt, die Sie auf Ihren eigenständigen Azure ATP-Sensorservern konfigurieren müssen.

[Azure ATP-Sensor](#azure-atp-lightweight-sensor-requirements): In diesem Abschnitt werden die Hardware- und Softwareanforderungen für den Azure ATP-Sensor beschrieben.

![Azure ATP-Architekturdiagramm](media/ATP-architecture-topology.png)

## <a name="before-you-start"></a>Vorbereitung
In diesem Abschnitt werden die Informationen aufgeführt, die Sie sammeln sollten, und Konten- und Netzwerk-Entitäten genannt, die vor der Installation von Azure ATP vorhanden sein sollten.


-   Ein **lokales** AD-Benutzerkonto und -Kennwort mit Lesezugriff auf alle Objekte in den überwachten Domänen.

    > [!NOTE]
    > Wenn Sie benutzerdefinierte ACLs für verschiedene Organisationseinheiten (OU) in Ihrer Domäne festgelegt haben, stellen Sie sicher, dass der ausgewählte Benutzer Leseberechtigungen für diese Organisationseinheiten hat.

-   Wenn Sie Wireshark auf einem eigenständigen Azure ATP-Sensor ausführen, müssen Sie den „Microsoft Advanced Threat Analytics“-Sensordienst neu starten, nachdem Sie das Erfassen mit Wireshark abgeschlossen haben. Wenn dies nicht der Fall ist, beendet der Sensor die Erfassung von Datenverkehr.

- Wenn Sie versuchen, den ATP-Sensor auf einem Computer zu installieren, der mit einem NIC-Teaming-Adapter konfiguriert ist, wird ein Installationsfehler gemeldet. Wenn Sie den ATP-Sensor auf einem Computer installieren möchten, der mit NIC-Teamvorgang konfiguriert ist, kontaktieren Sie bitte einen Azure ATP-Supportmitarbeiter.

-    Empfohlen: Benutzer sollten über schreibgeschützten Zugriff auf den Container mit gelöschten Objekten verfügen. So kann Azure ATP eine Massenlöschung von Objekten in der Domäne erkennen. Informationen zum Konfigurieren des schreibgeschützten Zugriffs auf den Container mit gelöschten Objekten finden Sie im Abschnitt **Changing permissions on a deleted object container** (Ändern von Berechtigungen für einen Container mit gelöschten Objekten) im Artikel [View or Set Permissions on a Directory Object](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) (Anzeigen und Festlegen von Berechtigungen für ein Verzeichnisobjekt).

-   Optional: ein Benutzerkonto eines Benutzers ohne Netzwerkaktivitäten. Dieses Konto wird als Azure ATP-Honeytoken-Benutzer konfiguriert. Weitere Informationen finden Sie unter [Configure IP address exclusions and Honeytoken user (Konfigurieren von Ausschlüssen und Honeytoken-Benutzern)](install-atp-step7.md).

-   Optional: Wenn Sie den eigenständigen Sensor bereitstellen, ist die Weiterleitung der Windows-Ereignisse 4776, 4732, 4733, 4728, 4729, 4756, 4757 und 7045 an ATP nötig, um in Azure ATP Pass-the-Hash, Brute Force, Änderungen an sensiblen Gruppen, Honeytoken-Erkennungen und das Erstellen eines schädlichen Diensts zu verbessern. Diese Ereignisse werden vom Azure ATP-Sensor automatisch empfangen. Im eigenständigen Azure ATP-Sensor können diese Ereignisse von SIEM erhalten oder durch Festlegen der Windows-Ereignisweiterleitung von Ihrem Domänencontroller aus abgerufen werden. Die gesammelten Ereignisse versorgen Azure ATP mit zusätzlichen Informationen, die nicht über den Datenverkehr des Domänencontrollers verfügbar sind.


## <a name="azure-atp-workspace-management-portal-and-workspace-portal-requirements"></a>Voraussetzungen für Azure ATP-Arbeitsbereich-Verwaltungsportal und -Arbeitsbereichsportal
Zugriff auf das Azure ATP-Arbeitsbereichsportal und das Azure ATP-Arbeitsbereich-Verwaltungsportal erfolgt über einen Browser. Folgende Browser und Einstellungen werden unterstützt:
-   Microsoft Edge
-   Internet Explorer Version 10 oder höher
-   Google Chrome 4.0 und höher
-   Mindestauflösung der Bildschirmbreite: 1.700 Pixel
-   Firewall/Proxy freigeben – Um mit dem Azure ATP-Clouddienst zu kommunizieren, müssen Sie in Ihrer Firewall und auf Ihrem Proxyserver Port 443 für „*.atp.azure.com“ freigeben. 

## <a name="azure-atp-standalone-sensor-requirements"></a>Voraussetzungen für den eigenständigen Azure ATP-Sensor
In diesem Abschnitt werden die Voraussetzungen für den eigenständigen Azure ATP-Sensor aufgeführt.
### <a name="general"></a>Allgemein
Der eigenständige Azure ATP-Sensor unterstützt die Installation auf einem Server mit Windows Server 2012 R2 oder Windows Server 2016 (einschließlich Server Core).
Der eigenständige Azure ATP-Sensor kann auf einem Server installiert werden, der Mitglied einer Domäne oder Arbeitsgruppe ist.
Der eigenständige Azure ATP-Sensor kann zur Überwachung von Domänencontrollern mit der Domänenfunktionsebene Windows 2003 und höher verwendet werden.

Für die Kommunikation Ihrer Domänencontroller mit dem Clouddienst müssen Sie in Ihrer Firewall und auf Ihrem Proxyserver Port 443 für „*.atp.azure.com“ freigeben.


Informationen zur Verwendung von virtuellen Computern mit dem eigenständigen Azure ATP-Sensor finden Sie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md).

> [!NOTE]
> Mindestens 5 GB Speicherplatz auf dem Datenträger wird benötigt, 10 GB wird empfohlen. Dies umfasst den Speicherplatz, der für die Azure ATP-Binärdateien, Azure ATP-Protokolle und Leistungsprotokolle benötigt wird.

### <a name="server-specifications"></a>Serverspezifikationen
Um eine optimale Leistung zu erzielen, legen Sie die **Energieoptionen** des eigenständigen Azure ATP-Sensors auf **Hohe Leistung** fest.<br>
Ein eigenständiger Azure ATP-Sensor kann die Überwachung von mehreren Domänencontrollern unterstützen, abhängig vom Umfang des Datenverkehrs zwischen den Domänencontrollern.

>[!NOTE] 
> Bei Ausführung als virtueller Computer wird kein dynamischer Arbeitsspeicher und keine andere Speichererweiterungsfunktion unterstützt.

Weitere Informationen zu den Hardwareanforderungen des eigenständigen Azure ATP-Sensors finden Sie unter [Azure ATP-Kapazitätsplanung](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Zeitsynchronisierung

Die Zeitsynchronisierung der Server und Domänencontroller, auf denen der Sensor installiert ist, muss in einem Bereich von fünf Minuten zueinander liegen.


### <a name="network-adapters"></a>Netzwerkadapter
Der eigenständige Azure ATP-Sensor erfordert mindestens einen Verwaltungsadapter und mindestens einen Erfassungsadapter:

-   **Verwaltungsadapter:** wird für die Kommunikation im Unternehmensnetzwerk verwendet. Der Sensor nutzt diesen Adapter für Abfragen des Domänencontrollers, den er schützt, und für Korrekturen an Computerkonten. <br>Dieser Adapter sollte mit den folgenden Einstellungen konfiguriert werden:

    -   Statische IP-Adresse, einschließlich des Standardgateways

    -   Bevorzugte und alternative DNS-Server

    -   Das **DNS-Suffix für diese Verbindung** sollte der DNS-Name der Domäne für jede Domäne sein, die überwacht wird.

        ![Konfigurieren Sie das DNS-Suffix in den erweiterten TCP/IP-Einstellungen.](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > Wenn der eigenständige Azure ATP-Sensor Mitglied der Domäne ist, erfolgt diese Konfiguration möglicherweise automatisch.

-   **Erfassungsadapter**: wird verwendet, um den Datenverkehr zu und von den Domänencontrollern zu erfassen.

    > [!IMPORTANT]
    > -   Konfigurieren Sie die Portspiegelung für den Erfassungsadapter als Ziel des Domänencontroller-Netzwerkdatenverkehrs. Weitere Informationen finden Sie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md). In der Regel müssen Sie mit dem Netzwerk- oder Virtualisierungsteam zusammenarbeiten, um die Portspiegelung zu konfigurieren.
    > -   Konfigurieren Sie eine statische, nicht routingfähige IP-Adresse für Ihre Umgebung ohne Standardsensor und ohne DNS-Serveradressen. Beispiel: 1.1.1.1/32. Dadurch wird sichergestellt, dass der Erfassungsnetzwerkadapter die maximale Menge an Datenverkehr erfassen kann und der Verwaltungsnetzwerkadapter zum Senden und Empfangen des erforderlichen Netzwerkdatenverkehrs verwendet wird.

### <a name="ports"></a>Ports
In der folgenden Tabelle sind die Ports aufgeführt, die für den Verwaltungsadapter des eigenständigen Azure ATP-Sensors mindestens konfiguriert werden müssen:

|Protokoll|Transport|Port|Zu/Von|Richtung|
|------------|-------------|--------|-----------|-------------|
|**Internetports**|||||
|SSL (*.atp.azure.com)|TCP|443|Azure ATP-Clouddienst|Ausgehend|
|**Interne Ports**|||||
|LDAP|TCP und UDP|389|Domänencontroller|Ausgehend|
|Sicheres LDAP (LDAPS)|TCP|636|Domänencontroller|Ausgehend|
|LDAP an globalen Katalog|TCP|3268|Domänencontroller|Ausgehend|
|LDAPs an globalen Katalog|TCP|3269|Domänencontroller|Ausgehend|
|Kerberos|TCP und UDP|88|Domänencontroller|Ausgehend|
|Netlogon (SMB, CIFS, SAM-R)|TCP und UDP|445|Alle Geräte im Netzwerk|Ausgehend|
|Windows-Zeitdienst|UDP|123|Domänencontroller|Ausgehend|
|DNS|TCP und UDP|53|DNS-Server|Ausgehend|
|NTLM über RPC|TCP|135|Alle Geräte im Netzwerk|Ausgehend|
|NetBIOS|UDP|137|Alle Geräte im Netzwerk|Ausgehend|
|Syslog (optional)|TCP/UDP|514, je nach Konfiguration|SIEM-Server|Eingehend|
|RADIUS|UDDP|1813|RADIUS|Eingehend|
|RDP|TCP|3389|Alle Geräte im Netzwerk|Ausgehend|

> [!NOTE]
> - Bei Verwendung des Verzeichnisdienst-Benutzerkontos fragt der Sensor mithilfe von SAM-R (Netzwerkanmeldung) Endpunkte in Ihrer Organisation für lokale Administratoren ab, um [den Graph des Lateral-Movement-Pfads](use-case-lateral-movement-path.md) zu erstellen. Weitere Informationen finden Sie unter [Erforderliche Berechtigung für SAM-R konfigurieren](install-atp-step8-samr.md).
> - Die folgenden Ports müssen auf eingehenden Geräten im Netzwerk des eigenständigen Azure ATP-Sensors geöffnet sein:
>   -   NTLM über RPC (TCP-Port 135) für Lösungszwecke
>   -   NetBIOS (UDP-Port 137) für Lösungszwecke
>   -   RDP (TCP-Port 3389), nur das erste Paket von *Client hello* zu Auflösungszwecken<br> Beachten Sie, dass auf keinem Port eine Authentifizierung durchgeführt wird.

## <a name="azure-atp-sensor-requirements"></a>Voraussetzungen für den Azure ATP-Sensor
In diesem Abschnitt sind die Voraussetzungen für den Azure ATP-Sensor aufgeführt.
### <a name="general"></a>Allgemein
Der Azure ATP-Sensor unterstützt die Installation auf einem Domänencontroller mit Windows Server 2008 R2 SP1 (ohne Server Core), Windows Server 2012, Windows Server 2012 R2 und Windows Server 2016 (mit Core, jedoch ohne Nano).

Beim Domänencontroller kann es sich um einen schreibgeschützten Domänencontroller (Read Only Domain Controller, RODC) handeln.

Für die Kommunikation Ihrer Domänencontroller mit dem Clouddienst müssen Sie in Ihrer Firewall und auf Ihrem Proxyserver Port 443 für „*.atp.azure.com“ freigeben.

Während der Installation wird .NET Framework 4.7 installiert und erfordert möglicherweise einen Neustart des Domänencontrollers,wenn ein Neustart bereits aussteht.


> [!NOTE]
> Mindestens 5 GB Speicherplatz auf dem Datenträger wird benötigt, 10 GB wird empfohlen. Dies umfasst den Speicherplatz, der für die Azure ATP-Binärdateien, Azure ATP-Protokolle und Leistungsprotokolle benötigt wird.

### <a name="server-specifications"></a>Serverspezifikationen

Der Azure ATP-Sensor erfordert mindestens zwei Kerne und 6 GB RAM auf dem Domänencontroller.
Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des Azure ATP-Sensors auf **Hohe Leistung** fest.
Der Azure ATP-Sensor kann auf Domänencontrollern verschiedener Auslastungen und Größen bereitgestellt werden, abhängig vom Umfang des Datenverkehrs zwischen den Domänencontrollern und der installierten Ressourcen auf dem Domänencontroller.

>[!NOTE] 
> Bei Ausführung als virtueller Computer wird kein dynamischer Arbeitsspeicher und keine andere Speichererweiterungsfunktion unterstützt.

Weitere Informationen zu den Hardwareanforderungen des Azure ATP-Sensors finden Sie unter [Azure ATP-Kapazitätsplanung](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Zeitsynchronisierung

Die Zeitsynchronisierung der Server und Domänencontroller, auf denen der Sensor installiert ist, muss in einem Bereich von fünf Minuten zueinander liegen.

### <a name="network-adapters"></a>Netzwerkadapter

Der Azure ATP-Sensor überwacht den lokalen Datenverkehr auf allen Netzwerkadaptern des Domänencontrollers. <br>
Nach der Bereitstellung können Sie das Azure ATP-Arbeitsbereichsportal verwenden, wenn Sie die überwachten Netzwerkadapter jemals ändern möchten.

Der Sensor wird nicht in Domänencontrollern unter Windows 2008 R2 mit aktivierten Teamvorgängen für Broadcom-Netzwerkadapter unterstützt.

### <a name="ports"></a>Ports
In der folgenden Tabelle sind die Ports aufgeführt, die für den Azure ATP-Sensor mindestens konfiguriert werden müssen:

|Protokoll|Transport|Port|Zu/Von|Richtung|
|------------|-------------|--------|-----------|-------------|
|**Internetports**|||||
|SSL (*.atp.azure.com)|TCP|443|Azure ATP-Clouddienst|Ausgehend|
|**Interne Ports**|||||
|DNS|TCP und UDP|53|DNS-Server|Ausgehend|
|NTLM über RPC|TCP|135|Alle Geräte im Netzwerk|Ausgehend|
|Netlogon (SMB, CIFS, SAM-R)|TCP/UDP|445|Alle Geräte im Netzwerk|Ausgehend|
|NetBIOS|UDP|137|Alle Geräte im Netzwerk|Ausgehend|
|Syslog (optional)|TCP/UDP|514, je nach Konfiguration|SIEM-Server|Eingehend|
|RADIUS|UDDP|1813|RADIUS|Eingehend|
|TLS-zu-RDP-Port|TCP|3389|Alle Geräte im Netzwerk|Ausgehend|

> [!NOTE]
> - Bei Verwendung des Verzeichnisdienst-Benutzerkontos fragt der Sensor mithilfe von SAM-R (Netzwerkanmeldung) Endpunkte in Ihrer Organisation für lokale Administratoren ab, um [den Graph des Lateral-Movement-Pfads](use-case-lateral-movement-path.md) zu erstellen. Weitere Informationen finden Sie unter [Erforderliche Berechtigung für SAM-R konfigurieren](install-atp-step8-samr.md).
> - Die folgenden Ports müssen auf eingehenden Geräten im Netzwerk des eigenständigen Azure ATP-Sensors geöffnet sein:
>   -   NTLM über RPC (TCP-Port 135) für Lösungszwecke
>   -   NetBIOS (UDP-Port 137) für Lösungszwecke
>   -   RDP (TCP-Port 3389), nur das erste Paket von *Client hello* zu Auflösungszwecken<br> Beachten Sie, dass auf keinem Port eine Authentifizierung durchgeführt wird.




## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Azure ATP architecture (Azure ATP-Architektur)](atp-architecture.md)
- [Install ATP (Installieren von ATP)](install-atp-step1.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)

