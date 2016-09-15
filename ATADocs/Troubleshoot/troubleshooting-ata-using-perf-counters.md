---
title: Behandeln von Problemen mit ATA mithilfe der Leistungsindikatoren | Microsoft ATA
description: Beschreibt die Verwendung von Leistungsindikatoren zum Behandeln von Problemen mit ATA
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/21/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: df162a62-f273-4465-9887-94271f5000d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 21f28848dd22cfbcbb4b4871300621203b445fb4
ms.openlocfilehash: a6113c106653039ca3b4337d9250d9b9baca4611


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# Problembehandlung bei ATA mithilfe der Leistungsindikatoren
Die ATA-Leistungsindikatoren bieten Einblick in die Leistungsgrade der einzelnen ATA-Komponenten. Die Komponenten in ATA verarbeiten Daten sequenziell. Wenn also ein Problem vorliegt, kann dies dazu führen, dass an irgendeinem Punkt in der Komponentenkette ein Teil des Datenverkehrs verworfen wird. Um das Problem zu beheben, müssen Sie herausfinden, welche Komponente den Fehler bewirkt, und das Problem am Anfang der Kette beheben. Verwenden Sie Daten aus den Leistungsindikatoren, um zu verstehen, wie jede Komponente funktioniert.
Eine Beschreibung des Datenflusses zwischen internen ATA-Komponenten finden Sie unter [ATA-Architektur](/advanced-threat-analytics/plan-design/ata-architecture).

**ATA-Komponentenprozess**:

1.  Wenn eine Komponente ihre maximale Größe erreicht, wird verhindert, dass die vorgeschaltete Komponente weitere Entitäten an sie sendet.

2.  Dadurch steigt die Größe der **vorgeschalteten** Komponente, bis auch sie die eigene vorgeschaltete Komponente am Versand weiterer Entitäten hindert.

3.  Dieser Vorgang setzt sich fort, bis die NetworkListener-Komponente erreicht ist, die vorhandenen Datenverkehr löscht, wenn keine Entitäten mehr weitergeleitet werden können.


## Leistungsindikatoren für das ATA-Gateway

In diesem Abschnitt gilt jeder Verweis auf das ATA-Gateway auch für das ATA-Lightweight-Gateway.

Sie können den Leistungszustand des ATA-Gateways in Echtzeit verfolgen, indem Sie die Leistungsindikatoren des ATA-Gateways hinzufügen.
Hierzu öffnen Sie „Leistungsüberwachung“ und fügen dort die Indikatoren für das ATA-Gateway hinzu. Der Name des Leistungsindikatorobjekts lautet: „Microsoft ATA-Gateway“.

Auf folgende Indikatoren für das ATA-Gateway sollte hauptsächlich geachtet werden:

|Leistungsindikator|Beschreibung|Schwellenwert|Problembehandlung|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Gateway\NetworkListener PEF Parser Messages/Sec|Die Menge des Datenverkehrs, der pro Sekunde vom ATA-Gateway verarbeitet wird.|Kein Schwellenwert|Hilft bei der Einschätzung des vom ATA-Gateway analysierten Datenverkehrs.|
|NetworkListener PEF Dropped Events/Sec|Die Menge des Datenverkehrs, der pro Sekunde vom ATA-Gateway gelöscht wird.|Diese Zahl muss immer 0 sein (seltene kurze Löschvorgänge sind akzeptabel).|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|ATA GW Counter/NetworkListener ETW Dropped Events/Sec|Die Menge des Datenverkehrs, der pro Sekunde vom ATA-Gateway gelöscht wird.|Diese Zahl muss immer 0 sein (seltene kurze Löschvorgänge sind akzeptabel).|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|ATA GW Counter/NetworkActivityTranslator Message Data # Block Size|Die Menge des Datenverkehrs in der Warteschlange für die Übersetzung in Netzwerkaktivitäten (NAs).|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 100.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|ATA GW Counter/EntityResolver Activity Block Size|Die Menge der Netzwerkaktivitäten (NAs) in der Warteschlange für die Auflösung.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 10.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|ATA GW Counter/EntitySender Entity Batch Block Size|Die Menge der Netzwerkaktivitäten (NAs) in der Warteschlange für den Versand an ATA Center.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 1.000.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|ATA GW Counter/EntitySender Batch Send Time|Die Zeitdauer, die zum Senden des letzten Batches benötigt wurde.|Sollte in den meisten Fällen weniger als 1000 Millisekunden betragen.|Überprüfen Sie, ob Netzwerkprobleme zwischen dem ATA-Gateway und ATA Center vorliegen.|

