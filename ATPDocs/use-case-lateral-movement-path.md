---
title: Grundlegendes zu und Verwenden von Lateral-Movement-Pfaden mit Azure ATP | Microsoft-Dokumentation
description: Dieser Artikel beschreibt die potenziellen Lateral Movement-Pfade (LMPs) von Azure Advanced Threat Protection (ATP).
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0bc0272b51c0a8982d1c5134c68fba561d54db9b
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2020
ms.locfileid: "75905926"
---
# <a name="azure-atp-lateral-movement-paths-lmps"></a>Azure ATP-Lateral Movement-Pfade (LMPs) 

> [!NOTE]
> Die auf dieser Seite erläuterten Azure ATP-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

Lateral Movement bedeutet, dass ein Angreifer nicht sensible Konten benutzt, um über Ihr Netzwerk hinweg Zugriff auf sensible Konten zu erhalten. Lateral Movement wird von Angreifern genutzt, um Zugriff auf sensible Konten und Computer in Ihrem Netzwerk zu erhalten, die gespeicherte Anmeldeinformationen für Konten, Gruppen und Computer gemeinsam nutzen. Sobald ein Angreifer erfolgreich Lateral Moves in Richtung Ihrer wichtigsten Ziele ausführt, kann er das nutzen und sich Zugriff auf Ihre Domänencontroller verschaffen. Lateral Movement-Angriffe werden mithilfe vieler unterschiedlicher Methoden durchgeführt, die im [Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md) beschrieben werden.

Eine wichtige Komponente der Azure ATP-Sicherheitseinblicke sind Lateral Movement-Pfade oder LMPs. Azure ATP-LMPs sind visuelle Hilfsmittel, mit denen Sie genau verstehen und bestimmten können, wie Angreifer sich seitlich in Ihrem Netzwerk bewegen können. Der Zweck von Lateral Movements innerhalb der Cyber Kill Chain ist es, über nicht sensible Konten Zugriff auf Ihre sensiblen Konten zu erhalten. Das Kompromittieren Ihrer sensiblen Konten bringt die Angreifer ihrem Hauptziel, dem Kontrollieren der Domäne, einen Schritt näher. Um zu verhindern, dass diese Angriffe Erfolg haben, stellen Ihnen Azure ATP-LMPs einfach zu interpretierende, direkte visuelle Hilfsmittel für Ihre sensiblen Konten zur Verfügung. LMPs helfen Ihnen dabei, diese Risiken für die Zukunft zu verringern und zu verhindern, und blockieren den Zugriff für Angreifer, bevor diese die Domäne einnehmen können.

![Azure ATP-Lateral Movement-Pfad (LMP)](./media/atp-lmp.png)

Lateral Movement-Angriffe können auf unterschiedliche Weise durchgeführt werden. Einige der von Angreifern am häufigsten verwendeten Methoden sind der Diebstahl von Anmeldeinformationen und Pass-the-Ticket-Angriffe. Bei beiden Methoden werden Ihre nicht sensiblen Konten von den Angreifern für Seitenangriffe genutzt, indem sie nicht sensible Computer ausnutzen, die Anmeldeinformationen gemeinsam mit Konten, Endpunktgruppen und Computern mit sensiblen Konten verwenden.

## <a name="where-can-i-find-azure-atp-lmps"></a>Wo kann ich Azure ATP-LMPs finden?

Jeder Computer oder jedes Benutzerprofil, das sich laut den Azure ATP-Ermittlungen in einem LMP befindet, besitzt eine Registerkarte **Lateral Movement-Pfade**. Computer und Profile, die keine Registerkarte vorweisen, wurden noch nie innerhalb einer potenziellen LMP ermittelt. 

![Registerkarte „Azure ATP Lateral Movement Path (LMP)“ (Azure ATP-Lateral Movement-Pfad (LMP))](./media/lateral-movement-path-tab.png)

Der LMP für jede Entität bietet verschiedene Informationen abhängig von der Vertraulichkeit der Entität: 
- Sensible Benutzer: potenzielle LMP(s), die zu diesem Benutzer führen, werden angezeigt.
- Nicht sensible Benutzer und Computer: mit der Entität verknüpfte potenzielle LMP(s) werden angezeigt. <br>

Wenn Sie auf die Registerkarte klicken, werden immer die neuesten ermittelten LMP angezeigt. Jeder potenzielle LMP wird nach der Ermittlung 48 Stunden lang gespeichert. Der LMP-Verlauf ist verfügbar. Klicken Sie auf **Anzeigen einer anderen Datumsangabe**, um ältere LMPs, die in der Vergangenheit ermittelt wurden, anzuzeigen. 

![Registerkarte „Azure ATP-Lateral Movement-Pfad (LMP)“](./media/atp-lmp-complete.png)

Ermitteln Sie, wann potenzielle LMPs identifiziert wurden und welche verwandten Entitäten möglicherweise betroffen sind. 

## <a name="lmp-discovery"></a>LMP-Ermittlung

Auf der Registerkarte „Aktivitäten“ werden Warnungen angezeigt, wenn neue potenzieller LMP erkannt wurden:
- Sensible Benutzer: Wenn ein neuer Pfad zu einem sensiblen Benutzer identifiziert wird

![Azure ATP: Lateral Movement-Pfad (LMP), Als sensibel identifiziert](./media/atp-lmp-activities.png)

- Nicht sensible Benutzer und Computer: Wenn diese Entität in einem potenziellen LMP, der zu einem sensiblen Benutzer führt, identifiziert wird.

![Azure ATP: Lateral Movement-Pfad (LMP), Als nicht sensibel identifiziert](./media/atp-lateral-non-sensitive.png)

