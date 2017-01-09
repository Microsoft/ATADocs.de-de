---
title: Neuigkeiten in ATA Version 1.5 | Microsoft Docs
description: "Listet Neuerungen sowie bekannte Probleme in ATA 1.5 auf."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: 4130f19c828045327d9d439059a2beda9bca13dc


---

# <a name="whats-new-in-ata-version-15"></a>Neuerungen in ATA 1.5
Die vorliegenden Anmerkungen zu dieser Version enthalten Informationen zu bekannten Problemen in dieser Version von Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-15-update"></a>Neuerungen beim Update auf ATA 1.5
Das Update auf ATA 1.5 bietet Verbesserungen in folgenden Bereichen:

-   Schnellere Erkennung

-   Verbesserter automatischer Erkennungsalgorithmus für NAT-Geräte (Network Address Translation, Netzwerkadressübersetzung)

-   Verbessertes Namensauflösungsverfahren für nicht mit einer Domäne verbundene Geräte

-   Unterstützung für die Datenmigration während Produktupdates

-   Bessere Reaktionsfähigkeit der Benutzeroberfläche auf verdächtige Aktivitäten mit Tausenden von beteiligten Entitäten

-   Verbesserte automatische Auflösung von Überwachungswarnungen

-   Zusätzliche Leistungsindikatoren für die erweiterte Überwachung und Problembehandlung

## <a name="known-issues"></a>Bekannte Probleme
In dieser Version bestehen die folgenden bekannten Probleme.

### <a name="new-ata-gateway-installation-fails"></a>Installation eines neuen ATA-Gateways schlägt fehl
Nach dem Update der ATA-Bereitstellung auf ATA 1.5 erhalten Sie beim Installieren eines neuen ATA-Gateways die folgende Fehlermeldung: Microsoft Advanced Threat Analytics-Gateway ist nicht installiert.

![ATA-GW-Fehler](media/ata-install-error.png)

<b>Problemumgehung:</b> Senden Sie eine E-Mail an <ataeval@microsoft.com>, um Schritte zur Problemumgehung anzufordern.
### <a name="deployment"></a>Bereitstellung
Der angegebene Ordner für „Datenbankdatenpfad“ und „Datenbankjournalpfad“ muss leer sein (keine Dateien oder Unterordner).
Wenn er nicht leer ist, wird die Bereitstellung nicht fortgesetzt.

### <a name="installation-from-zip-file"></a>Installation über ZIP-Datei
Stellen Sie beim Installieren des ATA-Gateways sicher, dass Sie die Dateien aus der ZIP-Datei in ein lokales Verzeichnis extrahieren und von dort aus installieren. Installieren Sie das ATA-Gateway nicht direkt aus der ZIP-Datei, da andernfalls die Installation fehlschlägt.

### <a name="configuration"></a>Konfiguration
Nachdem die Konfiguration für ein ATA-Gateway festgelegt wurde, wird beim ersten Starten des ATA-Gateways die Bezeichnung „Nicht synchronisiert“ angezeigt, bis der Dienst vollständig gestartet wurde. Dies kann beim ersten Starten des Diensts bis zu 10 Minuten dauern.

### <a name="network-capture-software"></a>Software zur Netzwerkerfassung
Auf dem ATA-Gateway ist der [Microsoft-Netzwerkmonitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) die einzige unterstützte Software zur Netzwerkerfassung, die installiert werden kann. Installieren Sie nicht Microsoft Message Analyzer oder eine andere Software zur Netzwerkerfassung. Die Installation anderer Software führt dazu, dass das ATA-Gateway nicht mehr ordnungsgemäß funktioniert.

### <a name="kb-on-virtualization-host"></a>KB auf Virtualisierungshost
Installieren Sie KB3047154 nicht auf einem Virtualisierungshost. Dies kann dazu führen, dass die Portspiegelung nicht mehr ordnungsgemäß ausgeführt wird.

## <a name="see-also"></a>Weitere Informationen

[Aktualisieren von ATA auf Version 1.5 – Migrationsleitfaden](ata-update-1.5-migration-guide.md)

[Aktualisieren von ATA auf Version 1.6 – Migrationsleitfaden](ata-update-1.6-migration-guide.md)

[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jan17_HO1-->


