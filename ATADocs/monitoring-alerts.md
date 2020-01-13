---
title: Verstehen von ATA-Überwachungswarnungen | Microsoft-Dokumentation
description: Beschreibt die Verwendung der ATA-Protokolle zum Behandeln von Problemen.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b04fb8a4-b366-4b55-9d4c-6f054fa58a90
ms.reviewer: elofek
ms.suite: ems
ms.openlocfilehash: 2185c5e01631a33b8dcc0848c97f9f9ed7bf7878
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2020
ms.locfileid: "75908040"
---
# <a name="understanding-ata-monitoring-alerts"></a>Grundlegendes zu ATA-Überwachungswarnungen

*Gilt für: Advanced Threat Analytics Version 1.9*

Das ATA Health Center informiert Sie, wenn ein Problem mit der ATA-Bereitstellung aufgetreten ist, indem eine Überwachungswarnung ausgegeben wird.
Dieser Artikel beschreibt alle Überwachungswarnungen für jede Komponente und listet den Grund sowie die erforderlichen Schritte zur Lösung des Problems auf.
## <a name="ata-center-issues"></a>ATA Center-Probleme
### <a name="center-running-out-of-disk-space"></a>Festplattenspeicher für Center nahezu vollständig belegt
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The free space on the ATA Center machine drive that is used for storing the ATA database is getting low. (Der freie Speicherplatz auf dem Laufwerk des ATA-Center-Computers, der zum Speichern der ATA-Datenbank verwendet wird, geht zur Neige).|Das bedeutet, dass die Festplatte über weniger als 200 GB freien Speicherplatz verfügt oder dass es weniger als 20 % freien Speicherplatz gibt, was auch immer kleiner ist. Wenn ATA bemerkt, dass der Speicherplatz der Festplatte zur Neige geht, werden alte Daten von der Datenbank gelöscht. Wenn keine alten Daten gelöscht werden können, da diese noch immer für die Erkennungs-Engine benötigt werden, erhalten Sie diese Warnung. Wenn Sie diese Warnung erhalten, stoppt ATA die Nachverfolgung neuer Aktivitäten.|Erhöhen Sie die Festplattengröße, oder geben Sie Speicherplatz auf dieser Festplatte frei.|High (Hoch)|
### <a name="failure-sending-mail"></a>Fehler beim Senden von E-Mail
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|ATA Failed to send an email notification to the specified mail server. (ATA konnte keine E-Mail-Benachrichtigung an den angegebenen Mailserver senden.)|Es werden keine E-Mail-Benachrichtigungen von ATA gesendet.|Überprüfen Sie die SMTP-Serverkonfiguration|Low (Niedrig)|

### <a name="center-overloaded"></a>Center überlastet
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The ATA Center is not able to handle the amount of data being transferred from the ATA Gateways. (ATA Center kann die Menge der Daten, die von ATA-Gateways übertragen werden, nicht verarbeiten.) |ATA Center beendet die Analyse von neuem Netzwerkverkehr und Ereignissen. Das bedeutet, dass die Exaktheit der Erkennungen und Profile minimiert wird, während diese Überwachungswarnung aktiv ist.|Stellen Sie sicher, dass Sie genügen Ressourcen für ATA Center bereitgestellt haben. Weitere Details zur genauen Planung der ATA Center-Kapazität finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md). Untersuchen Sie die Leistung von ATA Center mithilfe der [Problembehandlung bei ATA mithilfe der Leistungsindikatoren](troubleshooting-ata-using-perf-counters.md).|High (Hoch)|

