---
title: Behandeln von Problemen mit ATA mithilfe der ATA-Protokolle | Microsoft Advanced Threat Analytics
description: Beschreibt die Verwendung der ATA-Protokolle zum Behandeln von Problemen.
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 4f02b0fba381eb76ad500e198392ec7624a3028a


---

# Behandeln von Problemen mit ATA mithilfe der ATA-Protokolle
Die ATA-Protokolle geben Einblick in die Aktivitäten der einzelnen Komponenten von ATA zu einem bestimmten Zeitpunkt.

## Protokolle des ATA-Gateways
In diesem Abschnitt gilt jeder Verweis auf das ATA-Gateway ebenfalls für das ATA-Lightweight-Gateway. 

Die Protokolle des ATA-Gateways befinden sich im Unterordner **Logs**. Dieser ist im Standardinstallationsverzeichnis unter **C:\Programme\Microsoft Advanced Threat Analytics\Gateway\Logs** zu finden.

Für das ATA-Gateway sind folgende Protokolle verfügbar:

-   **Microsoft.Tri.Gateway.log:** Dieses Protokoll enthält alle Aktivitäten im ATA-Gateway (einschließlich Auflösung und Fehlern). Sein Hauptverwendungszweck besteht im Abrufen des Gesamtstatus aller Vorgänge in ihrer zeitlichen Reihenfolge.

-   **Microsoft.Tri.Gateway-Resolution.log:** Dieses Protokoll enthält die Auflösungsdetails der vom ATA-Gateway im Datenverkehr ermittelten Entitäten. Sein Hauptverwendungszweck besteht im Untersuchen von Auflösungsproblemen bei Entitäten.

-   **Microsoft.Tri.Gateway-Errors.log:** Dieses Protokoll enthält nur die Fehler, die vom ATA-Gateway abgefangen werden. Sein Hauptverwendungszweck besteht im Ausführen von Integritätsprüfungen und Untersuchen von Problemen, die zu bestimmten Zeiten korreliert werden müssen.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log:** In diesem Protokoll werden alle ähnlichen Fehler und Ausnahmen zusammengefasst und ihre Anzahl gemessen.
    Diese Datei ist bei jedem Start des ATA-Gatewaydiensts leer und wird jede Minute aktualisiert. Sein Hauptverwendungszweck besteht im Ermitteln, ob neue Fehler oder Probleme mit dem ATA-Gateway aufgetreten sind. Da die Fehler gruppiert sind, kann einfacher festgestellt werden, ob neue Typen von Fehlern oder Problemen vorliegen.

> [!NOTE]
> Die ersten drei Protokolldateien haben eine maximale Größe von 50 MB. Wenn diese Größe erreicht ist, wird eine neue Protokolldatei geöffnet und die vorherige Datei in „&lt;Ursprünglicher Dateiname&gt;-Archived-00000“ umbenannt. Die Zahl erhöht sich bei jeder Umbenennung der Datei.

## Protokolle von ATA Center
Die Protokolle von ATA Center befinden sich im Unterordner **Logs**. Dieser ist im Standardinstallationsverzeichnis unter **C:\Programme\Microsoft Advanced Threat Analytics\Center\Logs** zu finden.

Für ATA Center sind folgende Protokolle verfügbar:

-   **Microsoft.Tri.Center.log:** Dieses Protokoll enthält alle Aktivitäten in ATA Center (einschließlich Erkennungen und Fehlern). Sein Hauptverwendungszweck besteht im Abrufen des Gesamtstatus aller Vorgänge in ihrer zeitlichen Reihenfolge.

-   **Microsoft.Tri.Center-Detection.log:** Dieses Protokoll enthält nur die Erkennungsdetails von ATA Center. Sein Hauptverwendungszweck besteht im Untersuchen von Problemen bei der Erkennung.

-   **Microsoft.Tri.Center-Errors.log:** Dieses Protokoll enthält nur die Fehler, die von ATA Center abgefangen werden. Sein Hauptverwendungszweck besteht im Ausführen von Integritätsprüfungen und Untersuchen von Problemen, die zu bestimmten Zeiten korreliert werden müssen.

-   **Microsoft.Tri.Center-ExceptionStatistics.log:** In diesem Protokoll werden alle ähnlichen Fehler und Ausnahmen zusammengefasst und ihre Anzahl gemessen.
    Diese Datei ist bei jedem Start des ATA Center-Diensts leer und wird jede Minute aktualisiert. Sein Hauptverwendungszweck besteht im Ermitteln, ob neue Fehler oder Probleme mit ATA Center aufgetreten sind. Da die Fehler gruppiert sind, kann einfacher festgestellt werden, ob neue Typen von Fehlern oder Problemen vorliegen.

