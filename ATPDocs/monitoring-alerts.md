---
title: "Grundlegende Informationen zu Überwachungswarnungen in Azure ATP | Microsoft-Dokumentation"
description: Beschreibt die Verwendung der Azure ATP-Protokolle zum Behandeln von Problemen.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: d0551e91-3b21-47d5-ad9d-3362df6d47c0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cdb440e92aef0f9d09d3aa9411d0ce65435469d1
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
*Gilt für: Azure Advanced Threat Protection*

# <a name="understanding-azure-atp-sensor-and-standalone-sensor-monitoring-alerts"></a>Grundlegende Informationen zu Überwachungswarnungen für Azure ATP-Sensor und selbstständige Azure ATP-Sensoren

Das Azure ATP-Integritätscenter informiert Sie, wenn ein Problem im Zusammenhang mit einem Ihrer Azure ATP-Arbeitsbereiche aufgetreten ist, indem es eine Überwachungswarnung ausgibt. Dieser Artikel beschreibt alle Überwachungswarnungen für jede Komponente und listet den Grund sowie die erforderlichen Schritte zur Lösung des Problems auf.

## <a name="read-only-user-password-to-expire-shortly"></a>Kennwort für schreibgeschützten Benutzer läuft bald ab

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|The read-only user password, used to perform resolution of entities against Active Directory, is about to expire in less than 30 days. (Das schreibgeschützte Benutzerkennwort, das zum Ausführen von Auflösungen von Entitäten für Active Directory verwendet wird, läuft in weniger als 30 Tagen ab.)|Wenn das Kennwort für diesen Benutzer abläuft, werden alle Azure ATP-Sensoren nicht mehr ausgeführt und keine neuen Daten gesammelt.|[Ändern Sie das Domänenverbindungskennwort](modifying-atp-config-dcpassword.md), und aktualisieren Sie dann das Kennwort in der Azure ATP-Konsole.|Mittel|

## <a name="read-only-user-password-expired"></a>Kennwort für schreibgeschützten Benutzer abgelaufen

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|The read-only user password, used to get directory data, expired. (Das Kennwort für schreibgeschützten Benutzer, das zum Abrufen von Verzeichnisdaten verwendet wird, ist abgelaufen.)|Es werden keine Azure ATP-Sensoren mehr ausgeführt (oder bald nicht mehr ausgeführt), und es werden keine neuen Daten gesammelt.|[Ändern Sie das Domänenverbindungskennwort](modifying-atp-config-dcpassword.md), und aktualisieren Sie dann das Kennwort in der Azure ATP-Konsole.|Hoch|

