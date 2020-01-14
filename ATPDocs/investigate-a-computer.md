---
title: 'Tutorial: Untersuchen eines Computers mit Azure ATP| Microsoft-Dokumentation'
d|Description: This article explains how to use Azure ATP security alerts to investigate a suspicious computer.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 09/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 93e8b62b9f7f1df1c0860345804a204ee01c11a0
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2020
ms.locfileid: "75906431"
---
# <a name="tutorial-investigate-a-computer"></a>Tutorial: Untersuchen eines Computers

> [!NOTE]
> Die auf dieser Seite erläuterten Azure ATP-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

Ein Beweis für Warnungen in Azure ATP zeigt eindeutig an, wenn Computer von verdächtigen Aktivitäten betroffen sind, oder wenn es Anzeichen dafür gibt, dass ein Computer gefährdet ist. In diesem Tutorial verwenden Sie die Untersuchungsempfehlungen dazu, das Risiko für Ihre Organisation zu ermitteln, Abhilfemaßnahmen zu bestimmen und festzulegen, wie ähnliche Angriffe in der Zukunft am besten verhindert werden können.  

> [!div class="checklist"]
> * Überprüfen Sie den Computer des angemeldeten Benutzers.
> * Überprüfen Sie, ob der Benutzer normalerweise auf die entsprechenden Computer zugreift.
> * Untersuchen Sie verdächtige Aktivitäten auf dem Computer.
> * Ermitteln Sie, ob zur gleichen Zeit andere Warnungen aufgetreten sind.


## <a name="investigation-steps-for-suspicious-computers"></a>Untersuchungsschritte für verdächtige Computer

Klicken Sie auf den in der Warnung genannten Computer, den Sie untersuchen möchten, um auf die Profilseite des Computers zuzugreifen. Als Unterstützung für Ihre Untersuchung sind in dem Beweis für Warnungen alle Computer (und [Benutzer](investigate-a-user.md)) aufgelistet, die mit den verdächtigen Aktivitäten in Verbindung stehen.

Überprüfen und untersuchen Sie das Computerprofil auf die folgenden Details und Aktivitäten:

- Was ist zum Zeitpunkt der verdächtigen Aktivität geschehen?  
  1. Welcher [Benutzer](investigate-a-user.md) war an dem Computer angemeldet?
  2. Meldet sich dieser Benutzer normalerweise an der Quelle oder am Zielcomputer an, oder greift er darauf zu?
  3. Auf welche Ressourcen ist zugegriffen worden? Durch welche Benutzer?
      - Wenn auf Ressourcen zugegriffen worden ist, hat es sich um wertvolle Ressourcen gehandelt?
  4. Hätte der Benutzer Zugriff auf diese Ressourcen haben dürfen?
  5. Hat der [Benutzer](investigate-a-user.md), der auf den Computer zugegriffen hat, weitere verdächtige Aktivitäten ausgeführt?

- Weitere zu untersuchende verdächtige Aktivitäten:
    1. Waren ungefähr gleichzeitig mit dieser Warnung noch weitere Warnungen in Azure ATP oder in anderen Sicherheitstools wie Windows Defender ATP, Azure Security Center und/oder Microsoft CAS geöffnet?
    2. Hat es Anmeldefehler gegeben?


- Wenn die Windows Defender ATP-Integration aktiviert ist, klicken Sie auf das Windows Defender ATP-Badge, um den Computer genauer zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind.
    1. Sind neue Programme bereitgestellt oder installiert worden?

## <a name="next-steps"></a>Nächste Schritte

- [Untersuchen eines Benutzers](investigate-a-user.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Warnungen zu Reconnaissance](atp-reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](atp-compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](atp-lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](atp-domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](atp-exfiltration-alerts.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
