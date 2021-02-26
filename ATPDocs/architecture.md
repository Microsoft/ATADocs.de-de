---
title: Microsoft Defender for Identity-Architektur
description: In diesem Artikel wird die Architektur von Microsoft Defender for Identity beschrieben.
ms.date: 12/23/2020
ms.topic: overview
ms.openlocfilehash: 920c4fa99ebe2dad211fd7edae9ed928c1426510
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533884"
---
# <a name="microsoft-defender-for-identity-architecture"></a>Microsoft Defender for Identity-Architektur

[!INCLUDE [Product long](includes/product-long.md)] erfasst und analysiert Netzwerkdatenverkehr und nutzt Windows-Ereignisse direkt von Ihren Domänencontrollern, um Ihre Domänencontroller zu überwachen. Diese Daten werden dann auf Angriffe oder Bedrohungen geprüft. [!INCLUDE [Product short](includes/product-short.md)] erhält durch Profilerstellung, deterministische Erkennungsmethoden, maschinelles Lernen und Verhaltensalgorithmen Informationen zu Ihrem Netzwerk, erkennt Anomalien und warnt Sie bei verdächtigen Aktivitäten.

[!INCLUDE [Product short](includes/product-short.md)]-Architektur:

![Topologiediagramm der [!INCLUDE [Product short](includes/product-short.md)]-Architektur](media/architecture-topology.png)

