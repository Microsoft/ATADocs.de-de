---
title: Konfigurieren der Portspiegelung | Microsoft ATA
description: "Beschreibt Optionen für die Portspiegelung und deren Konfiguration für ATA"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 18b6ceb2c2d3eacb51cc150d5c7faaac5791a3d0


---

# Konfigurieren der Portspiegelung
> [!NOTE] 
> Dieser Artikel ist für Sie nur interessant, wenn Sie ATA-Gateways anstelle von ATA-Lightweight-Gateways bereitstellen. Um festzustellen, ob Sie ATA-Gateways verwenden müssen, lesen Sie [Auswählen des richtigen Gateways für Ihre Bereitstellung](/advanced-threat-analytics/plan-design/ata-capacity-planning#choosing-the-right-gateway-type-for-your-deployment).
 
Als primäre Datenquelle verwendet ATA eine ausführliche Paketüberprüfung (Deep Packet Inspection) des Netzwerkdatenverkehrs zu und von den Domänencontrollern. Damit ATA den Netzwerkdatenverkehr sieht, muss entweder eine Portspiegelung eingerichtet oder ein Netzwerk-TAP verwendet werden.

Beim Konfigurieren der Portspiegelung ist für jeden überwachten Domänencontroller **Portspiegelung** als **Quelle** des Netzwerkdatenverkehrs auszuwählen. In der Regel müssen Sie mit dem Netzwerk- oder Virtualisierungsteam zusammenarbeiten, um die Portspiegelung zu konfigurieren.
Weitere Informationen finden Sie in der Dokumentation des jeweiligen Anbieters.

Die Domänencontroller und ATA-Gateways können physisch oder virtuell vorhanden sein. Im Folgenden werden häufige Methoden für die Portspiegelung mit nützlichen Hinweisen aufgelistet. Weitere Informationen finden Sie in der Produktdokumentation Ihres Switches oder Virtualisierungsservers. Der Hersteller Ihres Switches verwendet möglicherweise andere Bezeichnungen.

**Switched Port Analyzer (SPAN):** kopiert Netzwerkdatenverkehr von einem oder mehreren Switchports an einen anderen Port auf demselben Switch. Das ATA-Gateway und der Domänencontroller müssen mit demselben physischen Switch verbunden werden.

**Remote Switch Port Analyzer (RSPAN):** ermöglicht die Überwachung des Netzwerkdatenverkehrs aus Quellenports über mehrere physische Switches hinweg. RSPAN kopiert den Quellendatenverkehr in ein speziell für RSPAN konfiguriertes VLAN. Dieses VLAN muss mit den anderen beteiligten Switches einen Trunk bilden. RSPAN arbeitet in Schicht 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN):** eine proprietäre Cisco-Technologie für Schicht 3. ERSPAN ermöglicht das Überwachen von Datenverkehr über Switches hinweg, ohne Bedarf an VLAN-Trunks. ERSPAN verwendet für das Kopieren des überwachten Netzwerkverkehrs Generic Routing Encapsulation (GRE). ATA kann derzeit ERSPAN-Datenverkehr nicht direkt empfangen. Damit ATA mit ERSPAN-Datenverkehr arbeiten kann, muss ein Switch oder Router entsprechend als Ziel des ERSPAN-Datenverkehrs konfiguriert werden, um den Datenverkehr im Vorfeld aufzuschlüsseln. Der Switch oder Router muss dann so konfiguriert werden, dass der Datenverkehr mithilfe von SPAN oder RSPAN an das ATA-Gateway weitergeleitet wird.

> [!NOTE]
> Wenn der Domänencontroller mit der Portspiegelung über eine WAN-Anbindung angeschlossen ist, muss darauf geachtet werden, dass die WAN-Anbindung die zusätzliche Last des ERSPAN-Datenverkehrs aufnehmen kann.

## Unterstützte Optionen für die Portspiegelung

|ATA-Gateway|Domänencontroller|Überlegungen|
|---------------|---------------------|------------------|
|Virtuell|Virtuell auf demselben Host|Der virtuelle Switch muss Portspiegelung unterstützen.<br /><br />Durch einzelnes Verschieben der virtuellen Computer auf einen anderen Host kann die Portspiegelung aufhören zu funktionieren.|
|Virtuell|Virtuell auf unterschiedlichen Hosts|Achten Sie darauf, dass der virtuelle Switch dieses Szenario unterstützt.|
|Virtuell|Physisch|Erfordert einen dedizierten Netzwerkadapter, da ATA andernfalls den gesamten eingehenden und ausgehenden Datenverkehr des Hosts sieht, einschließlich des an ATA Center weitergeleiteten Datenverkehrs.|
|Physisch|Virtuell|Achten Sie darauf, dass der virtuelle Switch dieses Szenario unterstützt. Ebenfalls erforderlich ist eine entsprechende Konfiguration für die Portspiegelung auf den physischen Switches für folgendes Szenario:<br /><br />Wenn sich der virtuelle Host auf demselben physischen Switch befindet, muss auf Switchebene ein SPAN konfiguriert sein.<br /><br />Wenn sich der virtuelle Host auf einem anderen Switch befindet, muss RSPAN oder ERSPAN&#42; konfiguriert werden.|
|Physisch|Physisch auf demselben Switch|Der physische Switch muss SPAN/Portspiegelung unterstützen.|
|Physisch|Physisch auf einem anderen Switch|Erfordert physische Switches mit Unterstützung für RSPAN oder ERSPAN&#42;.|
&#42;ERSPAN wird nur unterstützt, wenn der Datenverkehr vor der Analyse durch ATA aufgeschlüsselt wird.

> [!NOTE]
> Achten Sie darauf, dass die Zeitsynchronisierung der ATA-Gateways und der Domänencontroller, mit denen sie verbunden sind, in einem Bereich von 5 Minuten zueinander liegt.

**Falls Sie mit Virtualisierungsclustern arbeiten:**

-   Konfigurieren Sie für jeden Domänencontroller, der auf dem Virtualisierungscluster in einem virtuellen Computer mit dem ATA-Gateway ausgeführt wird, die Affinität zwischen dem Domänencontroller und dem ATA-Gateway. Auf diese Weise folgt das ATA-Gateway dem Domänencontroller, wenn dieser auf einen anderen Host verschoben wird. Dieser Ansatz funktioniert gut, solange nur wenige Domänencontroller vorhanden sind.
> [!NOTE]
> Wenn Ihre Umgebung V2V ((Virtual-to-Virtual) auf unterschiedlichen Hosts (RSPAN) unterstützt, müssen Sie sich zu Affinität keine Gedanken machen.
> 
-   Um zu gewährleisten, dass die ATA-Gateways ausreichende Kapazität für die eigenständige Überwachung aller Domänencontroller aufweisen, eignet sich folgende Option: Installieren Sie auf jedem Virtualisierungshost einen virtuellen Computer, und installieren Sie auf jeden Host ein ATA-Gateway. Konfigurieren Sie jedes ATA-Gateway so, dass es alle Domänencontroller überwacht, die auf dem betreffenden Cluster ausgeführt werden. Auf diese Weise wird jeder Host überwacht, auf dem Domänencontroller ausgeführt werden.

Überprüfen Sie nach dem Konfigurieren der Portspiegelung deren ordnungsgemäße Funktion, bevor Sie die ATA-Gateways installieren.

## Siehe auch
- [Überprüfen der Portspiegelung](validate-port-mirroring.md)
- [Installieren von ATA](install-ata.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


