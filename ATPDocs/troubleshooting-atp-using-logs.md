---
title: Problembehandlung für Azure Advanced Threat Protection mithilfe der Protokolle | Microsoft-Dokumentation
description: Beschreibt die Verwendung der Azure ATP-Protokolle zum Behandeln von Problemen.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/13/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de796346-647d-48e1-970a-8f072e990f1e
ms.reviewer: ''
ms.suite: ''
ms.openlocfilehash: 4cac2722bcfaf51996b201d379991dc335bcf371
ms.sourcegitcommit: dc56b9e9533db1a2dc314b199e90191bb25adaba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/14/2018
ms.locfileid: "40102335"
---
*Gilt für: Advanced Threat Protection*



# <a name="troubleshooting-azure-advanced-threat-protection-atp-sensor-using-the-atp-logs"></a>Problembehandlung für den Azure Advanced Threat Protection-Sensor (ATP) mithilfe der ATP-Protokolle
Die ATA-Protokolle geben Einblick in die Aktivitäten der einzelnen Komponenten des Azure ATP-Sensors zu einem bestimmten Zeitpunkt.


Die Protokolle von Azure ATP befinden sich im Unterordner **Logs** im Installationsordner von ATP. Der Standardpfad lautet: **C:\Programme\Azure Advanced Threat Protection-Sensor\\**. Dieser ist im Standardinstallationsverzeichnis unter **C:\Programme\Azure Advanced Threat Protection-Sensor\Versionsnummer\Logs** zu finden.

Der Azure ATP-Sensor verfügt über folgende Protokolle:

-   **Microsoft.Tri.Sensor.log:** Dieses Protokoll enthält alle Aktivitäten im Azure ATP-Sensor (einschließlich Auflösung und Fehlern). Sein Hauptverwendungszweck besteht im Abrufen des Gesamtstatus aller Vorgänge in ihrer zeitlichen Reihenfolge.

-   **Microsoft.Tri.Sensor-Resolution.log:** Dieses Protokoll enthält die Auflösungsdetails der vom ATP-Sensor im Datenverkehr ermittelten Entitäten. Sein Hauptverwendungszweck besteht im Untersuchen von Auflösungsproblemen bei Entitäten.

-   **Microsoft.Tri.Sensor-Errors.log:** Dieses Protokoll enthält nur die Fehler, die vom ATP-Sensor abgefangen werden. Sein Hauptverwendungszweck besteht im Ausführen von Integritätsprüfungen und Untersuchen von Problemen, die zu bestimmten Zeiten korreliert werden müssen.

-   **Microsoft.Tri.Sensor.Updater.log:** Dieses Protokoll wird für den Updateprozess des Sensors verwendet, der für das Aktualisieren des ATP-Sensors verantwortlich ist, wenn er dafür konfiguriert wurde. 


> [!NOTE]
> Die ersten drei Protokolldateien haben eine maximale Größe von 50 MB. Wenn diese Größe erreicht ist, wird eine neue Protokolldatei geöffnet und die vorherige Datei in „&lt;Ursprünglicher Dateiname&gt;-Archived-00000“ umbenannt. Die Zahl erhöht sich bei jeder Umbenennung der Datei. Wenn bereits mehr als 10 Dateien des gleichen Typs vorhanden sind, werden die ältesten gelöscht.

## <a name="azure-atp-deployment-logs"></a>Azure ATP-Bereitstellungsprotokolle
Die Azure ATP-Bereitstellungsprotokolle befinden sich im temporären Verzeichnis des Benutzers, der das Produkt installiert hat. Es ist im Standardinstallationsverzeichnis unter **C:\Benutzer\Administrator\AppData\Local\Temp** (oder in dem „%temp%“ übergeordneten Verzeichnis) zu finden.

Bereitstellungsprotokolle für den Azure ATP-Sensor:

-   **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS.log**: In diesem Protokoll sind die Schritte im Verfahren zur Bereitstellung des Azure ATP-Sensors aufgeführt. Sein Hauptverwendungszweck besteht im Nachverfolgen des Verfahrens zum Bereitstellen des Azure ATP-Sensors.

-   **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS_001_MsiPackage.log**: In dieser Protokolldatei sind die Schritte im Bereitstellungsprozess der Azure ATP-Sensor-Binärdateien aufgeführt. Ihr Hauptverwendungszweck besteht im Nachverfolgen der Bereitstellung der Azure ATP-Sensor-Binärdateien.


> [!NOTE] 
> Zusätzlich zu den hier erwähnten Bereitstellungsprotokollen gibt es andere Protokolle, die mit „Azure Advanced Threat Protection“ beginnen und zusätzliche Informationen zum Bereitstellungsprozess bieten können.


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)