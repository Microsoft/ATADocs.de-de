---
# required metadata

title: ATA-Architektur | Microsoft Advanced Threat Analytics
description: Beschreibt die Architektur von Microsoft Advance Threat Analytics (ATA)
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA-Architektur
Dieses Diagramm veranschaulicht die Architektur von Advanced Threat Analytics:

![Topologiediagramm der ATA-Architektur](media/ATA-architecture-topology.jpg)

ATA besteht aus zwei Hauptkomponenten – dem ATA-Gateway und ATA Center.

Diese Komponenten sind mit Ihrem vorhandenen Netzwerk verbunden, indem sie den Netzwerkdatenverkehr zu und von Ihren Domänencontrollern spiegeln, Windows-Ereignisse (die direkt von den Domänencontrollern oder von einem SIEM-Server weitergeleitet werden) überprüfen und die Daten auf Angriffe und Bedrohungen analysieren.

In diesem Abschnitt wird der Ablauf der Netzwerk- und Ereigniserfassung beschrieben. Außerdem werden die Hauptkomponenten (ATA-Gateway und ATA Center) und deren Funktionen detailliert erläutert.

![Diagramm für ATA-Datenverkehrsfluss](media/ATA-traffic-flow.jpg)

## ATA-Komponenten
ATA umfasst Folgendes:

-   Einen oder mehrere ATA-Gateways

-   Ein ATA Center

## ATA-Gateway
Das **ATA-Gateway** führt die folgenden Funktionen aus:

-   Erfassen und Überprüfen des Domänencontroller-Netzwerkverkehrs über Portspiegelung

-   Empfangen von Windows-Ereignissen von SIEM- oder Syslog-Servern oder von Domänencontrollern mithilfe der Windows-Ereignisweiterleitung

-   Abrufen von Daten über Benutzer und Computer aus der Active Directory-Domäne

-   Auflösen von Netzwerkentitäten (Benutzer, Gruppen und Computer)

-   Übertragen relevanter Daten an ATA Center

-   Überwachen mehrerer Domänencontroller über ein einzelnes ATA-Gateway

Das ATA-Gateway empfängt den gespiegelten Netzwerkverkehr und die Windows-Ereignisse aus Ihrem Netzwerk und verarbeitet diese in den folgenden Hauptkomponenten:

|||
|-|-|
|Netzwerklistener|Der Netzwerklistener ist dafür verantwortlich, den Netzwerkdatenverkehr zu erfassen und den Datenverkehr zu analysieren. Diese Aufgabe sorgt für eine hohe CPU-Auslastung. Daher ist es besonders wichtig, beim Planen des ATA-Gateways die [ATA-Voraussetzungen](/advanced-threat-analytics/PlanDesign/ata-prerequisites) zu überprüfen.|
|Ereignislistener|Der Ereignislistener ist dafür verantwortlich, die von einem SIEM-Server in Ihrem Netzwerk weitergeleiteten Windows-Ereignisse zu erfassen und zu analysieren.|
|Windows-Ereignisprotokollleser|Der Windows-Ereignisprotokollleser ist dafür verantwortlich, die Windows-Ereignisse zu lesen und zu analysieren, die von den Domänencontrollern an das Windows-Ereignisprotokoll des ATA-Gateway weitergeleitet werden.|
|Netzwerkaktivitätenübersetzer | Übersetzt den analysierten Datenverkehr in die logische ATA-Darstellung des Datenverkehrs (NetworkActivity).
|Entitäten-Resolver|Der Entitäten-Resolver löst die analysierten Daten (Netzwerkverkehr und Ereignisse) mit Active Directory auf, um Konten- und Identitätsdaten zu suchen und diese den in den analysierten Daten gefundenen IP-Adressen zuzuordnen.  Darüber hinaus untersucht der Entitäten-Resolver die Paketheader gründlich, ermöglicht das Analysieren der Authentifizierungspakete für Computernamen, Eigenschaften und Identitäten und kombiniert diese mit den Daten im tatsächlichen Paket.|
|Entitätensender|Der Entitätensender ist dafür verantwortlich, die analysierten und zugeordneten Daten an ATA Center zu senden.|
Berücksichtigen Sie Folgendes bei der Entscheidung, wie viele ATA-Gateways Sie in Ihrem Netzwerk bereitstellen möchten:

