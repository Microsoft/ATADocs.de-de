---
title: Problembehandlung bei Advanced Threat Analytics mithilfe der Leistungsindikatoren | Microsoft-Dokumentation
description: Beschreibt die Verwendung von Leistungsindikatoren zum Behandeln von Problemen mit ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: df162a62-f273-4465-9887-94271f5000d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c7a0ded6092740f92c12fbd7c57100293bf735c2
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46134125"
---
*Gilt für: Advanced Threat Analytics Version 1.9*



# <a name="troubleshooting-ata-using-the-performance-counters"></a>Problembehandlung bei ATA mithilfe der Leistungsindikatoren
Die ATA-Leistungsindikatoren bieten Einblick in die Leistungsgrade der einzelnen ATA-Komponenten. Die Komponenten in ATA verarbeiten Daten sequenziell. Wenn also ein Problem vorliegt, kann dies dazu führen, dass an irgendeinem Punkt in der Komponentenkette ein Teil des Datenverkehrs verworfen wird. Um das Problem zu beheben, müssen Sie herausfinden, welche Komponente den Fehler bewirkt, und das Problem am Anfang der Kette beheben. Verwenden Sie Daten aus den Leistungsindikatoren, um zu verstehen, wie jede Komponente funktioniert.
Eine Beschreibung des Datenflusses zwischen internen ATA-Komponenten finden Sie unter [ATA-Architektur](ata-architecture.md).

**ATA-Komponentenprozess**:

1.  Wenn eine Komponente ihre maximale Größe erreicht, wird verhindert, dass die vorgeschaltete Komponente weitere Entitäten an sie sendet.

2.  Dadurch steigt die Größe der **vorgeschalteten** Komponente, bis auch sie die eigene vorgeschaltete Komponente am Versand weiterer Entitäten hindert.

3.  Dieser Vorgang setzt sich fort, bis die NetworkListener-Komponente erreicht ist, die vorhandenen Datenverkehr löscht, wenn keine Entitäten mehr weitergeleitet werden können.


## <a name="retrieving-performance-monitor-files-for-troubleshooting"></a>Abrufen von Leistungsüberwachungsdateien für die Problembehandlung

Um die Leistungsüberwachungsdateien (BLG) aus den verschiedenen ATA-Komponenten abzurufen, gehen Sie wie folgt vor:
1.  Öffnen Sie perfmon.
2.  Beenden Sie den Datensammlersatz mit dem Namen **Microsoft ATA Gateway** oder **Microsoft ATA Center**.
3.  Navigieren Sie zum Ordner „Datensammlersatz“ (In der Standardeinstellung finden Sie diesen unter „C:\Programme\Microsoft Advanced Thread Analytics\Gateway\Protokolle\DataCollectorSets“ oder „C:\Programme\Microsoft Advanced Threat Analytics\Center\Protokolle\DataCollectorSets“).
4.  Kopieren Sie die BLG-Datei, die zuletzt geändert wurde.
5.  Starten Sie den Datensammlersatz mit dem Namen **Microsoft ATA Gateway** oder **Microsoft ATA Center** erneut.


## <a name="ata-gateway-performance-counters"></a>Leistungsindikatoren für das ATA-Gateway

In diesem Abschnitt gilt jeder Verweis auf das ATA-Gateway auch für das ATA-Lightweight-Gateway.

Sie können den Leistungszustand des ATA-Gateways in Echtzeit verfolgen, indem Sie die Leistungsindikatoren des ATA-Gateways hinzufügen.
Öffnen Sie hierzu den **Systemmonitor**, und fügen Sie dort die Indikatoren für das ATA-Gateway hinzu. Der Name des Leistungsindikatorobjekts lautet **Microsoft ATA-Gateway**.

Auf folgende Indikatoren für das ATA-Gateway sollte hauptsächlich geachtet werden:

