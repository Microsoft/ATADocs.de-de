---
title: Tutorial zum Untersuchen eines Benutzers mit Azure ATP
d|Description: This article explains how to user Azure ATP security alerts to investigate a suspicious user.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 09/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2bec6fbb12d78bbfd8dd04046f63df267391b1d1
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2020
ms.locfileid: "79413416"
---
# <a name="tutorial-investigate-a-user"></a>Tutorial: Untersuchen eines Benutzers

> [!NOTE]
> Die auf dieser Seite erläuterten Azure ATP-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

Azure ATP-Beweise für Warnungen und Lateral Movement-Pfade zeigen klar an, wenn Benutzer verdächtige Aktivitäten durchgeführt haben oder Anzeichen dafür vorhanden sind, dass ihre Konten kompromittiert worden sind. In diesem Tutorial verwenden Sie die Untersuchungsempfehlungen dazu, das Risiko für Ihre Organisation zu ermitteln, Abhilfemaßnahmen zu bestimmen und festzulegen, wie ähnliche Angriffe in der Zukunft am besten verhindert werden können.  

> [!div class="checklist"]
> * Sammeln Sie Informationen zum Benutzer.
> * Untersuchen Sie vom Benutzer durchgeführte Aktivitäten.
> * Untersuchen Sie die Ressourcen, auf die der Benutzer zugegriffen hat.
> * Untersuchen Sie Lateral Movement-Pfade.

## <a name="recommended-investigation-steps-for-suspicious-users"></a>Empfohlene Untersuchungsschritte für verdächtige Benutzer

Überprüfen und untersuchen Sie das Benutzerprofil auf die folgenden Details und Aktivitäten:

1. Wer ist der [Benutzer](entity-profiles.md)?
     1. Ist der Benutzer ein [sensibler Benutzer](sensitive-accounts.md) (z. B. Administrator oder auf einer Watchlist o.ä.)?  
     2. Was ist seine Rolle innerhalb der Organisation?
     3. Ist er in der Organisationsstruktur wichtig?

2. Zu [untersuchende](investigate-entity.md) verdächtige Aktivitäten:
     1. Hat der Benutzer weitere Warnungen in Azure ATP oder in anderen Sicherheitstools wie Windows Defender ATP, Azure Security Center und/oder Microsoft CAS geöffnet?
     2. Hatte der Benutzer fehlgeschlagene Anmeldungsversuche?
     3. Auf welche Ressourcen hat der Benutzer zugegriffen?  
     4. Hat der Benutzer auf wertvolle Ressourcen zugegriffen?  
     5. Hatte der Benutzer Zugriffsrechte für die Ressourcen, auf die er zugegriffen hat?  
     6. Auf welchen Computern hat sich der Benutzer angemeldet? 
     7. Hätte der Benutzer sich auf diesen Computern anmelden dürfen?
     8. Ist ein [Lateral Movement-Pfad](use-case-lateral-movement-path.md) (LMP) zwischen dem Benutzer und einem sensiblen Benutzer vorhanden?


## <a name="see-also"></a>Weitere Informationen

- [Untersuchen eines Computers](investigate-a-computer.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Warnungen zu Reconnaissance](atp-reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](atp-compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](atp-lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](atp-domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](atp-exfiltration-alerts.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
