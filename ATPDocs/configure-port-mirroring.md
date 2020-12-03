---
title: Konfigurieren der Portspiegelung beim Bereitstellen von Microsoft Defender for Identity
description: Hier werden Optionen für die Portspiegelung und deren Konfiguration für Microsoft Defender for Identity beschrieben.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 72b453c5e90b46f432bd7eb89572e519d50d9e4a
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544044"
---
# <a name="configure-port-mirroring"></a>Konfigurieren der Portspiegelung

Dieser Artikel ist nur interessant, wenn Sie eigenständige [!INCLUDE [Product long](includes/product-long.md)]-Sensoren anstelle von [!INCLUDE [Product short](includes/product-short.md)]-Sensoren bereitstellen.

> [!NOTE]
> Eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensoren unterstützen keine Erfassung von Protokolleinträgen für die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die Daten für mehrere Erkennungen bereitstellen. Zur vollständigen Erfassung Ihrer Umgebung empfiehlt sich die Bereitstellung des [!INCLUDE [Product short](includes/product-short.md)]-Sensors.

Die Hauptdatenquelle von [!INCLUDE [Product short](includes/product-short.md)] ist die ausführliche Paketüberprüfung (Deep Packet Inspection) des Netzwerkdatenverkehrs zu und von den Domänencontrollern. Damit [!INCLUDE [Product short](includes/product-short.md)] Netzwerkdatenverkehr erkennt, müssen Sie die Portspiegelung einrichten oder einen Netzwerk-TAP verwenden.

Beim Konfigurieren der Portspiegelung ist für jeden überwachten Domänencontroller **Portspiegelung** als **Quelle** des Netzwerkdatenverkehrs auszuwählen. In der Regel müssen Sie mit dem Netzwerk- oder Virtualisierungsteam zusammenarbeiten, um die Portspiegelung zu konfigurieren.
Weitere Informationen finden Sie in der Dokumentation des jeweiligen Anbieters.

Die Domänencontroller und der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor können physisch oder virtuell vorhanden sein. Im Folgenden werden häufige Methoden für die Portspiegelung mit nützlichen Hinweisen aufgelistet. Weitere Informationen finden Sie in der Produktdokumentation Ihres Switchs oder Virtualisierungsservers. Der Hersteller Ihres Switches verwendet möglicherweise andere Bezeichnungen.

**Switched Port Analyzer (SPAN):** kopiert Netzwerkdatenverkehr von einem oder mehreren Switchports an einen anderen Port auf demselben Switch. Sowohl der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor als auch die Domänencontroller müssen mit demselben physischen Switch verbunden sein.

**Remote Switch Port Analyzer (RSPAN):** ermöglicht die Überwachung des Netzwerkdatenverkehrs aus Quellenports über mehrere physische Switches hinweg. RSPAN kopiert den Quellendatenverkehr in ein speziell für RSPAN konfiguriertes VLAN. Dieses VLAN muss mit den anderen beteiligten Switches einen Trunk bilden. RSPAN arbeitet in Schicht 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN):** eine proprietäre Cisco-Technologie für Schicht 3. ERSPAN ermöglicht das Überwachen von Datenverkehr über Switches hinweg, ohne Bedarf an VLAN-Trunks. ERSPAN verwendet für das Kopieren des überwachten Netzwerkverkehrs Generic Routing Encapsulation (GRE). [!INCLUDE [Product short](includes/product-short.md)] kann ERSPAN-Datenverkehr derzeit nicht direkt empfangen. Damit [!INCLUDE [Product short](includes/product-short.md)] mit ERSPAN-Datenverkehr arbeiten kann, muss ein Switch oder Router als ERSPAN-Ziel konfiguriert werden, um den Datenverkehr zu entkapseln. Konfigurieren Sie den Switch oder Router so, dass der entkapselte Datenverkehr über SPAN oder RSPAN an den eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor weitergeleitet wird.

