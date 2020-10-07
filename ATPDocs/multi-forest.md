---
title: Azure Advanced Threat Protection-Unterstützung für mehrere Gesamtstrukturen
description: Unterstützung für mehrere Active Directory-Gesamtstrukturen in Azure ATP
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cf3eb1dcc1d66caccfefda837804f771b3882e7a
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912682"
---
# <a name="azure-advanced-threat-protection-multi-forest-support"></a>Azure Advanced Threat Protection-Unterstützung für mehrere Gesamtstrukturen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="multi-forest-support-set-up"></a>Einrichten der Unterstützung für mehrere Gesamtstrukturen

Azure ATP unterstützt Organisationen mit mehreren Gesamtstrukturen, wodurch diese die Möglichkeit erhalten, Aktivitäten und Benutzerprofile in allen Gesamtstrukturen ganz einfach zu überwachen.

Unternehmensorganisationen können in der Regel über mehrere Active Directory-Gesamtstrukturen verfügen, die oft für verschiedene Zwecke genutzt werden. Dies schließt auch ältere, aus Unternehmenszusammenschlüssen und -übernahmen stammende Infrastrukturen, die geografische Verteilung und Sicherheitsbegrenzungen (Red Forests) ein. Sie können mehrere Gesamtstrukturen mit Azure ATP schützen, um die Überwachung und Untersuchungen Ihres gesamten Netzwerks über eine zentrale Konsole auszuführen.

Die Möglichkeit, mehrere Active Directory-Gesamtstrukturen zu unterstützen, bietet folgende Vorteile:

- Sie können Aktivitäten, die von Benutzern in mehreren Gesamtstrukturen ausgeführt werden, in einer zentralen Konsole im Blick behalten und untersuchen.
- Durch erweiterte Active Directory-Integration und -Kontoauflösung lassen sich falsch positive Ergebnisse besser erkennen und reduzieren.
- Sie ermöglicht eine bessere Kontrolle und eine einfachere Bereitstellung. Verbesserte Integritäts Warnungen und Berichterstellung für die übergreifende Abdeckung, wenn alle Domänen Controller über eine einzige Azure ATP Konsole überwacht werden.

## <a name="azure-atp-detection-activity-across-multiple-forests"></a>Erkennung von Aktivitäten in mehreren Gesamtstrukturen durch Azure ATP

Zum Erkennen von Aktivitäten, die mehrere Gesamtstrukturen umfassen, fragen Azure ATP-Sensoren Domänencontroller in Remotegesamtstrukturen ab, um Profile für alle beteiligten Entitäten zu erstellen, z.B. Benutzer und Computer aus Remotegesamtstrukturen.

- Azure ATP Sensoren können auf Domänen Controllern in allen Gesamtstrukturen installiert werden, sogar Gesamtstrukturen ohne Vertrauensstellung.
- Fügen Sie auf der Seite Verzeichnisdienste zusätzliche Anmelde Informationen hinzu, um nicht vertrauenswürdige Gesamtstrukturen in Ihrer Umgebung zu unterstützen.
    - Es ist nur eine Anmelde Information erforderlich, um alle Gesamtstrukturen mit einer bidirektionalen Vertrauensstellung zu unterstützen.
    - Zusätzliche Anmelde Informationen sind nur für jede Gesamtstruktur mit nicht-Kerberos-Vertrauensstellung oder keine Vertrauensstellung erforderlich.
    - Es gibt ein Standard Limit von 10 nicht vertrauenswürdigen Gesamtstrukturen pro Azure ATP Instanz. Wenden Sie sich an den Support, wenn Ihre Organisation über mehr als 10 Gesamtstrukturen verfügt.

![Azure ATP-Willkommensseite 1](media/directory-services-add-no-trust-forests.png)

### <a name="requirements"></a>Anforderungen

- Der Benutzer, den Sie in der Azure ATP-Konsole unter **Verzeichnisdienste** konfigurieren, muss in allen anderen Gesamtstrukturen vertrauenswürdig sein und mindestens über Leseberechtigungen verfügen, um LDAP-Abfragen der Domänencontroller auszuführen.
- Wenn eigenständige Azure ATP-Sensoren auf eigenständigen Computern und nicht direkt auf den Domänencontrollern installiert sind, stellen Sie sicher, dass die Kommunikation der Computer mit allen Domänencontrollern der Remotegesamtstrukturen über LDAP zulässig ist.

- Damit Azure ATP mit den Azure ATP-Sensoren und eigenständigen Azure ATP-Sensoren kommunizieren kann, öffnen Sie die folgenden Ports auf jedem Computer mit installiertem Azure ATP-Sensor:

  |Protokoll|Transport|Port|Zu/Von|Richtung|
  |----|----|----|----|----|
  |**Internetports**||||
  |SSL (*.atp.azure.com)|TCP|443|Azure ATP-Clouddienst|Ausgehend|
  |**Interne Ports**||||
  |LDAP|TCP und UDP|389|Domänencontroller|Ausgehend|
  |Sicheres LDAP (LDAPS)|TCP|636|Domänencontroller|Ausgehend|
  |LDAP an globalen Katalog|TCP|3268|Domänencontroller|Ausgehend|
  |LDAPs an globalen Katalog|TCP|3269|Domänencontroller|Ausgehend|

## <a name="multi-forest-support-network-traffic-impact"></a>Auswirkungen auf den Netzwerkdatenverkehr bei der Unterstützung mehrerer Gesamtstrukturen

Der Prozess des Zuordnens von Gesamtstrukturen durch Azure ATP hat folgende Auswirkungen:

- Sobald der Azure ATP-Sensor ausgeführt wird, fragt er die Active Directory-Gesamtstrukturen am Remotestandort ab und ruft eine Liste von Benutzern und Computerdaten für die Profilerstellung ab.
- Alle 5 Minuten fragt jeder Azure ATP-Sensor einen Domänencontroller aus jeder Domäne in jeder Gesamtstruktur ab, um alle Gesamtstrukturen im Netzwerk zuzuordnen.
- Jeder Azure ATP-Sensor ordnet die Gesamtstrukturen mithilfe des Objekts „trustedDomain“ in Active Directory zu, indem er sich anmeldet und den Vertrauenstyp überprüft.
- Sie können auch Ad-hoc-Datenverkehr anzeigen, wenn der Azure ATP-Sensor Aktivitäten zwischen Gesamtstrukturen erkennt. In diesem Fall senden die Azure ATP-Sensoren eine LDAP-Abfrage an die entsprechenden Domänencontroller, um Entitätsinformationen abzurufen.

## <a name="known-limitations"></a>Bekannte Einschränkungen

- Interaktive Anmeldungen, die von Benutzern in einer Gesamtstruktur durchgeführt werden, um auf Ressourcen in einer anderen Gesamtstruktur zuzugreifen, werden nicht im Azure ATP-Dashboard angezeigt.

## <a name="see-also"></a>Weitere Informationen

- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](https://aka.ms/aatpsizingtool)
- [Azure ATP architecture (Azure ATP-Architektur)](architecture.md)
- [Install Azure ATP (Installieren von Azure ATP)](install-step1.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)