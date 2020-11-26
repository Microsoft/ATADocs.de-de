---
title: Aktualisieren Ihrer Microsoft Defender for Identity-Sensoren
description: Hier wird beschrieben, wie Sie Updates für Sensoren in Microsoft Defender for Identity ausführen und verzögern.
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
ms.openlocfilehash: d65de1862d97a1d8dbb84fdc84252851fbe44d63
ms.sourcegitcommit: 07a855b87931875bdeca14b152b13a36db79bfa8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/26/2020
ms.locfileid: "94846781"
---
# <a name="update-product-long-sensors"></a>Aktualisieren von [!INCLUDE [Product long](includes/product-long.md)]-Sensoren

Stets aktuelle [!INCLUDE [Product long](includes/product-long.md)]-Sensoren bieten den bestmöglichen Schutz für Ihre Organisation.

Der [!INCLUDE [Product long](includes/product-long.md)]-Dienst wird in der Regel mehrmals pro Monat mit neuen Erkennungen, Features und Leistungsverbesserungen aktualisiert. In der Regel enthalten diese Updates auch ein entsprechendes Nebenversionsupdate für die Sensoren. [!INCLUDE [Product short](includes/product-short.md)]-Sensoren und die entsprechenden Updates haben niemals Schreibberechtigungen für Ihre Domänencontroller. Sensorupdatepakete steuern nur die [!INCLUDE [Product short](includes/product-short.md)]-Funktionen für Sensoren und die Sensorerkennung.

## <a name="product-short-sensor-update-types"></a>Updatetypen für [!INCLUDE [Product short](includes/product-short.md)]-Sensoren

[!INCLUDE [Product short](includes/product-short.md)]-Sensoren unterstützen zwei Arten von Updates:

- Updates von Nebenversionen:
  - Häufig
  - Keine Installation von MSI und keine Änderungen der Registrierung erforderlich
  - Neu gestartet: [!INCLUDE [Product short](includes/product-short.md)]-Sensordienste
  - Nicht neu gestartet: Domänencontroller-Dienste und Server-Betriebssystem

- Updates der Hauptversion:
  - Selten
  - Umfassen wichtige Änderungen
  - Neu gestartet: [!INCLUDE [Product short](includes/product-short.md)]-Sensordienste
  - Möglicherweise Neustart erforderlich: Domänencontroller-Dienste und Server-Betriebssystem

> [!NOTE]
>
> - Steuern den automatischen Neustart von Sensoren (bei Updates der **Hauptversion**) auf der Konfigurationsseite im [!INCLUDE [Product short](includes/product-short.md)]-Portal.
> - Ein [!INCLUDE [Product short](includes/product-short.md)]-Sensor reserviert auf dem Domänencontroller, auf dem er installiert ist, immer mindestens 15 % der verfügbaren Arbeitsspeicher- und CPU-Ressourcen. Wenn der [!INCLUDE [Product short](includes/product-short.md)]-Dienst zu viel Speicherplatz beansprucht, wird er automatisch angehalten und vom [!INCLUDE [Product short](includes/product-short.md)]-Sensorupdatedienst neu gestartet.

## <a name="delayed-sensor-update"></a>Verzögertes Sensorupdate

Angesichts der rasanten [!INCLUDE [Product short](includes/product-short.md)]-Entwicklung und der raschen Freigabe von Updates können Sie eine Untergruppe Ihrer Sensoren als verzögerten Updatering definieren und so einen graduellen Updateprozess für Ihre Sensoren ermöglichen. Mit [!INCLUDE [Product short](includes/product-short.md)] können Sie auswählen, wie Ihre Sensoren aktualisiert werden, und jeden Sensor als Kandidat für ein **verzögertes Update** festlegen.

Sensoren, die nicht für ein verzögertes Update ausgewählt wurden, werden bei jedem Update des [!INCLUDE [Product short](includes/product-short.md)]-Diensts automatisch aktualisiert. Sensoren, für die ein **verzögertes Update** festgelegt wurde, werden mit einer Verzögerung von 72 Stunden nach der offiziellen Freigabe der einzelnen Dienstupdates aktualisiert.

Mit der Option für ein **verzögertes Update** können Sie bestimmte Sensoren als automatischen Updatering auswählen, bei dem alle Updates automatisch erfolgen, und für den Rest der Sensoren ein verzögertes Update festlegen. Das gibt Ihnen Zeit, zuerst die erfolgreiche Ausführung der automatischen Aktualisierung Ihrer Sensoren zu bestätigen.

