---
title: Azure Advanced Threat Protection-Architektur | Microsoft-Dokumentation
description: Beschreibt die Architektur von Azure Advance Threat Analytics (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/20/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c7fda04658dc70406fc7c0d543286e46da4cfa86
ms.sourcegitcommit: 56886d06abd25035ffc9885c69aca9b0ebf14abc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2018
ms.locfileid: "43039078"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="azure-atp-architecture"></a>Azure ATP-Architektur
Architektur von Azure Advanced Threat Protection:

![Topologiediagramm der Azure ATP-Architektur](media/atp-architecture-topology.png)

Azure ATP überwacht den Datenverkehr Ihres Domänencontrollernetzwerks über die Portspiegelung an einem eigenständigen Azure ATP-Sensor mit physischen oder virtuellen Switches. Wenn Sie den Azure ATP-Sensor direkt auf Ihren Domänencontrollern bereitstellen, ist die Portspiegelung nicht mehr erforderlich. Darüber hinaus kann Azure ATP (direkt von den Domänencontrollern oder von einem SIEM-Server weitergeleitete) Windows-Ereignisse nutzen und die Daten analysieren, um nach Angriffen und Sicherheitsrisiken zu suchen. Azure ATP empfängt analysierten Datenverkehr von dem Azure ATP-Sensor und dem eigenständigen Azure ATP-Sensor. Anschließend führt Azure ATP die Profilerstellung, die deterministische Erkennung sowie Machine Learning- und Verhaltensalgorithmen aus, um Informationen über Ihr Netzwerk sammeln, die Erkennung von Anomalien ermöglichen und Sie bei verdächtigen Aktivitäten warnen zu können.

In diesem Abschnitt wird der Ablauf der Netzwerk- und Ereigniserfassung beschrieben. Außerdem werden die Funktionen der Hauptkomponenten von ATP detailliert erläutert: der Azure ATP-Sensor, der eigenständige Azure ATP-Sensor (der über dieselben Kernfunktionen wie der Azure ATP-Sensor verfügt, jedoch zusätzliche Hardware, Portspiegelung und Konfigurationen erfordert und nicht die Erkennung basierend auf der Ereignisablaufverfolgung für Windows (ETW) unterstützt) und der Azure ATP-Clouddienst. 

Bei direkter Installation auf Domänencontrollern greift der ATP-Sensor direkt vom Domänencontroller auf die erforderlichen Ereignisprotokolle zu. Nach Analyse dieser Protokolle und des Netzwerkdatenverkehrs durch den Sensor sendet Azure ATP nur diese analysierten Informationen (nicht alle Protokolle) an den Azure ATP-Dienst.

## <a name="azure-atp-components"></a>Azure ATP-Komponenten
Azure ATP umfasst die folgenden Komponenten:

-   **Azure ATP-Portal zur Verwaltung von Arbeitsbereichen** <br>
Über das Azure ATP-Portal zur Verwaltung von Arbeitsbereichen können Sie Arbeitsbereiche erstellen und verwalten und Integrationen in andere Microsoft-Dienste vornehmen.

-   **Azure ATP-Arbeitsbereichsportal** <br>
Das Azure ATP-Arbeitsbereichsportal empfängt Daten von ATP-Sensoren und eigenständigen Sensoren. Es überwacht, verwaltet und untersucht Bedrohungen in Ihrer Umgebung.

-   **Azure ATP-Sensor**<br>
Der Azure ATP-Sensor wird direkt auf den Domänencontrollern installiert und überwacht den Datenverkehr direkt, ohne dass ein dedizierter Server benötigt wird oder die Portspiegelung konfiguriert werden muss. 

-   **Eigenständiger Azure ATP-Sensor**<br>
Der eigenständige Azure ATP-Sensor wird auf einem dedizierten Server installiert, der den Datenverkehr der Domänencontroller mit Portspiegelung oder einem Netzwerk-TAP überwacht. Es stellt eine Alternative zum Azure ATP-Sensor dar, der zusätzliche Hardware, Portspiegelung und Konfigurationen erfordert. Eigenständige Azure ATP-Sensoren unterstützen nicht die Erkennung basierend auf der Ereignisablaufverfolgung für Windows (ETW), die vom ATP-Sensor unterstützt werden. 

## <a name="deployment-options"></a>Bereitstellungsoptionen
Sie können Azure ATP mit der folgenden Kombination von Sensoren bereitstellen:

-   **Ausschließliche Verwendung von Azure ATP-Sensoren**<br>
Ihre Azure ATP-Bereitstellung kann ausschließlich Azure ATP-Sensoren enthalten: Die Azure ATP-Sensoren werden direkt auf jedem Domänencontroller bereitgestellt, und es sind keine zusätzlichen Server oder Konfigurationen für die Portspiegelung erforderlich.

-   **Ausschließliche Verwendung von eigenständigen Azure ATP-Sensoren** <br>
Ihre Azure ATP-Bereitstellung kann ausschließlich eigenständige Azure ATP-Sensoren (ohne Azure ATP-Sensoren) enthalten: Alle Domänencontroller müssen so konfiguriert sein, dass die Portspiegelung auf eigenständigen Azure ATP-Sensoren oder Netzwerk-TAPs aktiviert ist.

-   **Verwendung von sowohl eigenständigen Azure ATP-Sensoren als auch Azure ATP-Sensoren**<br>
Ihre Azure ATP-Bereitstellung umfasst sowohl eigenständige Azure ATP-Sensoren als auch Azure ATP-Sensoren. Die Azure ATP-Sensoren werden auf einigen Ihrer Domänencontroller installiert (z.B. alle Domänencontroller in Ihren Filialen). Gleichzeitig werden andere Domänencontroller von eigenständigen Azure ATP-Sensoren überwacht (z.B. die größeren Domänencontroller in Ihren Hauptrechenzentren). 


### <a name="azure-atp-management-portal"></a>Azure ATP-Verwaltungsportal

Über das Azure ATP-Verwaltungsportal können Sie folgende Vorgänge durchführen:

-   Erstellen und Verwalten Ihres Azure ATP-Arbeitsbereichs

-   Integrieren in andere Microsoft-Sicherheitsdienste

> [!NOTE]
> - Azure ATP unterstützt derzeit die Erstellung von lediglich einem Arbeitsbereich. Nachdem Sie einen Arbeitsbereich gelöscht haben, können Sie den Support kontaktieren, um den Arbeitsbereich erneut zu aktivieren. Sie können maximal drei Arbeitsbereiche löschen. Kontaktieren Sie den Azure ATP-Support, um die Anzahl an gespeicherten bzw. gelöschten Arbeitsbereichen zu erhöhen.
> - Wenn innerhalb von 60 Tagen kein Sensor in Ihrem Arbeitsbereich installiert wird, kann es sein, dass der Arbeitsbereich gelöscht wird und Sie ihn erneut erstellen müssen.



### <a name="azure-atp-workspace-portal"></a>Azure ATP-Arbeitsbereichsportal

Über den Azure ATP-Arbeitsbereich können Sie die folgenden Azure ATP-Funktionen verwalten:

-   Verwalten der Konfigurationseinstellungen des Azure ATP-Sensors und des eigenständigen Sensors

-   Anzeigen von Daten, die sowohl von den eigenständigen Azure ATP-Sensoren als auch von den Azure ATP-Sensoren gesendet wurden 

-   Überwachen von ermittelten verdächtigen Aktivitäten basierend auf verhaltensbedingten Machine Learning-Algorithmen zum Ermitteln von ungewöhnlichem Verhalten und deterministische Algorithmen zum Ermitteln von erweiterten Angriffen basierend auf der Kette der Angriffsabwehr

-   Optional: Das Portal zur Verwaltung von Arbeitsbereichen kann so konfiguriert sein, dass es E-Mails und Ereignisse sendet, wenn verdächtige Aktivitäten oder Integritätsereignisse ermittelt werden.


|||
|-|-|
|Azure ATP-Verwaltungsportal|Verwaltet Ihren Azure ATP-Arbeitsbereich.|
|Azure ATP-Arbeitsbereichsportal|Der Azure ATP-Arbeitsbereich wird verwendet, um Azure ATP zu konfigurieren und verdächtige Aktivitäten zu überwachen, die von Azure ATP auf Ihrem Netzwerk erkannt werden. Der Azure ATP-Arbeitsbereich ist nicht vom Azure ATP-Sensor abhängig und wird sogar weiter ausgeführt, wenn der Azure ATP-Sensordienst angehalten wird. |
|Detektoren|Die Detektoren verwenden Machine Learning-Algorithmen und deterministische Regeln, um verdächtige Aktivitäten und ungewöhnliches Benutzerverhalten im Netzwerk zu suchen.|


## <a name="azure-atp-sensor-and-azure-atp-standalone-sensor"></a>Azure ATP-Sensor und eigenständiger Azure ATP-Sensor

Der **Azure ATP-Sensor** und der **eigenständige Azure ATP-Sensor** verfügen über die gleichen Kernfunktionen:

-   Erfassen und Untersuchen von Datenverkehr des Domänencontrollernetzwerks Dabei handelt es sich um lokalen Datenverkehr von Domänencontrollern in Azure ATP-Sensoren und portgespiegelten Datenverkehr für eigenständige Azure ATP-Sensoren. 

-   Empfangen von Windows-Ereignissen – entweder direkt über den Domänencontroller (für ATP-Sensoren) oder über SIEM- bzw. Syslog-Server (für eigenständige Azure ATP-Sensoren)

-   Empfangen von Informationen zur RADIUS-Kontoführung über den VPN-Anbieter

-   Abrufen von Daten über Benutzer und Computer aus der Active Directory-Domäne

-   Auflösen von Netzwerkentitäten (Benutzer, Gruppen und Computer)

-   Übertragen von relevanten Daten in den Azure ATP-Clouddienst

-   Überwachen eines einzelnen Domänencontrollers für einen Azure ATP-Sensor oder Überwachen von mehreren Domänencontrollern über einen eigenständigen Azure ATP-Sensor.

Standardmäßig unterstützt Azure ATP bis zu 100 Sensoren. Kontaktieren Sie den Azure ATP-Support, wenn Sie noch mehr Sensoren installieren möchten.

Der eigenständige Azure ATP-Sensor empfängt den Netzwerkdatenverkehr und die Windows-Ereignisse aus Ihrem Netzwerk und verarbeitet diese in den folgenden Hauptkomponenten:

|||
|-|-|
|Netzwerklistener|Der Netzwerklistener erfasst Netzwerkdatenverkehr und analysiert diesen. Diese Aufgabe sorgt für eine hohe CPU-Auslastung. Daher ist es besonders wichtig, beim Planen des Azure ATP-Sensors oder des eigenständigen Azure ATP-Sensors die [Azure ATP-Voraussetzungen](atp-prerequisites.md) zu überprüfen.|
|Ereignislistener|Der Ereignislistener erfasst die von einem SIEM-Server in Ihrem Netzwerk weitergeleiteten Windows-Ereignisse und analysiert diese.|
|Windows-Ereignisprotokollleser|Der Windows-Ereignisprotokollleser liest Windows-Ereignisse und analysiert diejenigen, die von den Domänencontrollern an das Windows-Ereignisprotokoll des eigenständigen Azure ATP-Sensors weitergeleitet werden.|
|Netzwerkaktivitätenübersetzer | Übersetzt analysierten Datenverkehr in eine logische Darstellung des von Azure ATP verwendeten Datenverkehrs (NetworkActivity).
|Entitäten-Resolver|Der Entitäten-Resolver löst die analysierten Daten (Netzwerkverkehr und Ereignisse) mit Active Directory auf, um Konten- und Identitätsdaten zu suchen. Anschließend werden diese den in den analysierten Daten gefundenen IP-Adressen zugeordnet. Der Entitätenresolver untersucht die Paketheader gründlich, um die Analyse der Authentifizierungspakete in Bezug auf Computernamen, Eigenschaften und Identitäten zu ermöglichen. Der Entitätenresolver kombiniert die analysierten Authentifizierungspakete mit den Daten im tatsächlichen Paket.|
|Entitätensender|Der Entitätensender sendet die analysierten und zugeordneten Daten an den Azure ATP-Clouddienst.|

## <a name="azure-atp-sensor-features"></a>Azure ATP-Sensorfeatures

Die folgenden Features funktionieren für den Azure ATP-Sensor und den eigenständigen Azure ATP-Sensor auf unterschiedliche Weise.

-   Der Azure ATP-Sensor liest lokal Ereignisse, ohne dass zusätzliche Hardware erworben und verwaltet oder die bei eigenständigen ATP-Sensoren erforderliche Ereignisweiterleitung konfiguriert werden muss. Der Azure ATP-Sensor unterstützt zudem die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die die Protokollinformationen für mehrere Erkennungen bereitstellt. Die Erkennung basierend auf der ETW umfasst sowohl verdächtige Replikationsanforderungen als auch die Heraufstufung verdächtiger Domänencontroller. Beide stellen potenzielle DcShadow-Angriffe dar und werden nicht von eigenständigen ATP-Sensoren unterstützt.  

-   **Kandidat für die Domänensynchronisierung**<br>
Der Kandidat für den Domänensynchronizer ist für die proaktive Synchronisierung aller Entitäten aus einer bestimmten Active Directory-Domäne verantwortlich (ähnlich dem Mechanismus, der von den Domänencontrollern selbst für die Replikation verwendet wird). Aus der Liste der Kandidaten wird nach dem Zufallsprinzip ein Sensor für den Domänensynchronizer ausgewählt. <br><br>
Wenn das Gateway für die Domänensynchronisierung mehr als 30 Minuten offline ist, wird stattdessen ein anderer Kandidaten ausgewählt. Wenn für eine bestimmte Domäne kein Domänensynchronizer verfügbar ist, kann Azure ATP Entitäten und deren Änderungen proaktiv synchronisieren. Azure ATP ruft jedoch neue Entitäten ab, sobald sie im überwachten Datenverkehr erkannt werden. 
<br>Wenn kein Gateway für die Domänensynchronisierung verfügbar ist und Sie nach einer Entität suchen, der kein Datenverkehr zugeordnet ist, werden keine Suchergebnisse angezeigt.<br><br>
Standardmäßig sind nur eigenständige Azure ATP-Sensoren als Synchronizerkandidaten festgelegt.<br><br>
Azure ATP-Sensoren sind nicht standardmäßig als Synchronizerkandidaten gekennzeichnet.


-   **Ressourceneinschränkungen**<br>
Der Azure ATP-Sensor enthält eine Überwachungskomponente, die die verfügbare Compute- und Arbeitsspeicherkapazität auf dem Domänencontroller auswertet, auf dem er ausgeführt wird. Der Überwachungsprozess wird alle 10 Sekunden ausgeführt und aktualisiert das CPU- und Arbeitsspeicherauslastungskontingent für den Azure ATP-Sensorprozess dynamisch, um sicherzustellen, dass der Domänencontroller zu jedem Zeitpunkt über mindestens 15 % freie Compute- und Arbeitsspeicherressourcen verfügt.<br><br>
Unabhängig davon, was auf dem Domänencontroller geschieht, gibt dieser Prozess immer Ressourcen frei, um sicherzustellen, dass die Kernfunktionalität des Domänencontrollers nicht beeinträchtigt wird.<br><br>
Wenn dem Azure ATP-Sensor dadurch nicht mehr genügend Ressourcen zur Verfügung stehen, wird nur ein Teil des Datenverkehrs überwacht, und die Überwachungswarnung „Dropped port mirrored network traffic.“ (Netzwerkdatenverkehr aus Portspiegelung gelöscht.) wird auf der Seite „Integrität“ angezeigt.

Die folgende Tabelle enthält ein Beispiel für einen Domänencontroller, der über genügend Rechenressourcen verfügt und ein größeres Kontingent als derzeit erforderlich bereitstellt und somit die Überwachung des gesamten Datenverkehrs ermöglicht:

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Azure ATP-Sensor („Microsoft.Tri.sensor.exe“)|Sonstiges (andere Prozesse) |Azure ATP-Sensorkontingent|Löscht der Sensor den Datenverkehr?|
|30%|20%|10%|45%|Nein|

Wenn Active Directory mehr Computeleistung erfordert, wird das vom Azure ATP-Sensor benötigte Kontingent reduziert. Im folgenden Beispiel benötigt der Azure ATP-Sensor mehr als das zugewiesene Kontingent und löscht einen Teil des Datenverkehrs (der Datenverkehr wird nur teilweise überwacht):

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Azure ATP-Sensor („Microsoft.Tri.sensor.exe“)|Sonstiges (andere Prozesse) |Azure ATP-Sensorkontingent|Löscht der Sensor den Datenverkehr?|
|60%|15%|10%|15%|Ja |


## <a name="your-network-components"></a>Ihre Netzwerkkomponenten
Stellen Sie sicher, dass die folgenden Komponenten eingerichtet sind, um mit Azure ATP arbeiten zu können.

### <a name="port-mirroring"></a>Portspiegelung
Wenn Sie eigenständige Azure ATP-Sensoren verwenden, muss die Portspiegelung für die überwachten Domänencontroller eingerichtet werden. Legen Sie den eigenständigen Azure ATP-Sensor über die physischen oder virtuellen Switches als Ziel fest. Eine andere Möglichkeit ist die Verwendung von Netzwerk-TAPs. Azure ATP funktioniert auch, wenn nur einige Domänencontroller überwacht werden, allerdings ist die Erkennung dann weniger effektiv.

In diesem Fall wird nur ein kleiner Prozentsatz dieses Datenverkehrs komprimiert und zur Analyse an den eigenständigen Azure ATP-Sensor gesendet, während durch die Portspiegelung sämtlicher Netzwerkverkehr der Domänencontroller an den Azure ATP-Clouddienst gesendet wird.

Die Domänencontroller und der eigenständige Azure ATP-Sensor können physisch oder virtuell vorhanden sein. Weitere Informationen finden Sie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md).


