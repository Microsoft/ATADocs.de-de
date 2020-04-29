---
title: Advanced Threat Analytics-Architektur
description: Beschreibt die Architektur von Microsoft Advance Threat Analytics (ATA)
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/08/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b47f32a99d7257daed2f942346ac87dca4fccdcb
ms.sourcegitcommit: 8c0222dc8333b5aa47430c5daee9bc7f1d82df31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81524751"
---
# <a name="ata-architecture"></a>ATA-Architektur

*Gilt für: Advanced Threat Analytics Version 1.9*

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
-   **Ausschließlich ATA-Lightweight-Gateways**<br>
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
|Erkennungsmodule|Die Detektoren verwenden Machine Learning-Algorithmen und deterministische Regeln, um verdächtige Aktivitäten und ungewöhnliches Benutzerverhalten im Netzwerk zu suchen.|
|ATA-Konsole|Die ATA-Konsole wird zum Konfigurieren von ATA und zum Überwachen verdächtiger Aktivitäten verwendet, die ATA in Ihrem Netzwerk erkennt. Die ATA-Konsole ist nicht vom ATA Center-Dienst abhängig und wird selbst dann ausgeführt, wenn der Dienst beendet wurde, solange die Kommunikation mit der Datenbank möglich ist.|

Berücksichtigen Sie Folgendes bei der Entscheidung, wie viele ATA Center Sie in Ihrem Netzwerk bereitstellen möchten:

-   Ein ATA Center kann eine einzelne Active Directory-Gesamtstruktur überwachen. Wenn Sie über mehrere Active Directory-Gesamtstrukturen verfügen, benötigen Sie mindestens ein ATA Center pro Active Directory-Gesamtstruktur.

-    In umfangreichen Active Directory-Bereitstellungen ist ein einzelnes ATA Center möglicherweise nicht in der Lage, den gesamten Datenverkehr von allen Domänencontrollern zu verarbeiten. In diesem Fall werden mehrere ATA Center benötigt. Die Anzahl der ATA Center sollte durch die [ATA-Kapazitätsplanung](ata-capacity-planning.md) vorgegeben werden.

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
Wenn das Gateway für die Domänensynchronisierung mehr als 30 Minuten offline ist, wird stattdessen ein anderer Kandidaten ausgewählt. Wenn für eine bestimmte Domäne kein Kandidat für den domänensynchronizer verfügbar ist, synchronisiert ATA proaktiv Entitäten und Ihre Änderungen, ATA ruft jedoch reaktiv neue Entitäten ab, sobald Sie im überwachten Datenverkehr erkannt werden. 
<br>Wenn kein Domänen Synchronisierungs Modul verfügbar ist, werden bei der Suche nach einer Entität ohne zugeordneten Datenverkehr keine Ergebnisse angezeigt.<br><br>
Standardmäßig handelt es sich bei allen ATA-Gateways um Domänen Synchronisierungs Kandidaten.<br><br>
Da alle ATA-Lightweight-Gateways eher in Filialen und auf kleinen Domänencontrollern bereitgestellt werden, sind sie standardmäßig keine Kandidaten für die Domänensynchronisierung. <br><br>In einer Umgebung mit nur Lightweight-Gateways empfiehlt es sich, zwei der Gateways als Synchronisierungs Kandidaten zuzuweisen, wobei ein Lightweight-Gateway der standardmäßige Synchronisierungs Kandidat ist, und einer für den Fall, dass der Standardwert für mehr als 30 Minuten offline ist. 


-   **Ressourcenbeschränkungen**<br>
Das ATA-Lightweight-Gateway enthält eine Überwachungskomponente, die die verfügbare Compute- und Arbeitsspeicherkapazität auf dem Domänencontroller auswertet, auf dem es ausgeführt wird. Der Überwachungsprozess wird alle 10 Sekunden ausgeführt und aktualisiert das CPU- und Arbeitsspeicher-Auslastungskontingent für den ATA-Lightweight-Gateway-Prozess dynamisch, um sicherzustellen, dass der Domänencontroller zu jedem Zeitpunkt über mindestens 15 % freie Rechen- und Arbeitsspeicherressourcen verfügt.<br><br>
Unabhängig davon, was auf dem Domänencontroller geschieht, gibt dieser Prozess immer Ressourcen frei, um sicherzustellen, dass die Kernfunktionalität des Domänencontrollers nicht beeinträchtigt wird.<br><br>
Wenn dies dazu führt, dass das ATA-Lightweight-Gateway nicht mehr über genügend Ressourcen verfügt, wird nur teilweiser Datenverkehr überwacht

