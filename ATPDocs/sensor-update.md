---
title: Aktualisieren von Azure ATP-Sensoren
description: Im Folgenden wird erläutert, wie Sie Azure ATP-Sensoren aktualisieren oder verzögert aktualisieren können.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/24/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 603d9e09-a07d-4357-862f-d5682c8bc3dd
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 860f856acd1a34e52032217b137b6350a0988365
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956583"
---
# <a name="update-azure-atp-sensors"></a>Aktualisieren von Azure ATP-Sensoren

Stets aktuelle Azure Advanced Threat Protection-Sensoren bieten den bestmöglichen Schutz für Ihr Unternehmen.

Der Azure ATP-Dienst wird in der Regel mehrmals pro Monat mit neuen Erkennungen, Features und Leistungsverbesserungen aktualisiert. In der Regel enthalten diese Updates auch ein entsprechendes Nebenversionsupdate für die Sensoren. Azure ATP-Sensoren und die entsprechenden Updates haben niemals Schreibberechtigungen für Ihre Domänencontroller. Sensorupdatepakete steuern nur die Azure ATP-Sensoren und die Erkennungsfunktionen der Sensoren. 

### <a name="azure-atp-sensor-update-types"></a>Updatetypen für den Azure ATP-Sensor    

Azure ATP-Sensoren unterstützen zwei verschiedene Arten von Updates:
- Updates von Nebenversionen: 
    - Häufig 
    - Keine Installation von MSI und keine Änderungen der Registrierung erforderlich
    - Neu gestartet: Azure ATP-Sensordienste 
    - Nicht neu gestartet: Domänencontroller-Dienste und Server-Betriebssystem

- Updates der Hauptversion:
    - Selten
    - Umfassen wichtige Änderungen 
    - Neu gestartet: Azure ATP-Sensordienste
    - Möglicherweise Neustart erforderlich: Domänencontroller-Dienste und Server-Betriebssystem

> [!NOTE]
>- Steuern den automatischen Neustart der Sensoren (bei Updates der **Hauptversion**) auf der Konfigurationsseite im Azure ATP-Portal. 
> - Ein Azure ATP-Sensor reserviert auf dem Domänencontroller, auf dem er installiert ist, immer mindestens 15 % des verfügbaren Arbeitsspeichers und der CPU-Ressourcen. Wenn der Azure ATP-Dienst zu viel Speicherplatz beansprucht, wird er automatisch angehalten und vom Azure ATP-Sensor-Aktualisierungsdienst neu gestartet.

## <a name="delayed-sensor-update"></a>Verzögertes Sensorupdate

Angesichts der rasanten Azure ATP-Entwicklung und der raschen Freigabe von Updates können Sie eine Untergruppe Ihrer Sensoren als verzögerten Updatering definieren, was einen graduellen Updateprozess für Ihre Sensoren ermöglicht. Mit Azure ATP können Sie auswählen, wie Ihre Sensoren aktualisiert werden, und jeden Sensor als Kandidat für ein **verzögertes Update** festlegen.  

Sensoren, die nicht für ein verzögertes Update ausgewählt wurden, werden bei jedem Update des Azure ATP-Diensts automatisch aktualisiert. Sensoren, für die ein **verzögertes Update** festgelegt wurde, werden mit einer Verzögerung von 72 Stunden nach der offiziellen Freigabe der einzelnen Dienstupdates aktualisiert. 

Mit der Option für ein **verzögertes Update** können Sie bestimmte Sensoren als automatischen Updatering auswählen, bei dem alle Updates automatisch erfolgen, und für den Rest der Sensoren ein verzögertes Update festlegen. Das gibt Ihnen Zeit, zuerst die erfolgreiche Ausführung der automatischen Aktualisierung Ihrer Sensoren zu bestätigen.

