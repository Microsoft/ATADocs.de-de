---
title: Konfigurieren der Portspiegelung in Advanced Threat Analytics | Microsoft-Dokumentation
description: "Beschreibt Optionen für die Portspiegelung und deren Konfiguration für ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: fb9c6aa3962f7fc121f3737a32c9a5cfb2fcfb8e
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# <a name="configure-port-mirroring"></a>Konfigurieren der Portspiegelung
> [!NOTE] 
> Dieser Artikel ist für Sie nur interessant, wenn Sie ATA-Gateways anstelle von ATA-Lightweight-Gateways bereitstellen. Lesen Sie [Auswählen des richtigen Gatewaytyps für die Bereitstellung](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment), um zu ermitteln, ob Sie ATA-Gateways verwenden müssen.
 
Als primäre Datenquelle verwendet ATA eine ausführliche Paketüberprüfung (Deep Packet Inspection) des Netzwerkdatenverkehrs zu und von den Domänencontrollern. Damit ATA den Netzwerkdatenverkehr sieht, muss entweder eine Portspiegelung eingerichtet oder ein Netzwerk-TAP verwendet werden.

Beim Konfigurieren der Portspiegelung ist für jeden überwachten Domänencontroller **Portspiegelung** als **Quelle** des Netzwerkdatenverkehrs auszuwählen. In der Regel müssen Sie mit dem Netzwerk- oder Virtualisierungsteam zusammenarbeiten, um die Portspiegelung zu konfigurieren.
Weitere Informationen finden Sie in der Dokumentation des jeweiligen Anbieters.

Die Domänencontroller und ATA-Gateways können physisch oder virtuell vorhanden sein. Im Folgenden werden häufige Methoden für die Portspiegelung mit nützlichen Hinweisen aufgelistet. Weitere Informationen finden Sie in der Produktdokumentation Ihres Switchs oder Virtualisierungsservers. Der Hersteller Ihres Switches verwendet möglicherweise andere Bezeichnungen.

**Switched Port Analyzer (SPAN):** kopiert Netzwerkdatenverkehr von einem oder mehreren Switchports an einen anderen Port auf demselben Switch. Das ATA-Gateway und der Domänencontroller müssen mit demselben physischen Switch verbunden werden.

**Remote Switch Port Analyzer (RSPAN):** ermöglicht die Überwachung des Netzwerkdatenverkehrs aus Quellenports über mehrere physische Switches hinweg. RSPAN kopiert den Quellendatenverkehr in ein speziell für RSPAN konfiguriertes VLAN. Dieses VLAN muss mit den anderen beteiligten Switches einen Trunk bilden. RSPAN arbeitet in Schicht 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN):** eine proprietäre Cisco-Technologie für Schicht 3. ERSPAN ermöglicht das Überwachen von Datenverkehr über Switches hinweg, ohne Bedarf an VLAN-Trunks. ERSPAN verwendet für das Kopieren des überwachten Netzwerkverkehrs Generic Routing Encapsulation (GRE). ATA kann derzeit ERSPAN-Datenverkehr nicht direkt empfangen. Damit ATA mit ERSPAN-Datenverkehr arbeiten kann, muss ein Switch oder Router entsprechend als Ziel des ERSPAN-Datenverkehrs konfiguriert werden, um den Datenverkehr im Vorfeld aufzuschlüsseln. Konfigurieren Sie den Switch oder Router dann so, dass der entkapselte Datenverkehr mithilfe von SPAN oder RSPAN an das ATA-Gateway weitergeleitet wird.

> [!NOTE]
> Wenn der Domänencontroller mit der Portspiegelung über eine WAN-Anbindung angeschlossen ist, muss darauf geachtet werden, dass die WAN-Anbindung die zusätzliche Last des ERSPAN-Datenverkehrs aufnehmen kann.
> ATA unterstützt nur dann die Überwachung des Netzwerkdatenverkehrs, wenn der Datenverkehr die NIC und den Domänencontroller auf die gleiche Weise erreicht. ATA unterstützt die Überwachung des Netzwerkdatenverkehrs nicht, wenn der Verkehr auf verschiedene Ports aufgeteilt ist.

