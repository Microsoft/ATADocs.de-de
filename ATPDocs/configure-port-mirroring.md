---
title: Konfigurieren der Portspiegelung bei der Bereitstellung von Azure Advanced Threat Protection
description: Beschreibt Optionen für die Portspiegelung und deren Konfiguration für Azure ATP
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/19/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9ec7eb4c-3cad-4543-bbf0-b951d8fc8ffe
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 29269fd123a0644a39c9ff87372908302e0c55e6
ms.sourcegitcommit: 098a20abe62e153372da4c96db256bc63c113bd1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88808664"
---
# <a name="configure-port-mirroring"></a>Konfigurieren der Portspiegelung

Dieser Artikel ist für Sie nur interessant, wenn Sie eigenständige Azure ATP-Sensoren anstelle von Azure ATP-Sensoren bereitstellen.

> [!NOTE]
> Eigenständige Azure ATP-Server unterstützen nicht die Erstellung von Protokolleinträgen für Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die Daten für mehrere Erkennungen bereitstellen. Zur vollständigen Abdeckung Ihrer Umgebung empfiehlt es sich, den Azure ATP-Sensor bereitzustellen.

Als primäre Datenquelle verwendet Azure ATP eine ausführliche Paketüberprüfung (Deep Packet Inspection) des Netzwerkdatenverkehrs zu und von den Domänencontrollern. Damit Azure ATP den Netzwerkdatenverkehr sieht, muss entweder eine Portspiegelung eingerichtet oder ein Netzwerk-TAP verwendet werden.

Beim Konfigurieren der Portspiegelung ist für jeden überwachten Domänencontroller **Portspiegelung** als **Quelle** des Netzwerkdatenverkehrs auszuwählen. In der Regel müssen Sie mit dem Netzwerk- oder Virtualisierungsteam zusammenarbeiten, um die Portspiegelung zu konfigurieren.
Weitere Informationen finden Sie in der Dokumentation des jeweiligen Anbieters.

Die Domänencontroller und der eigenständige Azure ATP-Sensor können physisch oder virtuell vorhanden sein. Im Folgenden werden häufige Methoden für die Portspiegelung mit nützlichen Hinweisen aufgelistet. Weitere Informationen finden Sie in der Produktdokumentation Ihres Switchs oder Virtualisierungsservers. Der Hersteller Ihres Switches verwendet möglicherweise andere Bezeichnungen.

**Switched Port Analyzer (SPAN):** kopiert Netzwerkdatenverkehr von einem oder mehreren Switchports an einen anderen Port auf demselben Switch. Sowohl der eigenständige Azure ATP-Sensor als auch der Domänencontroller müssen mit demselben physischen Switch verbunden werden.

**Remote Switch Port Analyzer (RSPAN):** ermöglicht die Überwachung des Netzwerkdatenverkehrs aus Quellenports über mehrere physische Switches hinweg. RSPAN kopiert den Quellendatenverkehr in ein speziell für RSPAN konfiguriertes VLAN. Dieses VLAN muss mit den anderen beteiligten Switches einen Trunk bilden. RSPAN arbeitet in Schicht 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN):** eine proprietäre Cisco-Technologie für Schicht 3. ERSPAN ermöglicht das Überwachen von Datenverkehr über Switches hinweg, ohne Bedarf an VLAN-Trunks. ERSPAN verwendet für das Kopieren des überwachten Netzwerkverkehrs Generic Routing Encapsulation (GRE). Azure ATP kann derzeit ERSPAN-Datenverkehr nicht direkt empfangen. Damit Azure ATP mit ERSPAN-Datenverkehr arbeiten kann, muss ein Switch oder Router entsprechend als Ziel des ERSPAN-Datenverkehrs konfiguriert werden, um den Datenverkehr im Vorfeld aufzuschlüsseln. Konfigurieren Sie den Switch oder Router dann so, dass der entkapselte Datenverkehr mithilfe von SPAN oder RSPAN an den eigenständigen Azure ATP-Sensor weitergeleitet wird.