### <a name="failure-connecting-to-the-siem-server-using-syslog"></a>Fehler bei der Verbindungsherstellung mit dem SIEM-Server unter Verwendung von Syslog.
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|ATA failed to send events to the specified SIEM. (ATA konnte keine Ereignisse an den angegebenen SIEM-Agent senden.)|Das bedeutet, dass ATA Center keine verdächtigen Aktivitäten und Überwachungswarnungen an SIEM senden kann.|Stellen Sie sicher, dass Ihre [Syslog-Servereinstellungen ordnungsgemäß konfiguriert sind](setting-syslog-email-server-settings.md).|Low (Niedrig)|
### <a name="center-certificate-is-about-to-expire"></a>Center certificate is about to expire (Center-Zertifikat läuft bald ab)
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The ATA Center certificate will expire in less than 3 weeks. (Das ATA Center-Zertifikat läuft in weniger als 3 Wochen ab.)|Nach dem Ablauf des Zertifikats: Die Konnektivität vom ATA-Gateway zu ATA Center schlägt fehl. Der ATA Center-Prozess stürzt ab, und alle ATA-Funktionen werden angehalten.|[Ersetzen Sie das Zertifikat für ATA Center](modifying-ata-center-configuration.md)|Medium (Mittel)|
### <a name="ata-center-certificate-expired"></a>Das ATA Center-Zertifikat ist abgelaufen
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The ATA Center certificate expired. (Das ATA Center-Zertifikat ist abgelaufen.)|Nach dem Ablauf des Zertifikats: Die Konnektivität vom ATA-Gateway zu ATA Center kann nicht hergestellt werden. Der ATA Center-Prozess stürzt ab, und alle ATA-Funktionen werden angehalten.|[Erneutes Bereitstellen von ATA Center](install-ata-step1.md)|High (Hoch)|
## <a name="ata-gateway-issues"></a>Probleme mit dem ATA-Gateway
### <a name="read-only-user-password-to-expire-shortly"></a>Kennwort für schreibgeschützten Benutzer läuft bald ab
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The read-only user password, used to perform resolution of entities against Active Directory, is about to expire in less than 30 days. (Das schreibgeschützte Benutzerkennwort, das zum Ausführen von Auflösungen von Entitäten für Active Directory verwendet wird, läuft in weniger als 30 Tagen ab.)|Wenn das Kennwort für diesen Benutzer abläuft, werden ATA-Gateways nicht mehr ausgeführt, und es werden keine neuen Daten gesammelt.|[Ändern Sie das Domänenverbindungskennwort](modifying-ata-config-dcpassword.md), und ändern Sie das Kennwort in der ATA-Konsole.|Medium (Mittel)|
### <a name="read-only-user-password-expired"></a>Kennwort für schreibgeschützten Benutzer abgelaufen
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The read-only user password, used to get directory data, expired. (Das Kennwort für schreibgeschützten Benutzer, das zum Abrufen von Verzeichnisdaten verwendet wird, ist abgelaufen.)|Es werden keine ATA-Gateways mehr ausgeführt (oder bald nicht mehr ausgeführt), und es werden keine neuen Daten gesammelt.|[Ändern Sie das Domänenverbindungskennwort](modifying-ata-config-dcpassword.md), und ändern Sie das Kennwort in der ATA-Konsole.|High (Hoch)|
### <a name="gateway-certificate-about-to-expire"></a>Gatewayzertifikat läuft bald ab
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The ATA Gateway certificate will expire in less than 3 weeks. (Das ATA-Gatewayzertifikat läuft in weniger als 3 Wochen ab.)|Es gibt keine Konnektivität vom jeweiligen ATA-Gateway zu ATA Center. Es werden keine Daten von diesem ATA-Gateway gesendet.|Das ATA-Gatewayzertifikat sollt automatisch erneuert werden. Lesen Sie die Protokolle für das ATA-Gateway und ATA Center, um zu verstehen, warum das Zertifikat sich nicht automatisch erneuert hat.|Medium (Mittel)|

