---
title: Problembehandlung bei Advanced Threat Analytics mithilfe der Protokolle
description: Beschreibt die Verwendung der ATA-Protokolle zum Behandeln von Problemen.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 8/27/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 49bf3e2e4e69d01713c57b48aea6b55ffab6b36b
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94689988"
---
# <a name="troubleshooting-ata-using-the-ata-logs"></a>Behandeln von Problemen mit ATA mithilfe der ATA-Protokolle

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Die ATA-Protokolle geben Einblick in die Aktivitäten der einzelnen Komponenten von ATA zu einem bestimmten Zeitpunkt.

## <a name="ata-gateway-logs"></a>Protokolle des ATA-Gateways
In diesem Abschnitt gilt jeder Verweis auf das ATA-Gateway ebenfalls für das ATA-Lightweight-Gateway. 

Die Protokolle des ATA-Gateways befinden sich in einem Unterordner mit dem Namen **Logs** , in dem ATA installiert ist. der Standard Speicherort ist: **c:\Programme\Microsoft Advanced Threat Analytics \\**. Der Standard Speicherort für die Installation finden Sie unter: **c:\Programme\Microsoft Advanced Threat analytics\gateway\logs**.

Für das ATA-Gateway sind folgende Protokolle verfügbar:

-   **Microsoft.Tri.Gateway.log:** Dieses Protokoll enthält alle Aktivitäten im ATA-Gateway (einschließlich Auflösung und Fehlern). Sein Hauptverwendungszweck besteht im Abrufen des Gesamtstatus aller Vorgänge in ihrer zeitlichen Reihenfolge.

-   **Microsoft.Tri.Gateway-Resolution.log:** Dieses Protokoll enthält die Auflösungsdetails der vom ATA-Gateway im Datenverkehr ermittelten Entitäten. Sein Hauptverwendungszweck besteht im Untersuchen von Auflösungsproblemen bei Entitäten.

-   **Microsoft.Tri.Gateway-Errors.log:** Dieses Protokoll enthält nur die Fehler, die vom ATA-Gateway abgefangen werden. Sein Hauptverwendungszweck besteht im Ausführen von Integritätsprüfungen und Untersuchen von Problemen, die zu bestimmten Zeiten korreliert werden müssen.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log:** In diesem Protokoll werden alle ähnlichen Fehler und Ausnahmen zusammengefasst und ihre Anzahl gemessen.
    Diese Datei ist bei jedem Start des ATA-Gatewaydiensts leer und wird jede Minute aktualisiert. Sein Hauptverwendungszweck besteht im Ermitteln, ob neue Fehler oder Probleme mit dem ATA-Gateway aufgetreten sind. Die Gruppierung der Fehler erleichtert das Lesen und die Feststellung, ob neue Probleme hinzugekommen sind.
- **Microsoft.Tri.Gateway.Updater.log:** Dieses Protokoll wird für den Updateprozess des Gateways verwendet, das für das Aktualisieren des ATA-Gateways verantwortlich ist, wenn es für ein automatisches Update konfiguriert wurde. Der Updateprozess des Gateways ist auch für die Ressourcenbeschränkungen des ATA-Lightweight-Gateways verantwortlich.
- **Microsoft.Tri.Gateway.Updater-ExceptionStatistics.log:** In diesem Protokoll werden alle ähnlichen Fehler und Ausnahmen zusammengefasst und ihre Anzahl gemessen. Diese Datei ist bei jedem Start des ATA-Updatediensts leer und wird jede Minute aktualisiert. Mithilfe dieser Datei können Sie bestimmen, ob neue Fehler oder Probleme mit dem ATA-Updatedienst vorliegen. Die Fehler werden gruppiert, um schneller festzustellen, ob neue Fehler oder Probleme erkannt wurden.

> [!NOTE]
> Die ersten drei Protokolldateien haben eine maximale Größe von 50 MB. Wenn diese Größe erreicht ist, wird eine neue Protokolldatei geöffnet und die vorherige Datei in „&lt;Ursprünglicher Dateiname&gt;-Archived-00000“ umbenannt. Die Zahl erhöht sich bei jeder Umbenennung der Datei. Wenn bereits mehr als 10 Dateien des gleichen Typs vorhanden sind, werden die ältesten gelöscht.

## <a name="ata-center-logs"></a>Protokolle von ATA Center
Die Protokolle von ATA Center befinden sich im Unterordner **Logs**. Dieser ist im Standardinstallationsverzeichnis unter **C:\Programme\Microsoft Advanced Threat Analytics\Center\Logs** zu finden.
> [!Note]
> Die ATA-Konsolenprotokolle, die früher unter den IIS-Protokollen gespeichert wurden, befinden sich nun bei den ATA Center-Protokollen.