## <a name="supported-port-mirroring-options"></a>Unterstützte Optionen für die Portspiegelung

|ATA-Gateway|Domänencontroller|Überlegungen|
|---------------|---------------------|------------------|
|Virtuell|Virtuell auf demselben Host|Der virtuelle Switch muss Portspiegelung unterstützen.<br /><br />Durch einzelnes Verschieben der virtuellen Computer auf einen anderen Host kann die Portspiegelung aufhören zu funktionieren.|
|Virtuell|Virtuell auf unterschiedlichen Hosts|Achten Sie darauf, dass der virtuelle Switch dieses Szenario unterstützt.|
|Virtuell|Physisch|Erfordert einen dedizierten Netzwerkadapter, da ATA andernfalls den gesamten eingehenden und ausgehenden Datenverkehr des Hosts sieht, einschließlich des an ATA Center weitergeleiteten Datenverkehrs.|
|Physisch|Virtuell|Achten Sie darauf, dass der virtuelle Switch dieses Szenario unterstützt. Ebenfalls erforderlich ist eine entsprechende Konfiguration für die Portspiegelung auf den physischen Switches für folgendes Szenario:<br /><br />Wenn sich der virtuelle Host auf demselben physischen Switch befindet, muss auf Switchebene ein SPAN konfiguriert werden.<br /><br />Wenn sich der virtuelle Host auf einem anderen Switch befindet, muss RSPAN oder ERSPAN&#42; konfiguriert werden.|
|Physisch|Physisch auf demselben Switch|Der physische Switch muss SPAN/Portspiegelung unterstützen.|
|Physisch|Physisch auf einem anderen Switch|Erfordert physische Switches mit Unterstützung für RSPAN oder ERSPAN&#42;.|
&#42;ERSPAN wird nur unterstützt, wenn der Datenverkehr vor der Analyse durch ATA aufgeschlüsselt wird.

> [!NOTE]
> Achten Sie darauf, dass die Zeitsynchronisierung der ATA-Gateways und der Domänencontroller, mit denen sie verbunden sind, in einem Bereich von fünf Minuten zueinander liegt.

**Falls Sie mit Virtualisierungsclustern arbeiten:**

-   Konfigurieren Sie für jeden Domänencontroller, der auf dem Virtualisierungscluster in einem virtuellen Computer mit dem ATA-Gateway ausgeführt wird, die Affinität zwischen dem Domänencontroller und dem ATA-Gateway. Auf diese Weise folgt das ATA-Gateway dem Domänencontroller, wenn dieser auf einen anderen Host verschoben wird. Dieser Ansatz funktioniert gut, solange nur wenige Domänencontroller vorhanden sind.
> [!NOTE]
> Wenn Ihre Umgebung V2V ((Virtual-to-Virtual) auf unterschiedlichen Hosts (RSPAN) unterstützt, müssen Sie sich zu Affinität keine Gedanken machen.
> 
-   Um zu gewährleisten, dass die ATA-Gateways ausreichende Kapazität für die eigenständige Überwachung aller Domänencontroller aufweisen, eignet sich folgende Option: Installieren Sie auf jedem Virtualisierungshost einen virtuellen Computer, und installieren Sie auf jeden Host ein ATA-Gateway. Konfigurieren Sie jedes ATA-Gateway so, dass es alle Domänencontroller überwacht, die auf dem betreffenden Cluster ausgeführt werden. Auf diese Weise wird jeder Host überwacht, auf dem Domänencontroller ausgeführt werden.

Überprüfen Sie nach dem Konfigurieren der Portspiegelung deren ordnungsgemäße Funktion, bevor Sie die ATA-Gateways installieren.

## <a name="see-also"></a>Weitere Informationen
- [Überprüfen der Portspiegelung](validate-port-mirroring.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