> [!NOTE]
> Wenn der Domänencontroller mit der Portspiegelung über eine WAN-Anbindung angeschlossen ist, muss darauf geachtet werden, dass die WAN-Anbindung die zusätzliche Last des ERSPAN-Datenverkehrs aufnehmen kann.
> Azure ATP unterstützt nur dann die Überwachung des Netzwerkdatenverkehrs, wenn der Datenverkehr die NIC und den Domänencontroller auf die gleiche Weise erreicht. Azure ATP unterstützt die Überwachung des Netzwerkdatenverkehrs nicht, wenn der Verkehr auf verschiedene Ports aufgeteilt ist.

## <a name="supported-port-mirroring-options"></a>Unterstützte Optionen für die Portspiegelung

|Eigenständiger Azure ATP-Sensor|Domänencontroller|Überlegungen|
|---------------|---------------------|------------------|
|Virtuell|Virtuell auf demselben Host|Der virtuelle Switch muss Portspiegelung unterstützen.<br /><br />Durch einzelnes Verschieben der virtuellen Computer auf einen anderen Host kann die Portspiegelung aufhören zu funktionieren.|
|Virtuell|Virtuell auf unterschiedlichen Hosts|Achten Sie darauf, dass der virtuelle Switch dieses Szenario unterstützt.|
|Virtuell|Physisch|Erfordert einen dedizierten Netzwerkadapter, da Azure ATP andernfalls den gesamten eingehenden und ausgehenden Datenverkehr des Hosts sieht, einschließlich des an den Azure ATP-Clouddienst weitergeleiteten Datenverkehrs.|
|Physisch|Virtuell|Achten Sie darauf, dass der virtuelle Switch dieses Szenario unterstützt. Ebenfalls erforderlich ist eine entsprechende Konfiguration für die Portspiegelung auf den physischen Switches für folgendes Szenario:<br /><br />Wenn sich der virtuelle Host auf demselben physischen Switch befindet, muss auf Switchebene ein SPAN konfiguriert werden.<br /><br />Wenn sich der virtuelle Host auf einem anderen Switch befindet, muss RSPAN oder ERSPAN&#42; konfiguriert werden.|
|Physisch|Physisch auf demselben Switch|Der physische Switch muss SPAN/Portspiegelung unterstützen.|
|Physisch|Physisch auf einem anderen Switch|Erfordert physische Switches mit Unterstützung für RSPAN oder ERSPAN&#42;.|

&#42;ERSPAN wird nur unterstützt, wenn der Datenverkehr vor der Analyse durch ATP aufgeschlüsselt wird.

> [!NOTE]
> Achten Sie darauf, dass die Zeitsynchronisierung des eigenständigen Azure ATP-Sensors und der Domänencontroller, mit denen sie verbunden sind, in einem Bereich von fünf Minuten zueinander liegt.

**Falls Sie mit Virtualisierungsclustern arbeiten:**

- Konfigurieren Sie für jeden Domänencontroller, der auf dem Virtualisierungscluster in einem virtuellen Computer mit dem eigenständigen Azure ATP ausgeführt wird, die Affinität zwischen dem Domänencontroller und dem eigenständigen Azure ATP-Sensor. Auf diese Weise folgt der eigenständige Azure ATP-Sensor dem Domänencontroller, wenn dieser auf einen anderen Host im Cluster verschoben wird. Dieser Ansatz funktioniert gut, solange nur wenige Domänencontroller vorhanden sind.

  > [!NOTE]
  > Wenn Ihre Umgebung V2V ((Virtual-to-Virtual) auf unterschiedlichen Hosts (RSPAN) unterstützt, müssen Sie sich zu Affinität keine Gedanken machen.

- Um zu gewährleisten, dass der eigenständige Azure ATP-Sensor ausreichende Kapazität für die Überwachung aller Domänencontroller aufweisen, eignet sich folgende Option: Installieren Sie auf jedem Virtualisierungshost einen virtuellen Computer, und installieren Sie auf jedem Host einen eigenständigen Azure ATP-Sensor. Konfigurieren Sie jeden eigenständigen Azure ATP-Sensor so, dass er alle Domänencontroller überwacht, die auf dem betreffenden Cluster ausgeführt werden. Auf diese Weise wird jeder Host überwacht, auf dem Domänencontroller ausgeführt werden.

Überprüfen Sie nach dem Konfigurieren der Portspiegelung deren ordnungsgemäße Funktion, bevor Sie den eigenständigen Azure ATP-Sensor installieren.

## <a name="see-also"></a>Weitere Informationen

- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
