---
# required metadata

title: Problembehandlung bei ATA mithilfe der Leistungsindikatoren | Microsoft Advanced Threat Analytics
description: Beschreibt die Verwendung von Leistungsindikatoren zum Behandeln von Problemen mit ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: df162a62-f273-4465-9887-94271f5000d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Problembehandlung bei ATA mithilfe der Leistungsindikatoren
Die ATA-Leistungsindikatoren bieten Einblick in die Leistungsgrade der einzelnen ATA-Komponenten. Die Komponenten in ATA verarbeiten Daten sequenziell, d. h., liegt ein Problem vor, verursacht es eine Kettenreaktion, die verringerten Datenverkehr verursacht. Um das Problem zu beheben, müssen Sie herausfinden, welche Komponente den Fehler bewirkt, und das Problem am Anfang der Kette beheben.
Eine Beschreibung des Datenflusses zwischen internen ATA-Komponenten finden Sie unter [ATA-Architektur](/advanced-threat-analytics/plan-design/ata-architecture).

**ATA-Komponentenprozess**:

1.  Wenn eine Komponente ihre maximale Größe erreicht, wird verhindert, dass die vorgeschaltete Komponente weitere Entitäten an sie sendet.

2.  Dadurch steigt die Größe der **vorgeschalteten** Komponente, bis auch sie die eigene vorgeschaltete Komponente am Versand weiterer Entitäten hindert.

3.  Dieser Vorgang setzt sich fort, bis die ursprüngliche NetworkListener-Komponente erreicht ist, die vorhandenen Datenverkehr abweist, wenn keine Entitäten mehr weitergeleitet werden können.

4. Verwenden Sie Daten aus den Leistungsindikatoren, um zu verstehen, wie jede Komponente funktioniert.

## Leistungsindikatoren für das ATA-Gateway

In diesem Abschnitt gilt jeder Verweis auf das ATA-Gateway auch für das ATA-Lightweight-Gateway.

Sie können den Leistungszustand des ATA-Gateways in Echtzeit verfolgen, indem Sie die Leistungsindikatoren des ATA-Gateways hinzufügen.
Hierzu öffnen Sie „Leistungsüberwachung“ und fügen dort die Indikatoren für das ATA-Gateway hinzu. Der Name des Leistungsindikatorobjekts lautet: „Microsoft ATA-Gateway“.

![Abbildung – Hinzufügen von Leistungsindikatoren](media/ATA-performance-counters.png)

Auf folgende Indikatoren für das ATA-Gateway sollte hauptsächlich geachtet werden:

|Leistungsindikator|Beschreibung|Schwellenwert|Problembehandlung|
|-----------|---------------|-------------|-------------------|
|NetworkListener PEF Parser Messages/Sec|Die Menge des Datenverkehrs, der pro Sekunde vom ATA-Gateway verarbeitet wird.|Kein Schwellenwert|Hilft bei der Einschätzung des vom ATA-Gateway analysierten Datenverkehrs.|
|NetworkListener PEF Dropped Events/Sec|Die Menge des Datenverkehrs, der pro Sekunde vom ATA-Gateway gelöscht wird.|Diese Zahl muss immer 0 sein (seltene kurze Löschvorgänge sind akzeptabel).|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|NetworkListener ETW Dropped Events/Sec|Die Menge des Datenverkehrs, der pro Sekunde vom ATA-Gateway gelöscht wird.|Diese Zahl muss immer 0 sein (seltene kurze Löschvorgänge sind akzeptabel).|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|NetworkActivityTranslator Message Data # Block Size|Die Menge des Datenverkehrs in der Warteschlange für die Übersetzung in Netzwerkaktivitäten (NAs).|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 100.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|EntityResolver Activity Block Size|Die Menge der Netzwerkaktivitäten (NAs) in der Warteschlange für die Auflösung.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 10.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|EntitySender Entity Batch Block Size|Die Menge der Netzwerkaktivitäten (NAs) in der Warteschlange für den Versand an ATA Center.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 1.000.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|EntitySender Batch Send Time|Die Zeitdauer, die zum Senden des letzten Batches benötigt wurde.|Sollte in den meisten Fällen weniger als 1000 Millisekunden betragen.|Überprüfen Sie, ob Netzwerkprobleme zwischen dem ATA-Gateway und ATA Center vorliegen.|

