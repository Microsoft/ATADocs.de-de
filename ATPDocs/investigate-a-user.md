---
title: Untersuchen eines Benutzers mit Azure ATP| Microsoft-Dokumentation
d|Description: This article explains how to user Azure ATP security alerts to investigate a suspicious user.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/14/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 126653dd2831e0e3dbd9c777d84d32b1c2e74bd9
ms.sourcegitcommit: 1ee052c4c6b04b290e2d5384c24b65a108b1f1f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2019
ms.locfileid: "54253400"
---
# <a name="tutorial-investigate-a-user"></a>Tutorial: Untersuchen eines Benutzers

Azure ATP-Beweise für Warnungen und Lateral Movement-Pfade zeigen klar an, wenn Benutzer verdächtige Aktivitäten durchgeführt haben oder Anzeichen dafür vorhanden sind, dass ihre Konten kompromittiert worden sind. Verwenden Sie die Untersuchungsempfehlungen dazu, das Risiko für Ihre Organisation zu ermitteln, Abhilfemaßnahmen zu bestimmen und festzulegen, wie ähnliche Angriffe in der Zukunft am besten verhindert werden können.  

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
