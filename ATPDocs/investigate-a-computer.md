---
title: Tutorial für die Untersuchung von Computern mit Microsoft Defender for Identity
description: In diesem Artikel wird erläutert, wie Sicherheitswarnungen von Microsoft Defender for Identity zur Untersuchung eines verdächtigen Computers verwendet werden.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 72a7f92d6fd77842b8fe34866d8757df8bc9203e
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847682"
---
# <a name="tutorial-investigate-a-computer"></a>Tutorial: Untersuchen eines Computers

> [!NOTE]
> Die auf dieser Seite erläuterten [!INCLUDE [Product long](includes/product-long.md)]-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

Ein Beweis für Warnungen in [!INCLUDE [Product long](includes/product-long.md)] zeigt eindeutig an, wenn Computer von verdächtigen Aktivitäten betroffen sind, oder wenn es Anzeichen dafür gibt, dass ein Computer gefährdet ist. In diesem Tutorial verwenden Sie die Untersuchungsempfehlungen dazu, das Risiko für Ihre Organisation zu ermitteln, Abhilfemaßnahmen zu bestimmen und festzulegen, wie ähnliche Angriffe in der Zukunft am besten verhindert werden können.  

> [!div class="checklist"]
>
> - Überprüfen Sie den Computer des angemeldeten Benutzers.
> - Überprüfen Sie, ob der Benutzer normalerweise auf die entsprechenden Computer zugreift.
> - Untersuchen Sie verdächtige Aktivitäten auf dem Computer.
> - Ermitteln Sie, ob zur gleichen Zeit andere Warnungen aufgetreten sind.

## <a name="investigation-steps-for-suspicious-computers"></a>Untersuchungsschritte für verdächtige Computer

Klicken Sie auf den in der Warnung genannten Computer, den Sie untersuchen möchten, um auf die Profilseite des Computers zuzugreifen. Als Unterstützung für Ihre Untersuchung sind in dem Beweis für Warnungen alle Computer (und [Benutzer](investigate-a-user.md)) aufgelistet, die mit den verdächtigen Aktivitäten in Verbindung stehen.

Überprüfen und untersuchen Sie das Computerprofil auf die folgenden Details und Aktivitäten:

- Was ist zum Zeitpunkt der verdächtigen Aktivität geschehen?  
    1. Welcher [Benutzer](investigate-a-user.md) war an dem Computer angemeldet?
    1. Meldet sich dieser Benutzer normalerweise an der Quelle oder am Zielcomputer an, oder greift er darauf zu?
    1. Auf welche Ressourcen ist zugegriffen worden? Durch welche Benutzer?
      - Wenn auf Ressourcen zugegriffen worden ist, hat es sich um wertvolle Ressourcen gehandelt?
    1. Hätte der Benutzer Zugriff auf diese Ressourcen haben dürfen?
    1. Hat der [Benutzer](investigate-a-user.md), der auf den Computer zugegriffen hat, weitere verdächtige Aktivitäten ausgeführt?

- Weitere zu untersuchende verdächtige Aktivitäten:
    1. Wurden ungefähr gleichzeitig mit dieser Warnung noch weitere Warnungen in [!INCLUDE [Product short](includes/product-short.md)] oder in anderen Sicherheitstools wie Microsoft Defender für Endpunkt, Azure Security Center und/oder Microsoft CAS geöffnet?
    1. Hat es Anmeldefehler gegeben?

- Wenn die Microsoft Defender für Endpunkt-Integration aktiviert ist, klicken Sie auf den Microsoft Defender für Endpunkt-Badge, um den Computer genauer zu untersuchen. In Microsoft Defender für Endpunkt können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind.
    - Sind neue Programme bereitgestellt oder installiert worden?

## <a name="next-steps"></a>Nächste Schritte

- [Untersuchen eines Benutzers](investigate-a-user.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Warnungen zu Reconnaissance](reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](exfiltration-alerts.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
