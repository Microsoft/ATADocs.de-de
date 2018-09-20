---
title: Exportieren und Importieren der Advanced Threat Analytics-Konfiguration | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie die ATA-Konfiguration exportieren und importieren.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3abe18d7da00e5af0373d74db2dc2dc1f91a6fc9
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133309"
---
*Gilt für: Advanced Threat Analytics Version 1.9*



# <a name="export-and-import-the-ata-configuration"></a>Exportieren und Importieren der ATA-Konfiguration
Die Konfiguration von ATA ist in der Sammlung „SystemProfile“ in der Datenbank gespeichert.
Diese Sammlung wird vom ATA Center-Dienst alle 4 Stunden in Dateien mit dem Namen **SystemProfile_*Zeitstempel*.json** gespeichert. Die 300 neuesten Versionen werden gespeichert.
Diese Datei befindet sich im Unterordner **Backup**. Im ATA-Standardinstallationsverzeichnis ist die Datei unter *C:\Programme\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_* Zeitstempel *.json* zu finden. 

**Hinweis**: Wenn Sie größere Änderungen an ATA vornehmen, wird empfohlen, eine Sicherung dieser Datei zu erstellen.

Sie können alle Einstellungen wiederherstellen, indem Sie den folgenden Befehl ausführen:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Weitere Informationen
- [ATA-Architektur](ata-architecture.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

