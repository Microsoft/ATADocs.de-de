---
title: Überwachen von Domänen Controllern und installierten Sensoren, die auf Ihren Domänen Controllern mit Microsoft Defender für Identity
description: Enthält Informationen zum Überwachen von Microsoft Defender für Identitäts Sensoren und Sensor Abdeckung mithilfe von Defender für die Identität.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 20e02b3281480024b67a1ef5908d82586c11f955
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94849020"
---
# <a name="monitoring-your-domain-controller-coverage"></a>Überwachen der Domänencontrollerabdeckung

Sobald der erste [!INCLUDE [Product long](includes/product-long.md)] Sensor auf einem beliebigen Domänen Controller in Ihrem Netzwerk installiert und konfiguriert ist, [!INCLUDE [Product short](includes/product-short.md)] beginnt mit der Überwachung Ihrer Umgebung für Domänen Controller.

Nachdem ein [!INCLUDE [Product short](includes/product-short.md)] Sensor auf einem Domänen Controller in Ihrem Netzwerk installiert und konfiguriert wurde, kommuniziert der Sensor [!INCLUDE [Product short](includes/product-short.md)] auf konstanter Basis mit dem Dienst, um Sensor Status-, Integritäts-und Versionsinformationen zu senden und Active Directory Ereignisse und Änderungen zu erfassen.

## <a name="domain-controller-status"></a>Domänencontrollerstatus

[!INCLUDE [Product short](includes/product-short.md)] überwacht kontinuierlich Ihre Umgebung auf nicht überwachte Domänen Controller, die in Ihrer Umgebung eingeführt wurden, und meldet diese, um Sie bei der Verwaltung der vollständigen Abdeckung Ihrer Umgebung zu unterstützen.

1. Um den Status der erkannten überwachten und nicht überwachten Domänen Controller und deren Status zu überprüfen, wechseln Sie zum **Konfigurations** Bereich des [!INCLUDE [Product short](includes/product-short.md)] Portals, und wählen Sie im Abschnitt **System** die Option **Sensoren** aus.

    ![[! Überwachung von "[Product Short]" (includes/Produkt-Short. MD)]](media/sensors-status-monitoring.png)

1. Ihre derzeit überwachten und nicht überwachten Domänencontroller werden oben auf der Anzeige angezeigt. Klicken Sie auf **Details herunterladen**, um die Überwachungsstatusinformationen zu Ihren Domänencontrollern herunterzuladen.

Die heruntergeladene Excel-Datei zur Abdeckung der Domänencontroller stellt folgende Informationen für alle ermittelten Domänencontroller in Ihrer Organisation bereit:

|Titel|BESCHREIBUNG|
|----|----|
|Hostname|Computername|
|Domänenname|Domänenname|
|Monitored|[!INCLUDE [Product short](includes/product-short.md)] Überwachungs Status|
|Sensortyp|[!INCLUDE [Product short](includes/product-short.md)] Sensor oder [!INCLUDE [Product short](includes/product-short.md)] eigenständiger Sensor|
|Organisationseinheit|Speicherort in Active Directory |
|Betriebssystemversion| Version des ermittelten Betriebssystems|
|IP-Adresse|Ermittelte IP-Adresse|

## <a name="search-domain-controllers"></a>Durchsuchen von Domänencontrollern

Die Verwaltung ihrer Flotte von Sensoren und Domänencontrollern kann eine Herausforderung darstellen. Um die Suche und Identifizierung zu vereinfachen, können Domänen Controller mithilfe der Suchfunktion in der Liste der Sensoren durchsucht werden [!INCLUDE [Product short](includes/product-short.md)] .

1. Wechseln Sie zum Durchsuchen Ihrer Domänen Controller zum **Konfigurations** Bereich des [!INCLUDE [Product short](includes/product-short.md)] Portals, und wählen Sie im Abschnitt **System** die Option **Sensoren** aus.
1. Wählen Sie in der Domänencontroller-Tabellenliste in der Spalte **Domänencontroller** die Filteroption aus.
1. Geben Sie den Namen ein, den Sie suchen möchten. Platzhalter werden im Suchfeld derzeit nicht unterstützt.

    ![[! INCLUDE [Product Short] (includes/Produkt-Short. MD)] Domänen Controller suchen](media/search-sensor.png)

> [!NOTE]
> [!INCLUDE [Product short](includes/product-short.md)] Portal Konfigurationsseiten können nur von Administratoren geändert werden [!INCLUDE [Product short](includes/product-short.md)] .

## <a name="see-also"></a>Weitere Informationen

- [[!INCLUDE [Product short](includes/product-short.md)]-Architektur](architecture.md)
- [Konfigurieren von [!INCLUDE [Product short](includes/product-short.md)] Sensoren](install-step5.md)
- [Azure Advanced Threat Protection-Unterstützung für mehrere Gesamtstrukturen](multi-forest.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
