---
title: Voraussetzungen für Microsoft Defender for Identity
description: In diesem Artikel werden die Voraussetzungen für eine erfolgreiche Bereitstellung von Microsoft Defender for Identity in Ihrer Umgebung beschrieben.
ms.date: 12/23/2020
ms.topic: overview
ms.openlocfilehash: f0807061c5ea57f063a1f5a4035b7059e1671a7d
ms.sourcegitcommit: e2b4ad613aa171f604ae526f0cba05fe79f4a8cb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2020
ms.locfileid: "97753387"
---
# <a name="product-long-prerequisites"></a>Voraussetzungen für [!INCLUDE [Product long](includes/product-long.md)]

In diesem Artikel werden die Voraussetzungen für eine erfolgreiche Bereitstellung von [!INCLUDE [Product long](includes/product-long.md)] in Ihrer Umgebung beschrieben.

>[!NOTE]
> Informationen zum Planen von Ressourcen und Kapazitäten finden Sie unter [[!INCLUDE [Product short](includes/product-short.md)]-Kapazitätsplanung](capacity-planning.md).

[!INCLUDE [Product short](includes/product-short.md)] besteht aus dem [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst, der aus dem [!INCLUDE [Product short](includes/product-short.md)]-Portal und dem [!INCLUDE [Product short](includes/product-short.md)]-Sensor besteht. Weitere Informationen zu den einzelnen [!INCLUDE [Product short](includes/product-short.md)]-Komponenten finden Sie unter [[!INCLUDE [Product short](includes/product-short.md)]-Architektur](architecture.md).

[!INCLUDE [Product short](includes/product-short.md)] schützt Ihre lokalen Active Directory-Benutzer und/oder Benutzer, die mit Ihrer Azure Active Directory-Instanz synchronisiert sind. Hinweise zum Schutz einer Umgebung, die nur aus AAD-Benutzern besteht, finden Sie unter [AAD Identity Protection](/azure/active-directory/identity-protection/overview).

Zum Erstellen Ihrer [!INCLUDE [Product short](includes/product-short.md)]-Instanz benötigen Sie einen AAD-Mandanten mit mindestens einem globalen Administrator bzw. einem Sicherheitsadministrator. Jede [!INCLUDE [Product short](includes/product-short.md)]-Instanz unterstützt mehrere Active Directory-Gesamtstrukturbegrenzungen und die Gesamtstrukturfunktionsebene (Forest Functional Level, FFL) von Windows 2003 und höher.

Dieser Leitfaden zu Voraussetzungen wird in die folgenden Abschnitte unterteilt, um sicherzustellen, dass Sie über alle erforderlichen Informationen verfügen, die Sie für eine erfolgreiche Bereitstellung von [!INCLUDE [Product short](includes/product-short.md)] benötigen.

[Bevor Sie beginnen:](#before-you-start) In diesem Abschnitt werden die zu sammelnden Informationen aufgeführt sowie Konten und Netzwerkentitäten, die vor Beginn der Installation vorhanden sein sollten.

[[!INCLUDE [Product short](includes/product-short.md)]-Portal:](#azure-atp-portal-requirements) In diesem Abschnitt werden die Browseranforderungen für das [!INCLUDE [Product short](includes/product-short.md)]-Portal erläutert.

[[!INCLUDE [Product short](includes/product-short.md)]-Sensor:](#azure-atp-sensor-requirements) In diesem Abschnitt werden die Hardware- und Softwareanforderungen für den [!INCLUDE [Product short](includes/product-short.md)]-Sensor beschrieben.

[Eigenständiger [!INCLUDE [Product short](includes/product-short.md)]-Sensor:](#azure-atp-standalone-sensor-requirements) Der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor wird auf einem dedizierten Server installiert und erfordert die Konfiguration einer Portspiegelung auf dem Domänencontroller, um Netzwerkdatenverkehr zu empfangen.

> [!NOTE]
> Eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensoren unterstützen keine Erfassung von Protokolleinträgen für die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die Daten für mehrere Erkennungen bereitstellen. Zur vollständigen Erfassung Ihrer Umgebung empfiehlt sich die Bereitstellung des [!INCLUDE [Product short](includes/product-short.md)]-Sensors.

## <a name="before-you-start"></a>Vor der Installation

In diesem Abschnitt werden die Informationen, die Sie erfassen sollten, sowie Konten und Netzwerkinformationen aufgeführt, die vor der Installation von [!INCLUDE [Product short](includes/product-short.md)] vorhanden sein sollten.

- Sie können eine Lizenz für Enterprise Mobility + Security 5 (EMS E5) entweder direkt über das [Microsoft 365-Portal](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) oder über das CSP-Lizenzierungsmodell (Cloud Solution Partner) erwerben. Eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Lizenzen sind ebenfalls verfügbar.

- Stellen Sie sicher, dass die Domänencontroller, auf denen Sie [!INCLUDE [Product short](includes/product-short.md)]-Sensoren installieren möchten, über das Internet mit dem [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst verbunden sind. Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor unterstützt die Verwendung eines Proxys. Weitere Informationen zur Proxykonfiguration finden Sie unter [Konfigurieren eines Proxys für [!INCLUDE [Product short](includes/product-short.md)]](configure-proxy.md).

- Mindestens eines der folgenden Verzeichnisdienstkonten mit Lesezugriff auf alle Objekte in den überwachten Domänen:
  - Ein **standardmäßiges** AD-Benutzerkonto und -Kennwort; erforderlich für Sensoren, die unter Windows Server 2008 R2 SP1 ausgeführt werden.
  - Ein von der **Gruppe verwaltetes Dienstkonto**; erfordert Windows Server 2012 oder höher.  
  Alle Sensoren benötigen Zugriffsberechtigungen zum Abrufen des Kennworts des gruppenverwalteten Dienstkontos.  
  Weitere Informationen zu gruppenverwalteten Dienstkonten finden Sie unter [Erste Schritte mit gruppenverwalteten Dienstkonten](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts#BKMK_CreateGMSA).

    In der folgenden Tabelle ist aufgeführt, welche AD-Benutzerkonten mit welchen Serverversionen verwendet werden können:

    |Kontotyp|Windows Server 2008 R2 SP1|Windows Server 2012 oder höher|
    |---|---|---|
    |**Standardbenutzerkonto** von AD|Ja|Ja|
    |**gruppenverwaltetes Dienstkonto**|Nein|Ja|

    > [!NOTE]
    >
    > - Für Sensorcomputer unter Windows Server 2012 und höher wird empfohlen, ein **gruppenverwaltetes Dienstkonto** für verbesserte Sicherheit und automatische Kennwortverwaltung zu verwenden.
    > - Wenn Sie über mehrere Sensoren verfügen, teilweise unter Windows Server 2008 oder unter Windows Server 2012 und höher, müssen Sie zusätzlich zum empfohlenen **gruppenverwalteten Dienstkonto** auch mindestens ein AD-**Standardbenutzerkonto** verwenden.
    > - Wenn Sie benutzerdefinierte ACLs für verschiedene Organisationseinheiten (OU) in Ihrer Domäne festgelegt haben, stellen Sie sicher, dass der ausgewählte Benutzer Leseberechtigungen für diese Organisationseinheiten hat.

- Wenn Sie Wireshark für einen eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor ausführen, müssen Sie den [!INCLUDE [Product short](includes/product-short.md)]-Sensordienst neu starten, nachdem Sie die Wireshark-Erfassung beendet haben. Wenn Sie den Sensordienst nicht neu starten, beendet der Sensor die Erfassung des Datenverkehrs.

- Wenn Sie versuchen, den [!INCLUDE [Product short](includes/product-short.md)]-Sensor auf einem Computer zu installieren, der mit einem NIC-Teaming-Adapter konfiguriert ist, wird ein Installationsfehler gemeldet. Wenn Sie den [!INCLUDE [Product short](includes/product-short.md)]-Sensor auf einem Computer installieren möchten, der mit einem NIC-Teamvorgang konfiguriert ist, finden Sie weitere Informationen unter [Problem mit NIC-Teamvorgängen beim [!INCLUDE [Product short](includes/product-short.md)]-Sensor](troubleshooting-known-issues.md#nic-teaming).

- Container mit **gelöschten Objekten** – Empfehlung: Der Benutzer sollte über den schreibgeschützten Zugriff auf den Container mit gelöschten Objekten verfügen. Mithilfe von Leseberechtigungen für diesen Container kann [!INCLUDE [Product short](includes/product-short.md)] Löschungen von Benutzern über Ihre Active Directory-Instanz erkennen. Informationen zum Konfigurieren des schreibgeschützten Zugriffs auf den Container mit gelöschten Objekten finden Sie im Abschnitt **Ändern von Berechtigungen für einen Container mit gelöschten Objekten** im Artikel [Anzeigen und Festlegen von Berechtigungen für ein Verzeichnisobjekt](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824(v=ws.10)).

- Optionales **Honeytoken**: Ein Benutzerkonto eines Benutzers ohne Netzwerkaktivitäten. Dieses Konto wird als [!INCLUDE [Product short](includes/product-short.md)]-Honeytoken-Benutzer konfiguriert. Weitere Informationen zu Verwendung von Honeytokens finden Sie unter [Konfigurieren von Ausschlüssen und Honeytoken-Benutzern](install-step7.md).

- Optional: Wenn Sie den eigenständigen Sensor bereitstellen, ist die Weiterleitung der [Windows-Ereignisse](configure-windows-event-collection.md#configure-event-collection) an [!INCLUDE [Product short](includes/product-short.md)] erforderlich, um authentifizierungsbasierte Erkennungen, Ergänzungen vertraulicher Gruppen und Erkennungen der Erstellung verdächtiger Dienste in [!INCLUDE [Product short](includes/product-short.md)] zu verbessern.  Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor empfängt diese Ereignisse automatisch. Im eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor können diese Ereignisse von Ihrer SIEM-Lösung (Security Information & Event Management) empfangen oder durch Festlegen der Windows-Ereignisweiterleitung von Ihrem Domänencontroller aus abgerufen werden. Die erfassten Ereignisse bieten [!INCLUDE [Product short](includes/product-short.md)] zusätzliche Informationen, die über den Netzwerkverkehr des Domänencontrollers nicht verfügbar sind.

<a name="azure-atp-portal-requirements"></a>

## <a name="product-short-portal-requirements"></a>Anforderungen für das [!INCLUDE [Product short](includes/product-short.md)]-Portal

Der Zugriff auf das [!INCLUDE [Product short](includes/product-short.md)]-Portal erfolgt über einen Browser. Folgende Browser und Einstellungen werden unterstützt:

- Ein Browser, der TLS 1.2 unterstützt, z. B.:
  - Microsoft Edge
  - Internet Explorer Version 11 oder höher
  - Google Chrome 30.0 und höher
- Mindestauflösung der Bildschirmbreite: 1.700 Pixel
- Firewall/Proxy geöffnet: Für die Kommunikation mit dem [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst muss Port 443 für „*.atp.azure.com“ in Ihrer Firewall und auf Ihrem Proxyserver geöffnet sein.

    > [!NOTE]
    > Sie können auch das Azure-Diensttag (**AzureAdvancedThreatProtection**) verwenden, um den Zugriff auf [!INCLUDE [Product short](includes/product-short.md)] zu ermöglichen. Weitere Informationen zu Diensttags finden Sie unter [Diensttags des virtuellen Netzwerks](/azure/virtual-network/service-tags-overview) oder in der Datei [Herunterladen der Diensttags](https://www.microsoft.com/download/details.aspx?id=56519).

 ![Diagramm der [!INCLUDE [Product short](includes/product-short.md)]-Architektur](media/architecture-topology.png)

> [!NOTE]
> [!INCLUDE [Product short](includes/product-short.md)] unterstützt standardmäßig bis zu 200 Sensoren. Kontaktieren Sie den [!INCLUDE [Product short](includes/product-short.md)]-Support, wenn Sie mehr Sensoren installieren möchten.

## <a name="product-short-network-name-resolution-nnr-requirements"></a>Anforderungen an die [!INCLUDE [Product short](includes/product-short.md)]-Netzwerknamensauflösung

Die Netzwerknamensauflösung (Network Name Resolution, NNR) ist ein Hauptbestandteil der [!INCLUDE [Product short](includes/product-short.md)]-Funktionalität. Zum Auflösen von IP-Adressen in Computernamen suchen [!INCLUDE [Product short](includes/product-short.md)]-Sensoren die IP-Adressen mithilfe der folgenden Methoden:

- NTLM über RPC (TCP-Port 135)
- NetBIOS (UDP-Port 137)
- RDP (TCP-Port 3389): nur das erste Paket von **ClientHello**
- Abfragen des DNS-Servers mittels Reverse-DNS-Lookup der IP-Adresse (UDP 53)

Damit die ersten drei Methoden funktionieren, müssen die entsprechenden Ports für eingehenden Datenverkehr von den [!INCLUDE [Product short](includes/product-short.md)]-Sensoren zu Geräten im Netzwerk geöffnet sein. Weitere Informationen über [!INCLUDE [Product short](includes/product-short.md)] und die Netzwerknamensauflösung finden Sie unter [Richtlinie für die [!INCLUDE [Product short](includes/product-short.md)]-Netzwerknamensauflösung](nnr-policy.md).

Um die besten Ergebnisse zu erzielen, sollten alle Methoden verwendet werden. Wenn dies nicht möglich ist, sollten Sie die DNS-Suchmethode und mindestens eine der anderen Methoden verwenden.

<a name="azure-atp-sensor-requirements"></a>

## <a name="product-short-sensor-requirements"></a>Voraussetzungen für den [!INCLUDE [Product short](includes/product-short.md)]-Sensor

In diesem Abschnitt werden die Voraussetzungen für [!INCLUDE [Product short](includes/product-short.md)]-Sensoren aufgeführt.

### <a name="general"></a>Allgemein

Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor unterstützt die Installation auf einem Domänencontroller und auf AD FS (Active Directory-Verbunddienste) mit Windows Server 2008 R2 SP1 (ausgenommen Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (einschließlich Server Core, aber ausgenommen Nano Server), Windows Server 2019\* (einschließlich Server Core, aber ausgenommen Nano Server) wie in der folgenden Tabelle gezeigt.

| Betriebssystemversion   | Server mit Desktopumgebung | Server Core | Nano Server    | Unterstützte Installationen  |
| -------------------------- | ------------------------------ | ----------- | -------------- | ------------------------ |
| Windows Server 2008 R2 SP1 | &#10004;                       | &#10060;    | Nicht zutreffend | Domänencontroller        |
| Windows Server 2012        | &#10004;                       | &#10004;    | Nicht zutreffend | Domänencontroller        |
| Windows Server 2012 R2     | &#10004;                       | &#10004;    | Nicht zutreffend | Domänencontroller        |
| Windows Server 2016        | &#10004;                       | &#10004;    | &#10060;       | Domänencontroller und AD FS |
| Windows Server 2019\*      | &#10004;                       | &#10004;    | &#10060;       | Domänencontroller und AD FS |

\* Erfordert [KB4487044](https://support.microsoft.com/help/4487044/windows-10-update-kb4487044) oder ein neueres kumulatives Update. Sensoren, die ohne dieses Update unter Server 2019 installiert sind, werden automatisch beendet, wenn die Dateiversion der Datei *ntdsai.dll* im Systemverzeichnis älter ist als *10.0.17763.316*.

Beim Domänencontroller kann es sich um einen schreibgeschützten Domänencontroller (Read Only Domain Controller, RODC) handeln.

Damit Sensoren, die auf Domänencontrollern und auf AD FS ausgeführt werden, mit dem Clouddienst kommunizieren können, müssen Sie Port 443 Ihrer Firewalls und Proxys für \*.atp.azure.com öffnen.

Falls .NET Framework 4.7 oder höher nicht installiert ist, wird .NET Framework 4.7 während der Installation installiert, und Sie müssen möglicherweise den Server neu starten. Ein Neustart ist möglicherweise auch erforderlich, wenn bereits ein Neustart aussteht.

> [!NOTE]
> Mindestens 5 GB Speicherplatz auf dem Datenträger wird benötigt, 10 GB wird empfohlen. Dies umfasst den Speicherplatz, der für die [!INCLUDE [Product short](includes/product-short.md)]-Binärdateien, [!INCLUDE [Product short](includes/product-short.md)]-Protokolle und Leistungsprotokolle benötigt wird.

### <a name="server-specifications"></a>Serverspezifikationen

Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor erfordert mindestens 2 Kerne und 6 GB RAM auf dem Domänencontroller.
Legen Sie die **Energieoption** des Computers, auf dem die [!INCLUDE [Product short](includes/product-short.md)]-Sensoren ausgeführt werden, auf **Hohe Leistung** fest, um die optimale Leistung zu erzielen.

[!INCLUDE [Product short](includes/product-short.md)]-Sensoren können auf Domänencontrollern oder AD FS-Servern verschiedener Auslastungen und Größen bereitgestellt werden, abhängig vom Umfang des Datenverkehrs zwischen den Servern und von der Menge installierter Ressourcen.

Unter den Windows-Betriebssystemen 2008 R2 und 2012 werden [!INCLUDE [Product short](includes/product-short.md)]-Sensoren im Modus [Multi Processor Group](/windows/win32/procthread/processor-groups) (Mehrere Prozessorgruppen) nicht unterstützt. Weitere Informationen über den Modus „Mehrere Prozessorgruppen“ finden Sie unter [Problembehandlung](troubleshooting-known-issues.md#multi-processor-group-mode).

>[!NOTE]
> Bei Ausführung als virtueller Computer wird kein dynamischer Arbeitsspeicher und keine andere Speichererweiterungsfunktion unterstützt.

Weitere Informationen zu den Hardwareanforderungen für [!INCLUDE [Product short](includes/product-short.md)]-Sensoren finden Sie unter [[!INCLUDE [Product short](includes/product-short.md)]-Kapazitätsplanung](capacity-planning.md).

### <a name="time-synchronization"></a>Zeitsynchronisierung

Die Zeitsynchronisierung der Server und Domänencontroller, auf denen der Sensor installiert ist, muss in einem Bereich von fünf Minuten zueinander liegen.

### <a name="network-adapters"></a>Netzwerkadapter

Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor überwacht den lokalen Datenverkehr auf allen Netzwerkadaptern des Domänencontrollers.  
Verwenden Sie nach der Bereitstellung das [!INCLUDE [Product short](includes/product-short.md)]-Portal, um anzupassen, welche Netzwerkadapter überwacht werden.

Der Sensor wird nicht in Domänencontrollern unter Windows 2008 R2 mit aktivierten Teamvorgängen für Broadcom-Netzwerkadapter unterstützt.

### <a name="ports"></a>Ports

In der folgenden Tabelle werden die Ports aufgeführt, die für den [!INCLUDE [Product short](includes/product-short.md)]-Sensor mindestens konfiguriert werden müssen:

|Protokoll|Transport|Port|Von|Beschreibung|
|------------|-------------|--------|-----------|
|**Internetports**|||||
|SSL (*.atp.azure.com)|TCP|443|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|[!INCLUDE [Product short](includes/product-short.md)]-Clouddienst|
|SSL (localhost)|TCP|444|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|localhost|
|**Interne Ports**|||||
|DNS|TCP und UDP|53|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|DNS-Server|
|Netlogon (SMB, CIFS, SAM-R)|TCP/UDP|445|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|Alle Geräte im Netzwerk|
|RADIUS|UDP|1813|RADIUS|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|
|**NNR-Ports**\*|||||
|NTLM über RPC|TCP|Port 135|[!INCLUDE [Product short](includes/product-short.md)]|Alle Geräte im Netzwerk|
|NetBIOS|UDP|137|[!INCLUDE [Product short](includes/product-short.md)]|Alle Geräte im Netzwerk|
|RDP|TCP|3389, nur das erste Client Hello-Paket|[!INCLUDE [Product short](includes/product-short.md)]|Alle Geräte im Netzwerk|

\* Einer dieser Ports ist erforderlich, aber Sie sollten alle öffnen.

### <a name="windows-event-logs"></a>Windows-Ereignisprotokolle

Die [!INCLUDE [Product short](includes/product-short.md)]-Erkennung basiert auf spezifischen [Windows-Ereignisprotokollen](configure-windows-event-collection.md#configure-event-collection), die der Sensor über Ihre Domänencontroller analysiert. Damit die richtigen Ereignisse überprüft und im Windows-Ereignisprotokoll eingeschlossen werden, benötigen Ihre Domänencontroller die korrekten erweiterten Überwachungsrichtlinieneinstellungen. Weitere Informationen zum Festlegen der richtigen Richtlinien finden Sie unter [Überprüfung der erweiterten Überwachungsrichtlinie von Azure ATP](configure-windows-event-collection.md). Um [sicherzustellen, dass das Windows-Ereignis 8004 überwacht wird](configure-windows-event-collection.md#configure-audit-policies), wie es der Dienst erfordert, überprüfen Sie die [NTLM-Überwachungseinstellungen](/archive/blogs/askds/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7).

Legen Sie für Sensoren, die auf AD FS-Servern ausgeführt werden, die Überwachungsstufe **Verbose** (Ausführlich) fest. Informationen zum Konfigurieren der Überwachungsstufe finden Sie unter [Informationen zur Ereignisüberwachung für AD FS](/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-logging#event-auditing-information-for-ad-fs-on-windows-server-2016).

> [!NOTE]
> Bei Verwendung des Verzeichnisdienst-Benutzerkontos fragt der Sensor mithilfe von SAM-R (Netzwerkanmeldung) Endpunkte in Ihrer Organisation für lokale Administratoren ab, um [den Graph des Lateral-Movement-Pfads](use-case-lateral-movement-path.md) zu erstellen. Weitere Informationen finden Sie unter [Erforderliche Berechtigung für SAM-R konfigurieren](install-step8-samr.md).

<a name="azure-atp-standalone-sensor-requirements"></a>

## <a name="product-short-standalone-sensor-requirements"></a>Voraussetzungen für den eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor

In diesem Abschnitt werden die Voraussetzungen für den eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor aufgeführt.

> [!NOTE]
> Eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensoren unterstützen keine Erfassung von Protokolleinträgen für die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die Daten für mehrere Erkennungen bereitstellen. Zur vollständigen Erfassung Ihrer Umgebung empfiehlt sich die Bereitstellung des [!INCLUDE [Product short](includes/product-short.md)]-Sensors.

### <a name="general"></a>Allgemein

Der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor unterstützt die Installation auf einem Server mit Windows Server 2012 R2 oder Windows Server 2016 (einschließlich Server Core).
Der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor kann auf einem Server installiert werden, der Mitglied einer Domäne oder Arbeitsgruppe ist.
Der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor kann zur Überwachung von Domänencontrollern mit der Domänenfunktionsebene Windows 2003 und höher verwendet werden.

Damit Ihr eigenständiger Sensor mit dem Clouddienst kommunizieren kann, muss in Ihrer Firewall und auf Ihrem Proxyserver Port 443 für „*.atp.azure.com“ freigegeben sein.

Informationen zur Verwendung von virtuellen Computern mit dem eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor finden Sie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md).

> [!NOTE]
> Mindestens 5 GB Speicherplatz auf dem Datenträger wird benötigt, 10 GB wird empfohlen. Dies umfasst den Speicherplatz, der für die [!INCLUDE [Product short](includes/product-short.md)]-Binärdateien, [!INCLUDE [Product short](includes/product-short.md)]-Protokolle und Leistungsprotokolle benötigt wird.

### <a name="server-specifications"></a>Serverspezifikationen

Legen Sie die **Energieoption** des Computers, auf dem der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor ausgeführt wird, auf **Hohe Leistung** fest, um die optimale Leistung zu erzielen.

Ein eigenständiger [!INCLUDE [Product short](includes/product-short.md)]-Sensor kann die Überwachung von mehreren Domänencontrollern unterstützen, abhängig vom Umfang des Datenverkehrs zwischen den Domänencontrollern.

>[!NOTE]
> Bei Ausführung als virtueller Computer wird kein dynamischer Arbeitsspeicher und keine andere Speichererweiterungsfunktion unterstützt.

Weitere Informationen zu den Hardwareanforderungen für eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensoren finden Sie unter [[!INCLUDE [Product short](includes/product-short.md)]-Kapazitätsplanung](capacity-planning.md).

### <a name="time-synchronization"></a>Zeitsynchronisierung

Die Zeitsynchronisierung der Server und Domänencontroller, auf denen der Sensor installiert ist, muss in einem Bereich von fünf Minuten zueinander liegen.

### <a name="network-adapters"></a>Netzwerkadapter

Der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor erfordert mindestens einen Verwaltungsadapter und einen Erfassungsadapter:

- **Verwaltungsadapter:** wird für die Kommunikation im Unternehmensnetzwerk verwendet. Der Sensor nutzt diesen Adapter zum Abfragen des Domänencontrollers, den er schützt, und für Korrekturen an Computerkonten.

    Dieser Adapter sollte mit den folgenden Einstellungen konfiguriert werden:

    - Statische IP-Adresse, einschließlich des Standardgateways

    - Bevorzugte und alternative DNS-Server

    - Das **DNS-Suffix für diese Verbindung** sollte der DNS-Name der Domäne für jede Domäne sein, die überwacht wird.

        ![Konfigurieren Sie das DNS-Suffix in den erweiterten TCP/IP-Einstellungen.](media/dns-suffix.png)

        > [!NOTE]
        > Wenn der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor Mitglied der Domäne ist, erfolgt diese Konfiguration möglicherweise automatisch.

- **Erfassungsadapter**: wird verwendet, um den Datenverkehr zu und von den Domänencontrollern zu erfassen.

    > [!IMPORTANT]
    >
    > - Konfigurieren Sie die Portspiegelung für den Erfassungsadapter als Ziel des Domänencontroller-Netzwerkdatenverkehrs. Weitere Informationen finden Sie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md). In der Regel müssen Sie mit dem Netzwerk- oder Virtualisierungsteam zusammenarbeiten, um die Portspiegelung zu konfigurieren.
    > - Konfigurieren Sie eine statische, nicht routingfähige IP-Adresse (mit der Maske /32) für Ihre Umgebung ohne Standardsensorgateway und ohne DNS-Serveradressen. Beispiel: 10.10.0.10/32. Dadurch wird sichergestellt, dass der Erfassungsnetzwerkadapter die maximale Menge an Datenverkehr erfassen kann und der Verwaltungsnetzwerkadapter zum Senden und Empfangen des erforderlichen Netzwerkdatenverkehrs verwendet wird.

### <a name="ports"></a>Ports

In der folgenden Tabelle werden die Ports aufgeführt, die für den Verwaltungsadapter des eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensors mindestens konfiguriert werden müssen:

|Protokoll|Transport|Port|Von|Beschreibung|
|------------|-------------|--------|-----------|
|**Internetports**||||
|SSL (*.atp.azure.com)|TCP|443|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|[!INCLUDE [Product short](includes/product-short.md)]-Clouddienst|
|SSL (localhost)|TCP|444|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|localhost|
|**Interne Ports**||||
|LDAP|TCP und UDP|389|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|Domänencontroller|
|Sicheres LDAP (LDAPS)|TCP|636|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|Domänencontroller|
|LDAP an globalen Katalog|TCP|3268|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|Domänencontroller|
|LDAPs an globalen Katalog|TCP|3269|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|Domänencontroller|
|Kerberos|TCP und UDP|88|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|Domänencontroller|
|Netlogon (SMB, CIFS, SAM-R)|TCP und UDP|445|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|Alle Geräte im Netzwerk|
|Windows-Zeitdienst|UDP|123|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|Domänencontroller|
|DNS|TCP und UDP|53|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|DNS-Server|
|Syslog (optional)|TCP/UDP|514, je nach Konfiguration|SIEM-Server|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|
|RADIUS|UDP|1813|RADIUS|[!INCLUDE [Product short](includes/product-short.md)]-Sensor|
|**NNR-Ports** \*|||||
|NTLM über RPC|TCP|135|[!INCLUDE [Product short](includes/product-short.md)]|Alle Geräte im Netzwerk|
|NetBIOS|UDP|137|[!INCLUDE [Product short](includes/product-short.md)]|Alle Geräte im Netzwerk|
|RDP|TCP|3389, nur das erste Client Hello-Paket|[!INCLUDE [Product short](includes/product-short.md)]|Alle Geräte im Netzwerk|

\* Einer dieser Ports ist erforderlich, aber Sie sollten alle öffnen.

> [!NOTE]
>
> - Bei Verwendung des Verzeichnisdienst-Benutzerkontos fragt der Sensor mithilfe von SAM-R (Netzwerkanmeldung) Endpunkte in Ihrer Organisation für lokale Administratoren ab, um [den Graph des Lateral-Movement-Pfads](use-case-lateral-movement-path.md) zu erstellen. Weitere Informationen finden Sie unter [Erforderliche Berechtigung für SAM-R konfigurieren](install-step8-samr.md).

## <a name="see-also"></a>Weitere Informationen

- [[!INCLUDE [Product short](includes/product-short.md)]-Tool zur Größenanpassung](https://aka.ms/aatpsizingtool)
- [[!INCLUDE [Product short](includes/product-short.md)]-Architektur](architecture.md)
- [Installieren von [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Netzwerknamensauflösung](nnr-policy.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
