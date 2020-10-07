---
title: Architektur von Azure Advanced Threat Protection
description: Beschreibt die Architektur von Azure Advance Threat Analytics (ATP)
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/23/2019
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: aee16031c1682dc51b4c4da8fb3b123a8de93918
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913269"
---
# <a name="azure-atp-architecture"></a>Azure ATP-Architektur

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Azure ATP erfasst und analysiert Netzwerkdatenverkehr und nutzt Windows-Ereignisse direkt von Ihren Domänencontrollern, um Ihre Domänencontroller zu überwachen. Diese Daten werden dann auf Angriffe oder Bedrohungen geprüft. Azure ATP erhält durch Profilerstellung, deterministische Erkennungsmethoden, maschinelles Lernen und Verhaltensalgorithmen Informationen zu Ihrem Netzwerk, erkennt Anomalien und warnt Sie bei verdächtigen Aktivitäten.

Architektur von Azure Advanced Threat Protection:

![Topologiediagramm der Azure ATP-Architektur](media/atp-architecture-topology.png)

In diesem Abschnitt wird die Netzwerk- und Ereigniserfassung in Azure ATP erläutert. Des Weiteren wird auf die Funktionsweise der Hauptkomponenten eingegangen: das Azure ATP-Portal, der Azure ATP-Sensor und der Azure ATP-Clouddienst. 

Wenn Sie den Azure ATP-Sensor direkt auf Ihrem Domänencontroller installieren, greift er direkt vom Domänencontroller auf die erforderlichen Ereignisprotokolle zu. Nach Analyse dieser Protokolle und des Netzwerkdatenverkehrs durch den Sensor sendet Azure ATP nur diese analysierten Informationen (nicht alle Protokolle) an den Azure ATP-Clouddienst (nur ein Teil der Protokolle wird gesendet). 

## <a name="azure-atp-components"></a>Azure ATP-Komponenten
Azure ATP umfasst die folgenden Komponenten:

-    **Azure ATP-Portal** <br>
Über das Azure ATP-Portal können Sie Ihre Azure ATP-Instanz erstellen. Im Portal haben Sie zudem Zugriff auf die von Azure ATP-Sensoren erfassten Daten. Damit können Sie Bedrohungen in Ihrer Netzwerkumgebung überwachen, verwalten und untersuchen.  
-   **Azure ATP-Sensor**<br>
Azure ATP-Sensoren werden direkt auf Ihren Domänencontrollern installiert. Der Sensor überwacht den Datenverkehr des Domänencontrollers direkt, ohne dass ein dedizierter Server oder die Konfiguration der Portspiegelung erforderlich ist.

-   **Azure ATP-Clouddienst**<br>
Der Azure ATP-Clouddienst wird in der Azure-Infrastruktur ausgeführt und ist aktuell in den USA, Europa und China verfügbar. Der Azure ATP-Clouddienst ist mit dem Intelligent Security Graph von Microsoft verbunden. 

## <a name="azure-atp-portal"></a>Azure ATP-Portal 
Im Azure ATP-Portal können Sie die folgenden Aktionen durchführen:
- Erstellen einer Azure ATP-Instanz
- Integrieren in andere Microsoft-Sicherheitsdienste 
- Verwalten der Konfigurationseinstellungen des Azure ATP-Sensors 
- Anzeigen der Daten der Azure ATP-Sensoren
- Überwachen erkannter verdächtiger Aktivitäten und mutmaßlicher Angriffe anhand des Cyber Kill Chain-Modells
- **Optional:** Sie können außerdem festlegen, dass Sie E-Mails und Ereignisse erhalten, wenn Sicherheitswarnungen oder Integritätsprobleme erkannt werden.

> [!NOTE]
> - Wenn innerhalb von 60 Tagen kein Sensor in Ihrer Azure ATP-Instanz installiert wird, kann es sein, dass die Instanz gelöscht wird und Sie sie erneut erstellen müssen.

