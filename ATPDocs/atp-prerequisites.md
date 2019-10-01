---
title: Voraussetzungen für Azure Advanced Threat Protection | Microsoft Dokumentation
description: Beschreibt die Voraussetzungen für eine erfolgreiche Bereitstellung von Azure ATP in Ihrer Umgebung.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 763f27e9fb3e134f97b716306c747ecce7edf411
ms.sourcegitcommit: 0a98c0c151be2a81a3bb9ff1301d35a3091079ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71217665"
---
# <a name="azure-atp-prerequisites"></a>Voraussetzungen für Azure ATP

Dieser Artikel beschreibt die Voraussetzungen für eine erfolgreiche Bereitstellung von Azure ATP in Ihrer Umgebung.

>[!NOTE]
> Informationen zum Planen von Ressourcen und Kapazitäten finden Sie unter [Azure ATP-Kapazitätsplanung](atp-capacity-planning.md).


Azure ATP besteht aus dem Azure ATP-Clouddienst, der sich aus dem Azure ATP-Portal, dem Azure ATP-Sensor und/oder dem eigenständigen Azure ATP-Sensor zusammensetzt. Weitere Informationen zu den einzelnen Azure ATP-Komponenten finden Sie unter [Azure ATP-Architektur](atp-architecture.md).

Azure ATP schützt Ihre lokalen Active Directory-Benutzer und/oder Benutzer, die mit Ihrer Azure Active Directory-Instanz synchronisiert werden. Hinweise zum Schutz einer Umgebung, die nur aus AAD-Benutzern besteht, finden Sie unter [AAD Identity Protection](https://docs.microsoft.com/azure/active-directory/identity-protection/overview). 

Zum Erstellen Ihrer Azure ATP-Instanz benötigen Sie einen AAD-Mandanten mit mindestens einem globalen Administrator bzw. einem Sicherheitsadministrator. Jede Azure ATP-Instanz unterstützt mehrere Active Directory-Gesamtstrukturbegrenzungen und die Gesamtstrukturfunktionsebene (Forest Functional Level, FFL) von Windows 2003 und höher. 

Dieser Leitfaden zu Voraussetzungen wird in die folgenden Abschnitte unterteilt, um sicherzustellen, dass Sie über alle erforderlichen Informationen verfügen, die Sie für eine erfolgreiche Bereitstellung von Azure ATP benötigen. 

[Bevor Sie beginnen:](#before-you-start) In diesem Abschnitt werden die zu sammelnden Informationen aufgeführt sowie Konten und Netzwerkentitäten, die vor Beginn der Installation vorhanden sein sollten.

[Azure ATP-Portal](#azure-atp-portal-requirements): In diesem Abschnitt werden die Browseranforderungen für das Azure ATP-Portal erläutert.

[Azure ATP-Sensor](#azure-atp-sensor-requirements): In diesem Abschnitt werden die Hardware- und Softwareanforderungen für den Azure ATP-Sensor beschrieben.

[Eigenständiger Azure ATP-Sensor](#azure-atp-standalone-sensor-requirements): In diesem Abschnitt werden die Hardware- und Softwareanforderungen für den eigenständigen Azure ATP-Sensor beschrieben und Einstellungen genannt, die Sie auf Ihren eigenständigen Azure ATP-Sensorservern konfigurieren müssen.

## <a name="before-you-start"></a>Vorbereitung
In diesem Abschnitt werden die Informationen aufgeführt, die Sie sammeln sollten, sowie Konten und Netzwerkinformationen genannt, die vor der Azure ATP-Installation vorhanden sein sollten.

- Sie können eine Lizenz für Enterprise Mobility + Security 5 (EMS E5) entweder direkt über das [Microsoft 365-Portal](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) oder über das CSP-Lizenzierungsmodell (Cloud Solution Partner) erwerben. Eigenständige Azure ATP Lizenzen sind ebenfalls verfügbar.  

- Überprüfen Sie, ob die Domänencontroller, auf denen Sie Azure ATP-Sensoren installieren möchten, über das Internet mit dem Azure ATP-Clouddienst verbunden sind. Der Azure ATP-Sensor unterstützt die Verwendung eines Proxys. Weitere Informationen zur Proxykonfiguration finden Sie unter [Konfigurieren eines Proxys für Azure ATP](configure-proxy.md).  

-   Ein **lokales** AD-Benutzerkonto und -Kennwort mit Lesezugriff auf alle Objekte in den überwachten Domänen.

    > [!NOTE]
    > Wenn Sie benutzerdefinierte ACLs für verschiedene Organisationseinheiten (OU) in Ihrer Domäne festgelegt haben, stellen Sie sicher, dass der ausgewählte Benutzer Leseberechtigungen für diese Organisationseinheiten hat.

-   Wenn Sie Wireshark für einen eigenständigen Azure ATP-Sensor ausführen, müssen Sie den Azure Advanced Threat Protection-Sensordienst neu starten, nachdem Sie die Wireshark-Erfassung beendet haben. Wenn Sie den Sensordienst nicht neu starten, beendet der Sensor die Erfassung des Datenverkehrs.

- Wenn Sie versuchen, den Azure ATP-Sensor auf einem Computer zu installieren, der mit einem NIC-Teaming-Adapter konfiguriert ist, wird ein Installationsfehler gemeldet. Wenn Sie den Azure ATP-Sensor auf einem Computer installieren möchten, der mit NIC-Teamvorgang konfiguriert ist, finden Sie weitere Informationen unter [Problem mit NIC-Teamvorgängen beim Azure ATP-Sensor](troubleshooting-atp-known-issues.md#nic-teaming).

- Container mit **gelöschten Objekten** – Empfehlung: Der Benutzer sollte über den schreibgeschützten Zugriff auf den Container mit gelöschten Objekten verfügen. Durch schreibgeschützte Berechtigungen für diesen Container kann Azure ATP Löschungen von Benutzern über Ihr Active Directory erkennen. Informationen zum Konfigurieren des schreibgeschützten Zugriffs auf den Container mit gelöschten Objekten finden Sie im Abschnitt **Ändern von Berechtigungen für einen Container mit gelöschten Objekten** im Artikel [Anzeigen und Festlegen von Berechtigungen für ein Verzeichnisobjekt](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

- Optionales **Honeytoken**: Ein Benutzerkonto eines Benutzers ohne Netzwerkaktivitäten. Dieses Konto wird als Azure ATP-Honeytoken-Benutzer konfiguriert. Weitere Informationen zu Verwendung von Honeytokens finden Sie unter [Konfigurieren von Ausschlüssen und Honeytoken-Benutzern](install-atp-step7.md).

- Optional: Wenn Sie den eigenständigen Sensor bereitstellen, ist die Weiterleitung der Windows-Ereignisse 4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045 und 8004 an Azure ATP erforderlich, um in Azure ATP authentifizierungsbasierte Erkennungen, Ergänzungen sensibler Gruppen und Erkennungen der Erstellung verdächtiger Dienste zu verbessern.  Der Azure ATP-Sensor empfängt diese Ereignisse automatisch. Im eigenständigen Azure ATP-Sensor können diese Ereignisse von SIEM empfangen oder durch Festlegen der Windows-Ereignisweiterleitung von Ihrem Domänencontroller aus abgerufen werden. Die gesammelten Ereignisse versorgen Azure ATP mit zusätzlichen Informationen, die nicht über den Datenverkehr des Domänencontrollers verfügbar sind.

## <a name="azure-atp-portal-requirements"></a>Anforderungen an das Azure ATP-Portal
Der Zugriff auf das Azure ATP-Portal erfolgt über einen Browser. Folgende Browser und Einstellungen werden unterstützt:
-   Microsoft Edge
-   Internet Explorer Version 10 oder höher
-   Google Chrome 4.0 und höher
-   Mindestauflösung der Bildschirmbreite: 1.700 Pixel
-   Firewall/Proxy freigeben – Um mit dem Azure ATP-Clouddienst zu kommunizieren, muss in Ihrer Firewall und auf Ihrem Proxyserver Port 443 für „*.atp.azure.com“ freigegeben sein.

 ![Azure ATP-Architekturdiagramm](media/azure-atp-architecture.png)

> [!NOTE]
> Standardmäßig unterstützt Azure ATP bis zu 200 Sensoren. Kontaktieren Sie den Azure ATP-Support, wenn Sie mehr Sensoren installieren möchten.


## <a name="azure-atp-network-name-resolution-nnr-requirements"></a>Anforderungen an die Azure ATP-Netzwerknamensauflösung
Die Netzwerknamensauflösung (Network Name Resolution, NNR) ist ein Hauptbestandteil der Azure ATP-Funktionalität. Damit der Azure ATP-Dienst ordnungsgemäß funktioniert, muss mindestens eine der folgenden NNR-Methoden für Azure ATP-Sensoren zugänglich sein:
1. **NTLM über RPC** (TCP-Port 135)
2. **NetBIOS** (UDP-Port 137)
3. **RDP** (TCP-Port 3389): nur das erste Client Hello-Paket
4. **Abfragen des DNS-Servers mittels Reverse-DNS-Lookup der IP-Adresse** (UDP-Port 53)

Damit die Methoden 1, 2 und 3 funktionieren, müssen die entsprechenden Ports für eingehenden Datenverkehr von den Azure ATP-Sensoren zu Geräten im Netzwerk geöffnet sein. Weitere Informationen zu Azure ATP und NNR finden Sie unter [Azure ATP-NNR-Richtlinie](atp-nnr-policy.md). 

## <a name="azure-atp-sensor-requirements"></a>Voraussetzungen für den Azure ATP-Sensor
In diesem Abschnitt sind die Voraussetzungen für den Azure ATP-Sensor aufgeführt.

### <a name="general"></a>Allgemein

> [!NOTE]
> Achten Sie darauf, dass [KB4487044](https://support.microsoft.com/help/4487044/windows-10-update-kb4487044) installiert ist, wenn Sie Server 2019 verwenden. Azure ATP-Sensoren, die bereits auf Servern mit Windows 2019 ohne dieses Update installiert sind, werden automatisch deaktiviert.
 
Der Azure ATP-Sensor unterstützt die Installation auf einem Domänencontroller mit Windows Server 2008 R2 SP1 (ausgenommen Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (einschließlich Windows Server Core, aber ausgenommen Windows Nano Server), Windows Server 2019 (einschließlich Windows Core, aber ausgenommen Windows Nano Server).

Beim Domänencontroller kann es sich um einen schreibgeschützten Domänencontroller (Read Only Domain Controller, RODC) handeln.

Für die Kommunikation Ihrer Domänencontroller mit dem Clouddienst müssen Sie in Ihrer Firewall und auf Ihrem Proxyserver Port 443 für „*.atp.azure.com“ freigeben.

Während der Installation wird .NET Framework 4.7 installiert und erfordert möglicherweise einen Neustart des Domänencontrollers,wenn ein Neustart bereits aussteht.


> [!NOTE]
> Mindestens 5 GB Speicherplatz auf dem Datenträger wird benötigt, 10 GB wird empfohlen. Dies umfasst den Speicherplatz, der für die Azure ATP-Binärdateien, Azure ATP-Protokolle und Leistungsprotokolle benötigt wird.

### <a name="server-specifications"></a>Serverspezifikationen

Der Azure ATP-Sensor erfordert mindestens 2 Kerne und 6 GB RAM auf dem Domänencontroller.
Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des Azure ATP-Sensors auf **Hohe Leistung** fest.

Der Azure ATP-Sensor kann auf Domänencontrollern verschiedener Auslastungen und Größen bereitgestellt werden, abhängig vom Umfang des Datenverkehrs zwischen den Domänencontrollern und der installierten Ressourcen.

Unter den Windows-Betriebssystemen 2008 R2 und 2012 werden Azure ATP-Sensoren im Modus [Mehrere Prozessorgruppen](https://docs.microsoft.com/windows/win32/procthread/processor-groups) nicht unterstützt. Weitere Informationen über den Modus „Mehrere Prozessorgruppen“ finden Sie unter [Problembehandlung](troubleshooting-atp-known-issues.md##multi-processor-group-mode). 

>[!NOTE] 
> Bei Ausführung als virtueller Computer wird kein dynamischer Arbeitsspeicher und keine andere Speichererweiterungsfunktion unterstützt.

Weitere Informationen zu den Hardwareanforderungen des Azure ATP-Sensors finden Sie unter [Azure ATP-Kapazitätsplanung](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Zeitsynchronisierung

Die Zeitsynchronisierung der Server und Domänencontroller, auf denen der Sensor installiert ist, muss in einem Bereich von fünf Minuten zueinander liegen.

### <a name="network-adapters"></a>Netzwerkadapter

Der Azure ATP-Sensor überwacht den lokalen Datenverkehr auf allen Netzwerkadaptern des Domänencontrollers. <br>
Verwenden Sie nach der Bereitstellung das Azure ATP-Portal, um anzupassen, welche Netzwerkadapter überwacht werden.

Der Sensor wird nicht in Domänencontrollern unter Windows 2008 R2 mit aktivierten Teamvorgängen für Broadcom-Netzwerkadapter unterstützt.

### <a name="ports"></a>Ports
In der folgenden Tabelle sind die Ports aufgeführt, die für den Azure ATP-Sensor mindestens konfiguriert werden müssen:

|Protokoll|Transport|Port|Zu/Von|Richtung|
|------------|-------------|--------|-----------|-------------|
|**Internetports**|||||
|SSL (*.atp.azure.com)|TCP|443|Azure ATP-Clouddienst|Ausgehend|
|**Interne Ports**|||||
|DNS|TCP und UDP|53|DNS-Server|Ausgehend|
|Netlogon (SMB, CIFS, SAM-R)|TCP/UDP|445|Alle Geräte im Netzwerk|Ausgehend|
|Syslog (optional)|TCP/UDP|514, je nach Konfiguration|SIEM-Server|Eingehend|
|RADIUS|UDP|1813|RADIUS|Eingehend|
|

### <a name="windows-event-logs"></a>Windows-Ereignisprotokolle
Die Azure ATP-Erkennung basiert auf den folgenden bestimmten Windows-Ereignisprotokollen, die der Sensor von Ihren Domänencontrollern aus analysiert: 4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045 und 8004. Damit die richtigen Ereignisse überprüft und im Windows-Ereignisprotokoll eingeschlossen werden, benötigen Ihre Domänencontroller die korrekten erweiterten Überwachungsrichtlinieneinstellungen. Weitere Informationen zum Festlegen der richtigen Richtlinien finden Sie unter [Überprüfung der erweiterten Überwachungsrichtlinie von Azure ATP](atp-advanced-audit-policy.md). Um [sicherzustellen, dass das Windows-Ereignis 8004 überwacht wird](configure-windows-event-collection.md##ntlm-authentication-using-windows-event-8004), wie es der Dienst erfordert, überprüfen Sie die [NTLM-Überwachungseinstellungen](https://blogs.technet.microsoft.com/askds/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7/).  


> [!NOTE]
> - Bei Verwendung des Verzeichnisdienst-Benutzerkontos fragt der Sensor mithilfe von SAM-R (Netzwerkanmeldung) Endpunkte in Ihrer Organisation für lokale Administratoren ab, um [den Graph des Lateral-Movement-Pfads](use-case-lateral-movement-path.md) zu erstellen. Weitere Informationen finden Sie unter [Erforderliche Berechtigung für SAM-R konfigurieren](install-atp-step8-samr.md).

## <a name="azure-atp-standalone-sensor-requirements"></a>Voraussetzungen für den eigenständigen Azure ATP-Sensor
In diesem Abschnitt werden die Voraussetzungen für den eigenständigen Azure ATP-Sensor aufgeführt.

### <a name="general"></a>Allgemein
Der eigenständige Azure ATP-Sensor unterstützt die Installation auf einem Server mit Windows Server 2012 R2 oder Windows Server 2016 (einschließlich Server Core).
Der eigenständige Azure ATP-Sensor kann auf einem Server installiert werden, der Mitglied einer Domäne oder Arbeitsgruppe ist.
Der eigenständige Azure ATP-Sensor kann zur Überwachung von Domänencontrollern mit der Domänenfunktionsebene Windows 2003 und höher verwendet werden.

Damit Ihr eigenständiger Sensor mit dem Clouddienst kommunizieren kann, muss in Ihrer Firewall und auf Ihrem Proxyserver Port 443 für „*.atp.azure.com“ freigegeben sein.


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
    > -   Konfigurieren Sie eine statische, nicht routingfähige IP-Adresse (mit der Maske /32) für Ihre Umgebung ohne Standardsensorgateway und ohne DNS-Serveradressen. Beispiel: 10.10.0.10/32. Dadurch wird sichergestellt, dass der Erfassungsnetzwerkadapter die maximale Menge an Datenverkehr erfassen kann und der Verwaltungsnetzwerkadapter zum Senden und Empfangen des erforderlichen Netzwerkdatenverkehrs verwendet wird.

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
|Syslog (optional)|TCP/UDP|514, je nach Konfiguration|SIEM-Server|Eingehend|
|RADIUS|UDP|1813|RADIUS|Eingehend|
|

> [!NOTE]
> - Bei Verwendung des Verzeichnisdienst-Benutzerkontos fragt der Sensor mithilfe von SAM-R (Netzwerkanmeldung) Endpunkte in Ihrer Organisation für lokale Administratoren ab, um [den Graph des Lateral-Movement-Pfads](use-case-lateral-movement-path.md) zu erstellen. Weitere Informationen finden Sie unter [Erforderliche Berechtigung für SAM-R konfigurieren](install-atp-step8-samr.md).


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Azure ATP architecture (Azure ATP-Architektur)](atp-architecture.md)
- [Install Azure ATP (Installieren von Azure ATP)](install-atp-step1.md)
- [Netzwerknamensauflösung](atp-nnr-policy.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)


