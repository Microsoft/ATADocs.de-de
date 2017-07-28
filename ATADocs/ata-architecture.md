---
title: Advanced Threat Analytics-Architektur | Microsoft-Dokumentation
description: Beschreibt die Architektur von Microsoft Advance Threat Analytics (ATA)
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/5/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5410f706e84517eb964e991deeb21001a09d0cef
ms.sourcegitcommit: 42ce07e3207da10e8dd7585af0e34b51983c4998
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/25/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*




# <a name="ata-architecture"></a>ATA-Architektur
Dieses Diagramm veranschaulicht die Architektur von Advanced Threat Analytics:

![Topologiediagramm der ATA-Architektur](media/ATA-architecture-topology.jpg)

ATA überwacht den Datenverkehr Ihres Domänencontrollernetzwerk mit der Portspiegelung an ein ATA-Gateway mit physischen oder virtuellen Schaltern. Wenn Sie das ATA-Lightweight-Gateway direkt auf Ihren Domänencontrollern bereitstellen, ist die Portspiegelung nicht mehr erforderlich. Darüber hinaus kann ATA (direkt von den Domänencontrollern oder von einem SIEM-Server weitergeleitete) Windows-Ereignisse nutzen und die Daten analysieren, um nach Angriffen und Sicherheitsrisiken zu suchen.
In diesem Abschnitt wird der Ablauf der Netzwerk- und Ereigniserfassung beschrieben. Außerdem werden die Funktionen der Hauptkomponenten von ATA (ATA-Gateway, ATA-Lightweight-Gateway) und von ATA Center detailliert erläutert.


![Diagramm für ATA-Datenverkehrsfluss](media/ATA-traffic-flow.jpg)

## <a name="ata-components"></a>ATA-Komponenten
ATA umfasst die folgenden Komponenten:

-   **ATA Center** <br>
ATA Center empfängt Daten von beliebigen ATA-Gateways und/oder ATA-Lightweight-Gateways, die Sie bereitstellen.
-   **ATA-Gateway**<br>
Das ATA-Gateway wird auf einem dedizierten Server installiert, der den Datenverkehr der Domänencontroller mit Portspiegelung oder einem Netzwerk-TAP überwacht.
-   **ATA-Lightweight-Gateway**<br>
Das ATA-Lightweight-Gateway wird direkt auf den Domänencontrollern installiert und überwacht den Datenverkehr direkt, ohne dass ein dedizierter Server benötigt wird oder die Portspiegelung konfiguriert werden muss. Das ATA-Lightweight-Gateway ist eine Alternative zum ATA-Gateway.

Eine ATA-Bereitstellung kann aus einem einzigen ATA Center bestehen, das mit allen ATA-Gateways, allen ATA-Lightweight-Gateways oder einer Kombination aus ATA-Gateways und ATA-Lightweight-Gateways verbunden ist.


## <a name="deployment-options"></a>Bereitstellungsoptionen
Sie können ATA mit der folgenden Kombination von Gateways bereitstellen:

-   **Ausschließliche Verwendung von ATA-Gateways** <br>
Ihre ATA-Bereitstellung kann nur ATA-Gateways und keine ATA-Lightweight-Gateways enthalten: alle Domänencontroller müssen für die Portspiegelung auf ein ATA-Gateway konfiguriert sein, oder es müssen Netzwerk-TAPs vorhanden sein.
-   **Ausschließliche Verwendung von ATA-Lightweight-Gateways**<br>
Ihre ATA-Bereitstellung kann nur ATA-Lightweight-Gateways enthalten: die ATA-Lightweight-Gateways werden auf jedem Domänencontroller bereitgestellt, und es sind keine zusätzlichen Server oder Konfigurationen für die Portspiegelung erforderlich.
-   **Verwendung von ATA-Gateways und ATA-Lightweight-Gateways**<br>
Ihre ATA-Bereitstellung enthält sowohl ATA-Gateways als auch ATA-Lightweight-Gateways. Die ATA-Lightweight-Gateways werden auf einigen Ihrer Domänencontroller installiert (z.B. alle Domänencontroller am Standort Ihres Branchs). Gleichzeitig werden andere Domänencontroller von ATA-Gateways überwacht (z.B. die größeren Domänencontroller in Ihrem Hauptdatenzentrum).

In allen diesen Szenarios senden alle Gateways ihre Daten an ATA Center.




## <a name="ata-center"></a>ATA Center
Das **ATA-Center** führt die folgenden Funktionen aus:

-   Verwalten der Konfigurationseinstellungen für ATA-Gateway und ATA-Lightweight-Gateway

-   Empfangen von Daten von ATA-Gateways und ATA-Lightweight-Gateways 

-   Erkennen verdächtiger Aktivitäten

