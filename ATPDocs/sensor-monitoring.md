---
title: Überwachen von Domänen Controllern und installierten Sensoren auf Ihren Domänen Controllern mithilfe von Azure Advanced Threat Protection
description: In diesem Artikel wird beschrieben, wie Sie Azure ATP-Sensoren und die Sensorabdeckung mit Azure ATP überwachen.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 92decce8-b3ae-4d32-8407-a95314a66863
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ac4c0b9bd4e8a99d5edaaec2746f3ce7d413005c
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912557"
---
# <a name="monitoring-your-domain-controller-coverage"></a>Überwachen der Domänencontrollerabdeckung

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Sobald Sie den ersten Azure ATP-Sensor auf einem Domänencontroller in Ihrem Netzwerk installiert und konfiguriert haben, beginnt Azure ATP mit der Überwachung von Domänencontrollern in Ihrer Umgebung.

Sobald ein Azure ATP-Sensor für einen Domänencontroller in Ihrem Netzwerk installiert und konfiguriert wurde, kommuniziert der Sensor konstant mit dem Azure ATP-Dienst und sendet Status-, Integritäts- und Versionsinformationen sowie ermittelte Active Directory-Ereignisse und -Änderungen.

## <a name="domain-controller-status"></a>Domänencontrollerstatus

Azure ATP überwacht Ihre Umgebung kontinuierlich auf nicht überwachte Domänencontroller, die in Ihre Umgebung eingeführt werden, und berichtet über diese, um Sie bei der Verwaltung der vollständigen Abdeckung Ihrer Umgebung zu unterstützen.

1. Öffnen Sie den Bereich **Konfiguration** im Azure ATP-Portal, und wählen Sie **Sensoren** im Abschnitt **System** aus, um den Status der erkannten, überwachten und nicht überwachten Domänencontroller zu überprüfen.

    ![Überwachen des Status von Azure ATP-Sensoren](media/atp-sensors-status-monitoring.png)

1. Ihre derzeit überwachten und nicht überwachten Domänencontroller werden oben auf der Anzeige angezeigt. Klicken Sie auf **Details herunterladen**, um die Überwachungsstatusinformationen zu Ihren Domänencontrollern herunterzuladen.

Die heruntergeladene Excel-Datei zur Abdeckung der Domänencontroller stellt folgende Informationen für alle ermittelten Domänencontroller in Ihrer Organisation bereit:

|Titel|Beschreibung|
|----|----|
|Hostname|Computername|
|Domänenname|Domänenname|
|Monitored|Azure ATP-Überwachungsstatus|
|Sensortyp|Azure ATP-Sensor oder eigenständiger Azure ATP-Sensor|
|Organisationseinheit|Speicherort in Active Directory |
|Betriebssystemversion| Version des ermittelten Betriebssystems|
|IP-Adresse|Ermittelte IP-Adresse|

## <a name="search-domain-controllers"></a>Durchsuchen von Domänencontrollern

Die Verwaltung ihrer Flotte von Sensoren und Domänencontrollern kann eine Herausforderung darstellen. Um das Auffinden und Identifizieren zu vereinfachen, können Domänencontroller mithilfe der Suchfunktion in der Liste der Azure ATP-Sensoren durchsucht werden.

1. Wechseln Sie zum Durchsuchen Ihrer Domänencontroller zum Bereich **Konfiguration** des Azure ATP-Portals, und wählen Sie im Abschnitt **System** die Option **Sensoren** aus.
1. Wählen Sie in der Domänencontroller-Tabellenliste in der Spalte **Domänencontroller** die Filteroption aus.
1. Geben Sie den Namen ein, den Sie suchen möchten. Platzhalter werden im Suchfeld derzeit nicht unterstützt.

    ![Domänencontrollersuche in Azure ATP](media/search-sensor.png)

> [!NOTE]
> Die Konfigurationsseiten des Azure ATP-Portals können nur von Azure ATP-Administratoren bearbeitet werden.

## <a name="see-also"></a>Weitere Informationen

- [Azure ATP-Architektur](architecture.md)
- [Konfigurieren von Azure ATP-Sensoren](install-step5.md)
- [Azure Advanced Threat Protection-Unterstützung für mehrere Gesamtstrukturen](multi-forest.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)