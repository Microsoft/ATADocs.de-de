---
title: Unterstützung von Microsoft Defender für die Identitäts übergreifende Unterstützung
description: Unterstützung für mehrere Active Directory Gesamtstrukturen in Microsoft Defender für die Identität.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9f3a6771591fb3e3d63a45887b1f7a89bddc57d7
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275712"
---
# <a name="product-long-multi-forest-support"></a>[!INCLUDE [Product long](includes/product-long.md)] Unterstützung für mehrere Gesamtstrukturen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="multi-forest-support-set-up"></a>Einrichten der Unterstützung für mehrere Gesamtstrukturen

[!INCLUDE [Product long](includes/product-long.md)] unterstützt Organisationen mit mehreren Gesamtstrukturen und ermöglicht Ihnen die einfache Überwachung von Aktivitäts-und Profil Benutzern in Gesamtstrukturen.

Unternehmensorganisationen können in der Regel über mehrere Active Directory-Gesamtstrukturen verfügen, die oft für verschiedene Zwecke genutzt werden. Dies schließt auch ältere, aus Unternehmenszusammenschlüssen und -übernahmen stammende Infrastrukturen, die geografische Verteilung und Sicherheitsbegrenzungen (Red Forests) ein. Sie können mehrere Gesamtstrukturen mithilfe [!INCLUDE [Product short](includes/product-short.md)] von schützen, sodass Sie das gesamte Netzwerk über einen einzelnen Glasbereich überwachen und untersuchen können.

Die Möglichkeit, mehrere Active Directory-Gesamtstrukturen zu unterstützen, bietet folgende Vorteile:

- Sie können Aktivitäten, die von Benutzern in mehreren Gesamtstrukturen ausgeführt werden, in einer zentralen Konsole im Blick behalten und untersuchen.
- Durch erweiterte Active Directory-Integration und -Kontoauflösung lassen sich falsch positive Ergebnisse besser erkennen und reduzieren.
- Sie ermöglicht eine bessere Kontrolle und eine einfachere Bereitstellung. Verbesserte Integritäts Warnungen und Berichterstellung für die übergreifende Abdeckung, wenn alle Domänen Controller über eine einzige Konsole überwacht werden [!INCLUDE [Product short](includes/product-short.md)] .

## <a name="product-short-detection-activity-across-multiple-forests"></a>[!INCLUDE [Product short](includes/product-short.md)] Erkennungs Aktivität in mehreren Gesamtstrukturen

Zum Erkennen von Gesamtstruktur übergreifenden Aktivitäten werden von den [!INCLUDE [Product short](includes/product-short.md)] Sensoren Domänen Controller in Remote Gesamtstrukturen abgefragt, um Profile für alle Beteiligten Entitäten (einschließlich Benutzer und Computer aus Remote Gesamtstrukturen) zu erstellen.

- [!INCLUDE [Product short](includes/product-short.md)] Sensoren können auf Domänen Controllern in allen Gesamtstrukturen installiert werden, sogar Gesamtstrukturen ohne Vertrauensstellung.
- Fügen Sie auf der Seite Verzeichnisdienste zusätzliche Anmelde Informationen hinzu, um nicht vertrauenswürdige Gesamtstrukturen in Ihrer Umgebung zu unterstützen.
  - Es ist nur eine Anmelde Information erforderlich, um alle Gesamtstrukturen mit einer bidirektionalen Vertrauensstellung zu unterstützen.
  - Zusätzliche Anmelde Informationen sind nur für jede Gesamtstruktur mit nicht-Kerberos-Vertrauensstellung oder keine Vertrauensstellung erforderlich.
  - Es gibt ein Standard Limit von 10 nicht vertrauenswürdigen Gesamtstrukturen pro [!INCLUDE [Product short](includes/product-short.md)] Instanz. Wenden Sie sich an den Support, wenn Ihre Organisation über mehr als 10 Gesamtstrukturen verfügt.

![[! INCLUDE [Product Short] (includes/Produkt-Short. MD)] Willkommens Phase 1](media/directory-services-add-no-trust-forests.png)

### <a name="requirements"></a>Anforderungen

