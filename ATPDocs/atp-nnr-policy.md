---
title: Azure Advanced Threat Protection-Netzwerknamensauflösung | Microsoft-Dokumentation
description: Dieser Artikel stellt eine Übersicht der erweiterten Funktionen und Einsatzweisen der Netzwerknamensauflösung von Azure ATP dar.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1ac873fc-b763-41d7-878e-7c08da421cb5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d3f6b3fda2dbfca0250069ba08d027b1b16d5659
ms.sourcegitcommit: 6975497acaf298af393f96573e1790ab617fa5b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/25/2019
ms.locfileid: "58406654"
---
# <a name="what-is-network-name-resolution"></a>Was ist Netzwerknamensauflösung?

Die Netzwerknamensauflösung (Network Name Resolution, NNR) ist eine Hauptkomponente der Azure ATP-Funktionalität. Azure ATP erfasst Aktivitäten auf der Grundlage von Netzwerkdatenverkehr, Windows-Ereignissen und ETW – diese Aktivitäten enthalten normalerweise IP-Daten.  

Durch die Verwendung von NNR ordnet Azure ATP reinen Aktivitäten (mit IP-Adressen) die entsprechenden, an der Aktivität beteiligten Computer zu. Auf Grundlage der reinen Aktivitäten erstellt Azure ATP ein Profil der Entitäten, wie etwa Computer, und generiert Sicherheitswarnungen für verdächtige Aktivitäten.

NNR-Daten spielen beim Erkennen der folgenden Bedrohungen eine entscheidende Rolle:

- Suspected identity theft (pass-the-ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket))
- Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))
- Network mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))
- Suspected NTLM relay attack (Exchange account) (Vermuteter NTLM-Relaisangriff (Exchange-Konto))

Um IP-Adressen zu Computernamen aufzulösen, fragen ATP-Sensoren die IP-Adresse für den Computernamen „hinter“ der IP ab und verwenden dazu eine der folgenden Methoden:

1. NTLM über RPC (TCP-Port 135)
2. NetBIOS (UDP-Port 137)
3. RDP (TCP-Port 3389): nur das erste Paket von **ClientHello**
4. Abfragen des DNS-Servers mittels Reverse-DNS-Lookup der IP-Adresse (UDP 53)

> [!NOTE]
>An keinem dieser Ports erfolgt eine Authentifizierung.

Nach dem Abrufen des Computernamens sieht der Azure ATP-Sensor in Active Directory nach, ob ein zugehöriges Computerobjekt mit gleichem Computernamen vorhanden ist. Wenn der Sensor die Korrelation findet, ordnet er diese IP dem betreffenden Computerobjekt zu.

### <a name="prerequisites"></a>Voraussetzungen
|Protokoll|  Transport|  Port|   Gerät| Richtung|
|--------|--------|------|-------|------|
|NTLM über RPC| TCP |135|   Alle Geräte im Netzwerk| Eingehend|
|NetBIOS|   UDP|    137|    Alle Geräte im Netzwerk| Eingehend|
|DNS|   UDP|    53| Domänencontroller| Ausgehend|
|

Wenn Port 3389 auf Geräten in der Umgebung geöffnet ist, verwendet ihn der Azure ATP-Sensor zum Zweck der Netzwerknamensauflösung.
Das Öffnen von Port 3389 **ist keine Voraussetzung**, es stellt lediglich eine zusätzliche Methode dar, wie der Computername bereitgestellt werden kann, wenn der Port bereits für andere Zwecke geöffnet ist.

Um sicherzustellen, dass Azure ATP optimal funktioniert und die Umgebung ordnungsgemäß konfiguriert ist, überprüft Azure ATP den Auflösungsstatus jedes Sensors und gibt pro Methode eine Überwachungswarnung heraus, sodass eine Liste der Azure ATP-Sensoren mit geringer Erfolgsquote bei der aktiven Namensauflösung für die einzelnen Methoden bereitgestellt wird.

Jede Überwachungswarnung enthält spezifische Details zu Methode, Sensoren, der problematischen Richtlinie sowie Konfigurationsempfehlungen.

![Warnung bei geringer Erfolgsquote der Netzwerknamensauflösung (NNR)](media/atp-health-alert-audit-policy.png)


### <a name="configuration-recommendations"></a>Konfigurationsempfehlungen

- RPC-über-NTLM:
    - Achten Sie darauf, dass Port 135 für eingehende Kommunikation von Azure ATP-Sensoren auf allen Computern in der Umgebung geöffnet ist.
    - Überprüfen Sie die gesamte Netzwerkkonfiguration (Firewalls), da diese die Kommunikation mit den relevanten Ports verhindern kann.

-NetBIOS:
    - Achten Sie darauf, dass Port 137 für eingehende Kommunikation von Azure ATP-Sensoren auf allen Computern in der Umgebung geöffnet ist.
    - Überprüfen Sie die gesamte Netzwerkkonfiguration (Firewalls), da diese die Kommunikation mit den relevanten Ports verhindern kann.
- Reverse-DNS:
    - Achten Sie darauf, dass der Sensor den DNS-Server erreichen kann und dass Reverse-Lookup-Zonen aktiviert sind.


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
