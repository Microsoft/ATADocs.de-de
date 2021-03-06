---
title: Neues in Advanced Threat Analytics Version 1,6
description: Listet Neuerungen sowie bekannte Probleme in ATA 1.6 auf.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 27b139e5-12b9-4953-8f53-eb58e8ce0038
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 73c8157b582f4f3eed0550a0d59ca76eae45ce92
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097282"
---
# <a name="whats-new-in-ata-version-16"></a>Neuerungen in ATA 1.6

Die vorliegenden Anmerkungen zu dieser Version enthalten Informationen zu bekannten Problemen in dieser Version von Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-16-update"></a>Neuerungen beim Update auf ATA 1.6

Das Update auf ATA 1.6 bietet Verbesserungen in folgenden Bereichen:

- Neue Erkennungen

- Verbesserungen an vorhandenen Erkennungen
- Das ATA-Lightweight-Gateway
- Automatische Aktualisierungen
- Verbesserte ATA Center-Leistung
- Niedrigere Speicheranforderungen
- Unterstützung für IBM QRadar

### <a name="new-detections"></a>Neue Erkennungen

- **Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit**  
Datenschutz-API (Data Protection AP, DPAPI) ist ein kennwortbasierter Datenschutzdienst. Dieser Schutzdienst wird von verschiedenen Anwendungen verwendet, in denen Geheimnisse des Benutzers gespeichert werden, z. b. Website Kennwörter und Anmelde Informationen für Dateifreigabe. Um Szenarios mit Kennwortverlust zu unterstützen, können Benutzer geschützte Daten mithilfe eines Wiederherstellungsschlüssels entschlüsseln, der nichts mit dem jeweiligen Kennwort zu tun hat. In einer Domänenumgebung können externe Angreifer den Wiederherstellungsschlüssel stehlen und diesen dazu verwenden, geschützte Daten auf allen zur Domäne gehörenden Computern zu entschlüsseln.

- **net session-Enumeration**  
Reconnaissance ist eine Hauptstufe in der erweiterten Kette der Angriffsabwehr. Domänencontroller (DCs) fungieren als Dateiserver für die Verteilung von Gruppenrichtlinienobjekten über das SMB-Protokoll (Server Message Block). Angreifer können im Rahmen der Reconnaissancephase den DC für alle aktiven SMB-Sitzungen auf dem Server abfragen. So erhalten sie Zugriff auf alle Benutzer und IP-Adressen, die diesen SMB-Sitzungen zugeordnet sind. SMB-Sitzungsenumeration kann von Angreifern verwendet werden, auf vertrauliche Konten abzuzielen, wodurch sie sich quer (seitlich) durch das Netzwerk bewegen können.

- **Böswillige Replikationsanforderungen**  
In Active Directory-Umgebungen erfolgt Replikation regelmäßig zwischen Domänencontrollern. Ein Angreifer kann für eine Active Directory-Replikationsanforderung (die manchmal die Identität eines Domänencontrollers annimmt) einen unzulässigen Vorgang durchführen. Mit diesem unzulässigen Vorgang kann der Angreifer die in Active Directory gespeicherten Daten abrufen, einschließlich Kennworthashes, ohne auffallendere Verfahren wie Volumeschattenkopien zu nutzen.

- **Erkennung des MS11-013-Sicherheitsrisikos**  
Es gibt eine Sicherheitsrisiko bei Rechteerweiterungen in Kerberos, wodurch bestimmte Aspekte eines Kerberos-Diensttickets gefälscht werden können. Ein böswilliger Benutzer oder ein Angreifer, der dieses Sicherheitsrisiko Anfälligkeiten erfolgreich ausnutzt, kann ein Token mit erhöhten Rechten auf dem Domänencontroller abrufen.

- **Ungewöhnliche Protokollimplementierung**  
Authentifizierungsanforderungen (Kerberos oder NTLM) erfolgen in der Regel über einen standardmäßigen Satz von Methoden und Protokollen. Für eine erfolgreiche Authentifizierung muss die Anforderung jedoch nur einen bestimmten Satz von Anforderungen erfüllen. Angreifer können diese Protokolle mit geringfügigen Abweichungen von der Standardimplementierung in der Umgebung implementieren. Diese Abweichungen können auf die Anwesenheit eines Angreifers hindeuten, der versucht, Angriffe wie z.B. Pass-The-Hash oder Brute-Force auszuführen.

### <a name="improvements-to-existing-detections"></a>Verbesserungen an vorhandenen Erkennungen