## <a name="domain-synchronizer-not-assigned"></a>Domain synchronizer not assigned (Domänensynchronizer nicht zugewiesen)

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|No domain synchronizer is assigned to any Azure ATP sensor. (Es sind keine Domänensynchronizer einem Azure ATP-Sensor zugewiesen.) This may happen if there is no Azure ATP sensor configured as domain synchronizer candidate. (Das kann passieren, wenn kein Azure ATP-Sensor als Kandidat für die Domänensynchronisierung konfiguriert ist.)|Wenn die Domäne nicht synchronisiert ist, können Änderungen an Entitäten dazu führen, dass Entitätsinformationen in Azure ATP veraltet sind oder fehlen. Die Erkennung wird jedoch nicht beeinträchtigt.|Stellen Sie sicher, dass zumindest ein Azure ATP-Sensor als [Domänensynchronizer](install-atp-step5.md) festgelegt ist.|Niedrig|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>Alle bzw. einige der Netzwerkdatenerfassungs-Adapter auf einem Sensor sind nicht verfügbar.

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|All/Some of the selected capture network adapters on the Azure ATP sensor are disabled or disconnected. (Alle bzw. einige der ausgewählten Netzwerkdatenerfassungs-Adapter auf dem Azure ATP-Sensor sind deaktiviert oder nicht verbunden.)|Der Netzwerkdatenverkehr für einige bzw. alle Domänencontroller wird nicht länger vom Azure ATP-Sensor erfasst. Dadurch wird die Fähigkeit beeinträchtigt, verdächtige Aktivitäten zu ermitteln, die im Zusammenhang mit diesen Domänencontrollern stehen.|Stellen Sie sicher, dass diese ausgewählten Netzwerkdatenerfassungs-Adapter auf dem Azure ATP-Sensor aktiviert und verbunden sind.|Mittel|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Einige Domänencontroller können nicht von einem Sensor erreicht werden.

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|An Azure ATP sensor has limited functionality due to connectivity issues to some of the configured domain controllers. (Ein Azure ATP-Sensor verfügt über eingeschränkte Funktionalität aufgrund von Verbindungsproblemen mit einigen der konfigurierten Domänencontroller.)|Die Pass-the-Hash-Erkennung ist möglicherweise ungenauer, wenn einige Domänencontroller nicht durch den Azure ATP-Sensor abgefragt werden können.|Stellen Sie sicher, dass die Domänencontroller ausgeführt werden und der Azure ATP-Sensor LDAP-Verbindungen mit ihnen öffnen kann.|Mittel|

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Keiner der Domänencontroller ist über einen Sensor erreichbar

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|The Azure ATP sensor is currently offline due to connectivity issues to all the configured domain controllers. (Der Azure ATP-Sensor ist derzeit aufgrund von Verbindungsproblemen mit allen konfigurierten Domänencontrollern offline.)|Dadurch wird die Fähigkeit des Azure ATP-Sensors beeinträchtigt, verdächtige Aktivitäten im Zusammenhang mit den von diesem Azure ATP-Sensor überwachten Domänencontrollern zu ermitteln.| Stellen Sie sicher, dass die Domänencontroller ausgeführt werden und der Azure ATP-Sensor LDAP-Verbindungen mit ihnen öffnen kann.|Mittel|

## <a name="sensor-stopped-communicating"></a>Sensor hat Kommunikation beendet

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|There has been no communication from the Azure ATP Sensor. (Es geht keine Kommunikation mehr vom Azure ATP-Sensor aus.) Die standardmäßige Zeitspanne für diese Warnung beträgt 5 Minuten.|Der Netzwerkdatenverkehr wird nicht länger vom Netzwerkadapter auf dem Azure ATP-Sensor erfasst. Dadurch wird die Fähigkeit von ATA, verdächtige Aktivitäten zu erkennen, beeinträchtigt, da der Netzwerkdatenverkehr den Azure ATP-Clouddienst nicht erreichen kann.|Stellen Sie sicher, dass der für die Kommunikation zwischen dem Azure ATP-Sensor und dem Azure ATP-Clouddienst verwendete Port nicht von Routern oder Firewalls blockiert wird.|Mittel|

## <a name="no-traffic-received-from-domain-controller"></a>Kein Datenverkehr vom Domänencontroller empfangen

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|No traffic was received from the domain controller via this Azure ATP sensor. (Es wurde kein Datenverkehr vom Domänencontroller über diesen Azure ATP-Sensor empfangen.)|Dies weist möglicherweise darauf hin, dass die Portspiegelung von den Domänencontrollern zum Azure ATP-Sensor noch nicht konfiguriert ist oder noch nicht ausgeführt wird.|Überprüfen Sie, dass die [Portspiegelung ordnungsgemäß auf Ihren Netzwerkgeräten konfiguriert ist](configure-port-mirroring.md).<br></br>Deaktivieren Sie diese Features für die verwendete NIC auf dem Azure ATP-Sensor unter „Erweiterte Einstellungen“:<br></br>Empfang zusammengeführter Segmente (IPv4)<br></br>Empfang zusammengeführter Segmente (IPv6)|Mittel|