-   Active Directory-Gesamtstrukturen und -Domänen

    ATA-Gateways können den Datenverkehr aus mehreren Domänen über eine einzelne Active Directory-Gesamtstruktur überwachen.   Die Überwachung mehrerer Active Directory-Gesamtstrukturen erfordert separate ATA-Bereitstellungen. ATA-Gateways sollten nicht für die Überwachung des Netzwerkdatenverkehrs von Domänencontrollern in unterschiedlichen Gesamtstrukturen konfiguriert werden.

-   Portspiegelung

    Im Hinblick auf die Portspiegelung müssen Sie wahrscheinlich mindestens ein ATA-Gateway pro Rechenzentrum/geografischer Region bereitstellen.

-   Kapazität

    Jedes ATA-Gateway kann eine bestimmte Menge an Datenverkehr pro Sekunde analysieren und senden. Wenn die überwachten Domänencontroller mehr Datenverkehr senden und empfangen, als vom ATA-Gateway verarbeitet werden kann, müssen Sie zusätzliche ATA-Gateways gemäß Ihrem Datenverkehrsvolumen hinzufügen. Weitere Informationen finden Sie unter [ATA-Kapazitätsplanung](/advanced-threat-analytics/PlanDesign/ata-capacity-planning).

## ATA Center
Das **ATA-Center** führt die folgenden Funktionen aus:

-   Verwalten der ATA-Gateway-Konfigurationseinstellungen

-   Empfangen von Daten von ATA-Gateways

-   Erkennen verdächtiger Aktivitäten

-   Ausführen verschiedener Machine Learning-Verhaltensmodule

-   Ausführen der ATA-Konsole

-   Optional: ATA Center kann zum Senden von E-Mail-Nachrichten und Ereignissen konfiguriert werden, wenn eine verdächtige Aktivität erkannt wird.

ATA Center empfängt den analysierten Datenverkehr vom ATA-Gateway und führt die Profilerstellung, die deterministische Erkennung sowie Machine Learning- und Verhaltensalgorithmen aus, um Informationen über Ihr Netzwerk zu sammeln, damit die Erkennung von Anomalien ermöglicht wird und Sie bei verdächtigen Aktivitäten gewarnt werden können.

|||
|-|-|
|Entitätenempfänger|Empfängt Batches von Entitäten von allen ATA-Gateways.|
|Netzwerkaktivitätenverarbeitung|Verarbeitet alle Netzwerkaktivitäten innerhalb der einzelnen empfangenen Batches. Beispiel: Zuordnung unterschiedlicher Kerberos-Schritte, die von potenziell verschiedenen Computern ausgeführt werden|
|Entityprofilerstellung|Erstellt Profile für alle eindeutigen Entitäten gemäß dem Datenverkehr und den Ereignissen. Hier aktualisiert zum Beispiel ATA die Liste der angemeldeten Computer für jedes Benutzerprofil.|
|ATA Center-Datenbankclient |Verwaltet das Schreiben der Netzwerkaktivitäten und Ereignisse in die Datenbank. |
|Datenbank|ATA verwendet MongoDB zum Speichern aller Daten im System:<br /><br />-   Netzwerkaktivitäten<br />-   Ereignisse<br />-   Eindeutige Entitäten<br />-   Verdächtige Aktivitäten<br />-   ATA-Konfiguration|
|Erkennungsmodule|Die Erkennungsmodule verwenden Machine Learning-Algorithmen und deterministische Regeln, um verdächtige Aktivitäten und ungewöhnliches Benutzerverhalten im Netzwerk zu suchen.|
|ATA-Konsole|Die ATA-Konsole wird zum Konfigurieren von ATA und zum Überwachen verdächtiger Aktivitäten verwendet, die ATA in Ihrem Netzwerk erkennt. Die ATA-Konsole ist nicht vom ATA Center-Dienst abhängig und wird selbst dann ausgeführt, wenn der Dienst beendet wurde, solange die Kommunikation mit der Datenbank möglich ist.|
Berücksichtigen Sie Folgendes bei der Entscheidung, wie viele ATA Center Sie in Ihrem Netzwerk bereitstellen möchten:

-   Ein ATA Center kann eine einzelne Active Directory-Gesamtstruktur überwachen. Wenn Sie über mehrere Active Directory-Gesamtstrukturen verfügen, benötigen Sie mindestens ein ATA Center pro Active Directory-Gesamtstruktur.

    In umfangreichen Active Directory-Bereitstellungen ist ein einzelnes ATA Center möglicherweise nicht in der Lage, den gesamten Datenverkehr von allen Domänencontrollern zu verarbeiten. In diesem Fall sind mehrere ATA Center erforderlich, und die ATA-Erkennung ist weniger effektiv. Die Anzahl der ATA Center sollte durch die [ATA-Kapazitätsplanung](/advanced-threat-analytics/PlanDesign/ata-capacity-planning) vorgegeben werden.

## Ihre Netzwerkkomponenten
Für die Verwendung von ATA sind nur geringfügige Änderungen an Ihrem vorhandenen Netzwerk nötig. Folgendes müssen Sie jedoch sicherstellen.

### Portspiegelung
Damit ATA funktioniert, müssen Sie die Portspiegelung für alle Domänencontroller in der überwachten Active Directory-Gesamtstruktur aktivieren. ATA funktioniert auch, wenn die Portspiegelung nur für einige, aber nicht für alle Domänencontroller aktiviert ist, allerdings ist die Erkennung dann weniger effektiv.

Richten Sie die Portspiegelung über Ihre Domänencontroller für das ATA-Gateway ein. Zwar wird damit sämtlicher Netzwerkverkehr der Domänencontroller an das ATA-Gateway gesendet, doch der Prozentsatz dieses Datenverkehrs, der dann komprimiert zur Analyse an ATA Center gesendet wird, ist sehr klein.

Die Domänencontroller und die ATA-Gateways können physisch oder virtuell sein. Weitere Informationen finden Sie unter [Portspiegelung](/advanced-threat-analytics/PlanDesign/configure-port-mirroring).

### Ereignisse
Zur Erhöhung der ATA-Erkennung von Pass-the-Hash benötigt ATA die Windows-Ereignisprotokoll-ID 4776. Diese kann auf zwei Arten an das ATA-Gateway weitergeleitet werden: durch die Konfiguration des ATA-Gateways zum Überwachen von SIEM-Ereignissen oder durch die Verwendung der Windows-Ereignisweiterleitung.

-   Konfigurieren des ATA-Gateways zum Überwachen von SIEM-Ereignissen

    Konfigurieren Sie SIEM zum Weiterleiten bestimmter Windows-Ereignisse an ATA. ATA unterstützt eine Reihe von SIEM-Anbietern. Weitere Informationen finden Sie unter [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/PlanDesign/configure-event-collection).

-   Konfigurieren der Windows-Ereignisweiterleitung

    Eine andere Möglichkeit, wie ATA Ihre Ereignisse erhalten kann, besteht darin, die Domänencontroller so zu konfigurieren, dass das Windows-Ereignis 4776 an das ATA-Gateway weitergeleitet wird. Dies ist insbesondere dann nützlich, wenn Sie nicht über SIEM verfügen oder SIEM von ATA derzeit nicht unterstützt wird. Weitere Informationen zur Windows-Ereignisweiterleitung in ATA finden Sie unter [Konfigurieren der Windows-Ereignisweiterleitung](/advanced-threat-analytics/PlanDesign/configure-event-collection#ATA_event_WEF).

## Siehe auch
- [ATA-Voraussetzungen](/advanced-threat-analytics/PlanDesign/ata-prerequisites)
- [ATA-Kapazitätsplanung](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/PlanDesign/configure-event-collection)
- [Konfigurieren der Windows-Ereignisweiterleitung](/advanced-threat-analytics/PlanDesign/configure-event-collection#ATA_event_WEF)
- [Unterstützung finden Sie in unserem Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


