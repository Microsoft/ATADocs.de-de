---
title: Azure Advanced Threat Protection-Unterstützung für mehrere Gesamtstrukturen | Microsoft-Dokumentation
description: Unterstützung für mehrere Active Directory-Gesamtstrukturen in Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/28/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a742cb7c64211d47a53a15b3906283ce523a938c
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2019
ms.locfileid: "54458987"
---
# <a name="azure-advanced-threat-protection-multi-forest-support"></a>Azure Advanced Threat Protection-Unterstützung für mehrere Gesamtstrukturen


## <a name="multi-forest-support-set-up"></a>Einrichten der Unterstützung für mehrere Gesamtstrukturen 

Azure ATP kann Organisationen mit mehreren Gesamtstrukturen unterstützen, wodurch diese die Möglichkeit erhalten, Aktivitäten und Benutzerprofile in allen Gesamtstrukturen ganz einfach über eine zentrale Konsole zu überwachen. 

Unternehmensorganisationen können in der Regel über mehrere Active Directory-Gesamtstrukturen verfügen, die oft für verschiedene Zwecke genutzt werden. Dies schließt auch ältere, aus Unternehmenszusammenschlüssen und -übernahmen stammende Infrastrukturen, die geografische Verteilung und Sicherheitsbegrenzungen (Red Forests) ein. Sie können mehrere Gesamtstrukturen mit Azure ATP schützen, um die Überwachung und Untersuchungen über eine zentrale Konsole auszuführen.

Die Möglichkeit, mehrere Active Directory-Gesamtstrukturen zu unterstützen, bietet folgende Vorteile:
-   Sie können Aktivitäten, die von Benutzern in mehreren Gesamtstrukturen ausgeführt werden, in einer zentralen Konsole im Blick behalten und untersuchen. 
-   Durch erweiterte Active Directory-Integration und -Kontoauflösung lassen sich falsch positive Ergebnisse besser erkennen und reduzieren. 
-   Sie ermöglicht eine bessere Kontrolle und eine einfachere Bereitstellung. Die Überwachung von Warnungen und Berichterstellung für die organisationsübergreifende Abdeckung wurde verbessert, wenn all Ihre Domänencontroller über eine einzelne Azure ATP-Konsole überwacht werden.


## <a name="how-azure-atp-detects-activities-across-multiple-forests"></a>Erkennung von Aktivitäten in mehreren Gesamtstrukturen durch Azure ATP 

Zum Erkennen von Aktivitäten, die mehrere Gesamtstrukturen umfassen, fragen Azure ATP-Sensoren Domänencontroller in Remotegesamtstrukturen ab, um Profile für alle beteiligten Entitäten zu erstellen, z.B. Benutzer und Computer aus Remotegesamtstrukturen. 

> [!NOTE]
> - Azure ATP-Sensoren können in allen Gesamtstrukturen installiert werden (sofern eine minimale unidirektionale Vertrauensstellung vorhanden ist).
> - Der Benutzer, den Sie in der Azure ATP-Konsole unter **Verzeichnisdienste** konfigurieren, muss in allen anderen Gesamtstrukturen vertrauenswürdig sein.


Wenn Gesamtstrukturen ohne installierte Azure ATP-Sensoren vorhanden sind, kann Azure ATP die Aktivitäten in diesen Gesamtstrukturen dennoch anzeigen und überwachen. Die installierten ATP-Sensoren können alle verbundenen Domänencontroller der Remotegesamtstrukturen abfragen, um Benutzer und Computer aufzulösen und entsprechende Profile zu erstellen. 

## <a name="installation-requirements"></a>Installationsanforderungen 

-   Wenn eigenständige Azure ATP-Sensoren auf eigenständigen Computern und nicht direkt auf den Domänencontrollern installiert sind, stellen Sie sicher, dass die Kommunikation der Computer mit allen Domänencontrollern der Remotegesamtstrukturen über LDAP zulässig ist. 
- Der Benutzer, den Sie in der Azure ATP-Konsole unter **Verzeichnisdienste** konfigurieren, muss in allen anderen Gesamtstrukturen vertrauenswürdig sein und mindestens über Leseberechtigungen verfügen, um LDAP-Abfragen der Domänencontroller auszuführen.

- Damit Azure ATP mit den Azure ATP-Sensoren und eigenständigen Azure ATP-Sensoren kommunizieren kann, öffnen Sie die folgenden Ports auf jedem Computer mit installiertem Azure ATP-Sensor:

 
  |Protokoll|Transport|Port|Zu/Von|Direction|
  |----|----|----|----|----|
  |**Internetports**||||
  |SSL (*.atp.azure.com)|TCP|443|Azure ATP-Clouddienst|Outbound|
  |**Interne Ports**||||           
  |LDAP|TCP und UDP|389|Domänencontroller|Outbound|
  |Sicheres LDAP (LDAPS)|TCP|636|Domänencontroller|Outbound|
  |LDAP an globalen Katalog|TCP|3268|Domänencontroller|Outbound|
  |LDAPs an globalen Katalog|TCP|3269|Domänencontroller|Outbound|


## <a name="multi-forest-support-network-traffic-impact"></a>Auswirkungen auf den Netzwerkdatenverkehr bei der Unterstützung mehrerer Gesamtstrukturen 

Der Prozess des Zuordnens von Gesamtstrukturen durch Azure ATP hat folgende Auswirkungen:

-   Sobald der Azure ATP-Sensor ausgeführt wird, fragt er die Active Directory-Gesamtstrukturen am Remotestandort ab und ruft eine Liste von Benutzern und Computerdaten für die Profilerstellung ab.
-   Alle 5 Minuten fragt jeder Azure ATP-Sensor einen Domänencontroller aus jeder Domäne in jeder Gesamtstruktur ab, um alle Gesamtstrukturen im Netzwerk zuzuordnen.
-   Jeder Azure ATP-Sensor ordnet die Gesamtstrukturen mithilfe des Objekts „trustedDomain“ in Active Directory zu, indem er sich anmeldet und den Vertrauenstyp überprüft.
-   Sie können auch Ad-hoc-Datenverkehr anzeigen, wenn der Azure ATP-Sensor Aktivitäten zwischen Gesamtstrukturen erkennt. In diesem Fall senden die Azure ATP-Sensoren eine LDAP-Abfrage an die entsprechenden Domänencontroller, um Entitätsinformationen abzurufen. 

## <a name="known-limitations"></a>Bekannte Einschränkungen
-   Interaktive Anmeldungen, die von Benutzern in einer Gesamtstruktur durchgeführt werden, um auf Ressourcen in einer anderen Gesamtstruktur zuzugreifen, werden nicht im Azure ATP-Dashboard angezeigt.



## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Azure ATP architecture (Azure ATP-Architektur)](atp-architecture.md)
- [Install Azure ATP (Installieren von Azure ATP)](install-atp-step1.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)