ATA-1.6 enthält verbesserte Erkennungslogik, die falsch positive und falsch negative Szenarios für vorhandene Erkennungen wie Golden Ticket, Honeytoken, Brute-Force und Remoteausführung verringert.

### <a name="the-ata-lightweight-gateway"></a>Das ATA-Lightweight-Gateway

Ab dieser Version von ATA gibt es eine neue Bereitstellungsoption für das ATA-Gateway, die es ermöglicht, ein ATA-Gateway direkt auf dem Domänencontroller zu installieren. Diese Bereitstellungsoption entfernt nicht kritische Funktionalität des ATA-Gateways und führt dynamische Ressourcenverwaltung entsprechend den auf dem DC verfügbaren Ressourcen ein. Dadurch ist sicherstellt, dass die vorhandenen Vorgänge des DCs nicht betroffen sind. Das ATA-Lightweight-Gateway reduziert die Kosten der ATA-Bereitstellung. Gleichzeitig vereinfacht es die Bereitstellung in Filialstandorten, in denen es begrenzte Hardwareressourcen oder keine Möglichkeit gibt, Unterstützung für Portspiegelung einzurichten.
Weitere Informationen zum ATA-Lightweight-Gateway finden Sie unter [ATA-Architektur](ata-architecture.md#ata-gateway-and-ata-lightweight-gateway).

Weitere Informationen zu Bereitstellungsüberlegungen und zum Auswählen des für Sie richtigen Gatewaytyps finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment).

### <a name="automatic-updates"></a>Automatische Aktualisierungen

Ab Version 1.6 kann ATA Center mit Microsoft Update aktualisiert werden. Darüber hinaus können die ATA-Gateways jetzt automatisch aktualisiert werden, wobei deren Standardkommunikationskanal zu ATA Center verwendet wird.

### <a name="improved-ata-center-performance"></a>Verbesserte ATA Center-Leistung

Ab dieser Version ermöglichen eine kleinere Datenbanklast und ein effizienteres Ausführen aller Erkennungen, dass viel mehr Domänencontroller mit einem einzigen ATA Center überwacht werden können.

### <a name="lower-storage-requirements"></a>Niedrigere Speicheranforderungen

ATA 1.6 erfordert erheblich weniger Speicherplatz zum Ausführen der ATA-Datenbank: Es erfordert nur noch 20 % des Speicherplatzes, der in früheren Versionen verwendet wird.

### <a name="support-for-ibm-qradar"></a>Unterstützung für IBM QRadar

ATA kann Ereignisse von IBMs SIEM-Lösung QRadar zusätzlich zu den zuvor unterstützten SIEM-Lösungen empfangen.

## <a name="known-issues"></a>Bekannte Probleme

In dieser Version bestehen die folgenden bekannten Probleme.

### <a name="failure-to-recognize-new-path-in-manually-moved-databases"></a>Fehler beim Erkennen eines neuen Pfads in manuell verschobenen Datenbanken

In Bereitstellungen, in denen der Datenbankpfad manuell verschoben wird, verwendet die ATA-Bereitstellung nicht den neuen Datenbankpfad für die Aktualisierung. Dieser manuell verschobene Datenbankpfad kann folgende Probleme verursachen:

- ATA verwendet möglicherweise den gesamten freien Speicherplatz auf dem Systemlaufwerk von ATA Center, ohne alte Netzwerkaktivitäten regelmäßig zu löschen.

- Beim Aktualisieren von ATA auf Version 1.6 tritt bei den vorbereitenden Bereitschaftsprüfungen möglicherweise ein Fehler auf (siehe folgende Abbildung).

    ![Fehler bei Bereitschaftsprüfung](media/ata_failed_readinesschecks.png)

    > [!IMPORTANT]
    > Vor der Aktualisierung von ATA auf Version 1.6 müssen Sie den folgenden Registrierungsschlüssel mit dem richtigen Datenbankpfad aktualisieren: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath`

### <a name="migration-failure-when-updating-from-ata-15"></a>Migrationsfehler, wenn von ATA 1.5 aktualisiert wird

Beim Aktualisieren auf ATA 1.6 kann der Aktualisierungsvorgang mit dem folgenden Fehlercode fehlschlagen:

![Fehler beim Aktualisieren auf ATA 1.6](http://i.imgur.com/QrLSApr.png)

Wenn dieser Fehler angezeigt wird, überprüfen Sie das Bereitstellungs Protokoll in: **c:\Users \<User> \AppData\Local\Temp**, und suchen Sie nach der folgenden Ausnahme:

```
System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> MongoDB.Driver.MongoWriteException: A write operation resulted in an error. E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : "<guid>" } ---> MongoDB.Driver.MongoBulkWriteException`1: A bulk write operation resulted in one or more errors.  E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : " <guid> " }
```