> [!div class="mx-tableFixed"]
|Leistungsindikator|Beschreibung|Schwellenwert|Problembehandlung|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Gateway\NetworkListener PEF Parser Messages\Sec|Die Menge des Datenverkehrs, der pro Sekunde vom ATA-Gateway verarbeitet wird.|Kein Schwellenwert|Hilft bei der Einschätzung des vom ATA-Gateway analysierten Datenverkehrs.|
|NetworkListener PEF Dropped Events\Sec|Die Menge des Datenverkehrs, der pro Sekunde vom ATA-Gateway gelöscht wird.|Diese Zahl muss immer 0 sein (seltene kurze Löschvorgänge sind akzeptabel).|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|Microsoft ATA Gateway\NetworkListener ETW Dropped Events\Sec|Die Menge des Datenverkehrs, der pro Sekunde vom ATA-Gateway gelöscht wird.|Diese Zahl muss immer 0 sein (seltene kurze Löschvorgänge sind akzeptabel).|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|Microsoft ATA Gateway\NetworkActivityTranslator Message Data # Block Size|Die Menge des Datenverkehrs in der Warteschlange für die Übersetzung in Netzwerkaktivitäten (NAs).|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 100.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|Microsoft ATA Gateway\EntityResolver Activity Block Size|Die Anzahl der Netzwerkaktivitäten (NAs), die aufgelöst werden sollen, in der Warteschlange.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 10.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|Microsoft ATA Gateway\EntitySender Entity Batch Block Size|Die Menge der Netzwerkaktivitäten (NAs) in der Warteschlange für den Versand an ATA Center.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 1.000.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|Microsoft ATA Gateway\EntitySender Batch Send Time|Die Zeitdauer, die zum Senden des letzten Batches benötigt wurde.|Sollte in den meisten Fällen weniger als 1000 Millisekunden betragen.|Überprüfen Sie, ob Netzwerkprobleme zwischen dem ATA-Gateway und ATA Center vorliegen.|

> [!NOTE]
> -   Die Zeitindikatoren werden in Millisekunden angegeben.
> -   Es ist manchmal hilfreich, die vollständige Liste der Leistungsindikatoren in Form des Diagrammtyps **Bericht** zu überwachen. (Beispiel: Echtzeitüberwachung aller Leistungsindikatoren).

## <a name="ata-lightweight-gateway-performance-counters"></a>Leistungsindikatoren für das ATA-Lightweight-Gateway
Die Leistungsindikatoren können zur Kontingentverwaltung auf dem Lightweight-Gateway verwendet werden, um sicherzustellen, dass ATA nicht zu viele Ressourcen von den Domänencontrollern bezieht, auf denen es installiert ist.
Fügen Sie diese Leistungsindikatoren hinzu, um die Ressourcenbeschränkungen zu messen, die ATA auf dem Lightweight-Gateway erzwingt.

Öffnen Sie hierzu die **Leistungsüberwachung**, und fügen Sie alle Indikatoren für das ATA-Lightweight-Gateway hinzu. Die Namen der Leistungsindikatorobjekte lauten **Microsoft ATA Gateway** und **Microsoft ATA Gateway Updater**.

