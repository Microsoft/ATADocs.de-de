---
title: Verweis auf ATA-Ereignis-IDs | Microsoft-Dokumentation
description: Gibt eine Liste der ATA-Ereignis-IDs und deren Beschreibungen zurück.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: a54c68f333cfc3eb47d47c66f1ded701fb855a80
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2019
ms.locfileid: "65196284"
---
# <a name="ata-event-id-reference"></a>Verweis auf ATA-Ereignis-IDs


*Gilt für: Advanced Threat Analytics Version 1.9*

Die Ereignisanzeige des ATA Centers protokolliert Ereignisse für ATA. In diesem Artikel wird eine Liste mit Event-IDs und den dazugehörigen Beschreibungen zur Verfügung gestellt.

Die Ereignisse finden Sie hier:

![Speicherort der Ereignis-ID](./media/event-id-location.png)

## <a name="ata-health-events"></a>ATA-Integritätsereignisse

|Überwachen der Ereignis-ID| Überwachen des Warnungsnamens|
|---------|---------------|
|1001|Festplattenspeicher für Center nahezu vollständig belegt|
|1003|Center überlastet|
|1004|Zertifikat für Center läuft bald ab/Zertifikat für Center ist abgelaufen|
|1005|MongoDB ist nicht verfügbar|
|1006|Kennwort für schreibgeschützten Benutzer läuft bald ab/Kennwort für schreibgeschützten Benutzer abgelaufen|
|1007|Domain synchronizer not assigned (Domänensynchronizer nicht zugewiesen)|
|1008|Einige oder alle der Netzwerkadapter für die Erfassung auf einem Gateway sind nicht verfügbar|
|1009|Ein Netzwerkdatenerfassungs-Adapter auf einem Gateway ist nicht mehr vorhanden|
|1010|Einige Domänencontroller können von einem Gateway nicht erreicht werden/Alle Domänencontroller können von einem Gateway nicht erreicht werden|
|1011|Gateway hat Kommunikation eingestellt|
|1012|Einige weitergeleitete Ereignisse werden nicht analysiert|
|1013|Ein Teil des Netzwerkdatenverkehrs wird nicht analysiert|
|1014|Fehler beim Senden von E-Mail|
|1015|Fehler bei der Verbindungsherstellung mit dem SIEM-Server unter Verwendung von Syslog.|
|1016|Gatewayversion veraltet|
|1017|Kein Datenverkehr vom Domänencontroller empfangen|
|1018|Fehler beim Starten des Gatewaydiensts.|
|1019|Lightweight-Gateway hat Arbeitsspeicherressourcenlimit erreicht|
|1020|Gateway verarbeitet keine Radius-Ereignisse|
|1021|Gateway verarbeitet keine Syslog-Ereignisse|
|1022|Geolocation-Dienst ist nicht verfügbar|
 
## <a name="ata-security-alert-events"></a>ATA-Sicherheitswarnungsereignisse

|Warnungsnamen|Ereignis-IDs der Warnungen|
|---------|---------------|
|2001|Verdacht des Identitätsdiebstahls auf Grundlage von ungewöhnlichem Verhalten|
|2002|Ungewöhnliche Protokollimplementierung|
|2003|Reconnaissance mithilfe von Kontoenumeration|
|2004|Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung|
|2006|Böswillige Replikation von Verzeichnisdiensten|
|2007|Reconnaissance über DNS|
|2008|Aktivität zur Herabstufung der Verschlüsselung|
|2009|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Golden Ticket-Angriff)|
|2010|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Overpass-the-Hash-Angriff)|
|2011|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Skeleton Key-Angriff)|
|2012|Reconnaissance mithilfe der SMB-Sitzungsenumeration|
|2013|Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten|
|2014|Honeytoken-Aktivität|
|2016|Umfangreiche Objektlöschungen|
|2017|Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs|
|2018|Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs|
|2019|Erkannter Remoteausführungsversuch|
|2020|Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit|
|2021|Reconnaissance mithilfe von Verzeichnisdienstabfragen|
|2022|Golden Ticket-Aktivität von Kerberos|
|2023|Verdächtige Authentifizierungsfehler|
|2024|Ungewöhnliche Modifizierung von sensiblen Gruppen|
|2026|Erstellen eines verdächtigen Diensts|

## <a name="ata-auditing-events"></a>ATA-Überwachungsereignisse

|Warnungsnamen|Ereignis-IDs der Warnungen|
|---------|---------------|
|3001|Änderung an der ATA-Konfiguration|
|3002|Hinzufügen von ATA-Gateway|
|3003|Löschen von ATA-Gateway|
|3004|Aktivieren der ATA-Lizenz|
|3005|Anmelden bei der ATA-Konsole|
|3006|Manuelle Änderung zum Status „Integritätsaktivität“|
|3007|Manuelle Änderung zum Status „verdächtige Aktivität“|

## <a name="see-also"></a>Weitere Informationen:
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
