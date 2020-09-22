---
title: Auflösung von Azure Advanced Threat Protection Netzwerknamen
description: Dieser Artikel stellt eine Übersicht der erweiterten Funktionen und Einsatzweisen der Netzwerknamensauflösung von Azure ATP dar.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/22/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ac873fc-b763-41d7-878e-7c08da421cb5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4c98696b11ba329b6b907003b86cc5bd3d111cdf
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912699"
---
# <a name="what-is-network-name-resolution"></a>Was ist Netzwerknamensauflösung?

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Network Name Resolution (NNR) ist eine Hauptkomponente der Azure ATP Funktionalität. Azure ATP erfasst Aktivitäten auf der Grundlage von Netzwerkdatenverkehr, Windows-Ereignissen und ETW – diese Aktivitäten enthalten normalerweise IP-Daten.

Mithilfe von NNR können Azure ATP zwischen rohaktivitäten (die IP-Adressen enthält) und den relevanten Computern, die an den einzelnen Aktivitäten beteiligt sind, korrelieren. Auf Grundlage der reinen Aktivitäten erstellt Azure ATP ein Profil der Entitäten, wie etwa Computer, und generiert Sicherheitswarnungen für verdächtige Aktivitäten.

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

Um Ihre Fähigkeit zur Bestimmung, ob es sich bei einer Warnung um eine **richtig positives** oder **falsch positives ** Ergebnis handelt, zu verbessern, schließt Azure ATP den Grad der Zuverlässigkeit der Computernamensauflösung in den Nachweis jeder Sicherheitswarnung ein.

Wenn beispielsweise Computernamen mit **hoher Gewissheit** aufgelöst werden, erhöht dies die Zuverlässigkeit, dass es sich bei der resultierenden Sicherheitswarnung um eine **richtig positives****Ergebnis** handelt.

Der Beweis umfasst die Uhrzeit, die IP-Adresse und den Computernamen, in den die IP-Adresse aufgelöst wurde. Wenn die Gewissheit der Auflösung **niedrig** ist, nutzen Sie diese Informationen, um zu untersuchen und zu bestätigen, welches Gerät zu diesem Zeitpunkt die tatsächliche Quelle der IP-Adresse war.
Nachdem Sie das Gerät bestätigt haben, können Sie anschließend feststellen, ob es sich bei der Warnung um ein **falsch positives****Ergebnis** handelt, ähnlich wie in den folgenden Beispielen:

- Vermuteter Identitätsdiebstahl (Pass-the-Ticket): Die Warnung wurde für denselben Computer ausgelöst.
- Vermuteter DCSync-Angriff (Replikation der Verzeichnisdienste): Die Warnung wurde vom Domänencontroller ausgelöst.
- „Reconnaissance über Netzwerkzuordnung“ (DNS): Die Warnung wurde von einem DNS-Server ausgelöst

    ![Beweissicherheit](media/nnr-high-certainty.png)

### <a name="prerequisites"></a>Voraussetzungen

|Protokoll|Transport|Port|Sicherungsmedium|Direction|
|--------|--------|------|-------|------|
|NTLM über RPC *|TCP|135|Alle Geräte im Netzwerk|Eingehende Verbindungen|
|NetBIOS-|UDP|137|Alle Geräte im Netzwerk|Eingehende Verbindungen|
|RDP|TCP|3389|Alle Geräte im Netzwerk|Eingehende Verbindungen|
|DNS|UDP|53|Domänencontroller|Ausgehend|

\* Eine dieser Methoden ist erforderlich, aber es wird empfohlen, alle zu verwenden.

Um sicherzustellen, dass Azure ATP im Idealfall funktioniert und die Umgebung ordnungsgemäß konfiguriert ist, prüft Azure ATP den Auflösungs Status der einzelnen Sensoren und gibt eine Integritäts Warnung pro Methode aus, um eine Liste der Azure ATP Sensoren mit niedriger Erfolgsrate der aktiven Namensauflösung mit jeder Methode bereitzustellen.

> [!NOTE]
> Wenn Sie eine optionale NNR-Methode in Azure ATP deaktivieren müssen, um die Anforderungen Ihrer Umgebung zu erfüllen, eröffnen Sie ein Supportticket.

Jede Integritäts Warnung enthält spezifische Details der Methode, der Sensoren, der problematischen Richtlinie und der Konfigurations Empfehlungen.

![Warnung bei geringer Erfolgsquote der Netzwerknamensauflösung (NNR)](media/atp-nnr-success-rate.png)

### <a name="configuration-recommendations"></a>Konfigurationsempfehlungen

- NTLM über RPC:
  - Achten Sie darauf, dass TCP-Port 135 für eingehende Kommunikation von Azure ATP-Sensoren auf allen Computern in der Umgebung geöffnet ist.
  - Überprüfen Sie die gesamte Netzwerkkonfiguration (Firewalls), da diese die Kommunikation mit den relevanten Ports verhindern kann.

- NetBIOS:
  - Achten Sie darauf, dass UDP-Port 137 für eingehende Kommunikation von Azure ATP-Sensoren auf allen Computern in der Umgebung geöffnet ist.
  - Überprüfen Sie die gesamte Netzwerkkonfiguration (Firewalls), da diese die Kommunikation mit den relevanten Ports verhindern kann.
- RDP:
  - Überprüfen Sie, ob der TCP-Port 3389 für die eingehende Kommunikation von Azure ATP Sensoren auf allen Computern in der Umgebung geöffnet ist.
  - Überprüfen Sie die gesamte Netzwerkkonfiguration (Firewalls), da diese die Kommunikation mit den relevanten Ports verhindern kann.
- Reverse-DNS:
  - Achten Sie darauf, dass der Sensor den DNS-Server erreichen kann und dass Reverse-Lookup-Zonen aktiviert sind.

## <a name="see-also"></a>Weitere Informationen

- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](prerequisites.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