## <a name="azure-atp-sensor"></a>Azure ATP-Sensor
Dies sind die Hauptfunktionen des Azure ATP-Sensors:
- Erfassen und Überprüfen des Datenverkehrs von Domänencontrollern (lokaler Datenverkehr)
- Empfangen von Windows-Ereignissen direkt von Domänencontrollern 
- Empfangen von Informationen zur RADIUS-Kontoführung über den VPN-Anbieter
- Abrufen von Daten über Benutzer und Computer aus der Active Directory-Domäne
- Auflösen von Netzwerkentitäten (Benutzer, Gruppen und Computer)
- Übertragen von relevanten Daten in den Azure ATP-Clouddienst

 
## <a name="azure-atp-sensor-features"></a>Azure ATP-Sensorfeatures

Der Azure ATP-Sensor liest lokal Ereignisse, ohne dass zusätzliche Hardware erworben und verwaltet oder Konfigurationen vorgenommen werden müssen. Der Azure ATP-Sensor unterstützt zudem die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die die Protokollinformationen für mehrere Erkennungen bereitstellt. ETW-basierte Erkennungen beinhalten vermutete DCShadow-Angriffe, die mithilfe von Replikationsanforderungen für Domänencontroller und der Heraufstufung des Domänencontrollers versucht wurden.

### <a name="domain-synchronizer-process"></a>Domänensynchronisierungsprozess

Der Prozess für die Domänensynchronisierung ist für die proaktive Synchronisierung aller Entitäten aus einer bestimmten Active Directory-Domäne verantwortlich (ähnlich dem Mechanismus, der von den Domänencontrollern selbst für die Replikation verwendet wird). Ein Sensor wird automatisch nach dem Zufallsprinzip aus allen berechtigten Sensoren ausgewählt, die als Domänensynchronizer fungieren. 

Wenn das Gateway für den Domänensynchronizer mehr als 30 Minuten offline ist, wird stattdessen ein anderer Sensor automatisch ausgewählt. 
    
### <a name="resource-limitations"></a>Ressourcenbeschränkungen

Der Azure ATP-Sensor enthält eine Überwachungskomponente, die die verfügbare Compute- und Arbeitsspeicherkapazität auf dem Domänencontroller auswertet, auf dem er ausgeführt wird. Der Überwachungsprozess wird alle 10 Sekunden ausgeführt, und die CPU- und Arbeitsspeicherauslastung des Azure ATP-Sensorprozesses wird dynamisch angepasst. Der Überwachungsprozess stellt sicher, dass der Domänencontroller immer mindestens 15 % der verfügbaren Compute- und Arbeitsspeicherressourcen verwenden kann.

Unabhängig von laufenden Aktionen macht der Überwachungsprozess Ressourcen für den Domänencontroller verfügbar, um sicherzustellen, dass die Hauptfunktionen des Domänencontrollers immer erfüllt werden können.

Wenn dem Azure ATP-Sensor dadurch nicht mehr genügend Ressourcen zur Verfügung stehen, wird nur ein Teil des Datenverkehrs überwacht, und die Integritätswarnung „Netzwerkdatenverkehr aus Portspiegelung aufgegeben“ wird auf der Seite „Integrität“ im Azure ATP-Portal angezeigt.

### <a name="windows-events"></a>Windows-Ereignisse

Um die Reichweite der Azure ATP-Erkennung bezogen auf NTLM-Authentifizierungen, Änderungen an sensiblen Gruppen und der Erstellung von verdächtigen Diensten zu verbessern, muss Azure ATP die Protokolle folgender Windows-Ereignisse analysieren: 4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045 und 8004. Diese Ereignisse werden automatisch von Azure ATP-Sensoren mit den entsprechenden [erweiterten Überwachungsrichtlinieneinstellungen](configure-windows-event-collection.md) gelesen. Um [sicherzustellen, dass das Windows-Ereignis 8004 überwacht wird](configure-windows-event-collection.md#ntlm-authentication-using-windows-event-8004), wie es der Dienst erfordert, überprüfen Sie die [NTLM-Überwachungseinstellungen](/archive/blogs/askds/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7).

## <a name="next-steps"></a>Nächste Schritte

- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](prerequisites.md)
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](https://aka.ms/trisizingtool)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](capacity-planning.md)
- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)