- Der Benutzer, den Sie in der- [!INCLUDE [Product short](includes/product-short.md)] Konsole unter **Verzeichnisdienste** konfigurieren, muss in allen anderen Gesamtstrukturen als vertrauenswürdig eingestuft werden und muss mindestens über Leseberechtigung verfügen, um LDAP-Abfragen auf den Domänen Controllern auszuführen.
- Wenn [!INCLUDE [Product short](includes/product-short.md)] eigenständige Sensoren auf eigenständigen Computern anstatt direkt auf den Domänen Controllern installiert werden, müssen Sie sicherstellen, dass die Computer mit allen Remote Gesamtstruktur-Domänen Controllern über LDAP kommunizieren können.

- Um [!INCLUDE [Product short](includes/product-short.md)] mit den [!INCLUDE [Product short](includes/product-short.md)] Sensoren und [!INCLUDE [Product short](includes/product-short.md)] eigenständigen Sensoren zu kommunizieren, öffnen Sie die folgenden Ports auf jedem Computer, auf dem der [!INCLUDE [Product short](includes/product-short.md)] Sensor installiert ist:

  |Protokoll|Transport|Port|Zu/Von|Richtung|
  |----|----|----|----|----|
  |**Internetports**||||
  |SSL (*.atp.azure.com)|TCP|443|[!INCLUDE [Product short](includes/product-short.md)] clouddienst|Ausgehend|
  |**Interne Ports**||||
  |LDAP|TCP und UDP|389|Domänencontroller|Ausgehend|
  |Sicheres LDAP (LDAPS)|TCP|636|Domänencontroller|Ausgehend|
  |LDAP an globalen Katalog|TCP|3268|Domänencontroller|Ausgehend|
  |LDAPs an globalen Katalog|TCP|3269|Domänencontroller|Ausgehend|

## <a name="multi-forest-support-network-traffic-impact"></a>Auswirkungen auf den Netzwerkdatenverkehr bei der Unterstützung mehrerer Gesamtstrukturen

Wenn die Gesamtstrukturen zuordnet [!INCLUDE [Product short](includes/product-short.md)] , wird ein Prozess verwendet, der sich auf Folgendes auswirkt:

- Nach der [!INCLUDE [Product short](includes/product-short.md)] Ausführung des Sensors werden die Remote Active Directory-Gesamtstrukturen abgefragt und eine Liste von Benutzern und Computer Daten für die Profilerstellung abgerufen.
- Alle fünf Minuten fragt jeder [!INCLUDE [Product short](includes/product-short.md)] Sensor einen Domänen Controller aus jeder Domäne (von jeder Gesamtstruktur) ab, um alle Gesamtstrukturen im Netzwerk zuzuordnen.
- Jeder [!INCLUDE [Product short](includes/product-short.md)] Sensor ordnet die Gesamtstrukturen mithilfe des Objekts "Treuhänder Domäne" in Active Directory zu, indem er sich anmeldet und den vertrauensungstyp prüft.
- Sie können auch Ad-hoc-Datenverkehr sehen, wenn der Sensor eine Gesamtstruktur [!INCLUDE [Product short](includes/product-short.md)] übergreifende Aktivität erkennt. Wenn dies auftritt, [!INCLUDE [Product short](includes/product-short.md)] senden die Sensoren eine LDAP-Abfrage an die relevanten Domänen Controller, um Entitäts Informationen abzurufen.

## <a name="known-limitations"></a>Bekannte Einschränkungen

- Interaktive Anmeldungen, die von Benutzern in einer Gesamtstruktur ausgeführt werden, um auf Ressourcen in einer anderen Gesamtstruktur zuzugreifen, werden im Dashboard nicht angezeigt [!INCLUDE [Product short](includes/product-short.md)] .

## <a name="see-also"></a>Weitere Informationen

- [[!INCLUDE [Product short](includes/product-short.md)] Tool zur Größenanpassung](https://aka.ms/aatpsizingtool)
- [[!INCLUDE [Product short](includes/product-short.md)] Architektur](architecture.md)
- [Installieren [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Sehen Sie sich das [!INCLUDE [Product short](includes/product-short.md)] Forum an!](https://aka.ms/MDIcommunity)