-   Ausführen von ATA-Machine Learning- und Verhaltensalgorithmen zum Erkennen von ungewöhnlichem Verhalten

-   Ausführen verschiedener deterministischer Algorithmen zum Erkennen erweiterter Angriffe basierend auf der „Attack Kill Chain“

-   Ausführen der ATA-Konsole

-   Optional: ATA Center kann zum Senden von E-Mail-Nachrichten und Ereignissen konfiguriert werden, wenn eine verdächtige Aktivität erkannt wird.

ATA Center empfängt analysierten Datenverkehr von dem ATA-Gateway und dem ATA-Lightweight-Gateway. Anschließend führt es die Profilerstellung, die deterministische Erkennung sowie Machine Learning- und Verhaltensalgorithmen aus, um Informationen über Ihr Netzwerk zu sammeln, um Anomalien zu erkennen und Sie bei verdächtigen Aktivitäten warnen zu können.

|||
|-|-|
|Entitätenempfänger|Empfängt Batches von Entitäten von allen ATA-Gateways und ATA-Lightweight-Gateways.|
|Netzwerkaktivitätenverarbeitung|Verarbeitet alle Netzwerkaktivitäten innerhalb der einzelnen empfangenen Batches. Beispiel: Zuordnung unterschiedlicher Kerberos-Schritte, die von potenziell verschiedenen Computern ausgeführt werden|
|Entityprofilerstellung|Erstellt Profile für alle eindeutigen Entitäten gemäß dem Datenverkehr und den Ereignissen. ATA aktualisiert zum Beispiel die Liste der angemeldeten Computer für jedes Benutzerprofil.|
|Center-Datenbank|Verwaltet das Schreiben der Netzwerkaktivitäten und Ereignisse in die Datenbank. |
|Datenbank|ATA verwendet MongoDB zum Speichern aller Daten im System:<br /><br />-   Netzwerkaktivitäten<br />-   Ereignisaktivitäten<br />-   Eindeutige Entitäten<br />-   Verdächtige Aktivitäten<br />-   ATA-Konfiguration|
|Detektoren|Die Detektoren verwenden Machine Learning-Algorithmen und deterministische Regeln, um verdächtige Aktivitäten und ungewöhnliches Benutzerverhalten im Netzwerk zu suchen.|
|ATA-Konsole|Die ATA-Konsole wird zum Konfigurieren von ATA und zum Überwachen verdächtiger Aktivitäten verwendet, die ATA in Ihrem Netzwerk erkennt. Die ATA-Konsole ist nicht vom ATA Center-Dienst abhängig und wird selbst dann ausgeführt, wenn der Dienst beendet wurde, solange die Kommunikation mit der Datenbank möglich ist.|
Berücksichtigen Sie Folgendes bei der Entscheidung, wie viele ATA Center Sie in Ihrem Netzwerk bereitstellen möchten:

-   Ein ATA Center kann eine einzelne Active Directory-Gesamtstruktur überwachen. Wenn Sie über mehrere Active Directory-Gesamtstrukturen verfügen, benötigen Sie mindestens ein ATA Center pro Active Directory-Gesamtstruktur.

-    In sehr großen Active Directory-Bereitstellungen ist ein einzelnes ATA Center möglicherweise nicht in der Lage, den gesamten Datenverkehr von allen Domänencontrollern zu verarbeiten. In diesem Fall werden mehrere ATA Center benötigt. Die Anzahl der ATA Center sollte durch die [ATA-Kapazitätsplanung](ata-capacity-planning.md) vorgegeben werden.

## <a name="ata-gateway-and-ata-lightweight-gateway"></a>ATA-Gateway und ATA-Lightweight-Gateway

### <a name="gateway-core-functionality"></a>Kernfunktionalität des Gateways
Das **ATA-Gateway** und das **ATA-Lightweight-Gateway** verfügen über die gleichen Kernfunktionen:

-   Erfassen und Untersuchen von Datenverkehr des Domänencontrollernetzwerks Dabei handelt es sich um portgespiegelten Datenverkehr für ATA-Gateways und lokalen Verkehr von Domänencontrollern in ATA-Lightweight-Gateways. 

-   Empfangen von Windows-Ereignissen von SIEM- oder Syslog-Servern oder von Domänencontrollern mithilfe der Windows-Ereignisweiterleitung

-   Abrufen von Daten über Benutzer und Computer aus der Active Directory-Domäne

-   Auflösen von Netzwerkentitäten (Benutzer, Gruppen und Computer)

-   Übertragen relevanter Daten an ATA Center

-   Überwachen mehrerer Domänencontroller über ein einziges ATA-Gateway bzw. Überwachen eines einzelnen Domänencontrollers durch ein ATA-Lightweight-Gateway.