> [!NOTE]
> -   Die Zeitindikatoren werden in Millisekunden angegeben.
> -   Es ist manchmal hilfreich, die vollständige Liste der Leistungsindikatoren in Form des Diagrammtyps „Bericht“ zu überwachen. (Beispiel: Echtzeitüberwachung aller Leistungsindikatoren)

## Leistungsindikatoren für das ATA-Lightweight-Gateway
Die Leistungsindikatoren können zur Kontingentverwaltung auf dem Lightweight-Gateway verwendet werden, um sicherzustellen, dass ATA nicht zu viele Ressourcen von den Domänencontrollern bezieht, auf denen es installiert ist.
Fügen Sie die folgenden Leistungsindikatoren hinzu, um die Ressourcenbeschränkungen zu messen, die ATA auf dem Lightweight-Gateway erzwingt:

Öffnen Sie „Leistungsüberwachung“, und fügen Sie dort alle Leistungsindikatoren für das ATA-Lightweight-Gateway hinzu. Der Name der Leistungsindikatorobjekte lautet: „Microsoft ATA Gateway“ und „Microsoft ATA Gateway Updater“.


|Leistungsindikator|Beschreibung|Schwellenwert|Problembehandlung|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager CPU Time Max %|Die maximale CPU-Zeit (in Prozent), die der Lightweight-Gatewayprozess nutzen kann. |Kein Schwellenwert. | Dies ist die Einschränkung, die verhindert, dass das ATA-Lightweight-Gateway die Ressourcen des Domänencontrollers vollständig erschöpft. Wenn Sie bemerken, dass der Prozess innerhalb eines Zeitraums häufig den maximalen Grenzwert erreicht (der Prozess erreicht das Limit und anschließend wird Datenverkehr gelöscht), müssen Sie dem Server mit dem Domänencontroller mehr Ressourcen hinzufügen.|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Commit Memory Max Size|Die maximale Menge von zugewiesenem Arbeitsspeicher (in Bytes), die der Lightweight-Gatewayprozess nutzen kann.|Kein Schwellenwert. | Dies ist die Einschränkung, die verhindert, dass das ATA-Lightweight-Gateway die Ressourcen des Domänencontrollers vollständig erschöpft. Wenn Sie bemerken, dass der Prozess innerhalb eines Zeitraums häufig den maximalen Grenzwert erreicht (der Prozess erreicht das Limit und anschließend wird Datenverkehr gelöscht), müssen Sie dem Server mit dem Domänencontroller mehr Ressourcen hinzufügen.| 
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Working Set Limit Size|Die maximale Menge von physischem Speicher (in Bytes), die der Lightweight-Gatewayprozess nutzen kann.|Kein Schwellenwert. | Dies ist die Einschränkung, die verhindert, dass das ATA-Lightweight-Gateway die Ressourcen des Domänencontrollers vollständig erschöpft. Wenn Sie bemerken, dass der Prozess innerhalb eines Zeitraums häufig den maximalen Grenzwert erreicht (der Prozess erreicht das Limit und anschließend wird Datenverkehr gelöscht), müssen Sie dem Server mit dem Domänencontroller mehr Ressourcen hinzufügen.|



Verwenden Sie die folgenden Leistungsindikatoren, um Ihren tatsächlichen Verbrauch zu erfahren:



