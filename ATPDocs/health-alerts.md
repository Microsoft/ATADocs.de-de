---
title: Grundlegendes zu Microsoft Defender for Identity-Integritätswarnungen
description: In diesem Artikel werden alle Integritätswarnungen für die einzelnen Komponenten beschrieben und die Ursachen und Schritte zur Behebung des jeweiligen Problems genannt.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 23c5ec5d87c38338dee43fb6665d7ed23830c1ff
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534326"
---
# <a name="understanding-microsoft-defender-for-identity-sensor-health-alerts"></a>Grundlegendes zu Microsoft Defender for Identity-Sensorintegritätswarnungen

Das [!INCLUDE [Product long](includes/product-long.md)]-Integritätscenter informiert Sie, wenn ein Problem im Zusammenhang mit Ihrer [!INCLUDE [Product short](includes/product-short.md)]-Instanz aufgetreten ist, indem es eine Integritätswarnung ausgibt. In diesem Artikel werden alle Integritätswarnungen für die einzelnen Komponenten beschrieben und die Ursachen und Schritte zur Behebung des jeweiligen Problems genannt.

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Keiner der Domänencontroller ist über einen Sensor erreichbar

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor ist derzeit aufgrund von Verbindungsproblemen mit allen konfigurierten Domänencontrollern offline.|Dies beeinträchtigt die Fähigkeit von [!INCLUDE [Product short](includes/product-short.md)], verdächtige Aktivitäten im Zusammenhang mit den von diesem [!INCLUDE [Product short](includes/product-short.md)]-Sensor überwachten Domänencontrollern zu ermitteln.| Stellen Sie sicher, dass die Domänencontroller ausgeführt werden und dieser [!INCLUDE [Product short](includes/product-short.md)]-Sensor LDAP-Verbindungen mit ihnen öffnen kann. Stellen Sie außerdem sicher, dass Sie unter **Einstellungen**, für jede bereitgestellte Gesamtstruktur ein Verzeichnisdienstkonto konfigurieren.|Mittel|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>Alle bzw. einige der Netzwerkdatenerfassungs-Adapter auf einem Sensor sind nicht verfügbar.

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Alle bzw. einige der ausgewählten Adapter zur Erfassung von Netzwerkdaten im [!INCLUDE [Product short](includes/product-short.md)]-Sensor sind deaktiviert oder nicht verbunden.|Der Netzwerkdatenverkehr für einige oder alle Domänencontroller wird vom [!INCLUDE [Product short](includes/product-short.md)]-Sensor nicht mehr erfasst. Dadurch wird die Fähigkeit beeinträchtigt, verdächtige Aktivitäten zu ermitteln, die im Zusammenhang mit diesen Domänencontrollern stehen.|Stellen Sie sicher, dass die ausgewählten Adapter zur Erfassung von Netzwerkdaten im [!INCLUDE [Product short](includes/product-short.md)]-Sensor aktiviert und verbunden sind.|Mittel|

