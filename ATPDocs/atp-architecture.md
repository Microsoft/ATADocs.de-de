---
title: Azure Advanced Threat Protection-Architektur | Microsoft-Dokumentation
description: Beschreibt die Architektur von Azure Advance Threat Analytics (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/27/2019
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6988b41b64dc3d8afef5f7af614f78b41501e2af
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085315"
---
# <a name="azure-atp-architecture"></a>Azure ATP-Architektur

Azure ATP erfasst und analysiert Netzwerkdatenverkehr und nutzt Windows-Ereignisse direkt von Ihren Domänencontrollern, um Ihre Domänencontroller zu überwachen. Diese Daten werden dann auf Angriffe oder Bedrohungen geprüft. Azure ATP erhält durch Profilerstellung, deterministische Erkennungsmethoden, maschinelles Lernen und Verhaltensalgorithmen Informationen zu Ihrem Netzwerk, erkennt Anomalien und warnt Sie bei verdächtigen Aktivitäten.

Architektur von Azure Advanced Threat Protection:

![Topologiediagramm der Azure ATP-Architektur](media/atp-architecture-topology.png)

In diesem Abschnitt wird die Netzwerk- und Ereigniserfassung in Azure ATP erläutert. Des Weiteren wird auf die Funktionsweise der Hauptkomponenten eingegangen: das Azure ATP-Portal, der Azure ATP-Sensor und der Azure ATP-Clouddienst. 

Wenn Sie den Azure ATP-Sensor direkt auf Ihrem Domänencontroller installieren, greift er direkt vom Domänencontroller auf die erforderlichen Ereignisprotokolle zu. Nach Analyse dieser Protokolle und des Netzwerkdatenverkehrs durch den Sensor sendet Azure ATP nur diese analysierten Informationen (nicht alle Protokolle) an den Azure ATP-Clouddienst (nur ein Teil der Protokolle wird gesendet). 

## <a name="azure-atp-components"></a>Azure ATP-Komponenten
Azure ATP umfasst die folgenden Komponenten:

-   **Azure ATP-Portal** <br>
Über das Azure ATP-Portal können Sie Ihre Azure ATP-Instanz erstellen. Im Portal haben Sie zudem Zugriff auf die von Azure ATP-Sensoren erfassten Daten. Damit können Sie Bedrohungen in Ihrer Netzwerkumgebung überwachen, verwalten und untersuchen.  
-   **Azure ATP-Sensor**<br>
Azure ATP-Sensoren werden direkt auf Ihren Domänencontrollern installiert. Der Sensor überwacht den Datenverkehr des Domänencontrollers direkt, ohne dass ein dedizierter Server oder die Konfiguration der Portspiegelung erforderlich ist.

-   **Azure ATP-Clouddienst**<br>
Der Azure ATP-Clouddienst wird in der Azure-Infrastruktur ausgeführt und ist aktuell in den USA, Europa und China verfügbar. Der Azure ATP-Clouddienst ist mit Microsoft Intelligent Security Graph verbunden. 

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

 
## <a name="azure-atp-sensor-features"></a>Features des Azure ATP-Sensors
Der Azure ATP-Sensor liest lokal Ereignisse, ohne dass zusätzliche Hardware erworben und verwaltet oder Konfigurationen vorgenommen werden müssen. Der Azure ATP-Sensor unterstützt zudem die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die die Protokollinformationen für mehrere Erkennungen bereitstellt. ETW-basierte Erkennungen beinhalten vermutete DCShadow-Angriffe, die mit Hilfe von Replikationsanforderungen für Domänencontroller und Heraufstufung des Domänencontrollers versucht wurden.

### <a name="domain-synchronizer-candidate"></a>Kandidat für die Domänensynchronisierung

    The domain synchronizer candidate is responsible for synchronizing all entities from a specific Active Directory domain proactively (similar to the mechanism used by the domain controllers themselves for replication). One sensor is chosen randomly, from the list of candidates, to serve as the domain synchronizer. 

    If the synchronizer is offline for more than 30 minutes, another candidate is chosen instead. If there is no domain synchronizer available for a specific domain, Azure ATP proactively synchronizes entities and their changes, however Azure ATP retrieves new entities as they are detected in the monitored traffic. 
    
    If there is no domain synchronizer available, and you search for an entity that did not have any traffic related to it, no search results are displayed.

    By default, Azure ATP sensors are not synchronizer candidates. To manually set an Azure ATP sensor as a domain synchronizer candidate, follow the steps in the [Azure ATP installation workflow](install-atp-step5.md#configure-azure-atp-sensor-settings).

### <a name="resource-limitations"></a>Ressourceneinschränkungen

    The Azure ATP sensor includes a monitoring component that evaluates the available compute and memory capacity on the domain controller on which it is running. The monitoring process runs every 10 seconds and dynamically updates the CPU and memory utilization quota on the Azure ATP sensor process. The monitoring process makes sure the domain controller always has at least 15% of free compute and memory resources available.

    No matter what occurs on the domain controller, the monitoring process continually frees up resources to make sure the domain controller's core functionality is never affected.

    If the monitoring process causes the Azure ATP sensor to run out of resources, only partial traffic is monitored and the monitoring alert "Dropped port mirrored network traffic" appears in the Azure ATP portal Health page.

### <a name="windows-events"></a>Windows-Ereignisse

    To enhance Azure ATP detection coverage of suspected identity theft (pass-the-hash), suspicious authentication failures,modifications to sensitive groups, creation of suspicious services, and Honeytoken activity types of attack, Azure ATP needs to analyze the logs of the following Windows events: 4776,4732,4733,4728,4729,4756,4757, and 7045. These events are read automatically by Azure ATP sensors with correct [advanced audit policy settings](atp-advanced-audit-policy.md). 

## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/trisizingtool)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