Das ATA-Gateway empfängt den Netzwerkverkehr und die Windows-Ereignisse aus Ihrem Netzwerk und verarbeitet diese in den folgenden Hauptkomponenten:

|||
|-|-|
|Netzwerklistener|Der Netzwerklistener erfasst Netzwerkdatenverkehr und analysiert diesen. Diese Aufgabe sorgt für eine hohe CPU-Auslastung. Daher ist es besonders wichtig, beim Planen des ATA-Gateways oder des ATA-Lightweight-Gateways die [ATA-Voraussetzungen](ata-prerequisites.md) zu überprüfen.|
|Ereignislistener|Der Ereignislistener erfasst die von einem SIEM-Server in Ihrem Netzwerk weitergeleiteten Windows-Ereignisse und analysiert diese.|
|Windows-Ereignisprotokollleser|Der Windows-Ereignisprotokollleser liest Windows-Ereignisse und analysiert diejenigen, die von den Domänencontrollern an das Windows-Ereignisprotokoll des ATA-Gateway weitergeleitet werden.|
|Netzwerkaktivitätenübersetzer | Übersetzt analysierten Datenverkehr in eine logische Darstellung des von ATA verwendeten Datenverkehrs (NetworkActivity).
|Entitäten-Resolver|Der Entitäten-Resolver löst die analysierten Daten (Netzwerkverkehr und Ereignisse) mit Active Directory auf, um Konten- und Identitätsdaten zu suchen. Anschließend werden diese den in den analysierten Daten gefundenen IP-Adressen zugeordnet. Der Entitätenresolver untersucht die Paketheader gründlich, um die Analyse der Authentifizierungspakete in Bezug auf Computernamen, Eigenschaften und Identitäten zu ermöglichen. Der Entitätenresolver kombiniert die analysierten Authentifizierungspakete mit den Daten im tatsächlichen Paket.|
|Entitätensender|Der Entitätensender sendet die analysierten und zugeordneten Daten an ATA Center.|

## <a name="ata-lightweight-gateway-features"></a>Funktionen des ATA-Lightweight-Gateways

Die folgenden Funktionen funktionieren für ATA-Gateways und ATA-Lightweight-Gateways unterschiedlich.

-   Das ATA-Lightweight-Gateway kann Ereignisse lokal lesen, ohne die Ereignisweiterleitung zu konfigurieren.

-   **Kandidat für die Domänensynchronisierung**<br>
Das Gateway für die Domänensynchronisierung ist für die proaktive Synchronisierung aller Entitäten aus einer bestimmten Active Directory-Domäne verantwortlich (ähnlich dem Mechanismus, der von den Domänencontrollern selbst für die Replikation verwendet wird). Aus der Liste der Kandidaten wird nach dem Zufallsprinzip ein Gateway für die Domänensynchronisierung ausgewählt. <br><br>
Wenn das Gateway für die Domänensynchronisierung mehr als 30 Minuten offline ist, wird stattdessen ein anderer Kandidaten ausgewählt. Wenn für eine bestimmte Domäne kein Gateway für die Domänensynchronisierung verfügbar ist, kann ATA Entitäten und ihre Änderungen nicht proaktiv synchronisieren, ATA ruft jedoch reaktiv neue Entitäten ab werden, sobald sie im überwachten Datenverkehr erkannt werden. 
<br>Ist kein Gateway für die Domänensynchronisierung verfügbar und suchen Sie nach einer Entität, der kein Datenverkehr zugeordnet ist, werden keine Suchergebnisse angezeigt.<br><br>
Standardmäßig sind alle ATA-Gateways Kandidaten für die Domänensynchronisierung.<br><br>
Da alle ATA-Lightweight-Gateways eher in Filialen und auf kleinen Domänencontrollern bereitgestellt werden, sind sie standardmäßig keine Kandidaten für die Domänensynchronisierung.


-   **Ressourceneinschränkungen**<br>
Das ATA-Lightweight-Gateway enthält eine Überwachungskomponente, die die verfügbare Rechen- und Arbeitsspeicherkapazität auf dem Domänencontroller auswertet, auf dem es ausgeführt wird. Der Überwachungsprozess wird alle 10 Sekunden ausgeführt und aktualisiert das CPU- und Arbeitsspeicher-Auslastungskontingent für den ATA-Lightweight-Gateway-Prozess dynamisch, um sicherzustellen, dass der Domänencontroller zu jedem Zeitpunkt über mindestens 15 % freie Rechen- und Arbeitsspeicherressourcen verfügt.<br><br>
Unabhängig davon, was auf dem Domänencontroller geschieht, gibt dieser Prozess immer Ressourcen frei, um sicherzustellen, dass die Kernfunktionalität des Domänencontrollers nicht beeinträchtigt wird.<br><br>
Wenn dem ATA-Lightweight-Gateway dadurch nicht mehr genügend Ressourcen zur Verfügung stehen, wird nur ein Teil des Datenverkehrs überwacht, und die Überwachungswarnung „Netzwerkdatenverkehr aus Portspiegelung gelöscht“ wird auf der Statusseite angezeigt.

