---
title: Azure Advanced Threat Protection-Netzwerknamensauflösung
description: Dieser Artikel stellt eine Übersicht der erweiterten Funktionen und Einsatzweisen der Netzwerknamensauflösung von Azure ATP dar.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 03/22/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ac873fc-b763-41d7-878e-7c08da421cb5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 35d3e630e8f8ff4752badc5e2dad09aec8058671
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80666204"
---
# <a name="what-is-network-name-resolution"></a>Was ist Netzwerknamensauflösung?

Die Netzwerknamensauflösung (Network Name Resolution, NNR) ist ein Hauptbestandteil der Azure ATP-Funktionalität. Azure ATP erfasst Aktivitäten auf der Grundlage von Netzwerkdatenverkehr, Windows-Ereignissen und ETW – diese Aktivitäten enthalten normalerweise IP-Daten.

Durch die Verwendung von NNR kann Azure ATP reinen Aktivitäten (mit IP-Adressen) die entsprechenden, an der Aktivität beteiligten Computer zuordnen. Auf Grundlage der reinen Aktivitäten erstellt Azure ATP ein Profil der Entitäten, wie etwa Computer, und generiert Sicherheitswarnungen für verdächtige Aktivitäten.

Zum Auflösen von IP-Adressen in Computernamen suchen Azure ATP-Sensoren die IP-Adressen mithilfe der folgenden Methoden:

- NTLM über RPC (TCP-Port 135)
- NetBIOS (UDP-Port 137)
- RDP (TCP-Port 3389): nur das erste Paket von **ClientHello**
- Abfragen des DNS-Servers mittels Reverse-DNS-Lookup der IP-Adresse (UDP 53)

Um die besten Ergebnisse zu erzielen, sollten alle Methoden verwendet werden. Wenn dies nicht möglich ist, sollten Sie die DNS-Suchmethode und mindestens eine der anderen Methoden verwenden.

> [!NOTE]
> An keinem dieser Ports erfolgt eine Authentifizierung.

Azure ATP wertet das Betriebssystem des Geräts basierend auf dem Netzwerkdatenverkehr aus und legt es fest. Nach dem Abrufen des Computernamens überprüft der Azure ATP-Sensor in Active Directory Domain Services, ob ein zugehöriges Computerobjekt mit gleichem Computernamen vorhanden ist und verwendet TCP-Fingerabdrücke. Mithilfe von TCP-Fingerabdrücken können nicht registrierte und Nicht-Windows-Geräte identifiziert werden, sodass der Untersuchungsprozess vereinfacht wird.
Wenn der Azure ATP-Sensor die Korrelation findet, ordnet er die IP dem betreffenden Computerobjekt zu.

In Fällen, in denen kein Name abgerufen wird, wird ein **nicht aufgelöstes Computerprofil nach IP-Adresse** mit der IP-Adresse und der relevanten erkannten Aktivität erstellt.

![Nicht aufgelöstes Computerprofil](media/unresolved-computer-profile.png)

NNR-Daten spielen beim Erkennen der folgenden Bedrohungen eine entscheidende Rolle:

- Suspected identity theft (pass-the-ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket))
- Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))
- Network mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))

Um Ihre Fähigkeit zur Bestimmung, ob es sich bei einer Warnung um eine **richtig positives** oder **falsch positives**  Ergebnis handelt, zu verbessern, schließt Azure ATP den Grad der Zuverlässigkeit der Computernamensauflösung in den Nachweis jeder Sicherheitswarnung ein.

Wenn beispielsweise Computernamen mit **hoher Gewissheit** aufgelöst werden, erhöht dies die Zuverlässigkeit, dass es sich bei der resultierenden Sicherheitswarnung um eine **richtig positives** **Ergebnis** handelt.