In diesem Abschnitt wird die Netzwerk- und Ereigniserfassung in [!INCLUDE [Product short](includes/product-short.md)] erläutert. Des Weiteren wird auf die Funktionsweise der Hauptkomponenten eingegangen: das [!INCLUDE [Product short](includes/product-short.md)]-Portal, der [!INCLUDE [Product short](includes/product-short.md)]-Sensor und der [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst.

Wenn Sie den [!INCLUDE [Product short](includes/product-short.md)]-Sensor direkt auf Ihrem Domänencontroller oder Ihren AD FS-Servern installieren, greift er direkt von den Servern auf die erforderlichen Ereignisprotokolle zu. Nach Analyse dieser Protokolle und des Netzwerkdatenverkehrs durch den Sensor sendet [!INCLUDE [Product short](includes/product-short.md)] nur diese analysierten Informationen (nicht alle Protokolle) an den [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst (nur ein Teil der Protokolle wird gesendet).

## <a name="defender-for-identity-components"></a>Defender for Identity-Komponenten

[!INCLUDE [Product short](includes/product-short.md)] umfasst die folgenden Komponenten:

- **[!INCLUDE [Product short](includes/product-short.md)]-Portal**  
Über das [!INCLUDE [Product short](includes/product-short.md)]-Portal können Sie Ihre [!INCLUDE [Product short](includes/product-short.md)]-Instanz erstellen. Im Portal haben Sie zudem Zugriff auf die von [!INCLUDE [Product short](includes/product-short.md)]-Sensoren erfassten Daten. Damit können Sie Bedrohungen in Ihrer Netzwerkumgebung überwachen, verwalten und untersuchen.

- **[!INCLUDE [Product short](includes/product-short.md)]-Sensor**  
[!INCLUDE [Product short](includes/product-short.md)]-Sensoren können auf den folgenden Servern direkt installiert werden:
  - **Domänencontroller:** Der Sensor überwacht den Datenverkehr des Domänencontrollers direkt, ohne dass ein dedizierter Server oder die Konfiguration der Portspiegelung erforderlich ist.
  - **AD FS:** Der Sensor überwacht den Netzwerkdatenverkehr und die Authentifizierungsereignisse direkt.
- **[!INCLUDE [Product short](includes/product-short.md)]-Clouddienst**  
Der [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst wird in der Azure-Infrastruktur ausgeführt und ist aktuell in den USA, Europa und Asien verfügbar. Der [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst ist mit Microsoft Intelligent Security Graph verbunden.

## <a name="defender-for-identity-portal"></a>Portal für Defender for Identity

Verwenden Sie das [!INCLUDE [Product short](includes/product-short.md)]-Portal für folgende Zwecke:

- Erstellen Ihrer [!INCLUDE [Product short](includes/product-short.md)]-Instanz
- Integrieren in andere Microsoft-Sicherheitsdienste
- Verwalten von [!INCLUDE [Product short](includes/product-short.md)]-Sensorkonfigurationseinstellungen
- Anzeigen der Daten von [!INCLUDE [Product short](includes/product-short.md)]-Sensoren
- Überwachen erkannter verdächtiger Aktivitäten und mutmaßlicher Angriffe anhand des Cyber Kill Chain-Modells
- **Optional:** Sie können außerdem festlegen, dass Sie E-Mails und Ereignisse erhalten, wenn Sicherheitswarnungen oder Integritätsprobleme erkannt werden.

> [!NOTE]
> Wenn innerhalb von 60 Tagen kein Sensor in Ihrer [!INCLUDE [Product short](includes/product-short.md)]-Instanz installiert wird, kann es sein, dass die Instanz gelöscht wird und neu erstellt werden muss.

## <a name="defender-for-identity-sensor"></a>Defender for Identity-Sensor

Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor umfasst die folgenden Hauptfunktionen:

- Erfassen und Überprüfen des Datenverkehrs von Domänencontrollern (lokaler Datenverkehr)
- Empfangen von Windows-Ereignissen direkt von Domänencontrollern
- Empfangen von Informationen zur RADIUS-Kontoführung über den VPN-Anbieter
- Abrufen von Daten über Benutzer und Computer aus der Active Directory-Domäne
- Auflösen von Netzwerkentitäten (Benutzer, Gruppen und Computer)
- Übertragen relevanter Daten an den [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst

## <a name="defender-for-identity-sensor-features"></a>Defender for Identity-Sensorfeatures

Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor liest lokal Ereignisse, ohne dass zusätzliche Hardware erworben und verwaltet oder Konfigurationen vorgenommen werden müssen. Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor unterstützt zudem die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die die Protokollinformationen für mehrere Erkennungen bereitstellt. ETW-basierte Erkennungen beinhalten vermutete DCShadow-Angriffe, die mithilfe von Replikationsanforderungen für Domänencontroller und der Heraufstufung des Domänencontrollers versucht wurden.

### <a name="domain-synchronizer-process"></a>Domänensynchronisierungsprozess

Der Prozess für die Domänensynchronisierung ist für die proaktive Synchronisierung aller Entitäten aus einer bestimmten Active Directory-Domäne verantwortlich (ähnlich dem Mechanismus, der von den Domänencontrollern selbst für die Replikation verwendet wird). Ein Sensor wird automatisch nach dem Zufallsprinzip aus allen berechtigten Sensoren ausgewählt, die als Domänensynchronizer fungieren.

Wenn das Gateway für den Domänensynchronizer mehr als 30 Minuten offline ist, wird stattdessen ein anderer Sensor automatisch ausgewählt.

### <a name="resource-limitations"></a>Ressourcenbeschränkungen

Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor enthält eine Überwachungskomponente, die die verfügbare Compute- und Arbeitsspeicherkapazität auf dem Domänencontroller auswertet, auf dem er ausgeführt wird. Der Überwachungsprozess wird alle 10 Sekunden ausgeführt, und die CPU- und Arbeitsspeicherauslastung des [!INCLUDE [Product short](includes/product-short.md)]-Sensorprozesses wird dynamisch angepasst. Der Überwachungsprozess stellt sicher, dass der Domänencontroller immer mindestens 15 % der verfügbaren Compute- und Arbeitsspeicherressourcen verwenden kann.

Unabhängig von laufenden Aktionen macht der Überwachungsprozess Ressourcen für den Domänencontroller verfügbar, um sicherzustellen, dass die Hauptfunktionen des Domänencontrollers immer erfüllt werden können.

Wenn dem [!INCLUDE [Product short](includes/product-short.md)]-Sensor dadurch nicht mehr genügend Ressourcen zur Verfügung stehen, wird nur ein Teil des Datenverkehrs überwacht, und die Integritätswarnung „Dropped port mirrored network traffic“ (Netzwerkdatenverkehr aus Portspiegelung gelöscht) wird auf der Seite „Integrität“ im [!INCLUDE [Product short](includes/product-short.md)]-Portal angezeigt.

### <a name="windows-events"></a>Windows-Ereignisse

[!INCLUDE [Product short](includes/product-short.md)] muss die Protokolle der folgenden Windows-Ereignisse analysieren, um die Reichweite der [!INCLUDE [Product short](includes/product-short.md)]-Erkennung bezüglich NTLM-Authentifizierungen, Änderungen an vertraulichen Gruppen und der Erstellung verdächtiger Dienste zu verbessern: 4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045 und 8004. Diese Ereignisse werden automatisch von [!INCLUDE [Product short](includes/product-short.md)]-Sensoren mit den entsprechenden [erweiterten Überwachungsrichtlinieneinstellungen](configure-windows-event-collection.md) gelesen. Um [sicherzustellen, dass das Windows-Ereignis 8004 überwacht wird](configure-windows-event-collection.md#ntlm-authentication-using-windows-event-8004), wie es der Dienst erfordert, überprüfen Sie die [NTLM-Überwachungseinstellungen](/archive/blogs/askds/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7).

## <a name="next-steps"></a>Nächste Schritte

- [Voraussetzungen für [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [[!INCLUDE [Product short](includes/product-short.md)]-Tool zur Größenanpassung](https://aka.ms/trisizingtool)
- [Kapazitätsplanung für [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
