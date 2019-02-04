---
title: Überwachen von Domänencontrollern und darauf installierten Sensoren mit Azure Advanced Threat Protection | Microsoft-Dokumentation
description: In diesem Artikel wird beschrieben, wie Sie Azure ATP-Sensoren und die Sensorabdeckung mit Azure ATP überwachen.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/27/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 92decce8-b3ae-4d32-8407-a95314a66863
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6dd6574250819bd8c60da00c7f1547bb34845f75
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085522"
---
# <a name="monitoring-your-domain-controller-coverage"></a>Überwachen der Domänencontrollerabdeckung

Sobald Sie Ihren ersten Azure ATP-Sensor auf einem Domänencontroller in Ihrem Netzwerk installiert und konfiguriert haben, beginnt Azure ATP mit der Überwachung von Domänencontroller in Ihrer Umgebung. 

Währen des Setups wird empfohlen, pro Domäne mindestens einen Domänencontroller als Domänensynchronizerkandidat festzulegen. Zu den Aufgaben des Domänensynchronizersensors gehört das Sicherstellen, dass dieser spezifische Sensor aktiv nach Domänencontrollern sucht. Sie können den Domänencontroller für den Domänensynchronizerkandidat nach der Erstkonfiguration wechseln. Weitere Informationen zum Konfigurieren eines Azure-Sensors und zum Festlegen als **Domänensynchronizerkandidat** finden Sie unter [Konfigurieren von Azure ATP-Sensoren](install-atp-step5.md). 

Sobald ein Azure ATP-Sensor für einen Domänencontroller in Ihrem Netzwerk installiert und konfiguriert wurde, kommuniziert der Sensor konstant mit dem Azure ATP-Dienst und sendet Status-, Integritäts- und Versionsinformationen sowie ermittelte Active Directory-Ereignisse und -Änderungen.  

### <a name="domain-controller-status"></a>Domänencontrollerstatus

Azure ATP überwacht Ihre Umgebung kontinuierlich auf nicht überwachte Domänencontroller, die in Ihre Umgebung eingeführt werden, und berichtet über diese, um Sie bei der Verwaltung der vollständigen Abdeckung Ihrer Umgebung zu unterstützen. 

1. Öffnen Sie den Bereich **Konfiguration** im Azure ATP-Portal, und wählen Sie **Sensoren** im Abschnitt **System** aus, um den Status der erkannten, überwachten und nicht überwachten Domänencontroller zu überprüfen.
   
     ![Überwachen des Status von Azure ATP-Sensoren](media/atp-sensors-status-monitoring.png)

2. Ihre derzeit überwachten und nicht überwachten Domänencontroller werden oben auf der Anzeige angezeigt. Klicken Sie auf **Details herunterladen**, um die Überwachungsstatusinformationen zu Ihren Domänencontrollern herunterzuladen. 

Die heruntergeladene Excel-Datei zur Abdeckung der Domänencontroller stellt folgende Informationen für alle ermittelten Domänencontroller in Ihrer Organisation bereit:

|Titel|Beschreibung|
|----|----|
|Hostname|Computername|
|Domänenname|Domänenname|
|Überwacht|Azure ATP-Überwachungsstatus|
|Sensortyp|Azure ATP-Sensor oder eigenständiger Azure ATP-Sensor|
|Organisationseinheit|Speicherort in Active Directory |
|Betriebssystemversion| Version des ermittelten Betriebssystems|
|IP-Adresse|Ermittelte IP-Adresse| 


> [!NOTE]
> Die Konfigurationsseiten des Azure ATP-Portals können nur von Azure ATP-Administratoren bearbeitet werden.


## <a name="see-also"></a>Weitere Informationen

- [Azure ATP-Architektur](atp-architecture.md)
- [Konfigurieren von Azure ATP-Sensoren](install-atp-step5.md)
- [Azure Advanced Threat Protection-Unterstützung für mehrere Gesamtstrukturen](atp-multi-forest.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)