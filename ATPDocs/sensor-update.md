---
title: Aktualisieren Ihrer Azure ATP-Sensoren | Microsoft-Dokumentation
description: Im Folgenden wird erläutert, wie Sie Azure ATP-Sensoren aktualisieren können.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 603d9e09-a07d-4357-862f-d5682c8bc3dd
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a24210415929b69152377d34aeec1bdc8906d08c
ms.sourcegitcommit: f4f2a1b2c674c4dba7a46ece0624f5ea10c4865e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/02/2018
ms.locfileid: "52744437"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="update-azure-atp-sensors"></a>Aktualisieren von Azure ATP-Sensoren
Azure Advanced Threat Protection muss aktuell sein, damit Ihre Organisation bestmöglich geschützt werden kann.

Der Azure ATP-Dienst wird mehrmals pro Monat mithilfe von Fehlerbehebungen, Leistungsverbesserungen und neuen Erkennungen aktualisiert. Gelegentlich erfordern diese Updates auch entsprechende Updates der Sensoren. 

Wenn Sie Ihre Sensoren nicht aktualisieren, können diese möglicherweise nicht mit dem Azure ATP-Clouddienst kommunizieren, wodurch der Dienst beeinträchtigt wird. 

Die Authentifizierung zwischen Ihren Sensoren und dem Azure-Clouddienst verwendet sichere, zertifikatbasierte gegenseitige Authentifizierung. 

Jedes Update wird getestet und für alle unterstützten Betriebssysteme überprüft, damit Ihr Netzwerk und Ihre Vorgänge nur minimal beeinträchtigt werden.

### <a name="azure-atp-sensor-update-types"></a>Updatetypen für den Azure ATP-Sensor   

Azure ATP-Sensoren unterstützen zwei verschiedene Arten von Updates:
- Updates von Nebenversionen: 
  - Häufig 
  - Erfordern keine Installation von MSI und keine Änderungen der Registrierung
  - Der Azure ATP-Sensordienst startet neu
  - Domänencontroller und Server müssen nicht neu gestartet werden

- Updates der Hauptversion:
 - Selten
 - Erfordern möglicherweise einen Neustart der Domänencontroller und Server
 - Umfassen wichtige Änderungen 

> [!NOTE]
>- Sie können automatische Neustarts der Sensoren (bei Updates der Hauptversion) über die Konfigurationsseite steuern. 
> - Der Azure ATP-Sensor bewahrt immer mindestens 15% des Speichers und der verfügbaren CPU. Wenn der Dienst zu viel Speicherplatz beansprucht, wird er automatisch vom Aktualisierungsdienst für den Azure ATP-Sensor neu gestartet.

## <a name="delayed-sensor-update"></a>Verzögertes Sensorupdate
Damit der Updateprozess schrittweise durchgeführt werden kann, können Sie mithilfe von Azure ATP einen Sensor als Kandidaten für ein **verzögertes Update** festlegen. 

In der Regel werden Sensoren automatisch aktualisiert, wenn der Azure ATP-Clouddienst aktualisiert wird. Sensoren, für die die Option **Delayed update** (Verzögertes Update) festgelegt sind, werden 24 Stunden nach dem ersten Update des Clouddiensts aktualisiert.

Dadurch können Sie bestimmte Sensoren auswählen, für die das Update automatisch erfolgt, und die restlichen Sensoren später aktualisieren, wenn das erste Update erfolgreich ausgeführt werden konnte.

> [!NOTE]
> Wenn ein Fehler auftritt und ein Sensor nicht aktualisiert wird, erstellen Sie ein Supportticket. Informationen zur weiteren Stärkung Ihres Proxys, damit er nur mit Ihrer Instanz kommuniziert, finden Sie unter [Proxykonfiguration](configure-proxy.md)

Gehen Sie wie folgt vor, um einen Sensor für ein verzögertes Update auszuwählen:

1. Klicken Sie im Azure ATP-Portal zuerst auf das Symbol „Einstellungen“ und dann auf **Konfiguration**.
2. Klicken Sie auf die Registerkarte **Updates**.
3. Legen Sie in der Tabellenzeile neben jedem Sensor, für den Sie das Update später ausführen möchten, den Schieberegler **Delayed update** (Verzögertes Update) auf **An** fest.
4. Klicken Sie auf **Speichern**.
 
## <a name="sensor-update-process"></a>Updateprozess für den Sensor

Die Azure ATP-Sensoren prüfen im Abstand weniger Minuten, ob sie bereits auf die neuste Version aktualisiert worden sind. Wenn der Azure ATP-Clouddienst auf eine neuere Version aktualisiert wird, startet der Azure ATP-Sensordienst den Aktualisierungsprozess:

1. Der Azure ATP-Clouddienst führt ein Update auf die neuste Version durch.
2. Der Aktualisierungsdienst für den Azure ATP-Sensor stellt fest, dass eine aktualisierte Version verfügbar ist.
3. Die Sensoren, für die nicht die Option **Verzögertes Update** ausgewählt ist, werden aktualisiert:
  1. Der Aktualisierungsdienst für den Azure ATP-Sensor entnimmt dem Clouddienst die aktualisierte Version (im CAB-Format).
  2. Der Aktualisierungsdienst für den Azure ATP-Sensor überprüft die Dateisignatur.
  3. Der Aktualisierungsdienst für den Azure ATP-Sensor extrahiert die CAB-Datei in einem neuen Unterordner im Installationsorder des Sensors. Standardmäßig wird sie unter folgendem Pfad extrahiert: *C:\Program Files\Azure Advanced Threat Protection Sensor\<Versionsnummer>*
  4. Der Aktualisierungsdienst für den Azure ATP-Sensor startet den Azure ATP-Sensordienst neu.
  5. Der Azure ATP-Sensordienst zeigt auf die neuen Dateien, die aus der CAB-Datei extrahiert werden.
  > [!NOTE]
  >Bei einem Update der Nebenversion des Sensors wird weder eine MSI installiert noch werden Änderungen an den Registrierungswerten oder den Systemdateien vorgenommen. Auch wenn ein Neustart aussteht, wird das Update der Sensoren nicht beeinträchtigt. 
  6. Die Sensoren werden basierend auf der vor kurzem aktualisierten Version ausgeführt.
  7. Sensoren erhalten eine Freigabe vom Azure-Clouddienst. Sie können dies über die Seite **Updates** prüfen.
  8. Der nächste Sensor startet den Aktualisierungsprozess. 

4. 24 Stunden nach der Aktualisierung des Azure ATP-Clouddiensts wird auch für die Sensoren, für die die Option **Delayed update** (Verzögertes Update) ausgewählt ist, der Updateprozess gestartet.

![Sensorupdate](./media/sensor-update.png)


Falls ein Fehler auftritt und der Sensor den Updateprozess nicht abschließen kann, wird eine betreffende Überwachungswarnung ausgelöst und als Benachrichtigung gesendet.

![Sensor veraltet](./media/sensor-outdated.png)


## <a name="see-also"></a>Weitere Informationen

- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)