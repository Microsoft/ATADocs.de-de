---
title: Tutorial für die Benutzeruntersuchung mit Microsoft Defender for Identity
description: In diesem Artikel wird erläutert, wie Sicherheitswarnungen von Microsoft Defender for Identity zur Untersuchung eines verdächtigen Benutzers verwendet werden.
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: c9d3cb67ff4eeae0e1f4a0808751d96c67cf326e
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96542820"
---
# <a name="tutorial-investigate-a-user"></a>Tutorial: Untersuchen eines Benutzers

> [!NOTE]
> Die auf dieser Seite erläuterten [!INCLUDE [Product long](includes/product-long.md)]-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

[!INCLUDE [Product long](includes/product-long.md)]-Beweise für Warnungen und Lateral Movement-Pfade zeigen klar an, wenn Benutzer verdächtige Aktivitäten durchgeführt haben oder Anzeichen dafür vorliegen, dass ihre Konten kompromittiert worden sind. In diesem Tutorial verwenden Sie die Untersuchungsempfehlungen dazu, das Risiko für Ihre Organisation zu ermitteln, Abhilfemaßnahmen zu bestimmen und festzulegen, wie ähnliche Angriffe in der Zukunft am besten verhindert werden können.

> [!div class="checklist"]
>
> - Sammeln Sie Informationen zum Benutzer.
> - Untersuchen Sie vom Benutzer durchgeführte Aktivitäten.
> - Untersuchen Sie die Ressourcen, auf die der Benutzer zugegriffen hat.
> - Untersuchen Sie Lateral Movement-Pfade.

## <a name="recommended-investigation-steps-for-suspicious-users"></a>Empfohlene Untersuchungsschritte für verdächtige Benutzer

Überprüfen und untersuchen Sie das Benutzerprofil auf die folgenden Details und Aktivitäten:

1. Wer ist der [Benutzer](entity-profiles.md)?
    1. Ist der Benutzer ein [sensibler Benutzer](sensitive-accounts.md) (z. B. Administrator oder auf einer Watchlist o.ä.)?
    1. Was ist seine Rolle innerhalb der Organisation?
    1. Ist er in der Organisationsstruktur wichtig?

1. Zu [untersuchende](investigate-entity.md) verdächtige Aktivitäten:
    1. Liegen andere offene Warnungen für den Benutzer in [!INCLUDE [Product short](includes/product-short.md)] oder anderen Sicherheitstools wie Microsoft Defender für Endpunkt, Azure Security Center und/oder Microsoft CAS vor?
    1. Hatte der Benutzer fehlgeschlagene Anmeldungsversuche?
    1. Auf welche Ressourcen hat der Benutzer zugegriffen?
    1. Hat der Benutzer auf wertvolle Ressourcen zugegriffen?
    1. Hatte der Benutzer Zugriffsrechte für die Ressourcen, auf die er zugegriffen hat?
    1. Auf welchen Computern hat sich der Benutzer angemeldet?
    1. Hätte der Benutzer sich auf diesen Computern anmelden dürfen?
    1. Ist ein [Lateral Movement-Pfad](use-case-lateral-movement-path.md) (LMP) zwischen dem Benutzer und einem sensiblen Benutzer vorhanden?

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen eines Computers](investigate-a-computer.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Warnungen zu Reconnaissance](reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](exfiltration-alerts.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