## <a name="directory-services-user-credentials-are-incorrect"></a>Anmeldeinformationen für Verzeichnisdienste nicht korrekt

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Die Anmeldeinformationen für das Verzeichnisdienstbenutzerkonto sind nicht korrekt.|Dies beeinträchtigt die Fähigkeit der Sensoren, Aktivitäten durch LDAP-Abfragen an Domänencontroller zu entdecken.|– Bei AD-**Standardkonten:** Überprüfen Sie, ob der Benutzername, das Kennwort und die Domäne auf der **Verzeichnisdienste**-Konfigurationsseite korrekt sind.<br>– Bei **gruppenverwalteten Dienstkonten:** Überprüfen Sie, ob der Benutzername und die Domäne auf der **Verzeichnisdienste**-Konfigurationsseite korrekt sind. Überprüfen Sie außerdem die anderen auf der Seite [Schnellstart: Herstellen einer Verbindung mit einer Active Directory-Gesamtstruktur](install-step2.md#prerequisites) beschriebenen Voraussetzungen für **gruppenverwaltete Dienstkonten**.|Mittel|

## <a name="low-success-rate-of-active-name-resolution"></a>Niedrige Erfolgsrate bei aktiver Namensauflösung

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Die aufgelisteten [!INCLUDE [Product short](includes/product-short.md)]-Sensoren können IP-Adressen in mehr als 90 % der Fälle nicht mehr anhand der folgenden Methoden in Gerätenamen auflösen:<br />– NTLM über RPC<br />– NetBIOS<br />– Reverse-DNS|Dies wirkt sich auf die Erkennungsfunktionen von [!INCLUDE [Product short](includes/product-short.md)] aus und kann zu einer erhöhten Anzahl falsch positiver Warnungen führen.|– Für NTLM über RPC: Achten Sie darauf, dass Port 135 auf allen Computern in der Umgebung für die eingehende Kommunikation von [!INCLUDE [Product short](includes/product-short.md)]-Sensoren geöffnet ist.<br />– Für Reverse-DNS: Achten Sie darauf, dass die Sensoren den DNS-Server erreichen können und dass Reverse-Lookup-Zonen aktiviert sind.<br />– Für NetBIOS: Achten Sie darauf, dass Port 137 auf allen Computern in der Umgebung für die eingehende Kommunikation von [!INCLUDE [Product short](includes/product-short.md)]-Sensoren geöffnet ist.<br />Stellen Sie außerdem sicher, dass die Netzwerkkonfiguration (beispielsweise Firewalls) nicht die Kommunikation mit den relevanten Ports verhindert.|Niedrig|

## <a name="no-traffic-received-from-domain-controller"></a>Kein Datenverkehr vom Domänencontroller empfangen

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Über diesen [!INCLUDE [Product short](includes/product-short.md)]-Sensor wurde kein Datenverkehr vom Domänencontroller empfangen.|Dies kann darauf hinweisen, dass die Portspiegelung von den Domänencontrollern zum [!INCLUDE [Product short](includes/product-short.md)]-Sensor noch nicht konfiguriert ist oder nicht funktioniert.|Überprüfen Sie, dass die [Portspiegelung ordnungsgemäß auf Ihren Netzwerkgeräten konfiguriert ist](configure-port-mirroring.md).<br></br>Deaktivieren Sie für die verwendete Netzwerkkarte im [!INCLUDE [Product short](includes/product-short.md)]-Sensor unter „Erweiterte Einstellungen“ die folgenden Features:<br></br>Empfang zusammengeführter Segmente (IPv4)<br></br>Empfang zusammengeführter Segmente (IPv6)|Mittel|

## <a name="read-only-user-password-to-expire-shortly"></a>Kennwort für schreibgeschützten Benutzer läuft bald ab

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|The read-only user password, used to perform resolution of entities against Active Directory, is about to expire in less than 30 days. (Das schreibgeschützte Benutzerkennwort, das zum Ausführen von Auflösungen von Entitäten für Active Directory verwendet wird, läuft in weniger als 30 Tagen ab.)|Wenn das Kennwort für diesen Benutzer abläuft, wird die Ausführung aller [!INCLUDE [Product short](includes/product-short.md)]-Sensoren beendet, und es werden keine neuen Daten gesammelt.|[Ändern Sie das Domänenverbindungskennwort](modifying-config-dcpassword.md), und aktualisieren Sie dann das Kennwort im [!INCLUDE [Product short](includes/product-short.md)]-Portal.|Mittel|

## <a name="read-only-user-password-expired"></a>Kennwort für schreibgeschützten Benutzer abgelaufen

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|The read-only user password, used to get directory data, expired. (Das Kennwort für schreibgeschützten Benutzer, das zum Abrufen von Verzeichnisdaten verwendet wird, ist abgelaufen.)|Die Ausführung aller [!INCLUDE [Product short](includes/product-short.md)]-Sensoren wird beendet (sofort oder in Kürze), und es werden keine neuen Daten gesammelt.|[Ändern Sie das Domänenverbindungskennwort](modifying-config-dcpassword.md), und aktualisieren Sie dann das Kennwort im [!INCLUDE [Product short](includes/product-short.md)]-Portal.|Hoch|

## <a name="sensor-outdated"></a>Sensor ist veraltet

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Ein [!INCLUDE [Product short](includes/product-short.md)]-Sensor ist veraltet.|In einem [!INCLUDE [Product short](includes/product-short.md)]-Sensor wird eine Version ausgeführt, die nicht mit der [!INCLUDE [Product short](includes/product-short.md)]-Cloudinfrastruktur kommunizieren kann.|Aktualisieren Sie den Sensor manuell, und prüfen Sie, warum der Sensor nicht automatisch aktualisiert wird. Wenn das nicht funktioniert, laden Sie das neueste Installationspaket für den Sensor herunter, deinstallieren Sie den Sensor, und installieren Sie ihn neu. Weitere Informationen finden Sie unter [Installieren des [!INCLUDE [Product short](includes/product-short.md)]-Sensors](install-step4.md).|Mittel|

## <a name="sensor-reached-a-memory-resource-limit"></a>Sensor hat Arbeitsspeicherressourcenlimit erreicht

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor hat sich selbst beendet und startet automatisch neu, um die Domänencontroller vor einem niedrigen Speicherzustand zu schützen.|Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor erzwingt Arbeitsspeicherbeschränkungen auf sich selbst, um zu verhindern, dass beim Domänencontroller Ressourceneinschränkungen auftreten. Dies geschieht, wenn die Speicherauslastung auf dem Domänencontroller hoch ist. Daten von diesem Domänencontroller werden nur teilweise überwacht.|Erhöhen Sie die Menge des Arbeitsspeichers (RAM) auf dem Domänencontroller, oder fügen Sie diesem Standort mehr Domänencontroller zur besseren Verteilung der Last dieses Domänencontrollers hinzu.|Mittel|

## <a name="sensor-service-failed-to-start"></a>Fehler beim Starten des Sensordiensts

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Der [!INCLUDE [Product short](includes/product-short.md)]-Sensordienst konnte mindestens 30 Minuten lang nicht gestartet werden.|Dies kann die Fähigkeit zum Erkennen verdächtiger Aktivitäten von Domänencontrollern beeinträchtigen, die von diesem [!INCLUDE [Product short](includes/product-short.md)]-Sensor überwacht werden.|Überwachen Sie die [!INCLUDE [Product short](includes/product-short.md)]-Sensorprotokolle, um die zugrunde liegende Ursache für Fehler im [!INCLUDE [Product short](includes/product-short.md)]-Sensordienst nachvollziehen zu können.|Hoch|

## <a name="sensor-stopped-communicating"></a>Sensor hat Kommunikation beendet

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Es gibt keine Kommunikation mehr vom [!INCLUDE [Product short](includes/product-short.md)]-Sensor. Die standardmäßige Zeitspanne für diese Warnung beträgt 5 Minuten.|Der Netzwerkdatenverkehr wird vom Netzwerkadapter im [!INCLUDE [Product short](includes/product-short.md)]-Sensor nicht mehr erfasst. Dies beeinträchtigt die Fähigkeit von ATA, verdächtige Aktivitäten zu erkennen, da der Netzwerkdatenverkehr den [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst nicht erreichen kann.|Stellen Sie sicher, dass der für die Kommunikation zwischen dem [!INCLUDE [Product short](includes/product-short.md)]-Sensor und dem [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst verwendete Port nicht von Routern oder Firewalls blockiert wird.|Mittel|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Einige Domänencontroller können nicht von einem Sensor erreicht werden.

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Die Funktionalität eines [!INCLUDE [Product short](includes/product-short.md)]-Sensors ist aufgrund von Konnektivitätsproblemen mit einigen der konfigurierten Domänencontrollern eingeschränkt.|Die Pass-the-Hash-Erkennung ist möglicherweise weniger präzise, wenn einige Domänencontroller nicht durch den [!INCLUDE [Product short](includes/product-short.md)]-Sensor abgefragt werden können.|Stellen Sie sicher, dass die Domänencontroller ausgeführt werden und dieser [!INCLUDE [Product short](includes/product-short.md)]-Sensor LDAP-Verbindungen mit ihnen öffnen kann.|Mittel|

## <a name="some-windows-events-are-not-being-analyzed"></a>Einige Windows-Ereignisse werden nicht analysiert

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor empfängt mehr Ereignisse, als er verarbeiten kann.|Einige Windows-Ereignisse werden nicht analysiert. Dies kann die Fähigkeit zum Erkennen verdächtiger Aktivitäten von Domänencontrollern beeinträchtigen, die von diesem [!INCLUDE [Product short](includes/product-short.md)]-Sensor überwacht werden.|Vergewissern Sie sich, dass nur erforderliche Ereignisse an den [!INCLUDE [Product short](includes/product-short.md)]-Sensor weitergeleitet werden, oder versuchen Sie, einige der Ereignisse an einen anderen [!INCLUDE [Product short](includes/product-short.md)]-Sensor weiterzuleiten.|Mittel|

## <a name="some-network-traffic-could-not-be-analyzed"></a>Ein Teil des Netzwerkdatenverkehrs konnte nicht analysiert werden.

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor empfängt mehr Netzwerkdatenverkehr, als er verarbeiten kann.|Ein Teil des Netzwerkdatenverkehrs konnte nicht analysiert werden. Dies kann die Fähigkeit zum Erkennen verdächtiger Aktivitäten von Domänencontrollern beeinträchtigen, die von diesem [!INCLUDE [Product short](includes/product-short.md)]-Sensor überwacht werden.|Erwägen Sie es, je nach Bedarf, [zusätzliche Prozessoren und Arbeitsspeicher hinzuzufügen](capacity-planning.md). Wenn es sich um einen eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor handelt, reduzieren Sie die Anzahl der überwachten Domänencontroller.<br></br>Dies kann auch vorkommen, wenn Sie Domänencontroller auf virtuellen VMware-Computer verwenden. Um zu vermeiden, dass diese Warnung ausgegeben wird, können Sie überprüfen, ob auf dem virtuellen Computer die folgenden Einstellungen auf „0“ oder „deaktiviert“ festgelegt sind:<br></br>- TsoEnable<br></br>- LargeSendOffload(IPv4)<br></br>- IPv4 TSO Offload<br></br>Deaktivieren Sie ebenso IPv4 Giant TSO Offload. Weitere Informationen finden Sie in der VMware-Dokumentation.|Mittel|

## <a name="some-etw-events-are-not-being-analyzed"></a>Einige ETW-Ereignisse werden nicht analysiert.

|Warnung|Beschreibung|Lösung|Schweregrad|
|----|----|----|----|
|Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor empfängt mehr Ereignisse der Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), als er verarbeiten kann.|Einige Ereignisse der Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW) werden nicht analysiert. Dies kann die Fähigkeit zum Erkennen verdächtiger Aktivitäten von Domänencontrollern beeinträchtigen, die von diesem [!INCLUDE [Product short](includes/product-short.md)]-Sensor überwacht werden.|Vergewissern Sie sich, dass nur erforderliche Ereignisse an den [!INCLUDE [Product short](includes/product-short.md)]-Sensor weitergeleitet werden, oder versuchen Sie, einige der Ereignisse an einen anderen [!INCLUDE [Product short](includes/product-short.md)]-Sensor weiterzuleiten.|Mittel|

<!--
## Windows events missing from domain controller audit policy

|Alert|Description|Resolution|Severity|
|----|----|----|----|
| Windows events missing from domain controller audit policy|For the correct events to be audited and included in the Windows Event Log, your domain controllers require accurate Advanced Audit Policy settings. Incorrect Advanced Audit Policy settings leave critical events out of your logs, and result in incomplete [!INCLUDE [Product short](includes/product-short.md)] coverage.|Review your [Advanced Audit policy](configure-windows-event-collection.md) and modify as needed. | Medium|
-->

## <a name="see-also"></a>Weitere Informationen

- [Voraussetzungen für [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Kapazitätsplanung für [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