### <a name="gateway-certificate-expired"></a>Gatewayzertifikat abgelaufen
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The ATA Gateway certificate expired. (Das ATA-Gatewayzertifikat ist abgelaufen.)|Es ist gibt keine Konnektivität von diesem ATA-Gateway zu ATA Center. Es werden keine Daten von diesem ATA-Gateway gesendet.|[Deinstallieren Sie ATA-Gateway, und installieren Sie es neu](install-ata-step3.md).|High (Hoch)|
### <a name="domain-synchronizer-not-assigned"></a>Domain synchronizer not assigned (Domänensynchronizer nicht zugewiesen)
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|No domain synchronizer is assigned to any ATA Gateway. (Es sind keine Domänensynchronizer einem ATA-Gateway zugewiesen.) Das kann passieren, wenn kein ATA-Gateway als Kandidat für die Domänensynchronisierung konfiguriert ist.|Wenn die Domäne nicht synchronisiert ist, können Änderungen an Entitäten dazu führen, dass Entitätsinformationen in ATA veraltet sind oder fehlen. Die Erkennung wird jedoch nicht beeinträchtigt.|Stellen Sie sicher, dass zumindest ein ATA-Gateway als [Domänensynchronizer](install-ata-step5.md) festgelegt ist.|Low (Niedrig)|
### <a name="allsome-of-the-capture-network-adapters-on-a-gateway-are-not-available"></a>Keiner der Netzwerkadapter für die Erfassung auf einem Gateway ist verfügbar/Einige der Netzwerkadapter für die Erfassung auf einem Gateway sind nicht verfügbar
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|All/Some of the selected capture network adapters on the ATA Gateway are disabled or disconnected. (Alle/Einige der ausgewählten Netzwerkdatenerfassungs-Adapter auf dem ATA-Gateway sind deaktiviert oder nicht verbunden.)|Der Netzwerkdatenverkehr für einige/alle Domänencontroller wird nicht länger vom ATA-Gateway erfasst. Dadurch wird die Fähigkeit beeinträchtigt, verdächtige Aktivitäten zu ermitteln, die im Zusammenhang mit diesen Domänencontrollern stehen.|Stellen Sie sicher, dass der ausgewählte Netzwerkdatenerfassungs-Adapter auf dem ATA-Gateway aktiviert und verbunden ist.|Medium (Mittel)|
### <a name="some-domain-controllers-are-unreachable-by-a-gateway"></a>Einige Domänencontroller können nicht durch ein Gateway erreicht werden.
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|An ATA Gateway has limited functionality due to connectivity issues to some of the configured domain controllers. (Ein ATA-Gateway verfügt über eingeschränkte Funktionalität aufgrund von Verbindungsproblemen mit einigen der konfigurierten Domänencontrollern.)|Die Übergabe der Hash-Erkennung ist möglicherweise ungenauer, wenn einige Domänencontroller nicht durch das ATA-Gateway abgefragt werden können.|Stellen Sie sicher, dass die Domänencontroller ausgeführt werden und der ATA-Gateway LDAP-Verbindungen für sie öffnen kann.|Medium (Mittel)|
### <a name="all-domain-controllers-are-unreachable-by-a-gateway"></a>Keiner der Domänencontroller kann durch ein Gateway erreicht werden.
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The ATA Gateway is currently offline due to connectivity issues to all the configured domain controllers. (Das ATA-Gateway ist derzeit aufgrund von Verbindungsproblemen mit allen der konfigurierten Domänencontrollern offline.)|Dadurch wird die Fähigkeit von ATA beeinträchtigt, verdächtige Aktivitäten im Zusammenhang mit den von diesem ATA-Gateway überwachten Domänencontrollern zu ermitteln.| Stellen Sie sicher, dass die Domänencontroller ausgeführt werden und der ATA-Gateway LDAP-Verbindungen für sie öffnen kann.|Medium (Mittel)|
### <a name="gateway-stopped-communicating"></a>Gateway hat Kommunikation eingestellt
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|There has been no communication from the ATA Gateway. (Es gibt keine Kommunikation mehr vom ATA-Gateway.) Die standardmäßige Zeitspanne für diese Warnung beträgt 5 Minuten.|Der Netzwerkdatenverkehr wird nicht länger vom Transportadapter auf dem ATA-Gateway erfasst. Dadurch wird die Fähigkeit von ATA, verdächtige Aktivitäten zu erkennen, beeinträchtigt, da der Netzwerkdatenverkehr ATA Center nicht erreichen kann.|Prüfen Sie, dass der für die Kommunikation zwischen dem ATA-Gateway und dem ATA Center-Dienst verwendete Port nicht von Routern oder Firewalls blockiert wird.|Medium (Mittel)|
### <a name="no-traffic-received-from-domain-controller"></a>Kein Datenverkehr vom Domänencontroller empfangen
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|No traffic was received from the domain controller via this ATA Gateway. (Es wurde kein Datenverkehr vom Domänencontroller über dieses ATA-Gateway empfangen.)|Dies kann angeben, dass die Portspiegelung von Domänencontrollern zum ATA-Gateway noch nicht konfiguriert ist oder noch nicht ausgeführt wird.|Überprüfen Sie, dass die [Portspiegelung ordnungsgemäß auf Ihren Netzwerkgeräten konfiguriert ist](configure-port-mirroring.md).<br></br>Deaktivieren Sie diese Funktionen auf dem verwendeten NIC auf dem ATA-Gateway unter „Erweiterte Einstellungen“:<br></br>Empfang zusammengeführter Segmente (IPv4)<br></br>Empfang zusammengeführter Segmente (IPv6)|Medium (Mittel)|
### <a name="some-forwarded-events-are-not-being-analyzed"></a>Einige weitergeleitete Ereignisse werden nicht analysiert
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The ATA Gateway is receiving more events than it can process. (Das ATA-Gateway enthält mehr Ereignisse, als es verarbeiten kann.)|Einige weitergeleitete Ereignisse werden nicht analysiert, was die Fähigkeit zum Erkennen verdächtiger Aktivitäten beeinflussen kann, die von Domänencontrollern stammen, die von diesem ATA-Gateway überwacht werden.|Überprüfen Sie, dass nur erforderliche Ereignisse an das ATA-Gateway weitergeleitet werden, oder versuchen Sie, einige der Ereignisse an ein anderes ATA-Gateway weiterzuleiten.|Medium (Mittel)|
### <a name="some-network-traffic-is-not-being-analyzed"></a>Ein Teil des Netzwerkdatenverkehrs wird nicht analysiert
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The ATA Gateway is receiving more network traffic than it can process. (Das ATA-Gateway erhält mehr Netzwerkdatenverkehr als es verarbeiten kann.)|Ein Teil des Netzwerkdatenverkehrs wird nicht analysiert, was die Fähigkeit zum Erkennen verdächtiger Aktivitäten beeinflussen kann, die von Domänencontrollern stammen, die von diesem ATA-Gateway überwacht werden.|Erwägen Sie es, je nach Bedarf, [zusätzliche Prozessoren und Arbeitsspeicher hinzuzufügen](ata-capacity-planning.md). Wenn es sich um ein eigenständiges ATA-Gateway handelt, reduzieren Sie die Anzahl der überwachten Domänencontroller.<br></br>Dies kann auch vorkommen, wenn Sie Domänencontroller auf virtuellen VMware-Computer verwenden. Um zu vermeiden, dass diese Warnung ausgegeben wird, können Sie überprüfen, ob auf dem virtuellen Computer die folgenden Einstellungen auf „0“ oder „deaktiviert“ festgelegt sind:<br></br>- TsoEnable<br></br>- LargeSendOffload(IPv4)<br></br>- IPv4 TSO Offload<br></br>Deaktivieren Sie ebenso IPv4 Giant TSO Offload. Weitere Informationen finden Sie in der VMware-Dokumentation.|Medium (Mittel)|

