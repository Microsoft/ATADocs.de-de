---
title: Planen der Advanced Threat Analytics-Bereitstellung (ATA) | Microsoft-Dokumentation
description: Hilft bei der Planung Ihrer Bereitstellung und der Entscheidung, wie viele ATA-Server für Ihr Netzwerk erforderlich sind.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 10/16/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.assetid: 1b5b24ff-0df8-4660-b4f8-64d68cc72f65
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0ec953c4311c12a44686cbbf4f4394492f74dd7f
ms.sourcegitcommit: 05f23a0add8d24ae92176e13c2a4ae8ada1844da
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79319153"
---
# <a name="ata-capacity-planning"></a>ATA-Kapazitätsplanung

*Gilt für: Advanced Threat Analytics Version 1.9*

Anhand dieses Artikels können Sie ermitteln, wie viele ATA-Server zur Überwachung Ihres Netzwerks benötigt werden. Es hilft Ihnen zu schätzen, wie viele ATA-Gateways und/oder ATA-Lightweight-Gateways Sie benötigen und welche Serverkapazität für ATA Center und ATA-Gateways erforderlich ist.

> [!NOTE] 
> ATA Center kann auf jedem IaaS-Anbieter bereitgestellt werden, solange die Leistungsanforderungen erfüllt werden, die in diesem Artikel beschrieben sind.

