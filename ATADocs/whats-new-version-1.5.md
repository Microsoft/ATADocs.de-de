---
title: Neues in Advanced Threat Analytics Version 1,5
description: Listet Neuerungen sowie bekannte Probleme in ATA 1.5 auf.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 110632e0d2f2b14f57f7e7fbb63136dc8e8df1fa
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913326"
---
# <a name="whats-new-in-ata-version-15"></a>Neuerungen in ATA 1.5

[!INCLUDE [Rebranding notice](includes/rebranding.md)]
Die vorliegenden Anmerkungen zu dieser Version enthalten Informationen zu bekannten Problemen in dieser Version von Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-15-update"></a>Neuerungen beim Update auf ATA 1.5
Das Update auf ATA 1.5 bietet Verbesserungen in folgenden Bereichen:

- Schnellere Erkennung

- Verbesserter automatischer Erkennungsalgorithmus für NAT-Geräte (Network Address Translation, Netzwerkadressübersetzung)

- Verbessertes Namensauflösungsverfahren für nicht mit einer Domäne verbundene Geräte

- Unterstützung für die Datenmigration während Produktupdates

- Bessere Reaktionsfähigkeit der Benutzeroberfläche auf verdächtige Aktivitäten mit Tausenden von beteiligten Entitäten

- Verbesserte automatische Auflösung von Integritäts Warnungen

- Zusätzliche Leistungsindikatoren für die erweiterte Überwachung und Problembehandlung

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
Stellen Sie beim Installieren des ATA-Gateways sicher, dass Sie die Dateien aus der ZIP-Datei in ein lokales Verzeichnis extrahieren und von dort aus installieren. Installieren Sie das ATA-Gateway nicht direkt aus der ZIP-Datei, da dann ein Fehler bei der Installation auftritt.

### <a name="configuration"></a>Konfiguration
Nachdem die Konfiguration für ein ATA-Gateway festgelegt wurde, wird beim ersten Starten des ATA-Gateways die Bezeichnung „Nicht synchronisiert“ angezeigt, bis der Dienst vollständig gestartet wurde. Dies kann beim ersten Starten des Diensts bis zu 10 Minuten dauern.

### <a name="network-capture-software"></a>Software zur Netzwerkerfassung
Auf dem ATA-Gateway ist der [Microsoft-Netzwerkmonitor 3.4](https://www.microsoft.com/download/details.aspx?id=4865) die einzige unterstützte Software zur Netzwerkerfassung, die installiert werden kann. Installieren Sie nicht Microsoft Message Analyzer oder eine andere Software zur Netzwerkerfassung. Die Installation anderer Software führt dazu, dass das ATA-Gateway nicht mehr ordnungsgemäß funktioniert.

### <a name="kb-on-virtualization-host"></a>KB auf Virtualisierungshost
Installieren Sie KB3047154 nicht auf einem Virtualisierungshost. Dies kann dazu führen, dass die Portspiegelung nicht mehr ordnungsgemäß ausgeführt wird.

## <a name="see-also"></a>Weitere Informationen

[Aktualisieren von ATA auf Version 1.5 – Migrationsleitfaden](ata-update-1.5-migration-guide.md)

[Aktualisieren von ATA auf Version 1.6 – Migrationsleitfaden](ata-update-1.6-migration-guide.md)

[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