Darüber hinaus wird möglicherweise folgender Fehler angezeigt:

```
System.ArgumentNullException: Value cannot be null.
```

Wenn einer dieser Fehler angezeigt wird, führen Sie die folgenden Schritte zur Problemumgehung aus:

**Problemumgehung**:

1. Verschieben Sie den Ordner „data_old“ in einen temporären Ordner (befindet sich normalerweise in „%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin“).
1. Deinstallieren Sie ATA Center 1.5, und löschen Sie alle Datenbankdaten.
![Deinstallieren von ATA 1.5](http://i.imgur.com/x4nJycx.png)
1. Installieren Sie ATA Center 1.5 erneut. Verwenden Sie dieselbe Konfiguration wie bei der vorherigen ATA 1.5-Installation (Zertifikate, IP-Adressen, Datenbankpfad usw.).
1. Beenden Sie diese Dienste in der folgenden Reihenfolge:
    1. Microsoft Advanced Threat Analytics Center
    2. MongoDB
1. Ersetzen Sie die MongoDB-Datenbankdateien durch die Dateien im Ordner "data_old".
1. Starten Sie diese Dienste in der folgenden Reihenfolge:
    1. MongoDB
    2. Microsoft Advanced Threat Analytics Center
1. Überprüfen Sie die Protokolle, um sich zu vergewissern, dass das Produkt ohne Fehler ausgeführt wird.
1. [Laden](/samples/browse/?redirectedfrom=TechNet-Gallery "Herunterladen") Sie das Tool "RemoveDuplicateProfiles.exe" herunter, und kopieren Sie es in den Haupt Installationspfad (%ProgramFiles%\Microsoft Advanced Threat analytics\center).
1. Führen Sie `RemoveDuplicateProfiles.exe` von einer Eingabeaufforderung mit erhöhten Rechten aus, und warten Sie, bis das Tool erfolgreich abgeschlossen wurde.
1. Hier: `…\Microsoft Advanced Threat Analytics\Center\MongoDB\bin` Directory: **Mongo ATA**, geben Sie den folgenden Befehl ein:

```dos
db.SuspiciousActivities.remove({ "_t" : "RemoteExecutionSuspiciousActivity", "DetailsRecords" : { "$elemMatch" : { "ReturnCode" : null } } }, { "_id" : 1 });
```

![Problemumgehung beim Update](http://i.imgur.com/Nj99X2f.png)

Es sollte ein zurückgegeben werden `WriteResult({ "nRemoved" : XX })` , wobei "XX" die Anzahl der gelöschten verdächtigen Aktivitäten ist. Wenn der Wert größer als 0 ist, beenden Sie die Eingabeaufforderung, und fahren Sie mit dem Updatevorgang fort.

### <a name="net-framework-461-requires-restarting-the-server"></a>.NET Framework 4.6.1 erfordert einen Neustart des Servers

![.NET Framework-Neustart](media/ata-net-framework-restart.png)

### <a name="historical-network-activities-no-longer-migrated"></a>Frühere Netzwerkaktivitäten werden nicht mehr migriert

Diese Version von ATA umfasst eine verbesserte Erkennungs-Engine, das eine genauere Erkennung bietet und viele falsch positive Szenarien eliminiert, insbesondere für Pass-the-Hash.
Für die neue und verbesserte Erkennungs-Engine wird Inline-Erkennungstechnologie genutzt, die eine Erkennung ohne Auswertung früherer Netzwerkaktivitäten ermöglicht, um die Leistung von ATA Center erheblich zu erhöhen. Dies bedeutet auch, dass es nicht erforderlich ist, frühere Netzwerkaktivitäten während des Aktualisierungsvorgangs zu migrieren.
Im ATA-Aktualisierungsvorgang werden die Daten für den Fall, dass Sie diese für zukünftige Untersuchungen benötigen, als JSON-Datei in `<Center Installation Path>\Migration` exportiert.

## <a name="see-also"></a>Siehe auch

[Sehen Sie sich das ATA-Forum an!](https://social.technet.microsoft.com/Forums/security/home?forum=mata) 
 [Aktualisieren von ATA auf Version 1,6: Migrations Handbuch](ata-update-1.6-migration-guide.md)