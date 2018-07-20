---
title: Azure Advanced Threat Protection-Unterstützung für mehrere Gesamtstrukturen | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Unterstützung für mehrere Active Directory-Gesamtstrukturen in Azure ATP einrichten.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/17/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c76e459709c786082bea7566a61e5384a235eda4
ms.sourcegitcommit: 8feb9b65dc0e1de0ace00aca11784e54f9852a15
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2018
ms.locfileid: "39098182"
---
*Gilt für: Azure Advanced Threat Protection*

# <a name="install-azure-atp---step-9"></a>Installieren von Azure ATP: Schritt 9

>[!div class="step-by-step"]
[« Schritt 8 ](install-atp-step8-samr.md)

## <a name="step-9--set-up-azure-advanced-threat-protection-multi-forest-support"></a>Schritt 9:  Einrichten der Azure Advanced Threat Protection-Unterstützung für mehrere Gesamtstrukturen

Azure ATP kann Organisationen mit mehreren Gesamtstrukturen unterstützen, wodurch diese die Möglichkeit erhalten, Aktivitäten und Benutzerprofile in allen Gesamtstrukturen zu überwachen. 

Eine Unternehmensorganisation kann über mehrere Active Directory-Gesamtstrukturen verfügen, die oft für verschiedene Zwecke genutzt werden. Dies schließt auch ältere, aus Unternehmenszusammenschlüssen und -übernahmen stammende Infrastrukturen, die geografischen Verteilung und Sicherheitsgrenzen (Red Forests) ein. Sie können mehrere Gesamtstrukturen mit Azure ATP schützen, indem Sie einen Bericht zu allen Daten an einen einzigen, primären Arbeitsbereich senden, um die Überwachung und Untersuchungen über eine zentrale Konsole auszuführen.

Die Möglichkeit, mehrere Active Directory-Gesamtstrukturen zu unterstützen, bietet folgende Vorteile:
-   Sie können in mehreren Gesamtstrukturen ausgeführte Benutzeraktivitäten von einer zentralen Konsole aus im Blick halten und untersuchen. 
-   Die Unterstützung mehrerer Gesamtstrukturen verbessert die Erkennung und reduziert falsch positive Ergebnisse durch erweiterte Active Directory-Integration und -Kontoauflösung. 
-   Da Sie durch die Unterstützung mehrerer Gesamtstrukturen nicht mehr mehrere Arbeitsbereiche benötigen, haben Sie mehr Kontrolle und auch die Bereitstellung wird einfacher. Gleichzeitig werden Ihre Domänencontroller alle zentral von einer einzigen Azure ATP-Konsole aus überwacht, die eine bessere, organisationsübergreifende Überwachung und Berichterstattung bietet.


## <a name="how-azure-atp-detects-activities-across-multiple-forests"></a>Erkennung von Aktivitäten in mehreren Gesamtstrukturen durch Azure ATP 

Zum Erkennen von Aktivitäten, die mehrere Gesamtstrukturen umfassen, fragen Azure ATP-Sensoren Domänencontroller in Remotegesamtstrukturen ab, um Profile für alle beteiligten Entitäten zu erstellen, z.B. Benutzer und Computer aus Remotegesamtstrukturen. 

> [!NOTE]
> - Damit dies funktioniert, muss seine Vertrauensstellung zwischen allen anderen Gesamtstrukturen und der Gesamtstruktur, in der die Azure ATP-Sensoren installiert sind, bestehen.
> - Der Benutzer, den Sie in der Azure ATP-Konsole unter **Verzeichnisdienste** konfigurieren, muss in allen anderen Gesamtstrukturen vertrauenswürdig sein.


Wenn Gesamtstrukturen ohne installierte Azure ATP-Sensoren vorhanden sind, kann Azure ATP die Aktivitäten in diesen Gesamtstrukturen dennoch anzeigen und überwachen. Die installierten ATP-Sensoren können alle angeschlossenen Domänencontroller der Remotegesamtstrukturen abfragen, um Benutzer und Computer aufzulösen und entsprechende Profile zu erstellen. 

## <a name="installation-requirements"></a>Installationsanforderungen 

-   Wenn eigenständige Azure ATP-Sensoren auf eigenständigen Computern und nicht direkt auf den Domänencontrollern installiert sind, stellen Sie sicher, dass die Kommunikation der Computer mit allen Domänencontrollern der Remotegesamtstrukturen über LDAP zulässig ist. 
- Der Benutzer, den Sie in der Azure ATP-Konsole unter **Verzeichnisdienste** konfigurieren, muss in allen anderen Gesamtstrukturen vertrauenswürdig sein und mindestens über Leseberechtigungen verfügen, um LDAP-Abfragen der Domänencontroller auszuführen.

- Damit Azure ATP mit den ATP-Sensoren und eigenständigen ATP-Sensoren kommunizieren kann, öffnen Sie die folgenden Ports auf jedem Computer mit installiertem ATP-Sensor:

 
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

-   Sobald der Azure ATP-Sensor ausgeführt wird, fragt er die Active Directory-Gesamtstrukturen am Remotestandort ab und ruft eine Liste von Benutzern und Computerdaten für die Profilerstellung ab.
-   Alle 5 Minuten fragt jeder Azure ATP-Sensor einen Domänencontroller aus jeder Domäne in jeder Gesamtstruktur ab, um alle Gesamtstrukturen im Netzwerk zuzuordnen.
-   Jeder Azure ATP-Sensor ordnet die Gesamtstrukturen mithilfe des Objekts „trustedDomain“ in Active Directory zu, indem er sich anmeldet und den Vertrauenstyp überprüft.
-   Sie können auch Ad-hoc-Datenverkehr anzeigen, wenn der ATP-Sensor Aktivitäten zwischen Gesamtstrukturen erkennt. In diesem Fall senden die ATP-Sensoren eine LDAP-Abfrage an die entsprechenden Domänencontroller, um Entitätsinformationen abzurufen. 

## <a name="known-limitations"></a>Bekannte Einschränkungen
-   Interaktive Anmeldungen, die von Benutzern in einer Gesamtstruktur durchgeführt werden, um auf Ressourcen in einer anderen Gesamtstruktur zuzugreifen, werden nicht im Azure ATP-Dashboard angezeigt.


>[!div class="step-by-step"]
[« Schritt 8 ](install-atp-step8-samr.md)


## <a name="see-also"></a>Weitere Informationen
- [Tool zur Bemessung von ATA-Gateways](http://aka.ms/aatpsizingtool)
- [ATA-Architektur](atp-architecture.md)
- [Installieren von ATA](install-atp-step1.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)

