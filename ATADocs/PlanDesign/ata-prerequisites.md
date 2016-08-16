---
title: ATA-Voraussetzungen | Microsoft ATA
description: "Beschreibt die Voraussetzungen für eine erfolgreiche Bereitstellung von ATA in Ihrer Umgebung."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 87891f6ad683ed9536d3d3f27449feac9bd9dee1


---

# ATA-Voraussetzungen
Dieser Artikel beschreibt die Voraussetzungen für eine erfolgreiche Bereitstellung von ATA in Ihrer Umgebung.

>[!NOTE]
> Informationen zum Planen von Ressourcen und Kapazitäten finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).


ATA besteht aus ATA Center, dem ATA-Gateway und/oder dem ATA-Lightweight-Gateway. Weitere Informationen zu den ATA-Komponenten finden Sie unter [ATA-Architektur](ata-architecture.md).


[Vorbereitung:](#before-you-start) In diesem Abschnitt werden die Informationen aufgeführt, die Sie sammeln sollten, und Konten und Netzwerkentitäten genannt, die vor der ATA-Installation vorhanden sein sollten.

[ATA Center:](#ata-center-requirements) In diesem Abschnitt werden die Hardware- und Softwarevoraussetzungen für ATA Center sowie die Einstellungen aufgeführt, die Sie für den ATA Center-Server konfigurieren müssen.

[ATA-Gateway:](#ata-gateway-requirements) In diesem Abschnitt werden die Hardware- und Softwarevoraussetzungen für das ATA-Gateway sowie die Einstellungen aufgeführt, die Sie für die ATA-Gatewayserver konfigurieren müssen.

[ATA-Lightweight-Gateway:](#ata-lightweight-gateway-requirements) In diesem Abschnitt sind die Hardware- und Softwareanforderungen für das ATA-Lightweight-Gateway aufgeführt.

[ATA-Konsole:](#ata-console) In diesem Abschnitt werden die Browseranforderungen für die Ausführung der ATA-Konsole aufgeführt.

![ATA-Architekturdiagramm](media/ATA-architecture-topology.jpg)

## Vorbereitung
In diesem Abschnitt werden die Informationen aufgeführt, die Sie sammeln sollten, und Konten und Netzwerkentitäten genannt, die vor der ATA-Installation vorhanden sein sollten.


-   Benutzerkonto und -kennwort mit Lesezugriff auf alle Objekte in den Domänen, die überwacht werden.

    > [!NOTE]
    > Wenn Sie benutzerdefinierte ACLs für verschiedene Organisationseinheiten (OU) in Ihrer Domäne festgelegt haben, stellen Sie sicher, dass der ausgewählte Benutzer Leseberechtigungen für diese Organisationseinheiten hat.

-   Erstellen Sie eine Liste aller Subnetze in Ihrem Netzwerk für VPN und WLAN, die IP-Adressen zwischen Geräten innerhalb eines sehr kurzen Zeitraums (Sekunden oder Minuten) neu zuordnen.  Sie sollten diese Subnetze mit kurzer Leasedauer angeben, damit ATA ihre Cachelebensdauer verringern kann, um die schnelle Neuzuordnung zwischen Geräten zu ermöglichen. Weitere Informationen zur Konfiguration von Subnetzen mit kurzer Leasedauer finden Sie unter [Installieren von ATA](/advanced-threat-analytics/deploy-use/install-ata).
-   Stellen Sie sicher, dass die Nachrichtenanalyse und Wireshark nicht auf dem ATA-Gateway oder in ATA Center installiert sind.
-    Optional: Der Benutzer sollte über den schreibgeschützten Zugriff auf den Container mit gelöschten Objekten verfügen. Dadurch wird es ATA ermöglicht, die Massenlöschung von Objekten in der Domäne zu erkennen. Weitere Informationen zum Konfigurieren des schreibgeschützten Zugriffs auf den Container für gelöschte Objekte finden Sie im Abschnitt **Changing permissions on a deleted object container** (Ändern von Berechtigungen für einen Container mit gelöschten Objekten) im Thema [View or Set Permissions on a Directory Object](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) (Anzeigen und Festlegen von Berechtigungen für ein Verzeichnisobjekt).

-   Optional: ein Benutzerkonto eines Benutzers ohne Netzwerkaktivitäten. Dieses Konto wird als ATA-Honeytoken-Benutzer konfiguriert. Zum Konfigurieren des Honeytoken-Benutzers benötigen Sie die SID des Benutzerkontos und nicht den Benutzernamen.

-   Optional: Zusätzlich zum Sammeln und Analysieren des Netzwerkverkehrs zu und von den Domänencontrollern kann ATA das Windows-Ereignis 4776 heranziehen, um die ATA-Erkennung von Pass-the-Hash weiter zu verbessern. Dies kann aus der SIEM heraus erfolgen oder indem Sie die Windows-Ereignisweiterleitung von Ihrem Domänencontroller aus einrichten. Die gesammelten Ereignisse versorgen ATA mit zusätzlichen Informationen, die nicht über den Netzwerkverkehr des Domänencontrollers verfügbar sind.


## Voraussetzungen für ATA Center
In diesem Abschnitt werden die Voraussetzungen für ATA Center aufgeführt.
### Allgemein
ATA Center unterstützt die Installation auf einem Server mit Windows Server 2012 R2. ATA Center kann auf einem Server installiert werden, der Mitglied einer Domäne oder Arbeitsgruppe ist.

Vergewissern Sie sich vor der Installation von ATA Center, dass das folgende Update installiert wurde: [KB2919355](https://support.microsoft.com/kb/2919355/).

Dies können Sie überprüfen, indem Sie das folgende Windows PowerShell-Cmdlet ausführen: `[Get-HotFix -Id kb2919355]`.

Die Installation von ATA Center als virtueller Computer wird unterstützt. 

Wenn Sie ATA Center als virtuellen Computer ausführen, fahren Sie vor dem Erstellen eines neuen Prüfpunkts den Server herunter, um eine mögliche Beschädigung der Datenbank zu verhindern.
### Serverspezifikationen
Wenn Sie auf einem physischen Server arbeiten, erfordert die ATA-Datenbank, dass Sie den nicht einheitlichen Speicherzugriff (Non-Uniform Memory Access, NUMA) im BIOS **deaktivieren**. Das System bezieht sich möglicherweise als Knotenüberlappung auf NUMA. In diesem Fall müssen Sie die Knotenüberlappung **aktivieren**, um NUMA zu deaktivieren. Weitere Informationen finden Sie in der BIOS-Dokumentation. Beachten Sie, dass dies nicht relevant ist, wenn ATA Center auf einem virtuellen Server ausgeführt wird.<br>
Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** von ATA Center auf **Hohe Leistung** fest.<br>
Die erforderlichen Serverspezifikationen hängen von der Anzahl der überwachten Domänencontroller und der Auslastung der einzelnen Domänencontroller ab. Weitere Informationen finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).

>[!NOTE] 
> Bei Ausführung als virtueller Computer wird kein dynamischer Arbeitsspeicher und keine andere Speichererweiterungsfunktion unterstützt.

### Zeitsynchronisierung
Die Zeitsynchronisierung des ATA Center-Servers, der ATA-Gatewayserver und der Domänencontroller muss in einem Bereich von 5 Minuten zueinander liegen.


### Netzwerkadapter
Sie benötigen Folgendes:
-   Mindestens einen Netzwerkadapter.

-   Zwei IP-Adressen (empfohlen aber nicht erforderlich)

Die Kommunikation zwischen ATA Center und dem ATA-Gateway wird mithilfe von SSL über Port 443 verschlüsselt. Darüber hinaus wird die ATA-Konsole unter IIS ausgeführt und mithilfe von SSL über Port 443 gesichert. **Zwei IP-Adressen** werden empfohlen. Der ATA Center-Dienst verbindet Port 443 mit der ersten IP-Adresse, und IIS verbindet Port 443 mit der zweiten IP-Adresse.

> [!NOTE]
> Es kann zwar eine einzelne IP-Adresse mit zwei verschiedenen Ports verwendet werden, zwei IP-Adressen werden jedoch empfohlen.

### Ports
In der folgenden Tabelle sind die Ports aufgelistet, die mindestens geöffnet werden müssen, damit ATA Center ordnungsgemäß funktioniert.

In dieser Tabelle ist IP-Adresse 1 an den ATA Center-Dienst gebunden, und IP-Adresse 2 ist an den IIS-Dienst für die ATA-Konsole gebunden:

|Protokoll|Transport|Port|Zu/Von|Richtung|IP-Adresse|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL** (ATA-Kommunikation)|TCP|443 oder konfigurierbar|ATA-Gateway|Eingehend|IP-Adresse 1|
|**HTTP**|TCP|80|Unternehmensnetzwerk|Eingehend|IP-Adresse 2|
|**HTTPS**|TCP|443|Unternehmensnetzwerk und ATA-Gateway|Eingehend|IP-Adresse 2|
|**SMTP** (optional)|TCP|25|SMTP-Server|Ausgehend|IP-Adresse 2|
|**SMTPS** (optional)|TCP|465|SMTP-Server|Ausgehend|IP-Adresse 2|
|**Syslog** (optional)|TCP|514|Syslog-Server|Ausgehend|IP-Adresse 2|

### Zertifikate
Stellen Sie sicher, dass ATA Center Zugriff auf den CRL-Verteilungspunkt hat. Wenn die ATA-Gateways keinen Zugriff auf das Internet haben, führen Sie [das Verfahren zum manuellen Importieren einer Zertifikatsperrliste](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx) durch. Achten Sie dabei darauf, alle CRL-Verteilungspunkte für die gesamte Kette zu installieren.

Um die Installation von ATA Center zu erleichtern, können Sie während dieser Installation selbstsignierte Zertifikate installieren. Nach der Bereitstellung können Sie die selbstsignierten Zertifikate durch ein Zertifikat einer internen Zertifizierungsstelle ersetzen, das vom ATA-Gateway verwendet werden soll.<br>
> [!NOTE]
> Der Anbietertyp des Zertifikats muss „Kryptografiedienstanbieter (CSP)“ sein.


ATA Center erfordert Zertifikate für die folgenden Dienste:

-   Internetinformationsdienste (IIS) – Webserverzertifikat

-   ATA Center-Dienst – Serverauthentifizierungszertifikat

> [!NOTE]
> Wenn Sie von anderen Computern aus auf die ATA-Konsole zugreifen werden, stellen Sie sicher, dass diese Computer dem von IIS verwendeten Zertifikat vertrauen. Andernfalls wird auf einer Warnseite die Meldung angezeigt, dass ein Problem mit dem Sicherheitszertifikat der Website vorliegt, bevor die Anmeldeseite geöffnet wird.

## Voraussetzungen für das ATA-Gateway
In diesem Abschnitt sind die Voraussetzungen für das ATA-Gateway aufgeführt.
### Allgemein
Das ATA-Gateway unterstützt die Installation auf einem Server mit Windows Server 2012 R2.
Das ATA-Gateway kann auf einem Server installiert werden, der Mitglied einer Domäne oder Arbeitsgruppe ist.

Vergewissern Sie sich vor der Installation des ATA-Gateways, dass das folgende Update installiert wurde: [KB2919355](https://support.microsoft.com/kb/2919355/).

Dies können Sie überprüfen, indem Sie das folgende Windows PowerShell-Cmdlet ausführen: `[Get-HotFix -Id kb2919355]`.

Informationen zur Verwendung von virtuellen Computern mit dem ATA-Gateway finden Sie unter [Konfigurieren der Portspiegelung](/advanced-threat-analytics/deploy-use/configure-port-mirroring).

### Serverspezifikationen
Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des ATA-Gateways auf **Hohe Leistung** fest.<br>
Ein ATA-Gateway kann die Überwachung von mehreren Domänencontrollern unterstützen, abhängig vom Umfang des Netzwerkverkehrs zu und von den Domänencontrollern.

>[!NOTE] 
> Bei Ausführung als virtueller Computer wird kein dynamischer Arbeitsspeicher und keine andere Speichererweiterungsfunktion unterstützt.

### Zeitsynchronisierung
Die Zeitsynchronisierung des ATA Center-Servers, der ATA-Gatewayserver und der Domänencontroller muss in einem Bereich von 5 Minuten zueinander liegen.

### Netzwerkadapter
Das ATA-Gateway erfordert mindestens einen Verwaltungsadapter und mindestens einen Erfassungsadapter:

-   **Verwaltungsadapter:** wird für die Kommunikation im Unternehmensnetzwerk verwendet. Dieser Adapter sollte wie folgt konfiguriert werden:

    -   Statische IP-Adresse, einschließlich des Standardgateways

    -   Bevorzugte und alternative DNS-Server

    -   Das **DNS-Suffix für diese Verbindung** sollte der DNS-Name der Domäne für jede Domäne sein, die überwacht wird.

        ![Konfigurieren Sie das DNS-Suffix in den erweiterten TCP/IP-Einstellungen.](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Wenn das ATA-Gateway Mitglied der Domäne ist, erfolgt diese Konfiguration automatisch.

-   **Erfassungsadapter** – wird verwendet, um den Datenverkehr zu und von den Domänencontrollern zu erfassen.

    > [!IMPORTANT]
    > -   Konfigurieren Sie die Portspiegelung für den Erfassungsadapter als Ziel des Domänencontroller-Netzwerkdatenverkehrs. Weitere Informationen finden Sie unter [Konfigurieren der Portspiegelung](/advanced-threat-analytics/deploy-use/configure-port-mirroring). In der Regel müssen Sie mit dem Netzwerk- oder Virtualisierungsteam zusammenarbeiten, um die Portspiegelung zu konfigurieren.
    > -   Konfigurieren Sie eine statische, nicht routingfähige IP-Adresse für Ihre Umgebung ohne Standardgateway und ohne DNS-Serveradressen. Beispiel: 1.1.1.1/32. Dadurch wird sichergestellt, dass der Erfassungsnetzwerkadapter die maximale Menge an Datenverkehr erfassen kann und der Verwaltungsnetzwerkadapter zum Senden und Empfangen des erforderlichen Netzwerkdatenverkehrs verwendet wird.

### Ports
In der folgenden Tabelle sind die Ports aufgeführt, die für den Verwaltungsadapter des ATA-Gateways mindestens konfiguriert werden müssen:

|Protokoll|Transport|Port|Zu/Von|Richtung|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP und UDP|389|Domänencontroller|Ausgehend|
|Sicheres LDAP (LDAPS)|TCP|636|Domänencontroller|Ausgehend|
|LDAP an globalen Katalog|TCP|3268|Domänencontroller|Ausgehend|
|LDAPs an globalen Katalog|TCP|3269|Domänencontroller|Ausgehend|
|Kerberos|TCP und UDP|88|Domänencontroller|Ausgehend|
|Netlogon|TCP und UDP|445|Domänencontroller|Ausgehend|
|Windows-Zeitdienst|UDP|123|Domänencontroller|Ausgehend|
|DNS|TCP und UDP|53|DNS-Server|Ausgehend|
|NTLM über RPC|TCP|135|Alle Geräte im Netzwerk|Ausgehend|
|NetBIOS|UDP|137|Alle Geräte im Netzwerk|Ausgehend|
|SSL|TCP|443 oder wie für den Center-Dienst konfiguriert|ATA Center:<br /><br />– IP-Adresse des Center-Diensts<br />– IIS-IP-Adresse|Ausgehend|
|Syslog (optional)|UDP|514|SIEM-Server|Eingehend|

> [!NOTE]
> Als Teil des vom ATA-Gateway durchgeführten Auflösungsprozesses müssen die folgenden eingehenden Ports für Geräte im Netzwerk geöffnet werden.
>
> -   NTLM über RPC
> -   NetBIOS

### Zertifikate
Stellen Sie sicher, dass ATA Center Zugriff auf den CRL-Verteilungspunkt hat. Wenn die ATA-Gateways keinen Zugriff auf das Internet haben, führen Sie das Verfahren zum manuellen Importieren einer Zertifikatsperrliste durch. Achten Sie dabei darauf, alle CRL-Verteilungspunkte für die gesamte Kette zu installieren.<br>
Um die Installation von ATA Center zu erleichtern, können Sie während dieser Installation selbstsignierte Zertifikate installieren. Nach der Bereitstellung können Sie die selbstsignierten Zertifikate durch ein Zertifikat einer internen Zertifizierungsstelle ersetzen, das vom ATA-Gateway verwendet werden soll.

> [!NOTE]
> Der Anbietertyp des Zertifikats muss „Kryptografiedienstanbieter (CSP)“ sein.<br>

Im lokalen Computerspeicher des ATA-Gateways muss ein Zertifikat installiert werden, das die **Serverauthentifizierung** unterstützt. Dieses Zertifikat muss für ATA Center vertrauenswürdig sein.

## ATA-Lightweight-Gateway-Anforderungen
In diesem Abschnitt sind die Voraussetzungen für das ATA-Lightweight-Gateway aufgeführt.
### Allgemein
Das ATA-Lightweight-Gateway unterstützt die Installation auf einem Domänencontroller mit Windows Server 2008 R2 SP1, Windows Server 2012, Windows Server 2012 R2.

Beim Domänencontroller kann es sich um einen schreibgeschützten Domänencontroller (Read Only Domain Controller, RODC) handeln.

Der Domänencontroller kann kein Server Core sein.

Vergewissern Sie sich vor der Installation des ATA-Gateways auf einem Domänencontroller unter Windows Server 2012 R2 SP1, dass das folgende Update installiert wurde: [KB2919355](https://support.microsoft.com/kb/2919355/).
Dies können Sie überprüfen, indem Sie das folgende Windows PowerShell-Cmdlet ausführen: `[Get-HotFix -Id kb2919355]`.

### Serverspezifikationen

Das ATA-Lightweight-Gateway erfordert mindestens 2 Kerne und 6 GB RAM auf dem Domänencontroller.
Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des ATA-Lightweight-Gateways auf **Hohe Leistung** fest.
Das ATA-Lightweight-Gateway kann auf den Domänencontrollern verschiedener Auslastungen und Größen bereitgestellt werden, abhängig vom Umfang des Netzwerkverkehrs zwischen den Domänencontrollern und der auf dem Domänencontroller installierten Ressourcen.

>[!NOTE] 
> Bei Ausführung als virtueller Computer wird kein dynamischer Arbeitsspeicher und keine andere Speichererweiterungsfunktion unterstützt.


### Zeitsynchronisierung
Die Zeitsynchronisierung des ATA Center-Servers, der ATA-Lightweight-Gatewayserver und der Domänencontroller muss in einem Bereich von 5 Minuten zueinander liegen.
### Netzwerkadapter
Das ATA-Lightweight-Gateway überwacht den lokalen Datenverkehr auf allen Netzwerkadaptern des Domänencontrollers. <br>
Nach der Bereitstellung können Sie die ATA-Konsole verwenden, wenn Sie die überwachten Netzwerkadapter jemals ändern möchten.

### Ports
In der folgenden Tabelle sind die Ports aufgeführt, die für das ATA-Lightweight-Gateway mindestens konfiguriert werden müssen.

|Protokoll|Transport|Port|Zu/Von|Richtung|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP und UDP|53|DNS-Server|Ausgehend|
|NTLM über RPC|TCP|135|Alle Geräte im Netzwerk|Ausgehend|
|NetBIOS|UDP|137|Alle Geräte im Netzwerk|Ausgehend|
|SSL|TCP|443 oder wie für den Center-Dienst konfiguriert|ATA Center:<br /><br />– IP-Adresse des Center-Diensts<br />– IIS-IP-Adresse|Ausgehend|
|Syslog (optional)|UDP|514|SIEM-Server|Eingehend|

> [!NOTE]
> Als Teil des vom ATA-Lightweight-Gateway durchgeführten Auflösungsprozesses müssen die folgenden eingehenden Ports für Geräte im Netzwerk geöffnet werden.
>
> -   NTLM über RPC
> -   NetBIOS

### Zertifikate
Stellen Sie sicher, dass ATA Center Zugriff auf den CRL-Verteilungspunkt hat. Wenn die ATA-Lightweight-Gateways keinen Zugriff auf das Internet haben, führen Sie das Verfahren zum manuellen Importieren einer Zertifikatsperrliste durch. Achten Sie dabei darauf, alle CRL-Verteilungspunkte für die gesamte Kette zu installieren.
Um die Installation von ATA Center zu erleichtern, können Sie während dieser Installation selbstsignierte Zertifikate installieren. Nach der Bereitstellung können Sie die selbstsignierten Zertifikate durch ein Zertifikat einer internen Zertifizierungsstelle ersetzen, das vom ATA-Lightweight-Gateway verwendet werden soll.
> [!NOTE]
> Der Anbietertyp des Zertifikats muss „Kryptografiedienstanbieter (CSP)“ sein.

Im lokalen Computerspeicher des ATA-Lightweight-Gateways muss ein Zertifikat installiert werden, das die Serverauthentifizierung unterstützt. Dieses Zertifikat muss für ATA Center vertrauenswürdig sein.

## ATA-Konsole
Der Zugriff auf die ATA-Konsole erfolgt über einen Browser. Folgende Browser werden unterstützt:

-   Internet Explorer Version 10 oder höher

-   Google Chrome 40 und höher

-   Mindestauflösung der Bildschirmbreite: 1.700 Pixel

## Siehe auch

- [ATA-Architektur](ata-architecture.md)
- [Installieren von ATA](/advanced-threat-analytics/deploy-use/install-ata)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Jul16_HO4-->