## <a name="some-forwarded-events-are-not-being-analyzed"></a>Einige weitergeleitete Ereignisse werden nicht analysiert

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|The Azure ATP sensor is receiving more events than it can process. (Der Azure ATP-Sensor empfängt mehr Ereignisse als er verarbeiten kann.)|Einige weitergeleitete Ereignisse werden nicht analysiert, was die Fähigkeit zum Erkennen verdächtiger Aktivitäten beeinflussen kann. Diese stammen von Domänencontrollern, die von diesem Azure ATP-Sensor überwacht werden.|Überprüfen Sie, ob nur erforderliche Ereignisse an den Azure ATP-Sensor weitergeleitet werden, oder versuchen Sie, einige der Ereignisse an einen anderen Azure ATP-Sensor weiterzuleiten.|Mittel|

## <a name="some-network-traffic-is-not-being-analyzed"></a>Ein Teil des Netzwerkdatenverkehrs wird nicht analysiert

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|The Azure ATP sensor is receiving more network traffic than it can process. (Der Azure ATP-Sensor empfängt mehr Netzwerkdatenverkehr als er verarbeiten kann.)|Ein Teil des Netzwerkdatenverkehrs wird nicht analysiert, was die Fähigkeit zum Erkennen verdächtiger Aktivitäten beeinflussen kann. Diese stammen von Domänencontrollern, die von diesem Azure ATP-Sensor überwacht werden.|Erwägen Sie es, je nach Bedarf, [zusätzliche Prozessoren und Arbeitsspeicher hinzuzufügen](atp-capacity-planning.md). Wenn es sich um einen eigenständigen Azure ATP-Sensor handelt, reduzieren Sie die Anzahl der überwachten Domänencontroller.<br></br>Dies kann auch vorkommen, wenn Sie Domänencontroller auf virtuellen VMware-Computer verwenden. Um zu vermeiden, dass diese Warnung ausgegeben wird, können Sie überprüfen, ob auf dem virtuellen Computer die folgenden Einstellungen auf „0“ oder „deaktiviert“ festgelegt sind:<br></br>- TsoEnable<br></br>- LargeSendOffload(IPv4)<br></br>- IPv4 TSO Offload<br></br>Deaktivieren Sie ebenso IPv4 Giant TSO Offload. Weitere Informationen finden Sie in der VMware-Dokumentation.|Mittel|

## <a name="sensor-service-failed-to-start"></a>Fehler beim Starten des Sensordiensts

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|The Azure ATP sensor service failed to start for at least 30 minutes. (Der Azure ATP-Sensordienst konnte für mindestens 30 Minuten nicht gestartet werden.)|Dies kann die Fähigkeit zum Erkennen verdächtiger Aktivitäten beeinflussen, die von Domänencontrollern stammen, die von diesem Azure ATP-Sensor überwacht werden.|Überwachen Sie die Azure ATP-Sensorprotokolle, um die Grundursache für Dienstfehler des Azure ATP-Sensors nachvollziehen zu können.|Hoch|

## <a name="sensor-reached-a-memory-resource-limit"></a>Sensor hat Arbeitsspeicherressourcenlimit erreicht

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|The Azure ATP sensor stopped itself and will restart automatically to protect the domain controller from a low memory condition. (Der Azure ATP-Sensor hat sich selbst angehalten und startet automatisch neu, um die Domänencontroller vor einem niedrigen Speicherzustand zu schützen.)|Der Azure ATP-Sensor erzwingt Arbeitsspeicherbeschränkungen auf sich selbst, um zu verhindern, dass beim Domänencontroller Ressourceneinschränkungen auftreten. Dies geschieht, wenn die Speicherauslastung auf dem Domänencontroller hoch ist. Daten von diesem Domänencontroller werden nur teilweise überwacht.|Erhöhen Sie die Menge des Arbeitsspeichers (RAM) auf dem Domänencontroller, oder fügen Sie diesem Standort mehr Domänencontroller zur besseren Verteilung der Last dieses Domänencontrollers hinzu.|Mittel|


## <a name="see-also"></a>Weitere Informationen

- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)