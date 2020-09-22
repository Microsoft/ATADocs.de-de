---
title: Exportieren und Importieren der Advanced Threat Analytics-Konfiguration
description: Erfahren Sie, wie Sie die ATA-Konfiguration exportieren und importieren.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e4f187610ada58c07afe90b23567353db29f1ac5
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90909203"
---
# <a name="export-and-import-the-ata-configuration"></a>Exportieren und Importieren der ATA-Konfiguration

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Die Konfiguration von ATA ist in der Sammlung „SystemProfile“ in der Datenbank gespeichert.
Diese Sammlung wird vom ATA Center-Dienst alle 4 Stunden in Dateien mit dem Namen **SystemProfile_*Zeitstempel*.json** gespeichert. Die 300 neuesten Versionen werden gespeichert.
Diese Datei befindet sich im Unterordner **Backup**. Im ATA-Standardinstallationsverzeichnis ist die Datei unter <em>C:\Programme\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_</em>Zeitstempel<em>.json</em> zu finden. 

**Hinweis**: Wenn Sie größere Änderungen an ATA vornehmen, wird empfohlen, eine Sicherung dieser Datei zu erstellen.

Sie können alle Einstellungen wiederherstellen, indem Sie den folgenden Befehl ausführen:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Weitere Informationen
- [ATA-Architektur](ata-architecture.md)
- [ATA-Voraussetzungen](ata-prerequisites.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

