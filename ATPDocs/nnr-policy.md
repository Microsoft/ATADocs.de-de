---
title: Auflösung von Microsoft Defender für Identitäts Netzwerknamen
description: Dieser Artikel bietet eine Übersicht über die erweiterten Funktionen und Verwendungsmöglichkeiten der Netzwerknamen Auflösung von Microsoft Defender für die Identität.
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
ms.openlocfilehash: 9b9688031ea9916a09b8beaa2ce5c67633fd935f
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847240"
---
# <a name="what-is-network-name-resolution"></a>Was ist Netzwerknamensauflösung?

Network Name Resolution (NNR) ist eine Hauptkomponente der-  [!INCLUDE [Product long](includes/product-long.md)] Funktionalität. [!INCLUDE [Product short](includes/product-short.md)] erfasst Aktivitäten auf der Grundlage von Netzwerk Datenverkehr, Windows-Ereignissen und etw-diese Aktivitäten enthalten normalerweise IP-Daten.

Die Verwendung von NNR [!INCLUDE [Product short](includes/product-short.md)] kann zwischen rohaktivitäten (die IP-Adressen enthalten) und den relevanten Computern, die an den einzelnen Aktivitäten beteiligt sind, korrelieren. Basierend auf den unformatierten Aktivitäten, [!INCLUDE [Product short](includes/product-short.md)] Profil Entitäten, einschließlich Computern, generiert Sicherheitswarnungen für verdächtige Aktivitäten.

Zum Auflösen von IP-Adressen in Computernamen suchen [!INCLUDE [Product short](includes/product-short.md)]-Sensoren die IP-Adressen mithilfe der folgenden Methoden:

- NTLM über RPC (TCP-Port 135)
- NetBIOS (UDP-Port 137)
- RDP (TCP-Port 3389): nur das erste Paket von **ClientHello**
- Abfragen des DNS-Servers mittels Reverse-DNS-Lookup der IP-Adresse (UDP 53)

Um die besten Ergebnisse zu erzielen, sollten alle Methoden verwendet werden. Wenn dies nicht möglich ist, sollten Sie die DNS-Suchmethode und mindestens eine der anderen Methoden verwenden.

> [!NOTE]
> An keinem dieser Ports erfolgt eine Authentifizierung.

[!INCLUDE [Product short](includes/product-short.md)] wertet das Betriebssystem des Geräts basierend auf dem Netzwerk Datenverkehr aus und legt es fest. Nach dem Abrufen des Computer namens prüft der [!INCLUDE [Product short](includes/product-short.md)] Sensor Active Directory und verwendet TCP-Fingerabdrücke, um festzustellen, ob ein korreliertes Computer Objekt mit demselben Computernamen vorhanden ist. Mithilfe von TCP-Fingerabdrücken können nicht registrierte und Nicht-Windows-Geräte identifiziert werden, sodass der Untersuchungsprozess vereinfacht wird.
Wenn der [!INCLUDE [Product short](includes/product-short.md)] Sensor die Korrelation findet, ordnet der Sensor dem Computer Objekt die IP-Adresse zu.

In Fällen, in denen kein Name abgerufen wird, wird ein **nicht aufgelöstes Computerprofil nach IP-Adresse** mit der IP-Adresse und der relevanten erkannten Aktivität erstellt.

![Nicht aufgelöstes Computerprofil](media/unresolved-computer-profile.png)

NNR-Daten spielen beim Erkennen der folgenden Bedrohungen eine entscheidende Rolle:

- Suspected identity theft (pass-the-ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket))
- Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))
- Network mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))

Um die Fähigkeit zu verbessern, festzustellen, ob es sich bei einer Warnung um ein **richtig positives (TP)** oder ein **falsches positives (FP)** handelt, [!INCLUDE [Product short](includes/product-short.md)] schließt den Grad der Sicherheit der Computer Benennung in den Beweis der einzelnen Sicherheitswarnungen ein.

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
|NTLM über RPC *|TCP|135|Alle Geräte im Netzwerk|Eingehend|
|NetBIOS-|UDP|137|Alle Geräte im Netzwerk|Eingehend|
|RDP|TCP|3389|Alle Geräte im Netzwerk|Eingehend|
|DNS|UDP|53|Domänencontroller|Ausgehend|

\* Eine dieser Methoden ist erforderlich, aber es wird empfohlen, alle zu verwenden.

Um sicherzustellen, dass [!INCLUDE [Product short](includes/product-short.md)] im Idealfall funktioniert und die Umgebung ordnungsgemäß konfiguriert ist, [!INCLUDE [Product short](includes/product-short.md)] prüft den Auflösungs Status der einzelnen Sensoren und gibt eine Integritäts Warnung pro Methode aus, um eine Liste der [!INCLUDE [Product short](includes/product-short.md)] Sensoren mit niedriger Erfolgsrate der aktiven Namensauflösung mit jeder Methode bereitzustellen.

> [!NOTE]
> Öffnen Sie einen Support-Support, um eine optionale NNR-Methode in [!INCLUDE [Product short](includes/product-short.md)] zu deaktivieren, die den Anforderungen Ihrer Umgebung entspricht.

Jede Integritäts Warnung enthält spezifische Details der Methode, der Sensoren, der problematischen Richtlinie und der Konfigurations Empfehlungen.

![Warnung bei geringer Erfolgsquote der Netzwerknamensauflösung (NNR)](media/nnr-success-rate.png)

### <a name="configuration-recommendations"></a>Konfigurationsempfehlungen

- NTLM über RPC:
  - Überprüfen Sie, ob der TCP-Port 135 für die eingehende Kommunikation von [!INCLUDE [Product short](includes/product-short.md)] Sensoren auf allen Computern in der Umgebung geöffnet ist.
  - Überprüfen Sie die gesamte Netzwerkkonfiguration (Firewalls), da diese die Kommunikation mit den relevanten Ports verhindern kann.

- NetBIOS:
  - Überprüfen Sie, ob der UDP-Port 137 für die eingehende Kommunikation von [!INCLUDE [Product short](includes/product-short.md)] Sensoren auf allen Computern in der Umgebung geöffnet ist.
  - Überprüfen Sie die gesamte Netzwerkkonfiguration (Firewalls), da diese die Kommunikation mit den relevanten Ports verhindern kann.
- RDP:
  - Überprüfen Sie, ob der TCP-Port 3389 für die eingehende Kommunikation von [!INCLUDE [Product short](includes/product-short.md)] Sensoren auf allen Computern in der Umgebung geöffnet ist.
  - Überprüfen Sie die gesamte Netzwerkkonfiguration (Firewalls), da diese die Kommunikation mit den relevanten Ports verhindern kann.
- Reverse-DNS:
  - Achten Sie darauf, dass der Sensor den DNS-Server erreichen kann und dass Reverse-Lookup-Zonen aktiviert sind.

## <a name="see-also"></a>Weitere Informationen

- [Voraussetzungen für [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