> [!div class="mx-tableFixed"]
|Leistungsindikator|Beschreibung|Schwellenwert|Problembehandlung|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager CPU Time Max %|Die maximale CPU-Zeit (in Prozent), die der Lightweight-Gatewayprozess nutzen kann. |Kein Schwellenwert. | Dies ist die Einschränkung, die verhindert, dass das ATA-Lightweight-Gateway die Ressourcen des Domänencontrollers vollständig erschöpft. Wenn Sie bemerken, dass der Prozess innerhalb eines Zeitraums häufig den maximalen Grenzwert erreicht (der Prozess erreicht das Limit und anschließend wird Datenverkehr gelöscht), müssen Sie dem Server mit dem Domänencontroller mehr Ressourcen hinzufügen.|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Commit Memory Max Size|Die maximale Menge von zugewiesenem Arbeitsspeicher (in Bytes), die der Lightweight-Gatewayprozess nutzen kann.|Kein Schwellenwert. | Dies ist die Einschränkung, die verhindert, dass das ATA-Lightweight-Gateway die Ressourcen des Domänencontrollers vollständig erschöpft. Wenn Sie bemerken, dass der Prozess innerhalb eines Zeitraums häufig den maximalen Grenzwert erreicht (der Prozess erreicht das Limit und anschließend wird Datenverkehr gelöscht), müssen Sie dem Server mit dem Domänencontroller mehr Ressourcen hinzufügen.| 
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Working Set Limit Size|Die maximale Menge von physischem Speicher (in Bytes), die der Lightweight-Gatewayprozess nutzen kann.|Kein Schwellenwert. | Dies ist die Einschränkung, die verhindert, dass das ATA-Lightweight-Gateway die Ressourcen des Domänencontrollers vollständig erschöpft. Wenn Sie bemerken, dass der Prozess innerhalb eines Zeitraums häufig den maximalen Grenzwert erreicht (der Prozess erreicht das Limit und anschließend wird Datenverkehr gelöscht), müssen Sie dem Server mit dem Domänencontroller mehr Ressourcen hinzufügen.|



Verwenden Sie die folgenden Leistungsindikatoren, um Ihren tatsächlichen Verbrauch zu erfahren:


> [!div class="mx-tableFixed"]
|Leistungsindikator|Beschreibung|Schwellenwert|Problembehandlung|
|-----------|---------------|-------------|-------------------|
|Process(Microsoft.Tri.Gateway)\%Processor Time|Die CPU-Zeit (in Prozent), die der Lightweight-Gatewayprozess zurzeit verwendet. |Kein Schwellenwert. | Vergleichen Sie die Ergebnisse dieses Leistungsindikators mit dem Grenzwert von GatewayUpdaterResourceManager CPU Time Max %. Wenn Sie bemerken, dass der Prozess innerhalb eines Zeitraums häufig den maximalen Grenzwert erreicht (der Prozess erreicht das Limit und anschließend wird Datenverkehr gelöscht), müssen Sie für das Lightweight-Gateway mehr Ressourcen bereitstellen.|
|Process(Microsoft.Tri.Gateway)\Private Bytes|Die Menge von zugewiesenem Arbeitsspeicher (in Bytes), die der Lightweight-Gatewayprozess zurzeit verwendet.|Kein Schwellenwert. | Vergleichen Sie die Ergebnisse dieses Leistungsindikators mit dem Grenzwert von GatewayUpdaterResourceManager Commit Memory Max Size. Wenn Sie bemerken, dass der Prozess innerhalb eines Zeitraums häufig den maximalen Grenzwert erreicht (der Prozess erreicht das Limit und anschließend wird Datenverkehr gelöscht), müssen Sie für das Lightweight-Gateway mehr Ressourcen bereitstellen.| 
|Process(Microsoft.Tri.Gateway)\Working Set|Die Menge von physischem Speicher (in Bytes), die der Lightweight-Gatewayprozess zurzeit verwendet.|Kein Schwellenwert. |Vergleichen Sie die Ergebnisse dieses Leistungsindikators mit dem Grenzwert von GatewayUpdaterResourceManager Working Set Limit Size. Wenn Sie bemerken, dass der Prozess innerhalb eines Zeitraums häufig den maximalen Grenzwert erreicht (der Prozess erreicht das Limit und anschließend wird Datenverkehr gelöscht), müssen Sie für das Lightweight-Gateway mehr Ressourcen bereitstellen.|

## <a name="ata-center-performance-counters"></a>Leistungsindikatoren für ATA Center
Sie können den Leistungszustand von ATA Center in Echtzeit verfolgen, indem Sie die Leistungsindikatoren von ATA Center hinzufügen.

Öffnen Sie hierzu die **Leistungsüberwachung**, und fügen Sie dort die Indikatoren für ATA Center hinzu. Der Name des Leistungsindikatorobjekts lautet **Microsoft ATA Center**.

