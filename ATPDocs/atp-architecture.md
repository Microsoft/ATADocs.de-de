---
title: Azure Advanced Threat Protection-Architektur | Microsoft-Dokumentation
description: Beschreibt die Architektur von Azure Advance Threat Analytics (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6853a2a768fabde94c7aa613c9a6c0403f14e066
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783558"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="azure-atp-architecture"></a>Azure ATP-Architektur

Azure ATP erfasst und analysiert Netzwerkdatenverkehr und nutzt Windows-Ereignisse direkt von Ihren Domänencontrollern, um Ihre Domänencontroller zu überwachen. Diese Daten werden dann auf Angriffe oder Bedrohungen geprüft. Azure ATP erhält durch Profilerstellung, deterministische Erkennungsmethoden, maschinelles Lernen und Verhaltensalgorithmen Informationen zu Ihrem Netzwerk, erkennt Anomalien und warnt Sie bei verdächtigen Aktivitäten.

Architektur von Azure Advanced Threat Protection:

![Topologiediagramm der Azure ATP-Architektur](media/atp-architecture-topology.png)

In diesem Abschnitt wird die Netzwerk- und Ereignisserfassung in Azure ATP erläutert. Des Weiteren wird auf die Funktionsweise der Hauptkomponenten eingegangen: das Azure ATP-Portal, der Azure ATP-Sensor und der Azure ATP-Clouddienst. 

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
> - Wenn innerhalb von 60 Tagen kein Sensor in Ihrem Arbeitsbereich installiert wird, kann es sein, dass der Arbeitsbereich gelöscht wird und Sie ihn erneut erstellen müssen.

## <a name="azure-atp-sensor"></a>Azure ATP-Sensor
Dies sind die Hauptfunktionen des Azure ATP-Sensors:
- Erfassen und Überprüfen des Datenverkehrs von Domänencontrollern (lokaler Datenverkehr)
- Empfangen von Windows-Ereignissen direkt von Domänencontrollern 
- Empfangen von Informationen zur RADIUS-Kontoführung über den VPN-Anbieter
- Abrufen von Daten über Benutzer und Computer aus der Active Directory-Domäne
- Auflösen von Netzwerkentitäten (Benutzer, Gruppen und Computer)
- Übertragen von relevanten Daten in den Azure ATP-Clouddienst

 
## <a name="azure-atp-sensor-features"></a>Features des Azure ATP-Sensors
Der Azure ATP-Sensor liest lokal Ereignisse, ohne dass zusätzliche Hardware erworben und verwaltet oder Konfigurationen vorgenommen werden müssen. Der Azure ATP-Sensor unterstützt zudem die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die die Protokollinformationen für mehrere Erkennungen bereitstellt. Die Erkennung basierend auf der ETW umfasst sowohl verdächtige Replikationsanforderungen als auch die verdächtige Heraufstufung zu Domänencontrollern. Beide stellen potenzielle DCShadow-Angriffe dar.
- Kandidat für die Domänensynchronisierung

    Der Kandidat für den Domänensynchronizer ist für die proaktive Synchronisierung aller Entitäten aus einer bestimmten Active Directory-Domäne verantwortlich (ähnlich dem Mechanismus, der von den Domänencontrollern selbst für die Replikation verwendet wird). Aus der Liste der Kandidaten wird nach dem Zufallsprinzip ein Sensor für den Domänensynchronizer ausgewählt. 

    Wenn das Gateway für die Domänensynchronisierung mehr als 30 Minuten offline ist, wird stattdessen ein anderer Kandidaten ausgewählt. Wenn für eine bestimmte Domäne kein Domänensynchronizer verfügbar ist, synchronisiert Azure ATP Entitäten und deren Änderungen proaktiv. Azure ATP ruft jedoch neue Entitäten ab, sobald sie im überwachten Datenverkehr erkannt werden. 
    
    Wenn kein Gateway für die Domänensynchronisierung verfügbar ist und Sie nach einer Entität suchen, der kein Datenverkehr zugeordnet ist, werden keine Suchergebnisse angezeigt.

    Azure ATP-Sensoren werden nicht standardmäßig als mögliche Synchronizer angesehen. Führen Sie die unter [Installieren von Azure ATP](install-atp-step5.md#step-5-configure-the-azure-atp-sensor-settings) beschriebenen Schritte durch, um einen Azure ATP-Sensor manuell als Domänensynchronizer einzurichten.
- Ressourceneinschränkungen

    Der Azure ATP-Sensor enthält eine Überwachungskomponente, die die verfügbare Compute- und Arbeitsspeicherkapazität auf dem Domänencontroller auswertet, auf dem er ausgeführt wird. Der Überwachungsprozess wird alle 10 Sekunden ausgeführt, und die CPU- und Arbeitsspeicherauslastung des Azure ATP-Sensorprozesses wird dynamisch angepasst. Der Überwachungsprozess stellt sicher, dass der Domänencontroller immer mindestens 15 % der verfügbaren Compute- und Arbeitsspeicherressourcen verwenden kann.

    Unabhängig von laufenden Aktionen macht der Überwachungsprozess Ressourcen für den Domänencontroller verfügbar, um sicherzustellen, dass die Hauptfunktionen des Domänencontrollers immer erfüllt werden können.

    Wenn dem Azure ATP-Sensor dadurch nicht mehr genügend Ressourcen zur Verfügung stehen, wird nur ein Teil des Datenverkehrs überwacht, und die Überwachungswarnung „Dropped port mirrored network traffic.“ (Netzwerkdatenverkehr aus Portspiegelung aufgegeben.) wird auf der Seite „Health“ (Integrität) im Azure ATP-Portal angezeigt.

-  Windows-Ereignisse

    Um die Reichweite der Azure ATP-Erkennung von Pass-the-Hash-Angriffen, verdächtigen Authentifizierungsfehlern, Änderungen an sensiblen Gruppen, der Erstellung von verdächtigen Diensten und Angriffen mit Honeytoken-Aktivitätstypen zu verbessern, muss Azure ATP die Protokolle folgender Windows-Ereignisse analysieren: 4776,4732,4733,4728,4729,4756,4757 und 7045. Diese Ereignisse werden automatisch von Azure ATP-Sensoren mit den entsprechenden [erweiterten Überwachungsrichtlinieneinstellungen](atp-advanced-audit-policy.md) gelesen. 

## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/trisizingtool)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