> [!NOTE]
> Wenn der Domänencontroller mit der Portspiegelung über eine WAN-Anbindung angeschlossen ist, muss darauf geachtet werden, dass die WAN-Anbindung die zusätzliche Last des ERSPAN-Datenverkehrs aufnehmen kann.
> [!INCLUDE [Product short](includes/product-short.md)] unterstützt die Überwachung des Netzwerkdatenverkehrs nur, wenn der Datenverkehr die Netzwerkkarte und den Domänencontroller auf die gleiche Weise erreicht. [!INCLUDE [Product short](includes/product-short.md)] unterstützt die Datenverkehrsüberwachung nicht, wenn der Verkehr auf verschiedene Ports aufgeteilt ist.

## <a name="supported-port-mirroring-options"></a>Unterstützte Optionen für die Portspiegelung

|Eigenständiger [!INCLUDE [Product short](includes/product-short.md)]-Sensor|Domänencontroller|Überlegungen|
|---------------|---------------------|------------------|
|Virtuell|Virtuell auf demselben Host|Der virtuelle Switch muss Portspiegelung unterstützen.<br /><br />Durch einzelnes Verschieben der virtuellen Computer auf einen anderen Host kann die Portspiegelung aufhören zu funktionieren.|
|Virtuell|Virtuell auf unterschiedlichen Hosts|Achten Sie darauf, dass der virtuelle Switch dieses Szenario unterstützt.|
|Virtuell|Physisch|Erfordert einen dedizierten Netzwerkadapter, da [!INCLUDE [Product short](includes/product-short.md)] andernfalls den gesamten eingehenden und ausgehenden Datenverkehr des Hosts sieht, einschließlich des an den [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst gesendeten Datenverkehrs.|
|Physisch|Virtuell|Achten Sie darauf, dass der virtuelle Switch dieses Szenario unterstützt. Ebenfalls erforderlich ist eine entsprechende Konfiguration für die Portspiegelung auf den physischen Switches für folgendes Szenario:<br /><br />Wenn sich der virtuelle Host auf demselben physischen Switch befindet, muss auf Switchebene ein SPAN konfiguriert werden.<br /><br />Wenn sich der virtuelle Host auf einem anderen Switch befindet, muss RSPAN oder ERSPAN&#42; konfiguriert werden.|
|Physisch|Physisch auf demselben Switch|Der physische Switch muss SPAN/Portspiegelung unterstützen.|
|Physisch|Physisch auf einem anderen Switch|Erfordert physische Switches mit Unterstützung für RSPAN oder ERSPAN&#42;.|

&#42;ERSPAN wird nur unterstützt, wenn die Entkapselung vor der Analyse des Datenverkehrs durch [!INCLUDE [Product short](includes/product-short.md)] erfolgt.

> [!NOTE]
> Achten Sie darauf, dass die Zeitsynchronisierung des eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensors und der Domänencontroller, mit denen er verbunden ist, innerhalb von fünf Minuten liegt.

**Falls Sie mit Virtualisierungsclustern arbeiten:**

- Konfigurieren Sie für jeden Domänencontroller, der im Virtualisierungscluster auf einem virtuellen Computer mit dem eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor ausgeführt wird, die Affinität zwischen dem Domänencontroller und dem eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor. Auf diese Weise folgt der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor dem Domänencontroller, wenn dieser auf einen anderen Host im Cluster verschoben wird. Dieser Ansatz funktioniert gut, solange nur wenige Domänencontroller vorhanden sind.

  > [!NOTE]
  > Wenn Ihre Umgebung V2V ((Virtual-to-Virtual) auf unterschiedlichen Hosts (RSPAN) unterstützt, müssen Sie sich zu Affinität keine Gedanken machen.

- Um zu gewährleisten, dass der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor ausreichende Kapazität für die Überwachung aller Domänencontroller aufweist, eignet sich folgende Option: Installieren Sie auf jedem Virtualisierungshost einen virtuellen Computer und einen eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor. Konfigurieren Sie jeden eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor so, dass er alle Domänencontroller überwacht, die im betreffenden Cluster ausgeführt werden. Auf diese Weise wird jeder Host überwacht, auf dem Domänencontroller ausgeführt werden.

Überprüfen Sie nach dem Konfigurieren der Portspiegelung deren ordnungsgemäße Funktion, bevor Sie den eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor installieren.

## <a name="see-also"></a>Weitere Informationen

- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