> [!NOTE]
> Die ersten drei Protokolldateien haben eine maximale Größe von 50 MB. Wenn diese Größe erreicht ist, wird eine neue Protokolldatei geöffnet und die vorherige Datei in „&lt;Ursprünglicher Dateiname&gt;-Archived-00000“ umbenannt. Die Zahl erhöht sich bei jeder Umbenennung der Datei.

## Protokolle der ATA-Konsole
Die Protokolle der ATA-Konsole (die Protokolle der Verwaltungs-API) befinden sich im Unterordner **Logs**. Dieser ist im Standardinstallationsverzeichnis unter **C:\Programme\Microsoft Advanced Threat Analytics\Center\Management\Logs** zu finden.

Für die ATA-Konsole sind folgende Protokolle verfügbar:

-   **w3wp.log:** Dieses Protokoll enthält alle Aktivitäten im Verwaltungsprozess (IIS).


-   **w3wp-Errors.log:** Dieses Protokoll enthält nur die Fehler, die vom Verwaltungsprozess (IIS) abgefangen werden.


-   **8e75f9f1-ExceptionStatistics.log:** In diesem Protokoll werden alle ähnlichen Fehler und Ausnahmen zusammengefasst und ihre Anzahl gemessen.
    Diese Datei ist bei jedem Start des Gatewaydiensts leer und wird jede Minute aktualisiert. Sein Hauptverwendungszweck besteht im Ermitteln, ob neue Fehler oder Probleme mit ATA Center aufgetreten sind. Da die Fehler gruppiert sind, kann einfacher festgestellt werden, ob neue Typen von Fehlern oder Problemen vorliegen.

> [!NOTE]
> Die ersten zwei Protokolldateien haben eine maximale Größe von 50 MB. Wenn diese Größe erreicht ist, wird eine neue Protokolldatei geöffnet und die vorherige Datei in „&lt;Ursprünglicher Dateiname&gt;-Archived-00000“ umbenannt. Die Zahl erhöht sich bei jeder Umbenennung der Datei.

## ATA-Bereitstellungsprotokolle
Die ATA-Bereitstellungsprotokolle befinden sich im temporären Verzeichnis des Benutzers, der das Produkt installiert hat. Es ist im Standardinstallationsverzeichnis unter **C:\Benutzer\Administrator\AppData\Local\Temp** (oder in dem „%temp%“ übergeordneten Verzeichnis) zu finden.

Bereitstellungsprotokolle von ATA Center:

-   **Microsoft Advanced Threat Analytics Center_20150601104213.log:** In diesem Protokoll sind die Schritte im Verfahren zur Bereitstellung von ATA Center aufgeführt. Sein Hauptverwendungszweck besteht im Nachverfolgen des Verfahrens zum Bereitstellen von ATA Center.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_0_MongoDBPackage.log:** In diesem Protokoll sind die Schritte im Verfahren zur Bereitstellung von MongoDB für ATA Center aufgeführt. Sein Hauptverwendungszweck besteht im Nachverfolgen des Verfahrens zum Bereitstellen von MongoDB.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_1_MsiPackage.log:** In dieser Protokolldatei sind die Schritte im Verfahren zur Bereitstellung der ATA Center-Binärdateien aufgeführt. Sein Hauptverwendungszweck besteht im Nachverfolgen der Bereitstellung der ATA Center-Binärdateien.

Bereitstellungsprotokolle für ATA-Gateway und ATA-Lightweight-Gateway:

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801.log:** In diesem Protokoll sind die Schritte im Verfahren zur Bereitstellung des ATA-Gateways aufgeführt. Sein Hauptverwendungszweck besteht im Nachverfolgen des Verfahrens zum Bereitstellen des ATA-Gateways.

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801_001_MsiPackage.log:** In dieser Protokolldatei sind die Schritte im Verfahren zur Bereitstellung der Binärdateien des ATA-Gateways aufgeführt. Sein Hauptverwendungszweck besteht im Nachverfolgen der Bereitstellung der Binärdateien des ATA-Gateways.

## Weitere Informationen
- [ATA-Voraussetzungen](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-Kapazitätsplanung](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurieren der Windows-Ereignisweiterleitung](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


