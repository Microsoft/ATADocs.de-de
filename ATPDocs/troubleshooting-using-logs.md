---
title: Behandeln von Problemen mit Microsoft Defender für die Identität mithilfe der Protokolle
description: Beschreibt, wie Sie Microsoft Defender für Identitäts Protokolle verwenden können, um Probleme zu beheben.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: ''
ms.suite: ''
ms.openlocfilehash: ea19abd7497d0d925e764a80666dc595862566f9
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275000"
---
# <a name="troubleshooting-product-long-sensor-using-the-product-short-logs"></a>Problembehandlung bei [!INCLUDE [Product long](includes/product-long.md)] Sensor mithilfe der [!INCLUDE [Product short](includes/product-short.md)] Protokolle

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Die [!INCLUDE [Product short](includes/product-short.md)] Protokolle bieten Einblicke in die einzelnen Komponenten des [!INCLUDE [Product long](includes/product-long.md)] Sensors zu einem bestimmten Zeitpunkt.

Die [!INCLUDE [Product short](includes/product-short.md)] Protokolle befinden sich in einem Unterordner namens **Logs** , in dem [!INCLUDE [Product short](includes/product-short.md)] installiert ist. der Standard Speicherort ist: **c:\programme\azure Advanced Threat \\ Protection Sensor**. Dieser ist im Standardinstallationsverzeichnis unter **C:\Programme\Azure Advanced Threat Protection-Sensor\Versionsnummer\Logs** zu finden.

Der [!INCLUDE [Product short](includes/product-short.md)] Sensor verfügt über die folgenden Protokolle:

- **Microsoft. Tri. Sensor. log** – dieses Protokoll enthält alles, was im [!INCLUDE [Product short](includes/product-short.md)] Sensor passiert (einschließlich Auflösung und Fehlern). Sein Hauptverwendungszweck besteht im Abrufen des Gesamtstatus aller Vorgänge in ihrer zeitlichen Reihenfolge.

- **Microsoft. Tri. Sensor-Errors. log** – dieses Protokoll enthält nur die Fehler, die vom Sensor abgefangen werden [!INCLUDE [Product short](includes/product-short.md)] . Sein Hauptverwendungszweck besteht im Ausführen von Integritätsprüfungen und Untersuchen von Problemen, die zu bestimmten Zeiten korreliert werden müssen.

- **Microsoft. Tri. Sensor. Updater. log** : Dieses Protokoll wird für den Aktualisierungsprozess des Sensors verwendet, der für die Aktualisierung des Sensors zuständig ist, [!INCLUDE [Product short](includes/product-short.md)] Wenn er für eine automatische Konfiguration konfiguriert ist.

> [!NOTE]
> Die ersten drei Protokolldateien haben eine maximale Größe von 50 MB. Wenn diese Größe erreicht ist, wird eine neue Protokolldatei geöffnet und die vorherige Datei in „&lt;Ursprünglicher Dateiname&gt;-Archived-00000“ umbenannt. Die Zahl erhöht sich bei jeder Umbenennung der Datei. Wenn bereits mehr als 10 Dateien des gleichen Typs vorhanden sind, werden die ältesten gelöscht.

## <a name="product-short-deployment-logs"></a>[!INCLUDE [Product short](includes/product-short.md)] Bereitstellungs Protokolle

Die [!INCLUDE [Product short](includes/product-short.md)] Bereitstellungs Protokolle befinden sich im temporären Verzeichnis des Benutzers, der das Produkt installiert hat. Der Standard Speicherort für die Installation finden Sie unter: **C:\Users\Administrator\AppData\Local\Temp** (oder in einem Verzeichnis oberhalb von% Temp%).

[!INCLUDE [Product short](includes/product-short.md)] Sensor Bereitstellungs Protokolle:

- **Azure Advanced Threat Protection Microsoft.Tri.Sensor.Deployment.Deployer_YYYYMMDDHHMMSS.log** : Diese Protokolldatei enthält den gesamten Prozess der Sensorbereitstellung und befindet sich in dem oben erwähnten temporären Ordner oder unter „C:\Windows\Temp“.

- **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS. log** : in diesem Protokoll sind die Schritte im Prozess der Bereitstellung des [!INCLUDE [Product short](includes/product-short.md)] Sensors aufgeführt. Die Hauptverwendung besteht darin, den [!INCLUDE [Product short](includes/product-short.md)] Prozess der Sensor Bereitstellung zu verfolgen.

- **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS_001_MsiPackage. log** : in dieser Protokolldatei sind die Schritte im Prozess der Bereitstellung der [!INCLUDE [Product short](includes/product-short.md)] Sensor Binärdateien aufgeführt. Der Haupt Verwendungs Grund ist das Nachverfolgen der Bereitstellung der [!INCLUDE [Product short](includes/product-short.md)] Sensor Binärdateien.

> [!NOTE]
> Zusätzlich zu den hier erwähnten Bereitstellungsprotokollen gibt es andere Protokolle, die mit „Azure Advanced Threat Protection“ beginnen und zusätzliche Informationen zum Bereitstellungsprozess bieten können.

## <a name="see-also"></a>Weitere Informationen

- [[!INCLUDE [Product short](includes/product-short.md)] Voraussetzung](prerequisites.md)
- [[!INCLUDE [Product short](includes/product-short.md)] Kapazitätsplanung](capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Sehen Sie sich das [!INCLUDE [Product short](includes/product-short.md)] Forum an!](https://aka.ms/MDIcommunity)