### <a name="gateway-version-outdated"></a>Gatewayversion veraltet
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The ATA Center is newer than the version installed on the ATA Gateway. (ATA Center ist neuer als die auf dem ATA-Gateway installierte Version.) Dadurch funktioniert das ATA-Gateway nicht mehr wie erwartet.|Dies kann die Fähigkeit zum Erkennen verdächtiger Aktivitäten beeinflussen, die von Domänencontrollern stammen, die von diesem ATA-Gateway überwacht werden.|Das ATA-Gateway wird automatisch auf die neueste Version aktualisiert, indem ein [automatisches Update](install-ata-step1.md) in der ATA-Konsole aktiviert oder das neueste in der ATA-Konsole verfügbare ATA-Gatewaypaket heruntergeladen wird.|High (Hoch)|
### <a name="gateway-service-failed-to-start"></a>Fehler beim Starten des Gatewaydiensts.
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The ATA Gateway service failed to start for at least 30 minutes. (Der ATA-Gatewaydienst konnte für mindestens 30 Minuten nicht gestartet werden.)|Dies kann die Fähigkeit zum Erkennen verdächtiger Aktivitäten beeinflussen, die von Domänencontrollern stammen, die von diesem ATA-Gateway überwacht werden.|Überwachen Sie ATA-Gatewayprotokolle, um [die Grundursache für den Fehler des ATA-Gatewaydiensts zu verstehen](troubleshooting-ata-using-logs.md).|High (Hoch)|
## <a name="lightweight-gateway"></a>Lightweight-Gateway
### <a name="lightweight--gateway-reached-a-memory-resource-limit"></a>Lightweight-Gateway hat Arbeitsspeicherressourcenlimit erreicht
|Warnung|Description|Lösung|Schweregrad|
|----|----|----|----|
|The Lightweight ATA Gateway stopped itself and will restart automatically to protect the domain controller from a low memory condition. (Das ATA-Lightweight-Gateway hat sich selbst angehalten und startet automatisch neu, um die Domänencontroller von einem niedrigen Speicherzustand zu schützen.)|Das ATA-Lightweight-Gateway erzwingt Arbeitsspeicherbeschränkungen auf sich selbst, um zu verhindern, dass beim Domänencontroller Ressourceneinschränkungen auftreten. Dies geschieht, wenn die Speicherauslastung auf dem Domänencontroller hoch ist. Daten von diesem Domänencontroller werden nur teilweise überwacht.|Erhöhen Sie die Menge des Arbeitsspeichers (RAM) auf dem Domänencontroller, oder fügen Sie diesem Standort mehr Domänencontroller zur besseren Verteilung der Last dieses Domänencontrollers hinzu.|Medium (Mittel)|


## <a name="see-also"></a>Weitere Informationen:
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