|Leistungsindikator|Beschreibung|Schwellenwert|Problembehandlung|
|-----------|---------------|-------------|-------------------|
|Process(Microsoft.Tri.Gateway)\%Processor Time|Die CPU-Zeit (in Prozent), die der Lightweight-Gatewayprozess zurzeit verwendet. |Kein Schwellenwert. | Vergleichen Sie die Ergebnisse dieses Leistungsindikators mit dem Grenzwert von GatewayUpdaterResourceManager CPU Time Max %. Wenn Sie bemerken, dass der Prozess innerhalb eines Zeitraums häufig den maximalen Grenzwert erreicht (der Prozess erreicht das Limit und anschließend wird Datenverkehr gelöscht), müssen Sie für das Lightweight-Gateway mehr Ressourcen bereitstellen.|
|Process(Microsoft.Tri.Gateway)\Private Bytes|Die Menge von zugewiesenem Arbeitsspeicher (in Bytes), die der Lightweight-Gatewayprozess zurzeit verwendet.|Kein Schwellenwert. | Vergleichen Sie die Ergebnisse dieses Leistungsindikators mit dem Grenzwert von GatewayUpdaterResourceManager Commit Memory Max Size. Wenn Sie bemerken, dass der Prozess innerhalb eines Zeitraums häufig den maximalen Grenzwert erreicht (der Prozess erreicht das Limit und anschließend wird Datenverkehr gelöscht), müssen Sie für das Lightweight-Gateway mehr Ressourcen bereitstellen.| 
|Process(Microsoft.Tri.Gateway)\Working Set|Die Menge von physischem Speicher (in Bytes), die der Lightweight-Gatewayprozess zurzeit verwendet.|Kein Schwellenwert. |Vergleichen Sie die Ergebnisse dieses Leistungsindikators mit dem Grenzwert von GatewayUpdaterResourceManager Working Set Limit Size. Wenn Sie bemerken, dass der Prozess innerhalb eines Zeitraums häufig den maximalen Grenzwert erreicht (der Prozess erreicht das Limit und anschließend wird Datenverkehr gelöscht), müssen Sie für das Lightweight-Gateway mehr Ressourcen bereitstellen.|

## Leistungsindikatoren für ATA Center
Sie können den Leistungszustand von ATA Center in Echtzeit verfolgen, indem Sie die Leistungsindikatoren von ATA Center hinzufügen.

Hierzu öffnen Sie „Leistungsüberwachung“ und fügen dort die Indikatoren für ATA Center hinzu. Der Name des Leistungsindikatorobjekts lautet: „Microsoft ATA Center“.

Auf folgende Indikatoren für ATA Center sollte hauptsächlich geachtet werden:

|Leistungsindikator|Beschreibung|Schwellenwert|Problembehandlung|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Center\EntityReceiver Entity Batch Block Size|Die Anzahl der Entitätenbatches in der Warteschlange von ATA Center.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 10.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren.  Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|Microsoft ATA Center\NetworkActivityProcessor Network Activity Block Size|Die Anzahl der Netzwerkaktivitäten (NAs) in der Warteschlange für die Verarbeitung.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 50.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|Microsoft ATA Center\EntityProfiler Network Activity Block Size|Die Anzahl der Netzwerkaktivitäten (NAs) in der Warteschlange für die Profilerstellung.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 10.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|
|Microsoft ATA Center\CenterDatabase &#42; Block Size|Die Anzahl der Netzwerkaktivitäten eines bestimmten Typs in der Warteschlange für das Schreiben in die Datenbank.|Sollte niedriger sein als der Maximalwert - 1 (Standardmaximalwert: 50.000)|Überprüfen Sie, ob Komponenten vorhanden sind, die ihre Maximalgröße erreicht haben und daher vorgeschaltete Komponenten bis hin zum NetworkListener blockieren. Informationen hierzu finden Sie oben im Abschnitt **ATA-Komponentenprozess**.<br /><br />Überprüfen Sie, ob Probleme bei CPU oder Arbeitsspeicher vorliegen.|


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
|\LogicalDisk&#42;\Disk Writes/sec|Die Übertragungsrate für Schreibvorgänge auf den Datenträger.|Kein Schwellenwert|Leistungsindikatoren für die Laufwerkauslastung (können nützliche Hinweise bei der Fehlerbehandlung der Speicherlatenz geben).|
|\LogicalDisk(&#42;)\Disk Write Bytes/sec|Die Anzahl der Bytes pro Sekunde, die auf den Datenträger geschrieben werden.|Kein Schwellenwert|Leistungsindikatoren für die Laufwerkauslastung können nützliche Hinweise bei der Fehlerbehandlung der Speicherlatenz geben.|

## Weitere Informationen
- [ATA-Voraussetzungen](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-Kapazitätsplanung](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurieren der Windows-Ereignisweiterleitung](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


