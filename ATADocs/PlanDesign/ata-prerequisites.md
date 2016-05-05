---
# required metadata

title: ATA-Voraussetzungen | Microsoft Advanced Threat Analytics
description: Beschreibt die Voraussetzungen für eine erfolgreiche Bereitstellung von ATA in Ihrer Umgebung.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA-Voraussetzungen
Dieser Artikel beschreibt die Voraussetzungen für eine erfolgreiche Bereitstellung von ATA in Ihrer Umgebung.

ATA besteht aus zwei Komponenten: ATA Center und ATA-Gateway. Weitere Informationen zu ATA-Komponenten finden Sie unter [ATA-Architektur](/advanced-threat-analytics/Understand/ata-architecture).

[Vorbereitung](#before-you-start): In diesem Abschnitt werden die Informationen aufgeführt, die Sie sammeln sollten, sowie Konten und Netzwerkentitäten genannt, die vor der ATA-Installation vorhanden sein sollten.

[ATA Center](#ata-center-requirements): In diesem Abschnitt werden die Hardware- und Softwarevoraussetzungen für ATA Center sowie die Einstellungen aufgeführt, die Sie für den ATA Center-Server konfigurieren müssen.

[ATA-Gateway](#ata-gateway-requirements): In diesem Abschnitt werden die Hardware- und Softwarevoraussetzungen für das ATA-Gateway sowie die Einstellungen aufgeführt, die Sie für die ATA-Gatewayserver konfigurieren müssen.

[ATA-Konsole](#ata-console): In diesem Abschnitt werden die Browseranforderungen für die Ausführung der ATA-Konsole aufgeführt.

![ATA-Architekturdiagramm](media/ATA-architecture-topology.jpg)

## Vorbereitung
In diesem Abschnitt werden die Informationen aufgeführt, die Sie sammeln sollten, sowie Konten und Netzwerkentitäten genannt, die vor der ATA-Installation vorhanden sein sollten.

-   **Domänencontroller** unter Windows Server 2008 und höher.

-   **Benutzerkonto und -kennwort** mit Lesezugriff auf **alle Objekte** in den Domänen, die überwacht werden.

    > [!NOTE]
    > Wenn Sie benutzerdefinierte ACLs für verschiedene Organisationseinheiten in Ihrer Domäne festgelegt haben, stellen Sie sicher, dass der ausgewählte Benutzer Leseberechtigungen für diese Organisationseinheiten hat.

    Optional: Der Benutzer sollte über den schreibgeschützten Zugriff auf den Container mit gelöschten Objekten verfügen. Dadurch wird es ATA ermöglicht, die Massenlöschung von Objekten in der Domäne zu erkennen. Weitere Informationen zum Konfigurieren des schreibgeschützten Zugriffs auf den Container mit gelöschten Objekten finden Sie im Abschnitt **Ändern von Berechtigungen für einen Container mit gelöschten Objekten** im Thema [Anzeigen und Festlegen von Berechtigungen für ein Verzeichnisobjekt](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Optional: Ein Benutzerkonto eines Benutzers ohne Netzwerkaktivitäten. Dieses Konto wird als ATA-Honeytoken-Benutzer konfiguriert. Zum Konfigurieren des Honeytoken-Benutzers benötigen Sie die SID des Benutzerkontos und nicht den Benutzernamen.

-   Optional: Zusätzlich zum Sammeln und Analysieren des Netzwerkverkehrs zu und von den Domänencontrollern kann ATA das Windows-Ereignis 4776 heranziehen, um die ATA-Erkennung von Pass-the-Hash weiter zu verbessern. Dies kann aus der SIEM heraus erfolgen, oder indem Sie die Windows-Ereignisweiterleitung von Ihrem Domänencontroller aus einrichten. Die gesammelten Ereignisse versorgen ATA mit zusätzlichen Informationen, die nicht über den Netzwerkdatenverkehr des Domänencontrollers verfügbar sind.

-   Möglicherweise empfiehlt es sich, eine Liste aller Subnetze in Ihrem Netzwerk für VPN und WLAN zu erstellen, die IP-Adressen zwischen Geräten innerhalb eines sehr kurzen Zeitraums (Sekunden oder Minuten) neu zuordnen.  Sie sollten diese Subnetze mit kurzer Leasedauer angeben, damit ATA ihre Cachelebensdauer verringern kann, um die schnelle Neuzuordnung zwischen Geräten zu ermöglichen. Weitere Informationen zur Konfiguration von Subnetzen mit kurzer Leasedauer finden Sie unter [Installieren von ATA](/advanced-threat-analytics/DeployUse/install-ata).

## Voraussetzungen für ATA Center
In diesem Abschnitt werden die Voraussetzungen für ATA Center aufgeführt.

ATA Center unterstützt die Installation auf einem Server mit Windows Server 2012 R2. Führen Sie Windows Update aus, und stellen Sie sicher, dass alle wichtigen Updates installiert sind.
 Die Hardwareanforderungen hängen von der Anzahl der Domänencontroller, die überwacht werden, und der Auslastung der einzelnen Domänencontroller ab.

Die Installation von ATA Center als virtueller Computer wird unterstützt. Weitere Informationen finden Sie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md).

Wenn Sie ATA Center als virtuellen Computer ausführen, fahren Sie vor dem Erstellen eines neuen Prüfpunkts den Server herunter, um eine potenzielle Beschädigung der Datenbank zu verhindern.

> [!NOTE]
> - ATA Center kann auf einem Server installiert werden, der Mitglied einer Domäne oder Arbeitsgruppe ist.
>
> - Für die Analyse des Benutzerverhaltens benötigt ATA Center die Daten von mindestens 21 Tagen.
>
> - Weitere Informationen zu den Hardwareanforderungen finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).


### Zeitsynchronisierung
Die Zeitsynchronisierung des ATA Center-Servers, der ATA-Gatewayserver und der Domänencontroller muss in einem Bereich von 5 Minuten zueinander liegen.

### BIOS-Einstellungen
Die ATA-Datenbank erfordert, dass Sie den nicht einheitlichen Speicherzugriff (NUMA) im BIOS **deaktivieren**. Das System bezieht sich möglicherweise als Knotenüberlappung auf NUMA. In diesem Fall müssen Sie die Knotenüberlappung **aktivieren**. Weitere Informationen finden Sie in der BIOS-Dokumentation.

### Netzwerkadapter
Anforderungen:

-   Ein Netzwerkadapter

-   Zwei IP-Adressen

Die Kommunikation zwischen ATA Center und dem ATA-Gateway wird mithilfe von SSL über Port 443 verschlüsselt. Darüber hinaus wird die ATA-Konsole unter IIS ausgeführt und mithilfe von SSL über Port 443 gesichert. **Zwei IP-Adressen** werden empfohlen. Der ATA Center-Dienst verbindet Port 443 mit der ersten IP-Adresse, und IIS verbindet Port 443 mit der zweiten IP-Adresse.

> [!NOTE]
> Eine einzelne IP-Adresse mit zwei verschiedenen Ports kann zwar verwendet werden, es werden jedoch zwei IP-Adressen empfohlen.

### Ports
In der folgenden Tabelle sind die Ports aufgelistet, die mindestens geöffnet werden müssen, damit ATA Center ordnungsgemäß funktioniert.

In dieser Tabelle ist die IP-Adresse 1 an den ATA Center-Dienst gebunden, und die IP-Adresse 2 ist an den IIS-Dienst für die ATA-Konsole gebunden.

|Protokoll|Transport|Port|Zu/Von|Richtung|IP-Adresse|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL** (ATA-Kommunikation)|TCP|443 oder konfigurierbar|ATA-Gateway|Eingehend|IP-Adresse 1|
|**HTTP**|TCP|80|Unternehmensnetzwerk|Eingehend|IP-Adresse 2|
|**HTTPS**|TCP|443|Unternehmensnetzwerk und ATA-Gateway|Eingehend|IP-Adresse 2|
|**SMTP** (optional)|TCP|25|SMTP-Server|Ausgehend|IP-Adresse 2|
|**SMTPS** (optional)|TCP|465|SMTP-Server|Ausgehend|IP-Adresse 2|
|**Syslog** (optional)|TCP|514|Syslog-Server|Ausgehend|IP-Adresse 2|

### Zertifikate
Stellen Sie sicher, dass die ATA-Gateways Zugriff auf den CRL-Verteilungspunkt haben. Wenn die ATA-Gateways keinen Zugriff auf das Internet haben, führen Sie [das Verfahren zum manuellen Importieren einer Zertifikatsperrliste](https://technet.microsoft.com/en-us/library/aa996972%28v=exchg.65%29.aspx) durch. Achten Sie dabei darauf, alle CRL-Verteilungspunkte für die gesamte Kette zu installieren.

Um die Installation von ATA Center zu erleichtern, können Sie während dieser Installation selbstsignierte Zertifikate installieren. Nach der Bereitstellung können Sie die selbstsignierten Zertifikate durch ein Zertifikat einer internen Zertifizierungsstelle ersetzen, das vom ATA-Gateway verwendet werden soll.

> [!NOTE]
> Selbstsignierte Zertifikate sollten nur für die Testbereitstellung verwendet werden.

ATA Center erfordert Zertifikate für die folgenden Dienste:

-   Internetinformationsdienste (Internet Information Services, IIS) – Webserverzertifikat

-   ATA Center-Dienst – Serverauthentifizierungszertifikat

> [!NOTE]
> Wenn Sie von anderen Computern aus auf die ATA-Konsole zugreifen werden, stellen Sie sicher, dass diese Computer dem von IIS verwendeten Zertifikat vertrauen. Andernfalls wird auf einer Warnseite die Meldung angezeigt, dass ein Problem mit dem Sicherheitszertifikat der Website vorliegt, bevor die Anmeldeseite geöffnet wird.

## Voraussetzungen für das ATA-Gateway
Das ATA-Gateway unterstützt die Installation auf einem Server mit Windows Server 2012 R2.

Führen Sie Windows Update aus, und stellen Sie sicher, dass alle **wichtigen** Updates installiert sind.
Vergewissern Sie sich vor der Installation des ATA-Gateways, dass das folgende Update installiert wurde: [KB2919355](https://support.microsoft.com/en-us/kb/2919355/).

Dies können Sie überprüfen, indem Sie das folgende Windows PowerShell-Cmdlet ausführen: `[Get-HotFix -Id kb2919355]`.

> [!NOTE]
> -   Das ATA-Gateway kann auf einem Server installiert werden, der Mitglied einer Domäne oder Arbeitsgruppe ist.
> -   Das ATA-Gateway kann nicht auf einem Domänencontroller installiert werden.

Informationen zur Verwendung von virtuellen Computern mit dem ATA-Gateway finden Sie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md).

> [!NOTE]
> Wenn Sie das ATA-Gateway als virtuellen Computer ausführen, fahren Sie vor dem Erstellen eines neuen Prüfpunkts den Server herunter, um eine potenzielle Beschädigung der Datenbank zu verhindern.

Ein ATA-Gateway kann die Überwachung von mehreren Domänencontrollern unterstützen, abhängig vom Umfang des Netzwerkverkehrs zu und von den Domänencontrollern.
Weitere Informationen finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).

### Energieeinstellungen
Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des ATA-Gateways auf **Hohe Leistung** fest.

### Zeitsynchronisierung
Die Zeitsynchronisierung des ATA Center-Servers und des ATA-Gatewayservers muss in einem Bereich von 5 Minuten zueinander liegen.

Zudem muss die Zeitsynchronisierung des ATA-Gateways und der Domänencontroller, mit denen er verbunden wird, in einem Bereich von 5 Minuten zueinander liegen.

### Netzwerkadapter
Das ATA-Gateway erfordert mindestens einen Verwaltungsadapter und mindestens einen Erfassungsadapter:

-   **Verwaltungsadapter** – wird für die Kommunikation im Unternehmensnetzwerk verwendet. Dieser Adapter sollte wie folgt konfiguriert werden:

    -   Statische IP-Adresse, einschließlich des Standardgateways

    -   Bevorzugte und alternative DNS-Server

    -   Das **DNS-Suffix für diese Verbindung** sollte der DNS-Name der Domäne für jede Domäne sein, die überwacht wird.

        ![Konfigurieren Sie das DNS-Suffix in den erweiterten TCP/IP-Einstellungen.](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Wenn das ATA-Gateway Mitglied der Domäne ist, erfolgt diese Konfiguration automatisch.

-   **Erfassungsadapter** – wird verwendet, um den Datenverkehr zu und von den Domänencontrollern zu erfassen.

    > [!IMPORTANT]
    > -   Konfigurieren Sie die Portspiegelung für den Erfassungsadapter als Ziel des Domänencontroller-Netzwerkdatenverkehrs. Weitere Informationen finden Sie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md). In der Regel müssen Sie mit dem Netzwerk- oder Virtualisierungsteam zusammenarbeiten, um die Portspiegelung zu konfigurieren.
    > -   Konfigurieren Sie eine statische, nicht routingfähige IP-Adresse für Ihre Umgebung ohne Standardgateway und ohne DNS-Serveradressen. Beispiel: 1.1.1.1/32. Dadurch wird sichergestellt, dass der Erfassungsnetzwerkadapter die maximale Menge an Datenverkehr erfassen kann und der Verwaltungsnetzwerkadapter zum Senden und Empfangen des erforderlichen Netzwerkdatenverkehrs verwendet wird.

### Ports
In der folgenden Tabelle werden die Ports aufgeführt, die für den Verwaltungsadapter des ATA-Gateways mindestens konfiguriert werden müssen.

|Protokoll|Transport|Port|Zu/Von|Richtung|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP und UDP|389|Domänencontroller|Ausgehend|
|Sicheres LDAP (LDAPS)|TCP|636|Domänencontroller|Ausgehend|
|LDAP für globalen Katalog|TCP|3268|Domänencontroller|Ausgehend|
|LDAPS für globalen Katalog|TCP|3269|Domänencontroller|Ausgehend|
|Kerberos|TCP und UDP|88|Domänencontroller|Ausgehend|
|Netlogon|TCP und UDP|445|Domänencontroller|Ausgehend|
|Windows-Zeitdienst|UDP|123|Domänencontroller|Ausgehend|
|DNS|TCP und UDP|53|DNS-Server|Ausgehend|
|NTLM über RPC|TCP|135|Alle Geräte im Netzwerk|Ausgehend|
|NetBIOS|UDP|137|Alle Geräte im Netzwerk|Ausgehend|
|SSL|TCP|443 oder wie für den Center-Dienst konfiguriert,|ATA Center:<br /><br />-   IP-Adresse des Center-Diensts<br />-   IIS-IP-Adresse|Ausgehend|
|Syslog (optional)|UDP|514|SIEM-Server|Eingehend|

> [!NOTE]
> Als Teil des vom ATA-Gateway durchgeführten Auflösungsprozesses müssen die folgenden eingehenden Ports für Geräte im Netzwerk geöffnet werden.
>
> -   NTLM über RPC
> -   NetBIOS

### Zertifikate
Um die Installation von ATA Center zu erleichtern, können Sie während dieser Installation selbstsignierte Zertifikate installieren. Nach der Bereitstellung können Sie die selbstsignierten Zertifikate durch ein Zertifikat einer internen Zertifizierungsstelle ersetzen, das vom ATA-Gateway verwendet werden soll.

> [!NOTE]
> Selbstsignierte Zertifikate sollten nur für die Testbereitstellung verwendet werden.

Im lokalen Computerspeicher des ATA-Gateways muss ein Zertifikat installiert werden, das die **Serverauthentifizierung** unterstützt. Dieses Zertifikat muss für ATA Center vertrauenswürdig sein.

## ATA-Konsole
Der Zugriff auf die ATA-Konsole erfolgt über einen Browser. Folgende Browser werden unterstützt:

-   Internet Explorer Version 10 oder höher

-   Google Chrome 40 und höher

-   Mindestauflösung der Bildschirmbreite: 1700 Pixel

## Siehe auch
- [ATA-Architektur](/advanced-threat-analytics/Understand/ata-architecture)
- [Installieren von ATA](/advanced-threat-analytics/DeployUse/install-ata)
- [Unterstützung finden Sie in unserem Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


