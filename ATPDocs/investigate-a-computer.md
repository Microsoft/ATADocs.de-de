---
title: 'Tutorial: Untersuchen eines Computers mit Azure ATP| Microsoft-Dokumentation'
d|Description: This article explains how to use Azure ATP security alerts to investigate a suspicious computer.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/14/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3c707376635facd0fe9ba8e3c3f32f36f5a71c25
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2019
ms.locfileid: "54839545"
---
# <a name="tutorial-investigate-a-computer"></a>Tutorial: Untersuchen eines Computers

Ein Beweis für Warnungen in Azure ATP zeigt eindeutig an, wenn Computer von verdächtigen Aktivitäten betroffen sind, oder wenn es Anzeichen dafür gibt, dass ein Computer gefährdet ist. Verwenden Sie die Untersuchungsempfehlungen dazu, das Risiko für Ihre Organisation zu ermitteln, Abhilfemaßnahmen zu bestimmen und festzulegen, wie ähnliche Angriffe in der Zukunft am besten verhindert werden können.  

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

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen eines Benutzers](investigate-a-user.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Warnungen zu Reconnaissance](atp-reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](atp-compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](atp-lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](atp-domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](atp-exfiltration-alerts.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