> [!NOTE]
> -   Die Zeitindikatoren werden in Millisekunden angegeben.
> -   Es ist manchmal hilfreich, die vollständige Liste der Leistungsindikatoren in Form des Diagrammtyps „Bericht“ zu überwachen. (Beispiel: Echtzeitüberwachung aller Leistungsindikatoren)

## Leistungsindikatoren für ATA Center
Sie können den Leistungszustand von ATA Center in Echtzeit verfolgen, indem Sie die Leistungsindikatoren von ATA Center hinzufügen.

Hierzu öffnen Sie „Leistungsüberwachung“ und fügen dort die Indikatoren für ATA Center hinzu. Der Name des Leistungsindikatorobjekts lautet: „Microsoft ATA Center“.

![Hinzufügen von Leistungsindikatoren für ATA Center](media/ATA-Gateway-perf-counters.png)

Auf folgende Indikatoren für ATA Center sollte hauptsächlich geachtet werden:

|Leistungsindikator|Beschreibung|Schwellenwert|Problembehandlung|
|-----------|---------------|-------------|-------------------|
|EntityReceiver Entity Batch Block Size|Die Anzahl der Entitätenbatches in der Warteschlange von ATA Center.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 10.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren.  Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|NetworkActivityProcessor Network Activity Block Size|Die Anzahl der Netzwerkaktivitäten (NAs) in der Warteschlange für die Verarbeitung.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 50.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|EntityProfiler Network Activity Block Size|Die Anzahl der Netzwerkaktivitäten (NAs) in der Warteschlange für die Profilerstellung.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 10.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|CenterDatabase &#42; Block Size|Die Anzahl der Netzwerkaktivitäten eines bestimmten Typs in der Warteschlange für das Schreiben in die Datenbank.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 50.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|


> [!NOTE]
> -   Die Zeitindikatoren werden in Millisekunden angegeben
> -   Es ist manchmal hilfreich, die vollständige Liste der Leistungsindikatoren in Form des Diagrammtyps „Bericht“ zu überwachen. (Beispiel: Echtzeitüberwachung aller Leistungsindikatoren)

## Leistungsindikatoren des Betriebssystems
In der folgenden Liste sind die Leistungsindikatoren des Betriebssystems aufgeführt, auf die hauptsächlich geachtet werden sollte:

|Leistungsindikator|Beschreibung|Schwellenwert|Problembehandlung|
|-----------|---------------|-------------|-------------------|
|Prozessor(_Total)\%Prozessorzeit (%)|Die prozentuale Angabe der vergangenen Prozessorzeit, die zum Ausführen eines Threads benötigt wird, der sich nicht im Leerlauf befindet.|Weniger als 80 % im Durchschnitt|Überprüfen Sie, ob ein bestimmter Prozess wesentlich mehr Prozessorzeit verbraucht, als sinnvoll ist.<br /><br />Fügen Sie weitere Prozessoren hinzu.<br /><br />Reduzieren Sie den Umfang des Datenverkehrs pro Server.<br /><br />Der Indikator „Prozessor(_Total)\%Prozessorzeit (%)“ ist möglicherweise auf virtuellen Servern weniger genau. In diesem Fall ist die genauere Möglichkeit zum Messen einer verringerten Prozessorleistung der Indikator „System\Prozessor-Warteschlangenlänge“.|
|System\Context Switches/sec|Die kombinierte Häufigkeit, mit der die Prozessoren von einem Thread zu einem anderen umgeschaltet werden.|Weniger als 5.000 &#42; Kerne (physische Kerne)|Überprüfen Sie, ob ein bestimmter Prozess wesentlich mehr Prozessorzeit verbraucht, als sinnvoll ist.<br /><br />Fügen Sie weitere Prozessoren hinzu.<br /><br />Reduzieren Sie den Umfang des Datenverkehrs pro Server.<br /><br />Der Indikator „Prozessor(_Total)\%Prozessorzeit (%)“ ist möglicherweise auf virtuellen Servern weniger genau. In diesem Fall ist die genauere Möglichkeit zum Messen einer verringerten Prozessorleistung der Indikator „System\Prozessor-Warteschlangenlänge“.|
|System\Prozessor-Warteschlangenlänge|Die Anzahl der Threads, die zur Ausführung bereit sind und auf Zeitplanung warten.|Weniger als 5 &#42; Kerne (physische Kerne)|Überprüfen Sie, ob ein bestimmter Prozess wesentlich mehr Prozessorzeit verbraucht, als sinnvoll ist.<br /><br />Fügen Sie weitere Prozessoren hinzu.<br /><br />Reduzieren Sie den Umfang des Datenverkehrs pro Server.<br /><br />Der Indikator „Prozessor(_Total)\%Prozessorzeit (%)“ ist möglicherweise auf virtuellen Servern weniger genau. In diesem Fall ist die genauere Möglichkeit zum Messen einer verringerten Prozessorleistung der Indikator „System\Prozessor-Warteschlangenlänge“.|
|Memory\Available MBytes|Die Menge des für die Zuteilung zur Verfügung stehenden physischen Speichers (RAM).|Sollte mehr als 512 betragen|Überprüfen Sie, ob ein bestimmter Prozess wesentlich mehr physischen Speicher verbraucht, als sinnvoll ist.<br /><br />Erhöhen Sie die Menge des physischen Speichers.<br /><br />Reduzieren Sie den Umfang des Datenverkehrs pro Server.|
|LogicalDisk(&#42;)\Avg. Sek./Lesevorgänge“.|Die durchschnittlich auftretende Latenz beim Lesen von Daten vom Datenträger (als Instanz sollte das Datenbanklaufwerk ausgewählt werden).|Sollte weniger als 10 Millisekunden betragen|Überprüfen Sie, ob ein bestimmter Prozess das Datenbanklaufwerk mehr als sinnvoll verwendet.<br /><br />Informieren Sie sich bei dem Team/Anbieter, von dem der Speicher bereitstellt wird, ob dieses Laufwerk die aktuelle Workload mit weniger als 10 ms Latenz bereitstellen kann. Die aktuelle Workload kann mithilfe der Leistungsindikatoren für die Laufwerkauslastung ermittelt werden.|
|LogicalDisk(&#42;)\Avg. Sek./Schreibvorgänge|Die durchschnittlich auftretende Latenz beim Schreiben von Daten auf den Datenträger (als Instanz sollte das Datenbanklaufwerk ausgewählt werden).|Sollte weniger als 10 Millisekunden betragen|Überprüfen Sie, ob ein bestimmter Prozess das Datenbanklaufwerk mehr als sinnvoll verwendet.<br /><br />Informieren Sie sich bei dem Team/Anbieter, von dem der Speicher bereitstellt wird, ob dieses Laufwerk die aktuelle Workload mit weniger als 10 ms Latenz bereitstellen kann. Die aktuelle Workload kann mithilfe der Leistungsindikatoren für die Laufwerkauslastung ermittelt werden.|
|\LogicalDisk(&#42;)\Disk Reads/sec|Die Übertragungsrate für Lesevorgänge auf dem Datenträger.|Kein Schwellenwert|Leistungsindikatoren für die Laufwerkauslastung können nützliche Hinweise bei der Fehlerbehandlung der Speicherlatenz geben.|
|\LogicalDisk(&#42;)\Disk Read Bytes/sec|Die Anzahl der Bytes pro Sekunde, die vom Datenträger gelesen werden.|Kein Schwellenwert|Leistungsindikatoren für die Laufwerkauslastung können nützliche Hinweise bei der Fehlerbehandlung der Speicherlatenz geben.|
|\LogicalDisk(&#42;)\Disk Writes/sec|Die Übertragungsrate für Schreibvorgänge auf den Datenträger.|Kein Schwellenwert|Leistungsindikatoren für die Laufwerkauslastung (können nützliche Hinweise bei der Fehlerbehandlung der Speicherlatenz geben).|
|\LogicalDisk(&#42;)\Disk Write Bytes/sec|Die Anzahl der Bytes pro Sekunde, die auf den Datenträger geschrieben werden.|Kein Schwellenwert|Leistungsindikatoren für die Laufwerkauslastung können nützliche Hinweise bei der Fehlerbehandlung der Speicherlatenz geben.|

## Weitere Informationen
- [ATA-Voraussetzungen](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-Kapazitätsplanung](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurieren der Windows-Ereignisweiterleitung](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