> [!NOTE]
> Wenn ein Fehler auftritt und ein Sensor nicht aktualisiert wird, erstellen Sie ein Supportticket. Informationen zur weiteren Stärkung Ihres Proxys, damit er nur mit Ihrer Instanz kommuniziert, finden Sie unter [Proxykonfiguration](configure-proxy.md).
Die Authentifizierung zwischen Ihren Sensoren und dem Azure-Clouddienst verwendet sichere, zertifikatbasierte gegenseitige Authentifizierung.

Jedes Update wird getestet und für alle unterstützten Betriebssysteme überprüft, damit Ihr Netzwerk und Ihre Vorgänge nur minimal beeinträchtigt werden.

Gehen Sie wie folgt vor, um einen Sensor für ein verzögertes Update auszuwählen:

1. Klicken Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal auf das Symbol „Einstellungen“ und dann auf **Konfiguration**.
1. Klicken Sie auf die Registerkarte **Updates**.
1. Legen Sie in der Tabellenzeile neben jedem Sensor, für den Sie das Update später ausführen möchten, den Schieberegler **Delayed update** (Verzögertes Update) auf **An** fest.
1. Klicken Sie auf **Speichern**.

## <a name="sensor-update-process"></a>Updateprozess für den Sensor

Die [!INCLUDE [Product short](includes/product-short.md)]-Sensoren prüfen im Abstand weniger Minuten, ob sie bereits auf die neuste Version aktualisiert worden sind. Wenn der [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst auf eine neuere Version aktualisiert wird, startet der [!INCLUDE [Product short](includes/product-short.md)]-Sensordienst den Updateprozess:

1. Der [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst wird auf die neueste Version aktualisiert.
1. Der [!INCLUDE [Product short](includes/product-short.md)]-Sensorupdatedienst stellt fest, dass eine aktualisierte Version verfügbar ist.
1. Bei den Sensoren, für die kein **verzögertes Update** festgelegt, beginnt der sensorweise Updateprozess:
    1. Der [!INCLUDE [Product short](includes/product-short.md)]-Sensorupdatedienst bezieht die aktualisierte Version (im CAB-Dateiformat) vom Clouddienst.
    1. Der [!INCLUDE [Product short](includes/product-short.md)]-Sensorupdatedienst überprüft die Dateisignatur.
    1. Der [!INCLUDE [Product short](includes/product-short.md)]-Sensorupdatedienst extrahiert die CAB-Datei in einen neuen Ordner im Installationsverzeichnis des Sensors. Standardmäßig wird sie in folgenden Ordner extrahiert: *C:\Programme\Azure Advanced Threat Protection Sensor\<version number>* .
    1. Der [!INCLUDE [Product short](includes/product-short.md)]-Sensordienst verweist auf die neuen Dateien, die aus der CAB-Datei extrahiert wurden.
    1. Der [!INCLUDE [Product short](includes/product-short.md)]-Sensorupdatedienst startet den [!INCLUDE [Product short](includes/product-short.md)]-Sensordienst neu.
        > [!NOTE]
        > Nebenversionupdates erfordern keine Installation von MSI und keine Änderungen an Registrierungswerten oder Systemdateien. Selbst ein anstehender Neustart wirkt sich nicht auf ein Sensorupdate aus.
    1. Die Sensoren werden auf Basis der neuen aktualisierten Version ausgeführt.
    1. Der Sensor erhält eine Freigabe vom Azure-Clouddienst. Den Sensorstatus können Sie auf der Seite **Updates** überprüfen.
    1. Der nächste Sensor startet den Aktualisierungsprozess.

1. 72 Stunden nach der Aktualisierung des [!INCLUDE [Product short](includes/product-short.md)]-Clouddiensts startet der Updateprozess für die Sensoren, für die ein **verzögertes Update** ausgewählt wurde. Bei diesem Prozess werden dieselben Schritte ausgeführt wie bei den automatisch aktualisierten Sensoren.

![Sensorupdate](media/sensor-update.png)

Für jeden Sensor, bei dem der Updateprozess nicht abgeschlossen werden kann, wird eine entsprechende Integritätswarnung ausgelöst und als Benachrichtigung gesendet.

![Fehler beim Sensorupdate](media/sensor-outdated.png)

## <a name="see-also"></a>Weitere Informationen

- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Voraussetzungen für [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