Der Beweis umfasst die Uhrzeit, die IP-Adresse und den Computernamen, in den die IP-Adresse aufgelöst wurde. Wenn die Gewissheit der Auflösung **niedrig** ist, nutzen Sie diese Informationen, um zu untersuchen und zu bestätigen, welches Gerät zu diesem Zeitpunkt die tatsächliche Quelle der IP-Adresse war.
Nachdem Sie das Gerät bestätigt haben, können Sie anschließend feststellen, ob es sich bei der Warnung um ein **falsch positives** **Ergebnis** handelt, ähnlich wie in den folgenden Beispielen:

- Vermuteter Identitätsdiebstahl (Pass-the-Ticket): Die Warnung wurde für denselben Computer ausgelöst.
- Vermuteter DCSync-Angriff (Replikation der Verzeichnisdienste): Die Warnung wurde vom Domänencontroller ausgelöst.
- „Reconnaissance über Netzwerkzuordnung“ (DNS): Die Warnung wurde von einem DNS-Server ausgelöst

    ![Beweissicherheit](media/nnr-high-certainty.png)

### <a name="prerequisites"></a>Voraussetzungen

|Protokoll|Transport|Port|Device|Richtung|
|--------|--------|------|-------|------|
|NTLM über RPC*|TCP|135|Alle Geräte im Netzwerk|Eingehende Verbindungen|
|NetBIOS*|UDP|137|Alle Geräte im Netzwerk|Eingehende Verbindungen|
|RDP*|TCP|3389|Alle Geräte im Netzwerk|Eingehende Verbindungen|
|DNS|UDP|53|Domänencontroller|Ausgehend|

\* Eine dieser Methoden ist erforderlich, aber sie sollten alle verwenden.

Um sicherzustellen, dass Azure ATP optimal funktioniert und die Umgebung ordnungsgemäß konfiguriert ist, überprüft Azure ATP den Auflösungsstatus jedes Sensors und gibt pro Methode eine Integritätswarnung heraus, sodass eine Liste der Azure ATP-Sensoren mit geringer Erfolgsquote bei der aktiven Namensauflösung für die einzelnen Methoden bereitgestellt wird.

> [!NOTE]
> Wenn Sie eine optionale NNR-Methode in Azure ATP deaktivieren müssen, um die Anforderungen Ihrer Umgebung zu erfüllen, eröffnen Sie ein Supportticket.

Jede Integritätswarnung enthält spezifische Details zu Methode, Sensoren, der problematischen Richtlinie sowie Konfigurationsempfehlungen.

![Warnung bei geringer Erfolgsquote der Netzwerknamensauflösung (NNR)](media/atp-nnr-success-rate.png)

### <a name="configuration-recommendations"></a>Konfigurationsempfehlungen

- NTLM über RPC:
  - Achten Sie darauf, dass TCP-Port 135 für eingehende Kommunikation von Azure ATP-Sensoren auf allen Computern in der Umgebung geöffnet ist.
  - Überprüfen Sie die gesamte Netzwerkkonfiguration (Firewalls), da diese die Kommunikation mit den relevanten Ports verhindern kann.

- NetBIOS:
  - Achten Sie darauf, dass UDP-Port 137 für eingehende Kommunikation von Azure ATP-Sensoren auf allen Computern in der Umgebung geöffnet ist.
  - Überprüfen Sie die gesamte Netzwerkkonfiguration (Firewalls), da diese die Kommunikation mit den relevanten Ports verhindern kann.
- RDP:
  - Achten Sie darauf, dass TCP-Port 3389 für eingehende Kommunikation von Azure ATP-Sensoren auf allen Computern in der Umgebung geöffnet ist.
  - Überprüfen Sie die gesamte Netzwerkkonfiguration (Firewalls), da diese die Kommunikation mit den relevanten Ports verhindern kann.
- Reverse-DNS:
  - Achten Sie darauf, dass der Sensor den DNS-Server erreichen kann und dass Reverse-Lookup-Zonen aktiviert sind.

## <a name="see-also"></a>Weitere Informationen:

- [Voraussetzungen für Azure ATP](atp-prerequisites.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