### <a name="events"></a>Ereignisse
Um die Abdeckung der Azure ATP-Erkennung von Pass-the-Hash-Angriffen, verdächtigen Authentifizierungsfehlern, Änderungen an sensiblen Gruppen, der Erstellung von verdächtigen Diensten und Angriffen mit Honeytoken-Aktivitätstypen zu verbessern, muss Azure ATP die Protokolle folgender Windows-Ereignisse analysieren: 4776, 4732, 4733, 4728, 4729, 4756, 4757 und 7045. Diese Ereignisse werden automatisch von Azure ATP-Sensoren mit den richtigen erweiterten Überwachungsrichtlinieneinstellungen gelesen. In Situationen, in denen eigenständige Azure ATP-Sensoren bereitgestellt werden, können Ereignisprotokolle auf zwei Arten weitergeleitet werden: durch die Konfiguration des eigenständigen Azure ATP-Sensors, sodass dieser auf SIEM-Ereignisse lauscht, oder durch die [Konfiguration der Windows-Ereignisweiterleitung](configure-event-forwarding.md). 

> [!NOTE]
> - Die Windows-Ereignisweiterleitung für eigenständige Sensoren unterstützt nicht die ETW (Event Tracing for Windows). Die Erkennung basierend auf der ETW umfasst sowohl verdächtige Replikationsanforderungen als auch die verdächtige Heraufstufung zu Domänencontrollern. Beide stellen potenzielle DcShadow-Angriffe dar.  