Auf folgende Indikatoren für ATA Center sollte hauptsächlich geachtet werden:

> [!div class="mx-tableFixed"]
|Leistungsindikator|Beschreibung|Schwellenwert|Problembehandlung|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Center\EntityReceiver Entity Batch Block Size|Die Anzahl der Entitätenbatches in der Warteschlange von ATA Center.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 10.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren.  Informationen hierzu finden Sie im vorhergehenden Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|Microsoft ATA Center\NetworkActivityProcessor Network Activity Block Size|Die Anzahl der Netzwerkaktivitäten (NAs) in der Warteschlange für die Verarbeitung.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 50.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie im vorhergehenden Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|Microsoft ATA Center\EntityProfiler Network Activity Block Size|Die Anzahl der Netzwerkaktivitäten (NAs) in der Warteschlange für die Profilerstellung.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 10.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie im vorhergehenden Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|Microsoft ATA Center\Database &#42; Block Size|Die Anzahl der Netzwerkaktivitäten eines bestimmten Typs in der Warteschlange für das Schreiben in die Datenbank.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 50.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie im vorhergehenden Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|


> [!NOTE]
> -   Die Zeitindikatoren werden in Millisekunden angegeben
> -   Es ist manchmal hilfreich, die vollständige Liste der Leistungsindikatoren in Form des Diagrammtyps „Bericht“ zu überwachen (Beispiel: Echtzeitüberwachung aller Leistungsindikatoren).

## <a name="operating-system-counters"></a>Leistungsindikatoren des Betriebssystems
In der folgenden Tabelle werden die Leistungsindikatoren des Betriebssystems aufgeführt, auf die hauptsächlich geachtet werden sollte:

> [!div class="mx-tableFixed"]
|Leistungsindikator|Beschreibung|Schwellenwert|Problembehandlung|
|-----------|---------------|-------------|-------------------|
|Prozessor(_Total)\%Prozessorzeit (%)|Die prozentuale Angabe der vergangenen Prozessorzeit, die zum Ausführen eines Threads benötigt wird, der sich nicht im Leerlauf befindet.|Weniger als 80 % im Durchschnitt|Überprüfen Sie, ob ein bestimmter Prozess wesentlich mehr Prozessorzeit verbraucht, als sinnvoll ist.<br /><br />Fügen Sie weitere Prozessoren hinzu.<br /><br />Reduzieren Sie den Umfang des Datenverkehrs pro Server.<br /><br />Der Indikator „Prozessor(_Total)\%Prozessorzeit (%)“ ist möglicherweise auf virtuellen Servern weniger genau. In diesem Fall ist die genauere Möglichkeit zum Messen einer verringerten Prozessorleistung der Indikator „System\Prozessor-Warteschlangenlänge“.|
|System\Context Switches\sec|Die kombinierte Häufigkeit, mit der die Prozessoren von einem Thread zu einem anderen umgeschaltet werden.|Weniger als 5.000 &#42; Kerne (physische Kerne)|Überprüfen Sie, ob ein bestimmter Prozess wesentlich mehr Prozessorzeit verbraucht, als sinnvoll ist.<br /><br />Fügen Sie weitere Prozessoren hinzu.<br /><br />Reduzieren Sie den Umfang des Datenverkehrs pro Server.<br /><br />Der Indikator „Prozessor(_Total)\%Prozessorzeit (%)“ ist möglicherweise auf virtuellen Servern weniger genau. In diesem Fall ist die genauere Möglichkeit zum Messen einer verringerten Prozessorleistung der Indikator „System\Prozessor-Warteschlangenlänge“.|
|System\Prozessor-Warteschlangenlänge|Die Anzahl der Threads, die zur Ausführung bereit sind und auf Zeitplanung warten.|Weniger als fünf (physische) &#42;Kerne|Überprüfen Sie, ob ein bestimmter Prozess wesentlich mehr Prozessorzeit verbraucht, als sinnvoll ist.<br /><br />Fügen Sie weitere Prozessoren hinzu.<br /><br />Reduzieren Sie den Umfang des Datenverkehrs pro Server.<br /><br />Der Indikator „Prozessor(_Total)\%Prozessorzeit (%)“ ist möglicherweise auf virtuellen Servern weniger genau. In diesem Fall ist die genauere Möglichkeit zum Messen einer verringerten Prozessorleistung der Indikator „System\Prozessor-Warteschlangenlänge“.|
|Memory\Available MBytes|Die Menge des für die Zuteilung zur Verfügung stehenden physischen Speichers (RAM).|Sollte mehr als 512 betragen|Überprüfen Sie, ob ein bestimmter Prozess wesentlich mehr physischen Speicher verbraucht, als sinnvoll ist.<br /><br />Erhöhen Sie die Menge des physischen Speichers.<br /><br />Reduzieren Sie den Umfang des Datenverkehrs pro Server.|
|LogicalDisk(&#42;)\Avg. Disk sec\Read|Die durchschnittlich auftretende Latenz beim Lesen von Daten vom Datenträger (als Instanz sollte das Datenbanklaufwerk ausgewählt werden).|Sollte weniger als 10 Millisekunden betragen|Überprüfen Sie, ob ein bestimmter Prozess das Datenbanklaufwerk mehr als sinnvoll verwendet.<br /><br />Informieren Sie sich beim Team/Anbieter, von dem der Speicher bereitstellt wird, ob dieses Laufwerk die aktuelle Workload mit weniger als 10 ms Latenz bereitstellen kann. Die aktuelle Workload kann mithilfe der Leistungsindikatoren für die Laufwerkauslastung ermittelt werden.|
|LogicalDisk(&#42;)\Avg. Disk sec\Write|Die durchschnittlich auftretende Latenz beim Schreiben von Daten auf den Datenträger (als Instanz sollte das Datenbanklaufwerk ausgewählt werden).|Sollte weniger als 10 Millisekunden betragen|Überprüfen Sie, ob ein bestimmter Prozess das Datenbanklaufwerk mehr als sinnvoll verwendet.<br /><br />Informieren Sie sich beim Team/Anbieter, von dem der Speicher bereitstellt wird, ob dieses Laufwerk die aktuelle Workload mit weniger als 10 ms Latenz bereitstellen kann. Die aktuelle Workload kann mithilfe der Leistungsindikatoren für die Laufwerkauslastung ermittelt werden.|
|\LogicalDisk(&#42;)\Disk Reads\sec|Die Übertragungsrate für Lesevorgänge auf dem Datenträger.|Kein Schwellenwert|Leistungsindikatoren für die Laufwerkauslastung können nützliche Hinweise bei der Fehlerbehandlung der Speicherlatenz geben.|
|\LogicalDisk(&#42;)\Disk Read Bytes\sec|Die Anzahl der Bytes pro Sekunde, die vom Datenträger gelesen werden.|Kein Schwellenwert|Leistungsindikatoren für die Laufwerkauslastung können nützliche Hinweise bei der Fehlerbehandlung der Speicherlatenz geben.|
|\LogicalDisk&#42;\Disk Writes\sec|Die Übertragungsrate für Schreibvorgänge auf den Datenträger.|Kein Schwellenwert|Leistungsindikatoren für die Laufwerkauslastung (können nützliche Hinweise bei der Fehlerbehandlung der Speicherlatenz geben).|
|\LogicalDisk(&#42;)\Disk Write Bytes\sec|Die Anzahl der Bytes pro Sekunde, die auf den Datenträger geschrieben werden.|Kein Schwellenwert|Leistungsindikatoren für die Laufwerkauslastung können nützliche Hinweise bei der Fehlerbehandlung der Speicherlatenz geben.|

## <a name="see-also"></a>Weitere Informationen
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