## <a name="lmp-related-entities"></a>LMP-verwandte Entitäten
LMP können Sie jetzt direkt bei Ihrem Untersuchungsprozess unterstützen. Azure ATP-Beweislisten für Sicherheitswarnungen geben die verwandten Entitäten an, die an jedem potenziellen Lateral Movement-Pfad beteiligt sind. Die Beweislisten können Ihrem Sicherheitsreaktionsteam direkt helfen, die Wichtigkeit der Sicherheitswarnung und/oder der Untersuchung der verwandten Entitäten zu senken oder zu erhöhen. Wenn z.B. eine Pass-the-Ticket-Warnung ausgegeben wird, sind der Quellcomputer, der kompromittierte Benutzer und der Zielcomputer, von dem aus das gestohlene Ticket benutzt wurde, alle Teil des potenziellen Lateral Movement-Pfads, der zu einem sensiblen Benutzer führt. Das Vorhandensein des identifizierten LMP macht das Untersuchen der Warnung und das Überwachen des verdächtigen Benutzers umso wichtiger, um den Angreifer an weiteren Seitenangriffe zu hindern. Nachverfolgbare Beweise werden in LMPs zur Verfügung gestellt, um Ihnen ein leichteres und schnelleres Stoppen von Angreifern zu ermöglichen, die sich durch Ihr Netzwerk bewegen. 

## <a name="lateral-movement-paths-to-sensitive-accounts-report"></a>Bericht zu Lateral Movement-Pfaden zu sensiblen Konten 
LMP-Daten sind auch im [Bericht zu Lateral Movement-Pfaden zu sensiblen Konten](investigate-lateral-movement-path.md) verfügbar. In diesem Bericht werden die sensiblen Konten auf,gelistet die über Lateral Movement offen gelegt wurden, und umfasst Pfade, die manuell für einen bestimmten Zeitraum ausgewählt wurden oder im Zeitraum für geplante Berichte enthalten sind.  Passen Sie den enthaltenen Datumsbereich über die Kalenderauswahl an. 

## <a name="preventative-best-practices"></a>Empfohlene präventive Methoden
Mit Sicherheitserkenntnissen ist es nie zu spät, den nächsten Angriff zu verhindern und Schaden zu beheben. Aus diesem Grund bietet das Untersuchen eines Angriffs, selbst wenn die Domäne bereits eingenommen wurde, ein anderes, jedoch wichtiges Beispiel. In der Regel ist Ihr Domänencontroller während der Untersuchung einer Sicherheitswarnung möglicherweise bereits gefährdet, wie z.B. der Codeausführungen von Remotestandorten, wenn die Warnung ein richtig positives Ereignis ist. Aber LMPs informieren Sie darüber, wo sich der Angreifer Berechtigungen verschafft und welchen Pfad in Ihrem Netzwerk er benutzt hat. Auf diese Weise können LMPs auch wichtige Einblicke in mögliche Ansätze zum Abwehren oder Abschwächen derartiger Angriffe geben.  

- Sie können Lateral Movement-Angriffe am besten verhindern, indem Sie sicherstellen, dass sensible Benutzer ihre Administratoranmeldeinformationen nur dann verwenden, wenn sie sich an gehärteten Computern anmelden. Überprüfen Sie in diesem Beispiel, ob der Administrator im Pfad tatsächlich Zugriff auf den gemeinsam genutzten Computer benötigt. Wenn sie keinen Zugriff benötigen, stellen Sie sicher, dass Sie sich bei dem gemeinsam genutzten Computer mit einem anderen Benutzernamen und Kennwort und nicht mit den Anmeldeinformationen des Administrators anmelden.

- Stellen Sie sicher, dass Ihre Benutzer wirklich Administratorrechte benötigen. Überprüfen Sie im Beispiel, ob alle Benutzer in der geteilten Gruppe tatsächlich Administratorrechte auf dem bereitgestellten Computer erfordern.

- Stellen Sie sicher, dass Personen nur Zugriff auf die Ressourcen haben, die sie benötigen. Im Beispiel verstärkt Ron Harper erheblich Nick Cowleys Reichweite. Ist es erforderlich, dass Ron Harper Mitglied in der Gruppe ist? Können Untergruppen erstellt werden, mit denen sich die Anfälligkeit für Lateral Movement minimieren lässt?

**Tipp**: Wenn Sie keine potenzielle Lateral Movement-Pfadaktivität für eine Entität in den letzten 48 Stunden ermitteln können, klicken Sie auf **Ein anderes Datum anzeigen**, und suchen Sie nach vorherigen potenziellen Lateral Movement-Pfaden. Der **Bericht „LMP zu sensiblen Benutzern“** ist immer verfügbar, wenn LMPs ermittelt wurden und bietet Ihnen Informationen über identifizierte potenzielle Lateral Movement-Pfade zu sensiblen Benutzern. 

**Tipp**: Unter [Konfigurieren von SAM-R](install-atp-step8-samr.md) finden Sie Informationen darüber, wie Sie Ihre Clients und Server so einrichten, dass Azure ATP das Ausführen von den SAM-R-Vorgängen erlaubt wird, die für die Erkennung von Lateral Movement-Pfaden erforderlich sind.


## <a name="investigating-lmps"></a>Untersuchen von LMPs
Anleitungen zum Identifizieren und Untersuchen mit Azure ATP-Lateral Movement-Pfaden finden Sie unter [Untersuchen von Lateral Movement-Pfaden](investigate-lateral-movement-path.md).


## <a name="see-also"></a>Weitere Informationen
- [Untersuchen von Azure ATP-LMPs](investigate-lateral-movement-path.md)
- [Konfigurieren von Azure ATP für das Ausführen von Remoteaufrufen an SAM](install-atp-step8-samr.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