Die folgende Tabelle enthält ein Beispiel für einen Domänencontroller, der über genügend Rechenressourcen verfügt und ein größeres Kontingent als derzeit erforderlich bereitstellt und somit die Überwachung des gesamten Datenverkehrs ermöglicht:

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA-Lightweight-Gateway (Microsoft.Tri.Gateway.exe)|Sonstiges (andere Prozesse) |ATA-Lightweight-Gateway-Kontingent|Nimmt Gateway Löschungen vor|
|30%|20%|10%|45%|Nein|

Wenn Active Directory mehr Rechenkapazität erfordert, wird das vom ATA-Lightweight-Gateway benötigte Kontingent reduziert. Im folgenden Beispiel benötigt das ATA-Lightweight-Gateway mehr als das zugewiesene Kontingent und löscht einen Teil des Datenverkehrs (der Datenverkehr wird nur teilweise überwacht):

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA-Lightweight-Gateway (Microsoft.Tri.Gateway.exe)|Sonstiges (andere Prozesse) |ATA-Lightweight-Gateway-Kontingent|Nimmt Gateway Löschungen vor|
|60%|15%|10%|15%|Ja|



## <a name="your-network-components"></a>Ihre Netzwerkkomponenten
Stellen Sie für die Arbeit mit ATA Folgendes sicher:

### <a name="port-mirroring"></a>Portspiegelung
Wenn Sie ATA-Gateways verwenden, müssen Sie für die Domänencontroller, die überwacht werden, die Portspiegelung einrichten und das ATA-Gateway als Ziel mit den physischen oder virtuellen Switches festlegen. Eine andere Möglichkeit ist die Verwendung von Netzwerk-TAPs. ATA funktioniert auch, wenn nur einige, aber nicht alle Domänencontroller überwacht werden, allerdings ist die Erkennung dann weniger effektiv.

In diesem Fall wird nur ein sehr kleiner Prozentsatz dieses Datenverkehrs komprimiert und zur Analyse an ATA Center gesendet, während durch die Portspiegelung sämtlicher Netzwerkverkehr der Domänencontroller an das ATA-Gateway gesendet wird.

Die Domänencontroller und die ATA-Gateways können physisch oder virtuell sein. Weitere Informationen finden Sie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md).


### <a name="events"></a>Ereignisse
Um die ATA-Erfassung von Pass-the-Hash, Brute Force, die Modifizierung von sensiblen Gruppen und Honey Token zu verbessern, benötigt ATA die folgenden Windows-Ereignisse: 4776, 4732, 4733, 4728, 4729, 4756 und 4757. Diese können entweder automatisch vom ATA-Lightweight-Gateway gelesen werden, oder, falls das ATA-Lightweight-Gateway nicht bereitgestellt wurde, an das ATA-Gateway weitergeleitet werden. Dazu gibt es zwei Möglichkeiten: zum einen das Konfigurieren des ATA-Gateways, sodass es auf SIEM-Ereignisse lauscht, oder das [Konfigurieren der Windows-Ereignisweiterleitung](#configuring-windows-event-forwarding).

-   Konfigurieren des ATA-Gateways zum Überwachen von SIEM-Ereignissen <br>Konfigurieren Sie SIEM zum Weiterleiten bestimmter Windows-Ereignisse an ATA. ATA unterstützt eine Reihe von SIEM-Anbietern. Weitere Informationen finden Sie unter [Konfigurieren der Ereignissammlung](configure-event-collection.md).

-   Konfigurieren der Windows-Ereignisweiterleitung<br>Eine andere Möglichkeit, wie ATA Ihre Ereignisse erhalten kann, besteht darin, die Domänencontroller so zu konfigurieren, dass das Windows-Ereignis 4776, 4732, 4733, 4728, 4729, 4756 und 4757 an das ATA-Gateway weitergeleitet wird. Dies ist insbesondere dann nützlich, wenn Sie nicht über SIEM verfügen oder SIEM von ATA derzeit nicht unterstützt wird. Weitere Informationen zur Windows-Ereignisweiterleitung in ATA finden Sie unter [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md#configuring-windows-event-forwarding). Beachten Sie, dass dies nur für physische ATA-Gateways gilt und nicht für ATA-Lightweight-Gateways.

## <a name="see-also"></a>Weitere Informationen
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