> [!NOTE]
> Wenn ein Fehler auftritt und ein Sensor nicht aktualisiert wird, erstellen Sie ein Supportticket. Informationen zur weiteren Stärkung Ihres Proxys, damit er nur mit Ihrer Instanz kommuniziert, finden Sie unter [Proxykonfiguration](configure-proxy.md).
Die Authentifizierung zwischen Ihren Sensoren und dem Azure-Clouddienst verwendet sichere, zertifikatbasierte gegenseitige Authentifizierung. 

Jedes Update wird getestet und für alle unterstützten Betriebssysteme überprüft, damit Ihr Netzwerk und Ihre Vorgänge nur minimal beeinträchtigt werden.


Gehen Sie wie folgt vor, um einen Sensor für ein verzögertes Update auszuwählen:

1. Klicken Sie im Azure ATP-Portal zuerst auf das Symbol „Einstellungen“ und dann auf **Konfiguration**.
1. Klicken Sie auf die Registerkarte **Updates**.
1. Legen Sie in der Tabellenzeile neben jedem Sensor, für den Sie das Update später ausführen möchten, den Schieberegler **Delayed update** (Verzögertes Update) auf **An** fest.
1. Klicken Sie auf **Speichern**.
 
## <a name="sensor-update-process"></a>Updateprozess für den Sensor

Die Azure ATP-Sensoren prüfen im Abstand weniger Minuten, ob sie bereits auf die neuste Version aktualisiert worden sind. Wenn der Azure ATP-Clouddienst auf eine neuere Version aktualisiert wird, startet der Azure ATP-Sensordienst den Aktualisierungsprozess:

1. Der Azure ATP-Clouddienst führt ein Update auf die neueste Version durch.
1. Der Azure ATP-Sensor-Aktualisierungsdienst stellt fest, dass eine aktualisierte Version verfügbar ist.
1. Bei den Sensoren, für die kein **verzögertes Update** festgelegt, beginnt der sensorweise Updateprozess:
   1. Der Azure ATP-Sensor-Aktualisierungsdienst bezieht vom Clouddienst die aktualisierte Version (im CAB-Dateiformat).
   2. Der Azure ATP-Sensor-Aktualisierungsdienst überprüft die Dateisignatur.
   3. Der Azure ATP-Sensor-Aktualisierungsdienst extrahiert die CAB-Datei in einen neuen Unterordner im Installationsverzeichnis des Sensors. Standardmäßig wird sie in folgenden Ordner extrahiert: *C:\Programme\Azure Advanced Threat Protection Sensor\<version number>* .
   4. Der Azure ATP-Sensordienst verweist auf die neuen Dateien, die aus der CAB-Datei extrahiert wurden.    
   5. Der Azure ATP-Sensor-Aktualisierungsdienst startet den Azure ATP-Sensordienst neu.
       > [!NOTE]
      >Nebenversionupdates erfordern keine Installation von MSI und keine Änderungen an Registrierungswerten oder Systemdateien. Selbst ein anstehender Neustart wirkt sich nicht auf ein Sensorupdate aus. 
   6. Die Sensoren werden auf Basis der neuen aktualisierten Version ausgeführt.
   7. Der Sensor erhält eine Freigabe vom Azure-Clouddienst. Den Sensorstatus können Sie auf der Seite **Updates** überprüfen.
   8. Der nächste Sensor startet den Aktualisierungsprozess. 

1. 72 Stunden nach der Aktualisierung des Azure ATP-Clouddiensts startet der Updateprozess für die Sensoren, für die ein **verzögertes Update** ausgewählt wurde. Dieser Updateprozess entspricht dabei dem Vorgang für automatisch aktualisierte Sensoren.

![Sensorupdate](media/sensor-update.png)


Für jeden Sensor, bei dem der Updateprozess nicht abgeschlossen werden kann, wird eine entsprechende Integritätswarnung ausgelöst und als Benachrichtigung gesendet.

![Fehler beim Sensorupdate](media/sensor-outdated.png)


## <a name="see-also"></a>Weitere Informationen

- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
