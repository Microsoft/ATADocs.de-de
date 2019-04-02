---
title: Exportieren und Importieren der Advanced Threat Analytics-Konfiguration | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie die ATA-Konfiguration exportieren und importieren.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cc62b556cc27e363a0d37260d80fda4a7bfdd105
ms.sourcegitcommit: 62b631f64a639f5df04bf805755f26c69b40e8e4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638795"
---
# <a name="export-and-import-the-ata-configuration"></a>Exportieren und Importieren der ATA-Konfiguration

*Gilt für: Advanced Threat Analytics Version 1.9*

Die Konfiguration von ATA ist in der Sammlung „SystemProfile“ in der Datenbank gespeichert.
Diese Sammlung wird vom ATA Center-Dienst alle 4 Stunden in Dateien mit folgendem Namen gespeichert: **SystemProfile_*Zeitstempel*.json**. Die 300 neuesten Versionen werden gespeichert.
Diese Datei befindet sich im Unterordner **Backup**. Beim ATA-Standardinstallationsspeicherort lautet der Pfad:  <em>C:\Programme\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_</em>Zeitstempel<em>.json</em>. 

**Hinweis**: Wenn Sie größere Änderungen an ATA vornehmen, wird empfohlen, eine Sicherung dieser Datei zu erstellen.

Sie können alle Einstellungen wiederherstellen, indem Sie den folgenden Befehl ausführen:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Weitere Informationen
- [ATA-Architektur](ata-architecture.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