Für ATA Center sind folgende Protokolle verfügbar:

-   **Microsoft.Tri.Center.log:** Dieses Protokoll enthält alle Aktivitäten in ATA Center (einschließlich Erkennungen und Fehlern). Sein Hauptverwendungszweck besteht im Abrufen des Gesamtstatus aller Vorgänge in ihrer zeitlichen Reihenfolge.

-   **Microsoft.Tri.Center-Detection.log:** Dieses Protokoll enthält nur die Erkennungsdetails von ATA Center. Sein Hauptverwendungszweck besteht im Untersuchen von Problemen bei der Erkennung.

-   **Microsoft.Tri.Center-Errors.log:** Dieses Protokoll enthält nur die Fehler, die von ATA Center abgefangen werden. Sein Hauptverwendungszweck besteht im Ausführen von Integritätsprüfungen und Untersuchen von Problemen, die zu bestimmten Zeiten korreliert werden müssen.

-   **Microsoft.Tri.Center-ExceptionStatistics.log:** In diesem Protokoll werden alle ähnlichen Fehler und Ausnahmen zusammengefasst und ihre Anzahl gemessen.
    Diese Datei ist bei jedem Start des ATA Center-Diensts leer und wird jede Minute aktualisiert. Sein Hauptverwendungszweck besteht im Ermitteln, ob neue Fehler oder Probleme mit ATA Center aufgetreten sind. Die Gruppierung der Fehler erleichtert das Lesen und die Feststellung, ob neue Fehler oder Probleme hinzugekommen sind.

> [!NOTE]
> Die ersten drei Protokolldateien haben eine maximale Größe von 50 MB. Wenn diese Größe erreicht ist, wird eine neue Protokolldatei geöffnet und die vorherige Datei in „&lt;Ursprünglicher Dateiname&gt;-Archived-00000“ umbenannt. Die Zahl erhöht sich bei jeder Umbenennung der Datei. Wenn bereits mehr als 10 Dateien des gleichen Typs vorhanden sind, werden die ältesten gelöscht.


## <a name="ata-deployment-logs"></a>ATA-Bereitstellungsprotokolle
Die ATA-Bereitstellungsprotokolle befinden sich im temporären Verzeichnis des Benutzers, der das Produkt installiert hat. Der Standard Speicherort für die Installation finden Sie unter: **c:\Users \<logged-in-user> \AppData\Local\Temp** (oder ein Verzeichnis oberhalb von% Temp%).

Bereitstellungsprotokolle von ATA Center:

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS.log**: In diesem Protokoll sind die Schritte im Verfahren zur Bereitstellung von ATA Center aufgeführt. Sein Hauptverwendungszweck besteht im Nachverfolgen des Verfahrens zum Bereitstellen von ATA Center.

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS_0_MongoDBPackage.log**: In diesem Protokoll sind die Schritte im Verfahren zur Bereitstellung von MongoDB für ATA Center aufgeführt. Sein Hauptverwendungszweck besteht im Nachverfolgen des Verfahrens zum Bereitstellen von MongoDB.

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS_1_MsiPackage.log**: In dieser Protokolldatei sind die Schritte im Verfahren zur Bereitstellung der ATA Center-Binärdateien aufgeführt. Sein Hauptverwendungszweck besteht im Nachverfolgen der Bereitstellung der ATA Center-Binärdateien.

Bereitstellungsprotokolle für ATA-Gateway und ATA-Lightweight-Gateway:

-   **Microsoft Advanced Threat Analytics Gateway_YYYYMMDDHHMMSS.log**: In diesem Protokoll sind die Schritte im Verfahren zur Bereitstellung des ATA-Gateways aufgeführt. Sein Hauptverwendungszweck besteht im Nachverfolgen des Verfahrens zum Bereitstellen des ATA-Gateways.

-   **Microsoft Advanced Threat Analytics Gateway_YYYYMMDDHHMMSS_001_MsiPackage.log**: In dieser Protokolldatei sind die Schritte im Verfahren zur Bereitstellung der Binärdateien des ATA-Gateways aufgeführt. Sein Hauptverwendungszweck besteht im Nachverfolgen der Bereitstellung der Binärdateien des ATA-Gateways.


> [!NOTE] 
> Zusätzlich zu den hier erwähnten Bereitstellungsprotokollen gibt es andere Protokolle, die mit „Microsoft Advanced Threat Analytics“ beginnen und zusätzliche Informationen zum Bereitstellungsprozess bieten können.


## <a name="see-also"></a>Weitere Informationen
- [ATA-Voraussetzungen](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