## <a name="using-the-sizing-tool"></a>Verwenden das Tools zur Größenanpassung
Die empfohlene und einfachste Methode zum Ermitteln der Kapazität für die ATA-Bereitstellung besteht in der Verwendung des [ATA-Tools zur Größenanpassung](https://aka.ms/atasizingtool). Führen Sie das ATA-Tool zur Größenanpassung aus, und verwenden Sie aus den Excel-Dateiergebnissen heraus die folgenden Felder zum Ermitteln der benötigten ATA-Kapazität:

- ATA Center-CPU und -Arbeitsspeicher: Gleichen Sie das Feld **Busy Packets/sec** in der ATA Center-Tabelle in der Ergebnisdatei mit dem Feld **PACKETS PER SECOND** in der [ATA Center-Tabelle](#ata-center-sizing) ab.

- ATA Center-Speicher: Gleichen Sie das Feld **Avg Packets/sec** in der ATA Center-Tabelle in der Ergebnisdatei mit dem Feld **PACKETS PER SECOND** in der [ATA Center-Tabelle](#ata-center-sizing) ab.
- ATA-Gateway: Gleichen Sie das Feld **Busy Packets/sec** in der ATA-Gateway-Tabelle in der Ergebnisdatei mit dem Feld **PACKETS PER SECOND** in der [ATA Gateway-Tabelle](#ata-gateway-sizing) oder der [ATA Lightweight Gateway-Tabelle](#ata-lightweight-gateway-sizing) ab, je nach [ausgewähltem Gateway](#choosing-the-right-gateway-type-for-your-deployment).


![Beispiel für das Kapazitätsplanungstool](media/capacity-tool.png)


> [!NOTE]
> Da sich Umgebungen unterscheiden und besondere und unerwartete Eigenschaften beim Datenverkehr aufweisen, kann es sein, dass Sie, nachdem Sie ATA zum ersten Mal bereitgestellt haben und das Tool zum Anpassen der Größe ausführen, die Kapazität Ihrer Bereitstellung anpassen und optimieren müssen.


Wenn Sie das ATA-Tool zur Größenanpassung aus irgendeinem Grund nicht verwenden können, sammeln Sie die Informationen zum Pakete/Sek.-Leistungsindikator manuell von allen Domänencontrollern über einen Zeitraum von 24 Stunden mit einem niedrigen Erfassungsintervall (etwa 5 Sekunden). Berechnen Sie dann für jeden Domänen Controller den täglichen Durchschnitt und den am stärksten ausgelasteten Zeitraum (15 Minuten).
In den folgenden Abschnitten finden Sie Anweisungen zum Erfassen des Zählers/Sek. für einen Domänen Controller.


> [!NOTE]
> Da sich Umgebungen unterscheiden und besondere und unerwartete Eigenschaften beim Datenverkehr aufweisen, kann es sein, dass Sie, nachdem Sie ATA zum ersten Mal bereitgestellt haben und das Tool zum Anpassen der Größe ausführen, die Kapazität Ihrer Bereitstellung anpassen und optimieren müssen.


### <a name="ata-center-sizing"></a>Größenzuteilung für ATA Center
Für die Analyse des Benutzerverhaltens benötigt das ATA Center die Daten von mindestens 30 Tagen.
 

|Pakete pro Sekunde von allen Domänencontrollern|CPU (Kerne&#42;)|Arbeitsspeicher (GB)|Datenbankspeicher pro Tag (GB)|Datenbankspeicher pro Monat (GB)|IOPS&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1\.000|2|32|0.3|9|30 (100)
|40,000|4|48|12|360|500 (750)
|200.000|8|64|60|1\.800|1\.000 (1.500)
|400.000|12|96|120|3,600|2\.000 (2.500)
|750,000|24|112|225|6,750|2,500 (3,000)
|1,000,000|40|128|300|9\.000|4,000 (5,000)

&#42;Dies umfasst physische Kerne, keine Hyperthreadingkerne.

&#42;&#42;Durchschnittliche Werte (Spitzenwerte)
> [!NOTE]
> - ATA Center kann auf allen überwachten Domänen Controllern aggregierte maximal 1 Mio. Pakete pro Sekunde verarbeiten. In einigen Umgebungen kann dasselbe ATA Center den gesamten Datenverkehr über 1 Mio. verarbeiten, und einige Umgebungen überschreiten möglicherweise die ATA-Kapazität. Kontaktieren Sie uns unter azureatpfeedback@microsoft.com, um Unterstützung beim Planen und schätzen von großen Umgebungen zu erhalten.

> - Wenn der freie Speicherplatz auf 20 % oder 200 GB fällt, wird die älteste Sammlung gelöscht. Wenn es nicht möglich ist, die Datensammlung erfolgreich auf diesen Wert zu senken, wird eine Warnung ausgelöst.  ATA funktioniert weiterhin, bis der Grenzwert von 5 % oder 50 GB erreicht ist.  Dann füllt ATA die Datenbank nicht weiter mit Daten auf, und eine Warnung wird ausgelöst.
> - Es ist möglich, ATA Center auf jedem IaaS-Anbieter bereitzustellen, solange die Leistungsanforderungen erfüllt werden, die in diesem Artikel beschrieben sind.
> - Die Speicherlatenz für Lese- und Schreibvorgänge sollte unter 10 ms betragen.
> - Das Verhältnis zwischen Schreib- und Lesevorgängen beträgt unterhalb von 100.000 Paketen pro Sekunde etwa 1:3 und oberhalb dieser Grenze etwa 1:6.
> - Wenn das Center als virtueller Computer (VM) ausgeführt wird, ist es erforderlich, dass der gesamte Arbeitsspeicher dem virtuellen Computer ständig zugeordnet wird. Weitere Informationen zum Ausführen von ATA Center als virtuellen Computer finden Sie unter [Anforderungen für ATA Center](https://docs.microsoft.com/advanced-threat-analytics/ata-prerequisites#dynamic-memory) .
> - Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** von ATA Center auf **Hohe Leistung** fest.<br>
> - Wenn Sie auf einem physischen Server arbeiten, erfordert die ATA-Datenbank, dass Sie den nicht einheitlichen Speicherzugriff (Non-Uniform Memory Access, NUMA) im BIOS **deaktivieren**. Das System bezieht sich möglicherweise als Knotenüberlappung auf NUMA. In diesem Fall müssen Sie die Knotenüberlappung **aktivieren**, um NUMA zu deaktivieren. Weitere Informationen finden Sie in der BIOS-Dokumentation. Dies ist nicht relevant, wenn ATA Center auf einem virtuellen Server ausgeführt wird.


## <a name="choosing-the-right-gateway-type-for-your-deployment"></a>Auswählen des richtigen Gatewaytyps für die Bereitstellung
In einer ATA-Umgebung wird jede Kombination der ATA-Gatewaytypen unterstützt:

- Ausschließlich ATA-Gateways
- Ausschließlich ATA-Lightweight-Gateways
- Eine Kombination aus beiden Typen

Berücksichtigen Sie folgende Vorteile bei der Entscheidung für den Bereitstellungstyp für das Gateway:

|Gatewaytyp|Vorteile|Cost|Bereitstellungstopologie|Domänencontrollerverwendung|
|----|----|----|----|-----|
|ATA-Gateway|Eine Out-of-Band-Bereitstellung erschwert es Angreifern, herauszufinden, ob ATA vorhanden ist.|Höher|Neben dem Domänencontroller installiert (out-of-band).|Unterstützt bis zu 50.000 Pakete pro Sekunde.|
|ATA-Lightweight-Gateway|Erfordert keinen dedizierten Server und keine Konfiguration der Portspiegelung.|KLEIN|Auf dem Domänencontroller installiert.|Unterstützt bis zu 10.000 Pakete pro Sekunde.|

Es folgen Beispiele für Szenarien, in denen Domänencontroller durch das ATA-Lightweight-Gateway abgedeckt werden sollten:


- Filialstandorte

- Virtuelle Domänencontroller, die in der Cloud bereitgestellt wurden (IaaS).


Es folgen Beispiele für Szenarien, in denen Domänencontroller durch das ATA-Gateway abgedeckt werden sollten:


- Rechenzentren an Hauptstandorten (mit Domänencontrollern mit mehr als 10.000 Paketen pro Sekunde).


### <a name="ata-lightweight-gateway-sizing"></a>Dimensionierung von ATA-Lightweight-Gateways

Ein ATA-Lightweight-Gateway kann die Überwachung eines Domänencontrollers basierend auf der Menge des vom Domänencontroller erzeugten Netzwerkverkehrs unterstützen. 


|Pakete pro Sekunde&#42;|CPU (Kerne&#42;&#42;)|Arbeitsspeicher (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1\.000|2|6|
|5,000|6|16|
    |10.000|10|24|

&#42;Gesamtanzahl der Pakete pro Sekunde auf dem von dem betreffenden ATA-Lightweight-Gateway überwachten Domänencontroller.

&#42;&#42;Gesamtanzahl der Kerne ohne Hyperthreading, die auf diesem Domänencontroller installiert sind.<br>Hyperthreading ist zwar für das ATA-Lightweight-Gateway akzeptabel, bei der Kapazitätsplanung sollten Sie aber die tatsächlichen Kernen und nicht die Kerne mit Hyperthreading zählen.

&#42;&#42;&#42;Gesamtgröße des auf diesem Domänencontroller installierten Arbeitsspeichers.

> [!NOTE]   
> -   Wenn der Domänencontroller nicht über die für das ATA-Lightweight-Gateway erforderlichen Ressourcen verfügt, wird die Leistung des Domänencontrollers zwar nicht beeinträchtigt, aber das ATA-Lightweight-Gateway funktioniert möglicherweise nicht wie erwartet.
> -   Wenn das Center als virtueller Computer (VM) ausgeführt wird, ist es erforderlich, dass der gesamte Arbeitsspeicher dem virtuellen Computer ständig zugeordnet wird. Weitere Informationen zum Ausführen von ATA Center als virtuellen Computer finden Sie unter [Anforderungen für ATA Center](https://docs.microsoft.com/advanced-threat-analytics/ata-prerequisites#dynamic-memory).)
> -   Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des ATA-Lightweight-Gateways auf **Hohe Leistung** fest.
> -   Es sind mindestens 5 GB Speicherplatz erforderlich, und 10 GB werden empfohlen, einschließlich des Speicherplatzes, der für die ATA-Binärdateien, [ATA-Protokolle](troubleshooting-ata-using-logs.md) und [Leistungsprotokolle](troubleshooting-ata-using-perf-counters.md) benötigt wird.


### <a name="ata-gateway-sizing"></a>Bemessung von ATA-Gateways

Berücksichtigen Sie folgende Fehler bei der Entscheidung, wie viele ATA-Gateways bereitgestellt werden sollen.

-   **Active Directory-Gesamtstrukturen und -Domänen**<br>
    ATA kann den Datenverkehr aus mehreren Domänen einer einzigen Active Directory-Gesamtstruktur überwachen. Die Überwachung mehrerer Active Directory-Gesamtstrukturen erfordert separate ATA-Bereitstellungen. Für die Überwachung des Netzwerkdatenverkehrs von Domänencontrollern in unterschiedlichen Gesamtstrukturen sollte keine einzelne ATA-Bereitstellung konfiguriert werden.

-   **Portspiegelung**<br>
Überlegungen zur Portspiegelung machen möglicherweise die Bereitstellung mehrerer ATA-Gateways pro Rechenzentrum oder Filialstandort erforderlich.

-   **Kapazität**<br>
    Ein ATA-Gateway kann die Überwachung von mehreren Domänencontrollern unterstützen, abhängig vom Umfang des Netzwerkverkehrs der überwachten Domänencontroller. 
<br>



|Pakete pro Sekunde&#42;|CPU (Kerne&#42;&#42;)|Arbeitsspeicher (GB)|
|---------------------------|-------------------------|---------------|
|1\.000|1|6|
|5,000|2|10|
|10.000|3|12|
|20.000|6|24|
|50.000|16|48|

&#42;Durchschnittliche Gesamtanzahl der Pakete pro Sekunde von allen Domänencontrollern, die von dem betreffenden ATA-Gateway überwacht werden, und zwar zum Zeitpunkt der höchsten Nutzung.

&#42;Die Gesamtmenge des per Portspiegelung verarbeiteten Domänencontroller-Datenverkehrs darf die Kapazität der für das Sammeln verwendeten NIC auf dem ATA-Gateway nicht überschreiten.

&#42;&#42;Hyperthreading muss deaktiviert sein.

> [!NOTE] 
> -   Wenn das Center als virtueller Computer (VM) ausgeführt wird, ist es erforderlich, dass der gesamte Arbeitsspeicher dem virtuellen Computer ständig zugeordnet wird. Weitere Informationen zum Ausführen von ATA Center als virtuellen Computer finden Sie unter [Anforderungen für ATA Center](https://docs.microsoft.com/advanced-threat-analytics/ata-prerequisites#dynamic-memory) .
> -   Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des ATA-Gateways auf **Hohe Leistung** fest.
> -   Es sind mindestens 5 GB Speicherplatz erforderlich, und 10 GB werden empfohlen, einschließlich des Speicherplatzes, der für die ATA-Binärdateien, [ATA-Protokolle](troubleshooting-ata-using-logs.md) und [Leistungsprotokolle](troubleshooting-ata-using-perf-counters.md) benötigt wird.



## <a name="related-videos"></a>Verwandte Videos
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Weitere Informationen:
- [Tool zur Bemessung von ATA-Gateways](https://aka.ms/atasizingtool)
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Architektur](ata-architecture.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