Die folgende Tabelle enthält ein Beispiel für einen Domänencontroller, der über genügend Rechenressourcen verfügt und ein größeres Kontingent als derzeit erforderlich bereitstellt und somit die Überwachung des gesamten Datenverkehrs ermöglicht:

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA-Lightweight-Gateway (Microsoft.Tri.Gateway.exe)|Sonstiges (andere Prozesse) |ATA-Lightweight-Gateway-Kontingent|Nimmt Gateway Löschungen vor|
|30 %|20%|10 %|45 %|Nein|

Wenn Active Directory mehr Rechenkapazität erfordert, wird das vom ATA-Lightweight-Gateway benötigte Kontingent reduziert. Im folgenden Beispiel benötigt das ATA-Lightweight-Gateway mehr als das zugewiesene Kontingent und löscht einen Teil des Datenverkehrs (der Datenverkehr wird nur teilweise überwacht):

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA-Lightweight-Gateway (Microsoft.Tri.Gateway.exe)|Sonstiges (andere Prozesse) |ATA-Lightweight-Gateway-Kontingent|Nimmt Gateway Löschungen vor|
|60%|15 %|10 %|15 %|Ja|


## <a name="your-network-components"></a>Ihre Netzwerkkomponenten
Um mit ATA zu arbeiten, stellen Sie sicher, dass die folgenden Komponenten eingerichtet sind.

### <a name="port-mirroring"></a>Portspiegelung
Wenn Sie ATA-Gateways verwenden, müssen Sie für die Domänencontroller, die überwacht werden, die Portspiegelung einrichten und das ATA-Gateway über die physischen oder virtuellen Schalter als Ziel festlegen. Eine andere Möglichkeit ist die Verwendung von Netzwerk-TAPs. ATA funktioniert auch, wenn nur einige, aber nicht alle Domänencontroller überwacht werden, allerdings ist die Erkennung dann weniger effektiv.

In diesem Fall wird nur ein kleiner Prozentsatz dieses Datenverkehrs komprimiert und zur Analyse an ATA Center gesendet, während durch die Portspiegelung sämtlicher Netzwerkverkehr der Domänencontroller an das ATA-Gateway gesendet wird.

Die Domänencontroller und die ATA-Gateways können physisch oder virtuell sein. Weitere Informationen finden Sie unter [Portspiegelung](configure-port-mirroring.md).


### <a name="events"></a>Events
Um die ATA-Erfassung von Pass-the-Hash, Brute Force, die Modifizierung von sensiblen Gruppen und Honey Token zu verbessern, benötigt ATA die folgenden Windows-Ereignisse: 4776, 4732, 4733, 4728, 4729, 4756 und 4757. Diese können entweder automatisch vom ATA-Lightweight-Gateway gelesen werden, oder für den Fall, dass das ATA-Lightweight-Gateway nicht bereitgestellt wird, kann es auf zwei Arten an das ATA-Gateway weitergeleitet werden: durch Konfigurieren des ATA-Gateways zum lauschen auf Siem-Ereignisse oder durch [Konfigurieren der Windows-Ereignis Weiterleitung](configure-event-collection.md).

-   Konfigurieren des ATA-Gateways zum Überwachen von SIEM-Ereignissen <br>Konfigurieren Sie SIEM zum Weiterleiten bestimmter Windows-Ereignisse an ATA. ATA unterstützt eine Reihe von SIEM-Anbietern. Weitere Informationen finden Sie unter [Konfigurieren der Ereignissammlung](configure-event-collection.md).

-   Konfigurieren der Windows-Ereignisweiterleitung<br>Eine andere Möglichkeit, wie ATA Ihre Ereignisse erhalten kann, besteht darin, die Domänencontroller so zu konfigurieren, dass die Windows-Ereignisse 4776, 4732, 4733, 4728, 4729, 4756 und 4757 an das ATA-Gateway weitergeleitet werden. Dies ist insbesondere dann nützlich, wenn Sie nicht über SIEM verfügen oder SIEM von ATA derzeit nicht unterstützt wird. Informationen darüber, wie Sie die Konfiguration der Windows-Ereignisweiterleitung in ATA abschließen, finden Sie unter [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md). Dies gilt nur für physische ATA-Gateways und nicht für das ATA-Lightweight-Gateway.

## <a name="related-videos"></a>Verwandte Videos
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Weitere Informationen
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [Tool zur Bemessung von ATA-Gateways](https://aka.ms/atasizingtool)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