-   Konfigurieren des eigenständigen Azure ATP-Sensors zum Lauschen an SIEM-Ereignissen <br>Konfigurieren Sie SIEM zum Weiterleiten bestimmter Windows-Ereignisse an ATP. Azure ATP unterstützt eine Reihe von SIEM-Lieferanten. Weitere Informationen finden Sie unter [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md).

-   Konfigurieren der Windows-Ereignisweiterleitung<br>Eine andere Möglichkeit, wie Azure ATP Ihre Ereignisse abrufen kann, besteht darin, die Domänencontroller so zu konfigurieren, dass die Windows-Ereignisse 4776, 4732, 4733, 4728, 4729, 4756, 4757 und 7045 an den eigenständigen Azure ATP-Sensor weitergeleitet werden. Dies ist insbesondere dann nützlich, wenn Sie nicht über SIEM verfügen oder SIEM von ATP derzeit nicht unterstützt wird. Weitere Informationen zur Windows-Ereignisweiterleitung in ATP finden Sie unter [Configuring Windows event forwarding (Konfigurieren der Windows-Ereignisweiterleitung)](configure-event-forwarding.md). Dies gilt nicht für den Azure ATP-Sensor, sondern nur für physische eigenständige Azure ATP-Sensoren.


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/trisizingtool)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)

- - [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
